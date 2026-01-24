# Method 1. Web Access (JupyterHub)

## Account Registration

To access our GPU servers, simply complete our [**registration form**](https://forms.gle/ghY9dEvQY1548kmK7). You'll receive your login credentials via email once your registration is approved.

## Network Prerequisite

Please make sure that the internet cable (in CYT) is available at your workplace OR that you have connected onto the [CUHK VPN service](https://www.itsc.cuhk.edu.hk/all-it/wifi-and-network/cuhk-vpn/). Otherwise, you will NOT be able to connect to the server for safety reasons.

If you're accessing the server from mainland China, you'll need the CUHK add-on VPN service for a stable connection. You can request this service through [this link](https://cuhk-edt.knowledgeowl.com/docs/pilot-cuhk-vpn-add-on-service). After approval, you'll receive an email with a specific portal address - use this instead of the standard VPN portal (access.cuhk.edu.hk).



## Use Custom Conda Environment [Optional]

If you need a customized environment, you can create your own conda environment in a terminal by following the procedures described in the ["Custom Conda Environment"](#custom-conda-environment) section.

## Begin to Use Slurm

SSH connection offers the most powerful and flexible way to work with our GPU servers, especially for computationally-intensive research projects. The same username and password will be used.

> ⚠️ **NOTE**
>
> If you choose to bypass our web-based JupyterHub service and connect via SSH directly, please first launch JupyterHub once to initialize the conda environments. Without this step, you may encounter errors indicating that the conda command or `.bashrc` file cannot be found.

### Recommended SSH Workflow

1. **Connect to the cluster** - You can connect directly to the login nodes (137.189.75.119) .
2. **Development environment** - Use VSCode Remote SSH or similar tools for code editing, which provides a familiar interface with syntax highlighting, code completion, and integrated terminal.
3. Running your code - **SLURM jobs**: Use the `sbatch` command to submit jobs with specific resource requirements. This allows for efficient resource allocation and lets your jobs run even when you're disconnected. [Learn more about SLURM commands here](#running-time-consuming-scripts-efficiently-through-slurm).

> ⚠️**IMPORTANT**
>
> Please avoid running intensive computational tasks on the login node (137.189.75.119), as it has limited CPU resources and is shared by all users for administrative purposes. *This means you should not run Python script on login node directly. All computation job should be submitted by `slurm`*.