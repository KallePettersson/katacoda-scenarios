## Creating the MakeFile
Now for the final part of the implementation of the C++ project lets create the makefile. First lets define some variables to make writing the makefile more straight forward. You can use the `Copy to Editor` button or write it yourself by clicking: `devops-executable-tutorial/src/makefile`{{open}}.
 
<pre class="file" data-filename="devops-executable-tutorial/src/makefile" data-target="replace">
CC = g++
flags = -std=c++11
 
# Compile complex
</pre>
 
Now lets add two rules to our makefile. The first rule will compile our Complex implementation into an object file that can be linked in to any other C++ file that includes our header file and uses our Complex class. The second rule is just for cleaning up. In a make file you can reference any variable created using the `$(<name>)` syntax and to run a given rule you simply type `make complex` in the terminal.
 
<pre class="file" data-filename="devops-executable-tutorial/src/makefile" data-target="insert" data-marker='# Compile complex'>
# Compile complex
complex: complex.cpp
$(CC) $(flags) -c complex.cpp -o complex.o
 
clear:
rm -f *.out *.o
 
 
# Future test rule
</pre>
 
 
Now the makefile is completed and should look something like this. We will add one more rule to compile the tests in a later step of this tutorial.
 
<pre class="file" data-filename="devops-executable-tutorial/src/makefile" data-target="replace">
CC = g++
flags = -std=c++11
 
# Compile complex
complex: complex.cpp
$(CC) $(flags) -c complex.cpp -o complex.o
 
clear:
rm -f *.out *.o
 
 
# Future test rule
 
</pre>
 

 
<!-- ## Optional
In order to test out the implementations you've created thus far you could create a main.cpp file and add the following code.
<pre class="file" data-filename="devops-executable-tutorial/src/main.cpp" data-target="replace">
#include "complex.h"
using namespace std;
 
int main(){
   //Your code goes here
 
   return 0;
}
</pre>
Now you can create `Complex` objects and play around with the code you've created. Then you can add the following rule to the makefile for compiling your code:
 
<pre class="file" data-filename="devops-executable-tutorial/src/makefile" data-target="insert" data-marker='# main rule(optional)'>
# main rule(optional)
main: main.cpp complex.o
$(CC) $(flags) main.cpp -o main.out complex.o
</pre>
 
 
Finally you can execute your code by running `make main && ./main.out`{{execute}} -->
 
**Note:** In the makefile, every line of code where a rule should execute needs to start with a tab. For this tutorial this needs to be done manually for every rule added. For instance the line `$(CC) $(flags) -c complex.cpp -o complex.o` needs to be tabbed in. **This can not be done in the UI** and is easiest done in the end of this step by using vim. In the terminal type `vim makefile`{{execute}} when vim has opened press `i` to start editing the file(Tab in each rule). This is done correctly when the rule is highlighted purple. When you are done tabbing in all the rules you can save the file and exit vim by first pressing the `esc` button, then type `:wq` and press `enter`. Editing the file in vim desyncs the makeifle in the UI, the best solution for avoiding issues with this is to close the makefile in the UI after its been edited in vim.(Sorry for the inconvenience, this seems to be caused by a katacode error in interpreting tabs correctly for makefiles)

The rules are tabbed in correctly when the file looks something like this in vim:
![correct makefile file](https://github.com/KallePettersson/katacoda-scenarios/blob/main/repeat-executable-tutorial/assets/correct-makefile.JPG?raw=true)

