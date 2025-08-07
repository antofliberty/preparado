# First steps

```bash
# update
apt update
apt upgrade -y

# create your user
adduser username
usermod -aG sudo username

# From PC
ssh-copy-id username@<SERVER_IP>

# configure ssh
nano /etc/ssh/sshd_config

"
Port <PORT>
PermitRootLogin no
PasswordAuthentication no
AllowUsers username
ClientAliveInterval 60
ClientAliveCountMax 0
TCPKeepAlive yes
"

# change port here too
nano /etc/systemd/system/sockets.target.wants/ssh.socket

# restart ssh
systemctl restart ssh
systemctl daemon-reload
service ssh restart
 
# check port changed
lsof -n -i :22 | grep LISTEN

ufw allow <PORT>/tcp
ufw enable
exit
```

Install Docker
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
