## Kesimpulan
1. WPScan adalah sebuah alat yang digunakan untuk mengecek seberapa kuat tingkat keamanan dari situs WordPress. Hasil akhirnya adalah mengetahui kelemahan dari Plugin yang terinstall
2. SQLMap adalah alat untuk memudahkan dalam melakukan SQL Injection, karena SQL Injection dapat mencari kelemahan dari suatu website dari target link address. SQLMap akan mencari kelemahan secara otomatis dengan hanya memasukkan link target dari post kedalam database.
3. Dari hasil uji coba penetrasi SQL Injection didapatkan bahwa masih terdapat celah-celah yang dapat ditembus, kita dapat melakukan SQL Injection melalui celah yang terdapat pada plugin yang belum update walaupun wordpress sudah paling update terbaru.

## Saran
1. Saat ini sudah banyak tools yang aman dari serangan SQL Injection, jadi sebaiknya gunakanlah update dari Plugin atau aplikasi terbaru
2. Hal lain yang harus diperhatikan adalah periksalah update-update pada wordpress dan pluginya secara berkala, jika terdapat update pada wordpress dan plugin-plugin yang terinstall, segeralah untuk melakukan update karena celah-celah SQL Injection bisa terdapat pada plugin yang belum update tersebut.