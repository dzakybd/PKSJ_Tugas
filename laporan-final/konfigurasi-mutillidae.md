Konfirgurasi Multilidae
-----------------------
Multilidae sudah langsung terinstall pada virtual machine Metasploitable
- **Step 1**    : Ganti nama database multilidae
    - Akses config.inc
    ```
    nano /var/www/multilidae/config.inc
    ```
    - Ganti isi config.inc menjadi berikut
    ```
    <?php
        /* NOTE: On Samurai, the $dbpass password is "samurai" rather than blank */

        $dbhost = '0.0.0.0';
        $dbuser = 'root';
        $dbpass = '';
        $dbname = 'owasp10';
    ?>
    ```

- **Step 2**    : Akses multilidae pada metasploitable
```
http://10.151.36.64/mutillidae/
```
- **Step 2**    : 


