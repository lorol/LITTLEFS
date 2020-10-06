# How to run on PlatformIO IDE

- Download and extract to project root a **mklittlefs** executable for your OS from a zipped binary [here](https://github.com/earlephilhower/mklittlefs/releases) 
- Open **LITTLEFS_PlatformIO** folder
- Run PlatformIO project task: **Upload Filesystem Image** 
- Run PlatformIO project task: **Upload and Monitor**
- You will see a Serial output like:
```
--- Miniterm on COM5  115200,8,N,1 ---
--- Quit: Ctrl+C | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---
Listing directory: /
  FILE: /file1.txt      SIZE: 3
  FILE: /test.txt       SIZE: 0
  DIR : /testfolder
Creating Dir: /mydir
Dir created
Writing file: /mydir/hello2.txt
- file written
Listing directory: /
  FILE: /file1.txt      SIZE: 3
  DIR : /mydir
Listing directory: /mydir
  FILE: /mydir/hello2.txt       SIZE: 6
  FILE: /test.txt       SIZE: 0
  DIR : /testfolder
Listing directory: /testfolder
  FILE: /testfolder/test2.txt   SIZE: 3
Deleting file: /mydir/hello2.txt
- file deleted
Removing Dir: /mydir
Dir removed
Listing directory: /
  FILE: /file1.txt      SIZE: 3
  FILE: /test.txt       SIZE: 0
  DIR : /testfolder
Listing directory: /testfolder
  FILE: /testfolder/test2.txt   SIZE: 3
Writing file: /hello.txt
- file written
Appending to file: /hello.txt
- message appended
Reading file: /hello.txt
- read from file:
Hello World!
Renaming file /hello.txt to /foo.txt
- file renamed
Reading file: /foo.txt
- read from file:
Hello World!
Deleting file: /foo.txt
- file deleted
Testing file I/O with /test.txt
- writing................................................................
 - 1048576 bytes written in 11369 ms
- reading................................................................
- 1048576 bytes read in 523 ms
Deleting file: /test.txt
- file deleted
Test complete
```
- If you have a module with more than 4MB flash, you can uncomment **partitions_custom.csv** in **platformio.ini** and modify the csv file accordingly