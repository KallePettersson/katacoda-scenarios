# Installing CxxTest
As mentioned in the introduction we will be using the `CxxTest` framework for creating our tests so before we start with this tutorial we need to install it.
We can do this by first running `apt-get update -y` to update our default dependencies. After this command finishes run:
`apt-get install -y cxxtest`
to install `CxxTest`. This can be done by clicking on the following commands or by writing them manually in the terminal.<br/>
`apt-get update -y`{{execute}} <br/>
`apt-get install -y cxxtest`{{execute}}
 
# Cloning the tutorial repo
Now that we've installed `CxxTest` we need to clone the tutorial repo we will work with during this tutorial this can be done by executing the following command:<br/>
`git clone -b tutorial-start https://github.com/KallePettersson/devops-executable-tutorial.git`{{execute}}<br/>
After the repo has been cloned we can move into the repo using:<br/>
`cd devops-executable-tutorial/src`{{execute}}