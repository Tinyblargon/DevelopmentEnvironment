# Cache Disk

This document explains hot to configure the `.cache` folder to be stored on a different disk.

## Insall prerequisites

```bash
sudo apt install -y lvm2 xfsprogs
```

## Prepare the disk

Get the name of the disk in most cases it will be `/dev/sdb` or `/dev/vdb`.
You can use `lsblk` to find out.

```bash
export DISK_PATH="/dev/sdb"
```

```bash
sudo pvcreate $DISK_PATH -ff
sudo vgcreate cache-vg $DISK_PATH
sudo lvcreate --extents 100%FREE --name cache cache-vg
```

Since this will only be a cache disk we don't need a journaling filesystem.

```bash
sudo mkfs.xfs /dev/cache-vg/cache
```

## Mount the disk

Create a mount point:

```bash
sudo mkdir -p /mnt/cache
sudo chattr +i /mnt/cache # prevents accidenal writes to this folder if the disk is not mounted
```

Add the following line to `/etc/fstab`:

```bash
echo '/dev/cache-vg/cache /mnt/cache xfs defaults,nofail 0 2' | sudo tee -a /etc/fstab
```

Mount the disk:

```bash
sudo systemctl daemon-reload
sudo mount /mnt/cache
```

The cache disk is now mounted.

## Move the cache folder to the new disk

```bash
sudo mv ~/.cache /mnt/cache/$(whoami)
sudo chown -R $(whoami): /mnt/cache/$(whoami)
```

```bash
sudo mkdir ~/.cache
sudo chown -R $(whoami): ~/.cache
sudo chattr +i ~/.cache
```

Add a bind mount to `/etc/fstab`:

```bash
echo "/mnt/cache/$(whoami) /home/$(whoami)/.cache none defaults,bind 0 0" | sudo tee -a /etc/fstab
```

```bash
sudo systemctl daemon-reload
sudo mount /home/$(whoami)/.cache
```

Your `.cache` folder is now on a different disk.
