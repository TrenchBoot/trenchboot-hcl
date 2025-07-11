# TrenchBoot Hardware Compatibility List

HCL reports for the [TrenchBoot Project](https://trenchboot.org/).

## Hardware requirements

In order to have a slight chance of success, you must meet the minimum
[hardware requirements](https://trenchboot.org/user-docs/requirements/).
They will be briefly described here. The goal of this section is not to
describe all of the requirements and details about them. It focuses on the most
important ones and easiest to check by a regular user.

### TPM

You need a
[Trusted Platform Module (TPM)](https://en.wikipedia.org/wiki/Trusted_Platform_Module)
of some sort. It may come as a discrete module attached to the board (dTPM), or
as a firmware TPM (fTPM). Usually it's configurable in BIOS settings and
enabled by default. In case of no TPM being detected by the tools, check the
BIOS settings.

### CPU

#### AMD

There are no prerequisites to check.
[AMD Zen](https://en.wikipedia.org/wiki/Zen_(microarchitecture)) or newer CPUs
will likely not work in the current stage of development, although
contributions are still welcome, as we have very little data points here.

#### Intel

1. Identify the model of your CPU by any means available:
  - physical inspection
  - Windows (e.g. `My Computer`)
  - Linux (e.g. `lscpu`) command
1. Go to [Intel Products page](https://www.intel.com/content/www/us/en/products/overview.html)
   and enter the CPU model name in the search bar (`e.g. i5-8500T`)
1. Check whether the ` Intel® Trusted Execution Technology ` in `Security &
   Reliability` table is marked as `Yes`. If you cannot find such entry, your
   CPU does not support `TXT`, and you will not be able to use TrenchBoot.
1. Go into the BIOS settings of your machine and look for the
   `Trusted Execution Technology (TXT)` option. It is usually disabled and must
   be enabled first.
1. With this set of preparation, you are good to try the HCL tools to see if
   your system is applicable for TrenchBoot.

## Contributing

### Success cases

This section presents the process of reporting success cases. By such cases we
mean those resulting in booting TrenchBoot entries into Linux login prompt. If
it fails to boot (e.g. platform reboots automatically after selection), please
refer to the next section. 

> **Note:** A bunch of `error: SINIT ACM does not match platform.` or similar
> errors appearing on the screen after you select boot menu entry is still
> considered a success, as long as `Press any key to continue...` appears, and
> you will be able to boot into Linux prompt after that.
 
1. Go into
   [meta-trenchboot releases](https://github.com/zarhus/meta-trenchboot/releases)
   and download the latest image.
1. [Flash](https://github.com/zarhus/meta-trenchboot?tab=readme-ov-file#flash)
   the image to USB stick.
1. [Boot](https://github.com/zarhus/meta-trenchboot?tab=readme-ov-file#booting)
   the image.
1. Select `Boot Linux with TrenchBoot`
   - login as: `root`
   - execute `trenchboot-hcl-report` command
   - send a Pull Request with resulting `.yml` file and (optionally) `.cpio.gz`
   file to: `<version>/success/linux` directory in this repository
1. Select `Boot Linux with Xen (EFI)`
   - login as: `root`
   - execute `trenchboot-hcl-report` command
   - send a Pull Request with resulting `.yml` file and (optionally) `.cpio.gz`
   file to: `<version>/success/xen` directory in this repository

### Failed cases

The failure will usually result in a platform automatically rebooting after
selecting one of the `TrenchBoot` boot entries. In such a case:
- **important** - do not reboot or otherwise power cycle the platform by
  yourself; if you do, select the failing entry once again, and simply wait for
  the platform to reboot by itself
- enter `Boot Linux normally` boot menu entry
- login as: `root`
- execute `trenchboot-hcl-report` command
- send a Pull Request with resulting `.yml` file and (optionally) `.cpio.gz`
file to: `<version>/failure/linux` or `<version>/failure/xen` directory in
this repository, depending on which of the options failed to boot

In case of a different failures or problems regarding this HCL process, feel
free to ask in the
[trenchboot-issues](https://github.com/TrenchBoot/trenchboot-issues/issues)
repository.
