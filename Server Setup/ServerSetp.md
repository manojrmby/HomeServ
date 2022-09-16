# Setup
## 1.Download server Iso (Ubuntu) 
## 2.Download Proxmox
## 3.Port forwarding in Router (BSNL)
## 4. DNS setting 


# 1.Ubuntu Iso
## https://ubuntu.com/download/server
## https://www.youtube.com/watch?v=HS3bHNu-h-k&t=3s&ab_channel=ProximaX (ALL inside WIndows Hyper)
      Steps 
         ------------------- Step 07 -------------------
         apt update

         apt upgrade

         reboot
         ------------------- Step 09 -------------------
         lsblk

         parted /dev/sdb mklabel gpt

         parted -a opt /dev/sdb mkpart primary ext4 0% 100%

         lsblk

         mkfs.ext4 -L proximax -N 100000000 /dev/sdb1

         lsblk --fs

         mkdir /mnt/proximax

         nano /etc/fstab
         Add: LABEL=proximax /mnt/proximax ext4 defaults 0 2

         mount -a

         df -h

         df -i
         ------------------- Step 10 -------------------
         cd /mnt/proximax/

         curl -fsSL get.docker.com -o get-docker.sh

         sh get-docker.sh

         curl -L "github.com/docker/compose/releases/download/1.27.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

         sudo chmod +x /usr/local/bin/docker-compose

         sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

         docker-compose --version

         systemctl enable docker.service

         systemctl start docker.service

         systemctl status docker.service
# 2.Download Proxmox
## https://www.proxmox.com/en/downloads

# 3.Port forwarding in Router (BSNL)
## https://www.youtube.com/watch?v=-u4fVPRfzlA&ab_channel=NetlinkICTPvt.Ltd.

# 4. DNS setting ( https://dynu.com)
## https://www.youtube.com/watch?v=wCJjiHp0d0w&ab_channel=TechGuides
## https://techguides.yt/guides/linux-server/free-dynamic-dns/ 
## Steps
     sudo crontab -e

     */15 * * * * wget -O dynulog -4 "https://api.dynu.com/nic/update?hostname=example.dynu.com&myip=10.0.0.0&myipv6=no&username=someusername&password=somepassword"


