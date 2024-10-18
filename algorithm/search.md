# search 검색
* 검색(Search)
    * 저장되어 있는 자료 중에서 원하는 항목을 찾는 작업
    * 목적하는 탐색 키를 가진 항목을 찾는것
        * 탐색 키(search key) : 자료를 구별하여 인식할 수 있는 키
* 검색의 종류
    * 순차 검색(sequential serach)
    * 이진 검색(binary search)
    * 해쉬(hash)


## sequential search 순차 검색
* 가장 간단하고 직관적인 검색 방법
* 배열이나 연결 리스트 등 순차구조로 구현된 자료구조에서 원하는 항목을 찾을 때 유용함
* 알고리즘이 단순하여 구현이 쉽지만 검색 대상의 수가 많은 경우에는 수행시간이 급격히 증가하여 비효율적임
* 검색 과정 - 정렬이 되어 있지 않은 경우
    1. 첫 번째 원소부터 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교하며 찾는다.
    2. 키 값이 동일한 원소를 찾으면 그 원소의 인덱스를 반환한다.
    3. 자료구조의 마지막에 이를 때까지 검색 대상을 찾지 못하면 검색 실패
        ```python
        def sequential_search(a, n, key) :
            i = 0
            while i < n and a[i] != key :
                i += 1
            if i < n :
                return i
            else :
                return -1
        ```

        ![success sequential search (sort X)](../images/algorithm/search/sequential_search_success.png)

        ![fail sequential search (sort X)](../images/algorithm/search/sequential_search_fail.png)

    * 시간 복잡도 : O(n)
* 검색 과정 - 정렬이 되어 있는 경우
    1. 자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정하면
    2. 자료를 순차적으로 검색하면서 key값을 비교하며 원소의 key값이 검색 대상의 key값보다 크면 찾는 원소가 없는 것으로 검색 종료
        ```python
        def sequential_search(a, n, key) :
            i = 0
            while i < n and a[i] < key :
                i += 1
            if i < n and a[i] == key :
                return i
            else :
                return -1
        ```

        ![success sequential search (sort O)](../images/algorithm/search/sequential_search_success_sort.png)

        ![fail sequential search (sort O)](../images/algorithm/search/sequential_search_fail_sort.png)


## Binary Search 이진 검색
* 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법
    * 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여가면서 보다 빠르게 검색을 수행함
* 이진 검색을 위해서는 **정렬된** 상태의 자료여야 한다.
* 검색 과정
    1. 자료의 중앙에 있는 원소를 찾는다.
    2. 중앙 원소의 값과 찾고자 하는 목표 값을 비교한다.
    3. 목표 값이 중앙 원소의 값보다 작으면 자료의 왼쪽 반에 대해서 새로 수행하고, 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행한다.
    * 찾고자 하는 값을 찾을 때까지 반복한다.
        ```python
        def binary_search(a, n, key) :
            start = 0
            end = n-1
            while start <= end :
                middle = (start + end) // 2
                if a[middle] == key : # 검색 성공
                    return True
                elif a[middle] > key :
                    end = middle -1
                else :
                    start = middle + 1
            return False # 검색 실패
        ```
        ```python
        # 재귀함수 이용
        def binary_search(a, low, high, key) :
            if low > high : # 검색 실패
                return False
            else :
                middle = (low + high) // 2
                if key == a[middle] : # 검색 성공
                    return True
                elif key < a[middle] :
                    return binary_search(a, low, middle - 1, key)
                elif a[middle] < key :
                    return binary_search(a, middle + 1, high, key)
        ```

        ![success binary search](../images/algorithm/search/success_binary_search.png)

        ![fail binary search](../images/algorithm/search/fail_binary_search.png)


## Binary Search vs Sequential Search

![binary search vs sequential search](../images/algorithm/search/binary_vs_sequential.gif)