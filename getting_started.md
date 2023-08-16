# Getting Started on Linux
1. Go to https://www.anaconda.com/ and download and install anaconda.
	1. Find the Linux 64-bit (x86) installer from https://www.anaconda.com/download#downloads and copy the URL
	2. ssh into the Linux environment
	3. In your home directory, run ```wget <URL>``` to download the installer.
	4. Change the permissions of the installer with ```sudo chmod 755 <INSTALLER>```.
	5. Run the installer with ```./<INSTALLER>``` and continue with all default options.
	6. When it asks you to initialize, say yes.
	7. To be able to use Anaconda in the next step, either run ```source ~/.bashrc``` or logout and login.
3. Setup PyTorch environment, run the following commands:
	1. ```conda create --name torch```
	2. ```conda activate torch```
4. Go to https://pytorch.org/get-started/locally/
	1. For Linux, select Linux and Conda and the earliest CUDA version (currently is 11.7). 
	2. Run the listed command in terminal.
	3. Verify it is installed correctly by typing the following and it should print ```True```.
    	```
     	python
        import torch
     	torch.cuda.is_available()
6. Install dependencies
	1. ```conda install -c conda-forge matplotlib h5py scikit-learn dill scipy seaborn tensorboard tqdm numpy```
