# sip_asterisk_arm64v8
SIP Server dengan Asterisk pada Armbian 64 Bit (STB-B860H/HG680P) untuk Arsitektur SBC

# Langkah I
## Direktori Host

````
mkdir -p asterisk/{asterisk-config,asterisk-logs,asterisk-data,asterisk-spool}
cd asterisk
````

## File Konfigurasi Asterisk
#### Buat sip.conf di direktori asterisk-config:
````
[general]
context=default
bindport=5060
bindaddr=0.0.0.0
allowguest=no
disallow=all
allow=ulaw

[1001]
type=friend
username=1001
secret=securepassword
host=dynamic
context=default

[1002]
type=friend
username=1002
secret=securepassword
host=dynamic
context=default
````
#### Buat extensions.conf di direktori asterisk-config:
````
[default]
exten => 1001,1,Dial(SIP/1001,20)
exten => 1001,n,Hangup()
exten => 1002,1,Dial(SIP/1002,20)
exten => 1002,n,Hangup()

````

## Jalankan Hapus | Stop | Start container
````
docker-compose -p 'sip_astersik_arm64' up --remove-orphans --build -d
````

````
docker-compose -p 'sip_astersik_arm64' down -v
````

````
docker-compose -p 'sip_astersik_arm64' stop
````

````
docker-compose -p 'sip_astersik_arm64' start
````
## Uji Coba
### Registrasi Klien SIP:
#### Gunakan aplikasi seperti Linphone, Zoiper, atau perangkat SIP hardware.
#### Gunakan detail berikut untuk registrasi:
````
Server: IP atau domain server
Username: 1001 atau 1002
Password: securepassword
````
### Lakukan Panggilan:
#### Dari klien SIP 1001, panggil ekstensi 1002.
#### Verifikasi apakah panggilan tersambung.

# Langkah II
## 1. Download materi
````
git clone https://github.com/otn4mrehus/sip_asterisk_arm64v8.git
cd sip_asterisk_arm64v8
````
## 2. Jalankan Docker-compose
````
docker-compose -p 'sip_astersik_arm64' up --remove-orphans --build -d
````

