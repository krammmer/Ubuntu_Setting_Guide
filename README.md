# Ubuntu Setting Guide
ubuntu 20.04 LTS base

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
'adduser' automatically set password and create home directory
### 2.3. Allow sudo privilege
``` sh
vi /etc/sudoers

# User privilege specification
root	ALL=(ALL:ALL) ALL
testuser	ALL=(ALL:ALL) ALL # add testuser
```
### 2.4. Add SSH key
(client side)
``` sh
ssh keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub testuser@0.0.0.0
ssh -i ~/.ssh/id_rsa testuser@0.0.0.0
```

## 3. Install
### 3.1. apt-get
#### 3.1.1. update
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
reference: https://olgabotvinnik.com/blog/googledrive-ubuntu/
1. install package
``` sh
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt install google-drive-ocamlfuse
mkdir ~/GoogleDrive
```
2. Get client_id and client_secret from [Google Drive API](https://console.cloud.google.com/marketplace/product/google/drive.googleapis.com/)  
Credentials - OAuth 2.0 Client IDs - Client ID & Client Secret
3. run google-drive-ocamlfuse with headless mode
``` sh
google-drive-ocamlfuse ~/GoogleDrive -headless -id something1234.apps.googleusercontent.com -secret yoursecrethere
```
4. copy link generated and open ```https://accounts.google.com/o/oauth2/auth?client_id=REDACTED```
5. enter verification code from browser. if see ```Access token retrieved correctly.```
6. done.

_**(\*need to re-mount everytime after reboot -> crontab)**_

### 3.2. python packages
list all installed packages (except default)
``` sh
pip3 list
```
#### 3.2.1. youtube-dl
``` sh
sudo pip3 install --upgrade youtube-dl
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
## 4. Crontab
### 4.1. Change server timezone to JST
``` sh
date
sudo timedatectl set-timezone Asia/Tokyo
```



