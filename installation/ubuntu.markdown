# Linux - Setting up your Dev Environment

In this document, we're going to condense how you
should setup your machine in preparation for the rest
of the tutorials contained in this document. Running
OpenMined means having several different applications
and repositories correctly installed and ready to work
together, which can have unique challenges for each
system. To that end, let's get you set up and running!

# Step 1: Install Unity

The longest part of the process is downloading the Unity3d video game engine (because it's a rather large file). You can download an installer for linux [here](http://beta.unity3d.com/download/2ca68d182788/public_download.html).

Click on the `Linux Download Assistant` to download
the installer.  After the download is complete, make
it executable with `chmod +x UnitySetup-2017.3.0b1`.
Then, execute it with `./UnitySetup-2017.3.0b1`.  This
will open the installer.  Follow the instructions to
complete the unity installation.

A few quick tips:

* You only need the Free version in order to use OpenMined
* Unity will start with your internet turned off, but if you have your internet turned on but are simply attached to a bad connection, sometimes Unity will hang. Just turn off your Wifi and restart Unity if you have this issue.

# Step 2: Install Jupyter Notebook

I'll admit, this part can be annoying if you don't use
the right tools. For Linux, I've found that anaconda
is the best installation tool for jupyter notbook.
(READ: don't use pip...pip is unreliable for
installing jupyter notebook. Sometimes it works,
sometimes it totally screws up your system).

#### Part 1: Install Anaconda
First, navigate to the [Linux Anaconda Download Page](https://www.anaconda.com/download/#linux) and click "Download" for the Python 3.6 version.

Once you download the install script, use a terminal to make it executable and then run it.

```sh
chmod +x Anaconda3-5.0.1-Linux-x86_64.sh
./Anaconda3-5.0.1-Linux-x86_64.sh
```

Follow the instructions in the installer.
When asked if the installer should add the install location to your PATH, say yes.

Once the installer finishes.  Re-source your bashrc: `source ~/.bashrc`.

#### Part 2: Change to Python 3.6
At the time of writing, PySyft is built against Python 3.6, so we'll want to change over to 3.6 . Fortunately, anaconda includes a [Tutorial on how to do this](https://conda.io/docs/user-guide/tasks/manage-python.html).

First, see if you're already on 3.6
```
python --version
```

If it says 3.6, skip to Part 3!!
```
conda create -n py36 python=3.6 anaconda
```

```
source activate py36
```

Now, when you run the following command, it should tell you "3.6"
```
python --version
```

#### Part 3: Install Jupyter Notebook

If you installed Anaconda, you have already installed jupyter notebook! If you did not, you'll need to use [these instructions](http://jupyter.readthedocs.io/en/latest/install.html) as a backup.

# Step 3: Fork, Clone & Build Relevant Repositories

#### Part 0: If wanted, create an OpenMined directory (to hold all your OM projects)
Start by creating a general directory for your OpenMined projects. In that directory, run the following commands.
```
mkdir OpenMined
```

#### Part 1: Check that python 3.5 is activated
```
python --version
```

#### Part 2: If needed, activate python 3.5
If you don't currently have python 3.5 activated, run the following command
```
source activate py35
```

#### Part 3: Fork PySyft an OpenMined Repositories

- Go to the following link: [https://github.com/OpenMined/OpenMined](https://github.com/OpenMined/OpenMined)
- Click the "Fork" button at the top right corner.
![](../resources/images/fork.png)
- Go to the following link: [https://github.com/OpenMined/PySyft](https://github.com/OpenMined/PySyft)
- Clik the "Fork" button at the top right corner (yes this is a second time)

This will copy our repositories YOUR github account. Now, you want to clone those repositories to your OpenMined project directory that you created in Part 1.
```
git clone git@github.com:OpenMined/OpenMined.git
git clone https://github.com/<your github username>/PySyft.git
```

#### Part 4: Install and Build
```
cd PySyft
pip install -r requirements.txt
python setup.py install
cd ../
```

If you have any trouble with the installation of PySyft, debug using the [README](https://github.com/OpenMined/PySyft).

# Step 4: Start Jupyter Notebook

From your general directory (containing both your OpenMined and PySyft folders), run the following command.

```
jupyter notebook
```

This should start the jupyer notebook server and automatically open your browser to the main jupyter notebook folder.

# Step 5: Start OpenMined Unity Application

#### Part 1: Start Unity Application

Find where Unity installed and start the application.  
It should already be running if you haven't closed it
after the installer finished.

#### Part 2: Select OpenMined/UnityProject

Unity will ask you which project you want to open. You want to select the folder "UnityProject" within the [https://github.com/OpenMined/OpenMined](https://github.com/OpenMined/OpenMined) project.

![](../resources/images/OpenUnityProject.png)

#### Part 3: Double-click Assets/OpenMinedMain

In the project pane, in the "Assets" folder, double click the unity scene (little file with the unity logo next to it) called "OpenMinedMain".

![](../resources/images/SelectUnityScene.png)

#### Part 4: Make sure SyftServer is properly attached to the FloatTensorShaders file.

In the `Hierarchy` pane, click the `Main Camera`.

![](../resources/images/HierarchyMainCamera.png)

Then, in the `Inspector` pane (towards the bottom), you should see a `Syft Server (script)` inside of which is a textarea labeled `Shader`. The contents of this text area should say `FloatTensorShaders` like pictured below.

![](../resources/images/CameraInspector.png)

If you don't see `Syft Server Script` in the inspector pane, drag the file Assets/OpenMined/Network/Servers/SyftServer and drop it into the inspector as pictured below.

![](../resources/images/DragSyftServer.png)

If you DO see the `Syft Server Script` but `FloatTensorShaders` is NOT in the `Shader` area (if area will is grayed out and say `None (ComputeShader)`. Drag the file Assets/OpenMined/Syft/Tensor/Ops/Shaders/FloatTensorShaders into that text area like seen below.

![](../resources/images/DragShader.png)

#### Part 5: Press Play!!!

At the top of the Unity application there's a Play button. Press it! This will start the OpenMined server and you'll be ready to start doing some tutorials!!
![](../resources/images/UnityPlayButton.png)

#### Make sure everything is working!

If jupyter notebook is not running, start it with
`jupyter notebook`.  If you still have it running,
open the tree view by going to `localhost:8888/tree` in
your browser.  There are lots of notebooks in the
openmined repo that you can test. Navigate to
`openmined/notebooks` and then click `Syft Tensor Example Notebook`.

Inside the notebook, run the first two cells.  If they
execute properly, you are all set!

#### Getting help

If you have any trouble at any point.  Drop into our
[slack](https://openmined.slack.com/join/shared_invite/enQtMjU5MzE5ODk4MTc3LWI2ZGE1ODc1YjdkZDJiNjdmYTdkZmE4ZTY5N2NkNDgxZjUyNjgxMTVhMmJkOTZhZjEyZDA3MTM2MThkZWVhMjg) group and ask for help!  There are lots of people
always on line who are glad to help!
