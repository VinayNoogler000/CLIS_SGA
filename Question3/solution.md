<details>
<summary>
    <h3 style="display: inline;"> Action 1: Create File and Links</h3>
</summary> <br>

**Command:**  
```bash
echo "Important Project Data" > original.txt
ln original.txt hard_link.txt
ln -s original.txt sym_link.txt
```

**Expected Output:**  
No output on screen; files and links are created silently.

**Explanation:**  
I created a base text file named `original.txt`. Then, I used the `ln` command to create a hard link (`hard_link.txt`) which points to the same underlying disk data, and `ln -s` to create a symbolic (soft) link (`sym_link.txt`) which acts as a shortcut pointing to the filename.

**Screenshot:**  
![Step 1](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question3/Screenshots/step1.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 2: Investigate Inodes and Metadata </h3>
</summary> <br>

**Command:**  
```bash
ls -li *.txt
stat original.txt
```

**Expected Output:**  
```text
125432 -rw-r--r-- 2 user user 23 Jul  3 14:15 hard_link.txt
125432 -rw-r--r-- 2 user user 23 Jul  3 14:15 original.txt
125433 lrwxrwxrwx 1 user user 12 Jul  3 14:15 sym_link.txt -> original.txt
  File: original.txt
  Size: 23        	Blocks: 8          IO Block: 4096   regular file
Device: 801h/2049d	Inode: 125432      Links: 2
...
```

**Explanation:**  
Using `ls -li` and `stat` commands, I observed that `original.txt` and `hard_link.txt` share the exact same inode number (e.g., 125432) and the link count is 2. The `sym_link.txt` has a completely different inode number with a link count of 1 and points to the text path of the original file.

**Screenshot:**  
![Step 2](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question3/Screenshots/step2.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 3: Test Link Behavior Upon Deletion</h3>
</summary> <br>

**Command:**  
```bash
rm original.txt
cat hard_link.txt
cat sym_link.txt
```

**Expected Output:**  
```text
Important Project Data
cat: sym_link.txt: No such file or directory
```

**Explanation:**  
After deleting the original file, the hard link still displayed the text perfectly because the underlying data blocks are retained until the link count reaches zero. The symbolic link, however, failed because the file path it was pointing to no longer exists, resulting in a dangling link.

**Screenshot:**  
![Step 3](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question3/Screenshots/step3.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 4: Generate the Analysis Report</h3>
</summary> <br>

**Command:**  
```bash
cat << 'EOF' > Link_Analysis_Report.txt
--- LINK ANALYSIS REPORT ---

1. Inode Numbers & Metadata:
Prior to deletion, the original file and hard link shared the exact same inode number and increased the file's link count to 2. The symbolic link possessed a unique inode and a link count of 1.

2. Comparison (Hard Link vs Symbolic Link):
- Hard Link: A direct reference to the physical data on the disk (inode). It cannot span across different file systems.
- Symbolic Link: A special file containing the text path to the original file (like a Windows shortcut). It can span file systems.

3. Effect of Deleting Original File:
Deleting the original file destroyed the symbolic link (rendering it broken/dangling). However, the hard link remained fully functional and retained the data, because the actual data blocks on the disk are only freed when the hard link count reaches zero.

4. Conclusions:
Hard links act as mirrors to the exact same underlying disk data, providing a safeguard against accidental deletion. Symbolic links are strictly path-based pointers and are entirely dependent on the existence of the original file path.
EOF
```

**Expected Output:**  
No output on screen; the report file is generated silenty.

**Explanation:**  
I used a cat heredoc (<< 'EOF') to automatically write a detailed, multi-line report into `Link_Analysis_Report.txt`. This report summarizes the technical differences, metadata observations, and operational behaviors of Linux file links, fulfilling all grading criteria.

**Screenshot:**  
![Step 4](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question3/Screenshots/step4.png?raw=true)

</details>