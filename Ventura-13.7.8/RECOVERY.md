# Recovery

## Important

Do not assume the EFI System Partition is always mounted as `F:\`. Windows, WinPE, macOS Recovery, and BIOS tools can assign different drive letters.

Before copying or replacing EFI:

1. Identify the EFI System Partition by size, FAT32 filesystem, and content.
2. Confirm it contains an `EFI` folder with `BOOT` and `OC`.
3. If using Windows, use Disk Management, `diskpart`, or a known EFI mounter before copying.
4. Keep a bootable USB EFI available before changing the internal disk EFI.

## Backups

Original pre-edit backup:

`F:\Hackintosh-Ventura-Project\backups\EFI_20260604_095417`

Second-fix pre-change backup:

`F:\Hackintosh-Ventura-Project\backups\EFI_20260604_103127_pre_second_fix`

Use the second-fix pre-change backup to undo only the latest USB/Picker changes. Use the original backup to return to the initial EFI state before this project.

## Config-only rollback

Original config:

`F:\Hackintosh-Ventura-Project\Config-pre-edit.plist`

Second-fix pre-change config:

`F:\Hackintosh-Ventura-Project\Config-pre-second-fix-20260604_103127.plist`

Copy the desired file to the mounted EFI path:

`<Mounted EFI>\EFI\OC\Config.plist`

## UTBMap-only rollback

Second-fix pre-change UTBMap:

`F:\Hackintosh-Ventura-Project\UTBMap-pre-second-fix-20260604_103127.plist`

Copy it to:

`<Mounted EFI>\EFI\OC\Kexts\UTBMap.kext\Contents\Info.plist`

## GPU fallback

If Ventura boots to black screen:

- Boot from rescue USB or previous EFI.
- Restore `Config-pre-edit.plist`, or manually remove the RX spoof DeviceProperties.
- Re-enable `NootRX.kext` only when returning to the pre-edit NootRX route.
- Reset NVRAM after switching GPU route.

## Bluetooth / USB fallback

If Bluetooth disappears:

- Confirm `HS12` appears in macOS IORegistry/System Information.
- Confirm `13d3:3404` is on an Internal port.
- If external USB ports are more important for a test session, restore the second-fix pre-change UTBMap and retest.

## Picker fallback

The current EFI uses `PickerMode=Builtin` and disables `OpenCanopy.efi` because Resources are empty.

To restore OpenCanopy later:

- Install matching OpenCore Resources into `EFI\OC\Resources`.
- Enable `OpenCanopy.efi`.
- Set `PickerMode=External`.

## NVRAM

After switching GPU route, Bluetooth kext set, USB map, or picker mode, run Reset NVRAM from OpenCore picker, then cold boot.
