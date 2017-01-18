##**Interview Process**

* Listen carefully
* Make test cases with prototypes
* Bruteforce then optimize 
* Walk through your code with test cases
* Implement a solution and test it with extreme cases
* Talk about BUD (Bottlenecks, Unnecessary work, Duplicated work)


##**Big O**

[Big O Cheat Sheet](http://bigocheatsheet.com/)

[More detailed explanation of data structures](https://www.clear.rice.edu/comp160/data_cheat.html)

[Tech Interview](https://gist.github.com/TSiege/cbb0507082bb18ff7e4b)


## Data Structure Basics
###**Array**
####Definition:
- **Linear arrays**, or one dimensional arrays, are the most basic.
  - Are static in size, meaning that they are declared with a fixed size.
- **Dynamic arrays** are like one dimensional arrays, but have reserved space for additional elements.
  - If a dynamic array is full, it copies it's contents to a larger array.
- **Two dimensional arrays** have x and y indices like a grid or nested arrays. 
  
####What you need to know:
- Most efficient use of memory; use in cases where data size is fixed.
- Optimal for indexing; bad at searching, inserting, and deleting (except at the end).
 
####Big O efficiency:
- Indexing:         Linear array: O(1),      Dynamic array: O(1)
- Search:           Linear array: O(n),      Dynamic array: O(n)
- Optimized Search: Linear array: O(log n),  Dynamic array: O(log n)
- Insertion:        Linear array: n/a        Dynamic array: O(n)


###**Linked List**
####Definition: 
- Stores data with **nodes** that point to other nodes.
  - Nodes, at its most basic it has one data and one reference to another node.
- **Linked list** chains nodes together by pointing one node's reference towards another node.  
- **Doubly linked list** has nodes that reference the previous node.
- **Circularly linked list** is a linked list whose tail (last node) references the head (first node).

####What you need to know:
- Many operations are fast, but watch out for cache coherency.
- Designed to optimize insertion and deletion, slow at indexing and searching.
- **Doubly linked list** has nodes that reference the previous node.
- **Circularly linked list** is simple linked list whose **tail**, the last node, references the **head**, the first node.


####Big O efficiency:
- Indexing:         Linked Lists: O(n)
- Search:           Linked Lists: O(n)
- Optimized Search: Linked Lists: O(n)
- Insertion:        Linked Lists: O(1)  

####Tips
- If you need to keep a position, use a counter or a pointer.
- If lists are not the same length, you can pad with zeros or trim.
- Loops can be detected with slow runner / fast runner.

####Python implementation:
- class Node:
  - def __init__(self, initdata):
    - self.data = initdata
    - self.next = None;
  - def getData(self):
    - return self.data
  - def getNext(self):
    - return self.next
  - def setData(self, newdata):
    - self.data = newdata
  - def setNext(self, newnext):
    - self.next = newnext


###**Hash Table or Hash Map**
####Definition: 
- Stores data with key value pairs.
- **Hash functions** accept a key and return an output unique only to that specific key. 
  - This is known as **hashing**, which is the concept that an input and an output have a one-to-one correspondence to map information.
  - Hash functions return a unique address in memory for that data.

####What you need to know:
- Designed to optimize searching, insertion, and deletion.
- **Hash collisions** are when a hash function returns the same output for two distinct inputs.
  - All hash functions have this problem.
  - This is often accommodated for by having the hash tables be very large.
- Hashes are important for associative arrays and database indexing.

####Big O efficiency:
- Indexing:         Hash Tables: O(1)
- Search:           Hash Tables: O(1)
- Insertion:        Hash Tables: O(1)  
- Space complexity is O(n)


###**Binary Tree**
####Definition: 
- Is a tree-like data structure where every node has zero to two children.
  - A leaf has no children node. Otherwise, there is one left and right child node.

####What you need to know:
- Designed to optimize searching and sorting. Min heap, max heap.
- A **degenerate tree** is an unbalanced tree, which if entirely one-sided is a essentially a linked list.
  - A binary tree of N nodes has a depth log N. Worst case is a straight list of depth N.
- They are comparably simple to implement than other data structures.
- Used to make **binary search trees**.
  - A binary tree that uses comparable keys to assign which direction a child is.
  - All left descendants <= parent node <= all right descendant. This must be true for all node and all descendants. 
  - Left child has a key smaller than it's parent node.
  - Right child has a key greater than it's parent node.
  - There can be no duplicate node.

####Big O efficiency:
- Indexing:  Binary Search Tree: O(log n)
- Search:    Binary Search Tree: O(log n)
- Insertion: Binary Search Tree: O(log n) 

###**Stacks and Queues**
####Definition: 
- Stacks are LIFO (last-in first-out) and uses
  - pop() - remove the top item from the stack
  - push(item) - add item on top of the stack
  - peek() - return the top of the stack
  - isEmpty() - return true if and only if the stack is empty
- Queues are FIFO (first-in first-out) and uses:
  - add(item) - add item to the end of the list
  - remove() - remove the first item of the list
  - peek() - return the top (first?) item of the queue
  - isEmpty() - return true if and only if the stack is empty

####What you need to know:
- Shouldn't be selected for performance reasons, but algorithmic ones.
- Can be implemented with an array, a vector, an ArrayList, a linked list, or any other collection. 
  
####Big O efficiency:
- Indexing:  Stacks and Queues: O(n)
- Search:    Stacks and Queues: O(n)
- Insertion: Stacks and Queues: O(1) 

###**Graphs**
####Definition: 
- Graphs are a collection of nodes with edges between some of them.

####What you need to know:
- Can be implemented with adjacency list or adjacency matrix.
- Searching a graph is done by Breadth First Search or Depth First Search.

####Big O efficiency:
- Nothing found.

 

## Search Basics
###**Breadth First Search**
####Definition:
- Look at each neighbor before looking at children, uses a queue
  - Visit a node, add all neighbors to the queue and mark them as visited.
  - Go through the queue.

####What you need to know:
- Optimal for searching a tree that is wider than it is deep.
- Because it uses a queue it is more memory intensive than **depth first search**.
- The queue uses more memory because it needs to stores pointers
  
####Big O efficiency:
- Search: Breadth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices

###**Depth First Search**
####Definition:
- Recursive search through the child of each node before looking to the neighbors, uses a stack
  - Visit a node, mark it as visited and add it to the stack, visit the first child
  - If there are no more child, pop the stack.

####What you need to know:
- Optimal for searching a tree that is deeper than it is wide.
- Because a stack is LIFO it does not need to keep track of the nodes pointers and is therefore less memory intensive than breadth first search.
  
####Big O efficiency:
- Search: Depth First Search: O(|E| + |V|)
- E is number of edges
- V is number of vertices


####Breadth First Search Vs. Depth First Search
- The simple answer to this question is that it depends on the size and shape of the tree.
  - For wide, shallow trees use Breadth First Search
  - For deep, narrow trees use Depth First Search
 - Bidirectional search are usually Breadth First Search from point A and B simultaneously.

####Nuances:
  - Because BFS uses queues to store information about the nodes and its children, it could use more memory than is available on your computer.  (But you probably won't have to worry about this.)
  - If using a DFS on a tree that is very deep you might go unnecessarily deep in the search. See [xkcd](http://xkcd.com/761/) for more information.
  - Breadth First Search tends to be a looping algorithm.
  - Depth First Search tends to be a recursive algorithm.



## Efficient Sorting Basics
###**Merge Sort**
####Definition:
- A comparison based sorting algorithm
  - Divides entire dataset into groups of at most two.
  - Compares each number one at a time, moving the smallest number to left of the pair.
  - Once all pairs sorted it then compares left most elements of the two leftmost pairs creating a sorted group of four with the smallest numbers on the left and the largest ones on the right. 
  - This process is repeated until there is only one set.

####What you need to know:
- This is one of the most basic sorting algorithms.
- Know that it divides all the data into as small possible sets then compares them.

####Big O efficiency:
- Best Case Sort: Merge Sort: O(n)
- Average Case Sort: Merge Sort: O(n log n)
- Worst Case Sort: Merge Sort: O(n log n)
- Space Complexity: Merge Sort: O(n)


###**Quicksort**
####Definition:
- A comparison based sorting algorithm
  - Divides entire dataset in half by selecting the average element and putting all smaller elements to the left of the average.
  - It repeats this process on the left side until it is comparing only two elements at which point the left side is sorted.
  - When the left side is finished sorting it performs the same operation on the right side.
- Computer architecture favors the quicksort process.

####What you need to know:
- While it has the same Big O as (or worse in some cases) many other sorting algorithms it is often faster in practice than many other sorting algorithms, such as merge sort.
- Know that it halves the data set by the average continuously until all the information is sorted.

####Big O efficiency:
- Best Case Sort: Quicksort: O(n log n)
- Average Case Sort: Quicksort: O(n log n)
- Worst Case Sort: Quicksort: O(n^2)
- Space Complexity: Quicksort: O(log n)

####Merge Sort Vs. Quicksort
- Quicksort is likely faster in practice.
- Merge Sort divides the set into the smallest possible groups immediately then reconstructs the incrementally as it sorts the groupings.
- Quicksort continually divides the set by the average, until the set is recursively sorted.


###**Bubble Sort**
####Definition:
- A comparison based sorting algorithm
  - It iterates left to right comparing every couplet, moving the smaller element to the left.
  - It repeats this process until it no longer moves and element to the left.

####What you need to know:
- While it is very simple to implement, it is the least efficient of these three sorting methods.
- Popular for its capability to detect a very small error.

####Big O efficiency:
- Best Case Sort: Bubble Sort: O(n)
- Average Case Sort: Bubble Sort: O(n^2)
- Worst Case Sort: Bubble Sort: O(n^2)
- Space Complexity: Bubble Sort: O(1)


###**Selection Sort**
####Definition:
- Finds the smallest number in the unsorted array and put it into the sorted array.

####What you need to know:
- Among simple average-case O(n^2) algorithms, selection sort almost always outperforms bubble sort.
- Selection sort is greatly outperformed on larger arrays by divide-and-conquer algorithms such as mergesort. However, insertion sort or selection sort are both typically faster for small arrays

####Big O efficiency:
- Best Case Sort: Selection Sort: O(n^2)
- Average Case Sort: Selection Sort: O(n^2)
- Worst Case Sort: Selection Sort: O(n^2)
- Space Complexity: Selection Sort: O(1)


###**Radix Sort**
####Definition:
- Radix sort is a non-comparative integer sorting algorithm that sorts data with integer keys by grouping keys by the individual digits which share the same significant position and value.

####What you need to know:
- Works only with integers, strings, words or fixed-length integer representations. 

####Big O efficiency:
- Best Case Sort: Radix Sort: O(nk)
- Average Case Sort: Radix Sort: O(nk)
- Worst Case Sort: Radix Sort: O(nk)
- Space Complexity: Radix Sort: O(n+k)


## Basic Types of Algorithms
###**Recursive Algorithms**
####Definition:
- An algorithm that calls itself in its definition.
  - **Recursive case** a conditional statement that is used to trigger the recursion.
  - **Base case** a conditional statement that is used to break the recursion.

####What you need to know:
- **Stack level too deep** and **stack overflow**.
  - If you've seen either of these from a recursive algorithm, you messed up.
  - It means that your base case was never triggered because it was faulty or the problem was so massive you ran out of RAM before reaching it.
  - Knowing whether or not you will reach a base case is integral to correctly using recursion.
  - Often used in Depth First Search


###**Iterative Algorithms**
####Definition:
- An algorithm that is called repeatedly but for a finite number of times, each time being a single iteration.
  - Often used to move incrementally through a data set.

####What you need to know:
- Generally you will see iteration as loops, for, while, and until statements.
- Think of iteration as moving one at a time through a set.
- Often used to move through an array.

####Recursion Vs. Iteration
- The differences between recursion and iteration can be confusing to distinguish since both can be used to implement the other. But know that,
  - Recursion is, usually, more understanble and easier to implement.
  - Iteration uses less memory and harder to read.
- **Functional languages** tend to use recursion. (i.e. Haskell)
- **Imperative languages** tend to use iteration. (i.e. Ruby)
- Check out this [Stack Overflow post](http://stackoverflow.com/questions/19794739/what-is-the-difference-between-iteration-and-recursion) for more info.

####Pseudo Code of Moving Through an Array (this is why iteration is used for this)
```
Recursion                         | Iteration
----------------------------------|----------------------------------
recursive method (array, n)       | iterative method (array)
  if array[n] is not nil          |   for n from 0 to size of array
    print array[n]                |     print(array[n])
    recursive method(array, n+1)  |
  else                            |
    exit loop                     |
```


###**Greedy Algorithm**
####Definition:
- An algorithm that, while executing, selects only the information that meets a certain criteria.
- The general five components, taken from [Wikipedia](http://en.wikipedia.org/wiki/Greedy_algorithm#Specifics):
  - A candidate set, from which a solution is created.
  - A selection function, which chooses the best candidate to be added to the solution.
  - A feasibility function, that is used to determine if a candidate can be used to contribute to a solution.
  - An objective function, which assigns a value to a solution, or a partial solution.
  - A solution function, which will indicate when we have discovered a complete solution.

####What you need to know:
- Used to find the optimal solution for a given problem.
- Generally used on sets of data where only a small proportion of the information evaluated meets the desired result.
- Often a greedy algorithm can help reduce the Big O of an algorithm.

####Pseudo Code of a Greedy Algorithm to Find Largest Difference of any Two Numbers in an Array.
```
greedy algorithm (array)
  var largest difference = 0
  var new difference = find next difference (array[n], array[n+1])
  largest difference = new difference if new difference is > largest difference
  repeat above two steps until all differences have been found
  return largest difference
```

This algorithm never needed to compare all the differences to one another, saving it an entire iteration.


###**Binary Search**
####Definition:
- Binary search is a fast search algorithm with run-time complexity of ?(log n). This search algorithm works on the principle of divide and conquer. For this algorithm to work properly, the data collection should be in the sorted form.

####What you need to know:
- Compare the middle item of the collection.
  - If a match occurs, return the index of item.
  - If it is greater than the item, then recursively search the sub-array to the left of the middle item. 
  - If it is smaller than the item, then recursively search the sub-array to the right of the middle item. 
  - If the sub-array is empty, return an error.

####Pseudo Code 
Procedure binary_search
   A <- sorted array
   n <- size of array
   x <- value to be searched

   Set lowerBound = 1
   Set upperBound = n 

   while x not found
      if upperBound < lowerBound 
         EXIT: x does not exists.
   
      set midPoint = lowerBound + ( upperBound - lowerBound ) / 2
      
      if A[midPoint] < x
         set lowerBound = midPoint + 1
         
      if A[midPoint] > x
         set upperBound = midPoint - 1 

      if A[midPoint] = x 
         EXIT: x found at location midPoint


###**Scalability**
- Design framework
  - Scope the problem by asking questions
  - Make reasonable assumptions
  - Draw the major components (provide an end-to-end flow)
  - Analyze key issues and locate bottlenecks
  - Redesign to account for the key issues
Key concepts
  - Horizontal vs Vertical Scaling (Increase the number of nodes vs increase the resources per node)
  - Load Balancer (if a server crash, design so that it doesn't take down the whole system)
  - Database Denormalization (relational databases such as SQL get slow as the system grows bigger. Denormalization, i.e. adding redundant information speeds up reads. Or go with a NoSQL database)
  - Database Partitioning/Sharding (strategies to find which data is on which machine)
    - Vertical Partitioning (Partition by feature. - might get very large)
    - Key/Hash-based Partitioning (Use an ID and do a mod(key, n). - n must be fixed)
    - Directory-based Partitioning (Maintain a look-up table. - single point of failure, - impacts performance)
  - Caching (i.e. simple key-value pairing)
  - Asynchronous Processing and Queues
  - Networking metrics: bandwidth (maximum data transfer), throughput (actual data transfer), latency (delay between sender and receiver)
  - Consider failures, availability and reliability, read-heavy vs write-heavy, security


###**Testing**
- Real World Object
  - 1. Who will use it and why?
  - 2. What are the use cases?
  - 3. What are the bounds of use? (e.g. temperature)
  - 4. What are the stress / failure conditions?
  - 5. How would you perform the testing?
- Testing software
  - 1. Black box or white box testing?
  - 2. Who will use it and why?
  - 3. What are the use cases?
  - 4. What are the bounds of use? (e.g. temperature)
  - 5. What are the stress / failure conditions?
  - 6. What are the test cases? How would you perform the testing?
- Testing a function
  - 1. Define the test cases (differentiate normal, extremes, illegal, strange inputs)
  - 2. Define the expected result
  - 3. Write test code
- Troubleshooting
  - 1. Understand the scenario
  - 2. Break down the problem
  - 3. Create specific, manageable tests

  
###**Unclassified**
- String encoding: ASCII (128 values, 256 extended) or Unicode (2^21 chars, UTF-32 or UTF-8)
- 2^10 = 1024 (1KB); 2^20 ~= 1 million (1MB); 2^30 ~= 1 billion (1GB)
