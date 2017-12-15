Konfirgurasi Multilidae
-----------------------
Multilidae sudah langsung terinstall pada virtual machine Metasploitable. Sebelum menggunakannya, ada beberapa tahap untuk konfigurasi Multilidae 
- **Step 1**    : Ganti nama database Multilidae
    - Akses **config.inc**
    ```
    nano /var/www/multilidae/config.inc
    ```
    - Ganti isi __**config.inc**__ menjadi berikut
    ```
    <?php
        /* NOTE: On Samurai, the $dbpass password is "samurai" rather than blank */

        $dbhost = '0.0.0.0';
        $dbuser = 'root';
        $dbpass = '';
        $dbname = 'owasp10';
    ?>
    ```

- **Step 2**    : Akses Multilidae pada Metasploitable
```
http://10.151.36.64/mutillidae/
```
![](/assets/konfigurasi-multilidae/multilidae_home.png)
- **Step 3**    : Reset DB untuk membuat struktur basis data dari Multilidae ke MySQL pada Metasploitable
![](/assets/konfigurasi-multilidae/reset_db.png)

Mulitilidae sudah siap digunakan


