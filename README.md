WayDroid
===========

Getting started
---------------

To get started with WayDroid, you'll need to get
familiar with [Repo](https://source.android.com/source/using-repo.html) and [Version Control with Git](https://source.android.com/source/version-control.html).

To initialize your local repository using the LineageOS trees, use a command like this:
```
repo init -u git://github.com/LineageOS/android.git -b lineage-17.1
```
Add the WayDroid manifest:
```
wget https://raw.githubusercontent.com/Anbox-halium/anbox-halium/lineage-17.1/anbox.xml -P .repo/local_manifests/
```
Then to sync up:
```
repo sync
```
Then to apply WayDroid patches:
```
anbox-patches/apply-patches.sh --mb
```

How to build
---------------
Please see the [LineageOS Wiki](https://wiki.lineageos.org/) for building environment setup.

To build WayDroid:
```
. build/envsetup.sh
lunch lineage_anbox_arm64-userdebug
make systemimage -j$(nproc --all)
make vendorimage -j$(nproc --all)
```

How to install
---------------
Execute command blew: 
```
wget -O - https://github.com/Anbox-halium/anbox-halium/raw/lineage-17.1/scripts/install.sh | bash
```
Note: Run installer on the user you are willing to install WayDroid on.

Patching kernel
---------------
Running WayDroid requires: 
* Veth for networking
* Ashmem
* Specific binder nodes (anbox-binder anbox-hwbinder anbox-vndbinder)
Checkout defconfig kernel patcher [script](https://github.com/Anbox-halium/anbox-halium/blob/lineage-17.1/scripts/check-kernel-config.sh) for patching halium devices kernel.
```
check-kernel-config.sh halium_device_defconfig -w 
```
On mainline devices it is highly recommanded to use needed drivers as module. (binder_linux and ashmem_linux)
