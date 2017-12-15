Lesson 5
--------
### SQL Injection: Single Quote Test On Username Field
- **Step 1**    : Buka Login/Register
    ![](/assets/lesson-5/login-register.png)
- **Step 2**    : Ketik `'` di kolom **Name**    
- **Step 3**    : Klik Login
    ![](/assets/lesson-5/quote_test.png)
- **Step 3**    : Anda akan mendapatkan error, jika terjadi error setelah anda login dengan **Name** `'`, berarti backend dari sistem rentan terhadap SQL Injection
    ![](/assets/lesson-5/quote_test_error.png)
    