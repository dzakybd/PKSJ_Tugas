#KONFIGURASI
1. Update shared libraries `sudo ldconfig` 

2. Symblic link ke file Snort `sudo ln -s /usr/local/bin/snort /usr/sbin/snort`

3. Membuat Username `sudo groupadd snort`

4. Masukkan user ke dalam grup `sudo useradd snort -r -s /sbin/nologin -c SNORT_IDS -g snort`

5. Buat folder untuk konfigurasi Snort `sudo mkdir -p /etc/snort/rules /var/log/snort /usr/local/lib/snort_dynamicrules`

6. Mengatur permission Snort 1`sudo chmod -R 5775 /etc/snort /var/log/snort /usr/local/lib/snort_dynamicrules`

7. Mengatur permission Snort 2 `sudo chown -R snort:snort /etc/snort /var/log/snort /usr/local/lib/snort_dynamicrules`

8. Membuat file untuk menampung black list dan white list `sudo touch /etc/snort/rules/white_list.rules /etc/snort/rules/black_list.rules /etc/snort/rules/local.rules`

9. Meng-copy konfigurasi ke lokasi Snort `sudo cp ~/snort_src/snort-2.9.9.0/etc/*.conf* /etc/snort ~/snort_src/snort-2.9.9.0/etc/*.map /etc/snort`

10. Mendownload rules untuk community `wget https://www.snort.org/rules/community -O ~/community.tar.gz`

11. Ekstrak rules untuk community `sudo tar -xvf ~/community.tar.gz -C ~/`

12. Copy rules ke folder Snort `sudo cp ~/community-rules/* /etc/snort/rules`

13. Menghilangkan rules yang tidak dibutuhkan saat konfigurasi `sudo sed -i 's/include \$RULE\_PATH/#include \$RULE\_PATH/' /etc/snort/snort.conf`

14. Edit file konfigurasi `sudo gedit /etc/snort/snort.conf`
```
# Setup the network addresses you are protecting
ipvar HOME_NET <server public IP>/32
# Set up the external network addresses. Leave as "any" in most situations
ipvar EXTERNAL_NET !$HOME_NET
# Path to your rules files (this can be a relative path)
var RULE_PATH /etc/snort/rules
var SO_RULE_PATH /etc/snort/so_rules
var PREPROC_RULE_PATH /etc/snort/preproc_rules
# Set the absolute path appropriately
var WHITE_LIST_PATH /etc/snort/rules
var BLACK_LIST_PATH /etc/snort/rules
# unified2
# Recommended for most installs
output unified2: filename snort.log, limit 128
include $RULE_PATH/community.rules
```
15. Validasi konfigurasi yang telah diubah`sudo snort -T -c /etc/snort/snort.conf`

16. Buka file local.rules `sudo nano /etc/snort/rules/local.rules`
 
17. Tambahkan satu baris 
 `alert icmp any any -> $HOME_NET any (msg:"ICMP test"; sid:10000001; rev:001;)`
 
18. Cek tipe koneksi `ip addr`

19. Jika tipe koneksi `enp0s3`, maka masukkan konfigurasi `sudo snort -A console -i enp0s3 -u snort -g snort -c /etc/snort/snort.conf`

20. Buka link panda.gtisc.gatech.edu/malrec/

21. Klik PCAP untuk mengunduh file

22. Deteksi File PCAP dengan `snort -r <file.pcap>`

