<p><img src="https://discuss.linuxcontainers.org/uploads/default/original/1X/9a2865f528f7b846cda54335dec298dda6109bb3.png" alt="lxd-logo" title="lxd" align="top" height=105 /></p>

Manifests to build custom LXD system container and virtual machine images using Distrobuilder.

### General informations

#### Images

The following distribution images can be built :

| Distribution   | Default release   | Variant      | Architecture | Container  | Virtual machine  |
| :--------------| :-----------------| :------------| :------------| :--------- | :--------------- |
| Fedora         | `35`              | `default`    | `x86_64`     | ✅         | ✅               |
|                |                   |              |              |            |                  |
| Ubuntu         | `impish` (21.10)  | `default`    | `amd64`      | ✅         | ✅               |
| Ubuntu         | `impish` (21.10)  | `default`    | `arm64`      | ✅         | ❌               |
| Ubuntu         | `impish` (21.10)  | `k8s`        | `amd64`      | ❌         | ✅               |

#### Requirements

- LXD >= 4.0 (for virtual machines support)
- Distrobuilder >= 2.0

### How to build these images ?

Firstly, install `distrobuilder` using `snap` :

```shell
snap install distrobuilder --classic [--edge]
```

Then, build the image using `distrobuilder` (and import it directly) :

* **Container image**

  ```shell
  distrobuilder build-lxd fedora.yml --import-into-lxd=<image alias> [options]
  ```

* **Virtual machine image**

  You need to add a `--vm` flag in order to build a virtual machine image :

  ```shell
  distrobuilder build-lxd ubuntu.yml --import-into-lxd=<image alias> --vm [options]
  ```

* **Build image for Raspberry Pi (ARM64)**

  To build an image on Raspberry Pi, you need to specify the architecture and an alternative URL for source packages :

  ```shell
  distrobuilder build-lxd ubuntu.yml -o image.architecture=arm64 -o source.url=http://ports.ubuntu.com/ubuntu-ports [options]
  ```

### References

* LXD : https://linuxcontainers.org/lxd/introduction/
* Distrobuilder : https://linuxcontainers.org/distrobuilder/introduction/
* Distrobuilder (doc) : https://distrobuilder.readthedocs.io/en/latest/
* Official LXD images manifests : https://github.com/lxc/lxc-ci/tree/master/images/
