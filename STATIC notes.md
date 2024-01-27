Static in c++;
  # 1. static keyword in variable:
  1. c++ static variables maintian their values till their end of the program<br>
  2. A static variable is allocated memory only once during the complete program during its initialization.<br>
  3. All static variables are stored in a part of the virtual memory, called the data segment, unlike other variables that are allocated memory in the stack.<br>
  4. Suppose the static variable is initialized with a value. In that case, it is stored in the initialized data segment, and in case it is uninitialized, it is given a default value of 0. It is stored in the uninitialized data   segment, also called BSS (Block Started by Symbol).<br>
  5. This allocated memory remains until the program ends, even if the function where the static variable was declared terminates.<br>
  6. When declared in a function, static variables are not deallocated even if the function terminates. They stay in the memory until the program finishes executing.<br>
  7. These are used in co routines in c++(for asynchronous programming )<br>
  8. When an object declaration is prepended with a static specifier, it means the storage for a static object is allocated when the program starts and deallocated when the program ends.<br>
  8. Java doesn’t allow static local variables in functions.<br>
  ### Static Array ###
  9.An array that is declared with the static keyword is known as static array. It allocates memory at compile-time whose size is fixed. We cannot alter the static array.<br>
  10.If we want an array to be sized based on input from the user, then we cannot use static arrays. In such a case, dynamic arrays allow us to specify the size of an array at run-time.<br>
  ```
int arr[] = { 1, 3, 4 }; // static integer array  
int* arr = new int[3]; // dynamic integer array 
  ```
  
```
#include <bits/stdc++.h>
using namespace std;

// Function to increment a variable.
int increment() {

    // Declare a static variable.
    static int temp = 0;

    temp++;

    return temp;
}

int main() {

    // Run a loop and call the increment function.
    for (int i = 0; i < 4; i++) {
        cout << increment() << endl;
    }

    return 0;
}

```
output:
```
1
2
3
4

```
# 2. C++ Static Variables in a Class
When variables that are members of a class are declared static, they are again allocated space only once throughout the program and deallocated only once the program ends.<br>
But as these variables are the member function of the class but declared as static, their copies cannot be made. This means that these variables have to be shared among the objects of the class.<br>
This is why static variables of a class can't be initialized using a constructor. Instead, they have to be initialized outside the class explicitly using the scope resolution operator like class_name::variable_name = value.<br>
We can define static class member fields. Static class members are not part of the object. They live independently of an object of a class. We declare a static data member inside the class and define it outside the class only once:<br>

```#include <bits/stdc++.h>
using namespace std;

// Class about car
class Car {

    public:

        // Member variables
        string model;
    static int no_of_tyres;

    // Constructor
    Car(string in ) {
        model = in;
    };

};

// Explicitly declare the value of the static member function.
// For a car, the number of tires is always 4.
int Car::no_of_tyres = 4;

int main() {

    // Create two objects of class Car.
    Car regular = Car("regular");
    Car premium = Car("premium");

    cout << "Before:" << endl;

    // Access the no_of_tyres variable for both objects.
    cout << regular.no_of_tyres << " " << premium.no_of_tyres << endl;

    // Change the value of the static variable.
    Car::no_of_tyres = 2;

    // It changes for both objects.
    cout << "After:" << endl;

    // Access the no_of_tyres variable for both objects.
    cout << regular.no_of_tyres << " " << premium.no_of_tyres << endl;

    return 0;
}

```
```
Before:
4 4
After:
2 2

```
# Static class objects
Like static variables in C++, static class objects in C++ are no different. So, static class objects are allocated memory only once during the program and deallocated after the completion of the program.<br>
Hence, even if the scope of wherever the object was declared ends, it remains in memory as it has been declared static. Like static variables, you can repeatedly use these objects with their previous value<br>
When is the destructor called?<br>

A destructor function is called automatically when the object goes out of scope:<br>

the function ends <br> the function ends still because of static object it remains 
the program ends <br>
a block containing local variables ends <br>
a delete operator is called  <br>
```
#include <bits/stdc++.h>
using namespace std;

class Things {

    int var;

    public:

        Things() {
            var = 0;
            cout << "Inside constructor" << endl;
        }

        ~Things() {
            cout << "Inside destructor" << endl;
        }

};

// Function to create a static object of class Things.
void createThing() {

    // Create a static object.
    static Things thing;
}

int main() {

    cout << "Start of program" << endl;

    // Create a static object inside the function.
    createThing();

    cout << "End of program" << endl;

    return 0;
}
```
```
Start of program
Inside constructor
End of program
Inside destructor

```

# C++ Static Functions in a Class
Like static variables, these static member functions can be called without any object using the class name and the scope resolution operator as class_name::function_name().<br>
But this is not the only way to call the function. We can call them using class objects using the . operator. <br>
**A very important thing to note is that these static member functions can only call static member variables and other static member functions, but not the other variables or functions.** <br>
```
#include <bits/stdc++.h>

using namespace std;

class Things {

    int var;

    public:

        Things() {
            var = 0;
        }

    // Static member function
    static void printHello() {
        cout << "Hello" << endl;
    }

};

int main() {

    // Create an object.
    Things thing1;

    // Call static function using . operator.
    thing1.printHello();

    // Call the static function using the :: operator.
    Things::printHello();

    return 0;
}
```
To define a static member function, we prepend the function declaration with the static keyword. The function definition outside the class does not use the static keyword:<br>
```
#include <iostream>
class MyClass
{
public:
    static void myfunction(); // declare a static member function
};
// define a static member function
void MyClass::myfunction()
{
    std::cout << "Hello World from a static member function.";
}
int main() {
    MyClass::myfunction(); // call a static member function
}
```
# this is example of static case
unctions declared static are not given global visibility <br>
The use of static in this context does not affect the behavior of the function itself, but rather it specifies that the function should only be visible within the same source file where it is declared.<br>
If this function is defined in a header file and included in multiple source files, each source file will have its own separate copy of the print function.<br>
In this example, the print function is declared as static, but in this context, it doesn't change the behavior of the function. It simply indicates that the function is intended for use only within the same translation unit.
```
#include <iostream>

// Standalone static function with internal linkage
static void print(const auto &c) {
    for (auto i : c) {
        std::cout << i << ", ";
    }
    std::cout << '\n';
}

int main() {
    // Example usage of the print function
    int arr[] = {1, 2, 3, 4, 5};
    print(arr);

    return 0;
}

```

