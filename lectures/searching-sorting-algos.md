---
title: "Searching and Sorting Algorithms"
output:
  ioslides_presentation: default
  slidy_presentation: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```

## Searching in a List

To implement the ```search``` method,
we develop the following strategy.
We visit each node of the list and we check
whether this node has stored the data
that we are looking for.
We conduct this process
until we find the appropriate node.

```python
def search(self,item):
    current = self.head
    found = False
    while current != None and not found:
        if current.getData() == item:
            found = True
        else:
            current = current.getNext()

    return found
```

## Search for an Element

```python
>>> mylist.search(17)
True
```

Here, the traversal needs to move up to the
node that contains the element ```17```.

![](./figures/search-ll.png)

## Remove an Element

To implement the remove method,
we need to perform two passes.

- First, we *traverse* the list until
we find the element to be removed.
This step is similar with the traversal
we conduct for the ```search``` method.

- Second, we *update* the nodes that
contain the references to the elements.
If we remove the node,
how can we update the links to the next nodes? 

## The ```previous``` Reference

Since a linked list does not premits
backwards traversal,
we use two external references.

The first reference is the ```current``` one
that represents the current location of the traverse,
and the second reference is the ```previous``` one
that represents a node *behind* the ```current```.

XX: To add a figure here.

## The ```remove``` Method

```python
def remove(self,item):
    current = self.head
    previous = None
    found = False
    while not found:
        if current.getData() == item:
            found = True
        else:
            previous = current
            current = current.getNext()

    if previous == None:
        self.head = current.getNext()
    else:
        previous.setNext(current.getNext())
```

## Searching and Sorting Algorithms

- Explain and implement sequential search and binary search.

- Explain and implement selection sort, bubble sort, merge sort, quick sort, insertion sort, and shell sort.

## Searching

A search returns ```true``` if the element is found in a collection, and
```false``` when it does not reside in that collection.

In Python, we can use the ```in``` operator
to search whether an element is a member of a particular collection of items.

But, how is this operation actually implemented?

```python
>>> 15 in [3,5,2,4,1]
False
>>> 3 in [3,5,2,4,1]
True
>>>
```

## Sequential Search

When elements are stored in a collection,
such as a list, where there are relative to each other,
we say that these elements have a linear or sequential relationship.
Since the values of lists are indexed,
it is possible to order the items and process them in a sequence.

```python
def sequentialSearch(alist, item):
    pos = 0
    found = False
    while pos < len(alist) and not found:
        if alist[pos] == item:
            found = True
        else:
            pos = pos+1
	
    return found
```

## Complexity of Sequential Search

To find the **complexity** of a sequential search algorithm,
we need to count the number of the comparisons we need to perform
until we find the element we are looking for in a collection.

If we make the assumption that the elements of a list are in a **random order**
the probability to find an element in a particular position,
is the same as if it was allocated in any other position in the list.

Whereas if the elements are in an **ascending order**,
we still need to make ```n``` comparisons to find a particular element,
but our search will be faster if the element is not, finally, in the list.

## Comparisons in Random Assignment

If an element does not belong in a randomly ordered list, ```L = {2, 6, 1, ... n}```,
we will need to conduct ```n``` comparisons for a sequential search.

On the contrary, if an element does belong in the above list,
we will conduct eather ```1``` comparison (best case scenario),
or ```n``` coparisons (worst case scenario) to find the right element.

Therefore, the complexity of the sequential search algorithm is ```O(n)```.

## Comparisons in Ordered List

If an element does not belong in a ordered list, ```L = {1, 2, 3, ... n}```,
we will need to conduct either ```1``` comparison (best case scenario)
or ```n``` comparisons (worst case scenario) for a sequential search.
What if we search for the element ```30``` in the following list?

If an element does belong in the above list,
we will conduct eather ```1``` comparison (best case scenario),
or ```n``` coparisons (worst case scenario) to find the right element.

Therefore, the complexity of the sequential search algorithm is again ```O(n)```.

![](./figures/ordered-ll.png)

## Binary Search

We can split the list in the middle and appling the searching process
in its both halfs.
For instance, consider to find the element ```54```
by using the so-called *divide and conquer* strategy.

![](./figures/binary.png)

## Implementation of Binary Search Algorithm

```python
	def binarySearch(alist, item):
	    first = 0
	    last = len(alist)-1
	    found = False
	    while first<=last and not found:
	        midpoint = (first + last)//2
	        if alist[midpoint] == item:
	            found = True
	        else:
	            if item < alist[midpoint]:
	                last = midpoint-1
	            else:
	                first = midpoint+1
	    return found
```

## Complexity of Binary Search

To estimate the complexity of a binary search algorithm,
we should take into account that each comparison eliminates
about half of the remaining elements.

If we have an *ordered* list of ```n``` elements,
around $n/2$ elements will be left after the first comparison.
After the second comparison, there will be around $n/4$, and so on.

The following table helps to understand how many time we need to split a list.

XX: the table to be added here.

## Sorting

Sorting is the process of assigning the elements of a collection (e.g. list)
in a particular order (e.g. put words in an alphabetical order).

A typical *systematic way* to sort the elements of a collection
is, *first*, to compare two values from the collection
seeing which is the smaller (or greater).

And, *second*, if the two values are not in the correct order,
based on their *comparison*,
we need to *exchange* them.

This *exchange* is expensive and,
therefore, the totall *number* of the needed exchanges
will indicate the *efficiency* of a sorting algorithm.

## Bubble Sort

![](./figures/bubble-sort.png)

## Bubble Sort Implementation

```python
def bubbleSort(alist):
    for passnum in range(len(alist)-1,0,-1):
        for i in range(passnum):
            if alist[i]>alist[i+1]:
                temp = alist[i]
                alist[i] = alist[i+1]
                alist[i+1] = temp
```

```python
alist = [54,26,93,17,77,31,44,55,20]
bubbleSort(alist)
print(alist)
```

```python
[17, 20, 26, 31, 44, 54, 55, 77, 93]
```

## Bubble Sort Complexity

Regardless of how the items are arranged in the initial list,
$n−1$ passes will be made to sort a list of size $n$.

In the *best* case scenario,
if the list is already ordered,
we will need to perform no exchanges.

However, in the *worst* case, every comparison will cause an exchange.
Therefore, the complexity of the algorithm is $O(n^2)$.

## Selection Sort

The selection sort makes *one* exchange for every pass in the list.
The algorithm finds the greater element in the list
and then places it in the proper location (from the end of the list).

![](./figures/selection-sort.png)

## Selection Sort Implementation

```python
def selectionSort(alist):
   for fillslot in range(len(alist)-1,0,-1):
       positionOfMax=0
       for location in range(1,fillslot+1):
           if alist[location]>alist[positionOfMax]:
               positionOfMax = location

       temp = alist[fillslot]
       alist[fillslot] = alist[positionOfMax]
       alist[positionOfMax] = temp
```

```python
alist = [54,26,93,17,77,31,44,55,20]
selectionSort(alist)
print(alist)
```

```python
[17, 20, 26, 31, 44, 54, 55, 77, 93]
```

## Selection Sort Complexity

The selection sort makes the same number of comparisons
as the bubble sort and is therefore also $O(n^2)$.

However, due to the reduction in the number of exchanges,
the selection sort typically executes faster than the bubble sort.

## Insertion Sort

The insertion sort algorith maintains
a sorted sublist in the lowest positions of a list.
Each new item is "inserted" sorted
to the sublist.

![](./figures/insertion-sort.png)

## Insertion Sort Implementation

```python
def insertionSort(alist):
   for index in range(1,len(alist)):

     currentvalue = alist[index]
     position = index

     while position>0 and alist[position-1]>currentvalue:
         alist[position]=alist[position-1]
         position = position-1

     alist[position]=currentvalue
```

```python
alist = [54,26,93,17,77,31,44,55,20]
insertionSort(alist)
print(alist)
```

```python
[17, 20, 26, 31, 44, 54, 55, 77, 93]
```

## Insertion Sort Complexity

The maximum number of comparisons for an insertion sort
is the sum of the first $n−1$ integers.
This is $O(n^2)$.

However, in the best case,
only one comparison needs to be done on each pass.
This would be the case for an already sorted list.

## Shell Sort

This alrgorithm starts by sorting pairs of elements far apart from each other,
then progressively reducing the gap between elements to be compared.

It is a generalization of the bubble and insertion sort algorithms.

XX: to be continued

## Merge Sort

Merge sort is a recursive algorithm that continually splits a list in the middle.

After two halves are sorted,
then the **merge** operation is performed.

![](./figures/split.png)

## Merge

![](./figures/merge.png)

## Complexity of Merge Sort

A merge sort is an $O(n log n)$ algorithm.

Can you explain why?

## Quick Sort

A quick sort first selects a value,
which is called the *pivot* value.

The role of the pivot value is to assist with splitting the list.
The actual position where the pivot value belongs in the final sorted list,
commonly called the split point,
will be used to divide the list for subsequent calls to the quick sort.

## How does it works?

![](./figures/quick-sort.png)

## Quick Sort Complexity

In the worst case, the split points may not be in the middle and
can be very skewed to the left or the right.
In this case, sorting a list of $n$ items divides into
sorting a list of $0$ items and a list of $n−1$ items.

Then sorting a list of $n−1$ divides into a list of size $0$ and a list of size $n−2$, and so on.
The result is an $O(n^2)$ sort with all of the overhead that recursion requires.

## Bibliography

- Problem Solving with Algorithms and Data Structures using Python, by Brad Miller and David Ranum, Luther College.