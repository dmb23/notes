# Fixing broken drivers

The main reason why I note this, is that I was greeted already two times by the warning 

> stopping User Manager for UID 121...

instead of booting my machine. This can be caused by *either too little space on the harddrive* or some messed-up NVIDIA drivers from the last update.
Steps that can help in different combinations to eot it working are:

- go into GRUB during boot
    - that is either `Shift` or `Esc` after the POST message during startup. 
    - there you can access a root shell
- check what is installed with `dpkg -l | grep nvidia`
- remove everything with `sudo apt --purge remove '*nvidia*'`
- possibly check if you can boot with the nouveau driver
- install a specific version of the driver (ideally the last one that worked) with `sudo apt install nvidia-driver-NNN`
- Once I had to revert from the *graphics-drivers* ppa back to ubuntu distro drivers. I think I also had to go to the PPA before.
    - `sudo add-apt-repository ppa:graphics-drivers/ppa` adds the PPA
    - `sudo add-apt-repository -r ppa:graphics-drivers/ppa` removes it again
- `ubuntu-drivers devices` gives you an overview of available drivers and sources
    `ubuntu-drivers autoinstall` installs the recommendation

Good luck!
