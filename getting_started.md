# Getting Started on Linux

## Install Package manager
1a. If you have root access, you can go to https://www.anaconda.com/ and download and install the mini-anaconda directly.
1b. Much easier: you can install a pre-downloaded anaconda package manager and then run it without root access (accomplishes same thing). If there is not already one in your home directory, there will probably be one in /home/dab/
	A. Either way, run the installer with ```./<INSTALLER>``` and continue with all default options. [Note the installer file will have to have 'executable' permissions to do this.]
	B. To be able to use conda in the next step, either run ```source ~/.bashrc``` or logout and login.
2. Setup PyTorch environment, run the following commands:
	1. ```conda create --name torch```
	2. ```conda activate torch```
3. Install and verify the installation of pytorch.
	1. pytorch now prefers being installed by pip, apparently. So first install pip by running ```conda install pip```
	2. Install pytorch: ```pip install torch torchvision```
	3. Verify it is installed correctly by typing the following and it should print ```True```.
    	```
     	python
        import torch
     	torch.cuda.is_available()
     	quit()
		```
4. Install dependencies
	1. ```conda install matplotlib h5py scikit-learn dill scipy seaborn tensorboard tqdm numpy jupyter scikit-image```
 	2. (Optional: for faster package finding, install ```conda install conda-libmamba-solver```, then set it as your solver ```conda config --set solver libmamba```.)
	3. (Optional: to install ```optuna``` for hyperparameter optimization, install it via the conda-forge channel ```conda install -c conda-forge optuna```.)
5. Setup a password for jupyter notebook. Type ```jupyter notebook password```. Enter your desired password.

## Setup git permissions
(https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux)
1. On the remote Linux machine (or while you are ssh'd), create a new ssh key with ```ssh-keygen```. (Use the defaults, and don't worry about creating a passcode for this.) In the output, find the filename ending in ```*.pub```. This is your ssh public key. (By default, your key is named ```id_ed25519.pub```.
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

## Setup ssh tunnel to connect to the jupyter notebook remotely
1. Optional - If you want to keep your jupyter server running even when you close your remote connection:
   	1. Open a new screen with the command ```screen```
   	2. Re-activate your conda environment in the new terminal screen with ```conda activate torch```
3. On the remote Linux machine, start a jupyter server on power 4567 without opening a browser with ```jupyter notebook --no-browser --port=4567```.
   	1. If you ran this command on a new screen from step 1, return to your original screen with ```Ctrl-A``` followed by ```Ctrl-D```.
5. Setup an ssh tunnel from your client machine (laptop). In terminal, type ```ssh -N -L 4567:localhost:4567 <username>@<ip address>```. Replace ```<username>``` with your username and ```<ip address>``` with the ip address of the remote Linux host you are connecting to.
6. Type in your password. If it succeeds, the comman will stay running in your terminal with no output. When you are ready to end the ssh tunnel, press Ctrl+C or just close the terminal window.
7. Go to your jupyter notebook by opening a browser and going to URL ```localhost:4567```. On the first connection, it will prompt you for a password. Provide the one you setup with ```jupyter notebook password``` in the Install Packages section.

## Checkout the NeuroTheoryLab packages
1. ```git clone git@github.com:NeuroTheoryUMD/ColorDataUtils.git```
2. ```git clone git@github.com:NeuroTheoryUMD/NDNT.git```
3. ```git clone git@github.com:NeuroTheoryUMD/NTdatasets.git```
