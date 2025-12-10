# Isambard
Some tips on how to setup environements on Isambard-AI

## Tips
- KEEP UPDATING...

### PyTorch
I cannot find how to install CUDA-Supported PyTorch for 2.1.0 - 2.3.1.
So always install torch==2.4.1 (which is the highest version that is compatible with PyTorch3D)
```shell
pip install torch==2.4.1 --index-url https://download.pytorch.org/whl/cu124
pip install torchvision==0.19.1 torchaudio==2.4.1 # cannot install if specifying cu124 whl
```

### PyTorch3D
Install ioPath:
```shell
pip install iopath
```

Download and export NVIDIA-CUB:
```shell
curl -LO https://github.com/NVIDIA/cub/archive/1.10.0.tar.gz
tar xzf 1.10.0.tar.gz
export CUB_HOME=$PWD/cub-1.10.0
```

Set the gcc & g++ environment:
```shell
# import the module
module av gcc # to check what versions are available
module load gcc-native/13.2

# set environment variables
which gcc -> export CC=$THAT_PATH
which g++ -> export CXX=$THAT_PATH
```

Install pytorch3d from git source
```shell
pip install "git+https://github.com/facebookresearch/pytorch3d.git@stable" --no-build-isolation # if not adding --no-build-isolation, will incur 'No module named torch' error
```

### Other Tips
- Sometimes building from source incur errors. Try to load the gcc-native/13.2 and modify env variables to get around.
