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

## Troubleshoot


```
/usr/include/boost/property_tree/detail/json_parser_read.hpp: In constructor ‘boost::property_tree::json_parser::json_grammar<Ptree>::definition<Scanner>::definition(const boost::property_tree::json_parser::json_grammar<Ptree>&)’:
/usr/include/boost/property_tree/detail/json_parser_read.hpp:257:264: error: ‘type name’ declared as function returning an array
                 escape
                                                                                                                                                                                                                                                                        ^
/usr/include/boost/property_tree/detail/json_parser_read.hpp:257:264: error: ‘type name’ declared as function returning an array
make: *** [.build_release/cuda/src/caffe/layers/detection_output_layer.o] 错误 1
```
更新g++

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install -y software-properties-common  
sudo apt-get install -y gcc-5 g++-5
sudo rm /usr/bin/gcc
sudo ln -s /usr/bin/gcc-5 /usr/bin/gcc  
sudo rm /usr/bin/g++  
sudo ln -s /usr/bin/g++-5 /usr/bin/g++  
```
