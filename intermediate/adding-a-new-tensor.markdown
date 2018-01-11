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

To keep this tutorial simple, and to provide a real world reference, we'll chose a method that has already been implemented: Inline Add.

If you just want to code:

* Original issue: https://github.com/OpenMined/PySyft/issues/414
* PySyft pull request (Python interface code): https://github.com/OpenMined/PySyft/pull/635
* OpenMined pull request (Unity CPU/GPU code): https://github.com/OpenMined/OpenMined/pull/63/files

## The Python interface

## The Unity Test

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined.Tests/Editor/FloatTensorTest.cs

## Syft Controller

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Network/Controllers/SyftController.cs

## GPU Code

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Math/Shaders/FloatTensorShaders.compute
https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Tensor/FloatTensor.ShaderOps.cs

## CPU Code

https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Tensor/FloatTensor.ShaderOps.cs
