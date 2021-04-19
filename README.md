# Ubuntu Setting Guide
ubuntu 20.04 LTS base

## 1. Connect
``` bash
ssh root@0.0.0.0
```
Enter initial password

## 2. Security
### 2.1. Change root password
```something```
### 2.2. Add Accounts (Easier way)
```adduser testuser```\
'adduser' automatically set password and create home directory
### 2.3. Add SSH key
(client side)\
``` bash
ssh keygen
```
```ssh-copy-id -i ~/.ssh/id_rsa.pub testuser@0.0.0.0```

## 3. Install
### 3.1. apt-get
#### update
```sudo apt-get update```\
```sudo apt-get upgrade```
#### pip
```sudo apt-get install python3-pip```
#### ffmpeg
```sudo apt install ffmpeg```\
```ffmpeg -version```
#### google-drive-ocamlfuse
```sudo add-apt-repository ppa:alessandro-strada/ppa```\
```sudo apt install google-drive-ocamlfuse```\

### 3.2. python packages
#### youtube-dl
```sudo pip3 install --upgrade youtube-dl```
#### 




