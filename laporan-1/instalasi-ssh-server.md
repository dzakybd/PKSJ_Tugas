## Langkah menginstal SSH Server ##

**SSH** (Secure Shell) adalah protokol jaringan yang memungkinkan remote login. SSH yang sering digunakan adalah OpenSSH

[Fitur OpenSSH](https://www.openssh.com/features.html) :
 
- Secure Communication
- Strong Encryption (3DES, Blowfish, AES, Arcfour)
- X11 Forwarding (encrypt X Window System traffic)
- Port Forwarding (encrypted channels for legacy protocols)
- Strong Authentication (Public Key, One-Time Password and KerberosAuthentication)
- Agent Forwarding (Single-Sign-On)
- Interoperability (Compliance with SSH 1.3, 1.5, and 2.0 protocol Standards)
- SFTP client and server support in both SSH1 and SSH2 protocols.
- Kerberos and AFS Ticket Passing
- Data Compression


### Cara 1 : Instalasi SSH pada saat menginstall OS ###

##### Ubuntu Server #####
Pada saat instalasi Ubuntu Server 16.04 LTS kita akan disuguhkan menu *Software Selection*
 
![Openssh install](https://i.imgur.com/Yf7C3Wj.png)

Untuk menginstall SSH kita pilih saja OpenSSH lalu Continue. Maka SSH akan terinstall

##### Ubuntu Desktop & OS Linux lainnya #####
Pada Ubuntu Dekstop dan OS Linux lainnya biasanya SSH akan secara default terinstall.

Untuk mengeceknya jalankan command berikut `ssh -V`

Hasil pada Ubuntu Dekstop 16.04 LTS mungkin akan seperti ini :
`OpenSSH_7.2p2 Ubuntu-4ubuntu2.2, OpenSSL 1.0.2g 1 Mar 2016`

### Cara 2 : Instalasi SSH sesudah terinstall OS ###

##### Ubuntu Server / Dekstop & OS Linux lainnya  #####
Untuk melakukan instalasi, hanya perlu jalankan command berikut

1. Install SSH pada OS Linux
	- Pada Ubuntu/Debian/Linux Mint : `sudo apt-get install openssh-server openssh-client`
	- Pada RHEL/Centos/Fedora : `yum -y install openssh-server openssh-clients`
2. Lalu jalankan serive SSH `sudo /etc/init.d/ssh start`
3. Untuk pengecekan status lakukan `sudo /etc/init.d/ssh status`
4. Untuk konfigurasi SSH bisa ditemukan di `/etc/ssh/sshd_config`

----------

**Dokumentasi command** bisa dilihat disini [OpenSSH manual](https://www.openssh.com/manual.html)
