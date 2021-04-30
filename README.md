# CMPE283_HW2
1. I did this homework by myself.
2. Steps I took:
	1. Install Ubuntu 20.04 desktop on Fusion.
	2. Inside Ubuntu, go to github.com/torvalds/linux, fork the repo. Clone the repo.
	3. Open terminal in Ubuntu, cd into linux folder
	4. use "uname -a", get the current config file
	5. use "cp /boot/config-.... ./.config" to copy the config file to linux folder, make sure that the version of the config file match with result of previous commend.
	6. use "make oldconig" to update old config file, keep hitting under to use default values.
	7. go inside .config file, change CONFIG_SYSTEM_TRUSTED_KEYS's value to ""(empty)
	8. use "make -j 4 modules && make -j 4 && sudo make modules_install && sudo make install" to build everything, replace number with number of cpus you wish to use.
	9. reboot vm, you should see a different config version if you do "uname -a"

	10. use "sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager" to install kvm for ubuntu 20.04
	11. use "sudo adduser user1 libvirt" and "sudo adduser user1 libvirt-qemu" to add user to the groups
	12. restart vm, make sure to turn on vmx capability
	13. open virtual machine manager in ubuntu, download a new ubuntu iso in the vm, install a vm(vm1) inside the vm
	14. go to /linux/arch/x86/kvm open cpuid.c
	15. inside of kvm_emulate_cpuid add necessary code(initialize counter and time, catch 0x4fffffff, set eax, ebx, ecx to the correct value).
	16. go to /linux/arch/x86/kvm/vmx, open vmx.c
	17. initialize counter, time, use "rdtsc()"" to read time and calculate duration inside of vmx_handle_exit()
	18. use "make -j 4 modules && make -j 4 && sudo make modules_install && sudo make install" to build project again, and restart outter vm.
	19. run vm1 inside of vm. create a test file. use "gcc test.c -0 test" to compile the file. run with "./test"
3. the number of exit seem to increase at a stable rate. About 1 million exit for a vm reboot.
