### Uji Coba fail2ban

#### Menggunakan Ncrack
* **Step 1** : Siapkan list password, [500-worst-passwords.txt](/assets/ncrack-hydra/500-worst-passwords.txt)
* **Step 2** : Masukkan perintah
    `ncrack -p 22 --user administrator <user> -P <file password> <ip> -v`
    
    Contoh:
    
    `ncrack -p 22 --user administrator -P 500-worst-passwords.txt 10.151.36.159 -v`
    ![](/assets/ncrack-hydra/ncrack-custom-ssh-1.png)
* **Step 3** : Tunggu hasilnya
* **Step 4** : Pada gambar step 2, ncrack tidak berhasil menemukan password karena terblok dan dapat dilihat dengan perintah
`sudo iptables -S`
![](/assets/uji-fail2ban/2-ncrack.PNG)
* **Step 5** : Pastikan ip yang terblok sama dengan ip komputer penyerang.

![](/assets/ncrack-hydra/ifconfig.png)



