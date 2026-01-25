# Method 3. SSH & SSH Client (Only for Standard Cluster)

## Account Registration

To access our GPU servers, simply complete our [**registration form**](https://forms.gle/ghY9dEvQY1548kmK7). You'll receive your login credentials via email once your registration is approved.

## Network Prerequisite

Please make sure that the internet cable (in CYT) is available at your workplace OR that you have connected onto the [CUHK VPN service](https://www.itsc.cuhk.edu.hk/all-it/wifi-and-network/cuhk-vpn/). Otherwise, you will NOT be able to connect to the server for safety reasons.

If you're accessing the server from mainland China, you'll need the CUHK add-on VPN service for a stable connection. You can request this service through [this link](https://cuhk-edt.knowledgeowl.com/docs/pilot-cuhk-vpn-add-on-service). After approval, you'll receive an email with a specific portal address - use this instead of the standard VPN portal (access.cuhk.edu.hk).


SSH connection offers the most powerful and flexible way to work with our GPU servers, especially for computationally-intensive research projects. The same username and password will be used.

> [!NOTE]
> If you choose to bypass our web-based JupyterHub service and connect via SSH directly, please first launch JupyterHub once to initialize the conda environments. Without this step, you may encounter errors indicating that the conda command or `.bashrc` file cannot be found.

#### Recommended SSH Workflow

1. **Connect to the cluster** - We recommend connecting directly to the compute nodes (137.189.75.114 or 137.189.75.115) rather than the login node, as the compute nodes have significantly more processing power.
2. **Development environment** - Use VSCode Remote SSH or similar tools for code editing, which provides a familiar interface with syntax highlighting, code completion, and integrated terminal.
3. Running your code. **Direct execution**: You can then run Python scripts directly on the compute nodes.

> [!IMPORTANT]
> Please avoid running intensive computational tasks on the login node (137.189.75.113), as it has limited CPU resources and is shared by all users for administrative purposes.