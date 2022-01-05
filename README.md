# anti-crash-alarm
Alarm goes off if the driver of the car in not looking in front for more than 3 sec


Install opencv with SURF
Install cv2 with surf

sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python3-dev

# Move to Downloads folder
cd ~/Downloads
wget -O opencv.zip -c https://github.com/opencv/opencv/archive/3.4.2.zip
wget -O opencv_contrib.zip -c https://github.com/opencv/opencv_contrib/archive/3.4.2.zip
unzip opencv.zip
unzip opencv_contrib.zip


conda activate regii

# Generate make files and install
cd opencv-3.4.2
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=~/miniconda3/envs/regii \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=~/Downloads/opencv_contrib-3.4.2/modules \
    -D PYTHON_EXECUTABLE=~/miniconda3/envs/regii/bin/python \
    -D BUILD_EXAMPLES=ON ..
make -j4
make install
ldconfig -n ~/miniconda3/envs/regii/lib

# Verify that it worked
python -c "import cv2; print(cv2.__version__)"

# Cleanup
cd ~/Downloads
rm opencv.zip opencv_contrib.zip
rm -rf opencv-3.4.2 opencv_contrib-3.4.2
cd
