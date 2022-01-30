---
layout: post
title:  "Rocky linux에 samba 설치하기"
date:   2022-01-30 08:23:00 +0900
categories: rocky samba
---

# Rocky linux에 samba 설치하기

패키지 설치하기

```
# dnf install samba samba-common samba-client
```


디렉토리 권한 설정하기

```
# mkdir -p /data/nas
# chmod -R 755 /data/nas
# chown -R  nobody:nobody /data/nas
# chcon -t samba_share_t /data/nas
```

samba 설정 파일 

```
[global]
workgroup = WORKGROUP
server string = Samba Server %v
netbios name = rocky-8
security = user
map to guest = bad user
dns proxy = no
ntlm auth = true


[Public]
path =  /data/nas
browsable =yes
writable = yes
guest ok = yes
read only = no
```

설정파일 테스트하기

```
# testparm
```

서비스 재시작
```
# systemctl start smb
# systemctl enable smb
# systemctl start nmb
# systemctl enable nmb
# systemctl status smb
# systemctl status nmb
```

samba 계정 추가
```
# useradd smbuser
# smbpasswd -a smbuser
```

samba 그룹 추가 및 samba 그룹 추가
```
# sudo groupadd smb_group
# sudo usermod -g smb_group smbuser
```

디렉토리 권한 설정 및 SE Linux 설정
```
# mkdir -p /srv/tecmint/private
# chmod -R 770 /srv/tecmint/private
# chcon -t samba_share_t /srv/tecmint/private
# chown -R root:smb_group /srv/tecmint/private 
```


개인 계정 설정 추가
```
[Private]
path = /srv/tecmint/private
valid users = @smb_group
guest ok = no
writable = no
browsable = yes
```

추가 확인할 내용
* /sbin/nologin 
* map to guest = bad user

https://www.tecmint.com/install-samba-rhel-centos-fedora/
https://www.linuxshelltips.com/install-samba-rockylinux-almalinux/