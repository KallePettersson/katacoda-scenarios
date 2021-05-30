<!--Writing and running CxxTest  -->
Now that we have finished the C++ project step we will in this step use CxxTest to create unit tests for testing our **Complex** implementation. 

## Creating our tests
We will start off by creating the test file where we will define our tests. First we need to include the two relevant header files at the top of our file. The first header file allows us to use CxxTest to define our tests and the second one allows us to work with our **Complex** class. You can use the `Copy to Editor` button or write it yourself by clicking: `devops-executable-tutorial/src/complexTests.cpp`{{open}}

<pre class="file" data-filename="devops-executable-tutorial/src/complexTests.cpp" data-target="replace">
#include <cxxtest/TestSuite.h>
#include "complex.h"

// Test class
</pre>


Now lets define the test suite class which will contain our tests. The class we create will extend the test suite built into CxxTest and any public void function where the name starts with "test" defined within it will be executed as a unit test later when we run our tests.

<pre class="file" data-filename="devops-executable-tutorial/src/complexTests.cpp" data-target="insert" data-marker='// Test class'>
// Test class
class MyTestSuite : public CxxTest::TestSuite {
    public:
    // Tests here:
};
</pre>

Now let’s add some tests! There is not much to mention about the tests, other than that some of them uses the built in `TS_ASSERT_EQUALS` to assert equality on standard types such as doubles while some use a helper function we've created called `ASSERT_COMPLEX_EQUALS` to assert equality between two complex numbers.

<pre class="file" data-filename="devops-executable-tutorial/src/complexTests.cpp" data-target="insert" data-marker='// Tests here:'>
// Tests here:
    void ASSERT_COMPLEX_EQUALS(Complex a, Complex b){
        double TOL = 1e-10;
        TS_ASSERT_EQUALS(abs(a.real()-b.real()) < TOL,1);
        TS_ASSERT_EQUALS(abs(a.img()-b.img()) < TOL,1);
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
</pre>

Now the test file is completed and it should look something like this:
<pre class="file" data-filename="devops-executable-tutorial/src/complexTests.cpp" data-target="replace">
#include <cxxtest/TestSuite.h>
#include "complex.h"

// Test class
class MyTestSuite : public CxxTest::TestSuite {
  public:
  // Tests here:

    void ASSERT_COMPLEX_EQUALS(Complex a, Complex b){
        double TOL = 1e-10;
        TS_ASSERT_EQUALS(abs(a.real()-b.real()) < TOL,1);
        TS_ASSERT_EQUALS(abs(a.img()-b.img()) < TOL,1);
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
</pre>

Now lets continue by learning how we compile and run our test code locally!