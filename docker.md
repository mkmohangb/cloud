### OverlayFS

How to know if current shell is inside a Docker container or not?
```Shell
> findmnt /
TARGET SOURCE  FSTYPE  OPTIONS
/      overlay overlay rw,relatime,lowerdir=/var/lib/docker/overlay2/l/2BKZYT7DSBOB576UNDXZTPXFKY:...
```
In this case the root filesystem is from a Docker overlay mount, making it highly likely it's a Docker container.

Docker images are often composed of like 25 “layers”. Overlayfs supports having multiple lower directories, so you can run

```Shell
mount -t overlay overlay
      -o lowerdir:/dir1:/dir2:/dir3:...:/dir25,upperdir=...
```
So I assume that’s how containers with many Docker layers work, it just unpacks each layer into a separate directory and then asks overlayfs to combine them all together with an empty upper directory that the container will write its changes to it.

### References
- https://jvns.ca/blog/2019/11/18/how-containers-work--overlayfs/
- https://askubuntu.com/questions/1309425/how-to-know-if-current-shell-is-from-a-docker-os-or-system-main-os
