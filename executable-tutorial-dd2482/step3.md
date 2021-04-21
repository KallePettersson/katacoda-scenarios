 <!--Writing and running CxxTest  -->
Now that we have finnished the C++ project step we will in this step use CxxTest to write to test our **Complex** implementation. 

## Creating our tests
We will start off by creating the test file where we will define our tests. Open the file in vim using `vim complexTests.cpp` when vim has opened press `i` to start editing the file. 

First we need to include the two relevant headerfiles at the top of our file. The first header file allows us to use CxxTest to define our tests and the second one allows us to work with our **Complex** class.

````c++
#include <cxxtest/TestSuite.h>
#include "complex.h"
````

Now lets define the test suite class which will contain our tests. The class we create will extend the testsuite built into CxxTest and any public void function where the name starts with "test" defined within it will be executed as a unit test later when we run our tests.

````c++
class MyTestSuite : public CxxTest::TestSuite {
    public:
    // Tests here
};
````

Now lets add some tests! There is not much to mention about the tests, other then that some of them uses the built in `TS_ASSERT_EQUALS` to assert equality on standard types such as doubles while some use a helper function we've created called `ASSERT_COMPLEX_EQUALS` to asserty equality between two complex numbers.
````c++
    void ASSERT_COMPLEX_EQUALS(Complex a, Complex b){
        double TOL = 1e-10;
        TS_ASSERT_EQUALS(abs(a.real()-b.real())<TOL,1);
        TS_ASSERT_EQUALS(abs(a.img()-b.img())<TOL,1);
    }

    void testDefaultConstructor () { 
        Complex a;
        TS_ASSERT_EQUALS(a.real(), 0);
        TS_ASSERT_EQUALS(a.img(), 0);
    }

    void testOneParamConstructor () { 
        Complex a(1);
        TS_ASSERT_EQUALS(a.real(), 1);
        TS_ASSERT_EQUALS(a.img(), 0);
    }

    void testTwoParamConstructor(){
        Complex a(2,3);
        TS_ASSERT_EQUALS(a.real(), 2);
        TS_ASSERT_EQUALS(a.img(), 3);
    }

    void testGetters(){
        Complex a(2,3);
        TS_ASSERT_EQUALS(2,a.real());
        TS_ASSERT_EQUALS(3,a.img());
    }

    void testassignmentEqual(){
        Complex a(2,3);
        Complex b = a;

        TS_ASSERT_EQUALS(b.real(), 2);
        TS_ASSERT_EQUALS(b.img(), 3);
    }


    void testBinaryPlus (){
        Complex a(1,1);
        Complex b(2,2);
        Complex c(3,3);

        Complex d = a + b;

        ASSERT_COMPLEX_EQUALS(c,d);
    }

    void testBinaryMinus (){
        Complex a(1,1);
        Complex b(2,2);
        Complex c(3,3);

        Complex d = c - a;

        ASSERT_COMPLEX_EQUALS(b,d);
    }
    
    void testAbs (){
        Complex a = abs(Complex(1,1));
        Complex b = abs(Complex(-2,2));
        Complex c = abs(Complex(-3,-3));
        Complex d = abs(Complex(0,0));

        Complex a_res(1,1);
        Complex b_res(2,2);
        Complex c_res(3,3);
        Complex d_res(0,0);

        ASSERT_COMPLEX_EQUALS(a,a_res);
        ASSERT_COMPLEX_EQUALS(b,b_res);
        ASSERT_COMPLEX_EQUALS(c,c_res);
        ASSERT_COMPLEX_EQUALS(d,d_res);
    }
````

Now the test file is completed and it should look something like this:
````c++
#include <cxxtest/TestSuite.h>
#include "complex.h"


class MyTestSuite : public CxxTest::TestSuite {
  public:
    void ASSERT_COMPLEX_EQUALS(Complex a, Complex b){
        double TOL = 1e-10;
        TS_ASSERT_EQUALS(abs(a.real()-b.real())<TOL,1);
        TS_ASSERT_EQUALS(abs(a.img()-b.img())<TOL,1);
    }

    void testDefaultConstructor () { 
        Complex a;
        TS_ASSERT_EQUALS(a.real(), 0);
        TS_ASSERT_EQUALS(a.img(), 0);
    }

    void testOneParamConstructor () { 
        Complex a(1);
        TS_ASSERT_EQUALS(a.real(), 1);
        TS_ASSERT_EQUALS(a.img(), 0);
    }

    void testTwoParamConstructor(){
        Complex a(2,3);
        TS_ASSERT_EQUALS(a.real(), 2);
        TS_ASSERT_EQUALS(a.img(), 3);
    }

    void testGetters(){
        Complex a(2,3);
        TS_ASSERT_EQUALS(2,a.real());
        TS_ASSERT_EQUALS(3,a.img());
    }

    void testassignmentEqual(){
        Complex a(2,3);
        Complex b = a;

        TS_ASSERT_EQUALS(b.real(), 2);
        TS_ASSERT_EQUALS(b.img(), 3);
    }


    void testBinaryPlus (){
        Complex a(1,1);
        Complex b(2,2);
        Complex c(3,3);

        Complex d = a + b;

        ASSERT_COMPLEX_EQUALS(c,d);
    }

    void testBinaryMinus (){
        Complex a(1,1);
        Complex b(2,2);
        Complex c(3,3);

        Complex d = c - a;

        ASSERT_COMPLEX_EQUALS(b,d);
    }
    
    void testAbs (){
        Complex a = abs(Complex(1,1));
        Complex b = abs(Complex(-2,2));
        Complex c = abs(Complex(-3,-3));
        Complex d = abs(Complex(0,0));

        Complex a_res(1,1);
        Complex b_res(2,2);
        Complex c_res(3,3);
        Complex d_res(0,0);

        ASSERT_COMPLEX_EQUALS(a,a_res);
        ASSERT_COMPLEX_EQUALS(b,b_res);
        ASSERT_COMPLEX_EQUALS(c,c_res);
        ASSERT_COMPLEX_EQUALS(d,d_res);
    }    

};
````
You can save the file and exit vim by first pressing the `esc` button, then type `:wq` and press `enter`.

## Compiling and running tests
Now that we've defined our tests we need to compile them into an executable file using cxxtestgen so that we can execute our tests and run them. We do this by adding a new rule to our make file. 
````makefile
tests: complex.cpp complexTests.cpp
	cxxtestgen --error-printer -o testrunner.cpp complexTests.cpp
	$(CC) $(flags) -c complex.cpp -o complex.o
	$(CC) $(flags) -o simple_test.out -I cxxtest/ \testrunner.cpp complex.o
````
The rules looks daunting at first glance but lets break it down. The first row uses cxxtestgen to compile our testsuite into **runner** file. The runner file is a `.cpp` file and is automatically generated by CxxTest. The next line is just the same line of code we use in our previously defined `complex` rule, it simply compiles our implementation code into an object file that the linker can use in the next line. In the final line we compile our testrunner into an executable file called `simple_test.out`. When we compile the runner we also have to include our object file `complex.o` so that the linker can link the executable code in `complex.o` to all out uses of the Complex class in the testsuite.


## Running the tests 
To run the tests you simply have to execute the `simple_test.out` file! This can be done be entering `./simple_test.out` into the terminal. 