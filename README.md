# Mount Image Partition action

An action that mounts an image partition inside a Ubuntu runner.

The main difference with other mount actions is that this one supports disk images, addressing a particular partition inside the image, using the `partitionIndex` input.

This is useful for OS images where multiple partitions (e.g.: `boot`, `root`, `recovery`, ...) might be available.

# Inputs

- `imagePath`: Path to image file.
- `mountPoint`: Path to mount point. Defaults to `/mnt/`.
- `partitionIndex`: Partition index in image, starting from 1. Defaults to 1.
- `extraDiskSpace`: Extra disk space to add to the partition in MiB. Defaults to 0 MiB.

# Examples

## Mounting an image 'boot' and 'root' partitions

```
- name: Mount root partition
  id: mount-root
  uses: jcapona/mount-image-partition-action@v1.0
  with:
    imagePath: image_file.img
    mountPoint: /tmp/img
    partitionIndex: 2

- name: Mount boot partition
  id: mount-boot
  uses: jcapona/mount-image-partition-action@v1.0
  with:
    imagePath: image_file.img
    mountPoint: /tmp/img/boot
    partitionIndex: 1

```

## Updating an OS image

Check [this workflow](https://github.com/jcapona/mount-image-partition-action/tree/main/.github/workflows/update-raspberry-pi-os.yml) included in the repository. 
It downloads a Raspberry Pi OS image; mounts it, updates it and uploads the image as an artifact.

# Outputs

| **Value**        | **Description**                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `loopbackDevice` | Loopback device for mounted partition (e.g. `/dev/loop0`)                                                                        |
| `imagePath`      | Path to mounted image. Might be different to the input image path if extra disk space was added (e.g.: `/tmp/qwe.qwe/image.img`) |