
# `testdisk` Command
A command to recover missing partitions and repair corrupt ones. See official documentation at [TestDisk Step By Step - CGSecurity](https://www.cgsecurity.org/wiki/TestDisk_Step_By_Step)

# TestDisk
TestDisk is a powerful command-line tool for recovering lost partitions and repairing file systems. It is particularly useful in Linux-based environments.

## Using TestDisk via SSH
You can use TestDisk via SSH on your Linux system. This is often faster and more direct than moving the drive to a PC, especially since the drive is already formatted for a Linux-based environment.

Here's how to run it:

### 1. Locate the Drive Path
Before starting the tool, you need to know how your system identifies your external USB drive.

- SSH into your system as an administrator.
- Switch to the root user (TestDisk requires full hardware access):
  - List the connected drives:
    
    ```bash
    lsblk
    # OR
    fdisk -l
    ```
- Identify your drive: for a connected USB SSD drive It will likely be something like `/dev/sdu` or `/dev/sdq1`.

### 2. Launch TestDisk

Once you have the path (let's assume it is `/dev/sdu`), run:

```bash
testdisk
```

### 3. The Recovery Steps

The interface is text-based but very logical. Use your arrow keys and Enter.

- **Log:** Select `[ Create ]` (to log the session).
- **Select Disk:** Highlight the drive you identified in Step 1 (e.g., `/dev/sdu`).
- **Partition Table:** Select `[ EFI GPT ]` (GPT is commonly used for modern external drives). If it auto-detects `[ Intel ]`, go with the auto-detection.
- **Analyse:** Select `[ Analyse ]` then `[ Quick Search ]`.
- **Identify Partition:**
    - If TestDisk finds the lost partition, it will highlight it in green.
    - Press "P" to list the files. If you see your actual backup data, you are in business.
    - Press Q to go back to the list.
- **Write:** _If the files looked correct, press Enter._
    - Select `[ Write ]` and confirm with Y.
    - This writes the fixed "map" back to the SSD.

### 4. Refresh the System

Once finished, exit TestDisk (Q until you are back at the command prompt).

- Unplug the USB cable and wait 10 seconds.
- Plug it back in.
- Check your system's disk management utility (e.g., `lsblk`, `fdisk -l`, or a graphical disk utility). The system should now recognize the partition and mount it automatically.