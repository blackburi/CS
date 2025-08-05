# 투 포인터 (Two Pointers)
* list에 순차적으로 접근해야 할 때, 2개의 점의 위치를 기록하면서 처리하는 알고리즘
* 대표적으로 특정한 합을 가지는 부분 연속 수열 찾기, 정렬되어 있는 두 리스트의 합집합 구하기 등의 문제들을 풀 때 사용한다.

## 특정한 합을 가지는 부분 연속 수열 찾기
* 시작점~끝점 사이의 모든 수의 합을 구하는데, 끝점을 오른쪽으로 이동하면 합은 항상 증가하고, 시작점을 오른쪽으로 이동하면 합은 항상 감소한다. (이때 존재하는 모든 수들은 0이상의 실수이다.)

    ```python
    N = int(input())  # 데이터의 개수
    M = int(input())  # 찾고자 하는 부분합
    data = list(map(int, input().split()))  # 전체 수열

    cnt = 0
    interval_sum = 0
    end = 0

    # start를 차례대로 증가시키며 반복
    for start in range(N):
        # end를 가능한 만큼 이동시키기
        while interval_sum < M and end < N:
            interval_sum += data[end]
            end += 1
        # 부분합이 M일 때 카운트 증가
        if interval_sum == M:
            cnt += 1
        interval_sum -= data[start]

    print(cnt)

    """
    <tc>
    5 : 숫자의 총 개수
    5 : 원하는 부분 합
    1 2 3 2 5 : 숫자 list

    <result>
    3 : 부분 합의 개수
    """
    ```

## 정렬되어 있는 두 리스트의 합집합 구하기
1. 정렬된 리스트 A, B를 입력받는다.
2. 리스트 A에서 처리되지 않은 원소 중 가장 작은 원소를 i가 가리키도록 한다.
3. 리스트 B에서 처리되지 않은 원소 중 가장 작은 원소를 j가 가리키도록 한다.
4. A[i]와 B[j] 중에서 더 작은 원소를 결과 리스트에 담는다.
5. 리스트 A, B에서 더이상 처리할 원소가 없을 때까지 1~4번의 과정을 반복한다.

```python
# 사전에 정렬된 리스트 A와 B 선언
n, m = map(int, input().split())  # 리스트 A, B의 크기
a = list(map(int, input().split()))
b = list(map(int, input().split()))

# 리스트 A와 B의 모든 원소를 담을 수 있는 크기의 결과 리스트 초기화
result = [0] * (n + m)
i = 0
j = 0
k = 0

# 모든 원소가 결과 리스트에 담길 때까지 반복
while i < n or j < m:
    # 리스트 B의 모든 원소가 처리되었거나, 리스트 A의 원소가 더 작을 때
    if j >= m or (i < n and a[i] <= b[j]):
        # 리스트 A의 원소를 결과 리스트로 옮기기
        result[k] = a[i]
        i += 1
    # 리스트 A의 모든 원소가 처리되었거나, 리스트 B의 원소가 더 작을 때
    else:
        # 리스트 B의 원소를 결과 리스트로 옮기기
        result[k] = b[j]
        j += 1
    k += 1

# 결과 리스트 출력
for i in result:
    print(i, end=' ')

"""
<tc>
3 4 : 두 리스트의 길이
1 3 5 : list 1
2 4 6 8 : list2

<result>
1 2 3 4 5 6 8 
"""
```