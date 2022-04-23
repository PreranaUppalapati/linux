## Assignment 1

To create a Linux kernel module that will query various MSRs to determine virtualization features available in our CPU. This module will report (via the system message log) the features it discovers.

## Team Members :

Venkata Lakshmi Praneetha Moturi (SJSU ID: 015913495)
Prerana Uppalapati (SJSU ID: 015933138)

## Work implemented by each member ( Question 1)

Prerana Uppalapati :

Worked on building the kernel
Forked the Linux Repository
Made required changes to the files as suggested by Professor Larkin in the class assignment videos

Venkata Lakshmi Praneetha Moturi :
 - To create a local copy of Linux Kernel, downloaded and built the Linux modules and required libraries.
 - With sample outputs, Verified the code functionality if it's working or not.
 - Documentation work

# To-Do:

To Discover VMX Features

# Prerequisites: 

A machine capable of running Linux, with VMX virtualization features exposed.

# Implementation Steps Followed : ( Question 2)

1. Download and install VMWare Workstation 16 Player from https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html

2. Download and install Ubuntu from here https://ubuntu.com/download/desktop and allocate 8 GB RAM and at least 200 GB Storage Space.

3. Fork the master branch of Linux from Torvalds’s Repo https://github.com/torvalds/linux

4. Install git on Ubuntu by typing the following command in the terminal: $ sudo apt install git.

5. Clone the forked Linux git repo onto the home directory of the system by navigating to the forked git repo and then clicking on code and copy the HTTPS URL and then type the following command: $ git clone https://github.com/preranaupplapati/linux.git

6. Following are some of the commands I used to overcome the errors I encountered during the compilation of the cloned repo: 

7. $ sudo apt-get install gcc $ sudo apt-get install make

8. Next, navigate to the Linux directory and run the following command: Make menuconfig with $ This command will show up a window asking whether you want to load a certain kernel configuration; I just hit Exit.

9. Install the modules using the following command: $ sudo make INSTALL_MOD_STRIP=1 modules_install

10. After this I copied the Makefile and the cmpe283-1.c file into the linux/cmpe283/ directory to commit my changes in my repo.

11. Now using the following command: $ sudo insmod cmpe283-1.ko  to insert the cmpe283-1.ko file into the kernel and run the file.

12. The command: $ lsmod | grep cmpe283 to verify if it was inserted correctly and it displays "cmpe283_1 if inserted correctly "

13. The command: $ dmesg will print out the VMX features which I added into the file onto the terminal console.

14. Next, using the command: $ sudo rmmod cmpe283_1. I deleted the file from the kernel. This will print the Assignment 1 end print message after executing the dmesg command again.

## Output 

![WhatsApp Image 2022-04-22 at 8 32 36 PM](https://user-images.githubusercontent.com/89679306/164879218-a05791bb-0e15-4476-93c8-8e5d24a08c24.jpeg)


The final step is to add, commit and push the cmpe283-1.c and Makefile onto the forked git repository using the following commands: $ git add cmpe283-1.c Makefile $ git commit $ git push

![Screenshot from 2022-04-22 14-23-15](https://user-images.githubusercontent.com/51155654/164881230-1ff34d1b-afe6-4b97-babc-18e108693b60.png)
![Screenshot from 2022-04-22 15-59-39](https://user-images.githubusercontent.com/51155654/164881235-52750708-61e2-429e-9420-9be9e0fd6854.png)
![Screenshot from 2022-04-22 16-00-01](https://user-images.githubusercontent.com/51155654/164881238-a96d2411-7615-4972-8764-640d42a8e6ab.png)


## ASSIGNMENT 2

# Team Members :

Venkata Lakshmi Praneetha Moturi (SJSU ID: 015913495)

Prerana Uppalapati (SJSU ID: 015933138)

Modified the cpuid file, vmx file and test file according to the requirement.


# Work Implemented by each member

Prerana Uppalapati
-
![Screenshot from 2022-04-22 16-00-16](https://user-images.githubusercontent.com/51155654/164881241-6486fe52-65d0-4c1d-8f64-31ee7cc5c136.png)

![Screenshot from 2022-04-22 16-00-25](https://user-images.githubusercontent.com/51155654/164881243-f01d0830-45c5-4a76-9140-43b38374ad36.png)

![Uploading Screenshot from 2022-04-22 16-09-08.png…]()


Venkata Lakshmi Praneetha Moturi
- 

TO-DO :

The goal of this project is to modify the behavior of instruction processor  under the KVM hypervisor.
When a special CPUID "leaf function" is called, we need to modify the CPUID emulation code in KVM to report back more information.

For CPUID leaf function %eax=0x4FFFFFFF:
• Return the total number of exits (all types) in %eax
• Return the high 32 bits of the total time spent processing all exits in %ebx
• Return the low 32 bits of the total time spent processing all exits in %ecx
• %ebx and %ecx return values are measured in processor cycles

## Steps Followed :

Initial Setup
1. First Build environment https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel
2. Next, Clone the Kernel code from GitHub: git clone https://github.com/torvalds/linux.git
3. Now, for Kernel Code Compilation : use
uname -a
cp /boot/config-5.8.0-43-generic ./.config
make oldconfig
make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install
reboot
Verify the updated Linux version: uname -a

Then to build follow, Modify cpuid.c and vmx.c and Compile using: make -j 2 modules && make -j 2 && sudo make modules_install && sudo make install

Now to Setup KVM, first Install KVM and supporting packages: sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils then Install the virt-manager using: sudo apt-get install virt-manager and Reboot

Created nested VM by - Using virt-manager to create nested virtual machine
 and Install Ubuntu in nested VM


Test: 
First Write test.c Next, Install gcc https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/ And Compile test file: gcc test.c then Check output

Then Check host VM kern.log: tail -n20 /var/log/kern.log

![WhatsApp Image 2022-04-22 at 8 32 36 PM (1)](https://user-images.githubusercontent.com/89679306/164880122-b10f9587-8ac9-4dc0-bc03-1c63a5e416f0.jpeg)

![WhatsApp Image 2022-04-22 at 8 32 36 PM (2)](https://user-images.githubusercontent.com/89679306/164880264-fbebe7ba-5dc0-4e47-8d90-210801e81b87.jpeg)

![WhatsApp Image 2022-04-22 at 8 32 36 PM (3)](https://user-images.githubusercontent.com/89679306/164880400-43416723-9ad9-43ff-802f-22338513dd70.jpeg)

![WhatsApp Image 2022-04-22 at 8 32 37 PM](https://user-images.githubusercontent.com/89679306/164880468-4f7511a1-a2e0-4853-b49f-4f760b441309.jpeg)
![WhatsApp Image 2022-04-22 at 8 32 37 PM (1)](https://user-images.githubusercontent.com/89679306/164880560-a47907ea-e2ff-4148-970d-63a5ce3cfe50.jpeg)

## 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?

Answer : No, the number of exits doesnot increase at a stable rate but unstable rate.
