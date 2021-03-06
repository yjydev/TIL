## 완전 검색  

### 반복과 재귀

- 해결할 문제를 고려해서 반복이나 재귀 선택
- 재귀는 문제 해결을 위한 알고리즘 설계가 간단하고 자연스럽다 
  - 추상 자료형(List, Tree)의 알고리즘 등   
- 하지만, 재귀는 반복보다 더 많은 메모리와 연산이 필요 
  - n이 커질수록 재귀는 반복에 비해 비효율적일 수 있음   

- 반복구조  

  1. 초기화  
     - 조건 검사에 사용할 변수의 초기값 설정 (`ex> i = 0`)  

  2. 조건검사  

  3. 반복할 명령문 실행  

  4. 업데이트  
     - 무한 루프가 되지 않게 조건이 거짓이 되게끔 설정  

  - 반복을 사용한 선택정렬
    - 주어진 구간에서 최소값을 구해 구간의 맨 앞으로 보내기

  ```python
  def SelectionSort(A):
      n = len(A)
      for i in range(0,n-1):
          minI = i
          for j in range(i+1,n):
              if A[j] < A[minI]:
                  minI = j
          A[minI], A[i] = A[i], A[minI]
  ```

  

- 재귀

  - 재귀적 정의는 `기본 경우(basis case)` 와 `유도된 경우(inductive case)` 로 나뉜다  

    - 기본 경우

      - 집합에 포함되어 있는 원소로 induction을 생성하기 위한 시드 역할

    - 유도된 경우

      - 새로운 집합의 원소를 생성하기 위해 결합되어지는 방법   

    - EX>

      ```python
      # 팩토리얼을 구현하는 경우
      
      기본 경우 :
          if n <=1 :
              return 1
      유도된 경우 :
          if n > 1:
              return n * fact(n-1)
      ```

      

  - 일반적으로 재귀적 정의를 이용하여 재귀 함수 구현

    - 재귀 함수는 함수 내부에서 직접 혹은 간접적으로 자기 자신을 호출하는 함수

  - 재귀적 프로그램을 작성하는 것은 바복 구조에 비해 간결하고 이해가 쉽다   

  - 함수 호출은 메모리 구조에서 스택을 사용하므로 재귀 호출은 반복적인 스택의 사용을 의미하며, 메모리 및 속도에서 성능 저하 발생   

|               | 재귀                                   | 반복                  |
| ------------- | -------------------------------------- | --------------------- |
| 종료          | 재귀함수 호출이 종료되는 베이스 케이스 | 반복문의 종료 조건    |
| 수행 시간     | 느림                                   | 빠름                  |
| 메모리 공간   | 상재적 많이 사용                       | 적게 사용             |
| 소스코드 길이 | 짧고 간결                              | 길다                  |
| 소스코드 형태 | 선택 구조(if .. else)                  | 반복 구조(for, while) |
| 무한 반복시   | 스택 오버플로우                        | CPU를 반복해서 점유   |



### 고지식한 방법(brute-force)  

- 대부분의 문제에 적용 가능하며, 상대적으로 빠른 시간에 문제 해결 가능 

- 문제에 포함된 자료(요소,인스턴스)의 크기가 작다면 유용   

- 학술적 또는 교육적 목적을 위해 알고리즘의 효율성을 판단하기 위한 척도로 사용   

  - '이 최적화된 알고리즘은 완전검색보다 이만큼 유용하다' 처럼 비교하기 위한 용도    

- Brute-force 탐색

  - 자료들의 리스트에서 키 값을 찾기 위해 첫번째 자료부터 비교하며 진행   

  ```python
  def SequentialSearch(A[0..n], k):
      # 탐색 성공/실패를 판단하기 위해 마지막에 k 할당
      A[n] = k
      i = 0
      while A[i] != k:
          i += 1
      if i < n:
          # 탐색 성공
          return i
      else:
          # 탐색 실패
          return -1
  ```

  

- 모든 경우의 수를 생성하고 테스트하기 때문에 수행 속도는 느리지만, 대부분의 경우 해답을 찾아낸다.    
  - 입력의 크기를 작게 해서 간편하고 빠르게 답을 구하는 프로그램 작성   
  - 다만, 불필요한 중복이 있으면 시간초과 날 가능성 多
- 이를 기반으로 그리디 기법이나 동적 계획법을 이용해 효율적인 알고리즘을 찾을 수 있다.
- 우선 완전 검색으로 접근하여 해답을 도출 -> 성능 개선을 위해 다른 알고리즘을 사용하고 해답을 확인하는 것이 바람직

#### 완전검색

- 많은 종류의 문제들이 특정조건을 만족하는 경우 or 요소 찾는 것   

- 전형적으로 순열, 조합, 부분집합 같은 조합적 문제들과 연관
- 완전 검색은 조합적 문제에 대한 brute-force 방법  



#### 조합적 문제

- 순열

  - 서로 다른 n 개 중 r개를 선택해서 한줄로 나열하는 것    

  - 다수의 알고리즘 문제들은 순서화된 요소들의 집합에서 최선의 방법을 찾는 것과 관련    

  - 다만, N개의 요소에 대해 n! 개의 순열이 존재하므로 

    n이 커지면 시간 복잡도가 폭발적으로 상승하여 주의 필요!

  ```python
  # {1,2,3} 을 포함하는 모든 순열 생성하는 함수 
  # 동일한 숫자가 포함되지 않을때, 각 자리수별로 루프를 이용해 구현
  
  for i1 in 1->3:
      for i2 in 1->3:
          if i2 != i1:
              for i3 in 1->3:
                  if i3 !=i1 and i3 != i2:
                      print(i1, i2, i3)  
  ```

  - 생성 방법

    - 사전적 순서

      1. 사용할 숫자를 배열 a에 저장

      2. 사용된 숫자의 위치를 표시할 배열 used 생성

      3. 왼쪽부터 사용하지 않은 숫자를 찾으면 표시하고, 숫자 복사

      4. 다음 자리를 정하기 위해 재귀호출  
      5. 선택할 숫자를 모두 선택했으면 출력/리턴한다.    

    - 최소 변경을 통한 방법

      - 이전의 상태에서 2개의 요소의 교환을 통해 생성   
      - 1950년대의 교회의 종소리 패턴과 유사
      - Johnson-Trotter 알고리즘  

    ```python
    # 재귀를 통한 순열 생성
    # p : 배열, n : 원소의 개수, i : 선택된 원소의 수
    # = n 개중 i 개 선택
    
    # 이 방법은 사전순은 아님 
    def perm(n,k):
        if k == n:
            # 원하는 작업 수행
            print (p) 
            return
        else:
            for i in range(k, n):
                p[k], p[i] = p[i], p[k]
                perm(n,k+1)
                p[k], p[i] = p[i], p[k]
                
    # 방법2 - 사전순 생성
    # p : 순열을 저장할 빈 배열, arr : 주어진 배열, used : 사용 체크배열 
    
    def perm(n,k):
        if (k==n):
            print(p)
        else:
            for i in range(0,n):
                if not used[i]:
                    p[k] = arr[i]
                    used[i] = True
                    perm(n,k+1)
                    used[i] = False
                    
    # m개 중 n개 선택 
    
    def perm(n,m,k):
        if (k==n):
            print(p)
        else:
            for i in range(m):
                if not used[i]:
                    p[k] = arr[i]
                    used[i] = 1
                    perm(n,m,k+1)
                    used[i] = 0
    ```



- 부분 집합

  - 다수의 중요 알고리즘들이 원소들의 그룹에서 최적의 부분집합 찾는 문제    

    - ex> 배낭 짐싸기 등

  - N개의 원소를 포함한 집합

    - 본인과 공집합 포함하여 모든 부분집합의 개수는 2^n 개

  - 생성 방법

    - 단순하게 생성

      ```python
      # 4개 원소를 포함한 집합에 대한 부분집합 생성
      # 단순 생성
      for i1 in range(0,2):
          bit[0] = i1
          for i2 in range(0,2):
              bit[1] = i2
              for i3 in range(0,2):
                  bit[2] = i3
                  for i4 in range(0,2):
                      bit[3] = i4
                      print(bit)
      ```

      

    - 바이너리 카운팅

      - 부분집합을 사전순으로 생성하기에 가장 자연스러운 방법   
      - 원소수에 해당하는 N개의 비트열 이용   
      - n번째 비트값이 1이면 n번째 원소가 포함되었음을 의미   

      ```python
      arr 배열
      n = len(arr)
      
      for i in range(0, (1<<n)):
          # 원소의 수만큼 비트 비교
          for j in range(0,n):
              # i의 j번째 비트가 1이면 j번째 원소 출력
              if i & (1 <<j):
                  print('{}'.format(arr[j]), end='')
          print()
      ```

- 조합

  - 서로 다른 n개의 원소 중 r개를 순서없이 골라낸 것    

  - nCr = n-1 C r-1 + n-1 C r 

    - n개중 r개를 선택하는 경우 = n이 선택된 경우(n-1 C r-1) + n 선택 X 경우(n-1 C r)

  - 조합 생성 알고리즘

    - 고를 수 있는 r 이 가변적인 경우 : 재귀
      - 그 외 : 반복문

    ```python
    # 재귀호출 사용
    an : n개의 원소를 갖고 있는 배열
    tr : r개의 배열, 조합이 임시저장될 배열
    
    def comb(n,r):
        if (r ==0 ):
            print tr
        elif n < r:
            return
        else:
            # 덮어쓸수 있으므로 리턴되서 돌아왔을 때 지울 필요는 X
            tr[r-1] = an[n-1]
            # 선택해야하는 r개를 조합을 저장할 배열의 인덱스로 활용
            comb(n-1, r-1)
            comb(n-1,r)
            
    # 재귀호출 사용2
    # n개중 r 개 고르는 조합, s: 선택가능한 구간의 시작, k:고른 갯수=comb의 인덱스
    def nCr(n,r,s,k) :
        if k == r:
            print(*comb)
        else:
            # n-r +k 까지의 범위 -> 아래의 10개중 3개 고르는조합 방식과 비슷
            for i in range(s,n-r+k+1):
                comb[k] = i
                nCr(n,r,i+1,k+1)
    
    N, R = 10,3
    comb = [0] * R
    nCr(N,R,0,0)
    ```

    ```python
    # 10개 중 3개 고르는 조합
    
    c = 0 # 조합 갯수
    for i in range(8):	# j,k 고를 범위 남기기, 8=n(10)-r(3)+k(0) +1
        for j in range(i+1,9): 	# k 고를 범위 남기기, 9 =n(10)-r(3)+k(1) +1
            for k in range(j+1,10):		# 10 = n(10)-r(3)+k(2) + 1
                c += 1
                print(c, i,j,k)
    ```

    
