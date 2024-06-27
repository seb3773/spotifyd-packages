# spotifyd-packages
Debian bookworm packages for spotifyd  
  
Spotifyd is an open source Spotify client running as a UNIX daemon.  
Spotifyd streams music just like the official client, but is more lightweight and supports more platforms.  
Spotifyd also supports the Spotify Connect protocol, which makes it show up as a device that can be controlled from the official clients.  
https://github.com/Spotifyd/spotifyd  
+-------------------------------------------------  

I builded these packages because they are not in debian 12 repository; and I don't want to use the infamous snap version. 
x64,i386 & armhf packages provided.  
  
# installation:  
  
download appropriate package, and do (for example for 32bits package):  
  
```
sudo apt install ./spotifyd-0.3.5_i386.deb
```
(or install with graphical .deb installer if you have one, for example QSI installer for q4os: left click the .deb, then 'open with' and choose QSI installer)  
  
# spotifyd config file:  
I suggest you to create a config file for spotifyd with the options you want. This way, you can for example set your password in the file to avoid spotify apps like spotify-qt to ask you for it when it starts the spotifyd client.  
This is not necessary, but if this file doesn't exist, default options for spotifyd will be used, which is maybe not what you want; for example, I prefer to use pulseaudio backend. You can specify prefered audio bitrate too in this file among other things.  
To create this file do like this:  
  
```
sudo nano /etc/spotifyd.conf
```
  
and paste theses lines as a start (configure it with your parameters):  
  
  
```
[global]
# This is your spotify account name. Not your email
username = "YOUR_USERNAME"

# Note that this will be a plaintext password. Make sure it is a
# unique password that is not used anywhere else. We will make this
# file only readable by the root user to *help* mitigate the security risk.

password = "YOUR_PASSWORD"

backend = "pulseaudio"

# The device name can't have spaces
device_name = "DEVICE_NAME_YOU_WANT"
device_type = "computer"

# Audio bitrate
bitrate = 320

# Set the inital volume of spotify to 100
initial_volume = "100"
```

To avoid this file containing plaintext password to be read by anyone, let's set permissions:  
```
sudo chmod 640 /etc/spotifyd.conf
```

just to be sure, let's create a symlink of this file to  ~/.config/spotifyd/ :  
```
~/.config/spotifyd/
sudo ln -s /etc/spotifyd.conf ~/.config/spotifyd/spotifyd.conf
```
(this is because, for example, spotify-qt seems to check the ~/.config/spotifyd/ folder; but spotifyd is checking /etc/ folder for his config file...)
  
