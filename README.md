# jetson nano AI
  jetson nano object detection

# Download python3-numpy
 $ cd<br/>
 $ sudo apt-get update<br/>
 $ sudo apt-get install git cmake libpython3-dev python3-numpy<br/>

# Download jetson-inference
 $ git clone --recursive https://github.com/dusty-nv/jetson-inference<br/>
 $ cd jetson-inference<br/>
 $ mkdir build<br/>
 $ cd build<br/>
 $ cmake ../<br/>
 $ make<br/>
 $ sudo make install<br/>
 $ sudo ldconfig<br/>

# Run docker
$ docker/run.sh <br/>
$ cd python/training/detection/ssd/data<br/>
$ mkdir electronics <br/>
Open another terminal <br/>
$ cd jetson-inference/python/training/detection/ssd/data/electronics<br/>
$ touch labels.txt<br/>

Open a text editor and edit the labels.txt file <br/>
add some labels <br/>
Phone<br/>
Ipad<br/>
Earbuds<br/>
Headset<br/>
Laptop<br/>
then save and exit the text editor<br/>

# Collect data
$ cd jetson-inference/python/training/detection/ssd <br/>

$ camera-capture /dev/video0 <br/>

(the video0 depends on your video feed)<br/>
Change dataset type to detection , Dataset path to ssd/data/electronics, Class labels to labels.txt, Then collect data for train, val, and test <br/>
Once have enough data, close the video window


# train model
$ python3 train_ssd.py -–dataset-type=voc –-data=data/electronics –-model-dir=models/electronics –-batch-size=2 --workers=1 –-epochs=5<br/>

$ python3 onnx_export.py –-model-dir=models/electronics <br/>


# test out the model 
$ detectnet –-model=models/electronics/ssd-mobilenet.onnx –-labels=models/electronics/labels.txt –-input-blob=input_0 –-output-cvg=scores –-output-bbox=boxes<br/>
