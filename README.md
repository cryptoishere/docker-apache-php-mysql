<!-- Try this to fix slow mysql loading -->
https://phpforus.com/how-to-make-mysql-run-fast-with-ext4-on-ubuntu/
I had performance issues when was working with MySQL server on UBUNTU machine. My application was running very slow.  Databases import was also very slow… If you have same issue to fix this you just need to do these steps:

    Disable writing barrier for the ext4 fs:

    $ sudo gedit /etc/fstab

    Here you’ll see something like this:

    UUID=b87de212-52ca-4600-9e30-6e80e24df1ed / ext4 errors=remount-ro 0 1

    So you just need to add barrier=0

    UUID=b87de212-52ca-4600-9e30-6e80e24df1ed / ext4 errors=remount-ro,barrier=0 0 1

    Reboot your system.

When I did these steps, my applications in local machine started working very fast.
I tried this on Linux mint 15, Ubuntu 12 and UBUNTU 13.

