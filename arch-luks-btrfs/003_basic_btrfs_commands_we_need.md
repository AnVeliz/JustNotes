# Some of the commands I need to have at hand</br>

### List all subvolumes
-> **btrfs subvolume list MOUNT_POINT**</br>
E.g.: -> btrfs subvolume list /</br>

### Create a snapshot</br>
-> **btrfs subvolume snapshot VOLUME /.snapshots/NAME_OF_THE_SNAPSHOT**</br>
E.g.: -> btrfs subvolume snapshot / /.snapshots/initial_system_snap</br>

### Create a read-only snapshot</br>
-> **btrfs subvolume snapshot VOLUME /.snapshots/NAME_OF_THE_SNAPSHOT**</br>
E.g.: -> btrfs subvolume snapshot -r / /.snapshots/initial_system_rosnap</br>

### Remove a snapshot</br>
-> **btrfs subvolume delete SNAPSHOT_PATH**</br>
E.g.: btrfs subvolume delete /.snapshots/initial_system_snap</br>


### Restore root from a snapshot!</br>
-> **o=defaults,x-mount.mkdir**</br>
-> **o_btrfs=$o,compress=lzo,ssd,noatime**</br>
-> **mount -t btrfs -o subvol=root,$o_btrfs LABEL=system /mnt**</br>
-> **rm -rf /mnt**</br>
-> **cp /.snapshots/*SNAPSHOT_NAME*/\* /mnt/**</br>
E.g.: -> cp /.snapshots/initial_snapshot_rosnap/* /mnt/</br>
