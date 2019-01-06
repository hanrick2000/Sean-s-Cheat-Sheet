<extoc></extoc>

# Java Virtual Machine JVM

- **JDK** 
    - Java Development Kit
    - JDK contains the tools for developing Java programs running on JRE.
    - for example, it provides the compiler 'javac'
- **JRE** 
    - Java Runtime Environment
    - JRE is the JVM program
- **JVM**
    - ![HotSpot JVM: Architecture](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide1.png)
    - **Class Loader**
    - **Java Threads**
    - **Garbage Collector**

## Garbage Collection

[Java tutorial](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)

- What is GC?
    - GC is the mechanism to automatically **detect**/**delete** the unused objects.
    - Automatic garbage collection is the process of looking at heap memory, **identifying** which objects are in use and which are not, and **deleting** the unused objects. An in use object, or a referenced object, means that some part of your program still maintains a pointer to that object. An unused object, or unreferenced object, is no longer referenced by any part of your program. So the **memory** used by an unreferenced object **can be reclaimed**.
- Why do we need it?
    - More efficiently manage dynamic memory allocation.
- Where is it implemented?
    - Stack
        - local varible, tracking method call flow, return address etc. 
        - one per thread
    - **Heap** 
        - dynamic memory allocation 
        - The heap is where your object data is stored.
        - only one per JVM
- How does it work?
    - **Step 1. Marking**
        - The first step in the process is called **marking**. This is where the garbage collector identifies which pieces of memory are in use and which are not.
        - ![marking](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide3.png)
    - **Step 2. Normal Deletion**
        - Normal deletion removes unreferenced objects leaving referenced objects and pointers to free space.
        - Inconvenient to allocate space again due to too many fragments, so we need compacting.
        - ![normal deletion](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide1b.png)
    - **Step 2a Deletion with Compacting**
        - To further improve performance, in addition to deleting unreferenced objects, you can also compact the remaining referenced objects. By moving referenced object together, this makes new memory allocation much easier and faster.
        - ![deletion with compacting](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide4.png)

### Why Generational Garbage Collection?

As stated earlier, having to mark and compact all the objects in a JVM is inefficient. As more and more objects are allocated, the list of objects grows and grows leading to longer and longer garbage collection time. However, empirical analysis of applications has shown that most objects are short lived.

[!](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/ObjectLifetime.gif)

#### JVM Generations

The information learned from the object allocation behavior can be used to enhance the performance of the JVM. Therefore, the heap is broken up into smaller parts or generations. The heap parts are: **Young Generation**, **Old or Tenured Generation**, and **Permanent Generation**

[!](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide5.png)

The **Young Generation** is where all new objects are allocated and aged. When the young generation fills up, this causes a **minor garbage collection**. Minor collections can be optimized assuming a high object mortality rate. A young generation full of dead objects is collected very quickly. Some surviving objects are aged and eventually move to the old generation.

**Stop the World Event** - All minor garbage collections are "Stop the World" events. This means that all application threads are stopped until the operation completes. Minor garbage collections are always Stop the World events.

The **Old Generation** is used to store long surviving objects. Typically, a threshold is set for young generation object and when that age is met, the object gets moved to the old generation. Eventually the old generation needs to be collected. This event is called a **major garbage collection**.

Major garbage collection are also Stop the World events. Often a major collection is much slower because it involves all live objects. So for Responsive applications, major garbage collections should be minimized. Also note, that the length of the Stop the World event for a major garbage collection is affected by the kind of garbage collector that is used for the old generation space.

The **Permanent generation** contains metadata required by the JVM to describe the classes and methods used in the application. The permanent generation is populated by the JVM at runtime based on classes in use by the application. In addition, Java SE library classes and methods may be stored here.

Classes may get collected (unloaded) if the JVM finds they are no longer needed and space may be needed for other classes. The permanent generation is included in a full garbage collection.

### How to know if an object can be GCed or not?

from a set of the root references/objects, find all the objects reachable through the paths on the dependency graph, other ones are not needed and can be GCed.

**4 kinds of GC roots in Java**

1. **Local varibles** are kept alive by the stack of a thread.
2. **Active Java threads**
3. **Static varibles**
4. **JNI (Java Native Interface) References**

### finalize method

- **finalize method**

It is a method that the Garbage Collector always **calls just before the deletion/destroying** the object which is eligible for Garbage Collection, so as to perform clean-up activity. Clean-up activity means closing the resources associated with that object like Database Connection, Network Connection or we can say resource de-allocation. Remember it is not a reserved keyword.

Once finalize method completes immediately Garbage Collector destroy that object. finalize method is present in Object class and its syntax is:

```protected void finalize throws Throwable{}```


- **Exception in finalize method**

If Garbage Collector calls finalize method, while executing finalize method some unchecked exception rises then **JVM ignores that exception** and rest of program will be continued normally. So in this case the program termination is Normal and not abnormal.

