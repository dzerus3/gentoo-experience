# Changing DNS servers
dhcdcd automatically overwrites resolv.conf. In order to overwrite your DNS settings, you can either use `chattr +i` to make `/etc/resolv.conf` immutable, or add `nohook resolv.conf` to the end of `/etc/dhcpcd.conf`.
