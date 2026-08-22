# PipeWire and EasyEffects configuration for Ubuntu 26.04 
# Requirements
- PipeWire
- WirePlumber
- EasyEffects

#Install dependencies
```bash
sudo apt update
```
#Install required packages:
```bash
sudo apt install \
     pipewire \
     pipewire-pulse \
     pipewire-alsa \
     pipewire-jack \
     wireplumber \
     qpwgraph\
     flatpak
```
# Add main flatpak repository: 
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
# Enable PipeWire Services
```bash
systemctl --user enable pipewire pipewire-pulse wireplumber
```
Start services:
```bash
systemctl --user start pipewire pipewire-pulse wireplumber
```
# Clone Repository
Clone repository:
```bash
git clone https://github.com/PersonalLinuxRepository/Sound.git
```
#Copy & Create directories 
```bash
mkdir -p ~/.config/pipewire && cd Sound
```
```bash
cp -r $PWD/pipewire/* ~/.config/pipewire
```
```bash
cp -r $PWD/easyeffects/db ~/.var/app/com.github.wwmm.easyeffects/config/easyeffects/
```
# Restart Audio Services
Reload user services:
```bash
systemctl --user restart pipewire pipewire-pulse wireplumber
```
# Verify Installation
Check audio server:
```bash
pactl info | grep "Имя сервера " 
```
or
```bash
pactl info | grep "Server Name "
```
#Enable passthrough for AC3,DTS,PCM contents: 
```bash 
wpctl status 
```
#Looking for output sound device marked with an asterisk (*)
```bash
pw-cli s <value_from_wpctl_status> Props '{ iec958Codecs = [ "PCM" "AC3" "DTS" ] }'
```