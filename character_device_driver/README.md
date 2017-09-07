# Character Device Files

### 1. Major and Minor Numbers

Char devices are accessed through names in the filesystem. Those names are called special files or device files or simply nodes of the filesystem tree; they are conventionally located in the `/dev` directory. Special files for char drivers are identified by a `"c"` in the first column of the ouput of command `ls -l`

```
crw-------  1 root root     10, 175 Sep  5 22:59 agpgart
crw-------  1 root root     10, 235 Sep  5 22:59 autofs
drwxr-xr-x  2 root root         620 Sep  5 22:59 block
drwxr-xr-x  2 root root          80 Sep  5 22:59 bsg
crw-------  1 root root     10, 234 Sep  5 22:59 btrfs-control
drwxr-xr-x  3 root root          60 Sep  5 22:59 bus
lrwxrwxrwx  1 root root           3 Sep  5 22:59 cdrom -> sr0
lrwxrwxrwx  1 root root           3 Sep  5 22:59 cdrw -> sr0
drwxr-xr-x  2 root root        3660 Sep  7 08:18 char
```

There are two numbers (separated by a comma). These numbers are the major and minor device number for particular device. Ex: Major number = 10, Minor number =  175, 235, ...

* `Major number: ` identifies the driver associated with the device. Modern Linux kernels allow multiple drivers to share major numbers, but most devices that you will see are still organized on the one-major-one-driver principle. To obtain the major use: `MAJOR (dev)`

* `Minor number: ` is used by the kernel to determine exactly which device is being referred to. Depending on how your driver is written, you can either get a direct pointer to your device from the kernel, or you can use the minor number yourself as an index into a local array of devices. To obtain the minor use: `MINOR (dev)`

If, instead, you have the major and minor numbers and need to turn them into a dev use:
`MKDEV (int major, int minor)`

### 2. The file_operations Structure

The file_operations structure is defined in `linux/fs.h` and holds pointers to functions defined by the driver that perform various operations on the device.
