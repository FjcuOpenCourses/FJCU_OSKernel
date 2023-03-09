# FJCU_OSKernel
The Design of Operating Systems and Cloud Systems Kernel

## Compiling Linux kernel
###### Step 1:
- Download Linux Kernel source with ```wget```
```
wget 	https://www.kernel.org/pub/linux/kernel/v6.x/linux-{any linux kernel version (the more latest the best)}.tar.xz
```


###### Step 2:
- Extract the whole tar file that you downloaded
- navigate to the folder
- right-click in the folder -> Open in Terminal


###### Step 3:
- Install required package
```
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
```


###### Step 4:
- Configure Kernel
- Copy existing config with ```cp```
```
cp -v /boot/config-$(uname -r) .config
```
- run the command below to configure the kernel
```
make menuconfig
```
- navigate using arrow key, select **Save** and press **Ok** to save the config
- after saving the config, select **Exit**

![menuconfig example](https://phoenixnap.com/kb/wp-content/uploads/2022/11/configuration-menu-pnap-update.png)


##### Step 5:
- build kernel using ```make```
- in the case that you assigned multiple threads/cores to your VM, you can use ```-j``` argument to utilize it all:
```
make -j {how many core you have}
```
- If you are compiling the kernel on Ubuntu, you may receive the following error that interrupts the building process:
```
No rule to make target 'debian/canonical-certs.pem
```
- Disable the conflicting security certificates by executing the two commands below:
```
scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```
- run ```make``` again and press **Enter** to all

- after ```make``` command finish running, install required module
```
sudo make modules_install
```

###### Step 6:
- Install the kernel that you finish compiled into the system
```
sudo make install
```
- Reboot system
- after reboot, check kernel version using the command below
```
uname -r
```

##### Step 7: Changing Kernel
- Press **Shift** and restart system
- Waiting system restarted until this screen appeared

![changing kernel](https://i.stack.imgur.com/sSCzp.png)
- Select the second option

![changing kernel](https://i.stack.imgur.com/yYhnM.png)
- Select the kernel version you compiled
