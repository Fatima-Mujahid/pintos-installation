# pintos-installation
In this lab, for the installation and setup of Pintos I followed the steps mentioned in this link:
https://tssurya.wordpress.com/2014/08/16/installing-pintos-on-your-machine/
All the steps performed for this installation and the issues and errors faced along with their solutions are listed below:
NOTE: The library “stropts.h” is included in some files in pintos. This library does not work for latest Ubuntu versions after 18.04 (e.g. 20.04). So, I used Ubuntu version 14.04.
Step 1: I installed qemu on my machine using the command sudo apt-get install qemu.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/1.png)

I tried to run some commands to check if qemu was properly installed. qemu and qemu-system-x86 commands did not work for me. qemu-system-x86_64 ran successfully and a qemu window popped up.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/2.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/3.png)

Step 2: I downloaded pintos using the following link:
http://web.stanford.edu/class/cs140/projects/pintos/pintos.tar.gz
Then I created a directory os-pintos in /home/fatimamujahid and pasted the extracted pintos directory inside os-pintos.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/4.png)

Step 3: I opened the file pintos-gdb present in /home/fatimamujahid/os-pintos/pintos/src/utils and changed line number 4 to GDBMACROS=/home/fatimamujahid/os-pintos/pintos/src/misc/gdb-macros.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/5.png)

Step 4: I opened the Makefile present in the utils directory and replaced line number 5 by LDLIBS = -lm.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/6.png)

Step 5: I used the make command to compile the utils folder.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/7.png)

Step 6: I opened the file Make.vars present in /home/fatimamujahid/os-pintos/pintos/src/threads and changed the last line to SIMULATOR = –qemu.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/8.png)

Step 7: I used the make command to compile the pintos kernel in the threads directory.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/9.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/10.png)

Step 8: I opened the file pintos present in the utils directory and changed line number 103 to $sim = “qemu” if !defined $sim;.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/11.png)

Then I changed line number 259 to my $name = find_file (“/home/fatimamujahid/os-pintos/pintos/src/threads/build/kernel.bin”);.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/12.png)

Then I changed line number 623 to my (@cmd) = (‘qemu-system-x86_64’);.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/13.png)

Step 9: I opened the file Pintos.pm present in the utils directory and changed line number 362 to  $name = find_file (“/home/fatimamujahid/os-pintos/pintos/src/threads/build/loader.bin”) if !defined $name;.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/14.png)

Step 10: I ran pintos run alarm-multiple command in the utils directory, but it was not recognized. I found the solution for this issue in the comment section of the link mentioned at the start of the document. Then I tried ./pintos run alarm-multiple command and it created 5 threads and the output was displayed both in the terminal and in the qemu window.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/pintos.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/15.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/16.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/17.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/18.png)

Step 11: I opened the file .bashrc present in /home/fatimamujahid using ls -a | grep bashrc command and added export PATH=$HOME/os-pintos/pintos/src/utils:$PATH at the end of this file and restarted the terminal.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/19.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/20.png)

Step 12: Finally, I used the starter code given in the lab manual and ran the following three commands:
i) cd os-pintos/pintos/threads/src/threads
ii) make
iii) make check
The make command compiles the code but in this case, I had already run this command in the threads directory, so nothing happened. The make check ran all the tests for this project. But here I encountered the timeout issue. All the tests got a timeout fault. 

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/21.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/22.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/23.png)

To solve this problem, I opened shutdown.c present in /home/fatimamujahid/os-pintos/pintos/src/devices and added outw (0xB004, 0x2000); after line number 104 in the
function shutdown_power_off(). Then I ran the make and make check commands again in the threads directory. The output screenshots are shown below in which all the tests ran, and the final result displayed the number of failed and passed tests.

![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/24.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/25.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/26.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/27.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/28.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/29.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/30.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/31.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/32.png)
![Image of Yaktocat](https://github.com/Fatima-Mujahid/pintos-installation/blob/main/Resources/33.png)

20 of 27 tests failed and the remaining passed. This was the output required as mentioned in the lab manual. 
Hence, Pintos was successfully installed, and the starter code worked perfectly fine and produced the desired output.
