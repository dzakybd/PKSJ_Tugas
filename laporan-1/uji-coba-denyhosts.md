## INSTALASI DENYHOSTS

* **Step 1**    : Instal dengan command berikut

  ```
  sudo apt-get install denyhosts
  ```
## PENGGUNAAN DENYHOSTS

* **Step 1**    : Konfigurasi Whitelist IP \(daftar IP yang dibolehkan mengakses ssh\)

  ```
  sudo nano /etc/hosts.allow
  ```

**  Jangan lupa juga untuk memasukan IP sendiri**
Formatnya penulisannya seperti berikut :

  ```
  sshd: 192.168.56.201
  sshd: 192.168.56.202
  ```
  atau mendatar seperti ini
  
  ```
  sshd: 192.168.56.201, 192.168.56.202
  ```
  
* **Step 2**    : Restart service denyhosts

  ```
  systemctl restart denyhosts.service
  systemctl enable denyhosts.service
  ```

## UJI COBA

* **IP whitelisted**    : 192.168.56.201 akan masuk daftar whitelisted, berikut hasilnya

![](/assets/denyhosts-hasil1.PNG)

* **IP not whitelisted**    : 192.168.56.201 dihapus dari daftar whitelisted, berikut hasilnya

![](/assets/denyhosts-hasil2.PNG)

* **Melihat log**    : Melihat riwayat akses ssh

  ```
  tail /var/log/denyhosts
  ```


## KESIMPULAN

Dengan uji coba yang telah dilakukan, Denyhosts berhasil membatasi akses ssh dari luar.

