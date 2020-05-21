# 백준 9012번 문제

* 날짜 : 20.04.13
* 언어 : java
* IDE : IntelliJ IDEA community 

## 요구사항

<img src="/doc/backjoon/stack/p9012/requirement.png"> 

## 풀이

괄호 문제는 대표적인 stack 문제이다.  하지만, 위 문제는 하나의 괄호에 대해서만 이슈를 삼고 있다.  이때는 int형 하나만으로 쉽게 풀 수 있다.

---
1. 열린 괄호면, +1한다.
2. 닫힌 괄호면, -1한다.  그리고 나서 합이 0보다 낮은 값이면 잘못된 괄호임을 반환한다.
3. 모든 문자열 탐색 후 sum이 0이면, 올바른 괄호임을, 0이 아니면 잘못된 괄호임을 반환한다.
---

하나의 스택이라 생각하면 된다.  스택으로 하면,  열린 괄호면 push하고 닫힌 괄호면 스택의 top이 열린 괄호면 pop한다.  이것이 하나의 타입만 생각하면 되므로, 간단하게 sum으로 판단할 수 있다.

예를 들어보자.<br>
string = (())()         
    
```
index = 0  -> '('
sum = 1
```

```
index = 1  -> '('
sum = 2
```

```
index = 2  -> ')'
sum = 1
```

```
index = 3  -> ')'
sum = 0
```

```
index = 4  -> '('
sum = 1
```

```
index = 5  -> ')'
sum = 0   따라서, 올바른 괄호열
```