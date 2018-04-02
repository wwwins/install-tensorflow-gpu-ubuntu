# install-tensorflow-gpu-ubuntu
Install tensorflow with gpu on ubuntu 16.04
- Ubuntu 16.04 LTS
- Python 3.5
- cuda 8.0
- cudnn 6.0
- Tensorflow-gpu 1.4.1

## pre-installation
```bash
$ sudo apt-get update
$ sudo agt-get upgrade
$ sudo apt-get install python2.7 python-pip python3 python3-pip build-essential
$ sudo apt-get install linux-headers-4.4.0-116-generic
```
## python env
```bash
$ sudo pip install virtualenv virtualenvwrapper
```
### add python virtualenv in .bashrc
```bash
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
$ mkvirtualenv py3
```
## disable nouveau
```bash
$ lsmod | grep nouveau
$ cat /etc/modprobe.d/blacklist-nouveau.conf
blacklist nouveau
options nouveau modeset=0
```
```bash
$ sudo update-initramfs -u
$ reboot
```
## cuda 8.0
### get and import meta-data
```bash
$ wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
$ wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/patches/2/cuda-repo-ubuntu1604-8-0-local-cublas-performance-update_8.0.61-1_amd64-deb
$ sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
$ sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-cublas-performance-update_8.0.61-1_amd64-deb
```
### download key to allow installation
```bash
$ sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda
```
### cudnn 6.0
```bash
$ wget https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v6/prod/8.0_20170307/cudnn-8.0-linux-x64-v6.0-tgz
$ sudo cp -pRP include/cudnn.h /usr/local/cuda/include/
$ sudo cp -pRP lib64/libcudnn* /usr/local/cuda/lib64/
```
### setup cuda/cudnn path in .bashrc
```bash
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:/usr/local/cuda-8.0/extras/CUPTI/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
## install tensorflow
```bash
$ workon py3
(py3) $ pip3 install 'tensorflow-gpu<1.5'
```