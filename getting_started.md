# Getting Started on Linux

## Install Package manager
<ol>
<li>If you have root access, you can go to https://www.anaconda.com/ and download and install the mini-anaconda directly.</li>
<li>Much easier: you can install a pre-downloaded anaconda package manager and then run it without root access (accomplishes same thing). If there is not already one in your home directory, there will probably be one in /home/dab/
	<ol>
	<li>Either way, run the installer with <code>./[INSTALLER]</code> and continue with all default options. [Note the installer file will have to have 'executable' permissions to do this.]
	<li>To be able to use conda in the next step, either run <code>source ~/.bashrc</code> or logout and login.
	</ol></li>
<li>Setup PyTorch environment, run the following commands:
	<pre>conda create --name torch<br>conda activate torch</pre>
</li>
<li>Install and verify the installation of pytorch.
	<ol>
	<li>Install pytorch: <code>pip install torch torchvision</code>
	<li>Verify it is installed correctly by typing the following and it should print <code>True</code>.
    	<pre>python<br>import torch<br>torch.cuda.is_available()<br>quit()</pre>
	</li></ol>
<li>Install dependencies
	<ol>
	<li><code>conda install matplotlib h5py scikit-learn dill scipy seaborn tensorboard tqdm numpy jupyter scikit-image</code></li>
 	<li>(Optional: for faster package finding, install <code>conda install conda-libmamba-solver</code>, then set it as your solver <code>conda config --set solver libmamba</code>.)
	</li></ol>
<li>Setup a password for jupyter notebook. Type <code>jupyter notebook password</code>. Enter your desired password.
</ol>

## Setup git permissions
(https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux)
1. On the remote Linux machine (or while you are ssh'd), create a new ssh key with <code>ssh-keygen</code>. (Use the defaults, and don't worry about creating a passcode for this.) In the output, find the filename ending in <code>*.pub</code>. This is your ssh public key. (By default, your key is named <code>id_ed25519.pub</code>.
2. Print out the key with <code>cat ~/.ssh/id_ed25519.pub</code> (or whichever name your key is named).
3. Copy the entire output from terminal.
4. On your GitHub page, go to Settings (click on the user picture at the top right and the menu option is near the bottom).
5. In the "Access" section of the sidebar, click  SSH and GPG keys.
6. Click New SSH key or Add SSH key.
7. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".
8. Use the default "Authentication Key" as the Key Type.
9. In the "Key" field, paste the output from the <code>cat ~/.ssh/id_ed25519.pub</code> command you did earlier. Do this again if you lost this.
10. Click Add SSH key.
11. If prompted, confirm access to your account on GitHub.

## Setup ssh tunnel to connect to the jupyter notebook remotely
1. Optional - If you want to keep your jupyter server running even when you close your remote connection:
   	1. Open a new screen with the command ```screen```
   	2. Re-activate your conda environment in the new terminal screen with <code>conda activate torch</code>
3. On the remote Linux machine, start a jupyter server on power 4567 without opening a browser with <code>jupyter notebook --no-browser --port=4567</code>.
   	1. If you ran this command on a new screen from step 1, return to your original screen with <code>Ctrl-A</code> followed by <code>Ctrl-D</code>.
5. Setup an ssh tunnel from your client machine (laptop). In terminal, type <code>ssh -N -L 4567:localhost:4567 [username]@[ip address]</code>. Replace <code>[username]</code> with your username and <code>[ip address]</code> with the ip address of the remote Linux host you are connecting to.
6. Type in your password. If it succeeds, the comman will stay running in your terminal with no output. When you are ready to end the ssh tunnel, press <code>Ctrl+C</code> or just close the terminal window.
7. Go to your jupyter notebook by opening a browser and going to URL <code>localhost:4567</code>. On the first connection, it will prompt you for a password. Provide the one you setup with <code>jupyter notebook password</code> in the Install Packages section.

## Checkout the NeuroTheoryLab packages
1. <code>git clone NeuroTheoryUMD/NDNT.git</code>
2. <code>git clone NeuroTheoryUMD/NTdatasets.git</code>
