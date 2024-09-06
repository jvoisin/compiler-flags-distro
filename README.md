# Usage of enabled-by-default hardening-related compiler flags across Linux distributions

|.                                | Alpine | Debian | Fedora    | Gentoo | Gentoo Hardened | Ubuntu | OpenSUSE | ArchLinux | OpenBSD | Chimera Linux | Android | Google Chrome |
|---------------------------------|--------|--------|-----------|--------|-----------------|--------|----------|-----------|---------|---------------|---------|---------------|
|`-fhardened`                     |[NA](# "only for GNU based GCC")|no|[no](https://src.fedoraproject.org/rpms/redhat-rpm-config/blob/rawhide/f/buildflags.md)|no|no|[no](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|?|no|[NA](# "only for GNU based GCC")|?|[NA](# "only for GNU based GCC")|?|
|`-D_FORTIFY_SOURCE=2`            |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[2011](https://github.com/guillemj/dpkg/commit/f3bb7d4939ae95cf44c89e8f599e7ed5da431e57)|[2007](https://listman.redhat.com/archives/fedora-devel-announce/2007-September/msg00015.html)|yes|superseded|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags#A-D_FORTIFY_SOURCE.3D2)|[2005](https://en.opensuse.org/openSUSE:Security_Features)|[2021](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/f409a72342bf37017f190021970efaaeac1bb619)|?|[yes](https://github.com/chimera-linux/cports/commit/9b78e55067f024b8dbf9fbceb472e8705f84ed5d)|[2017](https://android-developers.googleblog.com/2019/10/introducing-ndk-r21-our-first-long-term.html)|yes|
|`-D_FORTIFY_SOURCE=3`            |no      |[no](https://wiki.debian.org/Hardening)|[2023](https://fedoraproject.org/wiki/Changes/Add_FORTIFY_SOURCE%3D3_to_distribution_build_flags)|no|[2022](https://bugs.gentoo.org/876893)|[2024](https://bugs.launchpad.net/ubuntu/+source/gcc-13/+bug/2012440)|[2023](https://en.opensuse.org/openSUSE:Security_Features)|[2024](https://gitlab.archlinux.org/archlinux/devtools/-/releases/v1.2.0)|?|[2024](https://github.com/chimera-linux/cports/commit/a26be649d8a13c1012d5e165055d354a6bab1af8)|[no](https://android.googlesource.com/platform/bionic.git/+/HEAD/docs/status.md#fortify)|yes|
|`-D_GLIBCXX_ASSERTIONS`          |[2023](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/44c933da5d8e364d6cd755071f629c05444191df)|no|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|no|[2022](https://bugs.gentoo.org/876895)|[no](https://bugs.launchpad.net/ubuntu/+source/gcc-12/+bug/2016042)|yes|[2021](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/f409a72342bf37017f190021970efaaeac1bb619)|no|no|no|?|
|`-D_LIBCPP_HARDENING_MODE_HARDENED`/`-flibc++-hardening` |no|no|no|no|?|no|no|no|?|?|no|?|
|`-D_LIBCPP_ENABLE_HARDENED_MODE` (deprecated) |[not yet](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/65b5d578b2d9e3f170bc9d31dcd23f0014cfc36e)[^1]|no|no|no|[2023](https://bugs.gentoo.org/851111)|no|no|no|?|?|no|[yes](https://bugs.chromium.org/p/chromium/issues/detail?id=1335422)|
|`-D_LIBCXX_ENABLE_ASSERTIONS` (llvm16) |no|no|no|no|superseded|no|no|no|?|[yes](https://github.com/search?q=repo%3Achimera-linux%2Fcports+DLIBCXX_ENABLE_ASSERTIONS&type=code)|?|[yes](https://bugs.chromium.org/p/chromium/issues/detail?id=1335422)
|`-Wformat -Wformat-security`/`-Wformat=2` |[2023](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/ca8375f0e9d1715e38c14c918c675d6774f1eabc)|[2011](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[2013](https://fedoraproject.org/wiki/Changes/FormatSecurity)|[2009](https://bugs.gentoo.org/259417)|[2009](https://bugs.gentoo.org/259417)|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|yes|[2021](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/f409a72342bf37017f190021970efaaeac1bb619)|?|[2023](https://github.com/chimera-linux/cports/commit/ad898a6b645b11dee989f4504e89577f5395ba24)|[2010](https://source.android.com/docs/security/enhancements/enhancements41)|yes|
|`-Wl,-z,noexecstack`             |yes|yes|yes|yes|yes|yes|yes|yes|yes|yes|yes|
|`-Wl,-z,relro`/`-Wl,-z,now`      |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[2015](https://fedoraproject.org/wiki/Security_Features_Matrix#Built_as_PIE)|no|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2008](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2006](https://en.opensuse.org/openSUSE:Security_Features)|[2017](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/b4b2bb56174493ea2e60b1eecc0085db421908cc)|?|[yes](https://github.com/chimera-linux/cports/commit/9b78e55067f024b8dbf9fbceb472e8705f84ed5d)|[2013](https://source.android.com/docs/security/enhancements/enhancements43)|yes|
|`-fPIE`/`-fPIC`/…                |[2008](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/fdc478bde8a2a0d76d33fcc89fa313c9f31bb79c)|[2011](https://github.com/guillemj/dpkg/commit/f3bb7d4939ae95cf44c89e8f599e7ed5da431e57)|[2015](https://fedoraproject.org/wiki/Changes/Harden_All_Packages)|yes|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2016](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2017](https://bugzilla.suse.com/show_bug.cgi?id=912298)|[2017](https://github.com/archlinux/svntogit-packages/commit/5936710c764016ce306f9cb975056e5b7605a65b)|[yes](https://man.openbsd.org/clang-local)|[yes](https://github.com/chimera-linux/cports/blob/master/Packaging.md#hardening_options)|[2012](https://source.android.com/docs/security/enhancements/enhancements41)|yes|
|`-fcf-protection`/`-mcet`[^2]    |[no](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[2023](https://git.dpkg.org/cgit/dpkg/dpkg.git/commit/?id=8f5aca71c1435c9913d5562b8cae68b751dff663)|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|no|[2021](https://bugs.gentoo.org/822036)|[2019](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|yes|[2021](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/f409a72342bf37017f190021970efaaeac1bb619)|[2023](https://github.com/openbsd/src/commit/bba006a81846d90e529167c689ea0d456b4599bc)|[no](https://github.com/chimera-linux/cports/blob/master/src/cbuild/core/profile.py)|no|?|
|`-fsanitize=bounds`              |no|no|no|no|no|no|no|no|no|no|[2019](https://source.android.com/docs/security/enhancements/enhancements10), partial|no|
|`-fsanitize=cfi`[^2]             |no|no|no|no|no|no|no|no|no|[partial](https://github.com/search?q=repo%3Achimera-linux%2Fcports+%22cfi%22&type=code)|[2018](https://source.android.com/docs/security/test/cfi), partial|?|
|`-fsanitize=safe-stack`[^2]      |no|no|no|no|no|no|no|no|no|[no](https://github.com/chimera-linux/cports/blob/master/Packaging.md#hardening_options)|?|?|
|`-fsanitize=shadow-call-stack`[^2] |no|no|no|no|no|no|no|no|no|no|[2019](https://security.googleblog.com/2019/05/queue-hardening-enhancements.html), partial|?|
|`-fsanitize=signed-integer-overflow`/`-ftrapv`|no|no|no|no|no|no|no|no|[no](https://man.openbsd.org/clang-local)|[yes](https://github.com/chimera-linux/cports/blob/master/Packaging.md#hardening_options)|[2018](https://android-developers.googleblog.com/2018/06/compiler-based-security-mitigations-in.html), partial|?|
|`-fsanitize=undefined`|no|no|no|no|no|no|no|no|?|no|?|?|
|`-fstack-clash-protection`       |[2023](https://gitlab.alpinelinux.org/alpine/abuild/-/commit/4f7a2aff7b87cec7dd2783f95b5d6f744244c6c7)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[2018](https://fedoraproject.org/wiki/Changes/HardeningFlags28)|no|[2018](https://bugs.gentoo.org/675050)|[2019](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2018](https://en.opensuse.org/openSUSE:Security_Features)|[2021](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/f409a72342bf37017f190021970efaaeac1bb619)|?|[yes](https://github.com/chimera-linux/cports/blob/master/Packaging.md#hardening_options)|?|?|
|`-fstack-protector-strong`       |[yes](https://gitlab.alpinelinux.org/alpine/tsc/-/issues/64)|[yes](https://salsa.debian.org/toolchain-team/gcc/-/blob/master/debian/patches/gcc-distro-specs.diff)|[yes](https://src.fedoraproject.org/rpms/redhat-rpm-config//blob/rawhide/f/buildflags.md)|yes|[yes](https://wiki.gentoo.org/wiki/Hardened/Toolchain)|[2014](https://wiki.ubuntu.com/ToolChain/CompilerFlags)|[2006](https://en.opensuse.org/openSUSE:Security_Features)|[2014](https://gitlab.archlinux.org/archlinux/packaging/packages/pacman/-/commit/2ae260d290234c5fc4e5a2bd792d2d1b9e54f227)|[yes](https://man.openbsd.org/clang-local)|[yes](https://github.com/chimera-linux/cports/blob/master/Packaging.md#hardening_options)|[2015](https://android.googlesource.com/platform/build/+/8765b1035f813be2c26988a73cf3e9815aa5adf6)|?|
|`-fstack-protector`              |superseded|superseded|superseded|superseded|superseded|superseded|superseded|superseded|superseded|superseded|[2009](https://source.android.com/docs/security/enhancements/enhancements41)|?|
|`-ftrivial-auto-var-init=zero`   |no|[no](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=1010685)|no|no|[no](https://bugs.gentoo.org/913339)|[no](https://bugs.launchpad.net/ubuntu/+source/gcc-12/+bug/1972043)|no|no|?|[2023](https://github.com/chimera-linux/cports/commit/ad898a6b645b11dee989f4504e89577f5395ba24)|[2020](https://cs.android.com/android/_/android/platform/build/soong/+/59759dff24ffddca43a1940ed8615f96ee1e875f)|?|
|`-mbranch-protection=standard`/`-mbranch-target-enforce`|no|[2023](https://git.dpkg.org/cgit/dpkg/dpkg.git/commit/?id=8f5aca71c1435c9913d5562b8cae68b751dff663)|[2020](https://fedoraproject.org/wiki/Changes/Aarch64_PointerAuthentication)|no|no|[2023](https://launchpad.net/ubuntu/+source/dpkg/1.22.0ubuntu1)|no|no|[2023](https://github.com/openbsd/src/commit/990129f49dcc7205208dec5e29b252be8659896d)|[no](https://github.com/chimera-linux/cports/blob/master/src/cbuild/core/profile.py)|?|?|
|`-mshstk`                        |no|no|no|no|no|no|no|no|no|no|?|?|
|`-msign-return-address=[all/non-leaf]`|no|no|superseded|no|no|no|no|no|superseded|superseded|?|?|

Note that:
- some flags are incompatible between each other
- some flags are more useful than others
- some flags are superseding some others
- some libc are incompatible with some flags
- "partial" means "enabled in a lot of places, but not everywhere, with substantial caveats"
- while Google Chrome isn't a distribution, given the size of its source code,
  it's close enough™ to warrant inclusion in the table.


Sources and resources:
- https://src.fedoraproject.org/rpms/redhat-rpm-config//blob/rawhide/f/buildflags.md
- https://en.opensuse.org/openSUSE:Security_Features
- https://gcc.gnu.org/pipermail/gcc-patches/2023-August/628748.html
- https://wiki.gentoo.org/wiki/Hardened/Toolchain#Changes
- https://gitlab.archlinux.org/archlinux/rfcs/-/blob/master/rfcs/0003-buildflags.rst?ref_type=heads
- https://man.openbsd.org/clang-local
- https://sergesanspaille.fedorapeople.org/lpc2020.pdf
- https://wiki.ubuntu.com/Security/Features
- https://wiki.ubuntu.com/ToolChain/CompilerFlags
- https://fedoraproject.org/wiki/Security_Features_Matrix
- https://best.openssf.org/Compiler-Hardening-Guides/Compiler-Options-Hardening-Guide-for-C-and-C++.html

[^1]: As `-D_LIBCPP_ENABLE_HARDENED_MODE` only works for llvm18, which isn't in Alpine yet. It replaces `-D_LIBCPP_ASSERT` and `-D_LIBCPP_ENABLE_ASSERTIONS`.
[^2]: Not supported by [musl libc](https://musl.libc.org)
