# Caffe Install Tutorial

1. 安装cuda
2. 下载cudnn并安装

## 安装一依赖库

```
$sudo apt-get update
$sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev  libhdf5-serial-dev 
$sudo apt-get install -y --no-install-recommends libboost-all-dev protobuf-compiler
$sudo apt-get install -y libopenblas-dev liblapack-dev libatlas-base-dev
$sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev libopencv-dev
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
