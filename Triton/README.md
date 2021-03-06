# When logged in Triton:

**Step 1**: module load R

**Step 2**: Rscript triton_configuration.R model_set num_rep num_fits num_cores time

Generates triton_fit.slrm file, assumes that all the Stan models are in "SM" directory and that 10G memory per cpu is enough. For personal usage, notice that the directory paths "/scratch/work/kasevat1/BDA_SA/" in above script and in all other Triton scripts should be changed.

Parameters:

model_set = Keyword which is linked to all desired models. 

num_rep = Number of replications.

num_fits = Number of fits per array task (make sure num_rep/num_fits = integer).

num_cores = Number of cores per array task.

time = Time allocated for each job (x:00, where x depicts hours).



**Step 3**: sbatch triton_fit.slrm

Create partitions for fit diagnostics using data as "project_data.RData". Partitions are saved into "FDPS" directory and the "outputs" directory can be used for debugging. The progress of tasks can be checked with "slurm q" command.

**Step 4**: Rscript fill_fit_diagnostics.R

Fills all partial diagnostics to "fit_diagnostics_new" archive which can be visualized with "show_diagnostics.R" function. An example archive "fit_diagnostics" is included in master folder.








