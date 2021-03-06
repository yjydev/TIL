## 트리

- 비선형, 1 : n 관계(계층 관계)를 가지는 계층형 자료 구조 

  (상위 -> 하위로 내려가며 확장되는 나무모양 구조)     

- 1개 이상의 노드로 이루어진 유한집합

- 최상위 노드를 루트라 하며, 나머지 노드들은 N개의 부분 집합으로 분리될 수 있는데, 이들은 각각 하나의 트리가 되며 루트의 부트리라 한다. (재귀적 정의)

- 용어

  - 노드 - 트리의 원소
    - 단말노드 or 잎(leap) 노드 - 각 부트리의 가장 끝 노드, 차수가 0인 노드, 자식 노드가 없음             
    - 형제 노드 - 같은 부모 노드의 자식 노드들
    - 조상 노드 - 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들    
    - 서브트리 - 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리 (루트를 제외한 나머지 노드들로 이루어진 부분집합)     
    - 자손 노드 - 서브 트리에 있는 하위 레벨의 노드들         
  - 차수   
    - 노드의 차수 - 노드에 연결된 자식 노드의  수    
    - 트리의 차수 - 트리에 있는 노드의 차수 중 가장 큰 값    
  - 높이    
    - 노드의 높이 - 루트에서 노드에 이르는 간선의 수, 노드의 레벨       
    - 트리의 높이 - 트리에 있는 노드의 높이 중 가장 큰 값, 최대 레벨     

  ### 이진 트리     

  - 모든 노드들이 2개의 서브트리를 갖는 특별한 형태의 트리    

  - 각 노드가 자식 노드를 최대 2개 까지만 가질 수 있는 트리     

  - 레벨 i 에서의 노드의 최대 개수는 2^i 개이며, 높이가 h인 트리는 노드를 최소 (h+1)개, 최대 (2^(h+1) -1)개 가질 수 있다         

  - 종류   

    - 포화 이진 트리      
      - 모든 레벨에 노드가 포화상태(2개)로 차있는 이진 트리    
      - 높이가 h일 때, 노드 최대 개수인 (2^(h+1) -1)개의 노드를 가진다.     
      - 일반 이진 트리와 달리, 루트 번호가 항상 1번이다. 
        - 일반 트리는 편의상 1번으로 쓰기도 하지만. 1일 수도 아닐 수도 있다.        
      - 왼쪽부터 오른쪽으로 순차적으로 번호를 붙인다.     
    - 완전 이진 트리     
      - 높이가 h, 노드 수 n개 일 때, 포화 이진 트리처럼 왼쪽부터 번호를 붙이는데 노드 번호 1번부터 n번까지 빈 자리가 없는 이진 트리     
        - 만약, 오른쪽이 아닌 왼쪽이 빈다면, 완전 이진트리가 아니다      
    - 편향 이진 트리     
      - 높이 h에 대한 최소 개수의 노드를 가지며, 한쪽 방향의 자식 노드만을 가진 이진 트리  = 선형(순차) 자료구조와 다를 것이 없다.    

  - 순회    

    - 트리의 각 노드를 중복되지 않게 전부 방문하는 것     
    - 비 선형 구조이기 때문에 선후 관계를 알 수 없어, 목적에 맞는 순회 방법 선택 필요        
    - 순회 방법    
      - 전위 순회 (preorder / VLR) 
        - 부모 > 좌 서브트리(자식노드) > 우 서브트리(자식 노드)      
          1. 현재 노드 방문 처리 - V
          2. 현재 노드의 왼쪽 서브트리 이동 -  L   
          3. 현재 노드의 오른쪽 서브트리 이동 - R    
      - 중위순회 (inorder / LVR)
        - 좌 서브트리(자식 노드) > 부모 > 우 서브트리(자식 노드)      
      - 후위순회(postorder / LRV)
        - 좌 서브트리(자식 노드) > 우 서브트리(자식 노드) > 부모      
          - 가장 마지막에 루트노드가 처리된다.     

  - 배열을 이용한 이진 트리의 표현(저장)      

    - 포화/완전 이진 트리의 노드 번호 규칙만 따른다면 사용 가능    

    - 루트의 번호를 1번으로 하고, 왼쪽부터 오른쪽으로 순차적으로 번호를 붙인 트리     

    - 노드 번호의 성질

      - 노드 번호가 i 인 노드의 부모 노드 번호 - i//2
      - 노드 번호가 i 인 왼쪽 자식 노드 번호 - 2*i
      - 노드 번호가 i 인 오른쪽 자식 노드 번호 - 2*i + 1

      1)트리의 크기만큼의 인덱스를 가지고 정점번호를 인덱스로 사용하는 배열 생성    

      2)노드 번호의 성질 이용

    - 단점

      - 편향 이진 트리의 경우 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생      
      - 중간에 새로운 노드 삽입 or 삭제할 경우 배열의 크기 변경 어려워 비효율적    

    -> 연결 리스트를 이용하면 보완 가능     

    	- [왼쪽 자식노드 + 데이터 + 오른쪽 자식노드]구조의 단순 연결 리스트 노드 사용하여 구현    

  - 자식 번호를 인덱스로 저장한 배열 탐색    

    - 조상을 찾기 / root 찾기 에 사용 가능    

    - 자식 번호를 인덱스로 부모 번호를 값으로 저장    

      [0,2,0,1,2,3,3]  

      1번의 부모 2번, 3번의 부모 1번, 4번의 부모 2번, 5번의 부모 3번, 6번의 부모 3번 

- 수식 트리

  - 수식을 표현하는 이진트리로, 수식 이진트리라고 부르기도 한다.

  - 연산자는 루트노드이거나 가지노드이고, 피연산자가 모두 잎 노드     

  - `중위 순회` -> 식의 중위 표기법(일반식)  A / B * C * D + E 

    `후위 순회` -> 식의 후위 표기법 (연산자가 뒤로)  A B / C * D * E +

    `전위 순회` -> 식의 전위 표기법 (연산자 모두 앞으로) + * * / A B C D E

- 이진 탐색 트리

  - 탐색작업을 효율적으로 하기 위한 자료 구조
  - 모든 원소는 서로 다른 유일한 키를 갖는다.      
  - `규칙` : 왼쪽 - 루트보다 작은 값 / 오른쪽 - 루트보다 큰 값     
  - 왼/오른쪽 서브트리들도 모두 해당 규칙을 갖는 이진 탐색 트리      
  - 중위 순회 -> 오름차순 정렬    
  - 연산    
    - 탐색연산  
      - 루트에서 시작 / 탐색할 키 값 x <-> 루트 노드의 키 값 비교     
      - 한쪽 방향을 선택해서 탐색하면 되므로 재귀가 아닌 반복 구조     
      - `x = 루트노드의 키 값` : 성공
      - `x < 루트노드의 키 값` : 왼쪽 서브트리에 대해 탐색연산 수행     
      - `x > 루트노드의 키 값` : 오른쪽 서브트리에 대해 탐색연산 수행    
    - 삽입연산
      - 탐색 연산 수행 -> 같은 원소가 트리에 있는지  탐색    
      - 탐색 실패한 자리가 삽입 위치가 된다       
    - 삭제연산
      - 탐색 연산 수행 -> 삭제    
      - 만약 자식(a) 1개인 부모(b)를 삭제한다면, 해당 부모의 자식(a)을 부모의 부모(c)에게 연결    `c - b - a`  > `c - a`
      - 만약 자식(a < b) 2개인 부모(c)를 삭제한다면,  왼쪽 서브트리(a)의 자식 중 가장 큰 값(d)를 삭제하고 부모자리(c)에 삽입   `d -> a -> c <- b`    >   `a -> d <- b`    
        - 왼쪽 서브트리는 루트보다 작고, 오른쪽 서브트리는 크다는 규칙 준수를 위해    
  - 성능  
    - 탐색, 삽입, 삭제 시간은 트리의 높이(h, 이진탐색트리의 깊이)만큼의 시간 소요     
      - O(h) 
    - 평균의 경우 -> 균형적으로 생성되어 있는 경우
      - O(log n)
    - 최악의 경우 -> 한쪽으로 치우친 경사 이진트리인 경우    
      - O(n)
      - 순차탐색과 시간복잡도 동일     
    - 검색 알고리즘 비교   
      - 배열에서의 순차 검색 `O(N)`
      - 정렬된 배열에서의 순차 검색 `O(N)`
      - 정렬된 배열에서의 이진 탐색 `O(log N)`
        - 고정 배열 크기, 삽입 및 삭제 시 추가 연산 필요     
      - 이진 탐색 트리에서의 평균 `O(log N)`
        - 최악의 경우 `O(N)`
        - 완전 이진 트리 or 균형트리로 바꿀 수 있다면 최악의 경우 X
          - 새로운 원소를 삽입할 때 삽입시간을 줄일 수 있고, 평균과 최악의 시간이 같게되므로    
      - 해쉬 검색 `O(1)`    
        - 추가 저장 공간 필요       

- 힙    

  - 완전 이진 트리에 있는 노드 중에서 키 값이 가장 큰 노드 or 가장 작은 노드를 찾기 위한 자료 구조 (= 우선순위가 높은 정점 찾기)    
  - 힙의 크기를 우선순위로 활용하여 우선순위 큐를 구현할 수 있는 자료 구조    
    - 최대 힙
      - 큰 값일수록 우선순위 ↑
      - 키값이 가장 큰 노드를 찾기 위한 완전 이진 트리     
      - 부모 > 자식
      - 루트 노드 : 키값이 가장 큰 노드 (즉, 우선순위가 가장 높은 정점)     
      - 최대 힙을 모두 꺼내면 내림차순 정렬    
    - 최소 힙
      - 작은 값일수록 우선순위 ↑
      - 키값이 가장 작은 노드를 찾기 위한 완전 이진 트리         
      - 부모 < 자식
      - 루트 노드 : 키값이 가장 작은 노드 (즉, 우선순위가 가장 높은 정점)     
      - 최소 힙을 모두 꺼내면 오름차순 정렬    
  - 힙연산 - 삽입

  ```python
  # 완전 이진 트리이므로 노드번호가 순차적으로 모두 매겨짐
  heap = [] * N
  last = 0 
  enQ(n):
      last += 1					  # 삽입할 자리 확장
      heap[last] = n
      if heap[last//2] > heap[last]: # 부모노드가 더 크다면
      	return					   # 정상작동이므로 종료    
  
  enQ(n):
      last += 1
      heap[last] = n
      c = last			# 자식 노드 번호
      p = c//2			# 부모 노드 번호
      while p > 0 and heap[p] < heap[c]: # 부모노드가 더 작다면, 커질 때까지 반복
      # p > 0 이라는 소리는 부모가 없어진다 = 루트가 된다 
      # = 루트의 부모를 구하려고 하면 1//2 = 0이 되므로 반복 종료
          heap[p], heap[c] = heap[c], heap[p]	# 값 교환
          c = p		# 노드 번호도 교환
          p = c//2	
  ```

  - 힙연산 - 삭제

    - 힙에서는 루트 노드의 원소만 삭제 가능    

    - 루트 노드의 원소를 삭제하여 반환     

    - 힙 종류에 따라 최대값 or 최소값 구할 수 있다     

    - 개요

      1. 루트 노드의 원소 삭제

      2. 마지막 노드 삭제하여 루트 노드에 삽입    
      3. 삽입한 루트 노드 < 자식 노드 : 자리 바꾸기 
      4. 삽입한 루트 노드 > 자식 노드 : 자리 확정, 연산 종료 
