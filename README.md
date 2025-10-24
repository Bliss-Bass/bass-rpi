# Bass ARM - Raspberry Pi 

This is the releases channel for Bass OS for ARM devices, like the Raspberry Pi. 

## Bass OS for the Raspberry PI series based on the GloDroid project & raspberry-vanilla project

[![GloDroid](https://img.shields.io/badge/GLODROID-PROJECT-blue)](https://github.com/GloDroid/glodroid_manifest)
[![ProjectStatus](https://img.shields.io/badge/PROJECT-STATUS-yellowgreen)](https://github.com/GloDroidCommunity/raspberry-pi/issues/1)

[![Raspberry-Vanilla](https://img.shields.io/badge/RASPBERRY-VANILLA-blue)](https://github.com/raspberry-vanilla)
[![ProjectStatus](https://img.shields.io/badge/PROJECT-STATUS-yellowgreen)](https://github.com/raspberry-vanilla/android_local_manifest/issues/1)

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Requirements

### Raspberry Pi Imager
Download and install the official Raspberry Pi Imager from [here](https://www.raspberrypi.com/software/)

### sdcard.img
Find the latest Bass rpi image archive sdcard images for your target use-case from the Releases tab

You can also run the rpi-imager and point it to our OS list with the following command:

```
rpi-imager --repo https://raw.githubusercontent.com/Bliss-Bass/bass-rpi/refs/heads/main/rpi-imager-os-list.json
```

You will then find the current Bass Pi images under the "Other general-purpose OS" section.

![Screenshot from 2025-01-16 15-51-23](https://github.com/user-attachments/assets/4b7229b7-d355-41b7-a7eb-ac6bfb3ffb9d)

At the bottom, you will see "Bass ARM (Android)". 

![Screenshot from 2025-01-16 15-51-34](https://github.com/user-attachments/assets/1355bc6f-bb38-42ac-bf6b-7ccf9b2b65f4)

And in that, you will find our Bass ARM builds for the Raspberry Pi.

![Screenshot from 2025-01-16 15-51-46](https://github.com/user-attachments/assets/99256edc-47f4-4abc-97b8-34ed078a269e)


### Instructions

You can follow the instructions found on our documentation site: 
[Bass rpi installation](https://docs.blisscolabs.dev/installation/raspberry-pi/raspberry-pi-installation/)

### Source

Our main branch is open-source. If you require any of our Addons, the licenses for those are available individually. 
- https://github.com/Bliss-Bass/Bass-ARM

### Development Information

This repo also houses the bass-arm-os-sublist.json which is merged with the official Raspberry Pi Imager OS list. Here are a few steps for maintainers to use. 

#### Getting the required image data

We will need to grab the filesize and the sha256sum of each updated image, so we can update the rpi-imager-os-list.json file. This will have to be run on the downloaded .zip AND the extracted .img file (and folders if any).

##### Filesize

Use the following command:

```
du -b target.zip

```

Or if the extracted .img file:

```
du -b target.img

```

##### Sha256sum

Use the following command:

```
sha256sum target.zip

```

Or if the extracted .img file:

```
sha256sum target.img

```

#### Json Formatting

The .json file will need to be formatted a specific way for the information to be valid:

- name: The name of the OS build variant
- description: The description of the OS build variant
- icon: The icon of the OS build variant (supports images .jpg, .png)
- url: The direct download url of the OS build variant (Usually the GitHub Release download link URL)
- website: The website of the OS build variant
- extract_size: The size of the extracted .img file we got from above (in bytes)
- extract_sha256: The sha256sum of the extracted .img file we got from above
- image_download_size: The size of the downloaded .zip file we got from above (in bytes)
- image_download_sha256: The sha256sum of the downloaded .zip file we got from above
- release_date: The release date of the OS build variant
- init_format: The init format of the OS build variant (for Android, it is none)
- devices: The target devices of the OS build variant (pi5-64bit, pi4-32bit, etc. Our Android builds only support one device config per build variant)

#### Example Json

```
{
    "name": "Bass Tablet UI - Android 16 (RPi 5, 500, 500+) - SD Card Only",
    "description": "Minimal AOSP based Android OS. Includes Android Tablet UI with multi-window enabled, MicroG, Aurora Store and FOSS app stores",
    "icon": "https://github.com/user-attachments/assets/003d3f05-ceaf-4124-9cac-70058fe64313",
    "url": "https://github.com/Bliss-Bass/bass-rpi/releases/download/BassRPI-16-TabletUI-foss-202510221844-rpi5/BassRPI-16-TabletUI-foss-202510221844-rpi5.zip",
    "website": "https://bassos.navotpala.tech",
    "extract_size": 15360000000,
    "extract_sha256": "881a299fe74bc6f1ef2b066cef5b12eb1015fac4765f9d1fe826d87d207bb8ce",
    "image_download_size": 885893805,
    "image_download_sha256": "da74a07f97278ec317121a3156b63617a2ce75102e8a55695d1529ed5d9f749f",
    "release_date": "2025-10-23",
    "init_format": "none",
    "devices": [
    "pi5-64bit"
    ]
}
```

#### Testing and Debugging

You can run the rpi-imager from terminal with debugging enabled, and point it to your local .json for testing and validation:

```
rpi-imager --debug --repo '/home/user/projects/bass-rpi/rpi-imager-os-list.json'
```