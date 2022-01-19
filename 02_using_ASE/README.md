# Setup
Decide a working directory for your jupter notebooks. e.g. `$HOME/jupyter/notebooks/`

```
JUPDIR=$HOME/jupyter/notebook
mkdir -p $JUPDIR
cd $JUPDIR
git clone git@github.com:PaNOSC-ViNYL/workshop2020.git
cd workshop2020/
git checkout team2
cd demo/team2/
```

# Dependencies
This demo requires the following packages to be installed on the machine running the jupiter notebook

## python modules
 - notebook
 - ase
 - McStasScript
 - dill
You can install them by doing:
```
pip3 install --user -r requirements.txt
```

## Building dependencies for other executables

Executables might require compilation and installation if there are no packages for your distribution.

In the following instructions for CENTOS8 can be found.


The PREFIX variable stores the directory where you want the binaries to be installed. By default it is /usr/local/ but you might not have admin permission, so you might want to install it in your HOME directory.
Defining a PREFIX directory in your home is recommanded since there is no uninstall script for QE...

If you want to make a local installation, create a dedicated directory in your home, e.g. $HOME/PANOSC/src/ and set the following variables accordingly.
```
PREFIXDIR=$HOME/PANOSC/
PREFIX="--prefix=$PREFIXDIR"
if [ -n "$PREFIX" ]; export PATH=$PATH:$PREFIXDIR/bin; fi
```

Choose a directory where to download the source packages and compile and set the environment variables accordingly.
```
BUILDDIR=$HOME/PANOSC/src/
mkdir -p $BUILDDIR
```

### Quantum-Espresso (QE)
For this demo, only the planewave part needs to be compiled and installed, but you can decide to compile it entirely.

Dependencies:
- blas
- hdf5
- mpich

Install the dependencies:
```yum install -y gcc-gfortran blas-devel hdf5-devel```
	
Download and compile QE:
```
cd $BUILDDIR
QE_pkg="https://github.com/QEF/q-e/releases/download/qe-6.5/qe-6.5-ReleasePack.tgz"
wget -c $QE_pkg
tar -xzf `basename $QE_pkg`
cd `basename $QE_pkg`
./configure $PREFIX
make -j4 pw
make install
cd $BUILDDIR
```

### McStas
McStas is available in binary format via a dedicated repository.
So if you have root priviledges, this is the recommended way to install it.
```
yum-config-manager --add-repo http://packages.mccode.org/rpm/mccode.repo
yum install mcstas-2.6 mcstas-suite-python mpich-devel -y
```

# Execution
```
jupyter notebook
```

It should automatically open your browser to the right page, otherwise follow the instructions on the command line.

Click on the `ase.ipynb` file to open the notebook.
Enjoy.
