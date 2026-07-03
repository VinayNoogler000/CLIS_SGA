<details>
<summary>
<h3 style="display: inline;">Action 1: Username and groups</h3>
</summary> <br>

**Command:**
```bash
id
```

**Expected Output:**
```text
uid=1000(vinaytambey000) gid=1000(vinaytambey000) groups=1000(vinaytambey000),4(adm),27(sudo),996(docker)
```

**Explanation:**  
This command retrieves the user's UID, primary group GID, and supplementary groups. I observed my specific user identity, which verifies my system access permissions.

**Screenshot:**  
![Step 1](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step1.png?raw=true)

</details>




<br/> <br/>
<details>
<summary><h3 style="display: inline;">Action 2: Current shell </h3></summary> <br>

**Command:**
```bash
echo $SHELL
```

**Expected Output:**
```text
/bin/bash
```

**Explanation:**  
This command prints the value of the SHELL environment variable. It confirmed that my terminal session is actively operating within the Bash shell environment.

**Screenshot:**  
![Step 2](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step2.png?raw=true)

</details>




<br/> <br/>
<details>
<summary><h3 style="display: inline;">Action 3: Current working directory </h3></summary> <br>

**Command:**
```bash
pwd
```

**Expected Output:**
```text
/home/vinaytambey000/CLIS_SGA/Question1
```

**Explanation:**  
This command outputs the absolute path of the current directory. This verified that I am correctly positioned inside the designated `Question1` folder for this task.

**Screenshot:**  
![Step 3](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step3.png?raw=true)

</details>




<br/> <br/>
<details>
<summary><h3 style="display: inline;">Action 4: List of files and directories </h3></summary> <br>

**Command:**
```bash
ls -la
```

**Expected Output:**
```text
total 16
drwxrwxr-x 3 vinaytambey000 vinaytambey000 4096 Jul  3 06:45 .
drwxrwxr-x 8 vinaytambey000 vinaytambey000 4096 Jul  3 07:08 ..
drwxrwxr-x 2 vinaytambey000 vinaytambey000 4096 Jul  3 07:47 Screenshots
-rw-rw-r-- 1 vinaytambey000 vinaytambey000 1829 Jul  3 07:48 solution.md
```

**Explanation:**  
The ls -la command lists all files and directories, including hidden items (starting with '.' dot), in a long format detailing permissions and ownership. It allowed me to view the complete contents and security structure of my current workspace.

**Screenshot:**  
![Step 4](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step4.png?raw=true)

</details>




<br/><br/>
<details>
<summary><h3 style="display: inline;">Action 5: Network connectivity verification result </h3></summary> <br>

**Command:**
```bash
ping -c 4 8.8.8.8
```

**Expected Output:**
```text
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=0.856 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=0.409 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=0.401 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=114 time=0.364 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3039ms
rtt min/avg/max/mdev = 0.364/0.507/0.856/0.201 ms
```

**Explanation:**  
This command sends exactly 4 ICMP echo request packets to Google's Public DNS server to test network reachability. The transmission statistics showing 0% packet loss verified that the Linux environment has active outbound internet connectivity.

**Screenshot:**  
![Step 5 - ](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step5.png?raw=true)

</details>




<br/><br/>
<details>
<summary>
<h3 style="display: inline;"> Action 6: Generating Environment_Report.txt file </h3>
</summary> <br>

**Command:**  
```bash
{ echo "--- USER INFO ---"; id; echo -e "\n--- SHELL ---"; echo $SHELL; echo -e "\n--- DIRECTORY ---"; pwd; echo -e "\n--- WORKSPACE FILES ---"; ls -la; echo -e "\n--- NETWORK TEST ---"; ping -c 4 8.8.8.8; } > Environment_Report.txt
```

**Expected Output:**  
No output on screen; file is created silently.

**Explanation:**  
This command block groups all the previous verification commands, adds formatting headers using echo, and redirects (>) the entire standard output into a new file named `Environment_Report.txt`. This successfully compiled the required environment data into the final submission document.

**Screenshot:**  
![Step 6](https://github.com/VinayNoogler000/CLIS_SGA/blob/main/Question1/Screenshots/step6.png?raw=true)

</details>