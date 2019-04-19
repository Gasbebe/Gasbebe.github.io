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

# 문자열 매칭

```c++
#include <iostream>
#include <string>

using namespace std;

int findString(string parent, string pattern){
    int parentSize = parent.size;
    int patternSize = pattern.size;
    
    //O(n^2)
    for(int i = 0; i <= parentSize - patterntSize; i++){
        for(int j = 0 j < i; j++){
            if(parent[i+j] != pattern[j]){
                finded = false;
                break;
            }
        }
        if(finded){
            return i;
        }
    }
}
int main(void){
    
}
```







```c++
#include <iostream>
#include <stack>

using namespace std;

int n, S[1000000];

void swap(int a, int b){
    int temp = S[a];
    S[a] = S[b];
    S[b] = t;
}
//오름차순의 경우
bool compare(int a, int b){
    return a<b;
}

//내림차순의 경우
bool compare(int a, int b){
    return a>b;
}

//구조체
bool compare(Point a, Point b){
    return a.x < b.x;
}

//구조체
bool compare(Point a, Point b){
    if(a.x == b.x) return a.y < b.y;
    else return a.x < b.x;
}

void main(){
 return;    
}
```



# 탐색기반

선형구조, 비선형구조 low_bound, uper_bound, 

비선형구조란 i번째 원소를 탐색한 다음 그 원소와 연결된 다른 원소를 탐색하려고 할때 열거개의 원소가 존재하는 탐색구조를 말한다 일반적으로 자료가 트리나 그래프로 구성되어 있을 경우를 비선형구조라 하고 이러한 트리나 그래프의 모든 정점을 탐색하는 것을 비선형 탐색이라고 이해하면 된다

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespce std;
class Node{
    int data;
}

class BinaryTree{
    int value;
    Node *leftNode;
    Node *rightNode;
    
    public:
    	void PreOrder(){
        	
    	}
    
    	void PostOrder(){
        
	    }
}
```



DP

brute force approcach  모든 경우

divide and Conquer approach 모든 문제를 쪼개서 해결 - 문제가 독립적일때

dynamic programming approach 동적계획법 - 주어진 문제를 하위로 나눠어서 해결

동적 프로그래밍은 문제를 작은 문제로 쪼개서 푼다는 의미에서 divide and conquer와 비슷하지만

하위 문제가 서로 종속성을 가질 때 사용

- 가능한 해답이 무수히 존재하며
- 각각의 해답은 숫자 등의 크기가 있는 값을 가짐
- 가장 크거나 가장 작은 최적의 값을 가지는 해답을 찾을 수 있고.
- 그런 해답을 최적화 문제의 `최적해` 라고 부름

다이나믹 프로그래밍 단계

1. 최적해에 대한 구조적 특징 분석
2. 최적해를 값을 구하기 위한 재귀적 정의가 가능한지 확인
3. 하위문제로 부터 최적해의 값을 계산
4. 계산된 값으로 부터 최적해를 만듦

문제해결방법으로 최적화 문제를 해결할 때 문제의 크기를 작게 나누어서 해답을 찾으며 이떄 작은 문제들은 서로 연관성을 가진다. 동적계획법을 적용하기 위해서는 최적해 구조와 재귀 구조를 가져야함

조립을 통해 제품이 완성될 때 여러 개의 과정과 여러 개의 라인이 존재할 때 최적의 조합을 찾아 가장 빠른 시간과 경로를 동적계획법을 이용하여 해결





greedy approach

BFS

그래프

```c++
#include<iostream>
#include<queue>
#include<vector>

using namespace std;

int number = 7;
int checked[7];
vector<int> a[8];

void bfs(int start){
    queue<int> q;
  	q.push(start);
    checked[start] = true;
    while(!q.empty()){
        int x = q.front();
        q.pop();
        printf("%d", x);
        for(int i= 0; i < a[x].size(); i++){
            int y = a[x][i];
            if(!checked[y]){
                q.push(y);
                checked[y] = true;
            }
        }
    }
}
/*
     1
    / \
    2-3
   /\  /\
   4-5 6-7
   1->2->3->4->5->6->7
*/
int main(void){
    
    a[1].push_back(2);
    a[2].push_back(1);
    
    a[1].push_back(3);
    a[3].push_back(1);
    
    a[2].push_back(3);
    a[3].push_back(2);
    
    a[2].push_back(4); 
    a[4].push_back(2);
    
    a[2].push_back(5);
    a[5].push_back(2);
    
    a[4].push_back(5);
    a[5].push_back(4);
    
    a[3].push_back(6);
    a[6].push_back(3);
    
    a[3].push_back(7);
    a[7].push_back(3);
    
    a[6].push_back(7);
    a[7].push_back(6);
    
    bfs(1);
    return 0;
}
```



dfs(재귀, 스택)

1. 스택의 최상단 노드를 확입하니다.
2. 최상단 노드에게 방문하지 않은 인접 노드가 있으면 그 노드를 스택에 넣고 방문처리합니다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 뺍니다 

```c++
#include<iostream>
#include<vector>
#include<algorithm>
#include<stack>
#include<vector>

using namespace std;

int number = 7;
int checked[7];
vector<int> a[8];

void RecursionDfs(int x){
    if(checked[x]) return;
    checked[x] = true;
    cout << x << ' ';
    for(int i = 0; i< a[x].size(); i++){
        int y = a[x][i];
        dfs(y);
    }
}
void dfs(int start){
    stack<int> s;
    s.push(start);
    
    while(!s.empty()){
        int d = s.top();
        s.pop();
        
        for(int i = 0; i < a[x].size(); i++){
            
        }
    }
}

/*
     1
    / \
    2-3
   /\  /\
   4-5 6-7
   1->2->3->6->7->4->5   
*/
int main(){
    
}
```





```c++
//연습

bool compare(int a, int b){
    return a > b;
}

bool compare(int a ,int b){
    return a < b;
}

bool compare(Postion p1, Position p2){
    return p1.x > p2.x;
}
```



## Union find

활용도가 높은 알고리즘, 크루스칼 알고리즘에도 쓰임

```c++
#inclued <iostream>

int getParent(int parent[], int x){
    if(parent[x] == x) return x;
    return parent[x] = getParent(parent, parent[x]);
}

int unionParent(int parent[], int a, int b){
    a = getParent(parent, a);
    b = getParent(parent, b);
    
    if(a < b) parent[b] = a;
    else parent[a] = b;
}

int findParent(int parent[], int a, int b){
    a = getParent(parent, a);
    b = getParent(parent, b);
    
    if(a == b) return 1;
    else return 0;
}

```



1. preoder traversal
   1. 먼저 자기 자신을 처리한다.
   2. 왼쪽 자식을 방문합니다.
   3. 오른쪽 자식을 방문합니다.
2. inorder traversal
   1. 왼쪽 자식을 방문 합니다
   2. 먼저 자기자신을 처리합니다
   3. 오른쪽 자식을 방문합니다
3. postorder traversal
   1. 왼쪽 자식을 방문합니다
   2. 오른쪽 자식을 방문합니다
   3. 자기 자신을 처리합니다



```c++
#include <iostream>
#include <vector>

using namespace std;
//다익스트라 알고리즘, 흔히 인공위성, GPS 많이 쓰입니다.
//다이나믹, 그리드 알고리즘으로 분류 된다.
//1 출발 노드를 설정합니다.
//2 출발 노드를 기준으로 각 노드의 최소 비용을 저장합니다.
//3 방문하지 않은 노드 중에서 가장 비용이 적은 노드를 선택합니다.
//4 해당 노드를 거쳐서 특정한 노드로 가느 경우를 고려하여 최소 비용을 갱신합니다.
//5 위 과정에서 3번 ~ 4번을 반복합니다.

//2차원 배열사용 특정 행에서 열로 가는 비용
int INF = 9999;
int number = 6;

int a[6][6] ={
    {0,2,5,1,INF,INF},
    {2,0,3,2,INF,INF},
    {5,3,0,3,1,5},
    {1,2,3,0,1,INF},
    {INF,INF,1,1,0,2},
    {INF,INF,5,INF,2,0}
};

bool v[6]; //방문한 노드
int d[6]; //최단거리
//가장 최소 거리를 가지는 정점을 반환합니다.
int getSmallIndex(){
    int min = INF;
    int index = 0;
    for(int i = 0; i < number; i++){
        if(d[i] < min && !v[i]){
            min = d[i];
            index = i;
        }
    }
    return index;
}

void dijkstra(int start){
    for(int i = 0; i < number; i++){
        d[i] = a[start][i];
    }
    v[start] = true;
    for(int i = 0; i< number -2; i++){
        for(int j= 0; j <6; j++){
            
        }
    }
}
int main(){
    dijkstra(1);
    
    for(int i = 0; i < 6; i++){
        cout << d[i] << endl;
    }
}

```



---

길이가 n인 배열에 1부터 n까지 숫자가 중복 없이 한 번씩 들어 있는지를 확인하려고 합니다.
1부터 n까지 숫자가 중복 없이 한 번씩 들어 있는 경우 true를, 아닌 경우 false를 반환하도록 함수 solution을 완성해주세요.

##### 제한사항

- 배열의 길이는 10만 이하입니다.
- 배열의 원소는 0 이상 10만 이하인 정수입니다.

```c++
#include <vector>
#include <iostream>
using namespace std;
int number[100001];
bool solution(vector<int> arr)
{
    bool answer = true;
    for(int i = 0; i < arr.size(); i++){
        number[arr[i]] = arr[i];
    }
    
    for(int i = 1; i < arr.size(); i++){
        if(number[i] == 0){
          return answer = false;
        }
    }
    return answer;
}
//==== solution2
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

bool solution(vector<int> arr)
{
    bool answer = true;
	sort(arr.begin(), arr.end());
    
    for(int i  =0; i < arr.size(); ++i){
        if(arr[i] != i+1){
            return false;
        }
    }
    
    return true;
}
```





# 자릿수 더하기

```c++
while(n != 0){
            sum += (n % 10);
            n = n/10;
}
```



# 숫자 뒤집기

```
   public static int flip(int num){
        int result=0;
        while(num!=0){
            result= result * 10 + num % 10;
            num /= 10;
        }
        return result;
    }
```

