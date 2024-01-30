GPU Allocation using SLURM
==========================

**All users must use Slurm to request GPUs to prevent resource contention**

`Slurm <https://docs.rc.fas.harvard.edu/kb/convenient-slurm-commands/>`_ is used on all the PICSL lambda machines to handle GPU allocation fairly. Slurm an open source, fault-tolerant, and highly scalable cluster management  and job scheduling system for large and small Linux clusters, similar in function to LSF on the BSC PMACS cluster.

Slurm provides ``srun`` for running interactive commands and ``sbatch`` for non-interactive commands.

Interactive Sessions
--------------------

If you want to run an interactive task (e.g, train a deep learning network from command line) using one GPU, execute

.. code-block:: sh

    srun --gres gpu:1 --pty /bin/bash

This will launch a terminal for you on one of the GPU machines and set thee environment variable ``CUDA_VISIBLE_DEVICES`` to the number of the GPU that has been allocated for you, e.g., ``CUDA_VISIBLE_DEVICES=1``. It is a **very good idea** to use a terminal manager like tmux or screen to ensure a persistent session. 


Non-Interactive Sessions
------------------------
If you want to run a non-interactive script or a program on three GPUs, execute

.. code-block:: sh

    sbatch --gres gpu:3 myprogram

and Slurm will allocate 3 gpus for ``myprogram`` and set the environment variable ``CUDA_VISIBLE_DEVICES`` to a comma delimited list of the allocated gpus, eg: ``CUDA_VISIBLE_DEVICES="1,2,3"`` for ``/dev/nvidia1``, ``/dev/nvidia2``, ``/dev/nvidia3``.


For PMACS/LFS Users
-------------------
The equivalents of your familiar commands ``ibash`` and ``xbash`` are:

.. code-block:: bash

    ibash = srun --pty bash
    xbash = salloc --nodelist lambda-recon bash -c 'ssh -Y $(scontrol show hostnames | head -n 1)'

Additional Options
------------------
A more complete synopsis of srun and sbatch are:

.. code-block:: bash

    srun [-c N][--gres gpu:N][--{mem|mem-per-cpu|mem-per-gpu} N[K|M|G|T]][--node-list lambda-{picsl|recon|clam}] [-pty] command
    sbatch [-c N][--gres gpu:N][--{mem|mem-per-cpu|mem-per-gpu} N[K|M|G|T]] [-o stdout-file][--error stderr-file] command

By default, ``--gres gpu:N`` is exclusive access

See https://docs.rc.fas.harvard.edu/kb/convenient-slurm-commands/ for more complete documentation.

-Gaylord
