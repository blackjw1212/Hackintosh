[![](https://badgen.net/badge/icon/Telegram?icon=telegram&label)](https://t.me/blackjw1212)

# Hackintosh — ASUS TUF Z370-PLUS GAMING + RX 6650 XT

![System spec](https://github.com/blackjw1212/Hackintosh/blob/master/Pictures/system-Monterey-12.3.7.png?raw=true)

| | |
|---|---|
| **macOS** | Monterey 12.7.6 (21H1320) |
| **OpenCore** | 1.0.7 |
| **SMBIOS** | iMac19,1 |

## Hardware

| Component | Details |
|---|---|
| **CPU** | Intel Core i7-9700 (Coffee Lake, 8C/8T, 3.0 GHz / 4.7 GHz Turbo) |
| **Motherboard** | ASUS TUF Z370-PLUS GAMING |
| **GPU (dGPU)** | Fighter AMD Radeon RX 6650 XT 8GB GDDR6 |
| **GPU (iGPU)** | Intel UHD 630 (headless, QuickSync only) |
| **RAM** | Kingston HyperX Predator RGB DDR4 3200 MHz 16GB × 2 (XMP @ 3200 MHz) |
| **Storage** | Kingston NV1 500GB M.2 2280 NVMe SSD |
| **PSU** | Corsair TX550M 80 PLUS Gold |
| **Monitor** | LG 34UM58-P 34" 21:9 UltraWide WQHD IPS |
| **Mouse** | Logitech G502 HERO |
| **Keyboard** | Logitech G610 Orion Blue |

## What Works

| Feature | Status |
|---|---|
| Graphics (RX 6650 XT) | ✅ Full acceleration, H.264 & HEVC hardware encode/decode |
| iGPU (UHD 630) | ✅ Headless — QuickSync / DRM offload |
| Audio | ✅ AppleALC `alcid=1` |
| Wired Ethernet | ✅ Intel I219-V via IntelMausi |
| USB 3.1 | ✅ Properly mapped (15 ports via UTBMap) |
| Sleep / Wake | ✅ |
| CPU Power Management | ✅ Native, SSDT-based |
| Wi-Fi | ✅ (BCM card required) |
| Bluetooth | ✅ (BCM card required) |
| HandOff / AirDrop | ✅ |
| iMessage / FaceTime | ✅ |
| NVMe Power Management | ✅ NVMeFix |

## Kexts

| Kext | Version | Purpose |
|---|---|---|
| [Lilu](https://github.com/acidanthera/Lilu) | 1.7.0 | Platform patcher — must load first |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC) | 1.3.4 | SMC emulation |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen) | 1.6.9 | GPU patch — iGPU headless + AGDP bypass (`agdpmod=pikera`) |
| [SMCProcessor](https://github.com/acidanthera/VirtualSMC) | 1.3.4 | CPU temperature / voltage sensor |
| [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) | 1.3.4 | SuperIO fan sensor |
| [AppleALC](https://github.com/acidanthera/AppleALC) | 1.9.4 | Audio patch |
| [IntelMausi](https://github.com/acidanthera/IntelMausi) | 1.0.7 | Intel I219-V Ethernet |
| [NVMeFix](https://github.com/acidanthera/NVMeFix) | 1.1.1 | NVMe power management |
| [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) | 2.1.9 | BCM Wi-Fi patch |
| [BlueToolFixup](https://github.com/acidanthera/BrcmPatchRAM) | 2.6.9 | macOS 12+ Bluetooth patch |
| [USBToolBox](https://github.com/USBToolBox/kext) | 1.1.1 | USB port injection provider |
| [UTBMap](https://github.com/USBToolBox/kext) | — | USB port map (15 ports: HS01–8, SS01–7) |

> **Disabled / unused**: NootRX (replaced by WhateverGreen), CPUFriend (DataProvider empty), RadeonSensor (use [SMCRadeonSensors v2.4.0](https://github.com/ChefKissInc/SMCRadeonSensors) instead)

## BIOS Settings

Detailed BIOS screenshots available [here](BIOS/README.md).

| Setting | Value |
|---|---|
| CFG Lock | **Disabled** |
| CSM | **Disabled** |
| EHCI / XHCI Hand-off | **Enabled** |
| Above 4G Decoding | **Enabled** |
| VT-d | **Disabled** |
| XMP | **Enabled** (3200 MHz) |
| Integrated Graphics | **Enabled** (for iGPU headless) |
| DVMT Pre-Allocated | **64M or higher** |

## Boot Arguments

```
alcid=1 agdpmod=pikera
```

- `alcid=1` — ALC S1200A layout for ASUS TUF Z370
- `agdpmod=pikera` — Required for Navi (RX 6000) series with iMac19,1 SMBIOS; prevents black screen / white Apple freeze

## DeviceProperties

### iGPU — PciRoot(0x0)/Pci(0x2,0x0) (headless)

| Key | Value |
|---|---|
| `AAPL,ig-platform-id` | `07009B3E` (0x3E9B0007) |
| `device-id` | `9B3E0000` (UHD 630) |

iGPU is used exclusively for QuickSync / DRM offload. Display output is handled entirely by the RX 6650 XT.

## ACPI

| File | Purpose |
|---|---|
| `ssdt_data.aml` | CPU PM frequency table + plugin-type (replaces SSDT-PLUG) |
| `SSDT-EC-USBX.aml` | Embedded controller + USB power |
| `SSDT-AWAC.aml` | System clock fix (Coffee Lake) |

## Benchmarks

![Geekbench](https://github.com/blackjw1212/Hackintosh/blob/master/Pictures/geekbench.png?raw=true)

- [Geekbench 6 CPU](https://browser.geekbench.com/v6/cpu/5200659)
- [Geekbench 6 Compute (Metal)](https://browser.geekbench.com/v6/compute/1868101)

## Installation Notes

Follow the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) — **Coffee Lake** section.

Key points for this build:
- RX 6650 XT (Navi 23) has **native drivers in macOS Monterey 12.1+**; no NootRX needed
- **WhateverGreen** handles both iGPU headless init and `agdpmod=pikera` for Navi with iMac19,1 SMBIOS
- iGPU must be enabled in BIOS for QuickSync; set `AAPL,ig-platform-id = 07009B3E` (headless mode)
- USB mapping is mandatory — use USBToolBox + UTBMap to stay within the 15-port limit

## Screenshots

![HiDPI](https://github.com/blackjw1212/Hackintosh/blob/master/Pictures/hidpi.png?raw=true)
