# oobabooga macOS Apple Silicon Quick Start for the Impatient

Make sure Xcode at the minimum is installed.

```bash
# Install Miniconda MAke sure it is arm64
curl  https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o miniconda.sh
sh miniconda.sh
# After sucessful install of Conda you may remove miniconda.sh
rm miniconda.sh

# Get a new login Shell
exec bash -l

# Update Conda if necessary
conda update -n base -c defaults conda

# Create a new Conda environment with Python 3.10
conda create -n python3.10 python=3.10

# Activate the new environment
conda activate python3.10

# Clone and build CMake from source
git clone https://github.com/Kitware/CMake.git
cd cmake
./bootstrap
make -j24
make install
cd ..

# Clone, build, and install OpenBLAS
git clone https://github.com/xianyi/OpenBLAS
cd OpenBLAS
cmake .
make -j24
make install

# Install NumPy using pip with no cache, no binary, and compile
pip install --no-cache --no-binary :all: --compile numpy

# Alternatively, install NumPy using Conda
conda install numpy

# Install PyTorch using Conda
conda install pytorch torchvision torchaudio -c pytorch

# Alternatively, install PyTorch using pip
pip install torch torchvision torchaudio

# Clone the my slightly modified GitHub repository or use the clone after
# this to get the original oobabooga.
git clone https://github.com/unixwzrd/text-generation-webui-macos.git

# git clone https://github.com/oobabooga/text-generation-webui.git

# Install the Python modules listed in oobabooga's requirements.txt file
pip install -r requirements.txt

# Uninstall any existing version of llama-cpp-python
pip uninstall -y llama-cpp-python

# If necessary, reinstall llama-cpp-python with specific CMake arguments to enable Metal support
CMAKE_ARGS="--fresh -DLLAMA_METAL=ON -DLLAMA_OPENBLAS=ON -DLLAMA_BLAS_VENDOR=OpenBLAS" \
    FORCE_CMAKE=1 \
    pip install --no-cache --no-binary :all: --upgrade --compile llama-cpp-python==0.1.74

# Uninstall any existing version of pandas

pip uninstall -y pandas

# If necessary, reinstall pandas with specific CMake arguments to enable Metal support

FORCE_CMAKE=1 pip install --no-cache --no-binary :all: --compile pandas

# If necessary, reinstall PyTorch, torchvision, and torchaudio from the PyTorch Conda channel
conda install pytorch torchvision torchaudio -c pytorch
```

Add the --upgrade flag to upgrade any of the pip or conda commands if necessary.

Remember to create clones of your Conda environments at various stages to easily roll back to a previous state if something goes wrong.
