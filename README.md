# Isambard
Some tips on how to setup environements on Isambard-AI

## Tips
- KEEP UPDATING...

### PyTorch
- I cannot find how to install CUDA-Supported PyTorch for 2.1.0 - 2.3.1.
- torch 2.4.1
This is the highest version that is compatible with PyTorch3D
```shell
pip install torch==2.4.1 --index-url https://download.pytorch.org/whl/cu124
pip install torchvision==0.19.1 torchaudio==2.4.1 # cpu version only
```
- If you want torchvision for CUDA, you need to build from source.
Do it in a GPU node, and load gcc 13, change c++ environment variables accordingly.
```shell
git clone --branch release/0.19 https://github.com/pytorch/vision.git
cd vision
TORCH_CUDA_ARCH_LIST=9.0 pip install -e . -v --no-build-isolation
```

- Newer
```shell
# Torch 2.6.0:
pip install torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu126
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

### SpConv
Ref: [https://github.com/traveller59/spconv/tree/v2.3.6?tab=readme-ov-file](https://github.com/traveller59/spconv/tree/v2.3.6?tab=readme-ov-file)

**Do all the installations in GPU machine!** ```srun --gpus=1 --pty bash```

Install cumm-cu126 v0.7.3 from source: [cumm](https://github.com/FindDefinition/cumm/tree/v0.7.3)
```shell
export CUMM_CUDA_VERSION="12.6"
export CUMM_CUDA_ARCH_LIST="9.0"
export CUMM_DISABLE_JIT="1"
```

Modify the cuda path in ```cumm/common.py``` from ```/usr/local/cuda``` to the one in our machine (view by ```echo $PATH```).

Run ```python setup.py bdist_wheel```+```pip install dists/xxx.whl```

Install spconv-cu126 v2.3.6 from source: [spconv](https://github.com/traveller59/spconv/tree/v2.3.6?tab=readme-ov-file#install)
```shell
export CUMM_CUDA_VERSION="12.6"
export CUMM_CUDA_ARCH_LIST="9.0"
export SPCONV_DISABLE_JIT="1"
```

Remove the cumm dependence in ```pyproject.toml```, and in ```setup.py```.

Run ```python setup.py bdist_wheel```+```pip install dists/xxx.whl```

Go to another directory and try ```python -c "import spconv.pytorch"``` to see if the installation is successful.

### Installation Choices for Some Packages
```
CGAL: conda install conda-forge::cgal # pip won't work

```

### Other Tips
- Sometimes building from source incur errors. Try to load the gcc-native/13.2 and modify env variables to get around.
