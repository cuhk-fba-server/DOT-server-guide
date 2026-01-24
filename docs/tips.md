## Tips for Users

### File Storage and Transfer

Each user has a dedicated home directory located at `/mnt/disk5/home/username`. We've unified the storage system so you'll automatically access the same home directory whether connecting through SSH or JupyterHub on any node in our HPC cluster. This eliminates previous confusion with separate folders for different access methods.

> ⚠️ ** NOTE**
>
> **Storage Limit:** While we will start to conduct weekly backups of your files for data protection, each user has a 2TB storage limit. This ensures optimal performance for all users sharing the cluster resources.

#### Using JupyterHub (Beginner-Friendly)

When using JupyterHub's web interface, file transfer is straightforward:

- To upload: Simply drag and drop files from your computer into the JupyterHub file browser
- To download: Right-click on any file and select 'Download'
- Batch download: Click the right panel and find the extension manager, install the extension [`jupyter-archive`](https://github.com/jupyterlab-contrib/jupyter-archive). After restarting your Jupyter server (save your work first!) you'll find a new option called "Download as an archive" when you right-click a folder or multiple selected files.

#### Using SSH Commands (Command Line)

You can upload your files to the shared storage. First you should login to the login node. 

For larger files or batch transfers, SSH commands provide efficient file transfer:

```bash
# Upload a file from your computer to the login node
scp /path/to/local/file username@137.189.75.119:/path/on/server

# Upload an entire folder
scp -r /path/to/local/folder username@137.189.75.119:/path/on/server

# Download a file from server to your computer
scp username@137.189.75.119:/path/on/server/file /path/on/your/computer

# Examples:
scp data.csv xinyuli@137.189.75.119:/mnt/disk5/home/xinyuli/datafolder
scp -r codes/ xinyuli@137.189.75.119:/mnt/disk5/home/xinyuli/project/
```

> [!NOTE]
> Replace 'username' and 'server' with your actual login credentials and server address.

#### Alternative Methods

- **WinSCP**: A user-friendly graphical tool for Windows users that provides drag-and-drop file transfer
- **Downloading from Web**: To download files directly to the server, use the `wget` command:

```bash
wget https://example.com/dataset.zip
```

### Custom Conda Environment

Use `conda`, an environment and library management toolkit that allows you to have separate workspaces with different libraries equipped. Each user's environments are independent. Open your terminal and follow these steps to configure your own environments.

```bash
# Source your .bashrc to initialize conda if you don't see "(base)" in your prompt
# Please first launch JupyterHub once to initialize the conda environments.
# Without this step, you may encounter errors indicating that `.bashrc` file cannot be found.
# Add conda to your PATH if it is not available: export PATH="/mnt/disk5/software/miniconda3/bin:$PATH"`
. ~/.bashrc
conda activate

# The shell prompt will change from:
username@hostname:~$
# to:
(base) username@hostname:~$

# Create a new conda environment with Python and essential packages
# Important: Always include Python and pip when creating a new environment
conda create -n myenv python=3.13 pip

# Activate your new environment
conda activate myenv

# The shell prompt will change to:
(myenv) username@hostname:~$

# Before installing packages, verify you're using the correct pip
which pip
# Should show: /mnt/disk5/home/username/.conda/envs/myenv/bin/pip

# Install packages in your environment
pip install package-name

# Verify packages are installed in your conda environment (not in .local)
pip show package-name
# Should show path in your conda environment: /mnt/disk5/home/username/.conda/envs/myenv/...

# Add your environment as a Jupyter kernel (run this command in base env)
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

Some useful conda commands:

```shell
conda env list          # list all environments
conda list             # list all packages in current environment
conda remove -n <env-name> --all  # remove an environment
conda deactivate       # return to base environment
```

> [!NOTE] 
>
> - Two shared environments are available by default (read-only):
>
>   - `base`: Basic data analysis environment
>
>   - `pytorch`: Deep learning environment with PyTorch
>
> - If packages are installing to `.local` directory instead of your conda environment, check which pip you're using with `which pip`
> - Always ensure you've activated your environment before installing packages

### Running Time-consuming Scripts Efficiently through SLURM

SLURM (Simple Linux Utility for Resource Management) is a job scheduling system designed for HPC clusters. Its primary purpose is to efficiently allocate resources and prevent competition for computing power when multiple users run jobs simultaneously.

> [!NOTE] 
>
> Using SLURM is **recommended but optional** for users who want more stable and flexible resource assignment. It's particularly valuable for long-running tasks and jobs requiring specific GPU allocations.
>
> If your code requires GPU resources or will run for extended periods, we highly recommend using SLURM. It ensures your tasks run smoothly without resource conflicts and allows you to disconnect while your job continues running. 

|Partition Name |Nodes                |Resource in total                     |Description                |
| -------------- | -------------------- | --------------------------------- | ----------------------------------------- |
| **standard**   | gpu[114-115,137,142] | See specs below                   | Used for **JupyterHub**                   |
| **gtx4090***   | gpu[114-115]         | 64 CPU, 8 GPU, 503G RAM per node  | Default patition for submitting GPU tasks |
| **gtx3090**    | gpu[137,142]         | 112 CPU, 2 GPU, 250G RAM per node | Backup partition for submitting GPU tasks |

For detailed usage instructions, see the [Slurm official documentation](https://slurm.schedmd.com/documentation.html). Below we provide a quick start guide:

1. Create a job script (example: *my_job.sh*):

```bash
#!/bin/bash
#SBATCH --job-name=my_task       # Name for your job
#SBATCH --ntasks=1               # Number of tasks
#SBATCH --cpus-per-task=2        # CPUs per task
#SBATCH --gres=gpu:1             # Request 1 GPU per node
#SBATCH --nodes=2								 # Request 2 compute nodes
#SBATCH --time=2-00:00:00        # Request 2 days runtime (D-HH:MM:SS)
#SBATCH --output=%j_output.log   # Save output to a log file

# Your commands below
python /path/to/your/script.py
```

The `#SBATCH` lines specify resource requests and job parameters. For more options, see [this cheatsheet](https://slurm.schedmd.com/pdfs/summary.pdf).

> [!TIP]
> To request specific GPU resources, add:
>
> - `--gres=gpu:n` for n GPU per node
> - `--nodes=2` for 2 compute nodes
>
> The combination of the above two commands requests n*2=2n GPUs. For each user, we currently allow up to 12 GPUs.
>
> When requesting multiple GPUs with SLURM, your Python code must be configured to use them. For PyTorch users, you'll need to explicitly enable multi-GPU training (using `nn.DataParallel`, `nn.parallel.DistributedDataParallel`

2. Now submit your job:

```bash
  sbatch my_job.sh
```

Your code will run based on available resources, even if you disconnect from the cluster. The maximum job duration is 5 days.

> [!NOTE]
> When you connect via SSH, you'll be in the base conda environment by default. SLURM jobs will run in your currently activated conda environment, so make sure to activate the appropriate environment before submitting jobs if needed.

3. Monitor your job:

   ```bash
   squeue -u $USER       # List your running jobs
   scancel <job_id>      # Cancel a specific job
   ```

4. Alternative for shorter tasks: For quick tests or interactive sessions, you can use:

   ```bash
   srun --gres=gpu:1 --pty bash    # Get an interactive shell with 1 GPU from a single node
   ```

> [!NOTE]
> The `srun` command creates an interactive session that requires you to stay connected. If your SSH connection drops, your job will terminate immediately. For longer tasks or when you need to disconnect, always use `sbatch` instead.