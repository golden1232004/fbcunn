- Find a machine with [Ubuntu 14.04+](http://www.ubuntu.com/) and an NVIDIA GPU with compute capability 3.5 or above

Then, install everything that is needed by using the instructions below:

Install CUDA
=============
```bash
sudo apt-get install build-essential
```

If you are using a Virtual Machine (like Amazon EC2 instances), install:
```bash
sudo apt-get update
sudo apt-get install linux-generic
```

Download the CUDA .deb file for Linux Ubuntu 14.04 64-bit from this page: https://developer.nvidia.com/cuda-downloads  
It would be a file named similar this: cuda-repo-ubuntu1404_6.5-14_amd64.deb  
Now, install it using:
```bash
sudo dpkg -i cuda-repo-ubuntu1404_6.5-14_amd64.deb
sudo apt-get update
sudo apt-get install cuda
echo "export PATH=/usr/local/cuda/bin/:\$PATH; export LD_LIBRARY_PATH=/usr/local/cuda/lib64/:\$LD_LIBRARY_PATH; " >>~/.bashrc && source ~/.bashrc
```

Restart your computer

Install CuDNN
- Go to https://developer.nvidia.com/cuDNN and use the Download button (you have to register and login to download. no way around that.)
- Download cuDNN 6.5 R1 for Linux. You will download a file cudnn-6.5-linux-R1.tgz
then use the commands:
```bash
tar -xvf cudnn-6.5-linux-R1.tgz
sudo cp cudnn-6.5-linux-R1/*.h /usr/local/cuda/include
sudo cp cudnn-6.5-linux-R1/*.so* /usr/local/cuda/lib64
```

Install Torch Dependencies
==========================
```bash
curl -sk https://raw.githubusercontent.com/torch/ezinstall/master/install-deps | bash
```

Install Torch in a local folder
================================
```bash
cd ~/
git clone https://github.com/soumith/torch-distro.git
cd torch-distro
bash install.sh
echo "export PATH=~/torch-distro/install/bin:\$PATH; export LD_LIBRARY_PATH=~/torch-distro/install/lib:\$LD_LIBRARY_PATH; " >>~/.bashrc && source ~/.bashrc
```

If you want to uninstall torch, you can use the command: `rm -rf ~/torch-distro`

Install Folly, fbthrift, thpp and fblualib
============================================
```bash
curl -sk https://raw.githubusercontent.com/soumith/fblualib/master/install_all.sh | bash
```

Install fbcunn
==============
```bash
git clone https://github.com/torch/nn && cd nn && git checkout getParamsByDevice && luarocks make rocks/nn-scm-1.rockspec
git clone https://github.com/facebook/fbcunn.git
cd fbcunn && luarocks make rocks/fbcunn-scm-1.rockspec # go get a coffee
```
