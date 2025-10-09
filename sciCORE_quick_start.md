# SciCORE HPC — Quick Start Guide

SciCORE provides **high-performance computing (HPC)** resources for large-scale data processing. Researchers can remotely access these resources from their own laptop or desktop. HPC is perfect for tasks that require large amounts of RAM or take several hours/days to complete, since jobs run remotely while your own machine can be logged out or switched off. 

This is a quick start guide for SciCORE HPC. More details can be found [here](https://docs.scicore.unibas.ch/HPC%20Cluster/getstarted/).



---

## Login

Use your **UniBasel alias** to log in from the terminal:

```bash
ssh <username>@login12.scicore.unibas.ch # login11 also works
```

Alternatively, use SSH clients such as `Termius` or `MobaXterm` with the following settings:

- Remote host: `login12.scicore.unibas.ch` or `login11.scicore.unibas.ch`
- Username: your UniBasel alias.

Please write to the [SciCORE help centre](https://support.scicore.unibas.ch/servicedesk/customer/portal/1/create/17) if you do not have access.



---

## Command-Line Quick Start (Bash Users)

Running jobs on HPC requires two files:

- a **job script** (e.g. `test.sh`) with job name, run time, output file, modules, and commands
- your own **script** in python/R/etc. (e.g. `test.py`)

Example job script `test.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=myrun        # Job name
#SBATCH --cpus-per-task=1       # Number of cores
#SBATCH --mem-per-cpu=1G        # RAM per core
#SBATCH --time=01:00:00         # Maximum runtime (1h)
#SBATCH --qos=6hours            # Queue (maximum 6h runtime)
#SBATCH --output=./myrun.o%j    # Path/name for output file
#SBATCH --error=./myrun.e%j     # Path/name for error file

ml Biopython                    # Load module

python ./test.py                # Run your script

```

Example Python script `test.py`:

```python
import Bio

try:
    import Bio
    print("Biopython available,", getattr(Bio, "__version__", "version unknown"))
except ImportError:
    print("Biopython not available")
```

### Submit the job

```bash
sbatch test.sh
```

### Check job status

```bash
squeue -u <username>
```

### Cancel jobs

```bash
# Cancel job by job_id or username
scancel <job_id>/<username>
```

### Transfer files from local laptop to HPC

```bash
# Copy a single file to SciCORE
scp /path/to/your/file <username>@login12.scicore.unibas.ch:/path/to/destination/

# Copy a folder to SciCORE
scp -r /path/to/your/folder <username>@login12.scicore.unibas.ch:/path/to/destination/

# Copy a file directly to your home directory on SciCORE
scp /path/to/your/file <username>@login12.scicore.unibas.ch:~/
```

---

## Desktop Quick Start (Web-based Interface)

SciCORE also offers a [web-based interface](https://ood-ubuntu.scicore.unibas.ch/) that lets you interact with the HPC system from your browser (no local SSH configuration needed). Simply log in, launch your environment, and manage your work just like you would on your local machine - but powered by HPC resources. 



---

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

In your `job.sh`, add this before running your script:

```bash
source /scicore/soft/easybuild/apps/Miniconda3/24.7.1-0/etc/profile.d/conda.sh # initialise conda env
conda activate your_env_name
```



---

## Price List and node selection

Price list can be found [here](https://scicore.unibas.ch/using-scicore/user-fees/), and QoS (Quality of Service) list is available [here](https://docs.scicore.unibas.ch/HPC%20Cluster/batchcomputing/#queues-and-partitions).
