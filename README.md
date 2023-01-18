<p><img src="https://discuss.linuxcontainers.org/uploads/default/original/1X/9a2865f528f7b846cda54335dec298dda6109bb3.png" alt="lxd-logo" title="lxd" align="top" height=85 /></p>

*LXD is a next generation system container and virtual machine manager. It offers a unified user experience around full Linux systems running inside containers or virtual machines*

### General informations

This repository contains manifests to build custom LXD system container and virtual machine images using Distrobuilder.

**Images**

| Distribution   | Release   | Variants           | Container | Virtual machine |
| :--------------| :---------| :------------------| :---------| :---------------|
| Alma Linux     | `8`       | `default`, `cloud` | ✅        | ✅              |
| Alma Linux     | `9`       | `default`, `cloud` | ✅        | ✅              |
| Fedora         | `37`      | `default`, `cloud` | ✅        | ✅              |
| Ubuntu         | `focal`   | `default`, `cloud` | ✅        | ✅              |
| Ubuntu         | `jammy`   | `default`, `cloud` | ✅        | ✅              |
| Ubuntu         | `kinetic` | `default`, `cloud` | ✅        | ✅              |

**Variants**

* ***default*** - standard userspace
* ***cloud*** - standard userspace with an SSH server and `cloud-init` utilities embedded

#### Requirements

* LXD >= 4.0 (for virtual machines support)
* Distrobuilder >= 2.0
* Build tools
  - qemu-utils
  - debootstrap
  - btrfs-progs
  - rsync

### How to build these images ?

Firstly, install `distrobuilder` using `snap` :

```shell
snap install distrobuilder --classic [--edge]
```

Then, build the image using `distrobuilder`, you have multiple options :

* **Container image**

  ```shell
  distrobuilder build-lxd fedora.yml [options]
  ```

* **Virtual machine image**

  You need to add a `--vm` flag in order to build a virtual machine image :

  ```shell
  distrobuilder build-lxd ubuntu.yml --vm [options]
  ```

* **Build a specific image variant**

  ```shell
  distrobuilder build-lxd ubuntu.yml -o image.variant=cloud [options]
  ```

* **Choose a distribution release version**

  ```shell
  # Ubuntu
  distrobuilder build-lxd ubuntu.yml -o image.release=jammy [options]

  # Fedora
  distrobuilder build-lxd fedora.yml -o image.release=37 [options]

  # Alma Linux
  distrobuilder build-lxd almalinux.yml -o image.release=9 [options]
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

### References

* LXD : https://linuxcontainers.org/lxd/introduction/
* Distrobuilder : https://linuxcontainers.org/distrobuilder/introduction/
* Distrobuilder (doc) : https://distrobuilder.readthedocs.io/en/latest/
* Official LXD images manifests : https://github.com/lxc/lxc-ci/tree/master/images/
