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
something
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
```

## 3. Install
### 3.1. apt-get
#### update
``` bash
sudo apt-get update
sudo apt-get upgrade
```
#### pip
``` bash
sudo apt-get install python3-pip
```
#### ffmpeg
``` bash
sudo apt install ffmpeg
ffmpeg -version
```
#### google-drive-ocamlfuse (mount google drive as a folder)
https://olgabotvinnik.com/blog/googledrive-ubuntu/
``` bash
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt install google-drive-ocamlfuse
mkdir ~/GoogleDrive
```
(get client_id and client_secret from Google Drive API)
https://console.cloud.google.com/marketplace/product/google/drive.googleapis.com


### 3.2. python packages
#### youtube-dl
``` bash
sudo pip3 install --upgrade youtube-dl
```
#### 




