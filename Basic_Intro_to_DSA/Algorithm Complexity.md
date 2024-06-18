# How do you measure the efficiency of an algorithm?


# What is Big O?
- Big O is also known as the algorithm's upper bound since it analyses the worst-case situation.

- The best-case scenario usually tells us nothing — we'll possibly solve the problem on the first try. That’s why we employ worst-case scenarios to get meaningful input. It tells us that the algorithm will always perform equal to or better than the worst-case scenario.

- Now, the algorithm & data structure you employ while programming code is critical. Big O notation makes it easier to compare the performance of different algorithms and figure out which one is best for your code.

- In computer science, Big O Notation is a mathematical function used to determine the difficulty of an algorithm. It defines the time it takes to execute an algorithm. It will also help you determine how your algorithm's performance will change as the input size

## How do you measure the efficiency of an algorithm?
- Efficiency is measured in two ways: time complexity and space complexity.

- A function's time complexity measures how long it takes to execute in terms of computational steps. The space complexity of a function is determined by the amount of memory it uses.

- The big O notation, O(g(n)), is a collection of functions. A function f(n) is a member of that collection only if it fits the following criteria:
```c
0 ≤ f(n) ≤ c.g(n)
```
- So, when an algorithm performs a computation on each item in an array of size n, it takes O(n) time and performs O(1) work on each item.

### But why do we need Big O?
- The world we live in today consists of complicated apps and software, each running on various devices and each having different capabilities. Some devices like desktops can run heavy machine learning software, but others like phones can only run apps. So when you create an application, you’ll need to optimize your code so that it runs smoothly across devices to give you an edge over your competitors.
## What is Time Complexity?
- The time complexity, computational complexity, or temporal complexity describes the amount of time necessary to execute an algorithm. It is not a measure of the actual time taken to run an algorithm; instead, it is a measure of how the time taken scales with changes in the input length. As a result, the size and magnitude of the processed data have a significant impact. Moreover, it also aids in defining an algorithm's usefulness and evaluating its performance.

### What is Space Complexity?
- The overall amount of memory or space utilized by an algorithm/program, including the space of input values for execution, is called space complexity. To determine space complexity, simply compute how much space the variables in an algorithm/a program take up.

- People usually confuse auxiliary space with space complexity. Auxiliary space is not the equivalent of space complexity, but it’s a part of it. Auxiliary space is just the temporary or extra space, whereas space complexity also includes space used by input values.

- Put simply,
```c
Space Complexity = Auxiliary space + Space used by input values.
```
- The best algorithms/programs should have the least space complexity. The lesser the space used, the faster it executes.

- Ideally, space and time complexities depend on various factors, such as underlying hardware, OS, CPU, processor, etc. But to keep things simple, we typically don’t consider these factors when analyzing an algorithm's performance.

- Following are the key time and space complexities:

- 1.Constant: O(1)
- 2.Linear time: O(n)
- 3.Logarithmic time: O(n log n)
- 4.Quadratic time: O(n^2)
- 5.Exponential time: O(2^n)
- 6.Factorial time: O(n!)

- As a result, programmers should inspect and evaluate their code thoroughly. This cheat sheet for Big O Notation (a time complexity cheat sheet across data structures) will help you understand a range of complications.

### Constant => O(1)
- the size of input does not affect the number of operations or the amount of time it takes for an algorithm to complete

<img width="100%" src="https://github.com/Gurupatil0003/DSA_Tutorial/blob/master/Img/bigO1.png"/>

