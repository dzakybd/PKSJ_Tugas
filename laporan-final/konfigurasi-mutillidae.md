Konfirgurasi Multilidae
-----------------------
Multilidae sudah langsung terinstall pada virtual machine Metasploitable
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
- **Step 2**    : 


