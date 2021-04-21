<!-- Creating a simple C++ project -->
In this tutorial we will start of by creating a simple C++ project. We will create a small version of a class modeling **Complex** numbers `2+3i` and some functions that will allow us to perform simple operations such as addition and subtraction with complex numbers. If you already know C++ or just want to learn how to use CxxTest and integrate Travis CI you can just copy the full files from the bottom of each of the following sections into it's corresponding file and continue to the next step.



## Creating the header file
We will start off by creating the header file for our **Complex** class. CD into the `src` folder and open the file in vim using `vim complex.h` when vim has opened press `i` to start editing the file. 

<!-- Include guards -->
Start of by adding include guards to the header file. This will prevent the compiler form including multiple version of this header file when compiling, avoiding duplicate definitions. Use this [link](https://en.wikipedia.org/wiki/Include_guard) to learn more about include guards and why they are important.
```c++
#ifndef COMPLEX_H

#endif
```

<!-- Outer class definiton -->
Now lets define our class, between the guards from the previous section add the following code: 
```c++
class Complex {
private:
    double _real;
    double _img;
public:

};
```
Here we define a class called **Complex** which has two private variables, `_real` and `_img` which will hold the real and imaginary parts of a complex number.

<!-- Constructors -->
Now lets define a few constructors so that we can initialize instances of our Complex class approprietly. Add the following code under the `public:` section in the code, this is because we want the constructors to have public access so that other objects may create **Complex** instances. These constructors uses initializer lists in order to initialize the private variables, use this [link](https://en.cppreference.com/w/cpp/language/constructor) if you want to learn more about them.
```c++
    Complex(): _real(0),_img(0){}
    Complex(double real): _real(real), _img(0){}
    Complex (double real, double img): _real(real), _img(img) {}
```

<!-- Member functions -->
Lets add some member functions to our class. Again add them in the public scope of the class. 
```c++
    double & real();
    double & img();
    Complex& operator=(const Complex& comp);
```
In the header file we only declare the function header, the actual implementation of these function will be created in the `Complex.cpp` file. The first two functions are getters that will return the different parts of a complex number. The last function is a special type of function that overloads the internal `=` operator when it is used with complex numbers. Use this [link](https://www.tutorialspoint.com/cplusplus/cpp_overloading.htm) if you want to learn more about operator overloading. 

<!-- Friendly functions -->
Finally we will add the decleration of a some friendly functions. In C++ we can use the keyword `friend` to give a non-member function access to private variables, this is very usefull when we want to overload operators such as `+` and `-`. Again these declerations should be added in the public scope of the class.

```c++
    friend Complex operator+(const Complex& lhs, const Complex& rhs);
    friend Complex operator-(const Complex& lhs, const Complex& rhs);
    friend Complex abs(const Complex& src);
    friend std::ostream& operator<<(std::ostream& ostream, const Complex& complex);
```

<!-- Final look of header file -->
Now the header file is completeed and it should look something like this:
```c++
#ifndef COMPLEX_H
class Complex {
private:
  double _real;
  double _img;
public:

  // <----------------------- Constructors --------------------------->
  Complex(): _real(0),_img(0){}
  Complex(double real): _real(real), _img(0){}
  Complex (double real, double img): _real(real), _img(img) {}

  
  // <--------------------- member functions ------------------------->
  double & real();
  double & img();
  Complex& operator=(const Complex& comp);

  // <-------------------- friendly functions ------------------------>
  friend Complex operator+(const Complex& lhs, const Complex& rhs);
  friend Complex operator-(const Complex& lhs, const Complex& rhs);
  friend Complex abs(const Complex& src);
  friend std::ostream& operator<<(std::ostream& ostream, const Complex& complex);

};

#endif
```

You can save the file and exit vim by first pressing the `esc` button, then type `:wq` and press `enter`.

## Writing the implementation file
Now lets write the code for all the functions we just created. Open the implementation file in vim using `vim complex.cpp` when vim has opened press `i` to start editing the file. The first thing we need to add to the implementation file is the header file, this is done using the `#include <file>` command which tells the compiler at compile time to copy and paste the content of the `<file>` into the file where `#include <file>` was used. The iostream has an abs function defined in it that we will use later. So add the following code to the top of the `Complex.cpp` file.

```c++
#include "complex.h"
#include "iostream"
```

Lets start by defining our member functions. Lets start with the `Complex& operator=(const Complex& comp)` function. Add the following code snippet:
````c++
Complex& Complex::operator= (Complex const& src) {
  this->_real = src._real;
  this->_img = src._img;
  return *this;
}
````
The `Complex&` part species that this function will return a Complex **by reference** which means that this function will return an actual object and not a copy of an object. The `Complex::operator=` tells the compiler the we want to overload the `=`operator in the `Complex` scope and the `Complex const& src` means that we pass the argument by reference and we also promise that the content of the src variable will remain the same after executing the function. When we want to use the function we can for instance write `Complex a = Complex(2,3)`, this is then converted into `a.operator=(Complex(2,3))` which means that we copy the content of the Complex object we pass via the source parameter into the private varaibles of `a`. 

Now lets define the getter functions:
````c++
double & Complex::real(){
  return _real;
}

double & Complex::img(){
  return _img;
}
````
The functions are pretty simple and just returns private variables. Note that they are returned by reference which means that the private variables could be changed directly like this:
````c++
...
Complex a = Complex(2,3);
a.real() = 4; // this changes the real part from 2 to 4
...
````


Now finally lets define our firendly non-member functions:
````c++
Complex operator+(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real + rhs._real,lhs._img + rhs._img);
}


Complex operator-(const Complex& lhs, const Complex& rhs){
  return Complex(lhs._real - rhs._real,lhs._img - rhs._img);
}


Complex abs(const Complex& src){
  return Complex(abs((long long)src._real),abs((long long)src._img));
}
````
There are different ways of overloading these operators but doing it this way will allow us to chain multiple uses of the operator. `Complex a = b + c + d +... `. When we execute do this each the compiler will interperte it as `a = ((b + c) + d)` and since the operator+ return a new complex object the chainging is possible. In the `abs` function we use the built in abs function to convert each variable seperatly and create a new Complex object which we then return.


Now the implementation file is completeed and it should look something like this:
````c++
#include "complex.h"
#include "iostream"

// <=========================== Member functions =============================================>

// Override =
Complex& Complex::operator= (Complex const& src) {
  this->_real = src._real;
  this->_img = src._img;
  return *this;
}

double & Complex::real(){
  return _real;
}

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

````
You can save the file and exit vim by first pressing the `esc` button, then type `:wq` and press `enter`.

## Creating the MakeFile 
Now for the final part of the implementation of the C++ project lets create the make file. Open the make file in vim using `vim makefile` when vim has opened press `i` to start editing the file. First lets define some varaibles to make writing the makefile more straight forward.
````makefile
CC = g++
flags = -std=c++11
````

Now lets add two rules to our makefile. The first rule will compile our Complex implementation into an object file that can be linked in to any other C++ that includes our header file and uses our Complex class. The second rule is just for cleaning up. In a make file you can reference any variable created using the `$(<name>)` syntax and to run a given rule you simply type `make complex` in the terminal.
````makefile
complex: complex.cpp
	$(CC) $(flags) -c complex.cpp -o complex.o

clear: 
	rm -f *.out *.o
````


Now the make file is completed and it should look something like this. We will add one more rule to compile the tests in the next step of this tutorial.
````makefile
CC = g++
flags = -std=c++11

complex: complex.cpp
	$(CC) $(flags) -c complex.cpp -o complex.o

clear: 
	rm -f *.out *.o 
````
You can save the file and exit vim by first pressing the `esc` button, then type `:wq` and press `enter`.


## Optional
In order to test out the implementations you could create a main.cpp file and add the following code:
````c++
#include <iostream>
#include "complex.h"
using namespace std;

int main(){
    //Your code goes here

    return 0;
}
````

And then add the following rule to the makefile:
````
main: main.cpp complex.o
	$(CC) $(std) main.cpp -o main.out complex.o
````