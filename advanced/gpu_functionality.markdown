# Adding Functions to the GPU

In this tutorial, we're going to walk through the basics of how to write GPU code in the OpenMined ecosystem. Specifically, we're going to implement a new function on the IntTensor. Step 1 is to go to Github Issue and look for a good project.

## Step 1: Find an Issue on Github

The issues for our IntTensor live in the Python client, PySyft. So, we're going to navigate to the [PySyft Repository](https://github.com/OpenMined/PySyft) and click the [Issues](https://github.com/OpenMined/PySyft/issues) tab, showing a page that (at the time of writing) looks like this.

![](../resources/images/PySyftIssuesUnsorted.png)

Now, we're specifically interested in looking for issues requiring GPU functionality, so we're going to click the `Lables` dropdown and click the `needs GPU` label to filter the big list of issues down to ones requiring GPU functionality. At the time of writing, that looks like the following.

![](../resources/images/NeedsGpu.png)

Let's click the top issue and read a bit.

![](../resources/images/IssueConvoTop.png)

Looks like someone has already gotten started on this issue but no-one has started workinig on the GPU functionality yet. In fact, the last guy to comment was the person who added the "needs GPU" label, which means he's probably not working on that. However, before jumping in, I should check to make sure and offer to help.

![](../resources/images/IssueConvoBottom.png)

And we're in business!!! (in that conversation my username is "iamtrask"). 
