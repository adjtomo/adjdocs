# SCOPED Specfem/SeisFlows Workshop Material

Welcome! In this repository you will find SPECFEM/SeisFlows workshop material for the [2024 SCOPED UW Workshop](https://seisscoped.org/workshop-2024/) to be held May 20-24, 2024. Here you will find the workshop notebooks and below you will find installation instructions for the Docker container that hosts the software needed for this material.

## Docker Image Installation Instructions

- First you will need to install Docker: https://www.docker.com/get-started/ 
- The following instructions are meant to **install** a Docker Image, which contains all the software you need to participate  
- This Docker Image is ~3.98 GB, workshop material will create another ~1GB; please ensure you have sufficient disk space  
- See the troubleshooting notes at the bottom for common issues you might encounter  
- If you have any issues running the steps below that are not solved by the troubleshooting notes, feel free to open up a [GitHub issue](https://github.com/adjtomo/adjdocs/issues)

### 1) Open a Terminal
- The commands in the following sections will need to be run from your computer's terminal program   
- To open the terminal on your **local machine**: 
    - Mac: Type 'terminal' into Spotlight
    - Windows: Type 'powershell' in the system search bar
    - Linux: Type 'terminal' in the system search bar

### 2) Start Docker
- Docker will need to be running in the background before we can use it from the command line
- On **Windows or Mac**, use the search bar to find and open `Docker` `Docker.app` or `Docker Desktop`
- On **Linux**, run the following from the command line:
```bash
systemctl start docker
```


### 3) Pull Docker Image

- This will download the Docker Image from the SeisSCOPED GitHub repository
- Mac Intel Chip, Windows and Linux Users (AMD architecture) please follow instructions in A
- Mac Silicon Chip (ARM architecture; M1, M2, M3...) please follow instructions in B

#### 3A) Docker pull for Mac Intel, Windows, Linux
```bash
docker pull --platform amd64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

#### 3B) Docker pull for Mac Silicon 

Installs the Docker Image from GitHub
```bash
docker pull --platform arm64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

### 4) Make Empty Working Directory

To save the results we obtain from inside our container, we will need to mount our local filesystem.  
**> Please `cd` (change directory) to an empty working directory (example below)**  

```bash
# NOTE: This is only an EXAMPLE code snippet. Please create an 
# appropriate empty working directory on your machine
mkdir -p ~/Work/scoped_uw_2024
cd ~/Work/scoped_uw_2024
```

### 5) Run Container

Now run the container to open a JupyterLab instance (see notes below for explanation of this command)  
```bash
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

### 6) Open JupyterLab 

- After running the `docker run` command, you will see some output that ends with a web address, e.g,.

```bash
# DO NOT COPY THE CODE BLOCK BELOW, it is just an example
$ docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
[I 2024-05-16 15:59:20.338 ServerApp] jupyter_lsp | extension was successfully linked.
[I 2024-05-16 15:59:20.341 ServerApp] jupyter_server_terminals | extension was successfully linked.
[I 2024-05-16 15:59:20.343 ServerApp] jupyterlab | extension was successfully linked.
[I 2024-05-16 15:59:20.346 ServerApp] notebook | extension was successfully linked.
[I 2024-05-16 15:59:20.346 ServerApp] Writing Jupyter server cookie secret to /home/scoped/.local/share/jupyter/runtime/jupyter_cookie_secret
[I 2024-05-16 15:59:20.518 ServerApp] notebook_shim | extension was successfully linked.
[I 2024-05-16 15:59:20.529 ServerApp] notebook_shim | extension was successfully loaded.
[I 2024-05-16 15:59:20.530 ServerApp] jupyter_lsp | extension was successfully loaded.
[I 2024-05-16 15:59:20.530 ServerApp] jupyter_server_terminals | extension was successfully loaded.
[I 2024-05-16 15:59:20.532 LabApp] JupyterLab extension loaded from /opt/conda/lib/python3.10/site-packages/jupyterlab
[I 2024-05-16 15:59:20.532 LabApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
[I 2024-05-16 15:59:20.532 LabApp] Extension Manager is 'pypi'.
[I 2024-05-16 15:59:20.539 ServerApp] jupyterlab | extension was successfully loaded.
[I 2024-05-16 15:59:20.540 ServerApp] notebook | extension was successfully loaded.
[I 2024-05-16 15:59:20.541 ServerApp] Serving notebooks from local directory: /home/scoped
[I 2024-05-16 15:59:20.541 ServerApp] Jupyter Server 2.14.0 is running at:
[I 2024-05-16 15:59:20.541 ServerApp] http://c80bdafc9ee2:8888/lab?token=6e70b595bd7d62bde09db852053971b28f2f012574ca0a95
[I 2024-05-16 15:59:20.541 ServerApp]     http://127.0.0.1:8888/lab?token=6e70b595bd7d62bde09db852053971b28f2f012574ca0a95
[I 2024-05-16 15:59:20.541 ServerApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 2024-05-16 15:59:20.543 ServerApp]

    To access the server, open this file in a browser:
        file:///home/scoped/.local/share/jupyter/runtime/jpserver-8-open.html
    Or copy and paste one of these URLs:
        http://c80bdafc9ee2:8888/lab?token=6e70b595bd7d62bde09db852053971b28f2f012574ca0a95
        http://127.0.0.1:8888/lab?token=6e70b595bd7d62bde09db852053971b28f2f012574ca0a95
[I 2024-05-16 15:59:20.806 ServerApp] Skipped non-installed server(s): bash-language-server, dockerfile-language-server-nodejs, javascript-typescript-langserver, jedi-language-server, julia-language-server, pyright, python-language-server, python-lsp-server, r-languageserver, sql-language-server, texlab, typescript-language-server, unified-language-server, vscode-css-languageserver-bin, vscode-html-languageserver-bin, vscode-json-languageserver-bin, yaml-language-server
```

- Please **open** the bottom link (starting with http://127.0.0.1:8888) with a web browser
- You will be met with the following looking web page  

![JupyterLab](https://user-images.githubusercontent.com/23055374/193501549-8f0d9429-1414-40c7-ad4d-0bdcf8ad6e55.png)

### 7) Run Workshop Material

- Using the navigation bar on the left, click through the following directories  
- *adjdocs -> workshops -> 2024-05-21_scoped_uw*  
- **Clicking** any of the workshop notebooks (e.g., *1_intro_specfem2d.ipynb*) will open a Jupyter Notebook  
- See 'Jupyter Quick Tips' at the top of any notebook for information on how to run through a notebook  
- Run cells one-by-one and sequentially, read along with text to follow workshop material  

---------------

> Great! You are ready to run the workshop material, please follow along with the material in each of the notebooks. The material below is for when you are done with the workshop (Workshop Shut Down Procedures), or if you have trouble with any of the above install instructions (Troubleshooting Notes)

---------------

## Workshop Shut Down Procedures

- These instructions are for when you are finished with the workshop and want to shut down the container and free up space    
- Before you approach any of these shut down procedures, please be sure to save any work you might have created   
- 'Created work' may include exercise notebooks that you filled out on your own, or files that you may have generated on your own  

### a) Removing Files from the *work/* Directory

- If you want to free up memory taken up by our workshop materials, the easiest way is to do it from **inside** the container  
- **WARNING** This will delete all files created by our workshop notebooks. You will not be able to recover these files  
- From the *Terminal* **inside** your container, you can run the following commands to remove all the workshop-created files:  

```bash
# Run the following from inside your container's terminal, not on your local machine
rm -r /home/scoped/work
```

### b) Closing a Running Container

- From inside the JupyterLab interface, you can **click** `File -> Shut Down` in the top navigation bar  
- **OR** from the terminal where you ran the `docker run` command (which should still be running), you can type `Ctrl + c` on your keyboard to stop a running session

### c) Re-opening a Closed Container

- It is possible to re-open a closed container, however we did not do this during the workshop to keep things simpler  
- You may follow this documentation if you want to re-open a closed container (https://docs.docker.com/engine/reference/commandline/container_start/)

### d) Deleting Closed Containers

- Although you have closed your container, each container still occupies some memory on your local machine  
- This can be freed up if you no longer want to access the container's contents  
- Run the following command to free up memory associated with all closed containers

```bash
docker container prune
```

### e) Removing Workshop Docker Image

- If you want to **remove** our workshop's Docker Image (which takes up ~3.98GB), you will need to identify the Image ID
- To do that, you can run

```bash
docker images
```

- You will be met with a list of available Docker Images. Ours has Repository name: *'ghcr.io/seisscoped/adjtomo'*, and Tag: *'ubuntu20.04_jupyterlab'*  
- You will need to identify the hash value listed under **IMAGE ID** column and run the following command

```bash
docker rmi <IMAGE_ID>
```

- **For Example**: To do this on my own machine I would run:

```bash
# DO NOT COPY THE CODE BLOCK BELOW, it is just an example
REPOSITORY                   TAG                      IMAGE ID       CREATED         SIZE
ghcr.io/seisscoped/adjtomo   ubuntu20.04_jupyterlab   3a6ddce01b76   20 hours ago    3.99GB
bchow@tern [~] $ docker rmi 3a6ddce01b76
```

--------------

> If everything worked and you have successfully completed the steps above, congratulations! Please disregard everything below. If you are having trouble, please see the 'Troubleshooting Notes' section below.  

--------------

## Troubleshooting Notes

>__ERROR:__ $(pwd) not recognized in `docker run` command of Step 1  

- *$(pwd)* is a Linux command that might not be recognized by all operating systems  
- Please change the *$(pwd)* to the full path to your current working directory, e.g.,

```bash
# Note that you will need to substitute <PATH_TO_WORKING_DIR> with your own path
docker run -p 8888:8888 --mount type=bind,source=<PATH_TO_WORKING_DIR>,target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

for example on my own computer this might look like:  
```bash
# Do NOT copy-paste this, it is just an example and will not work on your computer
docker run -p 8888:8888 --mount type=bind,source=/Users/Chow/Work/specfem_users_workshop,target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

>__ERROR:__ *Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?*  

- You need to start Docker or Docker Desktop on your machine. 
- On **Windows or Mac**, use the search bar to find 'Docker' or 'Docker Desktop'. Open this program and try again  
- On **Linux** try running:   
```bash
systemctl start docker
```

>__ERROR:__ Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "...": dial unix /var/run/docker.sock: connect: permission denied
- Your user does not have the correct permission to access the Docker daemon
- If you have root privelage on your machine, try running the following:
```bash
 sudo chmod 666 /var/run/docker.sock
```
- You may also need to add your user to a Docker group which has the correct privileges ([see this link](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user))  

>__ERROR__: docker: Error response from daemon: driver failed programming external connectivity on endpoint hopeful_haslett (c3e93dc3530d474e5152cf7ec58d69030da2be534f47fc94bcc6da19177f60f4): Bind for 0.0.0.0:8888 failed: port is already allocated.
- You likely have another task (e.g., Jupyter Notebooks) running on the port we are trying to specify (8888:8888)
- Please change the port map to something else, e.g., *docker run -p 8889:8888*... and try again
- **Note** that you will also have to change the web address that you open in your browser to the new port number (e.g., http://127.0.0.1:8889/lab...)  


## Docker Command Explanation

```bash
docker pull ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

- `docker pull` downloads the Docker Image from GitHub  
- `docker run` launches the container. The flags in the `run` command are:  
    -  `--mount`: binds our local filesystem (in the current working directory) with the **container's internal filesytem** (at location */home/scoped/work* which resides **inside** the container)  
    -  `--shm-size`: tells Docker to give us 1 Gigabyte of shared memory, which is required for MPI processes  
- Note that the *$(pwd)* argument may not be recognized by your operating system. If so, please see the troubleshooting notes below    
- You may substitute any directory for *$(pwd)*, even remote filesystems, as long as they are accessible by your current machine  



## Version Tracking
Keeping track of versions used for the workshop. These will also be pinned to the container.

- SPECFEM2D 8.1.0: baeb71d
- SPEECFEM3D 4.1.1: ee3b095
- SeisFlows v3.2.1: e96e888c
- PySEP v0.6.0: 9e77ad3
- Pyatoa v0.4.0: 1a6b86a
