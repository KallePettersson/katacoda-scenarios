
![Travis CI logo](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/th.jpeg?raw=true)
<br/>
Travis CI is a continuous integration platform that supports the development process by automatically building and testing code changes and providing immidiate feedback on their success. Travis CI can also automate other parts of your development process by managing deployments and notifications.

When you run a build, Travis CI clones your GitHub repository into a brand-new virtual environment, and carries out a series of tasks to build and test your code. Travis CI uses webhooks to recieve information about events taking place in the repo. The developer can define which task should run and on which events they should run. For instance the developer could define some tasks that run on every push event to the repo and some other tasks that run when a PullRequest is created to a specific branch. If one or more of those tasks fail, the build is considered broken. If none of the tasks fail, the build is considered passed and Travis CI can deploy your code to a web server or application host. The image below shows the Travis CI dashboard connected to the repo for this tutorial.
![Travis CI dashboard](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/travis-ci?raw=true)
<br/>


Travis CI also integrate seemlessly into the GitHub interface and gives the developer information about the building and testing done directly on the repo page. 
![Travis CI in Github](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/github-travis?raw=true)
<br/>




Usefull link if you want to learn more in depth about what Travis CI is and how it works [What is Travis CI](https://petercoding.com/devops/2019/10/08/what-is-travis-ci/), [Travis CI for Beginners](https://docs.travis-ci.com/user/for-beginners/).