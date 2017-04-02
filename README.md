# Google Inception on a Raspberry Pi 3

# Cheat Sheet

## Installation

**For the Tensorflow installation variant use the master branch: [https://github.com/tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** 

### For Python 2.7

#### Installation
```
sudo apt-get update
sudo apt-get install python-pip python-dev
wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.0.0/tensorflow-1.0.0-cp27-none-linux_armv7l.whl
sudo pip install tensorflow-1.0.0-cp27-none-linux_armv7l.whl
sudo pip uninstall mock
sudo pip install mock
```

#### Traning
```
sudo python tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/home/pi/tf_files/bottlenecks \
--how_many_training_steps 500 \
--model_dir=/home/pi/tf_files/inception \
--output_graph=/home/pi/tf_files/retrained_graph.pb \
--output_labels=/home/pi/tf_files/retrained_labels.txt \
--image_dir /home/pi/tf_files/lego-pictures
```

#### Classify
```
python label_image.py /tf_files/lego-pictures/person/IMG_0008.jpg
```

scp lego-pictures.zip pi@192.168.0.17:/home/pi/tf_files

sudo chmod -R 777 tf_files

## Docker

### Dockerfile

**For the Docker variant use the branch r0.11: [https://github.com/tensorflow/tensorflow/tree/r0.11](https://github.com/tensorflow/tensorflow/tree/r0.11)**

```
FROM romilly/rpi-docker-tensorflow
COPY . /tensorflow
```

```
sudo docker build -t raspberry-inception .
sudo docker images
sudo docker run raspberry-inception
sudo docker ps
docker exec -it 01a31608d07f bash
sudo docker run -it -v $HOME/tf_files:/tf_files raspberry-inception
```

cd tensorflow  
git checkout r0.11 

```
sudo python tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/tf_files/bottlenecks \
--how_many_training_steps 500 \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/retrained_graph.pb \
--output_labels=/tf_files/retrained_labels.txt \
--image_dir /tf_files/lego-pictures
```

```
python label_image.py /tf_files/lego-pictures/person/IMG_0008.jpg
```

# Resources
**Tensorflow on Raspberry Pi 3**
https://github.com/samjabrahams/tensorflow-on-raspberry-pi 

**Tensorflow on Raspberry Pi 3 over Docker**
https://hub.docker.com/r/romilly/rpi-docker-tensorflow/

**Tensorflow**
https://github.com/tensorflow/tensorflow/tree/r0.11