# Oracle VirtualBox

## Troubleshooting
* VirtualBox can't operate in VMX root mode. Please disable the KVM kernel extension, recompile your kernel and reboot **`(VERR_VMX_IN_VMX_ROOT_MODE)`**.
```bash
Result Code: NS_ERROR_FAILURE (0X80004005)
Component: ConsoleWrap
Interface: IConsole {6ac83d89-6ee7-4e33-8ae6-b257b2e81be8}
```
  * Solution:
    1. List all module related to **`kvm`**: `sudo lsmod | grep vm`
    2. Now remove **`kvm_intel`**: `sudo rmmod kvm_intel`


