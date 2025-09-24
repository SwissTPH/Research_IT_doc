# sciCore HPC — Quick Start Guide

sciCORE provides **high-performance computing (HPC)** resources for large-scale data processing. Researchers can remotely access these resources from their own laptop or desktop. HPC is perfect for tasks that require large amounts of RAM or take several hours/days to complete, since jobs run remotely while your own machine can be logged out or switched off. 

More details can be found [here](https://docs.scicore.unibas.ch/HPC%20Cluster/getstarted/).



## Login

Use your **UniBasel alias** to log in from the terminal:

```bash
ssh <username>@login12.scicore.unibas.ch # login12/login11 would both work
```

Alternatively, use SSH clients such as `Termius` or `MobaXterm` with the following settings:

- Remote host: `login12.scicore.unibas.ch` or `login11.scicore.unibas.ch`
- Username: your UniBasel alias.



## Minimal workflow 

Running jobs on HPC requires two files:

- a **job script** (e.g. `test.sh`) with job name, run time, output file, modules, and commands
- your own **script** in python/R/etc. (e.g. `test.py`)

Example job script `test.sh`:

```bash
#!/bin/bash

#SBATCH --job-name=myrun     # Job name = `myrun`
#SBATCH --cpus-per-task=1    # Number of cores = 1
#SBATCH --mem-per-cpu=1G     # RAM reserved = 1G
#SBATCH --time=01:00:00      # Maximum run time = 1h
#SBATCH --qos=6hours         # Queue to allocate your job = 6hours queue (maximum runtime = 6h)
#SBATCH --output=./myrun.o%j   # Path and name to the output file
#SBATCH --error=./myrun.e%j    # Path and name to the error message

ml Biopython # Load biopython module

python ./test.py # run your script
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
# cancel job by job_id or username
scancel <job_id>/<username>
```



## Software & modules

sciCORE provides a wide range of pre-built-in modules, so you usually don’t need to install software manually.

List available modules:

```bash
module avail # to see the full module list
```
Full module list can also be found [here](https://scicore.unibas.ch/using-scicore/software/).

If a package isn’t available as a module, you can alternatively use **Miniconda3** to create and activate your own environment, or contact the sciCORE team at scicore-admin@unibas.ch.

Load modules in your job script with:

```bash
ml <module_name>
```

