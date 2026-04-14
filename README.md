# rpi-manifests

Yocto environment preparation for Raspberry Pi builds, now migrated to
[kas](https://kas.readthedocs.io/).

## Prerequisites

- Python 3.8+
- Git
- Network access to clone public layer repositories (including `meta-rpilinux`)

## Install kas

Recommended (isolated install with `pipx`):

```bash
pipx install kas
```

Alternative (distribution package, may be older):

```bash
sudo apt update
sudo apt install -y kas
```

## Quick start (kas)

1. Clone this repository:

   ```bash
   git clone https://github.com/ivrabie/rpi-manifests.git
   cd rpi-manifests
   ```

2. Checkout all Yocto layers and generate build configuration:

   ```bash
   kas checkout kas/rpi-scarthgap.yml
   ```

3. Build:

   ```bash
   kas build kas/rpi-scarthgap.yml
   ```

kas keeps Yocto working data under `build/` (`build/sources`, `build/downloads`, `build/sstate-cache`, `build/tmp`).

## Common kas commands

- `kas checkout kas/rpi-scarthgap.yml` - Prepare/update source tree in `build/sources` and generate build dir
- `kas checkout --update kas/rpi-scarthgap.yml` - Pull latest commits on tracked branches
- `kas shell kas/rpi-scarthgap.yml` - Enter configured build environment shell
- `kas shell kas/rpi-scarthgap.yml -c 'bitbake-layers show-layers'` - Inspect active layers
- `kas lock --update kas/rpi-scarthgap.yml` - Create/update lockfile with pinned commits

## Configuration files

- `kas/base.yml` - Repository and layer definitions checked out under `build/sources`, including ROS layers from `meta-ros`
- `kas/rpi-scarthgap.yml` - Build profile (`MACHINE`, `DISTRO`, `TARGET`) plus `local_conf_header` tuning migrated from local.conf (including `DL_DIR` and `SSTATE_DIR` under `build/`)

ROS layers enabled in `kas/base.yml`:

- `meta-ros-common`
- `meta-ros2`
- `meta-ros2-jazzy`

Defaults in `kas/rpi-scarthgap.yml`:

- `MACHINE = raspberrypi4-64`
- `DISTRO = poky`
- `TARGET = rpilinux-image`

You can override these at runtime:

```bash
KAS_MACHINE=raspberrypi5 KAS_TARGET=core-image-base kas build kas/rpi-scarthgap.yml
```
