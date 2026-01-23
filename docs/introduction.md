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

# Common-configuration Cluster

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



# High-configuration Cluster

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
