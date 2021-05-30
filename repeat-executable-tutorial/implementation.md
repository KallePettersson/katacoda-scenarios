## Writing the implementation file
Now let’s write the code for all the functions we just created. The first thing we need to add to the implementation file is the header file, this is done using the `#include <file>` command which tells the compiler at compile time to copy and paste the content of the `<file>` into the file where `#include <file>` was used. The iostream has an abs function defined in it that we will use later. So add the following code to the top of the `Complex.cpp` file. You can use the `Copy to Editor` button or write it yourself by clicking: `devops-executable-tutorial/src/complex.cpp`{{open}}.


<pre class="file" data-filename="devops-executable-tutorial/src/complex.cpp" data-target="replace">
#include "complex.h"
// <=========================== Member functions =============================================>

// Override =

</pre>


Lets start by defining our member functions. Lets start with the `Complex& operator=(const Complex& comp)` function. Add the following code snippet:

<pre class="file" data-filename="devops-executable-tutorial/src/complex.cpp" data-target="insert" data-marker='// Override ='>
// Override =
Complex& Complex::operator= (Complex const& src) {
  this->_real = src._real;
  this->_img = src._img;
  return *this;
}

// Access real part
</pre>


The `Complex&` part species that this function will return a Complex **by reference** which means that this function will return an actual object and not a copy of an object. The `Complex::operator=` tells the compiler the we want to overload the `=`operator in the `Complex` scope and the `Complex const& src` means that we pass the argument by reference and we also promise that the content of the src variable will remain the same after executing the function. When we want to use the function we can for instance write `Complex a = Complex(2,3)`, this is then converted into `a.operator=(Complex(2,3))` which means that we copy the content of the Complex object we pass via the source parameter into the private variables of `a`. 

Now lets define the getter functions:

<pre class="file" data-filename="devops-executable-tutorial/src/complex.cpp" data-target="insert" data-marker='// Access real part'>
// Access real part
double & Complex::real(){
  return _real;
}

// Access imaginary part
double & Complex::img(){
  return _img;
}
// <===================================== Non-member functions ================================================>
</pre>


The functions are pretty simple and just returns private variables. Note that they are returned by reference which means that the private variables could be changed directly like this:
````c++
...
Complex a = Complex(2,3);
a.real() = 4; // this changes the real part from 2 to 4
...
````

Now finally lets define our friendly non-member functions:
<pre class="file" data-filename="devops-executable-tutorial/src/complex.cpp" data-target="insert" data-marker='// <===================================== Non-member functions ================================================>'>
// <===================================== Non-member functions ================================================>

// overload binary + operator 
Complex operator+(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real + rhs._real,lhs._img + rhs._img);
}

// overload binary - operator 
Complex operator-(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real - rhs._real,lhs._img - rhs._img);
}

// Uses the standard abs method which takes a long long as input
Complex abs(const Complex& src){
  return Complex(abs((long long)src._real),abs((long long)src._img));
}

</pre>


There are different ways of overloading these operators but doing it this way will allow us to chain multiple uses of the operator. `Complex a = b + c + d +... `. When we execute do this each the compiler will interpret it as `a = ((b + c) + d)` and since the operator+ return a new complex object the chaining is possible. In the `abs` function we use the built in abs function to convert each variable separately and create a new Complex object which we then return.

Now the implementation file is completed and it should look something like this:
<pre class="file" data-filename="devops-executable-tutorial/src/complex.cpp" data-target="replace" >
#include "complex.h"

// <=========================== Member functions =============================================>

// Override =
Complex& Complex::operator= (Complex const& src) {
  this->_real = src._real;
  this->_img = src._img;
  return *this;
}

// Access real part
double & Complex::real(){
  return _real;
}

// Access imaginary part
double & Complex::img(){
  return _img;
}

// <===================================== Non-member functions ================================================>

// overload binary + operator 
Complex operator+(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real + rhs._real,lhs._img + rhs._img);
}

// overload binary - operator 
Complex operator-(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real - rhs._real,lhs._img - rhs._img);
}

// Uses the standard abs method which takes a long long as input
Complex abs(const Complex& src){
  return Complex(abs((long long)src._real),abs((long long)src._img));
}
</pre>

Lets continue by creating a Makefile!
