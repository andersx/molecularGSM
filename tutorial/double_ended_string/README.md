## Double-Ended Growing String (GSM) Method Tutorial - Claisen rearrangement 

#### 1) Compile the program. 
First off, clone my repository:

    $ git clone git@github.com:andersx/molecularGSM.git

You will need to install BLAS and LAPACK in order to compile (if not already installed):

    $ sudo apt-get install libblas-dev liblapack-dev
    
Note, the version from ZimmermanGroup requires Intel MKL and is set up to use Intel's non-free compilers. This version defaults to GCC with generic Lapack and BLAS.

To compile type:

    $ make

#### 2) Setting the program
2.1) Head into the tutorial/double_ended_string folder, and copy the executable to this directory.

    $ cd tutorial/double_ended_string
    $ ls
    ggrad  gstart  initial0001.xyz  inpfileq  ograd  scratch

You will see a bunch of file and a scratch directory

2.2) In the ggrad change the two variables to 1) where your gaussian executable is located, and your local scratch dir.

    export GAUSS_EXEDIR=/opt/g09
    export GAUSS_SCRDIR=/home/$USER/scr

2.3) In the gstart, you setup the header for the gaussian calculation. The default for this example is PM6:

    # pm6 force
    
    Title
    
    0 1

This is standard Gaussian notation. Change the pm6 for your method and basis of choice. The "force" keyword should not be changed. The line "0 1" is the charge and multiplicity, respectively

2.4) The file inpfileq contains the settings for the GSM method. The settings here work with the Claisen rearrangement in this example.

2.5) Furthermore, there is an initial0001.xyz file, which contains the reactant and the product for the reaction. Copy this file into the scratch/ dicrectory. The format of this filename is quite strict, so if you want another filname (e.g. running several calculations), you are only allowed to change the four digits. 

#### 3) Running the program
2.1) The program runs parallel with OpenMP, however, since the bottleneck is the gradient calculations, I suggest running your QM program in parallel, and just calculate a single node concurrently. I found that otherwise somtimes you end up with only one QM calculation running, but this is just my guide - might be different for your calculation.

To setup the number of concurrent nodes (set to 1) being calculated, export the following variable for OpenMP:

    $ export OMP_NUM_THREADS=1

3.2) Starting the program! You need to remember the the four digits of your inputfile (0001 in this case), and how many cores you want Gaussian to use for the QM gradient evaluation. These are the two arguments. Lets say four cores in this example.

    $ ./gfstringq.exe 0001 4

3.3) If it doesn't run, you failed. If it does, you should (after convergence) see a file called stringfile.xyz0001, which contains the string and the energies along the path. 


#### 4) Other information.

You choose the program you want to use for the QM evaluation in the file qchem.h. To use e.g. ORCA, set "SE_ORCA 1" and recompile. If you set all USE_xxx to 0, the default seems to be MOPAC. In the tutorial folder, there is a file named ograd, required to setup ORCA calculations (instead of the ggrad file), and it works very similary. I only tested these three programs so far, so I have no experience to setup GSM with other methods.

Feel free to fork+update this tutorial!
