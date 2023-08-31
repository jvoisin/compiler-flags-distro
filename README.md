# Usage of hardening-related compiler flags across Linux distributions

|.                                | Alpine | Debian | Fedora    | Gentoo Hardened | Ubuntu | OpenSUSE | ArchLinux | OpenBSD |
|---------------------------------|--------|--------|-----------|-----------------|--------|----------|-----------|---------|
|`-D_FORTIFY_SOURCE=2`            |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://wiki.debian.org/Hardening)|superseded|superseded|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags#A-D_FORTIFY_SOURCE.3D2)|[2005](https://en.opensuse.org/openSUSE:Security_Features)|superseded|?|
|`-D_FORTIFY_SOURCE=3`            |no      |[no](https://wiki.debian.org/Hardening)|[2023](https://fedoraproject.org/wiki/Changes/Add_FORTIFY_SOURCE%3D3_to_distribution_build_flags)|[2022](https://bugs.gentoo.org/876893)|[no](https://bugs.launchpad.net/ubuntu/+source/gcc-12/+bug/2012440)|[2023](https://en.opensuse.org/openSUSE:Security_Features)|[2023](https://gitlab.archlinux.org/archlinux/rfcs/-/merge_requests/17)|?|
|`-D_GLIBCXX_ASSERTIONS`          |[yes](https://gitlab.alpinelinux.org/alpine/abuild/-/blob/master/default.conf#L2)|no|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|[2022](https://bugs.gentoo.org/876895)|[no](https://bugs.launchpad.net/ubuntu/+source/gcc-12/+bug/2016042)|yes|[2021](https://gitlab.archlinux.org/archlinux/rfcs/-/commit/a7a94d354fe9ac490ea2f02d6d3ac697a2faee6f)|?|
|`-D_LIBCPP_ENABLE_HARDENED_MODE` |[yes](https://gitlab.alpinelinux.org/alpine/abuild/-/blob/master/default.conf#L2)|no|no|[2023](https://bugs.gentoo.org/851111)|no|no|no|?|
|`-Wformat -Wformat-security`     |[yes](https://gitlab.alpinelinux.org/alpine/abuild/-/blob/master/default.conf#L2)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[yes](https://src.fedoraproject.org/rpms/redhat-rpm-config/blob/rawhide/f/buildflags.md)|[2009?](https://bugs.gentoo.org/259417)|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|yes|[yes](https://gitlab.archlinux.org/archlinux/rfcs/-/commit/a7a94d354fe9ac490ea2f02d6d3ac697a2faee6f)|?|
|`-Wl,-z,relro`/`-Wl,-z,now`      |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[yes](https://src.fedoraproject.org/rpms/redhat-rpm-config/blob/rawhide/f/buildflags.md)|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2006](https://en.opensuse.org/openSUSE:Security_Features)|[yes](https://wiki.archlinux.org/title/Arch_package_guidelines/Security)|?|
|`-fPIE`/`-fPIC`/…                |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/rules2)|[2015](https://fedoraproject.org/wiki/Changes/Harden_All_Packages)|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2016](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2017](https://bugzilla.suse.com/show_bug.cgi?id=912298)|[2017](https://github.com/archlinux/svntogit-packages/commit/5936710c764016ce306f9cb975056e5b7605a65b)|[yes](https://man.openbsd.org/clang-local)|
|`-fcf-protection`/`-mcet`        |[no](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|[2021](https://bugs.gentoo.org/822036)|[2019](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|yes|[yes](https://gitlab.archlinux.org/archlinux/rfcs/-/commit/a7a94d354fe9ac490ea2f02d6d3ac697a2faee6f)|[2023](https://github.com/openbsd/src/commit/bba006a81846d90e529167c689ea0d456b4599bc)|
|`-fsanitize=undefined -fsanitize`|no|no|no|no|no|no|no|?|
|`-fstack-clash-protection`       |[2023](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/4f7a2aff7b87cec7dd2783f95b5d6f744244c6c7)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|[2018](https://bugs.gentoo.org/675050)|[2019](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2018](https://en.opensuse.org/openSUSE:Security_Features)|[yes](https://gitlab.archlinux.org/archlinux/rfcs/-/commit/a7a94d354fe9ac490ea2f02d6d3ac697a2faee6f)|?|
|`-fstack-protector-strong`       |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[yes](https://src.fedoraproject.org/rpms/redhat-rpm-config//blob/rawhide/f/buildflags.md)|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2014](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2006](https://en.opensuse.org/openSUSE:Security_Features)|[yes](https://github.com/archlinux/svntogit-packages/blob/packages/gcc/trunk/PKGBUILD)|[yes](https://man.openbsd.org/clang-local)|
|`-ftrivial-auto-var-init=zero`   |no|[no](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1010685)|no|[no](https://bugs.gentoo.org/913339)|[no](https://bugs.launchpad.net/ubuntu/+source/gcc-12/+bug/1972043)|no|no|?|
|`-mbranch-protection=standard`/`-mbranch-target-enforce`|no|no|[yes](https://src.fedoraproject.org/rpms/redhat-rpm-config/blob/rawhide/f/buildflags.md)|no|no|no|no|[2023](https://github.com/openbsd/src/commit/990129f49dcc7205208dec5e29b252be8659896d)|



Sources:
- https://src.fedoraproject.org/rpms/redhat-rpm-config//blob/rawhide/f/buildflags.md
- https://en.opensuse.org/openSUSE:Security_Features
- https://gcc.gnu.org/pipermail/gcc-patches/2023-August/628748.html
- https://wiki.gentoo.org/wiki/Hardened/Toolchain#Changes
- https://gitlab.archlinux.org/archlinux/rfcs/-/blob/master/rfcs/0003-buildflags.rst?ref_type=heads
- https://man.openbsd.org/clang-local
