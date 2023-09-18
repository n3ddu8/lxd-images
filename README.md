<p><img src="https://discuss.linuxcontainers.org/uploads/default/original/1X/9a2865f528f7b846cda54335dec298dda6109bb3.png" alt="lxd-logo" title="lxd" align="top" height=85 /></p>

*LXD is a next generation system container and virtual machine manager. It offers a unified user experience around full Linux systems running inside containers or virtual machines*

### General informations

This repository contains my personal manifests to build custom LXD container and virtual machine images using Distrobuilder in my homelab.

**Images**

The following images are known to work using these manifests, other distribution versions may not work.

| Distribution   | Release   | Variants  | Container | Virtual machine |
| :--------------| :---------| :---------| :---------| :---------------|
| Alpine Linux   | `3.18`    | `default` | ✅        | ✅              |
| Ubuntu         | `focal`   | `default` | ✅        | ✅              |
| Ubuntu         | `jammy`   | `default` | ✅        | ✅              |

\* *Virtual machine images only*

#### Requirements

* LXD >= 4.0 (for virtual machines support)
* Distrobuilder >= 2.0
* Build tools
  - *qemu-utils*
  - *debootstrap*
  - *btrfs-progs*
  - *rsync*

### How to build these images ?

Firstly, install `distrobuilder` using `snap` :

```shell
snap install distrobuilder --classic [--edge]
```

Then, build the image using `distrobuilder`, you have multiple options :

* **Container image**

  ```shell
  distrobuilder build-lxd ubuntu.yml [options]
  ```

* **Virtual machine image**

  You need to add a `--vm` flag in order to build a virtual machine image :

  ```shell
  distrobuilder build-lxd ubuntu.yml --vm [options]
  ```

* **Choose a distribution release version**

  ```shell
  # Ubuntu
  distrobuilder build-lxd ubuntu.yml -o image.release=jammy [options]
  ```

* **Use a tmpfs for build cache**

  It can be interesting to use a tmpfs to speed up the build and preserve SSDs if a lot of image builds are planned :

  ```shell
  mkdir -p /var/cache/distrobuilder/build
  mount -t tmpfs -o rw,size=4G,uid=0,gid=0,mode=1755 tmpfs /var/cache/distrobuilder/build
  ```

  Build the image by specifying the tmpfs cache directory :

  ```shell
  distrobuilder build-lxd ubuntu.yml --cache-dir=/var/cache/distrobuilder/build
  ```

* **Adding the container image to LXD**

  Add the container image to a LXD installation :

  ```shell
  lxc image import lxd.tar.xz rootfs.squashfs --alias mycontainerimage
  ```

  Launch a container from the freshly created container image :

  ```shell
  lxc launch mycontainerimage c1

### References

* LXD : https://linuxcontainers.org/lxd/introduction/
* Distrobuilder : https://linuxcontainers.org/distrobuilder/introduction/
* Distrobuilder (doc) : https://distrobuilder.readthedocs.io/en/latest/
* Official LXD images manifests : https://github.com/lxc/lxc-ci/tree/master/images/
