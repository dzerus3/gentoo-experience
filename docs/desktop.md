# Desktop setup

Once Gentoo can freely boot on its own, it is time to add a desktop to it. Several parts are needed for a working desktop:

- A seat management daemon (manages access to shared resources without giving Wayland compositors root)
- A display manager (in other words, the login screen and underlying authentication daemon)
- Display server (in extremely simplified terms: the thing that draws the desktop on the screen; either Wayland or X11)
- A compositor/window manager (the desktop)
- Some sort of audio backend (either ALSA, Pipewire, PulseAudio, JACK, or some combination of those)

On an OpenRC desktop, I use the following packages to provide that functionality:

- `sys-auth/seatd` (with `builtin` and `server` useflags)
- `gui-libs/greetd`, `gui-libs/display-manager-init`, and `gui-apps/tuigreet` (display manager)
- `dev-libs/wayland` (display server)
- `gui-wm/sway` or `gui-wm/wayfire` (compositor)
- `media-video/pipewire` (with `pipewire-alsa` and `sound-server` flags)

Once all the packages are installed, you need to do the following:

1. Set the `display-manager` service to start on boot.
2. Edit `/etc/conf.d/display-manager` to set `DISPLAYMANAGER=greetd`
3. Set `tuigreet` as the greeter by editing `/etc/greetd/config.toml` and adding `command = "tuigreet --cmd sway`. Consider also adding commands for `--power-reboot` and `--power-shutdown`.
4. Set the `seatd` service to start on boot.
5. Set the `elogind` service to start on boot.
6. Create a `.profile` file in each user's home directory and write a script to set the `XDG_RUNTIME_DIR` variable. Adding it to `/etc/skel` may be a good idea.
