---
toc: true
layout: base
title: Space and Time Hacks
---

# Hacks
- Record your findings when testing the time elapsed of the different algorithms.

The time it takes for the algorithm to run and present an output, increasing as the space the output takes up. It also changes based on the method/number increase that is set, determining whether the algorithm must loop through more numbers to display the same output.

- Although we will go more in depth later, time complexity is a key concept that relates to the different sorting algorithms. Do some basic research on the different types of sorting algorithms and their time complexity.

https://www.interviewkickstart.com/learn/time-complexities-of-all-sorting-algorithms

Bubble Sort: Compare each adjescent pair

Worst case- O(n2)

Average case- O(n2)

Best case- O(n)

Selection Sort: Divides array into two parts (one of already sorted, and one of to be sorted elements)

Worst, Average, and Best = O(n2)

Insertion Sort: Divides array into two parts (one of already sorted, and one of to be sorted elements). Iterate over each element and put them into the correct array.

Worst case- O(n2)

Average case- O(n2)

Best case- O(n)

Merge Sort: Divide unsorted arrays into sorted arrays

Worst case = Average Case = Best Case = O(n log n)

Quick Sort: Divide and conquer strategy

Worst case: O(n2)

Average case and best case: O(n log n)

- Why is time and space complexity important when choosing an algorithm?

Time and space complexity often determines the efficiency of a program, because when in use, a faster program which takes up the least amount of space it more likely to sell/or be used. It determines whether a program can be applied, because even if it works, if it does not work efficiently it doesn't serve its purpose.

- Should you always use a constant time algorithm / Should you never use an exponential time algorithm? Explain? 

It is good to stick to constant time algorithms, as the algorithm stays the same no matter how large the input it. On the contrary, exponential time algorithms increase in amount of steps as the input increases, making the run time larger and larger. By rule of thumb, it is better to stick with constant, though exponential is okay for small input algorithms.

- What are some general patterns that you noticed to determine each algorithm's time and space complexity?

Constant sequences run faster, and take up less space. Exponential algorithms take more time, and often take up more space do to the increases steps. Algorithms which have longer runtimes have more likelihood of breaking, due to the computer's capacity to continue a process past a certain amount of time.

Complete the Time and Space Complexity analysis questions linked below.
[Practice](https://www.geeksforgeeks.org/practice-questions-time-complexity-analysis/)

Reflection: While I still do not completely understand how to tell the pattern, I tended to get the answers to the questions correct. I found that through process of elimination, and determining whether the algorithm is multiplying or dividing, I was usually able to pick the correct time complexity.