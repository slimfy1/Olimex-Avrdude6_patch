# Olimex AVR-ISP-MK2 patch for Avrdude 6.0+
For those people, who have problem with Olimex AVR-ISP-MK2 using avrdude version 6.0+. In repos you can find avrdude with path for Linux user and for Windows users. (http://www.labor19.net/index.php/microcontroller/44-avrdude-patch - thank author for help!)

![alt text](http://json.tv/public/images/general/2016/08/05/thumbnail-20160805052419-1873.jpg)

//FOR WINDOWS USERS//
You can download compiled by me version of avrdude6.3, but if you want you can compile it by yourself.

__HOWTO__

1. Download latest avrdude with tar extension and unzip it somewhere(for example, "C:\avrdude-6.3"),
2. Download MinGW and install it with C++ options,
3. Download patch move it to avrdude folder - (https://savannah.nongnu.org/file/endpointdetect_pass1.patch?file_id=32171 if you can't dowload it from repo)
4. Download binary release of libusb-win32 (in my case libusb-win32-bin-1.2.3.0.zip) - (http://sourceforge.net/projects/libusb-win32/ if you can't download it from repo),
5. Copy from libusb package:
  include\usb.h    -> C:\MinGW\include\
  lib\gcc\libusb.a -> C:\MinGW\lib\
  bin\x86\libusb0_x86.dll (or other depending on your OS) -> C:\MinGW\bin\
6. Now you need to open MinGW terminal. Location of it (if you don't change settings) "C:\MinGW\msys\1.0\msys.bat"
7. Now you in MinGW terminal. First we use "cd" command to go to folder (For example, "cd C:\avrdude-6.3")
8. If you did all right you will see in terminal something like "User@WIN-E1N7C5DGBH5 /c/avrdude-6.3". Now we need to compile avrdude and download patch.
9. In terminal type:

  1)
  ```
  ./bootstrap
  ```
  you will see somethink like:
    
      + rm -rf autom4te.cache
      + libtoolize
      libtoolize: `./ltmain.sh' is newer: use `--force' to overwrite
      libtoolize: `m4/ltversion.m4' is newer: use `--force' to overwrite
      + aclocal
      + autoheader
      + autoconf
      + automake -a -c

   2)
   ```
   autoreconf --force --install
   ```
   you will see somethink like:
    
      $ autoreconf --force --install
      libtoolize: putting auxiliary files in `.'.
      libtoolize: copying file `./ltmain.sh'
      libtoolize: putting macros in AC_CONFIG_MACRO_DIR, `m4'.
      libtoolize: copying file `m4/libtool.m4'
      libtoolize: copying file `m4/ltoptions.m4'
      libtoolize: copying file `m4/ltsugar.m4'
      libtoolize: copying file `m4/ltversion.m4'
      libtoolize: copying file `m4/lt~obsolete.m4'
      
  3)
  ```
  cat endpointdetect_pass1.patch | patch -p0
  ```
  you will see somethink like:
      
      $  cat endpointdetect_pass1.patch | patch -p0
      patching file jtagmkII.c
      patching file stk500v2.c
      Hunk #1 succeeded at 1640 (offset 43 lines).
      Hunk #2 succeeded at 1698 (offset 43 lines).
      Hunk #3 succeeded at 3400 (offset 39 lines).
      Hunk #4 succeeded at 3511 (offset 39 lines).
      Hunk #5 succeeded at 3589 (offset 39 lines).
      patching file usb_libusb.c
      Hunk #2 succeeded at 243 (offset 7 lines).
      patching file usbdevs.h
 
  4)
  ```
  ./configure
  ```
  you will see a lot of text.If all is ok you will see:
    
        Configuration summary:
        ----------------------
        DON'T HAVE libelf
        DO HAVE    libusb
        DON'T HAVE libusb_1_0
        DON'T HAVE libftdi1
        DON'T HAVE libftdi
        DO HAVE    libhid
        DON'T HAVE pthread
        DISABLED   doc
        ENABLED    parport
        DISABLED   linuxgpio
    
  5)
  ```
  make
  ```
    
        make[2]: Leaving directory `/c/avrdude-6.3/windows'
        make[1]: Leaving directory `/c/avrdude-6.3'
  
  6)Thats all. At the end of compiling you can see, that you have no problem. If folder you need "avrdude.exe" and "avrdude.conf". Now       you can use Olimex with Avrdude6+.
      
        
![alt text](http://penguin.su/im_pic_article/123.jpg)

//FOR LINUX USERS//
You can download compiled by me version of avrdude6.3, but if you want you can compile it by yourself.

__HOWTO__

1. Download latest avrdude with tar extension and unzip it somewhere(for example, "/home/user/Document"),
2. Intall "make" (for Ubuntu "sudo apt-get install make"),
3. Open terminal and "cd" to avrdude source folder (for example, "/home/user/Document/avrdude-6.3"),
5. Download patch move it to avrdude folder - (https://savannah.nongnu.org/file/endpointdetect_pass1.patch?file_id=32171 if you can't dowload it from repo)
6. In terminal type:
  1)./bootstrap
  2)autoconf
  3)cat endpointdetect_pass1.patch | patch -p0
  4)make
  5)sudo make install
7. Now you can use avrdude in terminal.
