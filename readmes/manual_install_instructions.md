# Manual Software Install for SPECFEM Users Workshop Oct 5-7, 2022

- These instructions are **use at your own risk**, and meant for advanced Users
- Manual install instructions are for those running M1 Macs that cannot find alternatives
- The following instructions must be run from your terminal, on your local machine
- These instructions download SPECFEM2D, SPECFEM3D_Cartesian, Conda and the adjTomo software suite
- The end product is that your local machine will be set up the same as the workshop container
- Following along the the notebooks will require working in a `/home/scoped` working directory
- If you do not follow instructions exactly, there is a good chance that the workshop material will not work as expected.
- We heavily suggest that you attempt to find an alternative OS before attempting this manual setup


## Step 1: Download/Install Miniconda

https://docs.conda.io/en/latest/miniconda.html

Please follow along the instructions below and install Conda for your OS

## Step 2: Create a Conda environment

```bash
conda create -n adjtomo python=3.10
conda activate adjtomo
```

## Step 3: Download required software from GitHub
```bash
# Create a working directory that mimics the container
mkdir /home/scoped
cd /home/scoped

# Download the adjTomo software suite
git clone https://github.com/adjtomo/adjdocs 
git clone --branch devel https://github.com/adjtomo/seisflows 
git clone --branch devel https://github.com/adjtomo/pyatoa 
git clone https://github.com/uafgeotools/pysep.git

# Download SPECFEM2D and SPECFEM3D_Cartesian
git clone --branch devel https://github.com/geodynamics/specfem2d 
git clone --branch devel --depth=1 https://github.com/geodynamics/specfem3d
```

## Step 4: Install the adjTomo software suite
```bash
cd /home/scoped/pyatoa 
conda install --file requirements.txt 
pip install -e . 

cd /home/scoped/seisflows 
conda install --file requirements.txt 
pip install -e . 

cd /home/scoped/pysep 
conda install --file requirements.txt 
pip install -e . 
```

## Step 5: Install SPECFEM
```bash
cd /home/scoped/specfem2d 
./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi
make all 

cd /home/scoped/specfem3d 
./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi 
make all 
```

