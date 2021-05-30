<!-- Continuous Integration with Travis CI -->
Now that we can both build our project by running `make complex` and test our project using `make tests && ./simple_test.out` locally. Now we want to integrate Travis CI into our project so that every time we make changes to our code the project will be built and tested. 
 
## Creating and enabling a Travis CI account
Before we integrate Travis CI into our project we need to create an account and give that account access to our repository. Travis CI works by connecting itself to the repo via a webhook. A webhook that will be triggered every time something is pushed to the repo, thus triggering the `.travis.yaml` file and building and testing our project. **Note** that this step is not needed for this tutorial, since Travis is already connected to the repo but if you want to connect your own repos to Travis the following step is needed.
 
To create an account go to Travis home [page](https://www.travis-ci.com) and click on `sign up`. This will direct you to a sign up page where you can choose how to sign up for Travis, here you want to choose `sign up with github`. This will take you to a GitHub page where you have to log in to GitHub and verify that you want to sign up for Travis CI. Now you can either give Travis access to all you repos by clicking `Activate all repositories` button or you could go back to Travis and click on your profile picture in the top right of your Travis Dashboard, click Settings and then the green Activate button, and select the repositories you want to use with Travis CI. If there are any issues with this sign up guide here is a link to the official [one](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci-using-github). 
 
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
If you want to try and trigger a build you can commit your changes and push them to GitHub. When you try and run `git push` you will be asked to setup your identity, follow the instructions in the output and set the `user.email` and `user.name` appropriately. Then when you run `git push` again you will have to specify the username and password of your personal GitHub account in order to push to the repo. After pushing the changes you can visit the [repo](https://github.com/KallePettersson/devops-executable-tutorial/tree/tutorial-start) in the browser and watch as Travis builds and tests the project.
 
 
# Easter egg
Before we end this tutorial, did you find the Ester egg? If not you can view it by executing this command!
`cat /root/devops-executable-tutorial/.start/39/38/37/11/24/18/35/26/10/easteregg.txt`{{execute}}
 

