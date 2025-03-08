# Running cuOT on Gilbreth

### Building an Apptainer to run Ferret OT on GPU
1. Build a ferret apptainer: `apptainer build --sandbox ferret.sif ferret.apptainer`
2. Submit a job to Gilbreth to run the apptainer: `sbatch --nodes=1 --gpus-per-node=1 ferret_job_file`

### Building an Apptainer to run Silent OT
1. Build a silent apptainer: `apptainer build --sandbox silent.sif silent.apptainer`
2. Submit a job to Gilbreth to run the apptainer: `sbatch --nodes=1 --gpus-per-node=2 silent_job_file`

## Apptainer notes:
- Adding `--sandbox` will allow you to make changes and write to the apptainer after building. Removing `--sandbox` increases portability and shrinks the size of the apptainer.
- After building the apptainer, you can run it with `apptainer run --nv ferret.sif` (The `--nv` flag is important for allowing CUDA programming to be used)
- You can also run a writable shell of the apptainer with: `apptainer shell --writable --nv ferret.sif` (Do this if you need to make changes or install more items)
- Note: Running the apptainer on Gilbreth without submitting a job will result in failure because the proper resources have not been acquired

### Other Notes
- Currently, you must request 1 node with 2 GPUs for silent OT, because the Silent OT checks that each party has a GPU


More details on running jobs on Gilbreth and tracking them can be found [here](https://www.rcac.purdue.edu/knowledge/gilbreth/run/slurm/submit).
