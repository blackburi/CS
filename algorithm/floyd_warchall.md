# floyd warchall (플로이드 워셜)

* 모든 정점 사이의 최단 경로를 찾는 탐색 알고리즘

```python
import sys

INF = sys.maxsize

def Floyd_Warshall() :
    # 최단 경로를 담는 배열
    dist = [[INF]*n for _ in range(n)]

    # 최단 경로를 담는 배열 초기화
    for i in range(n) :
        for j in range(n) :
            dist[i][j] = graph[i][j]

    # 거치는 점
    for k in range(n) :
        # 시작점
        for i in range(n) :
            # 도착점
            for j in range(n) :
                # k를 거쳤을 때의 경로가 더 적은 경로
                if dist[i][j] > dist[i][k] + dist[k][j] :
                    dist[i][j] = dist[i][k] + dist[k][j]

    return dist

# 정점의 수
n = 4
# 정점과 정점 사이의 거리
graph = [
    [0, 2, INF, 4],
    [2, 0, INF, 5],
    [3, INF, 0, INF],
    [INF, 2, 1, 0]
]

dist = Floyd_Warshall()

for i in range(n) :
    for j in range(n) :
        print(dist[i][j], end='')
    print()
```