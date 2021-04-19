# Ubuntu Setting Guide
ubuntu 20.04 LTS base

## 1. Connect
```ssh root@0.0.0.0```

## 2. Security
### 2.1. Change root password
```something```
### 2.2. Add Accounts (Easier way)
```adduser testuser```\
automatically set password and create home directory
add addtional info (just press enter to skip)
### 2.3. Add SSH key
(client to server)
```ssh-copy-id -i ~/.ssh/id_rsa.pub testuser@0.0.0.0```

## 3. Install
### 3.1.apt-get
#### update
```sudo apt-get update```\
```sudo apt-get upgrade```
#### pip
```sudo apt-get install python3-pip```
#### ffmpeg
```sudo apt install ffmpeg```  
```ffmpeg -version```
### 3.2. python packages
```sudo pip3 install --upgrade youtube-dl```





