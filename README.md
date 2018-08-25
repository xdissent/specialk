# specialk

> Special kernels for special people

`specialk` is a tool to build customized versions of the official debian kernel packages. It generally follows the steps from [the wiki](https://wiki.debian.org/HowToCrossBuildAnOfficialDebianKernelPackage), applying custom patches, configs and definitions. A special kernel _flavour_ is created to avoid any ABI changes that would prevent the package from building, installing or playing well with other packages. Only the architecture-dependent packages are created, and are compatible with released versions of the architecture-independent packages.

## Requirements

The following packages are _always_ required for kernel building and will be auto-installed if missing:

- `bc`
- `bison`
- `cpio`
- `curl`
- `dh-exec`
- `dpkg-dev`
- `fakeroot`
- `flex`
- `g++-7`
- `gcc-7`
- `git`
- `kernel-wedge`
- `libssl-dev`
- `make`
- `python3`
- `quilt`
- `rsync`

Kernel building may require various other packages depending on configuration. For cross-compilation, the following packages will generally be required:

- `dpkg-cross`
- `g++-7-<arch>-linux-gnu`
- `gcc-7-<arch>-linux-gnu`

> Note: As of August 2018, current kernels are built with gcc-7. The current `crossbuild-essential-<arch>` meta packages install gcc-8 rather than gcc-7, so the specific `gcc-7-<arch>-linux-gnu` and `g++-7-<arch>-linux-gnu` packages are required.

The `ccache` package is optionally supported.

## Usage

All configuration is done with environment variables:

| Name          | Description                | Default                                          |
| ------------- | -------------------------- | ------------------------------------------------ |
| `SPK_TRACE`   | Debug command execution    | not set                                          |
| `SPK_BUILD`   | Path in which to build     | `.`                                              |
| `SPK_PATCHES` | Path to kernel patches     | `./patches`                                      |
| `SPK_CONFIG`  | Path to kernel config      | `./config`                                       |
| `SPK_DEFINES` | Path to kernel defines     | `./defines`                                      |
| `SPK_ARCH`    | Target Architecture        | current architecture                             |
| `SPK_FSET`    | Target kernel featureset   | `none`                                           |
| `SPK_FLAV`    | Kernel flavour name        | `spk`                                            |
| `SPK_DESC`    | Kernel flavour description | `special people`                                 |
| `SPK_REPO`    | Kernel repository          | `https://salsa.debian.org/kernel-team/linux.git` |
| `SPK_TAG`     | Kernel repo branch or tag  | current debian release                           |
| `SPK_MIRROR`  | Debian source package repo | `http://http.debian.net/debian`                  |

Run `specialk` to build the packages.
