<p><img src="https://discuss.linuxcontainers.org/uploads/default/original/1X/9a2865f528f7b846cda54335dec298dda6109bb3.png" alt="lxd-logo" title="lxd" align="top" height=105 /></p>

Manifests to build LXD images using Distrobuilder (containers and virtual machines).

### Images

The following images can be built :

| Name           | Release    | Variant      | Architecture | Container   |  Virtual machine     |
| :--------------| :----------| :------------| :------------| :-----------| :------------------- |
| Fedora         | 35         | `default`    | `x86_64`     | ✅          | ✅                  |
|                |            |              |              |             |                      |
| Ubuntu         | 21.10      | `default`    | `x86_64`     | ✅          | ✅                  |
| Ubuntu         | 21.10      | `k8s`        | `x86_64`     | ❌          | ✅                  |

### Requirements

- LXD >= 4.0
- Distrobuilder >= 2.0

### How to build these images ?

Firstly, install `distrobuilder` using `snap` :

```shell
$ snap install distrobuilder --classic
```

Then, build the image using `distrobuilder` (and import it directly) :

* **Container image**

  ```shell
  $ distrobuilder build-lxd fedora/default.yml --type=unified --compression=zstd --import-into-lxd=<image alias>
  ```

* **Virtual machine image**

  ```shell
  $ distrobuilder build-lxd ubuntu/default.yml --type=unified --compression=zstd --vm --import-into-lxd=<image alias>
  ```

You can also specify a distribution release version or architecture with the `-o image.*` flag :

  ```shell
  $ distrobuilder build-lxd fedora/default.yml -o image.release=35 [options]
  $ distrobuilder build-lxd ubuntu/default.yml -o image.release=impish -o image.architecture=arm64 [options]
  ```
### References

* LXD : https://linuxcontainers.org/lxd/introduction/
* Distrobuilder : https://linuxcontainers.org/distrobuilder/introduction/
* Distrobuilder (doc) : https://distrobuilder.readthedocs.io/en/latest/
* Official LXD images manifests : https://github.com/lxc/lxc-ci/tree/master/images/
