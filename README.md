# `Object Oriented Programming CPP`

Sir Mohsin Ansari  
[Lecture-10 Container Classes](https://www.youtube.com/watch?v=qpcpjy7G5yw&list=PL0OILbU3zRoDJo6H9WS1vEfBzlEZQKJD1&index=12)

---

## `Bag Operations`

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

## `Heap_Memory`

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

  /*
    int howMany(int value);
    bool remove(int value);
    bool checkDuplicate();
    bool removeDuplicate();
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
