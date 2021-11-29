# jetson nano AI
 jetson nano object detection

Download python3-numpy
sudo apt-get update
sudo apt-get install git cmake libpython3-dev python3-numpy

Download jetson-inference
git clone --recursive https://github.com/dusty-nv/jetson-inference
cd jetson-inference
mkdir build
cd build
cmake ../
make
sudo make install
sudo ldconfig
