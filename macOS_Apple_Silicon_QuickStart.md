# oobabooga macOS Apple Silicon Quick Start for the Impatient

Make sure Xcode at the minimum is installed.

```bash
# Install Miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
bash Miniconda3-latest-MacOSX-x86_64.sh

# Update Conda if necessary
conda update -n base -c defaults conda

# Create a new Conda environment with Python 3.10
conda create -n python3.10 python=3.10

# Activate the new environment
conda activate python3.10

# Clone and build CMake from source
wget https://github.com/Kitware/CMake/releases/download/v3.22.1/cmake-3.22.1.tar.gz
tar -xzvf cmake-3.22.1.tar.gz
cd cmake-3.22.1
./bootstrap
make -j24
make install

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

# Clone the oobabooga GitHub repository
git clone https://github.com/oobabooga/text-generation-webui.git

# Install the Python modules listed in oobabooga's requirements.txt file
pip install -r requirements.txt

# Uninstall any existing version of llama-cpp-python
pip uninstall -y llama-cpp-python

# If necessary, reinstall llama-cpp-python with specific CMake arguments to enable Metal support
CMAKE_ARGS="-DLLAMA_METAL=on" FORCE_CMAKE=1 pip install --no-cache --no-binary :all: --compile -v llama-cpp-python

# If necessary, reinstall PyTorch, torchvision, and torchaudio from the PyTorch Conda channel
conda install pytorch torchvision torchaudio -c pytorch
```

Remember to create clones of your Conda environments at various stages to easily roll back to a previous state if something goes wrong.