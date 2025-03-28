# Boot process
## BIOS és UEFI
### Basic Input/Output System
Low-level szoftver
Hardver inicializálás
Boot loader indítása MBR/GPTről vagy egy másik partícióról
### Unified Extensible Firmware Interface
efi renszer partícióról indt img-ket

## BIOS - Basic Input/Output System
Ellenőrzi a számítógép hardveres eszközeit - Power On Self Test(**POST**) és megkeresi a bootolható lemezeket

Ezt követően betölti a memóriába a sorrend szerinti első érvényes **MBR**rel rendelkező **boot sector**(**persistant data storage**: hdd,sdd,floppy etc.) **bootloader**ét
### MBR - Master Boot Record
Partíciós séma, létezik még ezen kívül GPT
Csak a particionált lemezeknek van MBRük, azok legelején találhatóak(`/dev/hda` vagy `/dev/sda`)
* **Boot code/bootstrap code**
Segít előkészíteni a rendszert egy operációs rendszer elindításához
* **Partition Table**
lemezen elhelyezkedő partíciókat mutatja
* **MBR valiation/boot signature**
Információt tartalmaz a Bootloaderről
## Bootloader
GNU GRUB - GNU GRand Unified Bootloader,GRUB2,LILO stb.
`boot/grub/grub.conf`
### Stage1
`boot.img` - boot code
Betölti és futtatja az első megfelelő boot codeot, ami lehetővé teszi a hardveres kapcsolatot
### Stage2
`core.img`
Futtatja azokat a szükséges állományokat amik szükségesek a stage3 beli fájlok felismeréséhez és futtatásához
Gyakori fájlrendszer-illesztőprogramok(EXT,FAT,NTFS)
### Stage3
`boot/grub`
Futásidejű kernel modulokat tartalmaz
Az egyes modulok megtalálhatóak a `/boot` könyvtárban
Kiválasztást követően a rendszer futtatja a kernelt és átadja az irányítást
Splash screen választási és alapértelmezett kernel a `/boot/grub/grub.conf`-ban lett definiálva
## Kernel
Betölti a kiválasztott kernelt a memóriába(összekapcsolja a root fájlrendszerét ahogy az definiálva lett a `boot/grub/grub.conf`-ban), az kicsomagolja magát majd betölti a **systemd/init** programot és átadja annak az irányítása

Ez a **boot process** vége, viszont az end user még semmire sem képes. Innentől **startup process**
# Startup process
##  Systemd
Minde process őse
"mounting filesystem" és elindítja a rendszer programokat a linux kernel részére
Fájlrendszerek csatolása `/etc/fstab` alapján
`/etc/systemd/system/default.target` szimbolikus link alapján eldönti, hogy milyen állapotba bootoljon a rendszer
| Runlevel | target |  |
|--|--|--|
|  | halt.target | Megállítja a rendszert |
| 0 | poweroff.target | Megállítja a rendszert és kikapcsolja az áramellátást |
| S | emergency.target |  |
| 1 | rescue.target |  |
| 2 |  |  |
| 3 | rescue.target |  |
| 4 |  |  |
| 5 | graphical.target |  |
| 6 | rebot.target |  |
|  | default.target |  |
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODUzODI4ODBdfQ==
-->