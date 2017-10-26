### Konfigurasi SSH non Default

##### Konfigurasi file ssh_config
![](/assets/customssh/Capture.PNG)

Keterangan :
* **PermitRootLogin** : parameter yang digunakan sebagai flag izin akses ssh menggunakan user root. Pada konfigurasi di atas, root tidak boleh login menggunakan ssh.
* **PrintLastLog** : parameter konfigurasi yang digunakan untuk flag izin menampilkan detail user yang melakukan akses ssh sebelumnya. Pada konfigurasi di atas, log tidak ditampilkan.
* **AllowTcpForwarding** dan **X11Forwarding** : parameter yang digunakan untuk mengatur izin teknik forwarding pada saat akses ssh. Pada konfigurasi diatas, kedua parameter tersebut di atur tidak bisa (no).
* **PermitEmptyPassword** : parameter untuk mengatur akses ssh untuk user yang tidak memiliki password. Pada konfigurasi diatas, user tanpa password tidak diizinkan.
* **Protocol** : parameter untuk mengatur versi protocol ssh. Awalnya konfigurasi default menggunakan protocol versi 1, kemudian di-_uncomment_ pada protocol 2 sehigga menggunakan protcol versi 2 yang lebih aman.
* **ClientAliveInterval** dan **ClientAliveCountMax** : kedua parameter tersebut untuk mengatur waktu _disconnect_ saat user idle (user tidak melakukan apapun). Pada **ClientAliveInterval** memiliki nilai 300 yang artinya saat user idle selamat 5 menit, maka koneksi akan diputus.

