# The Celebrity Problem

Last Updated : 25 Feb, 2025

Given a square matrix ****mat[][]**** of size ****n x n,**** such that ****mat[i][j] = 1**** means ****i********th**** person knows ****j********th**** person, the task is to find the ****celebrity****. A celebrity is a person who is known to all but does not know anyone. Return the index of the celebrity, if there is no celebrity return -1.

****Note:**** Follow 0-based indexing and mat[i][i] will always be 1.

****Examples:****  

> ****Input:**** mat[][] = [[1, 1, 0],  
> [0, 1, 0],  
> [0, 1, 1]]  
> ****Output:**** 1  
> ****Explanation:**** 0th and 2nd person both know 1. Therefore, 1 is the celebrity.
> 
> ****Input:**** mat[][] = [[1, 1],  
> [1, 1]]  
> ****Output:**** -1  
> ****Explanation:**** The two people at the party both know each other. None of them is a celebrity.
> 
> ****Input:**** mat[][] = [[1]]  
> ****Output:**** 0

[

Try it on GfG Practice

![redirect icon](https://media.geeksforgeeks.org/auth-dashboard-uploads/Group-arrow.svg)



](https://www.geeksforgeeks.org/problems/the-celebrity-problem/1)

Table of Content

- [[Naive Approach] - Using Adjacency List - O(n^2) Time and O(n) Space](https://www.geeksforgeeks.org/the-celebrity-problem/#naive-approach-using-adjacency-list-on2-time-and-on-space)
- [[Efficient Approach] - Using Stack - O(n) Time and O(n) Space](https://www.geeksforgeeks.org/the-celebrity-problem/#efficient-approach-using-stack-on-time-and-on-space)
- [[Expected Approach] - Using Two Pointers - O(n) Time and O(1) Space](https://www.geeksforgeeks.org/the-celebrity-problem/#expected-approach-using-two-pointers-on-time-and-o1-space)

### ****[Naive Approach] - Using Adjacency List - O(n^2) Time and O(n) Space****

> Analyze the problem using [Graphs](https://www.geeksforgeeks.org/introduction-to-graphs-data-structure-and-algorithm-tutorials/). Initialize ****indegree**** and ****outdegree**** of every vertex as 0.
> 
> - If A knows B, draw a ****directed edge**** from A to B, increase indegree of B and outdegree of A by 1.
> - Construct all possible edges of the graph for every possible pair [i, j].
> - There are ****n********C********2**** pairs. If a celebrity is present in the party, there will be one node in the graph which has the outdegree as ****zero**** and indegree equals to ****N-1.**** 

****Follow the steps below to solve the problem:****

- Create two arrays ****indegree**** and ****outdegree****, to store the indegree and outdegree
- Run a nested loop, the outer loop from 0 to n and inner loop from ****0 to n****.
- For every pair ****i, j**** check if ****i**** knows ****j**** then increase the outdegree of ****i**** and indegree of ****j****.
- For every pair ****i, j**** check if ****j**** knows ****i**** then increase the outdegree of ****j**** and indegree of ****i****.
- Run a loop from ****0 to n**** and find the id where the indegree is ****n-1**** and outdegree is ****0****.

// C++ program to find celebrity

#include <bits/stdc++.h>

using namespace std;

​

// Function to find the celebrity

int celebrity(vector<vector<int>> & mat) {

    int n = mat.size();

​

    // indegree and outdegree array

    vector<int> indegree(n, 0), outdegree(n, 0);

​

    // query for all edges

    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            int x = mat[i][j];

​

            // set the degrees

            outdegree[i] += x;

            indegree[j] += x;

        }

    }

​

    // find a person with indegree n-1

    // and out degree 0

    for (int i = 0; i < n; i++)

        if (indegree[i] == n - 1 && outdegree[i] == 0)

            return i;

​

    return -1;

}

​

int main() {

    vector<vector<int> > mat = {{ 0, 1, 0 },

                                { 0, 0, 0 },

                                { 0, 1, 0 }};

    cout << celebrity(mat);

    return 0;

}

  
**Output**

1

### ****[Better Approach] - Using Stack - O(n) Time and O(n) Space****

> Some observations are based on [****Stack****](https://www.geeksforgeeks.org/stack-data-structure/) ****Based elimination technique**** :
> 
> - If A knows B, then A can't be a celebrity. Discard A, and __B may be celebrity__.
> - If A doesn't know B, then B can't be a celebrity. Discard B, and __A may be celebrity__.
> - Repeat above two steps till there is only one person.
> - Ensure the remained person is a celebrity.

****Follow the steps below to solve the problem:****

- Create a ****stack**** and push all the ****ids**** in the stack.
- Run a loop while there are more than 1 element in the stack.
- Pop the top two elements from the stack (represent them as ****A and B****)
- If A knows B, then A can't be a celebrity and push B in the stack. Else if A doesn't know B, then B can't be a celebrity push A in the stack.
- Assign the remaining element in the stack as the celebrity.
- Run a loop from 0 to n-1 and find the count of persons who knows the celebrity and the number of people whom the celebrity knows.
    - If the count of persons who knows the celebrity is n-1 and the count of people whom the celebrity knows is 0 then return the id of the celebrity else return -1.

// JavaScript program to find celebrity

​

// Function to find the celebrity

function celebrity(mat) {

    let n = mat.length;

    let st = [];

​

    // Push everybody in stack

    for (let i = 0; i < n; i++)

        st.push(i);

​

    // Find a potential celebrity

    while (st.length > 1) {

​

        let a = st.pop();

        let b = st.pop();

​

        // if a knows b

        if (mat[a][b] !== 0) {

            st.push(b);

        }

        else {

            st.push(a);

        }

    }

​

    // Potential candidate of celebrity

    let c = st.pop();

​

    // Check if c is actually

    // a celebrity or not

    for (let i = 0; i < n; i++) {

        if(i === c) continue;

​

        // If any person doesn't

        // know 'c' or 'c' doesn't

        // know any person, return -1

        if (mat[c][i] !== 0 || mat[i][c] === 0)

            return -1;

    }

​

    return c;

}

​

// Driver Code

let mat = [ [0, 1, 0],

            [0, 0, 0],

            [0, 1, 0] ];

console.log(celebrity(mat));

  
**Output**

1

### ****[Expected Approach] - Using Two Pointers - O(n) Time and O(1) Space****

> The idea is to use [two pointers](https://www.geeksforgeeks.org/two-pointers-technique/), one from start and one from the end. Assume the start person is A, and the end person is B. If A knows B, then A must not be the celebrity. Else, B must not be the celebrity. At the end of the loop, only one index will be left as a celebrity. Go through each person again and check whether this is the celebrity. 

****Follow the steps below to solve the problem:****

- Create two indices i and j, where i = 0 and j = n-1
- Run a loop until ****i**** is less than ****j****.
- Check if ****i**** knows j, then ****i**** can't be a celebrity. so increment ****i****, i.e. i++
- Else ****j**** cannot be a celebrity, so decrement ****j****, i.e. j--
- Assign ****i**** as the celebrity candidate
- Now at last check whether the candidate is actually a celebrity by re-running a loop from 0 to n-1  and constantly checking if the candidate knows a person or if there is a candidate who does not know the candidate.
    - Then we should return -1. else at the end of the loop, we can be sure that the candidate is actually a celebrity.

// C++ program to find celebrity

#include <bits/stdc++.h>

using namespace std;

​

// Function to find the celebrity

int celebrity(vector<vector<int>> & mat) {

    int n = mat.size();

​

    int i = 0, j = n - 1;

    while (i < j) {

        // j knows i, thus j can't be celebrity

        if (mat[j][i] == 1) 

            j--;

​

        // else i can't be celebrity

        else

            i++;

    }

​

    // i points to our celebrity candidate

    int c = i;

​

    // Check if c is actually

    // a celebrity or not

    for (i = 0; i < n; i++) {

        if(i == c) continue;

​

        // If any person doesn't

        // know 'c' or 'c' doesn't

        // know any person, return -1

        if (mat[c][i] || !mat[i][c])

            return -1;

    }

​

    return c;

}

​

int main() {

    vector<vector<int> > mat = {{ 0, 1, 0 },

                                { 0, 0, 0 },

                                { 0, 1, 0 }};

    cout << celebrity(mat);

    return 0;

}

  
**Output**

1