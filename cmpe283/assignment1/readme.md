# CMPE-283 Assignment 1  
# Discovering VMX Features : Learn how to discover VMX features present in your processor by writing a Linux kernel module that queries these features. 

#Team
Mohit Mahendra Singhvi
Kushal Sai Vema

#Questions
	1.  Contribution : For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself). 
	
Mohit Mahendra Singhvi: I performed gcp setup, forked the linux git repo and cloned it on the instance, researched Intel SDM for the entry, exit and primary procbased vmexit controls and added the struct and logic to print the info to the files cmpe-283-1.c 
	
Kushal Sai Vema: Helped with researching for the vm exit controls for secondary and ertiary procbased control and collaborated in running and executing the changes made to cmpe-283-1.c
	
  Steps: Describe in detail the steps you used to complete the assignment.

		a. Forked the github repository https://github.com/torvalds/linux into your github account
		b. Created a gcp instance with support for nested virtualization.
		c. SSH into the created repo and clone this repo
		d.  Copied the files cmpe283-1.c and the Makefile to the instance 
		e. Made changes to the cmpe283-1.c file to include struct for Entry / Exit / Procbased / Secondary Procbased / Tertiary Procbased / Pinbased controls. Also added the handling to report, i.e. print the capabilities on the screen.
		f. In the linux directory execute:
			i. make menuconfig
			ii. cp /boot/<config> .config
			iii. Sudo make oldconfig
			iv. sudo make prepare
			v. sudo make modules
			vi. sudo make
			vii. sudo make INSTALL_MOD_STRIP =1  modules_install
			viii. sudo reboot
			ix. sudo  make
			x. sudo insmod cmpe283-1.ko (loads the module)
			xi. dmesg (To view the log entries on execution)
			xii. Screenshot:
   ![image](https://github.com/MohitSinghvi/linux/assets/35193178/01c3cccb-1cde-4ccc-b3b7-060c1a797614)

   Output: 
		[68528.985483] CMPE 283 Assignment 1 Module Start
		[68528.990045] Pinbased Controls MSR: 0x7f00000016
		[68528.994680]   External Interrupt Exiting: Can set=Yes, Can clear=Yes
		[68529.001138]   NMI Exiting: Can set=Yes, Can clear=Yes
		[68529.006292]   Virtual NMIs: Can set=Yes, Can clear=Yes
		[68529.011545]   Activate VMX Preemption Timer: Can set=Yes, Can clear=Yes
		[68529.018263]   Process Posted Interrupts: Can set=No, Can clear=Yes
		[68529.024551] Entry Controls MSR: 0x1d3ff000011ff
		[68529.029185]   Save debug controls: Can set=Yes, Can clear=No
		[68529.034951]   Host address-space size: Can set=Yes, Can clear=Yes
		[68529.041146]   Load IA32_PERF_GLOBAL_CTRL: Can set=Yes, Can clear=No
		[68529.047533]   Acknowledge interrupt on exit: Can set=Yes, Can clear=Yes
		[68529.054261]   Save IA32_PAT: Can set=No, Can clear=Yes
		[68529.059503]   Load IA32_PAT: Can set=No, Can clear=Yes
		[68529.064746]   Save IA32_EFER: Can set=No, Can clear=Yes
		[68529.070075]   Load IA32_EFER: Can set=No, Can clear=Yes
		[68529.075403]   Save VMX-preemption timer value: Can set=No, Can clear=Yes
		[68529.082210]   Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
		[68529.087887]   Conceal VMX from PT: Can set=No, Can clear=Yes
		[68529.093650]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
		[68529.099417]   Load CET state: Can set=No, Can clear=Yes
		[68529.104746]   Load PKRS: Can set=No, Can clear=Yes
		[68529.109644] Exit Controls MSR: 0xffefff00036dff
		[68529.114279]   Save debug controls: Can set=Yes, Can clear=No
		[68529.120043]   Host address space size: Can set=Yes, Can clear=Yes
		[68529.126244]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
		[68529.132625]   Acknowledge Interrupt on exit: Can set=Yes, Can clear=Yes
		[68529.139345]   Save IA32_PAT: Can set=Yes, Can clear=Yes
		[68529.144688]   Load IA32_PAT: Can set=Yes, Can clear=Yes
		[68529.150030]   Save IA32_EFER: Can set=Yes, Can clear=Yes
		[68529.155444]   Load IA32_EFER: Can set=Yes, Can clear=Yes
		[68529.160864]   Save VMX-preemption timer value: Can set=Yes, Can clear=Yes
		[68529.167755]   Clear IA32_BNDCFGS: Can set=Yes, Can clear=Yes
		[68529.173518]   Conceal VMX from PT: Can set=No, Can clear=Yes
		[68529.179283]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
		[68529.185045]   Clear IA32_LBR_CTL: Can set=No, Can clear=Yes
		[68529.190722]   Clear UNIV: Can set=No, Can clear=Yes
		[68529.195726]   Load CET state: Can set=No, Can clear=Yes
		[68529.201063]   Load PKRS: Can set=No, Can clear=Yes
		[68529.205958]   Save IA32_PREF_GLOBAL_CTL: Can set=No, Can clear=Yes
		[68529.212242]   Activate secondary controls: Can set=No, Can clear=Yes
		[68529.218702] Primary Processor based Controls MSR: 0xfff9fffe0401e172
		[68529.225160]   Interrupt-window exiting: Can set=Yes, Can clear=Yes
		[68529.231450]   Use TSC offsetting: Can set=Yes, Can clear=Yes
		[68529.237216]   HLT exiting: Can set=Yes, Can clear=Yes
		[68529.242377]   INVLPG exiting: Can set=Yes, Can clear=Yes
		[68529.247797]   MWAIT exiting: Can set=Yes, Can clear=Yes
		[68529.253128]   RDPMC exiting: Can set=Yes, Can clear=Yes
		[68529.258490]   RDTSC exiting: Can set=Yes, Can clear=Yes
		[68529.263819]   CR3-load exiting: Can set=Yes, Can clear=No
		[68529.269327]   CR3-store exiting: Can set=Yes, Can clear=No
		[68529.274918]   Activate tertiary controls: Can set=No, Can clear=Yes
		[68529.281303]   CR8-load exiting: Can set=Yes, Can clear=Yes
		[68529.286896]   CR8-store exiting: Can set=Yes, Can clear=Yes
		[68529.292573]   Use TPR shadow: Can set=Yes, Can clear=Yes
		[68529.297990]   NMI-window exiting: Can set=Yes, Can clear=Yes
		[68529.303755]   MOV-DR exiting: Can set=Yes, Can clear=Yes
		[68529.309172]   Unconditional I/O exiting: Can set=Yes, Can clear=Yes
		[68529.315547]   Use I/O bitmaps: Can set=Yes, Can clear=Yes
		[68529.321063]   Monitor trap flag: Can set=Yes, Can clear=Yes
		[68529.326743]   Use MSR bitmaps: Can set=Yes, Can clear=Yes
		[68529.332258]   MONITOR exiting: Can set=Yes, Can clear=Yes
		[68529.337763]   PAUSE exiting: Can set=Yes, Can clear=Yes
		[68529.343093]   Activate secondary controls: Can set=Yes, Can clear=Yes
		[68529.349642] Secondary Processor based Controls MSR: 0x1051ff00000000
		[68529.356100]   Virtualize APIC accesses: Can set=Yes, Can clear=Yes
		[68529.362382]   Enable EPT: Can set=Yes, Can clear=Yes
		[68529.367453]   Descriptor-table exiting: Can set=Yes, Can clear=Yes
		[68529.373864]   Enable RDTSCP: Can set=Yes, Can clear=Yes
		[68529.379199]   Virtualize x2APIC mode: Can set=Yes, Can clear=Yes
		[68529.385310]   Enable VPID: Can set=Yes, Can clear=Yes
		[68529.390480]   WBINVD exiting: Can set=Yes, Can clear=Yes
		[68529.395897]   Unrestricted guest: Can set=Yes, Can clear=Yes
		[68529.401681]   APIC-register virtualization: Can set=Yes, Can clear=Yes
		[68529.408313]   Virtual-interrupt delivery: Can set=No, Can clear=Yes
		[68529.414683]   Pause-loop exiting: Can set=No, Can clear=Yes
		[68529.420361]   RDRAND exiting: Can set=No, Can clear=Yes
		[68529.425694]   Enable INVPCID: Can set=Yes, Can clear=Yes
		[68529.431108]   Enable VM functions: Can set=No, Can clear=Yes
		[68529.436873]   VMCS shadowing: Can set=Yes, Can clear=Yes
		[68529.442293]   Enable ENCLS exiting: Can set=No, Can clear=Yes
		[68529.448142]   RDSEED exiting: Can set=No, Can clear=Yes
		[68529.453471]   Enable PML: Can set=No, Can clear=Yes
		[68529.458455]   EPT-violation #VE: Can set=No, Can clear=Yes
		[68529.464052]   Conceal VMX from PT: Can set=No, Can clear=Yes
		[68529.469816]   Enable XSAVES/XRSTORS: Can set=Yes, Can clear=Yes
		[68529.475840]   PASID translation: Can set=No, Can clear=Yes
		[68529.481444]   Mode-based execute control for EPT.: Can set=No, Can clear=Yes
		[68529.488598]   Sub-page write permissions for EPT: Can set=No, Can clear=Yes
		[68529.495664]   Intel PT uses guest physical addresses: Can set=No, Can clear=Yes
		[68529.503079]   Use TSC scaling: Can set=No, Can clear=Yes
		[68529.508494]   Enable user wait and pause: Can set=No, Can clear=Yes
		[68529.514864]   Enable PCONFIG: Can set=No, Can clear=Yes
		[68529.520193]   Enable ENCLV exiting: Can set=No, Can clear=Yes
		[68529.526042]   VMM bus-lock detection: Can set=No, Can clear=Yes
		[68529.532067]   Instruction timeout: Can set=No, Can clear=Yes
			

