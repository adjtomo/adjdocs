# Docker Image Installation Instructions
For the SPECFEM Users Workshop (Oct. 5-7, 2022)

- The following instructions are meant to **install** a Docker Image, which contains all the software you will need to participate in the workshop    
- This Docker Image is ~5.5 GB, workshop material ~2.5 GB; please ensure you have sufficient disk space (10 GB free to be safe)   
- Please ensure that you have completed these instructions **before** the workshop, to avoid any delays the day of  
- See the troubleshooting notes at the bottom if you run into any issues. If they do not help please attend Day 0  
- Please attend Day 0 if you have any trouble with installing Docker, installing the Image, or running the Day 0 notebook  
- These commands will need to be run from your computer's terminal program. To access Terminal,
    - Mac: Type 'terminal' into Spotlight
    - Windows: Type 'powershell' in the system search bar
    - Linux: Type 'terminal' in the system search bar


## 1A) Instructions for Windows, Linux and Mac Intel Chip

>__NOTE__: Mac M1 Users see '1B) Instructions for Mac M1 Chip' below!

Install the Docker Image from GitHub
```bash
docker pull ghcr.io/seisscoped/adjtomo:ubuntu20.04
```

To save the results we obtain from inside our container, we will need to mount our local filesystem.  
**> Please `cd` (change directory) to an empty working directory (example below)**  

```bash
# NOTE: This is only an EXAMPLE code snippet. Please create an 
# appropriate empty working directory on your machine
mkdir -p ~/Work/specfem_users_workshop
cd ~/Work/specfem_users_workshop
```

Now run the container to open a JupyterLab instance
```bash
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04 
```

## 1B) Instructions for Mac M1 Chip

Installs the Docker Image from GitHub
```bash
docker pull --platform arm64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

To save the results we obtain from inside our container, we will need to mount our local filesystem.  
**> Please `cd` (change directory) to an empty working directory (example below)**  
```bash
# NOTE: This is only an EXAMPLE code snippet. Please create an 
# appropriate empty working directory on your machine
mkdir -p ~/Work/specfem_users_workshop
cd ~/Work/specfem_users_workshop
```

Now run the container to open a JupyterLab instance
```bash
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

## 2) Open JupyterLab (all operating systems)

- After running the `docker run` command, you will see some output that ends with a web address, e.g,.

```bash
[bchow@blackbox specfem_users_workshop]$ docker run -p 8888:8888 --mount type=bind,source=(pwd),target=/home/scoped/work ghcr.io/seisscoped/adjtomo:ubuntu20.04              
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

## 3) Update adjDocs

- To get the latest copy of the workshop material we will need to update adjDocs, our documentation repository
- Please **double click** Terminal (`$_` icon in the 'Other' section) to open up the JupyterLab terminal  
- Run the following commands inside the terminal to update adjDocs  

```bash
cd ~/adjdocs
git pull
```

A successful 'git pull' should result in output that looks something like this:

```bash
root@2579daf64918:~/adjdocs# git pull
remote: Enumerating objects: 66, done.
remote: Counting objects: 100% (44/44), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 66 (delta 23), reused 44 (delta 23), pack-reused 22
Unpacking objects: 100% (66/66), 2.51 MiB | 1.64 MiB/s, done.
From https://github.com/adjtomo/adjdocs
   0b1596a..01da4ca  main       -> origin/main
...
root@2579daf64918:~/adjdocs# 
```

## 4) Run Day 0 Notebook

- Using the navigation bar on the left, click through the following directories  
- *adjdocs -> workshops -> 2022-10-05_specfem_users -> day_0_container_testing.ipynb*  
- This will open up a Jupyter Notebook  
    - **If you have time**, please read through the notebook and execute cells one by one  
    - **If you just want to test that things work**, please click 'Run' -> 'Run All Cells' in the navigation bar at the top  
- Please note the run time for completing the entire notebook, it should be on the order of 10-20 minutes for a modern computer  
- Please attend Day 0 of the Workshop (Oct. 4) if you have any trouble with the above instructions

--------------

# Troubleshooting Notes
You can disregard this section if you successfully completed steps 1-4 above

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
