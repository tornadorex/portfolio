# How to Partition Your Hard Drive in Windows 11

Why partition a hard drive? You may want the option to dual-boot, or better organize your data, or have an easier time backing up your data. You may even want to run different file systems on a single disk. Regardless your reason, partitioning a hard drive in Windows 11 is a simple process, but not without the risk of data loss. **Before you begin, back up your files.**

1. Press the **Windows** key and search for "partition".

![Search for "partition"](https://www.natebee.com/portfolio/writing/images/partition_search.png)

2. Select **Create and format hard drive partitions** to open the Disk Management tool.

![Windows 11 Disk Management tool](https://www.natebee.com/portfolio/writing/images/partition_disk-management.png)

3. Right-click the volume you want to partition and select **Shrink Volume**.

![Right-click to open the context menu for the disk being partitioned](https://www.natebee.com/portfolio/writing/images/partition_right-click.png)

4. Enter the size you want to allocate for this partition, labeled in the UI as **Enter the amount of space to shrink in MB**. This means that if you want a 100 GB partition, enter 100000.

![The Shrink volume dialog](https://www.natebee.com/portfolio/writing/images/partition_shrink-dialog.png)

5. Click **Shrink**. The new partition shows up as Unallocated space in the disk visualizer.

![Unallocated space in the disk visualizer](https://www.natebee.com/portfolio/writing/images/partition_unallocated-space.png)

6. Right-click the partition and select **New Simple Volume** to open the New Simple Volume Wizard.

![Right-click to open the context menu for the new volume](https://www.natebee.com/portfolio/writing/images/partition_new-simple-volume.png)

7. Follow the wizard with the settings you want for this new partition. This guide will stick to the defaults. Click **Next** to start.
8. Enter the **Simple volume size in MB**. By default, the wizard matches the maximum disk space.
9. Leave **Assign the following drive letter** selected and choose an available drive letter from the dropdown.
10. Leave **Format this volume with the following settings** selected.
11. Choose the File system and Allocation unit size from the dropdowns.
12. Enter a Volume label for the partition.
13. Click **Next**, then click **Finish**. The new partition opens in a new File Explorer window when it's ready.

![The new test-volume is ready to use](https://www.natebee.com/portfolio/writing/images/partition_final-state.png)
