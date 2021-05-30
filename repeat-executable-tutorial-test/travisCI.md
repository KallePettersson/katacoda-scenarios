<!-- Continuous Integration with Travis CI -->
Now that we can both build our project by running `make complex` and test our project using `make tests && ./simple_test.out` locally. Now we want to integrate Travis CI into our project so that every time we make changes to our code the project will be built and tested. 
 
## Creating and enabling a Travis CI account
Before we integrate Travis CI into our project we need to create an account and give that account access to our repository.
 
To create an account go to Travis home [page](https://www.travis-ci.com) and click on `sign up`. This will direct you to a sign up page where you can choose how to sign up for Travis, here you want to choose `sign up with github`. This will take you to a GitHub page where you have to log in to GitHub and verify that you want to sign up for Travis CI. Now you can either give Travis access to all you repos by clicking `Activate all repositories` button or you could go back to Travis and click on your profile picture in the top right of your Travis Dashboard, click Settings and then the green Activate button, and select the repositories you want to use with Travis CI. If there are any issues with this, here is a link to the official [get started guide](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci-using-github). 
 
## Connect repo to Travis CI
Now that we've created a Travis account that is connected to our repo lets create the `.travis.yaml` config file that tells Travis what to do when the webhook is triggered. You can use the `Copy to Editor` button or write it yourself by clicking: `devops-executable-tutorial/.travis.yml`{{open}}.
 
 
First lets set up our environment where we will build and test our project.
<pre class="file" data-filename="devops-executable-tutorial/.travis.yml" data-target="replace">
dist: trusty
sudo: false
language: cpp
 
# Commands here:
</pre>
 
The `dist:trusty` tell Travis that we want to run everything in an up to date ubuntu environment, the `sudo: false` tell Travis that we don't need sudo privileges in our shell and the `language: cpp` tells Travis that we have a cpp project.
 
Now let’s create the script that will run each time Travis is triggered. This will execute like a shell script that first installs CxxTest, moves to the source folder, builds the project and finally tests it. The script uses our previously defined make rules to both build our project and compile and run our tests.
 
<pre class="file" data-filename="devops-executable-tutorial/.travis.yml" data-target="insert" data-marker='# Commands here:'>
# Commands here:
script:
 - echo "Installing cxxtest"
 - sudo apt-get install -y cxxtest
 - echo "Moving to src directory"
 - cd src
 - echo "Building project (Compile object file)"
 - make complex
 - echo "Running tests"
 - make tests
 - ./simple_test.out
</pre>
 
 
Now the yaml file is completed and it should look something like this:
<pre class="file" data-filename="devops-executable-tutorial/.travis.yml" data-target="replace">
dist: trusty
sudo: false
language: cpp
 
# Commands here:
script:
 - echo "Installing cxxtest"
 - sudo apt-get install -y cxxtest
 - echo "Moving to src directory"
 - cd src
 - echo "Building project (Compile object file)"
 - make complex
 - echo "Running tests"
 - make tests
 - ./simple_test.out
</pre>
 
## Triggering builds and tests
To trigger the building and testing we simply have to push our changes to our forked repo on GitHub and Travis CI will be triggered automatically!
First we can add all our changes to our commit by running: <br/>
`git add *`{{execute}} <br/>

Then we can commit our changes by running: <br/>
`git commit -am"Done with the tutorial!"`{{execute}}<br/>

**Note:** Commiting from the terminal will trigger an git error where git wants to know who you are and you need to provide your email and name. 
![Git Error](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/Github-error.JPG?raw=true)
You can copy and paste this in your terminal to fix this(remember to put in your email and name).
`git config --global user.email "you@example.com"`{{copy}}<br/>
`git config --global user.name "Your Name"`{{copy}}<br/>

Now you can rerun the commit command above. And finally we can push our changes by running:<br/>
`git push`{{execute}}<br/>

Now go to the fork in your browser and change branch to `tutorial-start` and see how travis is building. It should look like this:
![Github travis running](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/github-travis-running.JPG?raw=true)

When Travis is done building and testing the project it will look something like this:
![github travis details](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/github-travis-details.JPG?raw=true)


You can also view the build directly in your dashboard at Travis or you can get a more detailed view in github by clicking the checkmark and then clicking `Details` and it will take you to a view that looks something like this:
![Github travis details view](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/github-travis-details-viwe.JPG?raw=true)
![Travis CI dashboard](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/travis-dashboard.JPG?raw=true)
 
 
# Easter egg
Before we end this tutorial, did you find the Ester egg? If you did'nt you can view it by executing this command!
`cat /root/devops-executable-tutorial/.start/39/38/37/11/24/18/35/26/10/easteregg.txt`{{execute}}
 

