<p><img src="https://discuss.linuxcontainers.org/uploads/default/original/1X/9a2865f528f7b846cda54335dec298dda6109bb3.png" alt="lxd-logo" title="lxd" align="top" height=105 /></p>

Manifests to build custom LXD system container and virtual machine images using Distrobuilder.

### General informations

#### Images

* **Distributions matrix**

  | Distribution   | Release   | Variant    | Architecture | Container | Virtual machine |
  | :--------------| :---------| :----------| :------------| :---------| :---------------|
  | Fedora         | `36`      | `default`  | `x86_64`     | ✅        | ✅              |
  |                |           |            |              |           |                 |
  | Rocky Linux    | `8`       | `default`  | `x86_64`     | ✅        | ✅              |
  |                |           |            |              |           |                 |
  | Ubuntu         | `jammy`   | `default`  | `amd64`      | ✅        | ✅              |
  | Ubuntu         | `jammy`   | `minimal`  | `amd64`      | ✅        | ✅              |
  | Ubuntu         | `focal`   | `default`  | `amd64`      | ✅        | ✅              |

* **Variants**

  - ***default*** - standard userspace with cloud-init capabilities
  - ***minimal*** - minimal userspace without cloud-init, ssh server nor debugging utilities.

#### Requirements

- LXD >= 4.0 (for virtual machines support)
- Distrobuilder >= 2.0

### How to build these images ?

Firstly, install `distrobuilder` using `snap` :

```shell
snap install distrobuilder --classic [--edge]
```

Then, build the image using `distrobuilder`, you have multiple options :

* **Container image**

  ```shell
  distrobuilder build-lxd fedora.yml --import-into-lxd=<image alias> [options]
  ```

* **Virtual machine image**

  You need to add a `--vm` flag in order to build a virtual machine image :

  ```shell
  distrobuilder build-lxd ubuntu.yml --import-into-lxd=<image alias> --vm [options]
  ```

* **Choose a distribution release version**

  ```shell
  # Ubuntu
  distrobuilder build-lxd ubuntu.yml -o image.release=jammy [options]

  # Fedora
  distrobuilder build-lxd fedora.yml -o image.release=36 [options]
  ```

* **Use a tmpfs for build cache**

  It can be interesting to use a tmpfs to speed up the build and preserve SSDs if a lot of image builds are planned :

  ```shell
  mkdir -p /var/cache/distrobuilder/build
  mount -t tmpfs -o rw,size=4G,uid=0,gid=0,mode=1755 tmpfs /var/cache/distrobuilder/build
  ```

  Build the image by specifying the tmpfs cache directory :

  ```shell
  distrobuilder build-lxd ubuntu.yml --import-into-lxd=<image alias> --cache-dir=/var/cache/distrobuilder/build
  ```

### References

* LXD : https://linuxcontainers.org/lxd/introduction/
* Distrobuilder : https://linuxcontainers.org/distrobuilder/introduction/
* Distrobuilder (doc) : https://distrobuilder.readthedocs.io/en/latest/
* Official LXD images manifests : https://github.com/lxc/lxc-ci/tree/master/images/
