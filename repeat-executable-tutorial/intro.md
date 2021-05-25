Continous integration or CI is the practice of smoothly and automatically integrating source code and features in your project from multiple contributors into a single project repository. For CI to work properly there is a need make sure that all the code merged into our central repo is correct. To acheive this we use automated testing and building. 

In this tutorial we will look at how we implement a CI workflow for a simple C++ projects. We will do this by using the test library `CxxTest` and the CI platform `Travis CI` to create tests in integrate an automated testing pipline. In the process we will learn some fundamentals about C++ programming, how unit tests are written in `CxxTest` and how we can create a CI pipeline with `Travis CI`.

# Tutorial outline
1. Background
2. Before you start
3. Creating a simple C++ project
4. What is CxxTest?
5. Writing CxxTests
6. Running CxxTests
7. What is Travis CI?
8. Continous Integration with Travis CI

# Usefull links for leraning more
Through out the tutorial we will use Vim to edit the files, here is a usefull link for how Vim works: [Vim 101](https://www.linux.com/training-tutorials/vim-101-beginners-guide-vim/)
Documentation about how to build and test C++ projects in Travis CI: [Building a C++ Project](https://docs.travis-ci.com/user/languages/cpp/)
CxxTest official documentation: [CxxTest User Guide](http://cxxtest.com/guide.html)
CxxTest documentation and tutorial from DD1388 course: [cxxtest a unit test framwork](https://gits-15.sys.kth.se/DD1388/labblydelser/blob/master/2021/lab_01.md#cxxtest-a-unit-test-framework)


