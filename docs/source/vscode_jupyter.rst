VS Code and Jupyter with GPU
----------------------------

This is a quick guide on how to combine ``slurm`` on the PICSL GPU workstations with VSCode and Jupyter. We should all switch to working this way to ensure that GPUs are shared fairly and consistently.

* Login to one of the lambda machines and use a terminal manager like ``tmux`` or ``screen`` to ensure a permanent session
* You should always use **slurm** to request GPU on the lambda machines

.. code-block:: sh

    srun --gres gpu:1 --nodelist lambda-picsl --pty /bin/bash    # if you want to land on a particular machine
    srun --gres gpu:1 --pty /bin/bash                            # if you don’t care which machine

* After this, you will get a terminal to the machine you requested, and ``CUDA_VISIBLE_DEVICES`` will be set
* Select your conda environment and run the Jupyter server (you may need a unique port):

.. code-block:: sh

    conda activate myenv
    $CONDA_ROOT/bin/jupyter notebook --no-browser --port 8891

* The notebook server will start and print a URL. Copy the ``http://127.0.0.1…`` URL to clipboard
* Connect to the machine using `VSCode SSH mode <https://code.visualstudio.com/docs/remote/ssh>`.
* Open/create a ``.ipynb`` file
* When selecting a Kernel, choose 'Existing Jupyter Kernel' and paste your URL
* PyTorch should respect the setting of ``CUDA_VISIBLE_DEVICES`` when you set the device to cuda
* Now you can run your notebook, and if you lose connection, you can reconnect to the running kernel with its state preserved.
