# Getting Started on Linux
1. Go to https://www.anaconda.com/ and download and install anaconda.
2. Setup PyTorch environment, run the following commands:
	1. ```conda create --name torch```
	2. ```conda activate torch```
3. Go to https://pytorch.org/get-started/locally/
	1. For Linux, select Linux and Conda and the earliest CUDA version (currently is 11.7). 
	2. Run the listed command in terminal.
4. Install dependencies
	1. ```conda install -c conda-forge matplotlib h5py scikit-learn dill scipy seaborn tensorboard tqdm numpy```