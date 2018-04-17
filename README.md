# Jupyter Notebook
[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/911)

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
user=$(whoami)

cd $PBS_O_WORKDIR

# print tunneling instructions jupyter-log
echo -e "
1. SSH tunnel from your workstation using the following command:
   
   ssh -L ${port}:${node}:${port} ${user}@$PBS_O_HOST
   
   and point your web browser to http://localhost:${port}.

2. Copy/paste the token below when you connect for the first time.
"

# load modules
module load jupyter-notebook/latest

jupyter-notebook
```

## Start a Jupyter Notebook
1. Copy contents of jupyternb.pbs (example above) to a file in your home directory.

2. Open terminal on cluster login node and submit the job script:

```
$ qsub jupyternb.pbs
```

## Connect to Notebook
1. Check output file (*jobname*.o*JOBNUM*) for details.

Example output file: jnb.o152668
```
MacOS or linux terminal command to create your ssh tunnel:
ssh -L 9454:node01:9454 tester@loginnode

Compute node: node01
Remote port: 9454

Use a Browser on your local machine to go to:
http://localhost:9454

[I 17:59:45.913 NotebookApp] Serving notebooks from local directory: /home/tester/jupyter-test
[I 17:59:45.913 NotebookApp] 0 active kernels
[I 17:59:45.913 NotebookApp] The Jupyter Notebook is running at:
[I 17:59:45.914 NotebookApp] http://node01:9454/?token=2dd17...
[I 17:59:45.914 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 17:59:45.920 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://node01:9454/?token=2dd17...
```

2. Open second terminal and run tunneling command from the output file:
```
$ ssh -L 9454:node01:9454 tester@loginnode
```
3. Open a browser and enter the URL from the output file:
```
http://localhost:9454
```
4. Enter the token (long string after ?token=) from the output file.

You should now be connected to your Jupyter Notebook that is running on a cluster compute node. To close the notebook, select Logout. If you need to reconnect, repeat steps. If you're done with your Notebook, remember to stop the job with qdel.

