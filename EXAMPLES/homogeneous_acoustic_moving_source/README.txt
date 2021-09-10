Simulation for moving souce at constant velocity in homogeneous acoustic medium 

Mesh Info: 
-100m cube
-36 mesh elements per side (=2.77m per element)

Source info: 
-speed= 4m/s
-freq=50Hz (sine)
-amplt=0.1
-f0=0.011

Simulation info:
Nsteps=20,000
dt=1.5e-4
time=3s

###############################################
to run simulation follow steps:

#First lets ensure we have everything in order before we run any jobs

1. Git pull both repos to update (OR CLONE NEW: git clone --recursive --branch master https://github.com/homnath/specfem3d.git)

2. Copy the .bash files (vim ~/.bashrc) - this makes sure we have proper
compilers

3. configure parallel program (./configure FC=gfortran CC=gcc MPIFC=mpif90
--with-mpi) - we can also configure for a single processor.

4. compile via either make all or make (xdecompose_mesh,xgenerate_databases,xspecfem3D)

5.Ensure all submit & DATA files have same number of processors and correct
file locations

6. link bin using command: ln -s ../../bin/  (ls bin to check)

7.make output files: "mkdir OUTPUT_FILES" followed by "mkdir OUTPUT_FILES/DATABASES_MPI"

8. decompose mesh: "./bin/xdecompose_mesh #PROCS MESH OUTPUT_FILES/DATABASES_MPI"    (substitude number of processors used for #PROCS)

For Parrallel processing on CAC:
-generate databses: "sbatch submit_data"     (Make sure to change directory in submit_data to current directory and number of proccessors used)
-run solver: "sbatch submit_run"             (Make sure to change directory in submit_data to current directory and number of proccessors used))


For Single processing:
-generate databses: "./bin/xgenerate_databases"
-run solver: "./bin/xspecfem3D"

EXTRA TIPS:
to check status of job use: squeue -u <username>
less output_solver.txt to check status of job in specfem3D
May need to modify source code (take DT out of 2 files)       
