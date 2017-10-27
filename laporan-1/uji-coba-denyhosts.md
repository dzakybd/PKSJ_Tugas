## INSTALASI DENYHOSTS

* **Step 1**    : Instal dengan command berikut

  ```
  sudo apt-get install denyhosts
  ```

* **Step 2**    : Konfigurasi Whitelist IP \(daftar IP yang dibolehkan mengakses ssh\)

  ```
  sudo nano /etc/hosts.allow
  ```

  Jangan lupa juga untuk memasukan IP sendiri, formatnya seperti berikut :

```
# hosts.allow   This file contains access rules which are used to
#               allow or deny connections to network services that
#               either use the tcp_wrappers library or that have been
#               started through a tcp_wrappers-enabled xinetd.
#
#               See 'man 5 hosts_options' and 'man 5 hosts_access'
#               for information on rule syntax.
#               See 'man tcpd' for information on tcp_wrappers
#
sshd: 192.168.56.201
sshd: 192.168.56.202
sshd: 10.151.254.180
```

* **Step 3**    : Restart service denyhosts

  ```
  systemctl restart denyhosts.service
  systemctl enable denyhosts.service
  ```

## UJI COBA

* **IP whitelisted**    : 192.168.56.201 akan masuk daftar whitelisted, berikut hasilnya



* **IP not whitelisted**    : 192.168.56.201 dihapus dari daftar whitelisted, berikut hasilnya

* **Melihat log**    : Melihat riwayat akses ssh

  ```
tail -f /var/log/denyhosts
tail -f /var/log/secure
  ```


## KESIMPULAN

Dengan uji coba yang telah dilakukan, Medusa dapat berhasil menyerang protokol ssh dengan _brute force attack_ jika password dari target terdapat didalam file password yang dibuat oleh penyerang dengan waktu 2 menit. Jika password tidak terdapat dalam file, maka serangan akan gagal.

