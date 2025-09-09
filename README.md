# ubuntu-setup

## Git
```
sudo apt install -y git
git config --global core.editor "code --wait"
git config --global user.email "myemail"
git config --global user.name dr3f
```

## Add SSH key
```
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Add to github

ssh -T git@github.com
```

## Add docker engine
- https://docs.docker.com/engine/install/ubuntu/
- https://docs.docker.com/engine/install/linux-postinstall/
- reboot

### Add qemu
```
sudo apt update
sudo apt install qemu-system-x86 qemu-system-arm qemu-utils
sudo apt install binfmt-support qemu-user-static
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
docker run --platform linux/arm64 arm64v8/ubuntu uname -m
```

## Add CUDA toolkit
- https://developer.nvidia.com/cuda-toolkit
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt update
sudo apt -y install cuda-toolkit-13-0
```

### CUDA for docker
```
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
    
sudo apt update
export NVIDIA_CONTAINER_TOOLKIT_VERSION=1.17.8-1
sudo apt install -y \
    nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}

sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```

## Add "open in code" to nautilus
- Checkout https://github.com/harry-cpp/code-nautilus
- Modify:  
```
wget -q -O ~/.local/share/nautilus-python/extensions/code-nautilus.py https://raw.githubusercontent.com/harry-cpp/code-nautilus/master/code-nautilus.py
```  
with:  
```
script_dir="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
cp $script_dir/code-nautilus.py ~/.local/share/nautilus-python/extensions/code-nautilus.py
```
- `./install.sh`