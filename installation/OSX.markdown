# OSX - Setting up your Dev Environment
-
In this document, we're going to condense how you should setup your machine in preparation for the rest of the tutorials contained in this document. Running OpenMined means having several different applications and repositories correctly installed and ready to work together, which can have unique challenges for each system. To that end, let's get your Mac up and running!!!

# Step 1: Install Unity

The longest part of the process is downloading the Unity3d video game engine (because it's a rather large file). Proceed to the [Unity3d Download Page](https://store.unity.com/download?ref=personal) to download the Installer. While you wait for the download, you can continue with the other steps in this tutorial.

A few quick tips:

* You only need the Free version in order to use OpenMined
* Unity will start with your internet turned off, but if you have your internet turned on but are simply attached to a bad connection, sometimes Unity will hang. Just turn off your Wifi and restart Unity if you have this issue.

# Step 2: Install Jupyter Notebook

I'll admit, this part can be annoying if you don't use the right tools. For OSX, I've found that anaconda is the best installation tool for jupyter notbook. (READ: don't use pip...pip is unreliable for installing jupyter notebook. Sometimes it works, sometimes it totally screws up your system). 

#### Part 1: Install Anaconda
First, navigate to the [OSX Anaconda Download Page](https://www.anaconda.com/download/#macos) and click "Download" for the Python 3.6 version.

#### Part 2: Change to Python 3.5
At the time of writing, PySyft is built against Python 3.5, so we'll want to change over to 3.5 even though anaconda downloads with 3.6 by default. Fortunately, anaconda includes a [Tutorial on how to do this](https://conda.io/docs/user-guide/tasks/manage-python.html).

>conda create -n py35 python=3.5 anaconda

>source activate py35

Now, when you run the following command, it should tell you "3.5"
>python --version


# Step 3: Clone & Build Relevant Repositories

Start by creating a general directory for your OpenMined projects. In that directory, run the following commands. 

#### Part 1: Check that python 3.5 is activated
>python --version

#### Part 2: If needed, activate python 3.5
If you don't currently have python 3.5 activated, run the following command

>source activate py35

#### Part 3: Install and Build

> git clone https://github.com/OpenMined/OpenMined.git
 
> git clone https://github.com/OpenMined/PySyft

> cd PySyft

> pip3 install -r requirements.txt

> python3 setup.py install

If you have any trouble with the installation of PySyft, debug using the [README](https://github.com/OpenMined/PySyft).


