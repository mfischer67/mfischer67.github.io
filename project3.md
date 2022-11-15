# Project 3 - Docker Project
### System Administration
### Madison Fischer

## Methodology

I used this source for setting up WireGuard: https://thematrix.dev/setup-wireguard-vpn-server-with-docker/


### Installing WireGuard

Once you have your droplet ready in Digital Ocean, you open the Droplet Console in order to install WireGuard

First you have to make the WireGuard directory by running `mkdir -p ~/wireguard/`

Then you have to make a subdirectory in wireguard by running `mkdir -p ~/wireguard/config/`

Next, you have to nano the docker-compose.yml file from wireguard by running `nano ~/wireguard/docker-compose.yml`

We then copy and paste the code below into the docker-compose.yml file 
`version: '3.8'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/Chicago
      - SERVERURL=142.93.246.0
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1`
     
 We did change the TZ to America/Chicago and change the SERVERURL to my public IP address, which in this case is 142.93.246.0
 
 We then hit CONTROL + X and then Y to save the file and then ENTER to exit the file
 
 We then cd into wireguard by running `cd ~/wireguard/`
 
 Then we have to install docker-compose by running the command `sudo apt install docker-compose`
 
 Once that is installed, you then run `docker-compose up -d` which will create the Wireguard
 
 You then run `docker-compose logs -f wireguard`  to see the QR codes in order to get the VPN on your phone. 
 
 You scan the QR code with your WireGuard app and then activate the VPN to turn it on
 
 To get the VPN on your desktop, you first cd into wireguard by running `cd wireguard`
 
 You then cd into config by running `cd config` 
 
 Finally, you cd into peer_pc1/ by running `cd peer_pc1/`
 
 Once you have cd'ed into all of those, you then cat the peer_pc1.conf file
 
 You take the info that is printed out and put it into a text file, and then name the text file any name, but it must end with .conf
 
 You then take that .conf file and put it into WireGuard and then your VPN is done and then you just activate it.
 
 ![WireGuard Active on Phone](/wireguardphone.png)
 
 ![Before WireGuard is Turned On- Phone](/nonwireguardphone.png)
 
 ![After WireGuard is Turned On-Phone](/wireguardactive.png)
 
 ![Before WireGuard is Turned On- Desktop](/beforewireguard.png)
 
 ![After WireGuard is Turned On- Desktop](/afterwireguard.png)
