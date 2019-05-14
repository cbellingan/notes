## GPU passthrough
It looks like Nvidia purposfully block the consumer grade GPU drivers from loading if they detect they are running in a virt. This manifests as a general 'code 43' error in windows. There are a ton of random sites dealing with this the ones below are the best and the fix is to force kvm to not report that the guest is a virt by editing the guests XML used by libvert.

* [description](https://passthroughpo.st/apply-error-43-workaround/)
* [virsh-patcher](https://github.com/PassthroughPOST/virsh-patcher)

## sr/iov
This allows you to create virtul functions (VF) from PCI devices supporting this and pass them through to the guests.

[redhad sriov](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/sect-pci_devices-pci_passthrough)

## ref
* [RHEL virtualization guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/index)
* [windows 10 VM perf](https://heiko-sieger.info/windows-10-virtual-machine-benchmarks/)
* [windows 10 as VM](https://heiko-sieger.info/running-windows-10-on-linux-using-kvm-with-vga-passthrough/)
* [make boot loader](https://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)
* [windows 10 iso downloader](https://www.windowscentral.com/e?link=https%3A%2F%2Fmicrosoft.msafflnk.net%2Fc%2F159229%2F433017%2F7593%3FsubId1%3DUUwpUdUnU50931%26subId2%3Ddwp%26url%3Dhttps%253A%252F%252Fwww.microsoft.com%252Fen-us%252Fsoftware-download%252Fwindows10&token=jYKEYCDD)
* [FreeNAS](https://www.freenas.org/download-freenas-release/)
* [TensorFlow](https://www.tensorflow.org/install/)
* [PortTainer docker UI](https://www.portainer.io/overview/)

## VBS to extract your windows key
I'm moving the same license to the new machine and no longer have the old one. This has to be run  as Admin.
* [howto geek](https://www.howtogeek.com/206329/how-to-find-your-lost-windows-or-office-product-keys/)

```
Set WshShell = CreateObject("WScript.Shell")
MsgBox ConvertToKey(WshShell.RegRead("HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\DigitalProductId"))

Function ConvertToKey(Key)
Const KeyOffset = 52
i = 28
Chars = "BCDFGHJKMPQRTVWXY2346789"
Do
Cur = 0
x = 14
Do
Cur = Cur * 256
Cur = Key(x + KeyOffset) + Cur
Key(x + KeyOffset) = (Cur \ 24) And 255
Cur = Cur Mod 24
x = x -1
Loop While x >= 0
i = i -1
KeyOutput = Mid(Chars, Cur + 1, 1) & KeyOutput
If (((29 - i) Mod 6) = 0) And (i <> -1) Then
i = i -1
KeyOutput = "-" & KeyOutput
End If
Loop While i >= 0
ConvertToKey = KeyOutput
End Function
```
