# Docker Image Installation Instructions
For the SPECFEM Users Workshop (Oct. 5-7, 2022)

- The following instructions are meant to **install** a Docker Image, which contains all the software you will need to participate in the workshop    
- This Docker Image is roughly 5.5 GB, workshop material will take about 2.5 GB. Please ensure you have sufficient disk space (10 GB free to be safe)   
- Please ensure that you have completed these instructions **before** the workshop, to avoid any delays the day of  
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


## 3) Run Day 0 Notebook

- Using the navigation bar on the left, click through the following directories  
- *adjdocs $\rightarrow$ workshops $\rightarrow$ 2022-10-05_specfem_users $\rightarrow$ day_0_container_testing.ipynb*  
- This will open up a Jupyter Notebook  
    - **If you have time**, please read through the notebook and execute cells one by one  
    - **If you just want to test that things work**, please hit 'Run All Cells' ($\blacktriangleright\blacktriangleright$ at the top)  
- Please note the run time for completing the entire notebook, it should be on the order of 10-20 minutes for a modern computer  
- Please attend Day 0 of the Workshop (Oct. 4) if you have any trouble with the above instructions
