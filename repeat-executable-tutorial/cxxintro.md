CxxTest is a unit testing framework for C++ that is similar in
spirit to JUnit, CppUnit, and xUnit. CxxTest is easy to use because
it does not require precompiling a CxxTest testing library and it supports a
very flexible form of test discovery. The CxxTest framework is designed to be as portable as possible and does not requeire RTTI, Member template functions, Exception handling and External libraries. The frameowkr was originally created for C++ compilers on embedded systems, since they often lack support for the previously mentioned features.


Creating and running unit test using the CxxTest framework have a simple straightforwad workflow consisting of four steps:
1. Tests are defined in C++ header files
2. The cxxtestgen command processes header files to generate files for the test runner. 
3. Compile the test runner.
4. Execute the test runner to run all test suites.


Usefull link if you want to learn more in depth about what the CxxTest framework is and how it works [CxxTest User Guide](http://cxxtest.com/guide.pdf)