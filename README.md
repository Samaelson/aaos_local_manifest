### Device specific configuration to build AOSP Android 13 for Raspberry Pi 4.

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
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r75 --depth=1
git clone https://github.com/Samaelson/aaos_local_manifest.git -b android-13.0_1024x600 .repo/local_manifests
```

Or optionally, you can reduce download size by creating a shallow clone and removing unneeded projects:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r75 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi4.xml -L https://raw.githubusercontent.com/Samaelson/aaos_local_manifest/android-13.0_1024x600/manifest_brcm_rpi4.xml --create-dirs
curl -o .repo/local_manifests/remove_projects.xml -L https://raw.githubusercontent.com/Samaelson/aaos_local_manifest/android-13.0_1024x600/remove_projects.xml
```

4. Sync source code:

```
repo sync
```

5. Compile:

```
. build/envsetup.sh
lunch aosp_rpi4_car-userdebug
make bootimage systemimage vendorimage
```

6. Make flashable image:

```
./rpi4-mkimg.sh
```

Also look into [Linux kernel build instructions](https://github.com/raspberry-vanilla/android_kernel_manifest/tree/android-13.0).

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
