CudaMiner instructions (Ubuntu 12.10)
=====================================

Download and install the official Nvidia kernel module

```sh
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/319.17/NVIDIA-Linux-x86_64-319.17.run
chmod +x *.run
sudo ./NVIDIA-Linux-x86_64-319.17.run # Accept/OK/Yes all :P
```

Download and install the official CUDA libraries

```sh
wget http://developer.download.nvidia.com/compute/cuda/5_0/rel-update-1/installers/cuda_5.0.35_linux_64_ubuntu10.04-1.run
chmod +x *.run
mkdir cuda5
./cuda_5.0.35_linux_64_ubuntu10.04-1.run --extract=`pwd`/cuda5
# Accept/OK/Yes everything and when asked to put the librariesin /opt/cuda-5.0
sudo ./cuda5/cudatoolkit_5.0*.run
```

Clone and install cudaminer

```sh
git clone https://github.com/cbuchner1/CudaMiner.git
cd CudaMiner
git checkout 88c6da6d5c2b798d1de7031e8dbcc2678f635e4b #Last known commit that works with Tesla K10
./autogen.sh
CFLAGS="-O3 -march=corei7-avx -mtune=corei7-avx -mmmx -msse -msse2 -msse3 -mssse3 -msse4 -msse4.1 -msse4.2" \
CPPFLAGS="-O3 -march=corei7-avx -mtune=corei7-avx -mmmx -msse -msse2 -msse3 -mssse3 -msse4 -msse4.1 -msse4.2" ./configure
make -j10
sudo make install
```

Run cudaminer

```sh
cudaminer -o stratum+tcp://teamcoinye.com:3333 -O pool_account_name.worker_name:worker_password -m 1,1 -C 1,1
```

Flags and options explanation http://4x.reddit.com/r/Dogecoinmining/comments/1tguse/a_treatise_on_cuda_miner/


cpuminer instructions (Ubuntu 12.10)
====================================

Install dependencies

```sh
sudo aptitude install libcurl4-openssl-dev
```

Clone and install cpuminer

```sh
git clone https://github.com/pooler/cpuminer.git
cd cpuminer
./autogen.sh
CFLAGS="-O3 -march=corei7-avx -mtune=corei7-avx -mmmx -msse -msse2 -msse3 -mssse3 -msse4 -msse4.1 -msse4.2" \
CPPFLAGS="-O3 -march=corei7-avx -mtune=corei7-avx -mmmx -msse -msse2 -msse3 -mssse3 -msse4 -msse4.1 -msse4.2" ./configure
make -j10
sudo make install
```

Run minerd

```sh
minerd -o stratum+tcp://teamcoinye.com:3333 -O pool_account_name.worker_name:worker_password -t 5*(num_processors)/3
```
