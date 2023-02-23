# MySelfHostSetup
Self Hosted Setup

# Introduction
This self-hosted setup is intented for entertainement mainly. It is hosted on a Raspberry Pi 4 and therefore isn't intended to host many consuming services.

# Hardware
- Raspberry Pi 4

# Software Used
- <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fi.redd.it%2Fuybguvnj1p821.png&f=1&nofb=1&ipt=c36f3dd7ec349cc70df7a22036817b83ecc7a86883ac8e3952b9f6f78cc29434&ipo=images" width="20" height="20" /> Jellyfin
- <img src="https://external-content.duckduckgo.com/ip3/org.cyphercolt.com.ico" width="20" height="20" /> OrganizrV2
- <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2F4.bp.blogspot.com%2F-wgdZB_sdTG4%2FXLxRypdhUXI%2FAAAAAAAAL_8%2FsfsSEqdhknISyipHK3hqeDgfXJpcPhndgCPcBGAYYCw%2Fs1600%2Fpicard_logo.png&f=1&nofb=1&ipt=cbaa57e78f2027f996799e102ebd27cec6bb8886ac0c91d6a6438de673833052&ipo=images" width="20" height="20" /> MusicBrainz Picard

# Installation of Software and Prerequisites
## Static Ip Adress
Modify the resolv conf file to enter your dns server
```
sudo nano /etc/resolv.conf
```
Contents in /etc/resolv.conf :
```
nameserver <ip of your dns-server>
```

Add Static Ip Settings
Modify the dhcpd.conf file and enter the settings for the network on which you want the static ip adress
```
sudo nano /etc/dhcpcd.conf
```
Contens in /etc/dhcpd.conf:
```
interface <interface-name> (ex: wlan0|eth0)
static ip_address= <static ip of your raspberry>/24 (ex: 192.168.1.120/24)
static routers= <ip of your router/modem> (ex: 192.168.1.254)
static domain_name_servers= <ip of your dns-server> (ex: 192.168.1.254)
```

## Jellyfin <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fi.redd.it%2Fuybguvnj1p821.png&f=1&nofb=1&ipt=c36f3dd7ec349cc70df7a22036817b83ecc7a86883ac8e3952b9f6f78cc29434&ipo=images" width="20" height="20" />

To install Jellyfin use the commands below: 

```
sudo apt update
sudo apt full-upgrade
sudo apt install apt-transport-https lsb-release
curl https://repo.jellyfin.org/debian/jellyfin_team.gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/jellyfin-archive-keyring.gpg >/dev/null
echo "deb [signed-by=/usr/share/keyrings/jellyfin-archive-keyring.gpg arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/debian $( lsb_release -c -s ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
sudo apt update
sudo apt install jellyfin
```
You can then access your jellyfin server on:
```
http://<ip of your raspberry>:8096
```

You'll then access the Gui to configure Jellyfin.
  
## OrganizrV2
WIP


Sources: 
MakeUseOf (Static Ip Addres) : https://www.makeuseof.com/raspberry-pi-set-static-ip/
PyMyLifeUp (Jellyfin) : https://pimylifeup.com/raspberry-pi-jellyfin/ 
