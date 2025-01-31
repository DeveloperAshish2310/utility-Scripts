To format a disk using Diskpart, follow these steps carefully:

### **Warning:** This will erase all data on the selected disk. Make sure to back up anything important before proceeding.

1. **Open Command Prompt as Administrator:**
   - Press `Windows + X` and select **Command Prompt (Admin)** or **Windows PowerShell (Admin)**.
   
2. **Open Diskpart:**
   - Type `diskpart` and press **Enter** to launch the Diskpart utility.

3. **List available disks:**
   - Type `list disk` and press **Enter**. This will show all connected disks. Identify the number of the disk you want to format.

4. **Select the disk to format:**
   - Type `select disk X` (replace X with the disk number you want to format) and press **Enter**. For example, if you're formatting disk 1, you would type:
     
     select disk 1
     

5. **Clean the disk (optional but recommended):**
   - If you want to wipe all partitions and data from the disk, type `clean` and press **Enter**. This will remove all partitions on the disk, effectively wiping it.

6. **Create a new partition:**
   - To create a new partition on the disk, type:
     
     create partition primary
     
     Press **Enter**.

7. **Select the newly created partition:**
   - Type `select partition 1` (assuming it’s the first partition) and press **Enter**.

8. **Format the partition:**
   - To format the partition, use the following command (you can choose between different file systems like `NTFS`, `FAT32`, etc.):
     
     format fs=ntfs quick
     
     For a quicker format, add the `quick` option. If you want a full format, leave out `quick`.

9. **Assign a drive letter (optional):**
   - To assign a letter to the formatted partition, type:
     
     assign letter=X
     
     Replace `X` with the letter you want to assign (for example, `assign letter=E`).

10. **Exit Diskpart:**
    - Type `exit` and press **Enter** to leave Diskpart.

### Done!
You should now have a formatted disk with a new partition and assigned letter ready to use. Let me know if you need more help with any of the steps!
