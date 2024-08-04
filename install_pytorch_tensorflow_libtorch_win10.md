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
5. Move .dll, .h, .lib files to cuda toolkit folder:

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
5. Move .dll, .h, .lib files to cuda toolkit folder
6. Check system variables
7. Install tensorflow-gpu along with its dependencies by running:

```
pip3 install tensorflow==2.10.1
```

## LibTorch

1. Install visual studio 2022
2. Repeat steps 2-6 above (except checking python path in step 6)
3. 




