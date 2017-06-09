# qubes-nodemcu

## install

Just put the file and the symlinks in `/usr/local/etc/qubes-rpc` in `sys-usb`
(or wherever you attached your USB host PCI device).

Then set up appropriate policy (`/etc/qubes-rpc/policy/nodemcu.*` in dom0).
My suggestion:

```
nodemcu-dev allow sys-usb,user=root
```

## usage

### nodemcu.UploadFile

This one behaves differently on Qubes<=R3.1 and Qubes>=R3.2, because since R3.2
there is a possibility for passing an argument to RPC call. Therefore, in R3.2
and later, the filename should be passed as argument. On R3.1, the filename
should be the first line of the data.

R3.1:
```
qrexec-client-vm sys-usb nodemcu.UploadFile /bin/sh -c 'echo init.lua; cat init.lua'
```

R3.2:
```
qrexec-client-vm sys-usb nodemcu.UploadFile+init.lua < init.lua
```

### nodemcu.UploadCA
```
qrexec-client-vm sys-usb nodemcu.UploadCA < isrgrootx1.pem
```

### nodemcu.Restart
```
qrexec-client-vm sys-usb nodemcu.Restart
```

<!-- vim: set ft=markdown ts=4 sts=4 sw=4 et tw=80 : -->
