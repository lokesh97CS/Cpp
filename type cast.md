# Four different casts that are more explicit: #
1. static_cast<to_type>(expression)
2. dynamic_cast<to_type>(expression)
3. const_cast<to_type>(expression)
4. reinterpret_cast<to_type>(expression)

## static cast
1. static_cast is checked at compile time<br>
2. Static casting always converts the data type, using the best conversion function available. In the case of double to int, it will truncate the number and change its representation to be an integer.<br>
3. Using static_cast with pointers or references is dangerous: it will perform the compile-time type conversion whether it makes sense or not. This is equivalent to just reinterpreting the pointer, and is a bad idea.
4.  For pointers and references, use dynamic_cast.<br>
** Example use-cases: **
Convert from an integral type to an enumeration
Convert from a floating-point type to an integra
Convert from one pointer-type to another pointer
example1
```
int *p = static_cast<int*>(malloc(100 * size
malloc()returns a void*which needs to b
```
example2
```
static_cast<to_type>(expression)
Used to:
1) Convert pointers of related types
Base* b = static_cast<Base*>(new Derived); - compiler error if types aren't related


2) Non-pointer conversion
 int qt = static_cast<int>(3.14);// 3
```
example 3
```
int a=10, b=3;
float result =9.77;
int loki=result;//9 compiler truncates
cout<< "implicit"<<a/b<<endl;//3 compiler will do this treuncation
cout<< "explicit"<< (float)a/b<<endl;//
```
example 4
for static _cast to use, inheritance must in classes
```
class A{
public:
int x;
}
class B{
public:
int y;
}

class C: class B{
public:
int w;
}

void foo(){
B b; C c;
A*p = static_cast<A *>(&b);// compile error because A and B classes are not related to each other

B *q = static_cast<B *>(&c);// B and C are related in heritance

C *r = static_cast<C *>(&b);// parent to children , dont use , no cimpile error , but dangerous
```

example 5
int&& y = static_cast<int&&>(x);: Uses static_cast to convert x to an rvalue reference, and assigns it to y. This effectively "moves" the ownership of x's value to y.<br>
```
#include <iostream>

int main() {
    int x = 42;

    // Use static_cast to move ownership of x to y
    int&& y = static_cast<int&&>(x);

    std::cout << "x: " << x << std::endl;  // x has been "moved from", its value is unspecified
    std::cout << "y: " << y << std::endl;  // y now owns the original value of x

    return 0;
}

```
output
```
x: <unspecified>
y: 42

```
