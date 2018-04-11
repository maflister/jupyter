# Jupyter-Notebook
[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/893)

Singularity container running latest Ubuntu and Jupyter Notebook.

Example job script:
```
#!/bin/bash
#PBS -N jnb
#PBS -l nodes=1:ppn=1
#PBS -l mem=5gb
#PBS -l walltime=1:00:00
#PBS -j oe

# get tunneling info
port=$(shuf -i8000-9999 -n1)
node=$(hostname -s)
jumphost=$(hostname)
user=$(whoami)

cd $PBS_O_WORKDIR

# print tunneling instructions jupyter-log
echo -e "
MacOS or linux terminal command to create your ssh tunnel:
ssh -L ${port}:${node}:${port} ${user}@${jumphost}

Compute node: ${node}
Remote port: ${port}
Use a Browser on your local machine to go to:
http://localhost:${port}
"

# load modules
module load jupyter-notebook/latest

jupyter-notebook
```

