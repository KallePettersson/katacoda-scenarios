# Installing CxxTest
As mentioned in the introduction we will be using the `CxxTest` framework for creating our tests so before we start with this tutorial we need to install it.
We can do this by first running `apt-get update -y` to update our default dependencies. After this command finishes run:
`apt-get install -y cxxtest`
to install `CxxTest`. This can be done by clicking on the following commands or by writing them manually in the terminal.<br/>
`apt-get update -y`{{execute}} <br/>
`apt-get install -y cxxtest`{{execute}}
 
# Forking the tutorial repo
Now that we've installed `CxxTest` we need to clone the tutorial repo we will work with during this tutorial. Start of by forking the repo. You fork the repo by clicking this [link](https://github.com/KallePettersson/devops-executable-tutorial/tree/main) and then pressing the button right under your profile picture saying "fork".

# Cloning the forked repo
After you've forked the repo you need to clone it. From you fork press `Code`, select `HTTPS` and copy the link.
Then run the following command in your terminal: <br/>
`git clone <your clone link here`
After the repo has been cloned we can move into the repo using:<br/>
`cd devops-executable-tutorial/src`{{execute}}<br/>
Finally we need to switch to the right branch:
`git checkout tutorial-start`{{execute}}<br/>
Great! Now we are ready to start the tutorial.