# Isambard
Some tips on how to setup environements on Isambard-AI

## Tips
- KEEP UPDATING...

### PyTorch
I cannot find how to install CUDA-Supported PyTorch for 2.1.0 - 2.3.1.
So always install torch==2.4.1 (which is the highest version that is compatible with PyTorch3D)
```python
pip install torch==2.4.1 --index-url https://download.pytorch.org/whl/cu124
pip install torchvision==0.19.1 torchaudio==2.4.1 # cannot install if specifying cu124 whl
```

### PyTorch3D
