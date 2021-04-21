# Continous Integration with Travis CI
Now that we can both build our project by running `make complex` and test our project using `make tests && ./simple_test.out` locally we now want to integrate Travis CI into our project so that everytime we make changes to our code the project will be built and tested.  

## Creating and enabling a Travis CI account 
Before we integrate Travis CI into our project we need to create an acount and give that acount access to our repository. Travis CI works by connecting itself to the repo via a webhook. A webhook that will be triggered everytime something is pushed to the repo, thus triggering the `.travis.yaml` file and building and testing our project. **Note** that this step is not needed for this tutorial, since travis is already connected to the repo but if you want to connect your own repos to Travis the following step is needed.

To create an acount go to travis home [page](https://www.travis-ci.com) and click on `sign up`. This will direct you to a sign up page where you can choose how to sign up for Travis, here you want to choose `sign up with github`. This will take you to a github page where you have to log in to github and verify that you want to sign up for Travis CI. Now you can either give Travis access to all you repos by clicking `Activate all repositories` button or you could go back to travis and click on your profile picture in the top right of your Travis Dashboard, click Settings and then the green Activate button, and select the repositories you want to use with Travis CI. If there are any issues with this sign up guide here is a link to the official [one](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci-using-github).  

## Connect repo to Travis CI
Now that we've created a Travis account that is connected to our repo lets create the `.travis.yaml` config file that tells Travis what to do when the webhook is triggered. Open the config file in vim using `vim .travis.yaml` when vim has opened press `i` to start editing the file.

First lets set up our environment where we will build and test our project.

````yaml
dist: trusty
sudo: false
language: cpp
````
The `dist:trusty` tell travis that we want to run everything in an up to date ubuntu environment, the `sudo: false` tell travis that we don't need sudo priviliges in our shell and the `language: cpp` tells travis that we have a cpp project.


Now lets create the script that will run each time travis is triggered. This will execute like a shell script that first installs CxxTest, moves to the source folder, builds the project and finally tests it. The script uses our previously defined make rules to both build our project and compile our tests.

````yaml
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
````

## Triggering builds and tests
If you want to try and trigger a build you can commit your changes and push them to github. When you try and run `git push` you will be asked to setup your identity, follow the instructions in the output and set the `user.email` and `user.name` appropriatly. Then when you run `git push`again you will have to specify the username and password of you personal github account in order to push to the repo. After pushing the changes you can visit the [repo](https://github.com/KallePettersson/devops-executable-tutorial/tree/tutorial-start) in the browser and watch as travis builds and tests the project.