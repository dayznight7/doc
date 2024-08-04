# Install PyTorch, TensorFlow, LibTorch on Windows 10

This guide explains how to install PyTorch 2.4.0, TensorFlow 2.10.1, and LibTorch 2.4.0 on Windows 10 with Python 3.10.11 and Visual Studio 2022.

## Checking version compatibility

Examples of compatibility:

* rtx 40 (cuda >= 11.8)
* cuda 11.8 (driver >= 452.39)
* pytorch 2.4.0 (python 3.8-3.11)
* tensorflow 2.10.1 (python 3.7-3.10, cuda & cudnn is just recommendation)
* libtorch vs2022, vs2019 (cuda 12.x-11.8)

## PyTorch

1. Install python 3.10.11 (stable version of 3.10)
2. Update nvidia driver
3. Install cuda 11.8
4. Unzip cudnn 8.6
5. Move DLL, H, LIB files to cuda toolkit folder:

`cudnn\bin` => `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\bin`

`cudnn\include` => `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\include`

`cudnn\lib\x64` => `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\lib\x64`

6. Check system variables:

`CUDA_PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8`

`CUDA_PATH_V11_8`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8`

`PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\bin`

`PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\libnvvp`

`PATH`  |  `C:\Python\Python310\`

`PATH`  |  `C:\Python\Python310\Scripts\`

7. Install pytorch along with its dependencies by running:

```
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

## TensorFlow

1. Install python 3.10.11 (steps 1-6 are the same as above)
2. Update nvidia driver
3. Install cuda 11.8
4. Unzip cudnn 8.6
5. Move DLL, H, LIB files to cuda toolkit folder:
6. Check system variables
7. Install tensorflow-gpu along with its dependencies by running:

```
pip3 install tensorflow==2.10.1
```

## LibTorch (Debug)

1. Install visual studio 2022
2. Repeat steps 2-6 above
3. Check system variables:

`CUDA_PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8`

`CUDA_PATH_V11_8`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8`

`PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\bin`

`PATH`  |  `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\libnvvp`

4. Download opencv (window) and extract (optional) 
5. Download libtorch and unzip (rename `libtorch(debug)` to `libtorchd`)

(Release version):

https://download.pytorch.org/libtorch/cu118/libtorch-win-shared-with-deps-2.4.0%2Bcu118.zip

(Debug version):

https://download.pytorch.org/libtorch/cu118/libtorch-win-shared-with-deps-debug-2.4.0%2Bcu118.zip

5. Project Properties (Configuration: Debug)

General | C++ Language Standard:
`ISO C++17 Standard (/std:c++17)`

C/C++ | General | SDL checks:
`No (/sdl-)`

C/C++ | General | Additional Include Directories:
```
C:\CppLibs\opencv\build\include
C:\CppLibs\libtorchd\include
C:\CppLibs\libtorchd\include\torch\csrc\api\include
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\include
C:\Program Files\NVIDIA Corporation\NvToolsExt\include
```

Linker | General | Additional Library Directories:
```
C:\CppLibs\libtorchd\lib
C:\CppLibs\opencv\build\x64\vc16\lib
```

Linker | Input | Additional Dependencies:

(All LIB files in `C:\CppLibs\libtorchd\lib`)

```
opencv_world4100d.lib
asmjit.lib
c10.lib
c10_cuda.lib
caffe2_nvrtc.lib
cpuinfo.lib
dnnl.lib
fbgemm.lib
fbjni.lib
fmtd.lib
kineto.lib
libprotobufd.lib
libprotobuf-lited.lib
libprotocd.lib
pthreadpool.lib
pytorch_jni.lib
sleef.lib
torch.lib
torch_cpu.lib
torch_cuda.lib
XNNPACK.lib
```

Debugging | Environment:
`PATH=C:\CppLibs\libtorchd\lib;%PATH%`

Linker | Command Line | Additional Options:
`/INCLUDE:"?warp_size@cuda@at@@YAHXZ" `

6. Copy following code and Start Without Debugging
```
#include <iostream>
#include <torch/torch.h>

int main()
{
    if (torch::cuda::is_available()) {
        std::cout << "CUDA is available. Number of CUDA devices: " << torch::cuda::device_count() << std::endl;
    }
    else {
        std::cout << "CUDA is not available." << std::endl;
    }
    std::cout << "Hello World!\n";
}
```

## LibTorch (Release)

1. Repeat steps 1-6, but every folder name should be libtorch
2. Make sure to delete every last 'd', especially LIB files

Linker | Input | Additional Dependencies:

(All LIB files in `C:\CppLibs\libtorch\lib`)

```
opencv_world4100.lib
asmjit.lib
c10.lib
c10_cuda.lib
caffe2_nvrtc.lib
cpuinfo.lib
dnnl.lib
fbgemm.lib
fbjni.lib
fmt.lib
kineto.lib
libprotobuf.lib
libprotobuf-lite.lib
libprotoc.lib
pthreadpool.lib
pytorch_jni.lib
sleef.lib
torch.lib
torch_cpu.lib
torch_cuda.lib
XNNPACK.lib
```

3. Copy require DLL files in `C:\CppLibs\libtorch\lib` to the same folder as EXE file

CUDA & cuDNN DLL files are also required when deploying externally. 










