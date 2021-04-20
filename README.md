# Ubuntu Setting Guide
ubuntu 20.04 LTS base

## 1. Connect
``` bash
ssh root@0.0.0.0
```
Enter initial password

## 2. Security
### 2.1. Change root password
``` bash
passwd
New password: 
Retype new password: 
```
### 2.2. Add Accounts (Easier way)
``` bash
adduser testuser
```
'adduser' automatically set password and create home directory
### 2.3. Add SSH key
(client side)
``` bash
ssh keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub testuser@0.0.0.0
ssh -i ~/.ssh/id_rsa testuser@0.0.0.0
```

## 3. Install
### 3.1. apt-get
#### 3.1.1. update
``` bash
sudo apt-get update
sudo apt-get upgrade
```
#### 3.1.2. pip
``` bash
sudo apt-get install python3-pip
```
#### 3.1.3. ffmpeg
``` bash
sudo apt install ffmpeg
ffmpeg -version
```
#### 3.1.4. google-drive-ocamlfuse (mount google drive as a folder)
reference: https://olgabotvinnik.com/blog/googledrive-ubuntu/
1. install package
``` bash
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt install google-drive-ocamlfuse
mkdir ~/GoogleDrive
```
1. Get client_id and client_secret from [Google Drive API](https://console.cloud.google.com/marketplace/product/google/drive.googleapis.com/)  
Credentials - OAuth 2.0 Client IDs - Client ID & Client Secret

1. run google-drive-ocamlfuse with headless mode
``` bash
google-drive-ocamlfuse ~/GoogleDrive -headless -id something1234.apps.googleusercontent.com -secret yoursecrethere
```
1. copy link generated and open ```https://accounts.google.com/o/oauth2/auth?client_id=REDACTED```
1. enter verification code from browser. if see ```Access token retrieved correctly.```
1. done.

_**(\*need to re-mount everytime after reboot -> crontab)**_

### 3.2. python packages
#### 3.2.1. youtube-dl
``` bash
sudo pip3 install --upgrade youtube-dl
```

## 4. Crontab
``` bash
crontab -e
```



