# Introduction to Bayesian statistics workshop

The workshop materials will be in python using a package called PyMC3. The workshop aims to build intuition for how Bayesian models work and then set out some practical examples of how Bayesian methods are used to a) fit distributions to data b) infer the correlation parameter and c) perform linear regression.

## Installation instructions
The rest of this README sets out installation instructions for the workshop materials.

You can install the software needed using the Anaconda python distribution. If you already have Anaconda installed then you can skip to the Virtual Environment section below.

### Python installation

There may be a version of python installed on your system already. However, it is unlikely that it will be up-to-date enough for the workshop software to run with that software.

To make sure that we are all using the same software we will download Anancona. Anaconda is a distribution of python – it has all the files needed to run python on your machine – and it also provides an environment manager called conda. conda is discussed further below.

If you have never downloaded Anaconda, you go to this page and download the python 3 version.

The anaconda installer may ask your permission to do various things such as appending to your .bashrc file during installation. You can agree to all the points it asks.

For mac/linux you need to open a new terminal window once Anaconda is installed.

If you are using windows you open the Anaconda prompt once the installation has finished (you can search for “Anaconda prompt” from the Start menu). All of the commands set out below occur in the terminal (mac/linux) or the Anaconda prompt (windows), rather than inside python.

To check that the installation has worked, enter in the terminal/Anaconda prompt
```
conda info
```
This will display some information about the version of conda that you are using. In this case conda is the command line utility that will allow you to manage the packages that are installed in your virtual environments. If you are interested, you can learn more about what conda does in this blog post.

### Virtual environment

It is good practice to create virtual environments on your machine. A virtual environment is like a ‘walled-off’ installation of a program such as python. Using a virtual environment lets you play around with different software set-ups on the same computer. For example, you might have one virtual environment that holds the set-up for one project that you started a couple of years ago with older versions of packages. When you start a new project you can create a new virtual environment with more recent version of packages without disturbing the older project. You can then switch between these environments with a single command.

For this workshop, we will create a virtual environment called bayes. This virtual environment will have the packages that we need for the workshop installed.

You can create this bayes environment and install the necessary packages using
conda by running the following command in the terminal (mac/linux) or the Anaconda prompt (windows):

```
conda create -n bayes python=3.6.1 ipython jupyter scipy pymc3 pandas scikit-learn xarray holoviews bokeh seaborn
```
Answer yes to any questions the installer asks.

This command:

1) creates an environment called bayes

2) sets python 3.6.1 as the python version

3) installs the packages listed from ipython:seaborn.

You can then ‘activate’ (switch-to) this virtual environment from the terminal in mac/linux with the command:
```
source activate bayes
```
or in windows from the Anaconda prompt
```
activate bayes
```
You should see bayes now appearing at the start of the command prompt.

You can deactivate your environment and return to your root environment with the command:
```
source deactivate bayes
```
or in windows:
```
deactivate bayes
```
### Ipython kernel for the Jupyter notebooks

We will be using interactive jupyter notebooks in the workshop. Notebooks allow you to run code and view plots in your web browser. To use the notebooks you need to make sure that the notebook knows about the python installation that you created above in the bayes virtual environment.
You can make sure the notebooks knows about the bayes environment with the command
```
python -m ipykernel install --user --name bayes --display-name "bayes"
```
Potential issue for mac/linux:

After running the command above in mac/linux you may get a long error message that ends with a line that is similar to the following:

ModuleNotFoundError: No module named '_sysconfigdata_x86_64
This error arises because a recent version of conda has included some files that think you want to set up a compiler for the C and C++ languages in this environment. As we don’t want to set up these compilers in this environment, we need to delete these files from the installation.

To address this error on a macbook you can use the spotlight search (the magnifying glass in the top right) to look for a folder called activate.d. Go to the activate.d folder and make sure that it is in your bayes environment - the directory path should be something like /envs/bayes/etc/conda/activate. Delete the two files :that begin activate_clang and activate_clangxx.
Once you have deleted these files, go up one level in the directory tree and you will find another sub-directory called deactivate. Delete the two corresponding deactivate files in this directory.
You may need to open a new terminal, activate the bayes environment and then try running the python -m ipykernel... command above again.

On a linux laptop you need to find the same files. They are in a sub-directory of your anaconda installation. If you installed anaconda in your home directory, then the files would be in ~/anaconda3/envs/bayes/etc/conda/activate and you can then follow the macbook instructions above.

### Test the installation (all users)

You can test whether the installation has worked by opening a jupyter notebook.
In the terminal (mac/linux) or the Anaconda prompt (windows) enter:
```
jupyter notebook
```
A notebook should then open in your web browser. Click the ‘new’ button on the top right and check that bayes is listed as an option amongst the kernels. A kernel in this context means an installation of python on your machine such as the installation in the bayes environment. If bayes does not appear amongst the list of kernels, then open a new terminal and try running the ipython kernel creation command again. If that fails then let me know.

Finally, to make sure everything is installed correctly, run the test notebook. You can download the test notebook by navigating to this page in your web browser.

Click ctrl + s somewhere on the page and save the file as _00_installation_check.ipynb. Remove any .txt extension from the file name.

Navigate to the directory where you saved this .ipynb file from your terminal.

You then open a jupyter notebook with the command
```
jupyter notebook
```
Open the file: _00_installation_check.ipynb.

Follow the instructions to see if the model fits and the plot appears at the end. It might take a couple of minutes to run everything. You can tell if the code is running because to the right of every cell you see

In [*]
The * means that the code is running. If you see:

In [6]
–where the 6 could be any number – it means that the code has run successfully.

If you see:

In []
with nothing in the square brackets, it means that an error has occurred. In this case scroll back up to the top to find the error message. Some possible errors and corrections to them are set out below.

### Potential issues with the installation test
When doing the above set-up in January 2018 a number of errors occured for some users.  Hopefully these errors will be corrected in future versions of the packages, but you may encounter them.  Workarounds are set out here.

You may get an error after the first code cell that says something like:

Module not found error

ModuleNotFoundError: No module named xarray
Alternatively, it may be pymc3 or holoviews that is not found. This error message means that the package did not install correctly when we created the virtual environment. To address this:

1) close down the notebook in your browser and in the terminal

2) make sure that you have activated the bayes environment in your terminal/Anaconda prompt

3) run pip install where is the module that was not found in the notebook

4) open a new terminal window

5) open a new jupyter notebook from the terminal

try to run _00_installation_check.ipynb again.
Theano error

An alternative issue that might arise leads to a very long error message after the first code block that ends with something like:

RuntimeError: To use MKL 2018 with Theano you MUST set "MKL_THREADING_LAYER=GNU" in your environement.
This error can be addressed by adding the following line to the first cell block of the notebook (with the second line added in to show where it goes)
```
%env MKL_THREADING_LAYER=GNU
import numpy as np
```
Contact me at braaannigan@gmail.com if there are any problems.