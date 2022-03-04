# ffmpeg-rtp-streaming for jetson


```
sudo apt build-dep ffmpeg
```

if error

fix sources.list with vi

  :%s/# deb-src/deb-src/
  :wq

  sudo apt update


build &　install library

git clone https://github.com/jocover/jetson-ffmpeg.git
cd jetson-ffmpeg
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig

build ffmpeg & patch

git clone git://source.ffmpeg.org/ffmpeg.git -b release/4.2 --depth=1
cd ffmpeg
wget https://github.com/jocover/jetson-ffmpeg/raw/master/ffmpeg_nvmpi.patch
git apply ffmpeg_nvmpi.patch
./configure --enable-nvmpi
make -j4 2>&1 |tee make.log
sudo make install

test ffmpeg 1
which ffmpeg
>>>>/usr/local/bin/ffmpeg

test ffmpeg 2
ffmpeg -codecs |grep 264

if not working
sudo nano /etc/profile

add file end line

export FFMPEG_HOME=/usr/local/bin/ffmpeg
export PATH=$FFMPEG_HOME/bin:$PATH

source /etc/profile
