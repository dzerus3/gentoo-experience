# eix

https://wiki.gentoo.org/wiki/Eix

`eix` is a utility for 


# Synchronization

https://www.reddit.com/r/Gentoo/comments/ja2iyf/are_gentoos_sync_speeds_slow_or_quite_good_for_a/

You can speed up `emerge --sync` by using `git` instead of `rsync` for synchronization. Simply paste the following into `/etc/portage/repos.conf/gentoo.conf`:

```
[DEFAULT]
main-repo = gentoo

[gentoo]
location = /var/db/repos/gentoo
sync-type = git
sync-uri = https://github.com/gentoo-mirror/gentoo.git
sync-git-verify-commit-signature = true
sync-depth = 1
auto-sync = yes
sync-openpgp-key-path = /usr/share/openpgp-keys/gentoo-release.asc
sync-openpgp-key-refresh-retry-count = 40
sync-openpgp-key-refresh-retry-overall-timeout = 1200
sync-openpgp-key-refresh-retry-delay-exp-base = 2
sync-openpgp-key-refresh-retry-delay-max = 60
sync-openpgp-key-refresh-retry-delay-mult = 4 
```

In case you've used regular `emerge --sync` before, you will need to remove the existing repository data first. Go to `/var/db/repos/` and rename the `gentoo` folder. Then, once you've successfully synced with git, remove that folder.

## Selecting mirrors
The easiest way to select mirrors is to use `app-portage/mirrorselect`. The command `mirrorselect -D -s3 -b10` should do the trick.

- `-D` downloads a 100kb file from each mirror to test them for speed.
- `-s3` chooses the three fastest mirrors to use.
- `-b10` should split hosts into a certain blocksize to prevent network issues.


