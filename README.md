# Pintos Installation
For the installation and setup of Pintos, I followed the steps mentioned [here](https://tssurya.wordpress.com/2014/08/16/installing-pintos-on-your-machine/)
All the steps performed for this installation and the issues and errors faced along with their solutions are listed below:
NOTE: 
1. The library “stropts.h” is included in some files in pintos. This library does not work for latest Ubuntu versions after 18.04 (e.g. 20.04). So, I used Ubuntu version 14.04.
2. Replace /home/fatimamujahid with /home/your-user-name at all places in the document.

### Step 1: 
Install qemu on your machine using the command: 
* sudo apt-get install qemu

![Resource 1](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/1.png)

Run following commands to check if qemu was properly installed. 
* qemu
* qemu-system-x86 

commands did not work for me. 
* qemu-system-x86_64 

ran successfully and a qemu window popped up.

![Resource 2](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/2.png)
![Resource 3](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/3.png)

### Step 2: 
Download pintos from this [link](http://web.stanford.edu/class/cs140/projects/pintos/pintos.tar.gz)
Create a directory os-pintos in /home/fatimamujahid and paste the extracted pintos directory inside os-pintos.

![Resource 4](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/4.png)

### Step 3: 
Open the file pintos-gdb present in /home/fatimamujahid/os-pintos/pintos/src/utils and changed line number 4 to 
* GDBMACROS=/home/fatimamujahid/os-pintos/pintos/src/misc/gdb-macros

![Resource 5](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/5.png)

### Step 4: 
Open the Makefile present in the utils directory and replaced line number 5 by 
* LDLIBS = -lm

![Resource 6](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/6.png)

### Step 5: 
Use the 
* make 

command to compile the utils folder.

![Resource 7](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/7.png)

### Step 6: 
Open the file Make.vars present in /home/fatimamujahid/os-pintos/pintos/src/threads and changed the last line to 
* SIMULATOR = –qemu

![Resource 8](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/8.png)

### Step 7: 
Use the 
* make 

command to compile the pintos kernel in the threads directory.

![Resource 9](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/9.png)
![Resource 10](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/10.png)

### Step 8: 
Open the file pintos present in the utils directory and change line number 103 to 
* $sim = “qemu” if !defined $sim;

![Resource 11](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/11.png)

Change line number 259 to 
* my $name = find_file (“/home/fatimamujahid/os-pintos/pintos/src/threads/build/kernel.bin”);

![Resource 12](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/12.png)

Change line number 623 to 
* my (@cmd) = (‘qemu-system-x86_64’);

![Resource 13](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/13.png)

### Step 9: 
Open the file Pintos.pm present in the utils directory and change line number 362 to  
* $name = find_file (“/home/fatimamujahid/os-pintos/pintos/src/threads/build/loader.bin”) if !defined $name;

![Resource 14](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/14.png)

### Step 10: 
Run 
* pintos run alarm-multiple

command in the utils directory. (In my case, it was not recognized. I found the solution for this issue in the comment section of the link mentioned at the start of the document. Then I tried 
* ./pintos run alarm-multiple 

command which worked.) 
It will create 5 threads and the output will be displayed both in the terminal and in the qemu window.

![Resource pintos](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/pintos.png)
![Resource 15](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/15.png)
![Resource 16](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/16.png)
![Resource 17](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/17.png)
![Resource 18](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/18.png)

### Step 11: 
Open the file .bashrc present in /home/fatimamujahid using 
* ls -a | grep bashrc 

command and add 
* export PATH=$HOME/os-pintos/pintos/src/utils:$PATH 

at the end of this file and restart the terminal.

![Resource 19](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/19.png)
![Resource 20](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/20.png)

### Step 12: 
Then run the following three commands to ensure successful pintos installation:
1. cd os-pintos/pintos/threads/src/threads
2. make
3. make check
The 'make' command compiles the code but in this case, as we have already run this command in the threads directory, so nothing will happen. The 'make check' runs all the tests for this project. (But here I encountered the timeout issue. All the tests got a timeout fault.) 

![Resource 21](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/21.png)
![Resource 22](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/22.png)
![Resource 23](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/23.png)

(To solve the timeout problem, I opened shutdown.c present in /home/fatimamujahid/os-pintos/pintos/src/devices and added outw (0xB004, 0x2000); after line number 104 in the
function shutdown_power_off(). Then ran the 'make' and 'make check' commands again in the threads directory.)
The output screenshots are shown below in which all the tests run, and the final result will be displayed, indicating the number of failed and passed tests.

![Resource 24](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/24.png)
![Resource 25](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/25.png)
![Resource 26](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/26.png)
![Resource 27](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/27.png)
![Resource 28](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/28.png)
![Resource 29](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/29.png)
.
.
.
![Resource 30](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/30.png)
![Resource 31](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/31.png)
![Resource 32](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/32.png)
![Resource 33](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/33.png)

20 of 27 tests failed and the remaining passed. This is the output required. 
Hence, Pintos will be successfully installed.
