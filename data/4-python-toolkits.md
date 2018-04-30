## Python Toolkits

#### Pyvenv

使用pyvenv来管理python环境，可以设置多个版本的python
以安装python3的环境为例

Mac osx
```
$brew install python3.6.5
$cd ~/workspace
$python3.6 -m venv py36
$cd py36
# 启动环境
$source bin/activate
(py36)$pip --version

# 关闭环境
(py36)$deactivate
$pip --version
```

Linux ubuntu
```
$sudo apt-get update
$sudo apt-get -y install python3.6
$cd ~/workspace
$python3.6 -m venv py36
$cd py36
# 启动环境
$source bin/activate
(py36)$pip --version
```
