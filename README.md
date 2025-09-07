# ubuntu-setup

## Add docker engine
- https://docs.docker.com/engine/install/ubuntu/
- https://docs.docker.com/engine/install/linux-postinstall/

## Add qemu
```
sudo apt update
sudo apt install qemu-system-x86 qemu-system-arm qemu-utils
sudo apt install binfmt-support qemu-user-static
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
docker run --platform linux/arm64 arm64v8/ubuntu uname -m
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