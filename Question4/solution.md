<details>
<summary>
    <h3 style="display: inline;"> Action 1: Observe File Descriptors and Open Files</h3>
</summary> <br>

**Command:**  
```bash
ls -l /proc/$$/fd
```

**Expected Output:**  
```text
total 0
lrwx------ 1 user user 64 Jul  3 14:33 0 -> /dev/pts/0
lrwx------ 1 user user 64 Jul  3 14:33 1 -> /dev/pts/0
lrwx------ 1 user user 64 Jul  3 14:33 2 -> /dev/pts/0
lrwx------ 1 user user 64 Jul  3 14:33 255 -> /dev/pts/0
```

**Explanation:**  
By examining the file descriptors (`fd`) for the current shell's Process ID (`$$`) inside the `/proc` virtual filesystem, I identified the three standard Linux I/O streams: `0` (Standard Input), `1` (Standard Output), and `2` (Standard Error), all currently pointing to the pseudo-terminal (`/dev/pts/0`).

**Screenshot:**  
![Step 1](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question4/Screenshots/step1.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 2: Perform Output and Error Redirection</h3>
</summary> <br>

**Command:**  
```bash
echo "Application logged successfully." > stdout.log
ls /fake_directory 2> stderr.log
cat stdout.log
cat stderr.log
```

**Expected Output:**  
```text
Application logged successfully.
ls: cannot access '/fake_directory': No such file or directory
```


**Explanation:**  
I demonstrated stream segregation by using `>` to redirect successful standard output (FD 1) into `stdout.log`, and `2>` to explicitly catch standard error (FD 2) from a failed command into `stderr.log`. Viewing the files confirms the data was successfully routed away from the terminal screen.

**Screenshot:**  
![Step 2](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question4/Screenshots/step2.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 3: Observe System Resource Limits</h3>
</summary> <br>

**Command:**  
```bash
ulimit -n
```

**Expected Output:**  
```text
1024
```

**Explanation:**  
The `ulimit -n` command displays the "open files" limit. I observed that a single process can open a maximum of 1024 file descriptors simultaneously. If an application is experiencing logging issues, hitting this limit (the "Too many open files" error) is a primary technical culprit.

**Screenshot:**  
![Step 3](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question4/Screenshots/step3.png?raw=true)

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 4: Generate the Investigation Report</h3>
</summary> <br>

**Command:**  
```bash
cat << 'EOF' > IO_Investigation_Report.txt
--- I/O INVESTIGATION REPORT ---

1. Open Files & File Descriptors:
Using /proc/$$/fd, the standard file descriptors were verified: 0 (stdin), 1 (stdout), and 2 (stderr). All were correctly linked to the active terminal. 

2. Output and Error Redirection:
Standard output (1>) and standard error (2>) were successfully segregated into stdout.log and stderr.log respectively. This proves that application logging can be cleanly split to isolate critical errors from routine info logs.

3. Resource Limits:
The open file limit per process (ulimit -n) is currently set to 1024. If the application opens more files/network sockets than this threshold, I/O operations will fail.

4. How Linux Manages File I/O:
Linux operates on the principle that "everything is a file." The kernel manages I/O operations by assigning an integer (File Descriptor) to every open file, socket, or pipe. The Virtual File System (VFS) provides a unified interface, allowing user-space applications to read and write to hardware and logs purely by manipulating these descriptor streams.
EOF
```

**Expected Output:**  
No output on screen; the report file is generated.

**Explanation:**  
This heredoc block compiles the raw technical data and pairs it with a conceptual explanation of Linux file I/O and descriptor management into the final `IO_Investigation_Report.txt` required for the assignment submission.

**Screenshot:**  
![Step 4](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question4/Screenshots/step4.png?raw=true)

</details>