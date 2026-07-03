<details>
<summary>
    <h3 style="display: inline;"> Action 1: Create the Project Workspace and Files </h3>
</summary> <br>

**Command:**  
```bash
umask 0022
mkdir -p secure_workspace/{docs,code}
touch secure_workspace/docs/project_plan.txt
```

**Expected Output:**  
No output on screen; directories and files are created silently.

**Explanation:**  
I first explicitly set the `umask` to `0022` (the standard default) so I can observe default permissions. Then, I used `mkdir -p` to create a parent directory named `secure_workspace` with two subdirectories (docs and code), and created a dummy text file inside to represent project data.

**Screenshot:**  
![Step 1]()

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 2: View Permissions Before Modification and Ownership </h3>
</summary> <br>

**Command:**  
```bash
ls -ld secure_workspace secure_workspace/docs/project_plan.txt
```

**Expected Output:**
```text
drwxr-xr-x 4 user user 4096 Jul  3 13:40 secure_workspace
-rw-r--r-- 1 user user    0 Jul  3 13:40 secure_workspace/docs/project_plan.txt
```

**Explanation:**  
Using `ls -ld`, I inspected the initial permissions and ownership. The directory has 755 (rwxr-xr-x) permissions, and the file has 644 (rw-r--r--). This means "others" (anyone outside my user/group) currently have read access to my project files, which is a security risk for a private workspace.

**Screenshot:**  
![Step 2]()

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 3: Modify Permissions for Security </h3>
</summary> <br>

**Command:**  
```bash
chmod -R 750 secure_workspace
```

**Expected Output:**
No output on screen; permissions are modified silently.

**Explanation:**  
I used the `chmod` command with the `-R` (recursive) flag to change the permissions of the directory and all its contents to 750. This sets the owner permissions to read/write/execute (7), the group to read/execute (5), and completely removes all access (0) for "others".

**Screenshot:**  
![Step 3]()

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 4: View Permissions After Modification </h3>
</summary> <br>

**Command:**  
```bash
ls -ld secure_workspace secure_workspace/docs/project_plan.txt
```

**Expected Output:**
```text
drwxr-x--- 4 user user 4096 Jul  3 13:40 secure_workspace
-rwxr-x--- 1 user user    0 Jul  3 13:40 secure_workspace/docs/project_plan.txt
```

**Explanation:**  
Re-running the list command verifies the changes. The permissions now show --- for the "others" category at the end of the permission string. The project data is now isolated from unauthorized users on the system.

**Screenshot:**  
![Step 4]()

</details>




<br> <br>
<details>
<summary>
    <h3 style="display: inline;"> Action 5: Generate the Expected Submission Report</h3>
</summary> <br>

**Command:**  
```bash
{
echo "--- PROJECT WORKSPACE SECURITY REPORT ---"
echo -e "\n1. Umask Value Used: 0022 (Default prior to manual chmod adjustment)"
echo -e "\n2. Directory Structure:"
ls -R secure_workspace
echo -e "\n3. Ownership and Final Permissions:"
ls -ld secure_workspace secure_workspace/docs/project_plan.txt
echo -e "\n4. Security Explanation:"
echo "By setting the permissions to 750 (rwxr-x---), we ensure that the owner has full control, group members can read and traverse the directories, and 'others' have absolutely zero access. This strict exclusion of 'others' protects sensitive project documentation and source code from being viewed, executed, or modified by unauthorized system users."
} > Project_Workspace_Report.txt
```

**Expected Output:**  
No output on screen; the report file is generated.

**Explanation:**  
This command block generates the required `Project_Workspace_Report.txt`. It dynamically pulls the directory tree, the final ownership/permission data, and appends a written explanation of how the Linux permission model protects the team's data, fulfilling all rubric requirements.

**Screenshot:**  
![Step ]()

</details>