# Manual Software Install for SPECFEM Users Workshop Oct 5-7, 2022

- These instructions are **use at your own risk**, and meant for advanced Users  
- Manual install instructions are aimed at those running M1 Macs that cannot find alternatives  
- Participants who are able should use the Docker container provided in the workshop email  
- The following instructions must be run from your terminal, on your **local** machine  
- Following along the the notebooks will require you to make edits to the root directory of the adjDocs notebooks
- If you do not follow instructions exactly, there is a good chance that the workshop material will not work as expected.
- **NOTE:** You will likely need ~10GB of free disk space for this installation and the workshop  


## Step 1: Download/Install Miniconda

https://docs.conda.io/en/latest/miniconda.html

Please follow along the instructions below and install Conda for your OS

## Step 2: Create a Conda environment
- Our container runs Python version 3.10
- All our Python-based tools are installed into a Conda environment
- Conda environments help preserve root environments

```bash
conda create -n adjtomo python=3.10
conda activate adjtomo
```

## Step 3: Download required software from GitHub
- Create an empty working directory where all workshop files are stored
- Here we choose a directory called 'scoped', created in our Home directory
- Remember where this directory is, you will need it during the workshop  
- Your SPECFEM2D and SPECFEM3D repositories will differ from the workshop versions. This is OK.

```bash
# Create an empty working directory under the Home directory
mkdir -p $HOME/scoped
cd $HOME/scoped

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
- These steps install the adjTomo software and all their dependencies
- **Run lines one-by-one** incase something fails, you know where the failure point is
- Make sure that you have run the 'conda activate' command in Step 2
- To confirm this, you should see the prefix '(adjtomo)' on your command line prompt

```bash
cd $HOME/scoped/pyatoa 
conda install --file requirements.txt -y
pip install -e . 

cd $HOME/scoped/seisflows 
conda install --file requirements.txt -y
pip install -e . 

cd $HOME/scoped/pysep 
conda install --file requirements.txt -y
pip install -e .

# We need Jupyter to run the adjDocs workshop notebooks
conda install jupyter -y
```

## Step 5: Install SPECFEM
- The following steps configure and compile SPECFEM2D and SPECFEM3D with MPI
- Your computer will need a FORTRAN compiler and MPI (see Compiler Note 1 if you are unsure)  
- If you do not have these, the install will likely fail. See 'Compiler Note 2' below

```bash
cd $HOME/scoped/specfem2d 
./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi
make all 

cd $HOME/scoped/specfem3d 
./configure FC=gfortran CC=gcc CXX=mpicxx MPIFC=mpif90 --with-mpi 
make all 
```

### Compiler Note 1
- To check if you have the required compilers, run the following
- Each statement should return a path to an existing compiler
- If any return nothing (blank line or immediate return to prompt), see 'Compiler Note 2'  

```bash
which gcc
which gfortran
which mpif90
```

### Compiler Note 2
- Only required if you do not have the required FORTRAN compiler or MPI necessary for Step 5
- We use Mac's native 'Homebrew' to install a FORTRAN compiler and OpenMPI
- First run the steps here in Note 1 and then **re-attempt** Step 5
- If things **still** do not work, attempt 'Compiler Note 3'

```bash
brew update
brew upgrade
brew install gcc
brew install gfortran
brew install openmpi
```

### Compiler Note 3
- If your FORTRAN compiler **still** does not work you may try removing CommandLineTools
- Some relevant links on this procedure incase you are worried  
    - https://www.cocoanetics.com/2012/07/you-dont-need-the-xcode-command-line-tools/
    - https://apple.stackexchange.com/questions/308943/how-do-i-uninstall-the-command-line-tools-for-xcode
    
```bash
sudo rm -r /Library/Developer/CommandLineTools
xcode-select --install
```

## Step 6: Check Installation
- Run the Day 0 Notebook inside Jupyter to make sure things have worked properly

```bash 
cd $HOME/scoped/adjdocs/workshops/2022-10-05_specfem_users/
jupyter notebook
```

- The 'Jupyter' command will have opened up an interface in your web browser
- **Click** on `day_0_container_testing.ipynb`
- **Click** `Run All` which is the $\blacktriangleright\blacktriangleright$ button at the top