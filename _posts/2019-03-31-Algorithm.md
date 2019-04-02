---
layout: post
title: "알고리즘 연습"
description: 알고리즘
image: '\images\bg.jpg'
category: 'Algorithm'
tag:
 - Algorithm
introduction: 알고리즘 연습
---

# 에스토스테네스의 체

2부터 N까지의 모든 소수의 합을 구하세요.
N이 7이라면 {2,3,5,7} = 17을 출력 하시면 됩니다.
N의 범위는 2이상 10,000,000이하 입니다.
효율성 테스트의 모든 시간 제한은 1초입니다.

```c++
#include <iostream>
#incldue <vector>

using namespace std;
int number[10000001];
long long solution(int N) {
    long long answer = 0;
    for(int i = 2; i < 10000001; i++){
        number[i] = i;
    }
    for(int i= 2; i < 1000001; i++){
        if(number[i] == 0) continue;
        for(int j = i + i; j < 10000001;  j += i){
            number[j] = 0;
        }
    }
    
    for(int i = 2; i <= N; i++){
        if(number[i] != 0){
            answer += number[i];
        }
    }
    return answer;
}
```

# 2n타일링

가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

- 타일을 가로로 배치 하는 경우
- 타일을 세로로 배치 하는 경우

- 가로의 길이 n은 60,000이하의 자연수 입니다.
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

```c++
#include <string>
#include <vector>

using namespace std;
//int number = 60001;
int result[60001];
int dp(int n){
    if(n == 1) return 1;
    if(n == 2) return 2;
    
    if(result[n] == 0){
       return result[n] = (dp(n-1) + dp(n-2)) % 1000000007;
    }
    else
    {
        return result[n];
    }
    
}
int solution(int n) {
    int answer;
    answer = dp(n);
    return answer;
}
```

dfs : stack bfs : queue