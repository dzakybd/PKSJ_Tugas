#KONFIGURASI
1. Update shared libraries `sudo ldconfig` 

2. Symblic link ke file Snort `sudo ln -s /usr/local/bin/snort /usr/sbin/snort`

3. Membuat Username `sudo groupadd snort`

4. Masukkan user ke dalam grup `sudo useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort`

5. Buat folder untuk konfigurasi Snort `sudo mkdir -p /etc/snort/rules /var/log/snort /usr/local/lib/snort_dynamicrules`

6. Mengatur permission Snort 1`sudo chmod -R 5775 /etc/snort /var/log/snort /usr/local/lib/snort_dynamicrules`

7. Mengatur permission Snort 2 `sudo chown -R snort:snort`