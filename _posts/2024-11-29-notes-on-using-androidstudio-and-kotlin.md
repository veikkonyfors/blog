---
layout: default
title:  "Notes on using Android Studio with Kotlin"
description: "Notes on using Android Studio with Kotlin"
tag: Android & Kotlin
katex: true
---
# Notes on using Android Studio with Kotlin

Documenting events, issues, incidents and such with Android Studio and Kotlin along the way


- [Poor emulator performance](#poor-emulator-performance)
	- [Emulator config changes](#emulator-config-changes)
	- [Wipe data](#wipe-data)
	- [Removing locks](#removing-locks)
	- [changing AndroidStudio Emulated performance](#changing-androidstudio-emulated-performance)
	- [enable kvm acceleration](#enable-kvm-acceleration)
- [Disabling libvirtd tricks](#disabling-libvirtd-tricks)

## Poor emulator performance

Android AVD performance is getting worse and worse. Top is now showing 200% cpu usage for itmost of the time.
Below some actions, after which cpu usage dropped to 50%

### Emulator config changes
pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/config.ini:
hw.audioInput = no # 20241129 VN: was yes \\
hw.audioOutput = no # 20241129 VN: add this \\
hw.gps = no # 020241129 VN:  was yes

### Wipe data

AndroidStudio - Device Manager - <your AVD> - ... - Wipe data \\
Note, this will remove all data you have gathered on the device.

### Removing locks 

may help if there is a total hang

	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ ls -l ~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/*.lock
	-rw-rw-r-- 1 pappa pappa 0 marras 29 10:16 /home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/multiinstance.lock
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ rm ~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/*.lock
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ ls -l ~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/*.qc*
	-rw-r--r-- 1 pappa pappa  209453056 marras 29 10:20 /home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/cache.img.qcow2
	-rw-r--r-- 1 pappa pappa    2097221 marras 29 10:20 /home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/encryptionkey.img.qcow2
	-rw-r--r-- 1 pappa pappa     720965 marras 29 10:20 /home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/sdcard.img.qcow2
	-rw-r--r-- 1 pappa pappa 1187971072 marras 29 10:20 /home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/userdata-qemu.img.qcow2
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ rm ~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/*.qco*

### Changing AndroidStudio Emulated performance
AndroidStudio - device manager - edit with pencil symbol - Emulated performace Graphics: from auto to hardware GLES 2.0

### Enable kvm acceleration

This was crucial. Gave most of the performance improvement.

#### kvm must be enabled on ubuntu
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ sudo kvm-ok
	INFO: /dev/kvm exists
	KVM acceleration can be used
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ 

#### No indication of KVM acceleration on emulator's process started from within AndroidStudio

	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$ ps aux | grep qemu-system-x86_64
	pappa      42366  174 13.1 4589800 2123060 ?     Sl   11:38   2:19 /home/pappa/Android/Sdk/emulator/qemu/linux-x86_64/qemu-system-x86_64 -netdelay none -netspeed full -no-snapshot-load -avd 5inchphode64bitemu_API_Tiramisu -qt-hide-window -grpc-use-token -idle-grpc-timeout 300
	pappa      42699  0.0  0.0  11580   656 pts/0    S+   11:39   0:00 grep --color=auto qemu-system-x86_64
	pappa@pappa-ThinkPad-X270:~/.android/avd/5inchphode64bitemu_API_Tiramisu.avd$

#### libvirtd must be running
	sudo apt update
	sudo apt install -y libvirt-daemon-system libvirt-clients
	sudo systemctl start libvirtd
	sudo systemctl enable libvirtd # enable on boot
	sudo usermod -aG kvm pappa
	sudo usermod -aG libvirt pappa
	sudo apt install qemu-kvm bridge-utils virt-manager
	virsh list --all

#### Install required libraries to start emulator from command line

	pappa@pappa-ThinkPad-X270:~$
	Install all required libraries:
	sudo apt install -y libtcmalloc-minimal4
	sudo apt install -y qt5-default libqt5widgets5 libqt5webchannel5
	export LD_LIBRARY_PATH=~/Android/Sdk/emulator/lib64/qt/lib:$LD_LIBRARY_PATH # For libQt5WebChannelAndroidEmu.so.5
	export LD_LIBRARY_PATH=~/Android/Sdk/emulator/lib64:$LD_LIBRARY_PATH

#### Add '-accel on' parameter on command line

	pappa@pappa-ThinkPad-X270:~$ /home/pappa/Android/Sdk/emulator/qemu/linux-x86_64/qemu-system-x86_64 -netdelay none -netspeed full -no-snapshot-load -avd 5inchphode64bitemu_API_Tiramisu -qt-hide-window -grpc-use-token -idle-grpc-timeout 300 -verbose -accel on > qemu-system-x86_64.log 2>&1 &
	[1] 45894
	pappa@pappa-ThinkPad-X270:~$ ps aux | grep qemu-system-x86_64
	pappa      50027 64.3  3.1 3909692 513036 pts/1  Sl   13:37   0:05 /home/pappa/Android/Sdk/emulator/qemu/linux-x86_64/qemu-system-x86_64 -netdelay none -netspeed full -no-snapshot-load -avd 5inchphode64bitemu_API_Tiramisu -qt-hide-window -grpc-use-token -idle-grpc-timeout 300 -verbose -accel on
	pappa      50204  0.0  0.0  11580   720 pts/1    S+   13:37   0:00 grep --color=auto qemu-system-x86_64

In log file we now have indication kvm acceleration is in use

	pappa@pappa-ThinkPad-X270:~$ grep kvm qemu-system-x86_64.log # kvm is now shown in log as well
	INFO    | 	 argv[12] = "-enable-kvm"
	INFO    | Concatenated QEMU options: /home/pappa/Android/Sdk/emulator/qemu/linux-x86_64/qemu-system-x86_64 -dns-server 1.1.1.1,1.0.0.1,208.67.222.222,208.67.220.220 -mem-path /home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/snapshots/default_boot/ram.img -mem-file-shared -serial null -device goldfish_pstore,addr=0xff018000,size=0x10000,file=/home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/data/misc/pstore/pstore.bin -cpu android64-xts -enable-kvm -smp cores=2 -m 2048 -lcd-density 420 -object iothread,id=disk-iothread -nodefaults -kernel /home/pappa/Android/Sdk/system-images/android-Tiramisu/google_apis/x86_64//kernel-ranchu -initrd /home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/initrd -drive if=none,index=0,id=system,if=none,file=/home/pappa/Android/Sdk/system-images/android-Tiramisu/google_apis/x86_64//system.img,read-only -device virtio-blk-pci,drive=system,iothread=disk-iothread,modern-pio-notify -drive if=none,index=1,id=cache,if=none,file=/home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/cache.img.qcow2,overlap-check=none,cache=unsafe,l2-cache-size=1048576 -device virtio-blk-pci,drive=cache,iothread=disk-iothread,modern-pio-notify -drive if=none,index=2,id=userdata,if=none,file=/home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/userdata-qemu.img.qcow2,overlap-check=none,cache=unsafe,l2-cache-size=1048576 -device virtio-blk-pci,drive=userdata,iothread=disk-iothread,modern-pio-notify -drive if=none,index=3,id=encrypt,if=none,file=/home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/encryptionkey.img.qcow2,overlap-check=none,cache=unsafe,l2-cache-size=1048576 -device virtio-blk-pci,drive=encrypt,iothread=disk-iothread,modern-pio-notify -drive if=none,index=4,id=vendor,if=none,file=/home/pappa/Android/Sdk/system-images/android-Tiramisu/google_apis/x86_64//vendor.img,read-only -device virtio-blk-pci,drive=vendor,iothread=disk-iothread,modern-pio-notify -drive if=none,index=5,id=sdcard,if=none,file=/home/pappa/.android/avd/5inchphode64bitemu_API_Tiramisu.avd/sdcard.img.qcow2,overlap-check=none,cache=unsafe,l2-cache-size=1048576 -device virtio-blk-pci,drive=sdcard,iothread=disk-iothread,modern-pio-notify -netdev user,id=mynet -device virtio-net-pci,netdev=mynet -chardev null,id=forhvc0 -chardev null,id=forhvc1 -device virtio-serial-pci,ioeventfd=off -device virtconsole,chardev=forhvc0 -device virtconsole,chardev=forhvc1 -chardev netsim,id=bluetooth -device virtserialport,chardev=bluetooth,name=bluetooth -device virtio-serial,ioeventfd=off -chardev socket,port=35915,host=::1,nowait,nodelay,reconnect=10,ipv6,id=modem -device virtserialport,chardev=modem,name=modem -device virtio-rng-pci -show-cursor -device virtio_input_multi_touch_pci_1 -device virtio_input_multi_touch_pci_2 -device virtio_input_multi_touch_pci_3 -device virtio_input_multi_touch_pci_4 -device virtio_input_multi_touch_pci_5 -device virtio_input_multi_touch_pci_6 -device virtio_input_multi_touch_pci_7 -device virtio_input_multi_touch_pci_8 -device virtio_input_multi_touch_pci_9 -device virtio_input_multi_touch_pci_10 -device virtio_input_multi_touch_pci_11 -device virtio-keyboard-pci -netdev user,id=virtio-wifi,dhcpstart=10.0.2.16 -device virtio-wifi-pci,netdev=virtio-wifi -device virtio-vsock-pci,guest-cid=77 -L /home/pappa/Android/Sdk/emulator/lib/pc-bios -soundhw hda -vga none -append 'no_timer_check 8250.nr_uarts=1 clocksource=pit console=0 cma=288M@0-4G ndns=4 loop.max_part=7 ramoops.mem_address=0xff018000 ramoops.mem_size=0x10000 memmap=0x10000$0xff018000 printk.devkmsg=on bootconfig' -android-hw /home/pappa/.android/avd/../avd/5inchphode64bitemu_API_Tiramisu.avd/hardware-qemu.ini
	pappa@pappa-ThinkPad-X270:~$ 

Unfortunately starting from within AndroidStudio still does not use kvm:

	pappa@pappa-ThinkPad-X270:~$ ps aux | grep qemu-system-x86_64
	pappa      49364  107 13.2 4869220 2133308 ?     Sl   13:31   3:14 /home/pappa/Android/Sdk/emulator/qemu/linux-x86_64/qemu-system-x86_64 -netdelay none -netspeed full -no-snapshot-load -avd 5inchphode64bitemu_API_Tiramisu -qt-hide-window -grpc-use-token -idle-grpc-timeout 300
	pappa      49896  0.0  0.0  11580   656 pts/1    S+   13:34   0:00 grep --color=auto qemu-system-x86_64
	pappa@pappa-ThinkPad-X270:~$
	
AndroidStudio is said to recognize if acceleration is available and use it automatically. Doesn't seem to be so.
Need to start it from command line for the time being until get it figured out how to do it from within AndroidStudio.

## Disabling libvirtd tricks
After taking above kvm emulation into use, my system started to have some network lags after having been up for a longer period without a boot. Shutdown after such a lag had been experienced also took a long time, cursor just blinked in a black screen. Eventually system was shut down though.  
Thought libvirtd enabling in boot might cause the problem, as that was enabled while taking kvm acceleration in use.
But sadly 

	sudo systemctl disable libvirtd
	
didn't remove it from boot, it was still running after reboot.
Had to disable below libvirt stuff as well

	sudo systemctl disable libvirt-guests
	sudo systemctl disable libvirtd-admin.socket
	sudo systemctl disable libvirtd.socket
	sudo systemctl disable libvirtd-ro.socket
	
	
	
Now after reboot, libvirtd wasn't running any more.


