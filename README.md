## Assignment 1

To create a Linux kernel module that will query various MSRs to determine virtualization features available in our CPU. This module will report (via the system message log) the features it discovers.

## Team Members :

Venkata Lakshmi Praneetha Moturi (SJSU ID: 015913495)
Prerana Uppalapati (SJSU ID: 015933138)

## Work implemented by each member ( Question 1)

Prerana Uppalapati :

- Worked on building the kernel
- Forked the Linux Repository
- Made required changes to the files as suggested by Professor Larkin in the class assignment videos
- Worked on the documentation

Venkata Lakshmi Praneetha Moturi :
 - To create a local copy of Linux Kernel, downloaded and built the Linux modules and required libraries.
 - With sample outputs, Verified the code functionality if it's working or not.
 - Documentation work
 - Generated output files and made commits to git.

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
15. 
![Screenshot from 2022-04-22 23-26-32](https://user-images.githubusercontent.com/51155654/164882930-23b9a20e-35df-473c-a8e7-bbd526d1de52.png)



## Output 


The final step is to add, commit and push the cmpe283-1.c and Makefile onto the forked git repository using the following commands: $ git add cmpe283-1.c Makefile $ git commit $ git push

![Screenshot from 2022-04-22 14-23-15](https://user-images.githubusercontent.com/51155654/164881230-1ff34d1b-afe6-4b97-babc-18e108693b60.png)

![Screenshot from 2022-04-22 15-59-39](https://user-images.githubusercontent.com/51155654/164881235-52750708-61e2-429e-9420-9be9e0fd6854.png)

![Screenshot from 2022-04-22 16-00-01](https://user-images.githubusercontent.com/51155654/164881238-a96d2411-7615-4972-8764-640d42a8e6ab.png)



![Screenshot from 2022-04-22 16-00-16](https://user-images.githubusercontent.com/51155654/164882779-04cfad5c-e659-43bc-8924-3cdc510b0db5.png)
![Screenshot from 2022-04-22 16-00-25](https://user-images.githubusercontent.com/51155654/164882782-0c67e994-869b-48d0-a217-141029ed34f6.png)

-------------------------------------------------------------------------------------------


## ASSIGNMENT 2

# Team Members :

Venkata Lakshmi Praneetha Moturi (SJSU ID: 015913495)

Prerana Uppalapati (SJSU ID: 015933138)


# Work Implemented by each member ( Question 1)

Prerana Uppalapati
- Modified the vmx file and test file according to the requirement.


Venkata Lakshmi Praneetha Moturi
- Modify the cupid.c file
- Install Virtual Machine Manager on the VM.
- Install ubuntu on a inner VM using Virtual machine manager.
- Install the cupid package on the innervm.

TO-DO :

The goal of this project is to modify the behavior of instruction processor  under the KVM hypervisor.
When a special CPUID "leaf function" is called, we need to modify the CPUID emulation code in KVM to report back more information.

For CPUID leaf function %eax=0x4FFFFFFF:
• Return the total number of exits (all types) in %eax
• Return the high 32 bits of the total time spent processing all exits in %ebx
• Return the low 32 bits of the total time spent processing all exits in %ecx
• %ebx and %ecx return values are measured in processor cycles

## Steps Followed : (Question 2)

Build Initial Setup
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

Answer : No, the number of exits doesnot increase at a stable rate but unstable rate. Other VM operations, such as EPT violation, RDRAND, I/O instructions, RDTSCP, and so on, exits are executed. After the first build, rebooting, and using KVM to enter the nested VM, there were 156,411 exits. Because there may be a shutdown time with a hardware disruption in between, this may not be very accurate.


## Assignment 3 :

## Description : 

Focuses on modifying the CPUID emulation code in KVM so that when a special CPID leaf node is requested, additional details will be reported back.

## Team Members :

Prerana Uppalapati (015933138)
- Using cpuid package in the inner VM, tested the modifications made for leaf nodes 
- 

Praneetha Moturi ( 015913495)
- Based on findings, modified vmx.c file.
- Modified cupid.c file


## Steps To Implement:

- Use Code from assignment 2 as a base code.
- Implement the functionality for tax = 0x4FFFFFFD and 0x4FFFFFFC by adding the code in vmx.c and cupid.c.
- make -j 8 modules
- sudo bash
- make INSTALL_MOD_STRIP=1 modules_install && make install
- lsmod | grep kvm
- rmmod kvm_intel; rmmod kvm
- modprobe kvm_intel; modprobe kvm

## Testing

- Start nested vm - CentOS
sudo virsh start centOSvm

sudo virsh console centOSvm
* Install cpuid in L1 VM
sudo yum -y install cpuid
* Run cpu commands
cpuid -l 0x4ffffffd -s <exit_number>
cpuid -l 0x4ffffffc -s <exit_number>

for i in `seq 0 69`; do cpuid -l 0x4ffffffd -s $i; done -- for all exit counts


## Obervation :

- Comment on exit frequency – does the number of exits increase at a consistent rate? Or do some VM processes require more exits than others? How many exits does a full VM boot entail on average?
- Approximately 700,000 exits were caused by a full boot. When queried within 5-10 seconds and no operations were being conducted (Refer 1 and Refer 2), the increase in the number of exits was very consistent. When you run multiple commands (top, ping, du) and work with it, the exits tend to increase at a faster rate.
- Which of the exit types defined in the SDM is the most common or Least?
- The following were some of the least(0) exits: 3 - INIT signal, 4 - SIPI,2 - Triple Fault, 6 - Other SMI Some of the most frequent exits were: 10 - CPUID, 28 - Control register access, 30 - I/O instruction , 48 - EPT violation.(Screenshot_1 and Screenshot_2)


## 3. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?

Answer:
The number of exits does not increase at a constant rate, as evidenced by the results of the first and second runs. Exits will be generated by operations such as External Interrupt, I/O instruction, and so on. Approximately 1,500,000 people.

## 4. Of the exit types defined in the SDM, which are the most frequent? Least?

Answer:
The most frequent exit types include external interrupt, cpuid, I/O instruction, and so on. MOV DR, INVD, and other exit types are the least frequent.

![image](https://user-images.githubusercontent.com/89679306/166095108-c4f24d60-6db0-4ba5-80dd-ceeddab01c13.png)

![image](https://user-images.githubusercontent.com/89679306/166095111-6b27fb44-01b5-485d-b4a5-d4127d1716b9.png)

![image](https://user-images.githubusercontent.com/89679306/166095113-09324a03-343c-4ac9-8c51-e25ad3b51e34.png)



## Assignment-4

## T0-D0:

To demonstrate the performance differences between nested paging and shadow paging, as well as the various exit frequencies and types

## Team Members :

Prerana Uppalapati (015933138)
* Made changes to configure shadow paging instead of nested paging

Praneetha Moturi ( 015913495)
* Note the exit counts with assignment 3 configuration and record observations

We had a meeting at library and did this research together. All the mentioned and performed steps are discussed and completed by both of us.


## Steps Used To Build 


- First setup Assignment-3 
- To see the current count of exits for all the exit reasons, run dmesg command 
With EPT :

SS

With ept =0 after insterting the module :

Ss


1. Test nested paging
Boost nested VM
Run test_assignment3.c in nested VM
Paste result in assignment4_nested.txt
Shut down nested VM

2. Test shadow paging Remove kvm-intel module from your running kernel sudo rmmod kvm-intel Reload kvm-intel module with the parameter ept=0 Sudo insmod /lib/modules/5.12.0+/kernel/arch/x86/kvm/kvm-intel.ko ept=0

3. Boost the same nested VM
4. Run test_assignment3.c in nested VM
5. Paste result in assignment4_shadow.txt
6. Shut down nested VM


## What did you learn from the count of exits? Was the count what you expected? If not, why not?

Observations:

After monitoring the exits in nested paging, the output of exits is not what we expected. We find a lot of exits with shadow paging for some of the exits that were very low or not there in the case of layered paging.

In contrast to what we see in nested paging, we do not see EPT exits in shadow paging, but we do see most exits in the case of CR ACCESS. There are also exits for INVLPG and INVPCID. In the instance of CR ACCESS, we witness a lot of exits because the hypervisor now takes exit when the control register is accessed, and during INVLPG, we see a lot of exits because the hypervisor takes exit to invalidate translations in the TLB.



## What changed between the two runs (ept vs no-ept)?

The number of exits for shadow paging (without ept) continues to grow in comparison to nested paging (with ept).

WITH EPT

![image](https://user-images.githubusercontent.com/89679306/166095125-65400f82-8c6b-48c6-9565-c8c5a10d8f52.png)

With EPT = 0

![image](https://user-images.githubusercontent.com/89679306/166095138-765550f3-f0ef-4d68-a46d-de4733364410.png)


