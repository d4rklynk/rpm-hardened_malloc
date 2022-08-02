Unofficial package for hardened_malloc
======================================

Overview
--------
This repo contains an RPM specfile and a PKGBUILD for micro-architecture optimized builds of the hardened_malloc library.

Upstream Project
----------------
- https://github.com/GrapheneOS/hardened_malloc
	- Donate:
		- https://grapheneos.org/donate
		- https://github.com/sponsors/thestinger

Compatibility
-------------
- Fedora 36
- Arch Linux

Prebuilts
---------
- Fedora via Divested-RPM: https://divested.dev/index.php?page=software#divested-release
- Fedora via CI: https://gitlab.com/divested/rpm-hardened_malloc/-/jobs/artifacts/master/browse?job=build_rpm
- Arch via CI: TODO

Included Variants
-----------------
Three variants are included compiled for four different micro-architetures:

- default
	- prioritizes security
- memefficient
	- prioritizes memory usage
		- disables slab quarantines and raises the guard slab interval from 1 to 8
- light
	- prioritizes CPU and memory usage
		- disables the slab quarantines, write after free check, slot randomization, and raises the guard slab interval from 1 to 8

The current default is memefficient.

Known Issues
------------
- Firefox/Tor Browser/etc.
	- Workaround: add `blacklist /etc/ld.so.preload` to their firejail profiles
	- Our patched firejail available via Divested-RPM includes this workaround
- php-fpm
	- Workaround: add `InaccessiblePaths=-/etc/ld.so.preload` to a systemd unit override
	- Our brace includes this workaround
- qemu with virgl enabled will randomly segfault

License
-------
MIT

Credits
-------
- @GrapheneOS for the hardened_malloc project itself
- @noatsecure/HardHatOS for the original RPM specfile
- @thithib for the original PKGBUILD
