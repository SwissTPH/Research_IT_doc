# Getting started with `conda`



## What is `conda` and why would I use it?

`conda` is a command-line tool for managing **software packages** and **environments**. It runs on Windows, macOS and Linux.

One of the main advantages of `conda` is that you can create a separate environment for each project or analysis.

For example, one project might require:

- Python 3.11
- NumPy 2.0
- SciPy 1.14
- a particular version of another scientific tool

Another project may require completely different versions.

Instead of installing everything into the same system, `conda` keeps these environments separate. This helps avoid software conflicts and makes your analyses easier to reproduce later.

You can also think of `conda` as a **software and package manager**. Instead of searching online for an installer for every tool, you can often find the package on [anaconda.org](https://anaconda.org/) and install it directly from the command line.

For example:

```
conda install scipy
```

`conda` will also try to install the dependencies that the package requires.



## Variations of `conda` installer

There are three common ways to install `conda`:

### 1. Anaconda

Anaconda is a full distribution that includes `conda`, Python and many commonly used packages and tools for data science.

It is convenient for **beginners** because many packages are already installed, but it requires considerably more disk space.

### 2. Miniconda

Miniconda is a minimal installer containing `conda`, Python and only a small number of essential packages.

**Packages such as `pandas`, `NumPy` or `Jupyter` are not installed by default.** You install only the packages that you actually need. This keeps the installation smaller and gives you more control over your environments.

### 3. Miniforge

Miniforge is a minimal installer maintained by the conda-forge community.

It comes preconfigured to use the `conda-forge` channel and also includes `mamba`, an alternative package manager that uses the same package ecosystem.



General installation instructions are available on the [official conda installation page](https://docs.conda.io/projects/conda/en/latest/user-guide/install/).



## Using `conda` on Swiss TPH laptops

### Windows / PowerShell

Install **Anaconda** or **Miniconda** from Company Portal.

You can then use `conda` from PowerShell or the terminal provided with your installation.

### Linux / WSL

If you need to work in Linux:

1. Apply for WSL access through the IT Service Portal if you do not already have access.
2. Install a **Linux version of** `conda` **inside WSL**.
3. Run your Linux `conda` environments and software from inside WSL.



Do not mix your Windows `conda` installation with your WSL/Linux installation. They are separate operating environments and should have separate `conda` installations.



> **Bioinformatics users:** Many packages from the `bioconda` channel are available only for Linux and macOS, not native Windows. If a Bioconda package is not available on Windows, use `conda` inside WSL instead.



## Understanding channels

A **channel** is a repository from which `conda` downloads packages.

Some commonly used channels are:

- `defaults`: the default Anaconda package repositories
- `conda-forge`: a large community-maintained collection of packages
- `bioconda`: bioinformatics software, commonly used together with `conda-forge`

For example, to install a package specifically from `conda-forge`:

```
conda install -c conda-forge scipy
```

Or from Bioconda:

```
conda install -c bioconda blast
```

Not every package is available for every operating system, so always check the supported platforms when looking at a package.



# A basic `conda` workflow



## 1️⃣ Create an environment

Create a new environment and give it a meaningful name:

```
conda create --name my_env
```

A better practice is to specify the Python version when creating a Python environment:

```
conda create --name my_env python=3.12
```

For example:

```
conda create --name malaria_analysis python=3.12
```

Using a meaningful name makes it much easier to remember what the environment is used for.



## 2️⃣ Activate the environment

```
conda activate my_env
```

Your command line will normally show the active environment:

```
(my_env) C:\Users\username>
```

Anything you install with `conda` will now be installed into this environment.



## 3️⃣ Install packages

For example:

```
conda install scipy
```

You can install several packages at once:

```
conda install numpy pandas scipy
```

You can also specify a version:

```
conda install scipy=1.14
```



## 4️⃣ Check your environments

To see all `conda` environments on your computer:

```
conda env list
```

The currently active environment is marked with `*`.



## 5️⃣ Check installed packages

To see all packages installed in the current environment:

```
conda list
```

To check whether a particular package is installed:

```
conda list scipy
```



## 6️⃣ Leave the environment

When you have finished working in an environment:

```
conda deactivate
```



# Export environments

One major advantage of `conda` is that you can save the configuration of an environment.

For example:

```
conda env export > environment.yml
```

This creates an `environment.yml` file containing information about the packages installed in the environment.

Someone else (or you at a later date) can use this file to recreate the environment:

```
conda env create -f environment.yml
```

Keeping an environment file together with your analysis or project helps make your work more reproducible.
