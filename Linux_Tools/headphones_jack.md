# Headphones not found after plugging in

In Ubuntu 20.04, I can use the headphones after boot, but the system does not find them, when I plug them in while the machine is running. 

The solution that seems to work is 

- remove the folder `~/.config/pulse`
- kill the running pulse server `pulseaudio -k`
    - the (post of which I took this)[https://askubuntu.com/questions/1230016/headset-microphone-not-working-on-ubuntu-20-04?noredirect=1&lq=1] recommends to also `sudo alsa force-reload`, but this did not seem to be necessary
