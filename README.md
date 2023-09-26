# install-accel-sim-framework
A straightforward way to install Accel-Sim framework. Follow README and clone this repo to execute `.sh` file.

# Steps
1) Download `https://releases.ubuntu.com/18.04/ubuntu-18.04.6-live-server-amd64.iso`. Use `Rufus` to make a bootable USB of this image. You can also install in VM. If you don't have a USB stick you can burn it into a CD using UltraISO.
2) Make sure you have a proper internet connection. Follow this or this for more information.
3) Run `sudo apt-get install -y wget build-essential xutils-dev bison zlib1g-dev flex libglu1-mesa-dev libssl-dev libxml2-dev libboost-all-dev git g++ libxml2-dev python-setuptools python-dev python3-pip`
4) Run `pip3 install pyyaml plotly psutil`
5) It is a good idea to download other requirements offline to make reusable for your future same installations. Download these links `http://developer.download.nvidia.com/compute/cuda/11.0.1/local_installers/cuda_11.0.1_450.36.06_linux.run`, `https://engineering.purdue.edu/tgrogers/gpgpu-sim/benchmark_data/all.gpgpu-sim-app-data.tgz` and `http://developer.download.nvidia.com/compute/cuda/4_2/rel/sdk/gpucomputingsdk_4.2.9_linux.run`.
6) Download latest releases of official `accel-sim-framework` and `gpu-app-collection`. Unzip them.
7) Move files in two above steps to your newly installed ubuntu machine.
8) Run `chmod +x cuda_11.0.1_450.36.06_linux.run` and then `sudo ./cuda_11.0.1_450.36.06_linux.run`. If you don't have a GPU hardware then just uncheck nvidia driver (first item).
9) Set variables as described in the ouptut of previous step. Next three steps set it permenantly.
10) Run `echo "export CUDA_INSTALL_PATH=\"/usr/local/cuda-11.0\"" >> ~/.bashrc`
11) Run `echo "export LD_LIBRARY_PATH=\"/usr/local/cuda-11.0/lib64:$LD_LIBRARY_PATH\"" >> ~/.bashrc`
12) Run `echo "export PATH=\"/usr/local/cuda-11.0/bin:$PATH\"" >> ~/.bashrc`
13) Run `source ~/.bashrc`.
14) Edit `src/setup_environment` from `gpu-app-collection`. Comment lines 8 to 10. Also, modify lines 11 and 12 to refer to the downloaded `gpucomputingsdk_4.2.9_linux.run`.
15) If `source ZZZ_PARENT_PATH_OF_GPU_APP_COLLECTION_ZZZ/gpu-app-collection-XXX/src/setup_environment` was successful, comment lines 11 to 14 of that file. Run `echo "source ZZZ_PARENT_PATH_OF_GPU_APP_COLLECTION_ZZZ/gpu-app-collection-XXX/src/setup_environment" >> ~/.bashrc`. Replace `XXX` with the downloaded version of `gpu-app-collection`. Currently it is `1.0.1`. Replace `ZZZ_PARENT_PATH_OF_GPU_APP_COLLECTION_ZZZ` with correct parent path.
16) Edit `get_data.sh` from `gpu-app-collection`. Comment lines 7 and 9. Also, modify line 8 to refer to the downloaded `all.gpgpu-sim-app-data.tgz`.
17) Run `source ~/.bashrc`.
18) **Building `gpu-app-collection` benchmarks:** First, `cd gpu-app-collection-XXX`. Then, (A) Run `make -C src/ data`. (B) Run the appropriate command for your desired benchmark. For example for `Rodinia 3.1`, run `make -j -C src/ rodinia-3.1`
19) **Building `accel-sim-framework`:** First, `cd accel-sim-framework-YYY`. Change `YYY` to the correct version of downloaded release file. Currently, it is `1.2.0`. Then, (A) Run `pip3 install -r requirements.txt`. (B) Run `source gpu-simulator/setup_environment.sh`; Similarly, run `echo "source ZZZ_PARENT_PATH_OF_ACCEL_SIM_ZZZ/accel-sim-framework-YYY/gpu-simulator/setup_environment.sh" >> ~/.bashrc` to make it permanent. Replace `ZZZ_PARENT_PATH_OF_ACCEL_SIM_ZZZ` with correct parent path. (B) Run `make -j -C gpu-simulator/`
20) Copy a configuration from `gpu-simulator/gpgpu-sim/configs/tested-configs/` to `bin/11.0/release` of `gpu-app-collection`. Run a program to verify your installation.
21) You can verify each steps by running `echo $?` after the running that command. Values other than `0` value are for errors.
