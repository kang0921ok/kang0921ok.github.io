---
layout: default
title: Algorithm
nav_order: 4
has_children: false
permalink: /docs/algorithm
---

# Algorithm

알고리즘 문제를 풀면서 기억해두면 좋을 것들을 정리

## Arrays & Strings

- 2pointer
- 라빈 카프(rabin-karp) algorithm
    - [implement-strstr leetcode](https://leetcode.com/problems/implement-strstr)

## Math

- 에라토스테네스의 체
    - 배수들은 모두 지워 나간다.
        - 2는 남기고, 2의 배수들을 모두 지움 (2*2=4, 2*3=6, 2*4=8...)
        - 3은 남기고, 3의 배수들을 모두 지움 (3*2=6, 3*3=9, 3*4=12...)
        - 4는 앞에서 이미 지워졌음
        - 5는 남기고, 5의 배수들을 모두 지움
        - 6은 앞에서 이미 지워졌음
        - 7은 남기고, 7의 배수들을 모두 지움
        - 핵심: N까지 체크하면되는데, 제곱근(Math.sqrt(N))까지만 체크하면 되는게 포인트
    - 남은 숫자들은 소수
    - [설명](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)
    - [count-primes leetcode](https://leetcode.com/problems/count-primes)

## Others
- Hamming distance 
   - 2개의 input을 비트 단위로 비교하여 다른 값 (문자가 될 수도 있음)
     - e.g) 7 -> 1011, 5 -> 0101 
     - 1011
     - 0101
     - 1~3번째 다르고 마지막은 같음, 즉 Hamming distance는 3개 (다른값)
   - int일때 처리 아이디어
     - input1 ^ input2 (XOR 처리)
       - XOR => 같으면 0, 다르면 1
     - Integer.bitCount(input1 ^ input2)
       - 이진수 내 1의 개수를 카운트하여 리턴
   - [Hamming-distance leetcode](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/762/)