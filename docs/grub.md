# GRUB

Unless the conditions for boot are perfect and no initramfs is needed (in other words, root is a dumb ext4 patition) some GRUB configuration is necessary. It is necessary both to boot correctly, and to make sure that `dracut` generates the initramfs properly.

```
GRUB_DISTRIBUTOR="Gentoo"

# Enables support for encrypted root partition
GRUB_ENABLE_CRYPTODISK=y
# Sets the label (UUID works too) of the (decrypted) root partition, the UUID of the LUKS partition, and the keyboard layout to use within initramfs and GRUB
GRUB_CMDLINE_LINUX="root=LABEL=gentooroot rd.luks.uuid=e2a7eb41-4644-4056-b46e-9898871f075e rd.vconsole.keymap=colemakdh"
```
