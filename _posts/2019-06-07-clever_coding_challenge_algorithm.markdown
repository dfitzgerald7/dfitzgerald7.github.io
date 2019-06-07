---
layout: post
title:      "Clever Coding Challenge Algorithm"
date:       2019-06-07 14:06:31 -0400
permalink:  clever_coding_challenge_algorithm
---


For the past several days I've been doing coding challenges on [Hacker Rank](https://www.hackerrank.com/dashboard) as interview prep. I came across  [this challenge](https://www.hackerrank.com/challenges/crush/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays). 

They explain the challenge as: 

```
`Starting with a 1-indexed array of zeros and a list of operations, for each operation add a value to each of the array element between two given indices, inclusive. Once all operations have been performed, return the maximum value in your array.

For example, the length of your array of zeros . Your list of queries is as follows:

    a b k
    1 5 3
    4 8 7
    6 9 1
Add the values of  between the indices  and  inclusive:

index->	 1 2 3  4  5 6 7 8 9 10
	[0,0,0, 0, 0,0,0,0,0, 0]
	[3,3,3, 3, 3,0,0,0,0, 0]
	[3,3,3,10,10,7,7,7,0, 0]
	[3,3,3,10,10,8,8,8,1, 0]
The largest value is  after all operations are performed.`
```

Basically, you gave an array of 0s and have to add numbers between certain indices. Once I understood the problem, I was initially surprised by it being in the hard category. You are given an array of arrays that contain a starting index, end index, and value to add to those indices. For each of those queries, I could have a for loop that goes from start to end and add that value. Simple enough, right?
```
function arrayManipulation(n, queries) {
    const arr = []
    for (let i = 0; i < n; i++){
        arr.push(0)
    }

    queries.forEach(([start, end, value]) => {
        for (let j = start-1; j<= end-1; j++) {
            arr[j] += value
        }
    })

    let max = arr[0]
    for (let k = 1; k < n; k++) {
        if (arr[k] > max) {
            max = arr[k]
        }
    }
    return max
}
```
I put something basic like this together and went to submit. The problem called for a 1-indexed array, so I just subtracted 1 from the queries. About half the tests passed. The ones that failed were due to a timeout. My solution right now is O(n^2) due to the queries.forEach block. 

After playing around with it for some time and not making any progress I visited the [forum](https://www.hackerrank.com/challenges/crush/forum) where user 'amansbhandari' shared their interesting solution. 

Instead of iterating through all indices individually and adding the values, you basically 'set up' the start and end conditions for each query and add them all at once. For each query, you add the value at the start index and subtract that value after the end index since the end is inclusive. Once you have done that for all queries, loop through the index again once and add the previous value. This permiates all of the queries through the array. If we take the example they gave, we start with the queries 
```
    a b k
    1 5 3
    4 8 7
    6 9 1
```
and the array
```
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
For the first query, we have:
```
[3, 0, 0, 0 , 0 , -3, 0 , 0, 0, 0]
```
Remember that it starts at index 1. For the second:
```
[3, 0, 0, 7, 0, -3, 0, 0, -7, 0]
```
and the third: 
```
[3, 0, 0, 7, 0,  -2, 0, 0, -7, -1] 
```
Now since the start and end points are set up we can just iterate from index 1 to the end and add the previous value, to get: 
```
[3, 3, 3, 10, 10, 8, 8, 8, 1, 0]
```
Instead of having having a potential n^2 runtime it is now 3n, or O(n). My final code was this: 

```
function arrayManipulation(n, queries) {
    const arr = [] //make array of 0s
    for (let i = 0; i < n; i++){
        arr.push(0)
    }
    //add value at start index, subtract at index after end
    queries.forEach(([start, end, value]) => {
        arr[start-1] += value
        arr[end] -= value
    })
    //add previous value so the queries permiate through arr 
    //since the end index subtracted that value previously,
        //the rest of the array is not affected by the wrong query
    for (let j = 1; j < n; j++){
        arr[j] += arr[j-1]
    }
    //find max
    let max = arr[0]
    for (let k = 1; k < n; k++){
        if (arr[k] > max) {
            max = arr[k]
        }
    }

    return max

}
```
