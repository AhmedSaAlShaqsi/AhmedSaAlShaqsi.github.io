# Create a Droplet in DigitalOcean:

1. Use this link to [DigitalOcean.com](https://m.do.co/c/d33d59113ab6) to sign up with your school email and Agent Miller’s credit card
2. Choose the lowest price tier - $6 per month
3. Create an Ubuntu droplet
4. Select all of the basic options
5. Choose password instead of ssh key - **set your password**
6. Name the project - Wireguard project
7. Droplet IP - **Now your droplet IP appear beside the droplet name.**
  
# Install Wireguard:

1. SSH into the droplet by opening a terminal and typing ssh root@[ip]
	a. Where you would replace [ip] with the IP of your DigitalOcean Droplet
2. Install the dependencies/packages needed to run docker. Commands: sudo apt install docker, sudo apt install docker-compose, sudo apt install wireguard
4. Set up Wireguard using Docker Compose: 
	a. Create a directory for Wireguard: 
	```bash
mkdir -p /opt/wireguard  
cd /opt/wireguard  
 ```
	b. Create a docker-compose.yml file: 
	```bash
nano docker-compose.yml  
 ```
3. Add the following configuration to docker-compose.yml: 

**yaml  docker-compose.yml**
  GNU nano 8.1                                                        
```bash
version: '3.8'

services:

  wireguard:

    container_name: wireguard

    image: linuxserver/wireguard

    environment:

      - PUID=1000

      - PGID=1000

      - TZ=American/New_York

      - SERVERURL=45.55.41.235

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

      - net.ipv4.conf.all.src_valid_mark=1
```
		d.Save and exit 
1. Run Wireguard: 
```bash
docker-compose up -d 
```
3. Check logs to get the QR code: 
```bash
docker logs wireguard 
```
# Test Your VPN 

**Mobile Device**

1. Open the Wireguard app and scan the QR code from the logs. 
2. Before connecting: 
	a. Visit [IPLeak.net](https://ipleak.net/) and screenshot your local IP. 
3. After connecting: 
	a. Turn on the Wireguard VPN and revisit IPLeak.net. 
	b. Screenshot the VPN IP to confirm it is active. 

**Laptop** 

1. Find the configuration file: 
```bash
ls /opt/wireguard/config  
```
2. Copy the .conf file to your laptop. 
	In our case the .conf file contained:
```bash
[Interface]

PrivateKey = iLwC8xbCzwVd5j9s7Et/72d6keAAVTlkmxcY/wX6Ako=

ListenPort = 518

.20

Address = 10.0.0.2/32

DNS = 10.0.0.1

  

[Peer]

PublicKey = P5GnsQQZk4X0KilGkKNg5ND/XZjV0KP7QDNuShSCcG4=

PresharedKey = 5X6AWptfcPEHqhgi3nVlEb6vx833rLQic/ofI4TMy5s=

AllowedIPs = 0.0.0.0/0, ::/0

Endpoint = 45.55.41.235:51820
```
3. Import the file into the Wireguard app or CLI. 
4. Follow the same steps as mobile to confirm functionality using IPLeak.net.
**Screenshots:**
This is a screenshot after activating the VPN and as we can see that our IP address shows that we are in New Jersey even if we are not there.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcJ1KLTAxI4OLaAj1g88hlSBJMIR-yZrpvL55Spz6cXWczK0xqC1neG_zzt76XH-COczSWKYZKi9K8qvIg9mKM3ioBlj7lgS3pxiGr10LDATVADHA53NPxM3ppzj6S1Wg?key=Bo4EsgvGOTNoLvI0BRUCGrwI)
