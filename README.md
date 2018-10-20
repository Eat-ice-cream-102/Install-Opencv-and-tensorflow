# Install-Opencv-and-tensorflow
Fast construct Environment for Opencv and tensorflow on Pi


雖然神經網路相關或高強度的訓練不適用在pi上，但我們還是可以盡量榨乾pi的性能(優化特定type的運算，全開樹莓派CPU4核)，
以下是針對這個為目的參數設定，須注意隨著版本的改變安裝或調整方式也有變化，我不確定這個方式會work到幾時，但目前可姑且用之。

https://www.theimpossiblecode.com/blog/build-faster-opencv-raspberry-pi3/
為了方便各位我也製作img檔，讓各位不必再浪費時間編譯安裝。
(可以mail或敲我跟我要，因為使用說明我還要跟各位說)

OS: 2018-06-27-raspbian-stretch.img

(自行下再安裝，並要自己開啟ssh、VNC、camera等功能)


PS:
1.
至於下面這個方式不是讓樹莓派能有最大效能的安裝方式(效能最優化安裝因為很耗時加上我們還用到tensorflow API也有步驟很耗時，我下面提供的方式傾向簡單快速為目標，最佳化的方式我已經製作成img檔)
2.
安裝的東西意義註解待補


pip install tensorflow

pip install picamera

pip install matplotlib

#sudo apt-get install libatlas-base-dev

pip install pillow

sudo pip install pillow lxml jupyter matplotlib cython

sudo apt-get install python-tk

sudo apt-get -y install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev

sudo apt-get -y install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev

sudo apt-get -y install libxvidcore-dev libx264-dev

sudo apt-get -y install qt4-dev-tools

pip install opencv-python

pip install opencv-contrib-python

sudo apt-get install libhdf5-dev

wget https://github.com/google/protobuf/releases/download/v3.5.1/protobuf-all-3.5.1.tar.gz

tar -zxvf protobuf-all-3.5.1.tar.gz

cd protobuf-3.5.1

./configure

make

make check

sudo make install

cd python

export LD_LIBRARY_PATH=../src/.libs

python setup.py build --cpp_implementation

python setup.py test --cpp_implementation

sudo python setup.py install --cpp_implementation

export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=cpp

export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION_VERSION=3

sudo ldconfig

protoc

sudo reboot now

mkdir tensorflowOB

cd tensorflowOB

git clone --recurse-submodules https://github.com/tensorflow/models.git

sudo nano ~/.bashrc

# Move to the end of the file, and on the last line, add:

export PYTHONPATH=$PYTHONPATH:/home/pi/tensorflowOB/models/research:/home/pi/tensorflowOB/models/research/slim

cd /home/pi/tensorflowOB/models/research

protoc object_detection/protos/*.proto --python_out=.

cd /home/pi/tensorflowOB/models/research/object_detection

#參考https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md

wget http://download.tensorflow.org/models/object_detection/ssdlite_mobilenet_v2_coco_2018_05_09.tar.gz

tar -xzvf ssdlite_mobilenet_v2_coco_2018_05_09.tar.gz
