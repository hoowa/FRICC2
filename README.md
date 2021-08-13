FRICC2

---

1. What's FRICC2?
   FRICC2 is a PHP Script encryption tool. When you are developing a commercial software using PHP, the script can be distributed as encrypted up until just before execution. Thanks for php-screw and screw-plus project.

   
   
2. Features

   1. Less file handle open or read.
   2. Compress supported, small size of target files.
   3. Fix serval memory Leak.
   4. More performance when php open files.
   5. Supported Bundle in PHP with static.
   6. Tested on Ubuntu / Openwrt.
   7. Tested in x86_64 / MIPS / ARM Processors.
   
3. Requirement

   1. PHP Version
      
      | PHP Version           | Status          | Notice                                               |
      | --------------------- | --------------- | ---------------------------------------------------- |
      | >= 7.4.0              | Static / Shared | Recommand                                            |
      | >= 7.0.0 and <= 7.4.0 | Static / Shared | Runtime Little Memory Leak (auto free when php exit) |
      | < 7.0.0               | NO TEST         | NO TEST                                              |
      
   2. ZLIB Support in PHP
      PHP must be compiled with the "--with-zlib" option.
      Check that PHP has zlib compiled in it with the PHP script:
      
      ```php
      <?php
          gzopen();
      ?>
      ```
      
      If PHP knows about the function you can happily proceed.
      
   3. UNIX like OS (LINUX, FreeBSD, etc. are included) .

      

4. Installation

   Get Source

   ```bash
   git clone https://github.com/hoowa/FRICC2.git
   cd FRICC2
   ```

   Change KEY / TAG (Recommend)

   ```bash
   # Edit fricc2load/fricc2_lib.h
   
   # Change TAG with your own string(example):
   #define FRICCTAG_STR    "HOOWA"
   #define FRICCTAG_LEN    5
   
   # Change New KEY(example):
   #define FRICCKEY 1,2,3,4,5,6,7,8
   ```

   Build Encoder Program

   ```bash
   cd fricc2/
   make
   cp fricc2 /usr/bin/
   # Syntax to encrypt php script code
   # Usage: ./fricc2 -o [target] [source]
   ```

   Build PHP Extension fricc2load (Optional Shared)

   ```bash
   cd friccload2/
   phpize
   ./configure
   make
   make install
   # Append this line to php.ini
   extension=fricc2load.so
   # Restart the web server / your php daemon
   # Test in CLI
   php -m|grep fricc2load
   ```

   Build PHP Extension fricc2load (Optional Bundled in PHP)

   ```bash
   # example of your php source in ~/php-7.4.22/
   cp -avf friccload2/ ~/php-7.4.22/ext
   cd ~/php-7.4.22
   buildconf --force
   # append --enable-fricc2load=static --with-zlib to configure
   # example ./configure --enable-fricc2load=static --with-zlib
   # normal make and make install
   # check modules
   php -m|grep fricc2load
   ```

   

5. How To Use

   ```bash
   # Create test.php
   <?php
   echo "hello fricc2\n";
   ?>
   
   # Encode it
   fricc2 -o test_new.php test.php
   
   # Execute Test
   php ./test_new.php
   # Screen output:
   hello fricc2
   ```

   

6. Copyright
   Sun Bing <hoowa.sun@gmail.com>

