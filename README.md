# Ubuntu Setting Guide
Ubuntu 20.04 LTS base

## 1. Connect
``` sh
ssh root@0.0.0.0
```
Enter initial password

## 2. Security
### 2.1. Change root password
``` sh
passwd
New password: 
Retype new password: 
```
### 2.2. Add Accounts (Easier way)
``` sh
adduser testuser
```
'adduser' automatically set password and create home directory\
while 'useradd' doesn't
### 2.3. Allow sudo privilege
``` sh
vi /etc/sudoers

# User privilege specification
root	ALL=(ALL:ALL) ALL
testuser	ALL=(ALL:ALL) ALL # add testuser
```
### 2.4. Add SSH key
(client side - macOS)
``` sh
ssh keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub testuser@0.0.0.0
ssh -i ~/.ssh/id_rsa testuser@0.0.0.0
```
### 2.5. Fail2Ban
#### Install
``` sh
sudo apt update && sudo apt install fail2ban -y
fail2ban-client -V
sudo vi /etc/fail2ban/jail.local
```
#### Contents for 'jail.local'
``` sh
[DEFAULT]
# IPs to NOT to ban
ignoreip = 127.0.0.1/8

# while try fails in "findtime" over "maxretry" count, ban ip for "bantime"
findtime = 86400
bantime = 86400
maxretry = 5

# How to ban: if using firewalld then 'firewallcmd-new'
# if using iptables then 'iptables-multiport'
banaction = iptables-multiport

# enable ban protection for ssh
[sshd]
enabled = true
```
#### Check Ban status
```
/etc/init.d/fail2ban start
sudo fail2ban-client status sshd
```

## 3. Install
### 3.1. apt-get
#### 3.1.1. update/upgrade
``` sh
sudo apt-get update
sudo apt-get upgrade
```
#### 3.1.2. pip
``` sh
sudo apt-get install python3-pip
```
#### 3.1.3. ffmpeg
``` sh
sudo apt install ffmpeg
ffmpeg -version
```
#### 3.1.4. google-drive-ocamlfuse (mount google drive as a folder)
references: https://olgabotvinnik.com/blog/googledrive-ubuntu/
https://github.com/astrada/google-drive-ocamlfuse
1. install package
``` sh
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt install google-drive-ocamlfuse
sudo add-apt-repository ppa:alessandro-strada/google-drive-ocamlfuse-beta
sudo apt-get install google-drive-ocamlfuse
mkdir ~/GoogleDrive
```
2. config setting
```
cd .gdfuse
cd default
vi config
oauth2_loopback=true
save(:wq)
```
3. Get client_id and client_secret from [Google Drive API](https://console.cloud.google.com/marketplace/product/google/drive.googleapis.com/)\
Credentials - OAuth 2.0 Client IDs - Client ID & Client Secret
4. run google-drive-ocamlfuse with headless mode
``` sh
google-drive-ocamlfuse ~/GoogleDrive -headless -id something1234.apps.googleusercontent.com -secret yoursecrethere
```
5. copy link generated and open ```https://accounts.google.com/o/oauth2/auth?client_id=REDACTED```
6. enter verification code from browser(URL).
7. ```Access token retrieved correctly.```
8. done.

_**(\*need to re-mount everytime after reboot -> crontab)**_
``` sh
google-drive-ocamlfuse ~/Googledrive -headless
```

#### 3.1.5. Chrome (for Selenium)
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt-get update
sudo apt-get install google-chrome-stable
google-chrome --version
```
Download Chrome driver at [HERE](https://sites.google.com/chromium.org/driver/)\
Copy driver's link and download with wget and unzip
```
wget -N LINK
unzip chromedriver_linux64.zip
```
Install xvfb
```
sudo apt-get install xvfb
```

### 3.2. python packages
list all installed packages (except default installed packs)
``` sh
pip3 list
```
#### 3.2.1. youtube-dl
``` sh
sudo pip3 install --upgrade youtube-dl
sudo pip3 install --upgrade yt-dlp
```
#### 3.2.2. Beautiful Soap
``` sh
sudo pip3 install beautifulsoup4
```
#### 3.2.3. python-telegram-bot
``` sh
sudo pip3 install python-telegram-bot
```
#### 3.2.4. google-api-python-client
``` sh
sudo pip3 install google-auth-oauthlib
sudo pip3 install google-api-python-client
```
#### 3.2.5. pyinstalive
``` sh
sudo pip3 install git+https://github.com/dvingerh/PyInstaLive.git@3.2.4
```
#### 3.2.6. Django
``` sh
sudo pip3 install Django
sudo pip3 install djangorestframework
sudo pip3 install django-rest-knox
sudo pip3 install django-cors-headers
sudo pip3 install psycopg2-binary
```

### 3.3. PostgreSQL
#### 3.3.1. Install
``` sh
sudo apt-get -y install postgresql
```
#### 3.3.2. Switch Account
``` sh
sudo -i -u postgres
psql
\q
```
#### 3.3.3. Create PostgreSQL Account
```
```

## 4. Crontab
### 4.1. Change server timezone to JST
``` sh
date
sudo timedatectl set-timezone Asia/Tokyo
sudo service cron stop
sudo service cron start
```
It is available to specify timezone by using ```CRON_TZ``` variable, but only works on INSIDE of cronjob(processes which started by cron), NOT the EXECUTE TIME itself.\
Need to change whole server timezone to run cronjob locally.

## 5. Others
### 5.1. Shell
#### 5.1.1. Check default Shell
``` sh
echo $SHELL
```

#### 5.1.2. Set Alias (bash)
``` sh
cd ~
vi .bashrc

# USER ALIAS
alias log='cd /home/testuser/Logs/'
alias prj='cd /home/testuser/Projects/'
```

### 5.2. Downgrade Python
#### 5.2.1. Install add-apt-repository
```
sudo apt update
sudo apt install -y software-properties-common
```
#### 5.2.2. Add ppa repository
```
sudo apt-add-repository ppa:deadsnakes/ppa
sudo apt update
```
#### 5.2.3. Install specific Python version
```
sudo apt install python3.8
sudo apt install python3.8-distutils
```
#### 5.2.4. Change default alias
```
update-alternatives --install /usr/bin/python3 python /usr/bin/python3.8 1
sudo update-alternatives --config python
```
