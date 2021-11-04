# Build Standalone Executable

Follow the environment setup and building procedures below. Be sure to follow the one corresponding to your operating system.

## Prerequisite

- Anaconda
- An OS of amd64 architecture
- Git (for downloading the repository)

> Note: This package can be built without Anaconda. You can create a python virtual environment using "python -m venv collage" and install all the required packages. The process will be similar.

> I believe this package can be built on other architectures. On a 32-bit OS, the collage size may be limited due to the 4GB upper limit of the memory, resulting the inability to allocate a large matrix.

## Pre-building step

If you have created the "collage" environment before, please remove it first.

```bash
conda-env remove -n collage
```

> Note: You can use other names for the conda environment as long as you activate it before running the build script. Under Linux, you need to change the build script for it to find the correct location of the library.

## Environment Setup: MacOS and Linux

Create a conda environment without mkl. We don't want mkl because it's a huge library which takes a lot of space.

```bash
conda create -n collage python=3.6 nomkl numpy scipy scikit-learn pillow tqdm
```

Activate the conda environment

```bash
conda activate collage
```

Install the packages that are not available in the Anaconda repo

```bash
pip install lapjv wurlitzer pyinstaller opencv-contrib-python
```

## Environment Setup: Windows

Similar to MacOS/Linux, but we need to install from conda-forge

```bash
conda create -n collage python=3.6 nomkl numpy scipy scikit-learn pillow tqdm -c conda-forge
```

Activate the conda environment

```bash
conda activate collage
```

Install rest of the packages using pip

```bash
pip install lapjv pyinstaller opencv-contrib-python
```

## Building Executable: MacOS

```bash
git clone https://github.com/hanzhi713/image-collage-maker
cd image-collage-maker/build_scripts
conda activate collage
sh build_macos.sh
```

## Building Executable: Linux

The building script assumes that your Anaconda is installed at ~/anaconda3. If you install Anaconda at a different location, you need to modify the CONDA variable in image-collage-maker/build_scripts/build_linux.sh to make it point to the correct Anaconda directory.

This script requires the Anaconda path because it needs to append the library files of Pillow to the application bundle that will be built. Without the full library, Pillow may not function correctly. This problem is specific to Linux.

```bash
git clone https://github.com/hanzhi713/image-collage-maker
cd image-collage-maker/build_scripts
conda activate collage
sh build_linux.sh
```

## Building Executable: Windows

Assuming you have git installed and have it in your path, open the command prompt and type

```
git clone https://github.com/hanzhi713/image-collage-maker
cd image-collage-maker/build_scripts
conda activate collage
build_windows.bat
```
