# Introduction 

This example shows how to use TensorFlow to run a training application using
one GPU both as a batch job and through a jupyter notebook.  You will use a
small, local dataset to train a MLP for classification. Investigate the
directory structure under `data.tar.gz` with the command `tar --exclude="*.png" -tvf`
and feel free to experiment with your own images instead. The dataset is a
a MNIST-digits but resized to 10x10 pixels and changed into only black or white
pixel values.

By the end of the tutorial, you should know how to run TensorFlow applications using: 

    1- the module tree
    2- jupyter notebooks
  
## 1- Using the batch system
To run the example as a batch job, submit the job script: `sbatch ex1.sh`. Read
the content of the job script and familiarize yourself with the important
parameters.  Note that on Alvis, launching at least one GPU is a must for jobs
to be allowed to run on the compute nodes.

After the job ends, investigate the log file generated by the dcgmi daemon to
see which performance metrics can be examined.


## 2- Jupyter Notebook

### Environment setup
To setup your environment for running jupyter notebooks, see
<https://www.c3se.chalmers.se/documentation/applications/jupyter/>. Note that
you must have logged in to the system with X forwarding. Load the IPython
module first:
```
module load GCC/8.3.0  CUDA/10.1.243  OpenMPI/3.1.4 IPython/7.9.0-Python-3.7.4
```

Next, load the TensorFlow and the Pillow modules:

```
ml TensorFlow/2.3.1-Python-3.7.4 Pillow/6.2.1
``` 

### Running jupyter notebooks
Using the command line, fire up a jupyter notebook and browse into the tutorial's notebook `cnn_with_own_data.ipynb`.

To run the heavier stuff, opt for a batch job, or use the compute nodes for
your notebooks:
```
srun -A YourAccount -p alvis --gpus-per-node=... -t 00:10:00 --pty jupyter notebook
```

where you should fill in the type and the number of
GPUs that you would like to launch as well as the right project account. Adjust
the wall time if needed too.
