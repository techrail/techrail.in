---
layout: single
title: "Big O Notation"
date: 2018-02-19 08:37:20 +0530
toc: true
toc_label: "On this page"
toc_icon: "exchange-alt"
author_profile: false
permalink: "/algorithms/big-o-notation"
sidebar:
  nav: "algorithms"

---

Big O notation sounds scary but it's not. Bog O notation is for measuring time complexity of an algorithm. But that you might have already heard. The problem is - most people do not understand what that means and that's what scares them. 

Big O in very simple terms means - how long can we expect this algorithm to run as we go on increasing the input size. 

Take Bubble sort for example: 

Bubble sort takes a list of n entities (usually numbers) and runs a loop n times to process n-1 entities in every iteration of the loop. Mathematically, that's `n * (n-1)`. That's approximately `n^2`. So if sorting 10 elements takes 10 seconds then sorting 20 elements will take about 100 seconds. For 40 elements it would take about 10000 seconds. For 80 elements, it would take 100000000 seconds. 

Thankfully, most modern computers can sort a lot faster. But the numbers were to show the importance of a O(n^2). Can you see the problem here? This is because the bubble sort contains two nested loops. If there were three nested loops, then the Big O notation for the algorithm would be `n^3` and the performance would be much worse.

## Examples of Big O notation

### O(1)

An algorithm with O(1) means that the algorithm always returns a valid output in the same amount of time. These two functions:

###### Function 1

```
function getFirstValue(fromThisArray) {
	// Takes 1 ms
	return fromThisArray[0];
}
```

###### Function 2

```
function getFirstValue(fromThisArray) {
	// Sleep for 2 seconds
	sleep(2000);
	// Takes 1 ms
	return fromThisArray[0];
}
```

both have the performance of O(1) because irrespective of the size of `fromThisArray`, they both return in constant amount of time - 2001 and 1 ms respectively.

### O(n^2)

We have already talked about the bubble sort. It looks something like this: 

```
function sort(inputArray) {
	for(i=0; i<inputArray.length; i++){
		for(j=1; j<inputArray.length; j++) {
			// Decide and Do swap
		}
	}
}
```

Depending on the size of `inputArray`, this function can run a total of 3 swaps or millions (imagine 1000+ elements in the array). The number of _decide and do swap_ operations performed is in direct proportion of the square of _length_ of `inputArray`. For an array with 10 elements, the inner loop will run for 90 times, while for an array of 100 elements, it runs for 900 times. For an element of 2000 elements, the inner loop runs for 3998000 times. 

Hence, it is advisable to bring down the value of the Big O of the algorithm.

### O(log n)




