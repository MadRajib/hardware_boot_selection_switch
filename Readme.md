# Hardware Boot Selection Switch Using Raspberry Pi PICO

Inspired by Hackaday.io project(https://hackaday.io/project/179539-hardware-boot-selection-switch)

### make the project
```bash
$ git clone this project
$ cd HARDWARE_BOOT_SELECTION_SWITCH

$ mkdir build
$ cd build
$ cmake ..
$ make
```
Now Copy the pico_msd.uf2 file to pico.

### In Ubuntu edit the grub file:
```bash
$ sudo vim /etc/grub.d/40_custom

# Look for hardware switch device by its hard-coded filesystem ID
search --no-floppy --fs-uuid --set hdswitch 0000-1234
# If found, read dynamic config file and select appropriate entry for each position
if [ "${hdswitch}" ] ; then
  source ($hdswitch)/switch.cfg

  if [ "${os_hw_switch}" == 0 ] ; then
    # Boot Linux
    set default="0"
  elif [ "${os_hw_switch}" == 1 ] ; then
    # Boot Windows
    set default="2"
  else
    # Fallback to default
    set default="${GRUB_DEFAULT}"
  fi

else
  set default="${GRUB_DEFAULT}"
fi

```