# Bellman Ford (벨만 포드)

* 한 노드에서 다른 노드(또는 자기 자신)까지 최단 거리를 구하는 알고리즘
* 간선의 가중치가 음수인 경우에도 구할수 있다.


## Bellman Ford(벨만 포드) vs Dijkstra(다익스트라)

|알고리즘|벨만 포드|다익스트라|
|:---:|:---:|:---:|
|시간 복잡도|O(VE)|O(ElogV)|
|특징|음수 간선이 있어도 최적의 해를 찾을 수 있다. (음수 간선의 순환을 감지할 수 있기 때문)|음수 간선이 없다면 최적의 해를 찾을 수 있다. (음수 간선이 있다면 최적의 해를 구할수 없음)|
|구하는 방법|(정점-1)번의 매 단계마다 모든 간선을 전부 확인하면서 모든 노드간의 최단 거리를 구해나간다.|매번 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하여 한 단계씩 최단 거리를 구해나간다.|
|차이점|매 반복마다 모든 간선을 확인|방문하지 않은 노드 중 최단 거리와 가장 가까운 노드만을 방문|


## 벨만 포드 알고리즘 수행 과정
1. 출발 노드 설정
2. 최단 거리 테이블 초기화
3. 다음 과정을 (정점-1)번 반복한다.
    1. 모든 간선 E개를 하나씩 확인
    2. 각 간선을 거쳐 다른 노드로 가는 최소 비용을 계산
* 만약 음수 간선 순환이 발생하는지 체크하고 싶다면 3번 과정을 한번더 수행한다. -> 이때 최단 거리 테이블이 갱신된다면 음수 간선 순환이 존재하는 것이다.


## python 코드

```python
import sys
input = sys.stdin.readline

def bellman_ford() :
    for i in range(n) :
        for (s, e, t) in edges :
            if times[e] > times[s] + t :
                times[e] = times[s] + t
                # n번째에 값이 또 갱신된다면 사이클이 존재한다는 뜻
                if i == n-1 :
                    return True
    return False

# 정점, 가중치가 양수인 간선 수, 가중기차 음수인 간선 수
n, m, w = map(int, input().rstrip().split())

# 간선 저장
edges = []

# times를 갱신하기 위해서는 float('inf')로 하면 안된다
# float('inf')는 매우 큰 "상태"를 의미 -> 연산이 불가능하다.
times = [1e9]*(n+1)

# 가중치가 양수이면서 양방향인 간선
for _ in range(m) :
    s, e, t = map(int, input().rstrip().split())
    edges.append((s, e, t))
    edges.append((e, s, t))
# 가중치가 음수이면서 단방향인 간선
for _ in range(w) :
    s, e, t = map(int, input().rstrip().split())
    edges.append((s, e, -t))

if bellman_ford() :
    print('음수 간선 순환이 존재합니다.')
else :
    print('음수 간선 순환이 존재하지 않습니다.')
```