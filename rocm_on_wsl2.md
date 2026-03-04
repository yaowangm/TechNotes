.wslconfig

[wsl2]
kernelCommandLine = intel_iommu=on iommu=pt pci=assign-busses pci=realloc
memory=48GB
swap=8GB
processors=20
networkingMode=mirrored
firewall=true
[experimental]
autoMemoryReclaim=gradual
sparseVhd=true

install dependencies:

sudo apt install -y cmake build-essential

install rocm lib:

cd /tmp
wget https://repo.radeon.com/amdgpu-install/7.2/ubuntu/jammy/amdgpu-install_7.2.70200-1_all.deb
sudo apt install ./amdgpu-install_7.2.70200-1_all.deb -y
sudo amdgpu-install -y --usecase=rocm --no-dkms

install librocdxg:

(install Windows SDK if necessary: https://learn.microsoft.com/en-us/windows/apps/windows-sdk/downloads
 default path after installation: c/Program Files (x86)/Windows Kits/10/)

git clone https://github.com/ROCm/librocdxg.git
cd librocdxg
cd ~/librocdxg/build
cmake .. \
  -DWIN_SDK="/mnt/c/Program Files (x86)/Windows Kits/10/Include/10.0.26100.0/shared/" \
  -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
sudo make install

echo 'export LD_PRELOAD=/opt/rocm/lib/librocdxg.so:$LD_PRELOAD' >> ~/.bashrc
echo 'export HSA_ENABLE_DXG_DETECTION=1' >> ~/.bashrc
source ~/.bashrc

/opt/rocm/bin/rocminfo
sudo cp librocdxg.so /opt/rocm/lib/

install openssl lib：
sudo a
pt install libssl-dev

install llama.cpp：

git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp
mkdir -p build-rocm && cd build-rocm
cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DGGML_HIP=ON \
  -DAMDGPU_TARGETS="gfx1150"
make -j$(nproc)
sudo make install

./bin/llama-cli --version

download model:

export HF_ENDPOINT=https://hf-mirror.com
wget https://hf-mirror.com/hfd/hfd.sh
chmod +x hfd.sh
sudo apt install aria2 -y
./hfd.sh unsloth/Qwen3.5-35B-A3B-GGUF   --tool aria2c -x 8   --include "*MXFP4_MOE*"   --local-dir /home/wy/models/qwen3.5-35b-a3b-mxfp4

llama-cli -m ~/models/qwen3.5-35b-a3b-mxfp4/Qwen3.5-35B-A3B-MXFP4_MOE.gguf -p "Hello" -n 30
