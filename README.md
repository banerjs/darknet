![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png)

# "You Only Look Once: Unified, Real-Time Object Detection (version 2)"

A yolo windows version (for object detection) pared down for compilation into Psi. Specifically, this code does not build to 32-bit architectures and does not build with OpenCV by default. It is aimed at generating a DLL that can then be used in the Psi ecosystem.

This repository is forked from the Windows fork: https://github.com/AlexeyAB/darknet of the Linux-version: https://github.com/pjreddie/darknet.

The documentation here is sparse and more details can be found at the above links and at: http://pjreddie.com/darknet/yolo/

## Building the code

Prerequisites:

- A CUDA capable GPU with compute capability >= 3.0. You can check your GPU's compute capability [here](https://en.wikipedia.org/wiki/CUDA#GPUs_supported).
- [CUDA 8.0](https://developer.nvidia.com/cuda-downloads)
- [cuDNN v5.1](https://developer.nvidia.com/cudnn). Don't use the latest v6.0 as there is a breaking API change.
  - Fetch the zip of CUDNN from Nvidia and unzip it
  - Copy all the files in the unzipped folder to where you have CUDA (for me it was `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0`).
  - Set the environment variable `cudnn` to match the variable `CUDA_PATH`
- Visual Studio 2015. CUDA 8.0 has been configured to work with this version, hence you should be using this IDE to build the code in this project

Optional:

- Download OpenCV2. (I haven't tested against OpenCV 3.0. You're welcome to do so and let me know)
  - Once you have unzipped OpenCV, set the environment variable `opencv` so that it points to the `build` directory of your download

Open and compile in Visual Studio 2015:

- Open the file `projects\darknet_dll.sln` in Visual Studio 2015.
- Download the YOLO weights based on the COCO dataset. Can be found at: http://pjreddie.com/media/files/yolo.weights
- Change the paths in `yolo_console_dll.cpp` to point to the directory(-ies) where you have the code and downloaded the weights.
- Assuming everything works as planned, you should simply be able to hit **Build Solution** (in Debug or Release) and have the `.dll` and a test `.exe` appear in the directory `projects\x64\<Debug/Release>`.

## Testing the build

Run `darknet_dll_test.exe` in the output directory to test your install.

## Gotchas

1. Make sure your file paths to the config files is correct.
1. This version of YOLO only outputs those COCO classes that I think are useful in an indoor setting. In addition to the object class `person`, it looks only for those object classes in the `relevant_class_str` variable in the `src\utils.c` file. Check to make sure the class you're trying to detect is in COCO as well as in that variable.

**Darknet can do a lot more, and you should check out the parent repositories of this repo to explore the full capabilities of this code**
