### Device specific configuration to build Automotive AOSP Android 14 for Raspberry Pi 4 and Raspberry Pi 5.
Based on: https://github.com/raspberry-vanilla/android_local_manifest

***

### How to build:

1. Establish [Android build environment](https://source.android.com/setup/initializing) and install [repo](https://source.android.com/docs/setup/develop#installing-repo).

2. Install additional packages:

```
sudo apt-get install bc coreutils dosfstools e2fsprogs fdisk kpartx mtools ninja-build pkg-config python3-pip
sudo pip3 install meson mako jinja2 ply pyyaml
```

3. Initialize repo:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-14.0.0_r22 --depth=1
git clone https://github.com/Samaelson/aaos_local_manifest.git -b android-14.0 .repo/local_manifests
```

4. Sync source code:

```
repo sync
```

***

### Compile and build RPi4:

***

5. Compile:

```
. build/envsetup.sh
lunch aosp_rpi4_car-userdebug
make bootimage systemimage vendorimage -j$(nproc)
```

6. Make flashable image:

```
./rpi4-mkimg.sh
```

***

### Compile and build RPi5: Still under development - disabled in manifest file for now!

***

5. Compile:

```
. build/envsetup.sh
lunch aosp_rpi5-userdebug
make bootimage systemimage vendorimage
```

In case of error  --> "-bash: build/soong/soong_ui.bash: Permission denied" <-- simply set permissions:

```
chmod -R 777 build
```

6. Make flashable image:

```
./rpi5-mkimg.sh
```

***

Also look into [Linux kernel build instructions](https://github.com/raspberry-vanilla/android_kernel_manifest/tree/android-14.0).

***

### Issues:

- [Android](https://github.com/raspberry-vanilla/android_local_manifest/issues)
- [Linux kernel](https://github.com/raspberry-vanilla/android_kernel_manifest/issues)

***

### Wiki:

- [Audio](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Audio)
- [DSI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/DSI-display)
- [HDMI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/HDMI-display)
- [Interfaces](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Interfaces)
- [USB boot](https://github.com/raspberry-vanilla/android_local_manifest/wiki/USB-boot)
- [Video decoding](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Video-decoding)
