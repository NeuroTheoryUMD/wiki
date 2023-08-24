# Getting Started on Linux

## Install Packages
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
     	quit()
6. Install dependencies
	1. For faster package finding, first install ```conda install conda-libmamba-solver```, then set it as your solver ```conda config --set solver libmamba```
	2. ```conda install -c conda-forge matplotlib h5py scikit-learn dill scipy seaborn tensorboard tqdm numpy optuna jupyter```
7. Setup a password for jupyter notebook. Type ```jupyter notebook password```. Enter your desired password.

## Setup git permissions
(https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux)
1. On the remote Linux machine, create a new ssh key with ```ssh keygen```. (Use the defaults, and don't worry about creating a passcode for this.) In the output, find the filename ending in ```*.pub```. This is your ssh public key. (By default, your key is named ```id_ed25519.pub```.
2. Print out the key with ```cat ~/.ssh/id_ed25519.pub``` (or whichever name your key is named).
3. Copy the entire output from terminal.
4. On your GitHub page, go to Settings (click on the user picture at the top right and the menu option is near the bottom).
5. In the "Access" section of the sidebar, click  SSH and GPG keys.
6. Click New SSH key or Add SSH key.
7. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".
8. Use the default "Authentication Key" as the Key Type.
9. In the "Key" field, paste the output from the ```cat ~/.ssh/id_ed25519.pub``` command you did earlier. Do this again if you lost this.
10. Click Add SSH key.
11. If prompted, confirm access to your account on GitHub.

## Setup ssh tunnelto connect to the jupyter notebook remotely.
2. On the remote Linux machine, start a jupyter server on power 4567 without opening a browser with ```jupyter notebook --no-browser --port=4567```.
3. Setup an ssh tunnel from your client machine (laptop). In terminal, type ```ssh -N -L 4567:localhost:4567 <username>@<ip address>```. Replace ```<username>``` with your username and ```<ip address>``` with the ip address of the remote Linux host you are connecting to.
4. Type in your password. If it succeeds, the comman will stay running in your terminal with no output. When you are ready to end the ssh tunnel, press Ctrl+C or just close the terminal window.
5. Go to your jupyter notebook by opening a browser and going to URL ```localhost:4567```. On the first connection, it will prompt you for a password. Provide the one you setup with ```jupyter notebook password``` in the Install Packages section.
