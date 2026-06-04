# Boot Test Checklist

## Before First Boot

- Prepare a rescue USB with a known bootable EFI.
- Confirm backups exist:
  `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_095417`
  `F:\Hackintosh-Ventura-Project\backups\EFI_20260604_103127_pre_second_fix`
- Keep verbose mode enabled for the first run. Current `boot-args` include `-v`.
- At the OpenCore picker, run Reset NVRAM once after these EFI changes.

## First Boot

- OpenCore picker appears in Builtin/text mode.
- Ventura 13.7.8 reaches desktop.
- No `OC: Failed to load configuration`.
- No missing kext/driver messages.
- No GPU black screen.

## macOS Commands

```sh
sw_vers
system_profiler SPDisplaysDataType SPUSBDataType SPBluetoothDataType SPAudioDataType SPEthernetDataType SPAirPortDataType
kmutil showloaded | grep -Ei "Lilu|WhateverGreen|AppleALC|IntelMausi|Brcm|BlueTool|USBToolBox|VirtualSMC"
```

## Hardware Checks

- RX 6650 XT: Metal supported, expected spoof path, correct resolution, DP/HDMI, sleep/wake.
- UHD 630: Quick Sync/H.264/HEVC only if iGPU is enabled in BIOS.
- USB/BT: Broadcom `13d3:3404` should appear on internal `HS12`.
- Wi-Fi: scan, connect, reconnect after sleep.
- Bluetooth: pair keyboard/mouse, reconnect after sleep.
- Audio ALC887: rear output, front headphone, mic, sleep/wake.
- Ethernet I219-V: DHCP, 1Gb link, sleep/wake.
- USB: test every physical USB2/USB3 port. Pay attention to SS06 because it was removed to keep the 15-port limit.

## Stability Loop

- Cold boot 3 times.
- Reboot 3 times.
- Sleep/wake 3 times.
- Shut down, remove power briefly, then boot once.

## After Stable

- Remove `-v` from boot-args only after repeated stable boots.
- If Wi-Fi is missing intermittently, consider `brcmfx-delay=15000` only after collecting logs.
- If Bluetooth is missing, inspect HS12 and USB map before changing kexts.
