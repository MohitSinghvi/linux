# CMPE-283 Assignment 3
# Modify proccessor behaviour inside KVM hypervisor

To modify the CPUID emulation code in KVM to report back additional information when special CPUID leaf nodes are requested.

For CPUID leaf node %eax=0x4FFFFFFD:

	Return the number of exits for the exit number provided (on input) in %ecx ▪ This value should be returned in %eax
 
For CPUID leaf node %eax=0x4FFFFFFC:

	Return the time spent processing the exit number provided (on input) in %ecx
 
	Return the high 32 bits of the total time spent for that exit in %ebx
 
	Return the low 32 bits of the total time spent for that exit in %ecx

Team
Mohit Mahendra Singhvi
Kushal Sai Vema

# Questions

Contribution : For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself). 
	
 Mohit Mahendra Singhvi:
		
  • I uploaded the completed files to Git and replicated them in a virtual machine (VM). 
		
  • I carried out the necessary procedures both in the outer and inner VM, capturing relevant code snippets along the way. 
		
  • Lastly, I engaged in a discussion about the questions and their corresponding answers related to the assignment.
	<br>
 Kushal Sai Vema: 
		
  • I understood the modifications needed for Assignment 3 and proceeded to incorporate them. 
		
  • Leveraging the foundational files from Assignment 2, specifically cpuid.c and vmx.c, I made the necessary adjustments to align them with the requirements of Assignment 3. 
    
  • Engaging in discussions related to the assignment questions and answers, I subsequently crafted documentation and updated the README.md file.

# Steps: Describe in detail the steps you used to complete the assignment.

		• Turn on the VM instance created during assignment 1.
![image](https://github.com/MohitSinghvi/linux/assets/35193178/3242179f-832d-4f5c-bb89-10dc4ef4e95f)
    • Fork the Linux repository to personal account: https://github.com/torvalds/linux.git <br>
    
		• Clone the forked repo in the gcp instance <br>
  
		• Execute "sudo bash" to enter root mode <br>
  
		• Execute "apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev"  to install the required package. <br>
  
		• Check current os info: uname -a <br>
  
		• Execute sudo make oldconfig <br>
  
		• sudo make -j <br>
  
		• sudo make modules <br>
  
		• sudo make install <br>
  
		• sudo make modules_install <br>
  
		• sudo reboot <br>
  
		• Verify updated linux version uname -a <br>
  
		• Modified cpuid.c and vmx.c files <br>
  
		• Executed sudo make -j && make modules && make install && make modules_install <br>
![Screenshot 2023-12-17 at 5 18 05 PM](https://github.com/MohitSinghvi/linux/assets/35193178/479bf92c-44c7-4474-ac7f-a120ae169e7d)

  
  
		• Connect to the gcp instance using the Chrome remote desktop <br>
  
		• On the remote, install virtual manager, and add Ubuntu as a guest operating system on top of this instance.<br>

![image](https://github.com/MohitSinghvi/linux/assets/35193178/ab51f920-7a86-4c02-be89-4b66ceb0b551)

		• On the guest ubuntu, installed cpuid package
  
		• Executed the cpuid commands to run the changes and view the register content on the guest OS
  
		• Executed the cpuid command to run the changes
  
cpuid -l  0x4FFFFFFD -s {{exitNumber}}
  
cpuid -l  0x4FFFFFFC -s {{exitNumber}}


<br>Q3.</br> Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?

The frequency of exits kept increasing steadily not necessarily a linear rise. Observed significant increase in exit numbers after rebooting the inner VM. After a full VM boot, approximately 3973521 exits occurred.

<br>
Q4.</br> Of the exit types defined in the SDM, which are the most frequent? Least?

CPUID(10) and I/O(30) exit types were the most frequent, 

CPUID (10) - [157,989], and I/O instruction (30) -- [254,784] 

Exception(0) exit type was the least frequent

Many exits did not occur at all like MOV DR(29), XSETBV(55), APIC Access(44)
