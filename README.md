# Failed-to-mount-home-Timeshift-and-btrfs

Issue: When using Timeshift with Btrfs, some users encounter an error where the system fails to mount /home after restoring from a snapshot. The error message might look like:

```[FAILED] Failed to mount /boot.
[DEPEND] Dependency failed for Local File Systems.
You are in emergency mode. After logging in, type "journalctl -xb" to view system logs, "systemctl reboot" to reboot, "systemctl default" or "exit" to boot into default mode.
Give root password for maintenance
(or press Control-D to continue): _
```

The ***/etc/fstab*** file is a configuration file that determines how partitions are mounted in the system. We will remove the problematic ***subvolid=xxx$*** entry.

**STEP**

1. Enter root terminal or enter the password in the emergency mode.
   
2. Open the ***/etc/fstab*** file for editing:
   
      ```sudo nano /etc/fstab```
  
3. Locate the line related to the /home partition that uses subvolid=xxx$. It might look something like this:
   
      ```UUID=xxx-yyy-zzz  /home  btrfs  rw,noatime,compress=zstd:3,ssd,space_cache,commit=120,subvolid=257,subvol=/@home 0 0```
  
4. Remove the subvolid=xxx$ part from the line so it looks like this:
   
      ```UUID=xxx-yyy-zzz  /home  btrfs  rw,noatime,compress=zstd:3,ssd,space_cache,commit=120,subvol=/@home 0 0```

5. Save the file by pressing Ctrl + O and then exit with Ctrl + X.

