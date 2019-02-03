# Omni minimal device tree for Razer Phone 2

## Setup
1. Head to https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni/tree/twrp-8.1 and set up your minimal tree
2. Add this to `.repo/local_manifests/cheryl2.xml`:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
        <project path="device/razer/cheryl2" name="thecubed/android_device_razer_cheryl2" remote="github" revision="android-8.1" />
        <project path="kernel/razer_sdm845" name="thecubed/android_kernel_razer_sdm845" remote="github" revision="android-8.1" />
</manifest>
```
3. Run `repo sync` to check it out.

## Building
```sh
. build/envsetup.sh
lunch omni_cheryl2-eng
# if using minimal omni tree -- IMPORTANT!
export ALLOW_MISSING_DEPENDENCIES=true
# to fix razer kernel not having latest DTC scripts (also important)
export DTC_EXT=$(pwd)/prebuilts/misc/linux-x86/dtc/dtc
make -j5 recoveryimage
```

## Notes
- **This currently does *NOT* build a working TWRP image. I'm currently using it to build the kernel and will be working on TWRP support shortly.**
  This does, however, build a working kernel. [Proof](https://i.imgur.com/788Lt7x.jpg).
- I'm using OmniROM because a nice minimal manifest exists for it. Everything should work for Lineage, you'll just need the appropriate combos.
- The kernel used here is a mashup of the official source a few sources. I've kept them as subtrees for reference, but the upstreams are listed here too.
    - Official Razer 4.9 source: https://s3.amazonaws.com/cheryl-factory-images/msm-4.9-aura-2009.tar.gz
    - CAF Audio-Kernel Techpack: https://source.codeaurora.org/quic/la/platform/vendor/opensource/audio-kernel/tree/?h=LA.UM.6.3.r4-04300-sdm845.0
    - CAF TFA98XX 'Techpack': https://source.codeaurora.org/external/mas/tfa98xx/tree/?h=DIN_v6.5.0 (with modified Makefile)

# Acknowledgements
Special thanks to:
- [Rashed97](https://github.com/Rashed97)
- [Dees_Troy](https://github.com/Dees-Troy)
