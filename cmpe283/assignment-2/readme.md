# CMPE-283 Assignment 2
# Modify proccessor behaviour inside KVM hypervisor

<b>For CPUID leaf node %eax=0x4FFFFFFF:</b>

Return the total number of exits (all types) in %eax


<b>For CPUID leaf node %eax=0x4FFFFFFE:</b>

Return the high 32 bits of the total time spent processing all exits in %ebx

Return the low 32 bits of the total time spent processing all exits in %ecx

%ebx and %ecx return values are measured in processor cycles, across all VCPUs

Team
Mohit Mahendra Singhvi
Kushal Sai Vema


# Questions
1.  Contribution : For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself). 
	
 Mohit Mahendra Singhvi:
		
		• Compiled the kernel and installed essential modules within it.

		• Conducted a thorough examination and research into the assignment's codebase.

		• Implemented the discussed modifications into the code.

		• Developed and compiled test files to validate the changes.

		• Produced comprehensive documentation and updated the README.md file.
		
Kushal Sai Vema: 

		• Successfully compiled the kernel.

		• Gained clarity on the required procedures by revisiting the lecture available on Canvas.

		• Conducted research on the cpuid instruction and CPU leaf nodes.

		• Identified specific areas for modification and understood the necessary changes for implementing the assignment.

3. Steps: Describe in detail the steps you used to complete the assignment.

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
  
		• cpuid -l  0x4FFFFFFF, cpuid -l  0x4FFFFFFE


3. Does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations?
   
		• No, the count of exits does not exhibit a consistent growth pattern.

		• Various virtual machine instructions and operations trigger exits,
including but not limited to EPT violation, RDRAND, I/O instructions, RDTSCP, and others.

5. Of the exit types defined in the SDM, which are the most frequent? Least?

    • The most frequent exit types for us :
   
    CPUID (10) - [127,581], and I/O instruction (30) -- [215,413] 

    • Least frequent exit types: 
   
    MOV DR (29) - 2



  





