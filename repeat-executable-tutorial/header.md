<!-- Creating a simple C++ project -->
We will start of by creating a simple C++ project. We will create a small version of a class modeling **Complex** numbers i.e. `2+3i` and some functions that will allow us to perform simple operations such as addition and subtraction with them.
 
If you already know C++ or just want to learn how to use CxxTest and integrate Travis CI you can just copy the full files from the bottom of each of the following sections into its corresponding file and continue to the next step.
 
 
## Creating the header file
We will start off by creating the header file for our **Complex** class.
 
<!-- Include guards -->
Start of by adding include guards to the header file. This will prevent the compiler from including multiple version of this header file when compiling, avoiding duplicate definitions. Use this [link](https://en.wikipedia.org/wiki/Include_guard) to learn more about include guards and why they are important. Press `Copy to Editor` to add the following to `Complex.h`. If you prefer writing the code yourself you can open the file directly and edit it yourself by clicking this: `devops-executable-tutorial/src/complex.h`{{open}}
 
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="replace">
#ifndef COMPLEX_H
// Outer class def:
 
#endif
</pre>
 
<!-- Outer class definition -->
Now lets define our class, between the guards from the previous section add the following code:
 
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="insert" data-marker='// Outer class def:'>
 
class Complex {
private:
   double _real;
   double _img;
public:
 // Constructors here:
};
 
</pre>
 
Here we define a class called **Complex** which has two private variables, `_real` and `_img` which will hold the real and imaginary parts of a complex number.
 
<!-- Constructors -->
Now let’s define a few constructors so that we can initialize instances of our Complex class appropriately. Add the following code under the `public:` section in the code, this is because we want the constructors to have public access so that other objects may create **Complex** instances. These constructors uses initializer lists in order to initialize the private variables, use this [link](https://en.cppreference.com/w/cpp/language/constructor) if you want to learn more about them.
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="insert" data-marker='// Constructors here:'>
// <----------------------- Constructors --------------------------->
   Complex(): _real(0),_img(0){}
   Complex(double real): _real(real), _img(0){}
   Complex (double real, double img): _real(real), _img(img) {}
 
   // Member functions here:
</pre>
 
 
<!-- Member functions -->
Lets add some member functions to our class. Again add them in the public scope of the class.
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="insert" data-marker='// Member functions here:'>
// <--------------------- member functions ------------------------->
   double & real();
   double & img();
   Complex& operator=(const Complex& comp);
 
   // Friendly functions here:
  
</pre>
 
In the header file we only declare the function header, the actual implementation of these function will be created in the `Complex.cpp` file. The first two functions are getters that will return the different parts of a complex number. The last function is a special type of function that overloads the internal `=` operator when it is used with complex numbers. Use this [link](https://www.tutorialspoint.com/cplusplus/cpp_overloading.htm) if you want to learn more about operator overloading.
 
<!-- Friendly functions -->
Finally we will add the declaration of a some friendly functions. In C++ we can use the keyword `friend` to give a non-member function access to private variables, this is very useful when we want to overload operators such as `+` and `-`. Again these declarations should be added in the public scope of the class.
 
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="insert" data-marker='// Friendly functions here:'>
// <-------------------- friendly functions ------------------------>
   friend Complex operator+(const Complex& lhs, const Complex& rhs);
   friend Complex operator-(const Complex& lhs, const Complex& rhs);
   friend Complex abs(const Complex& src);
  
</pre>
 
 
<!-- Final look of header file -->
Now the header file is completed and it should look something like this:
 
<pre class="file" data-filename="devops-executable-tutorial/src/complex.h" data-target="replace">
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
 
};
 
#endif
</pre>
 
Now that we are finished with the header file lets continue with the implementation file!
 

