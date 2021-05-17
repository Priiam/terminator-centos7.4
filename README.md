# terminator-centos7.4

Instructions on installing Terminator v2 with centos7.4 on deprecated python3.4

# Install packages
```
> yum install python34 python34-devel python34-cairo python34-qobject vte291 keybinder3 intltool gettext
```
# Create venv on pyton34

I've used pycharm (version <= 2019.3) to handle the venv but you might as well set it up manually or use the main interpreter.

Note that your venv must be setup with setuptools version <44 to support python 3.4

# Add Python packages
```
> pip install psutil configobj 
```
# Install teminator

```
> git clone https://github.com/gnome-terminator/terminator.git
> cd terminator
> $PATH_TO_VENV/bin/python34 setup.py build
> $PATH_TO_VENV/bin/python34 setup.py install --single-version-externally-managed --record=install-files.txt
```

# Notes

Error on first launch : 

AttributeError: 'Terminal' object has no attribute 'set_allow_hyperlink'

Requires to replace terminatorlib/terminal.py - line 154 with this condition:
```python
if (Vte.MAJOR_VERSION, Vte.MINOR_VERSION) >= (0, 50):
    self.vte.set_allow_hyperlink(True)
```
