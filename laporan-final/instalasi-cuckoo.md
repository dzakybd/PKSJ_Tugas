#CUCKOO
Cuckoo Sandbox adalah sistem analisis malware otomatis yang canggih, sangat modular, dan 100% open source dengan peluang aplikasi tak terbatas.

Anda bisa melempar file yang mencurigakan ke sana dan dalam hitungan menit Cuckoo akan memberikan laporan terperinci yang menguraikan perilaku file saat dijalankan di dalam lingkungan yang realistis namun terisolasi.

Perangkat lunak perusak adalah pisau swiss-army dari penjahat dunia maya dan musuh lainnya ke perusahaan atau organisasi Anda.

#REQUIREMENT
1. MacOs
2. VM Windows XP

#INSTALASI 
1. Dengan Brew Manager, lakukan instalasi untuk requirement sebelum melakukan instalasi `brew install libmagic cairo pango openssl`

2. Masuk ke dalam file include `cd /usr/local/include`

3. Lakukan symbolic link pada openssl `ln -s ../opt/openssl/include/openssl`

4. Instalasi tcpdump `brew install install tcpdump`

5. Permission untuk tcpdump `sudo chmod +s /usr/sbin/tcpdump`

6. Instalasi MongoDB `brew install mongodb`

7. Tambahkan user baru `sudo adduser cuckoo`

8. Memberian user baru untuk Virtualbox `sudo usermod -a -G vboxusers cuckoo`

9. Instalasi setuptools `pip install -U pip setuptools`

10. Instalasi Cuckoo `pip install -U cuckoo`

11. Run `cuckoo -d` untuk membuatkan file cuckoo untuk nanti digunakan, perintah yang sama berikutnya akan mengaktifkan fungsi cuckoo