### Konfigurasi SSH non Default

##### Konfigurasi file ssh_config
![](/assets/customssh/Capture.PNG)

Keterangan :
* **PermitRootLogin** : parameter yang digunakan sebagai flag izin akses ssh menggunakan user root. Pada konfigurasi di atas, root tidak boleh login menggunakan ssh.
* **PrintLastLog** : parameter konfigurasi yang digunakan untuk flag izin menampilkan detail user yang melakukan akses ssh sebelumnya. Pada konfigurasi di atas, log tidak ditampilkan.
* **AllowTcpForwarding** dan **X11Forwarding** : parameter yang digunakan untuk mengatur izin teknik forwarding pada saat akses ssh. Pada konfigurasi diatas, kedua parameter tersebut di atur tidak bisa (no).
