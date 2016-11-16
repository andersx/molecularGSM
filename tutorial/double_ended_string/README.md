#### Double-ended String Method Tutorial

## 1) Compile the program. 

You will need to install BLAS and LAPACK first (if not already installed)

    $ sudo apt-get install libblas-dev liblapack-dev
    
Note, the version from ZimmermanGroup requires Intel MKL and is set up to use Intel's non-free compilers. This version defaults to GCC with generic Lapack and BLAS.

To compile type:

    $ make

## 2) Setting the program
Head into the tutorial/double_ended_string folder, and copy the executable to this directory.

    $ cd tutorial/double_ended_string
    $ ls
    ggrad  gstart  initial0001.xyz  inpfileq  ograd  scratch

You will see a bunch of file and a scratch directory

In the ggrad change the two variables to 1) where your gaussian executable is located, and your local scratch dir.

    export GAUSS_EXEDIR=/opt/g09
    export GAUSS_SCRDIR=/home/$USER/scr

In the gstart, you setup the header for the gaussian calculation. The default for this example is PM6:

    # pm6 force
    
    Title
    
    0 1

This is standard Gaussian notation. Change the pm6 for your method and basis of choice. The "force" keyword should not be changed. The line "0 1" is the charge and multiplicity, respectively

Furthermore, there is an initial0001.xyz file, which contains the reactant and the product for the reaction. Copy this file into the scratch/ dicrectory
