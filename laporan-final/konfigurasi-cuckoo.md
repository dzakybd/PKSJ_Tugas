# KONFIGURASI
1. Masuk ke dalam file cuckoo yang telah di run sebelumnya 

2. Ubah file cuckoo.conf `$CWD/conf/cuckoo.conf`

3. Menjadi 

    ```
    machinery = virtualbox
    [resultserver]
    ip = 10.151.64.194 #This is the IP address of the host
    port = 2042 #leave default unless you have services running
    
    ```
4. Ubah file auxiliary.conf `$CWD/conf/auxiliary.conf`

5. Menjadi
    ```
    [sniffer]
    # Enable or disable the use of an external sniffer (tcpdump) [yes/no].
    enabled = yes
    # Specify the path to your local installation of tcpdump. Make sure this
    # path is correct.
    # You can check this using the command: whereis tcpdump
    tcpdump = /usr/sbin/tcpdump
    # Specify the network interface name on which tcpdump should monitor the
    # traffic. Make sure the interface is active.
    # The ifconfig command will show you the interface name.
    interface = vboxnet0
    ```
    
6. Ubah konfigurasi Virtualbox `$CWD/conf/virtualbox.conf`

7. Menjadi 
    ```
    machines = cuckoo1
    [cuckoo1]
    label = cuckoo1
    platform = windows
    ip = 10.151.64.196 # IP address of the guest
    snapshot = cuckoo # name of snapshot
    ```
    
8. Ubah konfigurasi reporting.conf `$CWD/conf/reporting.conf`

9. Menjadi 
    ```
    [mongodb]
    enabled = yes
    
    ```
10. Buat Virtualbox menggunakan Windows XP, gunakan bridge connection agar dapat terhubung dengan MacOS

11. Install python2.7 pada Windows XP https://www.python.org/downloads/release/python-2711/

12. Install python imaging library pada Windows XP http://effbot.org/downloads/PIL-1.1.7.win32-py2.7.exe

13. Copy file agent.py dari `.cuckoo/cuckoo/agent/agent.py` ke dalam virtual mesin Windows XP `C:/Documents and Settings/All Users/Start Menu/Programs/Startup`

14. Buatlah snapshot dari Windows XP saat dimatikan dan dilakukan restorasi dari state terakhir sebelum mati dengan
    ```
    vboxmanage snapshot "windowsxp" take "snapshot1" --pause
    vboxmanage controlvm "windowsxp" poweroff
    vboxmanage snapshot "windowsxp" restorecurrent
    
    ```

