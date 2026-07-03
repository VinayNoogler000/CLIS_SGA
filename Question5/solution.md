<details>
<summary>
    <h3 style="display: inline;"> Action 1: Collect Storage Information</h3>
</summary> <br>

**Command:**  
```bash
lsblk
df -h
df -i
```

**Expected Output:**  
```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   50G  0 disk 
└─sda1   8:1    0   50G  0 part /

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   10G   38G  22% /
tmpfs           2.0G     0  2.0G   0% /dev/shm

Filesystem      Inodes IUsed   IFree IUse% Mounted on
/dev/sda1        3.2M  150K    3.0M    5% /
tmpfs           512K      1    512K    1% /dev/shm
```

**Explanation:**  
I used `lsblk` to identify the physical block devices attached to the system. I then used `df -h` to analyze the mounted file systems and their human-readable capacity, and `df -i` to check the inode utilization (the limit on the number of files that can be created).

**Screenshot:**  
![Step 1](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question5/Screenshots/step1.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 2: Document Findings using `vi` Editor</h3>
</summary> <br>

**Command:**  
```bash
vi Storage_Assessment_Report.txt
```
*(Once inside vi, press i to enter Insert Mode, type/paste the report below, press Esc to return to Command Mode, and type :wq followed by Enter to save and quit).*

Input text into `vi`:
```text
--- STORAGE ASSESSMENT REPORT ---

1. Available Storage Devices:
The system currently utilizes a single 50GB primary disk (/dev/sda). 

2. Mounted File Systems & Disk Usage:
The primary root filesystem (/) is mounted on /dev/sda1. It has a total size of 50G, with 10G used and 38G available (22% utilization). A temporary filesystem (tmpfs) is mounted on /dev/shm.

3. Inode Utilization:
The root partition has 3.2 million total inodes. Only 150K are used (5% utilization), leaving 3.0 million available. 

4. Storage Health Observations:
The storage system is currently highly healthy. Both physical capacity (78% free) and inode capacity (95% free) have abundant headroom for the new application server deployment.

5. Recommendations:
While current capacity is sufficient, I recommend implementing logical volume management (LVM) for future deployments to allow for dynamic volume resizing. Additionally, setting up a cron job to monitor and alert if /dev/sda1 exceeds 80% usage will prevent future application downtime.
```

**Expected Output:**  
The terminal screen will switch to the visual vi editor interface, and then return to the standard prompt upon saving.


**Explanation:**  
The `vi` editor is a modal text editor native to Linux. By switching between command mode and insert mode, I was able to manually draft, edit, and safely save the storage assessment report directly from the command line.

**Screenshot:**  
![Step 2](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question5/Screenshots/step2.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 3: Verify the Saved Report</h3>
</summary> <br>

**Command:**  
```bash
cat Storage_Assessment_Report.txt
```

**Expected Output:**  
Displays the exact text entered in Action 2.

**Explanation:**  
I used the `cat` command to output the contents of the newly created file to the terminal, confirming that `vi` successfully wrote the data to the disk and the report is ready for submission.

**Screenshot:**  
![Step 3](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question5/Screenshots/step3.png?raw=true)

</details>