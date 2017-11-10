# Caffe Install Tutorial

1. 安装cuda
2. 下载cudnn并安装

## 安装一依赖库

```
$sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
$sudo apt-get install --no-install-recommends libboost-all-dev
$sudo apt-get install libopenblas-dev liblapack-dev libatlas-base-dev
$sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
$sudo apt-get install libcv-dev    # version 2.c opencv
```
## 下载caffe并安装

```
$wget https://github.com/BVLC/caffe/archive/1.0.tar.gz
$tar xzvf caffe-1.0.tar.gz
$cd caffe
$protoc src/caffe/proto/caffe.proto --cpp_out=.
$mkdir include/caffe/proto
$mv src/caffe/proto/caffe.pb.h include/caffe/proto
$cp Makefile.config.example Makefile.config
$make all
```
