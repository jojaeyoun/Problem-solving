## 기본예제 BFS 
<br>
 
### 1. 설명
 
 이 글은 동빈나님의 블로그([https://m.blog.naver.com/ndb796/221230944971](https://m.blog.naver.com/ndb796/221230944971))를 참고하여 정리하였다. (추천!!)
 
BFS는 넓이 우선 탐색이라는 의미이며, 현재 노드에서 가장 가까운 노드를 먼저 탐색하기 때문에 DFS와 차이가 있다.

BFS알고리즘의 동작은 다음과 같다.

    1.큐에서 노드 하나를 꺼낸다.
    2.해당 노드에 연결된 노드 중 방문하지 않는 노드를 방문처리하고,큐에 넣는다.
    3.큐가 비어질때까지 반복한다.

BFS에서는 다음과 같은것들을 신경써줘야한다.
 
  
+ 방문한 노드는 방문처리를 해준다.
+ queue를 활용하여 구현한다. 
+ 노드의 연결관계를 잘 설정해주어야한다.

BFS가 탐색하는 순서를 출력하는 알고리즘을 통해 BFS의 기초를 알아보자.
 

### 3. 구현

```cpp

#include <iostream>
#include <vector>
#include <queue>

using namespace std;


bool visited[8] = { 0 };
vector<int> a[8];

void bfs(int x)
{
	queue<int> q;
	q.push(x);
	visited[x] = true;
	
	while (q.empty() == false)
	{
		int index = q.front();
		q.pop();
		cout << index;

		for (int i = 0; i < a[index].size(); i++)
		{
			if (visited[a[index][i]] == false)
			{
				q.push(a[index][i]);
				visited[a[index][i]] = true;
			}
		}

	}
}

int main()
{
	a[1].push_back(2);
	a[1].push_back(3);

	a[2].push_back(1);
	a[2].push_back(4);
	a[2].push_back(5);

	a[3].push_back(1);
	a[3].push_back(6);
	a[3].push_back(7);

	bfs(1);
	return 0;
}
```
### 4. BFS 참고문제

다음 문제를 풀어보자!

+ 바이러스 : [https://www.acmicpc.net/problem/2606](https://www.acmicpc.net/problem/2606)

+ 단지번호 붙이기 : [https://www.acmicpc.net/problem/2667](https://www.acmicpc.net/problem/2667)

+ 보물섬 : [https://www.acmicpc.net/problem/2589](https://www.acmicpc.net/problem/2589)

+ 토마토 : [https://www.acmicpc.net/problem/7576](https://www.acmicpc.net/problem/7576)

+ N-Queen : [https://www.acmicpc.net/problem/9663](https://www.acmicpc.net/problem/9663)

  

  
  
