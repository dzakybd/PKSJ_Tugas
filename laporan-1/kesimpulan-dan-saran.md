### Kesimpulan dan Saran
#### Kesimpulan
* Hydra dan Ncrack melakukan brute force percobaan login dengan menggunakan kamus password.
* Kedua tools tersebut dapat diantisipasi dengan mengatur maksimal berapa kali percobaan login.
* Fail2ban merupakan tool tambahan pengamanan akses ssh yang dimana fail2ban menambahkan aturan pada firewall iptables untuk melakukan bloking dan izin hak akses.

#### Saran
* Aturan maksimal percobaan login sangat dianjurkan ketika kita mencoba melakukan pengamanan server untuk akses ssh.
* Port default ssh sangat dianjurkan untuk diganti.
* User root sangat dianjurkan untuk tidak diperbolehkan diakses menggunakan ssh.
* Penambahan firewall iptables sangat dianjurkan, karena tool fail2ban menggunakan iptables untuk mengatur hak akses ssh.
* Sangat disarankan menggunakan aplikasi pihak ketiga untuk pengamanan akses ssh, contohnya fail2ban.