# Linux

## Ssh configuration hardening

### New install

On a new install, it's always good to regenerate the server's keys especially on a hoster you don't know with:

```dpkg-reconfigure openssh```

### Hardening
Change `Port` to something else than 22

Increase `ServerKeyBits`

Set `PermitRootLogin` to `no`

Set `LoginGraceTime` to a low value like 15, it's the number of seconds you have to type the password

Set `DebianBanner` to `no` (depends on OS), prevents broadcasting system informations

### Util

`AllowUsers` to only allow few users to use ssh

### Disable password auth
To disable password authentication and just use RSA key auth:

`UsePAM` to `no`

`PasswordAuthentication` to `no`

`ChallengeResponseAuthentication` to `no`

## Password storage configuration

```/etc/login.defs```
Be sure to check `ENCRYPT_METHOD` is using a secure hashing algorithm, it's also a good thing to increase `SHA_CRYPT_MIN_ROUNDS` to a higher value for better security.
`UMASK` is the default rights for new user creation.

```/etc/skel/``` contains file being copied for new user. It's important to check that other groups don't have rights on ```/home/xxx```.
chmod /home directories

## APT

Check that ```/etc/apt/sources.list``` is using correct deb package to have good download rates.

### Switching to unstable

Switch all packages to `unstable main contrib non-free`

## Services

On a default installation, some services are not needed and should be disabled, like:
* port 25 (smtp/mail server)
* port 53 (dns)

## Apache

In file `/etc/apache2/apache2.conf`, set the following:
```
ServerTokens ProductOnly
ServerSignature Off
```
This will disable the broadcast of apache2 version.

## Gnome configuration

### autolock with gnome-screensaver

```
gsettings set org.gnome.desktop.session idle-delay 300
gsettings set org.gnome.desktop.screensaver lock-delay 0
```

### disable touchpad when mouse is present

```
gsettings set org.gnome.desktop.peripherals.touchpad send-events disabled-on-external-mouse
```

### Change the url selection in graphical environnement so you can select an URL with the protocol

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/word-char-exceptions '@ms "-,.;:/?%&#_=+@~·"'
```

To remove this key and get back to current Ubuntu defaults:
```
$ dconf reset /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/word-char-exceptions
```

## Tricks

This folder contains scripts that gets executed for every user on the system.
```
/etc/profile.d/
```
Force the resolution to full HD, put this in `/root/.bashrc`
```
if [ ! -f /tmp/res ]; then                                                      
    xrandr --newmode "1920x1080"  173.00  1920 2048 2248 2576  1080 1083 1088 1\
120 -hsync +vsync
    xrandr --addmode Virtual1 1920x1080
    xrandr --output Virtual1 --mode 1920x1080
    echo 'Done' > /tmp/res
fi
```

## List of usefull packages

```
apt-get install git emacs25-nox gdb valgrind subversion wget curl strace ltrace python-pip gcc screen sudo binwalk wipe nmap tcpdump zip p7zip-full
dpkg --add-architecture i386
apt-get install libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386
```
