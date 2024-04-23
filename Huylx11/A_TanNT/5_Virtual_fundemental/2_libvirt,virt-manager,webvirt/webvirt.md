# Webvirtmgr là gì?

[Hướng dẫn cách cài webvirtcloud](https://news.cloud365.vn/kvm-huong-dan-cai-dat-webvirtcloud-quan-li-ha-tang-kvm/)

- webvirt là một phần mềm giúp cho người dùng có thể tương tác với VM từ xa
- webvirtmgr và webvirtcloud đều là các công cụ quản lý dựa trên web để quản lý KVM

[Install webvirtcloud in ubuntu 20.04](https://www.howtoforge.com/how-to-install-webvirtcloud-kvm-management-on-ubuntu-20-04/)

# Khởi động VM với kvm mode

[huong dan dùng vmware-kvm.exe](https://us.informatiweb-pro.net/virtualization/vmware/vmware-workstation-15-use-your-vms-in-kvm-mode.html)

_Lưu ý: các command này phải được thực hiện trong folder VMware Workstation với file path: `C:\Program Files (x86)\VMware\VMware Workstation`_

- `.\vmware-kvm.exe "C:\Users\lxhuy\OneDrive\Documents\Virtual Machines\Ubuntu 64-bit\Ubuntu 64-bit.vmx"` để bật vm với kvm mode
- `.\vmware-kvm.exe --power-off "C:\Users\lxhuy\OneDrive\Documents\Virtual Machines\Ubuntu 64-bit\Ubuntu 64-bit.vmx"` để tắt vm
- `.\vmware-kvm.exe --detach "C:\Users\lxhuy\OneDrive\Documents\Virtual Machines\Ubuntu 64-bit\Ubuntu 64-bit.vmx"` để tách vm khỏi kvm mode
- `.\vmware-kvm.exe --exit` để tắt kvm mode
- cùng thêm với những option khác:
  - --suspend
  - --reset