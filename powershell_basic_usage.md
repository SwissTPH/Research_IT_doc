# Using PowerShell with Basic Linux Knowledge

This short guide helps users familiar with Linux quickly adapt to PowerShell. While the syntax differs slightly, the underlying logic of navigating directories, managing files, and running scripts remains the same. For a full command comparison, see Microsoft’s [table of basic powershell commands](https://devblogs.microsoft.com/scripting/table-of-basic-powershell-commands/).

---

###  ## Navigation & File Operations

PowerShell and Linux both use a hierarchical filesystem. The key difference is path separators (`\` in PowerShell vs `/` in Linux) and drive letters (e.g. `C:\`, `D:\`).

| **Task**               | **Linux Command**    | **PowerShell Command**               |
| ---------------------- | -------------------- | ------------------------------------ |
| Show current directory | `pwd`                | `pwd`                                |
| List files             | `ls`                 | `dir` or `ls`                        |
| Change directory       | `cd /path/to/folder` | `cd C:\path\to\folder`               |
| Move up one directory  | `cd ..`              | `cd ..`                              |
| Copy                   | `cp file file_copy`  | `cp .\file .\file_copy`              |
| Move                   | `mv file folder/`    | `Move-Item .\file .\folder\`         |
| Remove                 | `rm file`            | `rm .\file`                          |
| Create a folder        | `mkdir folder`       | `mkdir folder`                       |
| View a file            | `cat file`           | `Get-Content .\file` or `cat .\file` |
| Show first 10 lines    | `head -10 file`      | `Get-Content file -TotalCount 10`    |
| Show last 10 lines     | `tail -10 file`      | `Get-Content file -Tail 10`          |
| Search content in file | `grep text file`     | `Select-String "text" file`          |



## Environment and Conda Usage

Conda commands are mostly identical.

```powershell
# Initialise
conda init powershell

# List all packages
conda list

# List all environments
conda env list

# Activate an environment
conda activate my_env

# Deactivate environment
conda deactivate
```



## Running a Python Script

Running Python scripts works the same way as in Linux.

```powershell
# Run a Python script
python script_name.py

# Run interactively
python
```
