# KONFIGURASI
1. Masuk ke dala file cuckoo yang telah di run sebelumnya 

2. Ubah file cuckoo.conf `$CWD/conf/cuckoo.conf`

3. Menjadi 

    ```
    machinery = virtualbox
    [resultserver]
    ip = 192.168.56.1 #This is the IP address of the host
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

