# `Object Oriented Programming CPP`

Sir Mohsin Ansari  
[Lecture-10-end Container Classes](https://www.youtube.com/watch?v=qpcpjy7G5yw&list=PL0OILbU3zRoDJo6H9WS1vEfBzlEZQKJD1&index=12)

---

## `Table of Contents`

1. [Bag_Class](#bag_class)
2. [Heap_Memory](#heap_memory)
3. [Operator_Overloading](#operator_overloading)

---

## `Bag_Class`

### `Bag Operations`

- A bag can put in it's **initial state**, which is an **empty bag**.
- Number can be **inserted** into the bag.
- We may **count** how many occurrence of a certain number are in the bag.
- Numbers can be **erased** from the bag.
- We can check the **size** of the bag.
- We can **remove** a number from a bag. But we remove only one number at a time.

**Why need pointers for pag?**  
If the size of your bag is not known at compile time or if it changes dynamically during program execution, using pointers allows you to allocate memory on the heap using new. This can be useful when you want to manage memory more flexibly.  
Pointers can be assigned a null value (nullptr), allowing us to represent the absence of an object in the bag.

Bag class is nothing, It's a just manipulation of an array.

### `Heap_Memory`

Heap memory, often referred to simply as the "heap," is a region of a computer's memory that is used for dynamic memory allocation. Unlike the stack, which is used for function call management and local variables, the heap is a more flexible area of memory that can be used to allocate memory at runtime. The heap allows programs to allocate memory for variables whose size is not known until the program is running or for data structures like arrays and linked lists.

---

In bag class we just store an array of integers. In that array we can insert, delete, update values/integers.  
*Simply declaring a function is called **prototyping**.*
**One big advantage of OOP is that we can easily convert our requirements into code, without much thinking about it's implementation, we only focus on prototyping not on it's implementations. While in normal way of programming we must have to implement as well with prototyping one by one.**  
If we have not initialized an array, and we want to retrieve then it'll give us a garbage values.

```C++
#include <iostream>
using namespace std;

class bag{
  private:
    int data[20];
    int used;   // it tells how much our array is used. so if here 0 stored then we are at 0 index. array is empty.
    // instead of initializing data array itself. we just initialize the used variable. It tells us about array.


  public:
    // constructor
    bag(){
      used = 0;
    } 

    bool insert(int value){
      if(used==20){
        return 0;
      }else{
        data[used]=value;
        used++;
        return 1;
      }
    }

    int bagSize(){
      return used;
    }

    void clear(){
      used = 0;
    }

    bool checkValInBag(int value){
      if(used == 0){
        cout<< "Not found As bag is empty.";
        return 0;
      }else{
        for(int i=0;i<used;i++){
          if(value==data[i]){
            cout <<value << " Has been found at index " << i << endl;
            return 1;
          }
        }
        cout<< "Not found.";
        return 0;  
      }
    }

    // Occurrences of a specified number in array.
    int howMany(int value){
      if (used == 0){
        cout<<"Bag is empty."
        return 0;
      }
      int count = 0;
      for(int i=0;i<used;i++){
        if(value == data[i]){
          count++;
        }
      }
      return count;
    }

    // To remove first swap with last element and then next--
    bool remove(int value){
      if(used == 0){
        cout << "bag empty";
        return 0;
      }

      for (int i = 0; i < used; i++){
        if (data[i] == value){
          data[i] = data[used - 1];
          used--;
          return 1;
        }
      }
      return 0;
    }

    bool removeDuplicate(int value){
       if(used == 0){
        cout << "bag empty";
        return 0;
      }

      for (int i = 0; i < used; i++){
        if (data[i] == value){

          if(data[used-1]==value){
            used--;
            i--;
          }else{
          data[i] = data[used - 1];
          used--;
          }
        }
      }
      return 1;
    }

  /* 
    bool checkDuplicate();
  */

    void display() {
      if(used == 0){
        cout << "Bag is empty" << endl;
      } else {
         for(int i = 0; i < used; i++){
          cout << data[i] << endl;
         }
      }
    }
}

int main(){

  bag b;

  if(b.insert(4)){
    cout << "Data successfully Inserted" << endl;
  }else{
    cout << "Bag is full" << endl;
  }



  return 0;
}

```

**During execution/run time we have no way of increasing or decrementing the size of any static array.** So here comes pointers and dynamic memory. **Pointer is all about memory location and memory management.**  
We'll convert this static bag into a dynamic bag with the help of pointer.

---

### `Operator_Overloading`

let's say we want to add(combine) two bag objects, basically we want merge two bags. We will combine the two bag objects and store the result in third bag. **bag b3=b+b2;** Here compiler error. because it will expect integers before and after addition operator. Because of we haven't, yet overloaded any operator.  
Now to add two bags, compiler shouldn't use the default + operator, Instead we'll built our own addition operator.

The compiler will convert this statement **b3=b+b;** into **b.operator+(b)** So here b is a calling object and b is a parameter object into operator+ function. As we know **we can access attributes of calling object directly in a functions of class** just like we did. And to access b we will pass as a parameter.

```  c++

class bag{
  private:
    int data[20];
    int used;  


  public:
  // All above functions...


  // Operator overloads
  bag operator+(bag b1){

    if(used + b1.used >= 20){ // here used is for calling used of object
    cout << "Addition is not possible" <<endl;
    }else{

    bag b3;
      for(int i=0; i<used; i++){
        // b3[i]=data[i];
        b3.insert(data[i]);
      }
      for(int i=0; i<b1.used;i++){
        b3.insert(b1.data[i]);
      }

    }
    return b3;
  }

}


bag b;

b.insert(2);
b.insert(3);
b.insert(6);
b.insert(20);
b.insert(1);
b.display();


bag b2;
b2.insert(4);
b2.insert(1);
b2.insert(5);
b2.insert(2);
b2.insert(9);
b2.display();

cout << "After Combining: ";
bag b3 = b + b2; // For now Error // before overloading
// b.operator+(b2)  // converted to this


```

---

## `Pointer`

Now we want this bag to be dynamic. Bag should have a dynamic memory size. It should not full unless our system memory(RAM) not full. We also want if we remove some elements from this bag, so in array, then the reserved memory should also remove. Till now it's not possible, because this memory for bag is reserving by the compiler, which we called **static memory**. So we move to the **pointers** and **dynamic memory**.

**Limitations of our static bag class:**

- **Capacity is constant.** Every bag object will have a fixed capacity.
- **Wasteful if too big memory** is reserved, and **hard to reuse if too small** memory is reserved.
- To increase or decrease in size we need to **change in source code and recompile.** There no option to change the size during run time.

**Solution:**  

- Provide control over size in running time.
- **Dynamic Arrays**.
- **Pointers** and **Dynamic Memory**.

---

### `Concepts with Dynamic Memory`

1. Pointers
2. Static Memory VS Heap Memory
3. Shallow copy VS Deep copy
    1. Copy Constructor
    2. Assignment Operator Overload
    3. Destructor

---

### `Static Memory Vs Heap Memory`

**Static Memory:** Static Memory are those memory spaces that reserved by a compiler itself.  
**Heap Memory:** Heap Memory is a memory space where user defined memory are stored.

### `Shallow Copy VS Deep Copy`

There are two ways to copy values from one object to another.

1. using assignment operator, this process is called assignment operator.

    ```c++
    bag b;
    bag b2=b;
    ```

2. Passing an object into another object, The process of copying object value into another object with passing it as a parameter is called **copy constructor.**

    ```c++
    bag b;
    bag b2(b);
    ```

These both are not implemented in our code. We've not implemented assignment operator overloads nor we have one argument constructor, so we have not any constructor that have one argument, and data type that argument is object.

If we execute first one it's working correctly. So by default compiler will make a constructor with one argument, that constructor is called copy constructor. That constructor is working correctly.

Now if we execute second one, Again it's working correctly. This is working because if we do b2=b; then the compiler will put all the codes/data that are inside the memory location of b into b2, because b and b2 are simile type, and will occupy same memory space. compiler will not check for data in each block of memory. Copy constructor also doing the same. **This concept is called a Shallow copy**  
This copy is called shallow because here the data copying shallowly. Reason for that is it's not comparing the data deep inside of each memory block.

Let's Understand with simple example

```c++
int a = 10;
int c = a;
char b = a; // Type Miss match Error. Memory space for both int and char are not same.

```

Here⤴ compiler will take make a memory space according to the data type of c and then it'll copy the data from the memory location of a and paste it into the memory location of c. so a & b will be 10;

***`Attributes of any class will always takes different spaces for different objects. But functions will take common space for different objects. And during execution time the function will bound to the calling object.`***

**So to deep copy we use Pointer.** If our class contains some pointers then the shallow copy will not work correctly.
