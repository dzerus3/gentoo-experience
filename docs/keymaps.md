Switching keymaps for the virtual terminal is fairly straightforward. Firstly, you must locate the desired keymap under `/usr/share/keymaps`. Each keymap is a specially formatted, gzipped text file.

If the desired keymap does not exist, you may create a new keymap by following the example of one of the existing keymaps. Once your keymap is ready to use, simply copy it to some subfolder of `/usr/share/keymaps`. Make sure it has a unique filename.

Then, you need to set the correct keymap in `/etc/conf.d/keymaps` under the keymap entry. Simply use the keymap filename, but without the extensions. After this, you need to restart the `keymaps` service in OpenRC. The new keymap should be ready to use.

In order to make the new keymap work with dracut, you need to specify it in the `GRUB_CMDLINE_LINUX` option for GRUB.Specifically, you need to set `rd.console.keymap=<name of layout>` and rerun dracut.

https://wiki.gentoo.org/wiki/Keyboard_layout_switching
