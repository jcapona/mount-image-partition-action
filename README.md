# Mount Image Partition action

An action that mounts an image partition. Based on [damianperera/mount-image-action](https://github.com/damianperera/mount-image-action).

# Inputs

- `imagePath`: Path to image file.
- `mountPoint`: Path to mount point. Defaults to `/mnt/`.
- `partitionIndex`: Partition index in image. Defaults to 1.
- `filesystem`: Partition filesystem. Defaults to `ext4`.

# Examples

## Mounting an image 'boot' and 'root' partitions

```
- name: Mount root partition
  id: mount-root
  uses: jcapona/mount-image-partition-action@v0.3
  with:
    imagePath: image_file.img
    mountPoint: /tmp/img
    partitionIndex: 1
    filesystem: ext4

- name: Mount boot partition
  id: mount-boot
  uses: jcapona/mount-image-partition-action@v0.3
  with:
    imagePath: image_file.img
    mountPoint: /tmp/img/boot
    partitionIndex: 0
    filesystem: vfat

```

## Updating an OS image

Check [this workflow](https://github.com/jcapona/mount-image-partition-action/tree/main/.github/workflows/update-raspberry-pi-os.yml) included in the repository. It downloads an OS image, mounts it, updates it and uploads the image as an artifact.

# Outputs

| **Value**      | **Description**                                           |
| -------------- | --------------------------------------------------------- |
| `deviceMapper` | Device for mounted partition (e.g. `/dev/mapper/loop5p1`) |
