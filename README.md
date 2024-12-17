# GPU computations prereading (preinstalling)

Installation of OpenCL driver for CPU
========================================

Windows
-------

1. Go to https://software.intel.com/content/www/us/en/develop/tools/opencl-cpu-runtime.html
2. Download (registration is required, [link for шindows](http://registrationcenter-download.intel.com/akdlm/irc_nas/vcp/13794/opencl_runtime_18.1_x64_setup.msi) - if it doesn't work try incognito mode or [this one](https://disk.yandex.ru/d/dlVbMoI3tsPZfw))
3. Install

Linux (Recommended Ubuntu 18.04, 20.04 or 22.04)
----------------------------------

1. Go to https://software.intel.com/content/www/us/en/develop/tools/opencl-cpu-runtime.html
2. Download (registration is required, [link for bUbuntu](http://registrationcenter-download.intel.com/akdlm/irc_nas/vcp/15532/l_opencl_p_18.1.0.015.tgz) - if it doesn't work try incognito mode or [this one](https://disk.yandex.ru/d/dlVbMoI3tsPZfw))
3. ``apt-get install -yq cpio lsb-core``
4. ``tar -xzf l_opencl_p_18.1.0.015.tgz``
5. ``sudo ./l_opencl_p_18.1.0.015/install.sh``
6. Install.

If you have a relatively new CPU like i7-8550U, then driver may not support it - ```clCreateContext``` return error ```CL_DEVICE_NOT_AVAILABLE```, in this case use [this driver](https://github.com/intel/compute-runtime/releases).

Installation of OpenCL driver for GPU
========================================

Windows
-------

Install the driver in the standard way - by downloading the installer from the official website of your video card vendor and installing it.

Linux
-----

NVidia: ``sudo apt install nvidia-<version>`` (e.g, ``nvidia-384`` or ``nvidia-535``)

AMD: [download](https://www.amd.com/en/support) and install amdgpu-pro driver

Environment check
==================

CLI
-------
```shell
mkdir -p build && cd build
cmake ..
make
./enumDevices
```
If you see at least one device, then everything is fine (in my case it looks like this):
```
Number of OpenCL platforms: 1
Platform #1/1
    Platform name: NVIDIA CUDA
    Vendor name: NVIDIA Corporation
Number NVIDIA CUDA devices: 1
Device name:  NVIDIA RTX A2000 8GB Laptop GPU
  Device type: GPU
Device memory size:  7869 MBs
Size of global memory cache line in bytes: 128
Maximum configured clock frequency of the device in MHz: 1177
```
CLion
-------
1. Open project in CLion
2. Right click on CMakeLists.txt -> Reload CMake Project
3. Run enumDevices configuration

IDE and compiler
==================
For both Unix-like and Windows systems, it's recommended to use CLion.

For Windows make sure you use 64-bit compiler. It's recommended to use MSVC.

For Windows, you also can use Visual Studio with CMake, but it's not recommended.