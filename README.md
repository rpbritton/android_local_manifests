# Download Built ROMs
https://github.com/rpbritton/android_local_manifests/releases

# XDA Thread
https://forum.xda-developers.com/t/rom-11-unofficial-pixel-experience-mi-a2-jasmine_sprout-aosp.4269517/

# Build Yourself
## Download
https://source.android.com/setup/build/downloading
```
repo init --depth=1 -u https://github.com/PixelExperience/manifest -b eleven-plus
git clone https://github.com/rpbritton/android_local_manifests .repo/local_manifests -b eleven-plus-jasmine_sprout
repo sync -j$(nproc --all) -c --force-sync --no-clone-bundle --no-tag
```

## Build
https://source.android.com/setup/build/building
```
source build/envsetup.sh
lunch aosp_jasmine_sprout-userdebug
mka bacon
```

## Signed Build
https://source.android.com/devices/tech/ota/sign_builds
```
source build/envsetup.sh
lunch aosp_jasmine_sprout-userdebug
mka target-files-package otatools
sign_target_files_apks -o -d ~/.android-certs \
    $OUT/obj/PACKAGING/target_files_intermediates/*-target_files-*.zip \
    signed-target_files.zip
ota_from_target_files -k ~/.android-certs/releasekey \
    signed-target_files.zip \
    signed-ota_update.zip
```
