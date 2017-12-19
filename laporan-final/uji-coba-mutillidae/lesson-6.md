Lesson 6
--------
### Section 6: Open Console Terminal and Retrieve IP Address
- **Step 1**    : Buka Terminal Kali Linux
- **Step 2**    : Dapatkan IP address dari Kali Linux
    ```
    ifconfig
    ```
    - IP address yang didapatkan `10.151.64.195`
    - VM Kali Linux ini akan digunakan sebagai penyerang Metasploitable
    ![](/assets/lesson-6/ifconfig.png)

### Section 7: Start Web Browser Session to Mutillidae
- **Step 1**    : Buka Mozilla Firefox
- **Step 2**    : Buka Multilidae
    ![](/assets/lesson-6/open_multilidae.png)

### Section 8: Go To Login Page
- **Step 1**    : Klik Login/Register
    ![](/assets/lesson-6/click-login.png)

### Section 9: Configure Firefox Proxy Settings
- **Step 1**    : Buka Preference > Advanced > Network > Settings...
- **Step 2**    : Konfirgurasi Proxy
    - Klik **Manual Proxy Configuration**
    - Ketik `127.0.0.1` di kolom **HTTP Proxy**
    - Ketik `8080` di kolom **Port**
    - Check **Use this proxy server for all protocols**
    - Klik Ok
    - Klik Close
    ![](/assets/lesson-6/config-proxy.png)
    
### Section 10: Configure Burpsuite Settings
- **Step 1**    : Buka Burpsuite melalui Applications > Web Application Analysis > Burpsuite
    ![](/assets/lesson-6/VirtualBox_kali_19_12_2017_12_27_52.png)
- **Step 2**    : Pilih **Temporary project**, lalu **next**
    ![](/assets/lesson-6/temp_project.png)
- **Step 3**    : Pilih **Use Burp defaults**, lalu **Start Burp**
    ![](/assets/lesson-6/burp_config.png)
- **Step 4**    : Buka Proxy > Options, dan pastikan **Port** berupa 8080
    ![](/assets/lesson-6/burp_proxy.png)
- **Step 5**    : Buka Proxy > Intercept, ubah **Intercept is on** menjadi **Intercept is off**
    ![](/assets/lesson-6/proxy-intercept.png)
    
### Section 11: SQL Injection: By-Pass Password Without Username (Obtain Access #1)



    