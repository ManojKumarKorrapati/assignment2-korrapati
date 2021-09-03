# Manoj Kumar Korrapati
#### Monaco 

Monaco, officially Principality of Monaco, sovereign principality located along the **Mediterranean Sea** in the midst of the resort area of the Côte d’Azur (French Riviera). It also host **Formula 1** race every year.
***
###### Directions to Monaco
1. Get a cab to Kansas International Airport from maryville.
2. Take a flight to Monaco International Airport.
    1. Get contact with Hotal and get a room.
    2. Check with local transport to get vehicle to the airport.

Check List to visit Monaco.

* Map of the city.
* Camera.
* Watter Bolttle.
* F1 race tickets (It's the best time to visit Monaco).
* Multy Currency Travel Card.

**[To know more about me](AboutMe.md)**

***

Below are the few Food item I would recommend every one to try in India.
| Food | Location | Price |
| :--- | :--- | :--- |
| Shavarma | DLF Gachibouli, Hyderabad, India | 1.45$ | 
| Mandi | Moosapet, Hyderabad, India | 4.00$|
| PaniPuri | EveryStreet Courner in India :) | 0.14$ | 

***

##### My two Famous Quotes

> I have no special talent. I am only passioately curious. ---- *Albert Einstein*
>
> To suceceed in life, you need two things: ignorance and confidencez. ---- *Mark Twain*

***
Sparse Table

>Sparse Table is a data structure, that allows answering range queries. It can answer most range queries in O(logn), but its true power is answering range minimum queries (or equivalent range maximum queries). For those queries it can compute the answer in O(1) time.
>
>In computer science, a range minimum query (RMQ) solves the problem of finding the minimal value in a sub-array of an array of comparable objects. Range minimum queries have several use cases in computer science, such as the lowest common ancestor problem and the longest common prefix problem (LCP).
>
>**Definition**
>
>Given an array A[1 … n] of n objects taken from a totally ordered set, such as integers, the range minimum query RMQA(l,r) =arg min A[k] (with 1 ≤ l ≤ k ≤ r ≤ n) returns the position of the minimal element in the specified sub-array A[l … r].
>
>For example, when A = [0,5,2,5,4,3,1,6,3], then the answer to the range minimum query for the sub-array A[3 … 8] = [2,5,4,3,1,6] is 7, as A[7] = 1.
>
>In a typical setting, the array A is static, i.e., elements are not inserted or deleted during a series of queries, and the queries to be answered on-line (i.e., the whole set of queries are not known in advance to the algorithm). In this case a suitable preprocessing of the array into a data structure ensures faster query answering. A naïve solution is to precompute all possible queries, i.e. the minimum of all sub-arrays of A, and store these in an array B such that B[i, j] = min(A[i…j]); then a range min query can be solved in constant time by array lookup in B. There are Θ(n²) possible queries for a length-n array, and the answers to these can be computed in Θ(n²) time by dynamic programming.

For reference <https://en.wikipedia.org/wiki/Range_minimum_query>

Code for Precomputation
```
int st[MAXN][K + 1];
for (int i = 0; i < N; i++)
    st[i][0] = f(array[i]);

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = f(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);
```

Code for Range Sum Queries
```
long long st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = st[i][j-1] + st[i + (1 << (j - 1))][j - 1];
```

To answer the sum query for the range [L,R]
```
long long sum = 0;
for (int j = K; j >= 0; j--) {
    if ((1 << j) <= R - L + 1) {
        sum += st[L][j];
        L += 1 << j;
    }
}
```

Code for Range Minimun Queries (RMQ)

minimum of the range [L,R] 

Using min(st[L][j],st[R−2j+1][j]) where j=log2(R−L+1)
```
int log[MAXN+1];
log[1] = 0;
for (int i = 2; i <= MAXN; i++)
    log[i] = log[i/2] + 1;

int st[MAXN][K + 1];

for (int i = 0; i < N; i++)
    st[i][0] = array[i];

for (int j = 1; j <= K; j++)
    for (int i = 0; i + (1 << j) <= N; i++)
        st[i][j] = min(st[i][j-1], st[i + (1 << (j - 1))][j - 1]);

int j = log[R - L + 1];
int minimum = min(st[L][j], st[R - (1 << j) + 1][j]);
```        

Code Reference <https://cp-algorithms.com/data_structures/sparse-table.html>
