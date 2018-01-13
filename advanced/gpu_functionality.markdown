# Adding Functions to the GPU

In this tutorial, we're going to walk through the basics of how to work with the OpenMined community to write GPU code in the OpenMined ecosystem. Specifically, we're going to implement a new function in the IntTensor class. Step 1 is to go to PySyft's Github Issues page and look for a good project.

## Step 1: Find an Issue on Github

The issues for our IntTensor live in the Python client, PySyft. So, we're going to navigate to the [PySyft Repository](https://github.com/OpenMined/PySyft) and click the [Issues](https://github.com/OpenMined/PySyft/issues) tab, showing a page that (at the time of writing) looks like this.

![](../resources/images/PySyftIssuesUnsorted.png)

Now, we're specifically interested in looking for issues requiring GPU functionality, so we're going to click the `Labels` dropdown and click the `needs GPU` label to filter the big list of issues down to ones requiring GPU functionality. At the time of writing, that looks like the following.

![](../resources/images/NeedsGpu.png)

Let's click the top issue and read a bit.

![](../resources/images/IssueConvoTop.png)

Looks like someone has already gotten started on this issue but no-one has started workinig on the GPU functionality yet. In fact, the last guy to comment was the person who added the "needs GPU" label, which means he's probably not working on that. However, before jumping in, I should check to make sure and offer to help, so that we don't accidentally implement the same thing (this happens!)

![](../resources/images/IssueConvoBottom.png)

And we're in business!!! (in that conversation my username is "iamtrask"). 
<<<<<<< HEAD

## Step 2: Pull Down Gavin's Code Branch

So, in order to collaborate with @gavinuhma on this issue, I first need to know what branch he's working on. Since this issue doesn't yet have any pointers to a branch, I need to ask.

![](../resources/images/IssueConvoBranch.png)

Fortunately, his code was later merged into master.

![](../resources/images/Merged.png)

As you can see in the image above, Gavin's change modified code in two repositories: PySyft and OpenMined. So, all we need to do is pull from Master. 

From our local PySyft repository directory we run:

> git checkout master

> git pull

From our local OpenMined repository directory we run:

> git checkout master

> git pull

## Step 3: Locate Unit Test and Functionality

Fortunately, in the previous tutorial, Gavin [created a unit test](https://github.com/OpenMined/OpenMined/pull/319/files#diff-23257f4aaa85d138d55abd8e757b1761) for our GPU code that looks like this.

![](../resources/images/GpuAddUnitTest.png)

Our goal will be to make this test pass (at present it does not). Also, as requested, [Gavin made an if statement](https://github.com/OpenMined/OpenMined/pull/319/files#diff-56b88e118fd31ef74df498c393cce4e9) and (NotImplementException) flag where he would like for us to put our GPU code.

![](../resources/images/GpuNotImplemented.png)

So, now we know where we need to write our code, and what we want it to do. Let's get started!

## Step 4: Write our GPU Kernel.

Taking inspiration from [similar functionality in FloatTensor](https://github.com/OpenMined/OpenMined/blob/master/UnityProject/Assets/OpenMined/Syft/Tensor/Ops/Shaders/FloatTensorShaders.compute)...

![](../resources/images/AddElemFloat.png)

We can create a similar kernel for Elementwise Addition of integers by changing the types from float to int and renaming varaibles. Thus, our resulting Kernel looks like this.

![](../resources/images/AddElemInt.png)

## Step 5: Execute our GPU Kernel

So, in the code location Gavin specified, we added the following code to run our kernel with the correct parameters.

![](../resources/images/RunIntKernel.png)

The green commends indicate what each line does. 

## Step 6: Run our Unit Test

![](../resources/images/UnitTestPasses.png)

We did it! Now, along the way we actually ignored many of the conventions setout in FloatTensor for handling GPU code. This is because in the process we identified a bug and implemented a simplified version of this kernel as a workaround. Thus, we've commented inline in the code with "TODOs" and in a minute we need to mention them back in the main issue.

## Step 7: Commit our Code
From our OpenMined/OpenMined repository, run:

> git commit -am "added elementwise addition gpu functionality with a small workaround for a newly discovered bug"

> git checkout -b add_elem_gpu

> git push --set-upstream origin add_elem_gpu

## Step 8: Create a Pull Request
Now that you have created and pushed a new branch, if you navigate to the [main repository page](https://github.com/OpenMined/OpenMined), you'll see the following button. Click it! 
![](../resources/images/CompareAndPull.png)

Add relevant details [like so](https://github.com/OpenMined/OpenMined/pull/322)

## Step 9: Followup in Issue

Especially since we discovered bugs, we need to inform other participants of their existance and our temporary workaround which I've done on the [original issue](https://github.com/OpenMined/PySyft/issues/755).

![](../resources/images/Workaround.png)

## Step 10: Party! We're done!

Great job!
=======
>>>>>>> 65ec240bd71f433efb519a6f37e498d983d7c644
