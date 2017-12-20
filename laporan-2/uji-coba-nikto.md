## INSTALASI NIKTO

* **Step 1**    : Install package nikto
  ```
  sudo apt-get install nikto
  ```

* **Step 2**    : Update vulnerability database nikto
  ```
  sudo nikto -update
  ```

## UJI COBA

Pertama, pastikan server wordpress sudah aktif. Kali ini akan diuji coba pada alamat ip `192.168.56.202` 

**Command**:

```
sudo nikto -h 192.168.56.202
```
-h adalah host

Lalu tunggu hasilnya

![](/assets/nikto-themole/nikto-hasil.PNG)  

  
Hasil yang didapatkan log berisi hal-hal yang bisa kita ketahui mengenai web application tersebut dan kemungkinan vulnerability yang ada seperti :
- versi apache yang digunakan
- anti-clickjacking header tidak diterapkan
- halaman /wp-admin tidak diatur forbidden atau diredirect, bisa diakses siapapun
- OSVDB [kode] adalah kemungkinan vulnerability yang bisa dilihat di [osvdb.org](www.osvdb.org). Namun sayangnya website tersebut ditutup dan dialihkan menjadi blog biasa, sehingga untuk mencari kita bisa memanfaatkan google : OSVDB [kode]

## KESIMPULAN

Dengan uji coba yang telah dilakukan, Nikto berhasil mengetahui informasi-informasi penting dan kemungkinan vulnerability yang ada pada server wordpress
