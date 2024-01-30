`Slurm <https://docs.rc.fas.harvard.edu/kb/convenient-slurm-commands/>`_ is used on all the PICSL lambda machines to handle GPU allocation.

Slurm an open source, fault-tolerant, and highly scalable cluster management  and job scheduling system for large and small Linux clusters, similar in function to LSF on the BSC PMACS cluster.

Slurm provides ``srun`` for interactive commands -- waiting for the command to complete, and ``sbatch`` for non-interactive commands.

In the simplest form you can run

.. code-block:: bash

    sbatch --gres gpu:3 myprogram

and Slurm will allocate 3 gpus for ``myprogram`` and set the environment variable ``CUDA_VISIBLE_DEVICES``

to a comma delimited list of the allocated gpus, eg: ``CUDA_VISIBLE_DEVICES="1,2,3"`` for ``/dev/nvidia1``, ``/dev/nvidia2``, ``/dev/nvidia3``.

``ibash`` and ``xbash`` equivalents are:

.. code-block:: bash

    ibash = srun --pty bash
    xbash = salloc --nodelist lambda-recon bash -c 'ssh -Y $(scontrol show hostnames | head -n 1)'

A more complete synopsis of srun and sbatch are:

.. code-block:: bash

    srun [-c N][--gres gpu:N][--{mem|mem-per-cpu|mem-per-gpu} N[K|M|G|T]][--node-list lambda-{picsl|recon|clam}] [-pty] command
    sbatch [-c N][--gres gpu:N][--{mem|mem-per-cpu|mem-per-gpu} N[K|M|G|T]] [-o stdout-file][--error stderr-file] command

By default, ``--gres gpu:N`` is exclusive access

See https://docs.rc.fas.harvard.edu/kb/convenient-slurm-commands/ for more complete documentation.

-Gaylord
