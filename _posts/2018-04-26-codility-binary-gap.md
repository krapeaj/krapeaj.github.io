---
layout: post
title: Codility Lessons - Binary Gap
category: Algorithms
tags:
---

[Codility Lessons - BinaryGap](https://app.codility.com/programmers/lessons/1-iterations/binary_gap/)

I looped through the character array and counted the maximun number of zeros.

```java
class Solution {
    public int solution(int N) {
        String s = Integer.toBinaryString(N);
        long count = 0;
        long maxCount = 0;
        for(char c : s.toCharArray()){
            if(c == '0'){
                count++;
                continue;
            }
            if(count > maxCount){
                maxCount = count;
            }
            count = 0;
        }
        return (int)maxCount;
    }
}
```
