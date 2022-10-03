# Contributing to adjDocs using the adjTomo container

This document serves to show contributors how to push changes to the adjDocs repo using a combination of their local machine (for GitHub interface) and the adjTomo software container (to develop changes). 

The motivation is here is to:
- save contributors time by side-stepping software installation  
- ensure all contributors are using the same software suite  
- ensure that paths are all set correctly when running notebooks inside a container 
- mimic a real world run time environment, rather than a local development environment

Steps involved in a nutshell:
1) Download Docker for your machine
2) `docker pull` the latest adjTomo Image
3) `git pull` the latest adjDocs repo
4) `docker run` a container and **bind mount** your adjDocs repo into the container
5) Make and save changes to adjDocs **inside the container**
6) `git push` your changes from your local

Steps involved outside the nutshell:

#### 1) Download Docker

https://docs.docker.com/get-docker/

#### 2) `docker pull` 
see: https://github.com/adjtomo/adjdocs/blob/main/readmes/docker_image_install.md

For Mac Intel Chip, Linux and Windows:
```bash
docker pull ghcr.io/seisscoped/adjtomo:ubuntu20.04
```

For Mac M1 Chip:
```bash
docker pull --platform arm64 ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

**Note**: If you are constantly running Docker pull and running out of space, see Notes A and B below.

#### 3) `git pull`

On your local, you will want a copy of the adjDocs repository. Wherever you store repositories, you can run

```bash
git pull git@github.com:adjtomo/adjdocs.git
# OR 
git pull https://github.com/adjtomo/adjdocs.git
```

#### 4) `docker run`

We want to mount our adjDocs repo **inside** the container so that your local and container are sharing the same repo

For Mac Intel Chip, Linux and Windows:  
```bash
cd adjdocs
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/adjdocs --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04
```

For Mac M1 Chip:  
```bash
docker run -p 8888:8888 --mount type=bind,source=$(pwd),target=/home/scoped/work --shm-size=1gb ghcr.io/seisscoped/adjtomo:ubuntu20.04_jupyterlab
```

**Note**: if your adjDocs repo seems out of date compared to whats on GitHub, its likely because we haven't rebuilt the container since changes have been pushed. See Note A and pulling fresh changes from inside the container.

**Note**: if you want to save the work you did on the container to your local, see Note C below.

#### 5) Edit adjDocs (inside container)

From **inside** the container, you can make edits to adjDocs using the internal Jupyter Notebook system. Any changes you are making will also be made to your local repository. Please be sure the **clear all output** when saving notebooks to the workshop directory. Probably best practice to **run all** before pushing to make sure that there are no bugs.

#### 6) `git push` (outside container)

After completing your changes to adjDocs, go back to your local terminal and push the changes. We do this because the inside of the container doesn't know your Git information, and it doesn't store changes permanently. BUT your local machine doesn't know the containers file system, nor does it have the same software suite installed.

```bash
cd adjdocs  # if youre not already here
git push
```

Any quesitons, feel free to email: `bhchow@alaska.edu`


### Note A: Pulling adjDocs inside the container

If the adjTomo software suite hasn't changed since your last `docker pull`, but the adjDocs repo has, you can save yourself some time and hassle by just running a `git pull` inside the adjDocs repo, inside the container. That is, from inside the container you can run:

```bash
cd /home/scoped/adjdocs
git pull
```

### Note B: Removing old Docker images

These Images are large (>5Gb), and everytime you run `docker pull`, you download another copy. It is often useful then to remove old images. You can check what current images you have by running:

```bash
docker images
```

If you have multiple copies of the adjTomo Image, you are free to delete them. Some of these may have **Containers** associated with them (live or exited sessions which are spawned from the Image itself), which will need to be closed first. If you do not have any currently running Containers that you want to preserve, the fastest way to close **all** containers is to run:

```bash
docker ps -a  # view all open/exited containers
docker container prune  # delete all exited containers
```

Once all containers are closed, you can remove unnused images by running `docker rmi <image number>`, where the Image number is listed next to the name of of the Image when running `docker images`. For example, to **delete** an image on my machine, I woudl run

```bash
[~] $ docker images
REPOSITORY                   TAG           IMAGE ID       CREATED      SIZE
ghcr.io/seisscoped/adjtomo   ubuntu20.04   7de5769b1ba7   2 days ago   5.53GB
[~] $ docker rmi 7de5769b1ba7
```

### Note C: Bind mounting other directories

If you also want to save results of your development, you can bind mount a work directory to the container. All of the workshop material is saved (inside the container) at `/home/scoped/work`, so this will be our mount target. On your local, find an working directory \<PATH_TO_WORKDIR> before `docker run`ning your container. You'll also need to replace the path to the adjDocs repository \<PATH_TO_ADJDOCS> on your local in the command below

```bash
docker run -p 8888:8888 \
    --mount type=bind,source=<PATH_TO_ADJDOCS>,target=/home/scoped/adjdocs \
    --mount type=bind,source=<PATH_TO_WORKDIR>,target=/home/scoped/work \ 
    --shm-size=1gb \
    ghcr.io/seisscoped/adjtomo:ubuntu20.04
```
