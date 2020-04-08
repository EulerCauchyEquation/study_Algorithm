# 백준 11053번 문제

* 날짜 : 20.04.03
* 언어 : java
* IDE : IntelliJ IDEA community 

## 요구사항

<img src="/doc/backjoon/dynamic/p11053/requirement.png"> 

## 풀이


경우의 수를 생각하면서 하는 문제이므로 기본적으로 DFS 문제이다.     경우의 수를 따져보자

---
case 1. 선택한다.  (단, 현재 비교할 원소보다 기준 원소보다 클 때)<br>
case 2. 스킵한다.

---

예를 보자.  수열 = {10, 25 ,15 ,20 } 일 때, 어떤 경우의 수가 있을까.

---
1. 10 - 25<br>
2. 10 - 15 - 20

---

이렇게 두 가지 경우가 있다.  2번 경우를 보면 25에서 선택하지 않고 스킵한 case 2 경우이다.

이런식으로, DFS가 가능하다.  하지만, 이 방법은 시간 복잡도 2^n이다. 따라서, 조금 더 빠른 알고리즘이 필요하다.


이 문제는 동적 계획법이 가능하다.  기준 원소에 따라서 memoization을 쓸 수 있다.<br>
점화식.
```
dfs(n, 기준 값) = Max (
dfs(n + 1, sequence[n] ) + 1,    ( 단, 기준 값 < sequence[n] )   // case 1
dfs(n + 1) );                                                                                       // case 2
```

이 방법은 시간 복잡도 n^2의 효과를 볼 수 있다.

다른 방법으로는 이분 탐색을 이용하는 방법이 있다.  
수열을 처음부터 확인하는 것은 동일한데 이분탐색을 이용하여 LIS을 유지하며 삽입하는 방식이다.   자리를 찾는데 lower_bound를 이용하기 때문에 총 O(n log n)의 시간 복잡도를 가지게 된다. 과정은 간단하다.

---
1. 리스트를 하나 생성하고, 맨 앞에 있는 값은 삽입한다. <br>
2. 리스트의 마지막 원소와 현재 보고있는 수열의 원소를 비교하여 수열의 원소가 더 크면 그대로 뒤에 삽입하고,  작으면 lower_bound를 통하여 그 자리의 값과 현재 보고있는 수열의 원소와 교체한다.

---

예를 들어보겠다. 


```
sequence = {10, 5, 35,10, 25}   list = {}   현재 수열 원소 = 10
처음 원소이므로, 그대로 삽입
교체 후,  list = {10}
```

```
sequence = {10, 5, 35,10, 25}   list = {10}   현재 수열 원소 = 5
10 > 5이므로,  lower_bound(5)를 통해 10과 교체
교체 후,  list = {5}
```

```
sequence = {10, 5, 35,10, 25}   list = {5}   현재 수열 원소 = 35
5 < 35  이므로,  배열의 원소 뒤에 삽입
교체 후,  list = {5, 35}
```

```
sequence = {10, 5, 35,10, 25}   list = {5, 35}   현재 수열 원소 = 10
35 > 10이므로,  lower_bound(10)를 통해 35와 교체
교체 후,  list = {5, 10}
```

```
sequence = {10, 5, 35,10, 25}   list = {5, 10}   현재 수열 원소 = 25
10 < 25  이므로,  배열의 원소 뒤에 삽입
교체 후,  list = {5, 10, 25}

답 : 3
```

이분 탐색 방법은 LIS원소와는 무관하다.  단지 길이만 알고 싶을 때 쓸 수 있는 알고리즘이다.

추가로,  lower_bound 설명이다.
https://wootool.tistory.com/62
