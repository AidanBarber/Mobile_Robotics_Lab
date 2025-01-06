Autorace Packages
```shell
cd ~/catkin_ws/src/
git clone -b noetic https://github.com/ROBOTIS-GIT/turtlebot3_autorace_2020.git
cd ~/catkin_ws && catkin_make
```

Setup swapfile to prevent out of memory error
```
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

Dependencies
```shell
sudo apt-get update
sudo apt-get install build-essential cmake gcc g++ git unzip pkg-config
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libgtk2.0-dev libcanberra-gtk* libxvidcore-dev libx264-dev python3-dev python3-numpy python3-pip libtbb2 libtbb-dev libdc1394-22-dev libv4l-dev v4l-utils libopenblas-dev libatlas-base-dev libblas-dev liblapack-dev gfortran libhdf5-dev libprotobuf-dev libgoogle-glog-dev libgflags-dev protobuf-compiler
```

OpenCV Install
```shell
cd ~
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.5.0.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.5.0.zip

unzip opencv.zip
unzip opencv_contrib.zip

mv opencv-4.5.0 opencv
mv opencv_contrib-4.5.0 opencv_contrib
```

Setup Make file
```
cd opencv
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
  -D CMAKE_INSTALL_PREFIX=/usr/local \
  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
  -D ENABLE_NEON=ON \
  -D BUILD_TIFF=ON \
  -D WITH_FFMPEG=ON \
  -D WITH_GSTREAMER=ON \
  -D WITH_TBB=ON \
  -D BUILD_TBB=ON \
  -D BUILD_TESTS=OFF \
  -D WITH_EIGEN=OFF \
  -D WITH_V4L=ON \
  -D WITH_LIBV4L=ON \
  -D WITH_VTK=OFF \
  -D OPENCV_ENABLE_NONFREE=ON \
  -D INSTALL_C_EXAMPLES=OFF \
  -D INSTALL_PYTHON_EXAMPLES=OFF \
  -D BUILD_NEW_PYTHON_SUPPORT=ON \
  -D BUILD_opencv_python3=TRUE \
  -D OPENCV_GENERATE_PKGCONFIG=ON \
  -D BUILD_EXAMPLES=OFF ..
```

Make OpenCV (takes hours)
```shell
cd ~/opencv/build
make -j4
sudo make install
sudo ldconfig
make clean
sudo apt-get update
```


Turn off Raspberry Pi, take out the microSD card and edit the config.txt in system-boot section. add start_x=1 before the enable_uart=1 line.
```shell
sudo apt install ffmpeg
ffmpeg -f video4linux2 -s 640x480 -i /dev/video0 -ss 0:0:2 -frames 1 capture_test.jpg
```

Install additional dependent packages
```shell
sudo apt install ros-noetic-cv-camera
```
