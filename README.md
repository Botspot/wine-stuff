# wine-stuff
This repository hosts useful files to help the installation of Wine from [Pi-Apps](https://github.com/Botspot/pi-apps).  
[![badge](https://github.com/Botspot/pi-apps/blob/master/icons/badge.png?raw=true)](https://github.com/Botspot/pi-apps)  

Currently this repository has:
- A recent build of mesa thanks to Salva from Pi Labs
- A collection of 6 custom icons for use in the menu. Botspot drew them all using Boxy SVG.

Salva provided provided his Mesa build instructions:
```bash
sudo apt-get install -y libxcb-randr0-dev libxrandr-dev \
        libxcb-xinerama0-dev libxinerama-dev libxcursor-dev \
        libxcb-cursor-dev libxkbcommon-dev xutils-dev \
        xutils-dev libpthread-stubs0-dev libpciaccess-dev \
        libffi-dev x11proto-xext-dev libxcb1-dev libxcb-*dev \
        bison flex libssl-dev libgnutls28-dev x11proto-dri2-dev \
        x11proto-dri3-dev libx11-dev libxcb-glx0-dev \
        libx11-xcb-dev libxext-dev libxdamage-dev libxfixes-dev \
        libva-dev x11proto-randr-dev x11proto-present-dev \
        libclc-dev libelf-dev git build-essential mesa-utils \
        libvulkan-dev ninja-build libvulkan1 python3-mako \
        libdrm-dev libxshmfence-dev libxxf86vm-dev libwayland-dev \
        python3-mako wayland-protocols libwayland-egl-backend-dev \
        cmake libassimp-dev python3-pip

sudo pip3 install meson

git clone https://gitlab.freedesktop.org/mesa/drm.git
cd drm
meson builddir/
sudo ninja -C builddir/ install

git clone https://gitlab.freedesktop.org/mesa/mesa.git
cd mesa
meson --prefix /home/pi/mesa -Dgles1=disabled -Dgles2=enabled -Dplatforms=x11 -Dvulkan-drivers=broadcom -Ddri-drivers= -Dgallium-drivers=v3d,kmsro,vc4,virgl -Dbuildtype=release -Dc_args="-mcpu=cortex-a72 -mfpu=neon-fp-armv8 -mfloat-abi=hard" -Dcpp_args="-mcpu=cortex-a72 -mfpu=neon-fp-armv8 -mfloat-abi=hard" build
sudo ninja -C build/ install

#then remove the unnecesary drivers from /dri folder
```
The Wine prefix was generated using these commands:
```bash
#install wine and winetricks FIRST

rm -rf ~/.wine
wine wineboot
winetricks mfc42 vcrun6 vcrun2003 xact d3drm d3dx9_43 d3dcompiler_43 d3dx9
tar -czvf wine-prefix.tgz /home/pi/.wine
```
