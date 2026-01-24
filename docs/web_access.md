# Method 1. Web Access (JupyterHub)

## Account Registration

To access our GPU servers, simply complete our [**registration form**](https://forms.gle/ghY9dEvQY1548kmK7). You'll receive your login credentials via email once your registration is approved.

## Network Prerequisite

Please make sure that the internet cable (in CYT) is available at your workplace OR that you have connected onto the [CUHK VPN service](https://www.itsc.cuhk.edu.hk/all-it/wifi-and-network/cuhk-vpn/). Otherwise, you will NOT be able to connect to the server for safety reasons.

If you're accessing the server from mainland China, you'll need the CUHK add-on VPN service for a stable connection. You can request this service through [this link](https://cuhk-edt.knowledgeowl.com/docs/pilot-cuhk-vpn-add-on-service). After approval, you'll receive an email with a specific portal address - use this instead of the standard VPN portal (access.cuhk.edu.hk).



## Use Custom Conda Environment [Optional]

If you need a customized environment, you can create your own conda environment in a terminal by following the procedures described in the ["Custom Conda Environment"](#custom-conda-environment) section.

## Begin to Use Jupyter
Using Jupyter requires only a browser—no special software installation needed. Follow these steps to begin working with our GPU resources:

> ⚠️**NOTE**
>
> Each user's Jupyter server will automatically terminate after 1 days (24 hours). For longer tasks that may exceed this time limit, we recommend:
> 1. add periodic save points in your scripts
> 2. use Method 2 (SSH connection) instead, which doesn't have this time limitation.

1. In your web browser, navigate to `137.189.75.119`. You'll see the following login page:

![image](./img/hpc-login.png)

2. Enter your username and password to log in. Wait a few seconds for your Jupyter server to start. You'll then see the familiar JupyterLab interface:

> ⚠️**NOTE**
>
> You may see a `"Pending in Queue"` message. This indicates that your requested resources are not currently available. You can either select a lighter resource option or wait until you receive a notification that your server is ready.

![image](./img/hpc-jupyter.png)

By default, a **Standard CPU** setup will be automatically selected. If you would like to use other options, follow these steps:

1. Click "File -> Hub Control Panel" to access the server control page
2. Click "Stop My Server"
3. Then click "Start My Server"
4. You'll now see various computing environment options
5. Select the resource configuration that best fits your requirements

| Option                    | **Description**                                      | **Max CPU Power** | **Max RAM** | **GPU Available** |
| ------------------------- | ---------------------------------------------------- | ----------------- | ----------- | ----------------- |
| **Standard CPU Instance** | Suitable for general data analysis and computations  | 64 cores           | 24GB        | No GPU            |
| **Small GPU Instance**    | Designed for deep learning with a single GPU         | 64 cores           | 32GB        | 1 GPU             |
| **Medium GPU Instance**   | For mid-sized deep learning tasks with 2 GPUs        | 128 cores          | 64GB        | 2 GPUs            |
| **Large GPU Instance**    | High-performance setup for large-scale deep learning | 256 cores          | 128GB        | 4 GPUs            |

![image](./img/hpc-spawn-0.png)
![image](./img/hpc-spawn.png)

3. You're now ready to start coding! We've provided two pre-configured conda environments for easy access (see installed libraries [here](./conda_envs.md)). Simply click one of the two Python buttons under "Notebook" to begin.