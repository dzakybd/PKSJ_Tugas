## INSTALASI THE MOLE

  ```
  sudo apt-get install themole
  ```

## UJI COBA

Pertama, pastikan server wordpress sudah aktif. Kali ini akan diuji coba pada alamat ip `192.168.56.202` 

**Command**:

```
sudo nikto -h 192.168.56.202
```
-h adalah host

Lalu tunggu hasilnya

![](/assets/nikto-hasil.PNG)  


## KESIMPULAN

Dengan uji coba yang telah dilakukan, Nikto berhasil mengetahui informasi-informasi penting dan kemungkinan vulnerability yang ada pada server wordpress
