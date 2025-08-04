# DP

* Dynamic Programming (동적 계획법)
* 복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법
* 부분 문제 반복(Overlapping subproblems)과 최적 부분 구조(Optimal substructure)를 가지고 있는 알고리즘을 일반적인 방법에 비해 더욱 적은 시간 내에 풀 때 사용

## DP의 방식
1. Top-Down (Memoization) 방식
    * 한 번 계산한 결과를 메모리 공간에 저장
        * 같은 문제를 다시 호출하면, 저장한 결과를 사용
        * 값을 기록해놓는다는 점에서 caching(캐싱)이라고도 함
    * 재귀함수 사용
    ```python
    # 피보나치 수열
    def fibonacci_dp(num):
        f = [0, 1]
        for i in range(2, num+1):
            f.append(f[i-1] + f[i-2])
        return f
    ```
2. Buttom-up 방식
    * 작은 문제 + 작은 문제 => 큰 문제가 되는 방식
    * 반복문 사용
    ```python
    # 피보나치 수열
    def fibonacci_memoi(num):
        global memo
        if num >= 2 and len(memo) <= num:
            memo.append(fibonacci_memoi(num-1) + fibonacci_memoi(num-2))
        return memo[num]
    memo = [0, 1]
    ```