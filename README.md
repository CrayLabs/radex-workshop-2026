# Radex Workshop 2026

Materials for running workshop examples in 2026

## Running on Frontier

### Environment Setup

In order to set up your RHAPSODY/Dragon environment for Frontier, you need to execute the following:

```
source /lustre/orion/stf007/world-shared/atramirez/rhapsody-training/environment.sh
```

## Running on ALCF Aurora

### Environment Setup

In order to set up your RHAPSODY/Dragon environment for Aurora, source the following script.

```bash
source /flare/alcf_training/rhapsody/training_material/env_setup.sh
```

The contents of the script are also copied below

```bash
# Access venv with Rhapsody, DragonHPC and SmartSim/SmartRedis
module load frameworks
source /flare/alcf_training/rhapsody/training_material/venv/bin/activate
export PATH=/flare/alcf_training/rhapsody/training_material/SmartSim/smartsim/_core/bin:$PATH
export SR_LOG_FILE=stdout
export SR_LOG_LEVEL=QUIET

# Access OpenFOAM installation and the Rhapsody plugin
source /flare/catalyst/world_shared/bramesh/codes/OpenFOAM/OpenFOAM-v2606/etc/bashrc.aurora
export FOAM_USER_LIBBIN=/flare/alcf_training/rhapsody/training_material/OpenFOAM-v2606
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/flare/alcf_training/rhapsody/training_material/OpenFOAM-v2606
```

### Running the Examples

1. Get a compute node on Aurora with the following qsub command (one node is fine for the demo)

```bash
qsub -I -q R8794691 -A alcf_training -l select=1,walltime=01:00:00,filesystems=home:flare
```

2. Set up the environment

```bash
source /flare/alcf_training/rhapsody/training_material/env_setup.sh
``` 

3. To run the `pitzDaily-optimize` workflow, copy the clean example directory available on `/flare/alcf_training/rhapsody` to your preferred location and launch the workflow with `dragon`. When running on a single node, it is recommanded to use the `-s` option for the Dragon launcher.

```bash
cp -r /flare/alcf_training/rhapsody/training_material/pitzDaily-optimize /path/to/preferred/location
cd /path/to/preferred/location/pitzDaily-optimize
dragon -s driver-staged.py
```

You should expect to see something similar to the following output

```
Iteration 1: best parameters epsilon=30.8103, Cmu=0.138893, C1=1.02924, C2=1.88354; converged=True, final_step=346, avg_inlets=-2.36112, loss=0.212634
Iteration 2: best parameters epsilon=25.7455, Cmu=0.124644, C1=1.02196, C2=2.05247; converged=True, final_step=287, avg_inlets=-2.03995, loss=0.0195871
Iteration 3: best parameters epsilon=25.7455, Cmu=0.124644, C1=1.02196, C2=2.05247; converged=True, final_step=287, avg_inlets=-2.03995, loss=0.0195871
Iteration 4: best parameters epsilon=24.751, Cmu=0.141403, C1=1.02382, C2=2.02487; converged=True, final_step=259, avg_inlets=-1.84032, loss=0.00356132
Iteration 5: best parameters epsilon=24.751, Cmu=0.141403, C1=1.02382, C2=2.02487; converged=True, final_step=259, avg_inlets=-1.84032, loss=0.00356132
Iteration 6: best parameters epsilon=59.42, Cmu=0.1328, C1=1.01623, C2=2.00049; converged=True, final_step=352, avg_inlets=-1.91198, loss=0.000143552
```
