# Windows - Setting up your Dev Environment

In this document, we're going to condense how you should setup your machine in preparation for the rest of the tutorials contained in this document. Running OpenMined means having several different applications and repositories correctly installed and ready to work together, which can have unique challenges for each system. To that end, let's get your PC up and running!!!

# Step 1: Install Unity

The longest part of the process is downloading the Unity3d video game engine (because it's a rather large file). Proceed to the [Unity3d Download Page](https://store.unity.com/download?ref=personal) to download the Installer. While you wait for the download, you can continue with the other steps in this tutorial.

A few quick tips:

* You only need the Free version in order to use OpenMined
* Unity will start with your internet turned off, but if you have your internet turned on but are simply attached to a bad connection, sometimes Unity will hang. Just turn off your Wifi and restart Unity if you have this issue.

# Step 2: Install Jupyter Notebook

I'll admit, this part can be annoying if you don't use the right tools. For Windows, I've found that anaconda is the best installation tool for jupyter notbook. (READ: don't use pip...pip is unreliable for installing jupyter notebook. Sometimes it works, sometimes it totally screws up your system). 

#### Part 1: Install Anaconda
First, navigate to the [Windows Anaconda Download Page](https://www.anaconda.com/download/#windows) and click "Download" for the Python 3.6 version.

#### Part 2: Install Jupyter Notebook

If you installed Anaconda, you have already installed jupyter notebook! If you did not, you'll need to use [these instructions](http://jupyter.readthedocs.io/en/latest/install.html) as a backup.

# Step 3: Clone & Build Relevant Repositories

Start by creating a general directory for your OpenMined projects. In that directory, run the following commands. 

#### Part 1: Fork & Clone

At this point if you're planning on contributing back to the project its best to fork the repo on Github. Navigate to [OpenMined Repo](https://github.com/OpenMined/OpenMined.git) and click the Fork button. Repeat the same process for the [PySyft Repo](https://github.com/OpenMined/PySyft).

Now clone! This can be completed in Git bash if you have that installed or where ever you have Git installed. Here's how to clone from Git bash. You might also need to set up public/private keys to clone in this way. See tutorial [here](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows).

> git clone git@github.com:**YOUR-GITHUB-USERNAME-HERE**/OpenMined.git
 
> git clone git@github.com:**YOUR-GITHUB-USERNAME-HERE**/PySyft.git

#### Part 2: Build

From here I'd recommend using the Anaconda commandline. Might not be the best interface but I found it the easiest way to get access to python and Anaconda commandline tools without to much fuss!

TODO: image to Anaconda commandline

> cd PySyft

> ./install_for_anaconda_windows.bat TODO: what is the actual way to run this?

> python3 setup.py install

> cd ../

If you have any trouble with the installation of PySyft, debug using the [README](https://github.com/OpenMined/PySyft).

# Step 4: Start Jupyter Notebook

From your general directory (containing both your OpenMined and PySyft folders), run the following command.

>jupyter notebook

This should start the jupyer notebook server and automatically open your browser to the main jupyter notebook folder.

# Step 5: Start OpenMined Unity Application

#### Part 1: Start Unity Application

Find where Unity installed and start the application.

#### Part 2: Select OpenMined/UnityProject

Unity will ask you which project you want to open. You want to select the folder "UnityProject" within the [https://github.com/OpenMined/OpenMined](https://github.com/OpenMined/OpenMined) project. 

![](../resources/images/OpenUnityProject.png) TODO image from windows

#### Part 3: Double-click Assets/OpenMinedMain

In the project pane, in the "Assets" folder, double click the unity scene (little file with the unity logo next to it) called "OpenMinedMain".

![](../resources/images/SelectUnityScene.png) TODO image from windows

#### Part 4: Make sure SyftServer is properly attached to the FloatTensorShaders file.

In the `Hierarchy` pane, click the `Main Camera`. 

![](../resources/images/HierarchyMainCamera.png) TODO image from windows

Then, in the `Inspector` pane (towards the bottom), you should see a `Syft Server (script)` inside of which is a textarea labeled `Shader`. The contents of this text area should say `FloatTensorShaders` like pictured below.

![](../resources/images/CameraInspector.png) TODO image from windows

If you don't see `Syft Server Script` in the inspector pane, drag the file Assets/OpenMined/Network/Servers/SyftServer and drop it into the inspector as pictured below.

![](../resources/images/DragSyftServer.png) TODO image from windows

If you DO see the `Syft Server Script` but `FloatTensorShaders` is NOT in the `Shader` area (if area will is grayed out and say `None (ComputeShader)`. Drag the file Assets/OpenMined/Syft/Tensor/Ops/Shaders/FloatTensorShaders into that text area like seen below.

![](../resources/images/DragShader.png) TODO image from windows

#### Part 5: Press Play!!!

At the top of the Unity application there's a Play button. Press it! This will start the OpenMined server and you'll be ready to start doing some tutorials!!

![](../resources/images/UnityPlayButton.png) TODO image from windows
