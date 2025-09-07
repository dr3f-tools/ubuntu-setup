# ubuntu-setup

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