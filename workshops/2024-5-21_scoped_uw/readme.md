# SCOPED Specfem/SeisFlows Workshop Material

Welcome! In this repository you will find SPECFEM/SeisFlows workshop material for the [2024 SCOPED UW Workshop](https://seisscoped.org/workshop-2024/) to be held May 20-24, 2024. Here you will find the workshop notebooks and below you will find installation instructions for the Docker container that hosts the software needed for this material.

## Docker Image Installation Instructions

- The following instructions are meant to **install** a Docker Image, which contains all the software you will need to participate in the workshop. This assumes you have already installed Docker on your machine  
- This Docker Image is ~3.98 GB, workshop material will create another ~1GB; please ensure you have sufficient disk space  
- See the troubleshooting notes at the bottom for common issues you might encounter  
- If you have any issues running the steps below that are not solved by the troubleshooting notes, feel free to open up a [GitHub issue](https://github.com/adjtomo/adjdocs/issues)

### 0) Open a Terminal
- The commands in the following sections will need to be run from your computer's terminal program   
- To open the terminal on your **local machine**: 
    - Mac: Type 'terminal' into Spotlight
    - Windows: Type 'powershell' in the system search bar
    - Linux: Type 'terminal' in the system search bar


### 1) Pull Docker Image

- This will download the Docker Image from GitHub
- Mac Intel Chip, Windows and Linux Users (AMD architecture) please follow instructions in 1A
- Mac M1 Chip (ARM architecture) please follow instructions in 1B


#### 1A) Docker pull for Mac Intel, Windows, Linux
```bash
docker pull --platform amd64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

#### 1B) Docker pull for Mac M1

Installs the Docker Image from GitHub
```bash
docker pull --platform arm64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

### 2) Make Empty Working Directory

To save the results we obtain from inside our container, we will need to mount our local filesystem.  
**> Please `cd` (change directory) to an empty working directory (example below)**  

```bash
# NOTE: This is only an EXAMPLE code snippet. Please create an 
# appropriate empty working directory on your machine
mkdir -p ~/Work/specfem_users_workshop
cd ~/Work/specfem_users_workshop
```

### 3) Run Container

Now run the container to open a JupyterLab instance (see notes below for explanation of this command)  
```bash
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

### 4) Open JupyterLab 

- After running the `docker run` command, you will see some output that ends with a web address, e.g,.

```bash
# DO NOT COPY THE CODE BLOCK BELOW, it is just an example
[bchow@blackbox specfem_users_workshop]$ docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work ghcr.io/seisscoped/adjtomo:workshop2022           
[I 2022-10-03 02:45:25.543 ServerApp] jupyterlab | extension was successfully linked.
[I 2022-10-03 02:45:25.548 ServerApp] nbclassic | extension was successfully linked.
[I 2022-10-03 02:45:25.549 ServerApp] Writing Jupyter server cookie secret to /home/scoped/.local/share/jupyter/runtime/jupyter_cookie_secret
[I 2022-10-03 02:45:25.704 ServerApp] notebook_shim | extension was successfully linked.
[I 2022-10-03 02:45:25.714 ServerApp] notebook_shim | extension was successfully loaded.
[I 2022-10-03 02:45:25.715 LabApp] JupyterLab extension loaded from /opt/conda/lib/python3.10/site-packages/jupyterlab
[I 2022-10-03 02:45:25.715 LabApp] JupyterLab application directory is /opt/conda/share/jupyter/lab
[I 2022-10-03 02:45:25.717 ServerApp] jupyterlab | extension was successfully loaded.
[I 2022-10-03 02:45:25.719 ServerApp] nbclassic | extension was successfully loaded.
[I 2022-10-03 02:45:25.719 ServerApp] Serving notebooks from local directory: /home/scoped
[I 2022-10-03 02:45:25.719 ServerApp] Jupyter Server 1.18.1 is running at:
[I 2022-10-03 02:45:25.719 ServerApp] http://4196322a7bd0:8888/lab?token=864237545761973aa9f70fd458c19d40d6b3b52549dafc6e
[I 2022-10-03 02:45:25.719 ServerApp]  or http://127.0.0.1:8888/lab?token=864237545761973aa9f70fd458c19d40d6b3b52549dafc6e
[I 2022-10-03 02:45:25.719 ServerApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 2022-10-03 02:45:25.721 ServerApp] 
    
    To access the server, open this file in a browser:
        file:///home/scoped/.local/share/jupyter/runtime/jpserver-13-open.html
    Or copy and paste one of these URLs:
        http://4196322a7bd0:8888/lab?token=864237545761973aa9f70fd458c19d40d6b3b52549dafc6e
     or http://127.0.0.1:8888/lab?token=864237545761973aa9f70fd458c19d40d6b3b52549dafc6e
```

- Please **open** the bottom link (starting with http://127.0.0.1:8888) with a web browser
- You will be met with the following looking web page  

![JupyterLab](https://user-images.githubusercontent.com/23055374/193501549-8f0d9429-1414-40c7-ad4d-0bdcf8ad6e55.png)

### 5) Update adjDocs

- To get the latest copy of the workshop material we will need to update adjDocs, our documentation repository
- Please **double click** Terminal (`$_` icon in the 'Other' section) to open up the JupyterLab terminal  
- Run the following commands inside the terminal to update adjDocs  

```bash
cd ~/adjdocs
git pull
```

A successful 'git pull' should result in output that looks something like this:

```bash
# DO NOT COPY THE CODE BLOCK BELOW, it is just an example
root@9613bff72a41:~/adjdocs# git pull
remote: Enumerating objects: 345, done.
remote: Counting objects: 100% (173/173), done.
remote: Compressing objects: 100% (93/93), done.
remote: Total 345 (delta 119), reused 120 (delta 80), pack-reused 172
Receiving objects: 100% (345/345), 29.07 MiB | 22.27 MiB/s, done.
Resolving deltas: 100% (204/204), completed with 11 local objects.
From https://github.com/adjtomo/adjdocs
   17378b6..77b2fe6  main       -> origin/main
Updating 17378b6..77b2fe6
Fast-forward
...
root@2579daf64918:~/adjdocs# 
```

>__NOTE:__ If you have made any changes to the adjDocs repository, the `git pull` command may fail. The easiest way to resolve this is to stop your current container and start a new one. Alternatively you may run `git stash` to hide any changes you have made, before running `git pull`  

### 6) Run Workshop Material

- Using the navigation bar on the left, click through the following directories  
- *adjdocs -> workshops -> 2024-05-21_scoped_uw*  
- **Clicking** any of the workshop notebooks (e.g., *1_intro_specfem2d.ipynb*) will open a Jupyter Notebook  
- See 'Jupyter Quick Tips' at the top of any notebook for information on how to run through a notebook  
- Run cells one-by-one and sequentially, read along with text to follow workshop material  
- If encounter any issues running the notebooks, please open up a [GitHub issue](https://github.com/adjtomo/adjdocs/issues)  

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


### Docker Command Explanation

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


### Troubleshooting Notes

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


### Version Tracking
Keeping track of versions used for the workshop. These will also be pinned to the container.

- SPECFEM2D 8.1.0: baeb71d
- SPEECFEM3D 4.1.1: ee3b095
- SeisFlows v3.2.1: e96e888c
- PySEP v0.6.0: 9e77ad3
- Pyatoa v0.4.0: 1a6b86a
