# Intermediate - Building the Guts of a Deep Learning Framework

Deep learning frameworks can be thought of as a set of mathematical operations. After laying the foundation for the OpenMined Python API, the bulk of the effort became implementing these operations, also known as `tensor methods`. This would normally be a long dev process. But the OpenMined community has enabled this development to scale incredibly well. Members of the community have been building these operations in parallel, and making tons of progress, but we're not done!

This tutorial will show where to find the operations that still need to be implemented. Once you have the OpenMined development environment setup, you can become an OpenMined contributor in less than an hour. This tutorial will explain everything. We look forward to adding you to the GitHub org!

# How OpenMined Tensors Work - The Magic Under the Hood

Tensor methods (link) are operations that we perform on a matrix. One of the goals of OpenMined, is to be as portable as possible. For this reason, we're building our backend in Unity. A data scientist can still develop their models in Python, their preferred language, but the computations are happening in Unity!

For performance reasons, we want to be able to run computations of the GPU. GPUs are really good at matrix math because of their large number of cores (link). For portability reasons, we also want to support CPU computations. This means when we add a new tensor method to OpenMined, we need to write the CPU and the GPU code.

A major benefit of the Unity platform is the ability to access GPUs across a wide range of platforms (link) - from Xbox, Mac OS X, to mobile platforms like iOS and Android. As a developer, this means writing tensor methods in a shader language called HLSL (link).

The CPU methods are written in C#, which is the main language of Unity.

Let's take a look at what happens when you call a tensor method from Python:

* Python sends a request to Unity over a socket connection.
* Unity checks for GPU compatibility on the current device.
* If a GPU is available, the operation is processed by HLSL.
* Otherwise, the operation is processed by C#.

# Add a feature to Float Tensors (Code!)

First we want to search GitHub for a "good first issue": https://github.com/OpenMined/PySyft/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22

This will give us a big list of tensor methods that haven't been implemented yet.

To keep this tutorial simple, and to provide a real world reference, we'll chose a method that has already been implemented: IntTensor Add.

If you just to see the finished code:

* Original issue: https://github.com/OpenMined/PySyft/issues/755
* PySyft pull request (Python interface code): _
* OpenMined pull request (Unity CPU/GPU code): _

## Forking PySyft

We need to implement the PySyft interface for our tensor method.

The PySyft repo is https://github.com/OpenMined/PySyft . If you're not already setup you can `git clone` and follow the local setup instructions on the readme:

```bash
git clone git@github.com:OpenMined/PySyft.git
```

You should fork the PySyft repo so that you can send a pull request later.

On the PySyft repo in GitHub, click the `Fork` button.

Now back in the terminal you can `git remote add` to add the url of your personal PySyft fork. Mine is https://github.com/gavinuhma/PySyft , so the terminal command looks like below. Just change `gavinuhma` to your github username. I like to give my remote forks the name `fork` (Seems fitting!)

```bash
git remote add fork git@github.com:gavinuhma/PySyft.git
```

To verify, you can list your remotes with `git remote`.

```bash
git remote
```

If you cloned PySyft a while ago, you can push to your fork to get it up to date with master.

```bash
git push fork master
```

## The PySyft interface (Python)

Since we're adding a method to `IntTensor`, the code for the interface is in the [PySyft](/OpenMined/PySyft) repo under [syft/tensor.py](/OpenMined/PySyft/blob/master/syft/tensor.py).

You'll notice the method is called `__add__`. This is a ["magic method"](https://www.python-course.eu/python3_magic_methods.php) that allows us to overload the `+` operator.

There was already an `__add__` method for the `FloatTensor` class. In this case, the only difference between the two classes are the `int` vs `float` values. So it's fairly easy for us to subclass the `IntTensor` and `FloatTensor` from a `BaseTensor` class.

Take a look at the pull request to see how this was done.

By moving `__add__` into `BaseTensor` we now have our PySyft interface implemented for the `IntTensor` class.

## The Unity Test (C#)

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined.Tests/Editor/FloatTensorTest.cs

## Syft Controller (C#)

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Network/Controllers/SyftController.cs

## GPU Code (HLSL)

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Math/Shaders/FloatTensorShaders.compute
https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Tensor/FloatTensor.ShaderOps.cs

## CPU Code (C#)

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Tensor/FloatTensor.ShaderOps.cs
