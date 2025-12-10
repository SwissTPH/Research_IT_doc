# SciCORE HPC — Quick Start Guide

SciCORE provides **high-performance computing (HPC)** resources for large-scale data processing. Researchers can remotely access these resources from their own laptop or desktop. HPC is perfect for tasks that require large amounts of RAM or take several hours/days to complete, since jobs run remotely while your own machine can be logged out or switched off. 

This is a quick start guide for SciCORE HPC. More details can be found [here](https://docs.scicore.unibas.ch/HPC%20Cluster/getstarted/).

## Login (Bash Users)

Use your **UniBas alias** to connect from any terminal (Unix, macOS, or Windows with PowerShell/WSL) to the SciCORE login node over VPN:

```bash
ssh <username>@login12.scicore.unibas.ch # login11 also works
```

Alternatively, use SSH clients such as `Termius` or `MobaXterm` with the following settings:

- Remote host: `login12.scicore.unibas.ch` or `login11.scicore.unibas.ch`
- Username: your UniBasel alias.

Please write to the [SciCORE help centre](https://support.scicore.unibas.ch/servicedesk/customer/portal/1/create/17) if you do not have access.

## Command-Line Quick Start

Running jobs on HPC compute nodes requires **two files**:

- 1️⃣ A **job script** (e.g. `job.sh`). 
- 2️⃣ Your actual **script** in python/R/etc. (e.g. `test.py`)

Example job script `job.sh` (include job name, runtime, QoS (*Quality of Service*), memory, output/error files, modules to load, and commands to execute.):

```bash
#!/bin/bash
#SBATCH --job-name=myrun        # Job name
#SBATCH --cpus-per-task=1       # Number of cores
#SBATCH --mem-per-cpu=1G        # RAM per core
#SBATCH --time=01:00:00         # Maximum runtime
#SBATCH --qos=6hours            # Quality of Service
#SBATCH --output=./myrun.o%j    # Output file
#SBATCH --error=./myrun.e%j     # Error file

# load python
ml Python/3.13.5-GCCcore-14.3.0

# Run your script
python ./test.py

```

Example Python script `test.py`:

```python
import os

# print cwd
current_dir = os.getcwd()
print("Current directory is", current_dir)

# list files
print("\nFiles in this directory:")
for item in os.listdir(current_dir):
    print("-", item)
```

### ✅ Submit the job

```bash
sbatch job.sh
```

### 📃Check job status

```bash
squeue -u <username>
```

### ❌ Cancel jobs

```bash
# Cancel job by job_id or username
scancel <job_id>/<username>
```

### 📲 Transfer files from local laptop to HPC

```bash
# Copy a single file to SciCORE
scp /path/to/your/file <username>@login12.scicore.unibas.ch:/path/to/destination/

# Copy a folder to SciCORE
scp -r /path/to/your/folder <username>@login12.scicore.unibas.ch:/path/to/destination/
```



## Software & modules

SciCORE provides a wide range of pre-built-in modules, so you usually don’t need to install software manually.

List available modules:

```bash
module avail # To see the full module list
```
Full module list can also be found [here](https://scicore.unibas.ch/using-scicore/software/).

Load modules in your job script with:

```bash
ml <module_name>
```

If a package isn’t available as a module, you can alternatively use **Miniconda3** to create and activate your own environment, or contact the SciCORE team at scicore-admin@unibas.ch. To use Miniconda3:

```bash
ml Miniconda3/24.7.1-0

# then create your conda env, e.g. using an existing yml file:
conda env create -f environment.yml 
```

In your `job.sh`, initialize and activate conda env before running your script:

```bash
#!/bin/bash
#SBATCH --job-name=myrun        # Job name
#SBATCH --cpus-per-task=1       # Number of cores
#SBATCH --mem-per-cpu=1G        # RAM per core
#SBATCH --time=01:00:00         # Maximum runtime (1h)
#SBATCH --qos=6hours            # Queue (maximum 6h runtime)
#SBATCH --output=./myrun.o%j    # Path/name for output file
#SBATCH --error=./myrun.e%j     # Path/name for error file

source /scicore/soft/easybuild/apps/Miniconda3/24.7.1-0/etc/profile.d/conda.sh # <- Initialize 

conda activate your_env_name	# <- Activate 

python ./test.py                # Run your script
```



## Login Node vs Computing Nodes (Important!)
When you first connect to SciCORE, you land on a **login node** (`login11` or `login12`). These nodes are shared by all users and are meant **only for basic tasks** (instead of computation), such as:

- navigating folders
- editing files
- submitting jobs
- checking job status

**⚠️ Do not run CPU- or memory-intensive analyses on the login node.** Heavy computations may slow down or disrupt other users and can trigger automatic process termination.

All real analyses must run on **computing nodes**, which are allocated through SLURM when you submit a job using:

```bash
sbatch job.sh
```

SLURM then assigns your job to a suitable compute node based on your requested resources (cores, RAM, time, QoS).

In the job file, we requested a compute node using these lines:

```bash
#SBATCH --cpus-per-task=1       # Number of cores
#SBATCH --mem-per-cpu=1G        # RAM per core
#SBATCH --time=01:00:00         # Maximum runtime (1h)
#SBATCH --qos=6hours            # Queue (maximum 6h runtime)
```

After SLURM grants a node, you job will be placed *inside* that compute node. Only here is it safe to run commands that use significant CPU/RAM. Full selection of SLURM node can be found [here](https://docs.scicore.unibas.ch/HPC%20Cluster/batchcomputing/#queues-and-partitions).



## Desktop Quick Start (Web-based Interface)

SciCORE also offers a [web-based interface](https://ood-ubuntu.scicore.unibas.ch/) that lets you interact with the HPC system from your browser (no local SSH configuration needed). Simply log in, launch your environment, and manage your work just like you would on your local machine - but powered by HPC resources. 



## Data Transfer

SciCORE and SciCORE+ offer several secure methods for transferring data.

If your project involves **personal**, **sensitive**, or **clinical** data, you must ensure all necessary **legal agreements** and **ethical approvals** are in place *before* any transfer. Details can be found [here](https://docs.scicore.unibas.ch/sciCORE%2B/datamanagement/).

If you are unsure which method to choose:

- **For general HPC use (non-sensitive data):**
   ➡️ `scp` or `sftp` on the standard SciCORE cluster.
- **For sensitive/clinical data under sciCORE+:**
   ➡️ **SFTP** (simple, secure) or **SETT** (encrypted + traceable transfers)
