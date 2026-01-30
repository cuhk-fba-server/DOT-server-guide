[[**Create Account / Reset Password**](https://forms.gle/ghY9dEvQY1548kmK7)] [[**Report Issue**](https://docs.google.com/forms/d/e/1FAIpQLSfEhb-JFyDJY4YJZTm_8JhlqI9xnspSksopMaF1Cem5TAclyw/viewform?usp=sf_link)] [[**Deposit Datasets on CUHK Data Repository**](https://github.com/qcbegin/cuhkbiz-data-repo-guide)]
<br></br>

# Introduction

This document provides an overview of two HPC (High Performance Computing) clusters in the Department of Decisions, Operations and Technology (DOT), CUHK Business School. 

These clusters are designed to support research requiring significant computational resources, such as machine learning, data analytics, optimization algorithms, and simulation modeling.

Currently, clusters are divided into two types based on their configuration levels. They are independent of each other.

> ⚠️ **Important Note:**
> 
> For now, only the faculty and PhD Students of the Department of Decisions, Operations and Technology are allowed to apply for an account. If you are a CUHK affiliate, please ask your collaborating faculty of the DOT department to apply for an account on your behalf.

Our HPC system follows a shared resource model that balances flexibility with efficiency:

- Each user has an independent base environment that can be customized according to specific research needs
- The SLURM scheduling system ensures fair allocation of computational resources among all users
- A unified file system allows seamless access to your files from any node in the cluster

If you encounter any issues with the system or have specific customization requests, please contact the administrator via [this support form](https://docs.google.com/forms/d/e/1FAIpQLSfEhb-JFyDJY4YJZTm_8JhlqI9xnspSksopMaF1Cem5TAclyw/viewform?usp=sf_link). We maintain a regularly updated [troubleshooting document](https://github.com/QiansiqiHu/DOT-server/blob/main/Jupyter_env.pdf) that addresses common installation and configuration issues.

# Standard Cluster

> **Latest Update on Server Status:**
> 
> [Jan. 13, 2026]
> The cluster is online and is available for user testing.
> </br>

## Resouce Summary

Here’s a summary of the total computing resources available in our HPC cluster:

| Resource         | Quantity                     |
| ---------------- | ---------------------------- |
| CPU              | 64 cores, 128 threads        |
| RAM              | 96GB (32GB DDR4 + 64GB DDR5) |
| GPU              | 16 NVIDIA RTX 4090           |
| Storage          | 144 TB (18TB × 8 drives)     |
| Operating System | Ubuntu 22.04.4 LTS           |


## Components

Our cluster consists of two types of computer servers at this moment:

- *Login nodes* handle user login, light computation, and storage.
- *Compute nodes* handle heavy computation.

![HPC-architecture](./img/architecture.png)

You will spend most of your time interacting with our **login node (113)**, including using JupyterLab and uploading your files and codes. As all nodes share a common file system, your files will be available everywhere even though you are only uploading them to a login node.

### Login Node (137.189.75.113)

This server is used for login and your data storage. You can do light computations on this server, but since they are shared by all users and many services are running on it, this is NOT RECOMMENDED.

|Component| Description|
|---------|------------|
|Operating System| Ubuntu 22.04.4 LTS |
|RAM| 32GB DDR4-3200 ECC RDIMM [x1] |
|CPU| Intel® Xeon® Silver 4309Y 12M Cache, 2.80 GHz (8C16T) [x1] |
|Storage|18TB SAS 12Gb/s 7.2K rpm Seagate Enterprise [x8]|

### Compute Nodes

#### GTX4090 Servers (137.189.75.114 & 137.189.75.115)

These two servers are equipped with graphics cards (NVIDIA 4090). You may use them for computational experiments. Below is the summary of these two servers. They are identical in configuration. 

|Component| Description|
|---------|------------|
|Operating System       |Ubuntu 22.04.4 LTS|
|RAM                    |32GB DDR5-4800 ECC RDIMM [x16]|
|CPU|Intel® Xeon® Gold 5416S 30M Cache, 2.00GHz (16C32T) [x2]|
|GPU|NVIDIA GeForce RTX 4090 24GB (CUDA 16,384 / Tensor 512) [x8]|

#### GTX3090 Servers (137.189.75.137 & 137.189.75.142)

|Component| Description|
|---------|------------|
|Operating System       |Ubuntu 22.04.4 LTS|
|RAM                    |32GB DDR4-3200 ECC RDIMM [x8]|
|CPU|Intel(R) Xeon(R) Gold 6348 CPU @ 2.60GHz (28C56T) [x2]|
|GPU|NVIDIA GeForce RTX 3090 24GB (CUDA 10,496 / Tensor 328) [x2]|

## How to use it?

There are two ways to use the cluster.

- Method 1. Web Access (JupyterHub)

In your web browser, you can navigate to login node `137.189.75.113`. The rest of the usage process can simply follow the standard Jupyterlab workflow. If you haven't used JupyterLab before, please refer to the [documentation](https://jupyterlab.readthedocs.io/en/latest/user/index.html) to learn it firstly.

Once you're familiar with JupyterLab, you can follow the steps in our Quick Start guide to use our cluster.

- Method 2. SLURM Task Submission

You can also submit your computational jobs via Slurm. Slurm allows you to directly submit Python scripts and supports submitting jobs either individually or in batches. Our Quick Start guide provides a brief overview of how to use Slurm on our platform. If you'd like to learn more about Slurm in detail, please refer to its official [documentation](https://slurm.schedmd.com/documentation.html).

- Method 3. SSH & SSH Client

This is a method that will soon be deprecated; currently, **it is only available on the standard cluster and is no longer supported on the H100 cluster**.

SSH connection offers the most powerful and flexible way to work with our GPU servers, especially for computationally-intensive research projects. The same username and password will be used.


# H100 Cluster

> **Latest Update on Server Status:**
> 
> [July 21, 2025]
> Server 114 is back online with 8 GPU cards available for use.
>
> [July 14, 2025]
> The maintenance on server 114 has been completed, and 7 GPU cards are now available for use. Another maintenance to identify the issue with the problematic GPU card (bus address: 0000:3F:00.0) is planned in the near future.
> 
> [July 2, 2025]
> The maintenance on server 114 has been completed, and all services have returned to normal operation.
>
> [May 8, 2025]
> All the nodes are back to service.
>
> [May 7, 2025]
> Our GPU servers have been unavailable for the past two days. Users who logged in may have been unable to access their notebooks (always pending in queue). We're pleased to report that one server is now operational and JupyterHub access has been restored. We will notify all users when server 115 returns to service.
>
> [March 24, 2025]
> The old JupyterHub service on 115 has been shut down. Please stop using the old login credentials and switch to the new ones instead. The JupyterHub service on 113 is now operational after its scheduled maintenance period (1:30 - 2:00 PM).
>
> [March 19, 2025]
> GPU card issue resolved: The previously missing GPU card is now functioning properly. We apologize for any inconvenience caused by the unexpected server shutdown resulting from our miscommunication.
>
> [March 18, 2025]
> We've identified that one GPU card is missing from node 115. Our team is currently working with IT staff to inspect the physical connection. Once we identify the issue, a system reboot may be necessary. We will notify all users before any scheduled downtime.
>
> [March 3, 2025]
> We have completed the service upgrade and data migration. Our new high-performance computing (HPC) cluster now integrates the computational resources of two GPU servers with a centralized storage and management system. Existing users can access the cluster through IP address 137.189.75.113 via web browser (JupyterHub) or SSH connections. To minimize disruption, we've created backups of your previous working folders. You can find these backups as a compressed archive or a folder with timestamps indicating when they were created. If no major issues arise during the **pilot phase (by Mar 23)**, we plan to discontinue the existing JupyterHub service on 115.
>
> [January 20, 2025]
> The server (137.189.75.115) has been successfully restored. All services are up and running.
>
> [January 18, 2025]
> IP address 137.189.75.115 is currently inaccessible from campus network (both browser and SSH connections affected). We are working with IT staff to identify and > resolve the connectivity issue. We will notify all users once service is restored.
> <br></br>

## Resouce Summary

Here’s a summary of the total computing resources available in our HPC cluster:

| Resource         | Quantity                     |
| ---------------- | ---------------------------- |
| CPU              | 768 (256x3) cores, 1,536(512x3) threads        |
| RAM              | 9 (3x3) TB |
| GPU              | 24 (8x3) NVIDIA H100           |
| Storage          | 502 TB     |
| Operating System | Ubuntu 22.04.5 LTS           |


## Components

Our cluster consists of two types of computer servers at this moment:

- *Login nodes* handle user login, light computation, and storage.
- *Compute nodes* handle heavy computation.

![HPC-architecture](./img/architecture_1.png)

You will spend most of your time interacting with our **login node (119)**, including using JupyterLab and uploading your files and codes. As all nodes share a common file system, your files will be available everywhere even though you are only uploading them to a login node.

### Login Node (137.189.75.119)

This server is used for login and your data storage. You can do light computations on this server, but since they are shared by all users and many services are running on it, this is NOT RECOMMENDED.

|Component| Description|
|---------|------------|
|Operating System| Ubuntu 22.04.5 LTS |
|RAM| 63GB |
|CPU| Intel(R) Xeon(R) Silver 4310 CPU @ 2.10GHz [x2] |
|Storage|1TB|

### Compute Nodes

#### H100 Servers (137.189.75.116 & 137.189.75.117 & 137.189.75.118)

These three servers are equipped with graphics cards (NVIDIA H100). You may use them for computational experiments. Below is the summary of these three servers. They are identical in configuration. 

|Component| Description|
|---------|------------|
|Operating System       |Ubuntu 22.04.5 LTS|
|RAM                    |3.2 TB DDR5|
|CPU|AMD EPYC 9754 128-Core Processor [x2]|
|GPU|NVIDIA H100 NVL (96GB) [x8]|


## How to use it?

There are two ways to use the cluster.

- Method 1. Web Access (JupyterHub)

In your web browser, you can navigate to login node `137.189.75.113`. The rest of the usage process can simply follow the standard Jupyterlab workflow. If you haven't used JupyterLab before, please refer to the [documentation](https://jupyterlab.readthedocs.io/en/latest/user/index.html) to learn it firstly.

Once you're familiar with JupyterLab, you can follow the steps in our Quick Start guide to use our cluster.

- Method 2. SLURM Task Submission

You can also submit your computational jobs via Slurm. Slurm allows you to directly submit Python scripts and supports submitting jobs either individually or in batches. Our Quick Start guide provides a brief overview of how to use Slurm on our platform. If you'd like to learn more about Slurm in detail, please refer to its official [documentation](https://slurm.schedmd.com/documentation.html).


# Supported Software

Both clusters support the same software.

| Software | Jupyter Notebook | Console | Desktop Interface |
| -------- | ---------------- | ------- | ----------------- |
| Python   | Yes              | Yes     | -                 |
| R        | Yes              | Yes     | No                |
| Stata (needs extra application)   | Yes              | Yes     | No                |
| MATLAB   | No               | No      | No                |

### Python and R

Python is fully supported on our GPU servers and ready to use immediately through either Jupyter Notebook or command line interface. R is also available to all registered users through the same interfaces (See this [guide](R_guide.md) for more instructions if you have no prior experience to use R in Jupyter). 

### Stata

Stata is available on the server but requires an additional access application before use. This restriction exists because our subscription is a network license limited to 2 concurrent users. You must send an email beforehand or claim it when registering an account to request access. A guide is provided [here](stata.md).

### Additional Software Requests

If you need access to other software packages (such as `MATLAB`), please submit your request through [our form](https://docs.google.com/forms/d/e/1FAIpQLSfEhb-JFyDJY4YJZTm_8JhlqI9xnspSksopMaF1Cem5TAclyw/viewform?usp=sf_link). We regularly review all software requests to better accommodate our users' research needs.
