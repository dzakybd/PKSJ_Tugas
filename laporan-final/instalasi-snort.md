#SNORT
Snort adalah sistem pencegahan intrusi jaringan gratis dan open source (IPS) Dan sistem deteksi intrusi jaringan (IDS)  dibuat oleh Martin Roesch pada tahun 1998.  Snort sekarang dikembangkan oleh Sourcefire, dimana Roesch adalah pendiri dan CTO, dan yang telah dimiliki oleh Cisco sejak 2013.

Pada tahun 2009, Snort memasuki InfoWorld Open Source Hall of Fame sebagai salah satu perangkat lunak open source terbesar sepanjang masa.

#REQUIREMENT
1. Ubuntu 16.04
2. Snort
3. DAQ

#INSTALLASI
1. Instalasi library`sudo apt install -y gcc libpcre3-dev zlib1g-dev libpcap-dev openssl libssl-dev libnghttp2-dev libdumbnet-dev bison flex libdnet`

2. Membuat direktori `mkdir ~/snort_src`

3. Masuk ke direktori `cd ~/snort_src`

4. Download DAQ `wget https://www.snort.org/downloads/snort/daq-2.0.6.tar.gz`

5. Ekstrak DAQ `tar -xvzf daq-2.0.6.tar.gz`

6. Masuk ke dalam folder `cd daq-2.0.6`

7. Compile DAQ `./configure`

8. Install DAQ `make && sudo make install`

9. Masuk ke dalam folder Snort `cd ~/snort_src`

10. Download Snort `wget https://www.snort.org/downloads/snort/snort-2.9.11.tar.gz`
 