## 자료구조   
###### C, C++, 자바, 파이썬 등에 여러 언어에 있는 프로그래밍 구조이며, 메모리에 정보를 서로 다른 방법으로 저장할수 있도록 한다.         
###### ※ 노드 : 직사각형으로 나타낼 수 있는 메모리 덩어리, 그래프에서의 노드와 비슷한 역할   
</br>   

## 1. 기본 원칙   

#### 1-1. 구조체(struct)   
###### C에서 자신만의 구조를 만들 수 있는 키워드로 여러 자료형을 담는 그릇       
``` 
typedef struct 
{ (자료형1) (이름1); (자료형2) (이름2); } 
(새로운 자료명);
```   
#### 1-2. 점 표기법   
###### 구조체 안에 포함된 속성값은 점 연산자를 사용하여 (새로운 자료명).(이름1)로 표현할 수 있다.     
ex) 
``` 
typedef struct   
{ string abc; string cde; }   
aph;   
```      
-> 속성값 표현 : aph.abc 또는 aph.cde 등등      

#### 1-3. 별표 연산자 (```*```)   
###### 메모리 덩어리로 접근할 수 있는 역참조 연산자     
&연산자가 변수의 주소를 나타낸다면, ```*``` 연산자는 해당 주소로 이동하라는 뜻을 나타낸다.     

</br>   

## 2. 배열과 연결리스트    
- 배열과 연결 리스트는 값들의 리스트를 저장하는 방법        
- **배열은 값들이 연속적으로 이어져있어야 하지만, 연결 리스트는 메모리 내에서 떨어져있어도 리스트 저장 가능**      
  　　     
- 배열의 장점 : 1. [ ]를 활용하여 문법적으로 쉽게 인덱싱할 수 있다.    
　　　　　　2. 대괄호 안에 인덱스를 넣음으로 바로 접근할 수 있어 매우 빠르므로 바이너리 검색 같은 곳에 적용 가능하다.       
- 배열의 단점 : 1. 고정된 메모리 덩어리이므로 값을 추가하고 싶을 땐 O(n)만큼의 동작 시간이 소요되어 느리다.       
　　　　　　2. 메모리 내에서 연속된 공간으로 이루어져야 해서 값을 추가하는 등의 크기 조정 과정이 복잡하다.    
  　　   
- 연결 리스트의 장점 : 1. 값이 저장된 공간이 연속적일 필요가 없으므로 배열보다 좀 더 효율적인 메모리 사용이 가능하다.      
 　　　　　　2. 포인터로 연결되어있으므로 배열보다 값을 추가하는 등의 크기 조정이 자유롭다(=역동성)
- 연결 리스트의 단점 : 1. 포인터를 저장할 공간이 필요하므로 배열보다 메모리가 2배 더 소모된다.  
    　　　　　　2. 임의 접근이 불가능하다. 리스트의 끝이나 중간 값을 찾으려면 모든 포인터를 따라가봐야 알 수 있으므로 
    　　　　　　배열처럼 중간 값으로 바로 접근할 수 없다 = 이진 탐색의 효율성 감소     
</br>   

## - 연결 리스트   
#### 메모리 덩어리 여러 개를 포함한 데이터 구조이며 포인터로 연결되어 있다.           
- 마지막엔 다음 메모리 주소 대신 포인터인 널(NULL)을 사용함으로 종료 선언 - 널(NUL) 종단 문자(\0)와는 다른 것으로 16진법 0(0x0)    
- 하나를 저장할 때 __*값을 저장할 공간*__ 과 __*다음 메모리 덩어리의 주소(포인터)를 저장할 공간*__ 을 같이 저장하여 리스트 연결   
 즉, 2개의 필드로 이루어져 있다.       
1. number - 정수, 값      
2. next - 관례적인 이름이며 다른 이름으로 불러도 상관 X, 리스트의 다음 요소를 가리키는 메모리 덩어리      


#### - 기본 단위 node 구조체 정의        
``` 
typedef struct node    // 마지막 줄에 node가 나오기 전엔 node라는 단어를 못 쓰므로 앞에서 선언하는 것   
{ int number;
  struct node *next; }    // 연결 리스트는 그 다음 메모리 덩어리의 주소를 같이 저장하므로   
  node;    // 이 node 구조체의 별칭   
  ```   
  
#### - 구현   
```
int main(void)  
{
//리스트 첫 시작
node *list = NULL;      // 처음에는 비어있으므로 첫 번째 리스트에는 아무것도 없어서 NULL로 초기화     

node *n = malloc(sizeof(node));    // 메모리 덩어리 node를 저장할 공간을 malloc로 할당하고 그 반환값을 node의 주소 n에 저장
if (n == NULL)          // n이 널이라면 메모리 부족으로 할당안된거니 1을 반환하여 종료        
{ return 1; }   
 n->number = 2;        // n의 number값에 2 추가 = node n은 2를 기록함,  (*n).number = 2;와 같은 의미를 C 문법으로 작성   
  n->next = NULL;      // 아직 다음 리스트가 없어 비어있기 때문  
  
list = n;     // 새로운 node(값 2)를 가리키는 n을 list에 저장, 즉 list가 값 2의 node를 가리키게 됨.        

n = malloc(sizeof(node));     // 다른 node를 연결하기 위해 새로운 메모리 할당    
if (n == NULL)          // n이 널이라면 메모리 부족으로 할당안된거니 1을 반환하여 종료        
{ return 1; }
 n ->number = 4;
  n->next = NULL;        // 4를 기록하는 새로운 node 추가  
※ list->next = n;       // list의 next 값을 n으로 설정 = list가 현재 가리키는 값 2의 노드 next가 값 4의 노드를 가리키게 함.

// 리스트 맨뒤에 값 추가 
node *tmp = list;          // 임시 포인터 tmp가 list와 같은 곳을 가리키도록 함
while (tmp->next != NULL)   // tmp가 가리키는 곳의 next값이 널이라면 그게 현재 리스트의 끝을 의미하므로   
{ tmp = tmp->next; }        // 널이 아니라면 다음을 계속 찾아가며 스스로 업데이트   
tmp->next = n;

// list와 2 사이에 값을 끼워넣을 때 = 첫 부분에 값 추가
node *n = malloc(sizeof(node));    // 끼워넣을 값을 가지는 새로운 노드의 메모리 할당  
if (n == NULL)          // n이 널이라면 메모리 부족으로 할당안된거니 1을 반환하여 종료        
{ return 1; }
 n->number = 1;
  n->next = NULL; 
n->next = list;           // 메모리 누수를 막기 위해 n 포인터가 먼저 list가 가리키고 있는 것을 중복으로 가리키게 만듬
list = n;                 // 그 후 list가 n 포인터를 가리키게 하여서 시작이 list임을 알림   

// 위처럼 처음이 아니라 중간에 끼워넣는다면 루프로 탐색하고 부등호를 사용하여 적절한 위치 찾아내야 함  
// 즉, 반복문과 대소비교, 포인터 업데이터 과정 필요   

// list에 연결된 노드의 number 값 출력
for(node *tmp = list; tmp != NULL; tmp = tmp-> next)    // next값이 널이라면 리스트의 끝이므로 종료 조건   
{ printf("%i\n", tmp->number); }   

// 메모리 해제 
while (list != NULL)
{ node *tmp = list->next;
  free(list);
  list = tmp; }

}
```    


</br>    

## - 배열   
#### 값들의 리스트, 여러 개의 같은 자료형 값을 지닌 하나의 변수 설정할 때 사용     
###### 배열의 크기(갯수)는 처음 정의할때 부터 설정해야 한다.   
1. (자료형) (배열명)[갯수];   
2. (배열명)[0];    
3. (배열명)[1];   
 ...          
``` 
int (배열명)[갯수];   // 배열 선언   
for (int i = 0; i < n; i++)   // for 루프   
{ (배열명)[i]=get_int("~~~ %i: ",i); }   // 사용자로부터 배열값 받기   
```        
-> 배열값 정적 초기화      
(자료형) (배열명)[갯수] = { 배열 값 나열 };   

### (1) 2차원 배열　(배열명)[j][k]    
1. [j] : 배열의 인덱스-j번째 값    
2. [k] : j번째 값을 하나의 배열로 보고 그 중 k번째 문자      

### (2) 배열의 크기 조정 (i 크기 -> j 크기)  
###### 배열의 값은 처음부터 정해져있으므로 j 크기만큼 메모리를 재할당한 후 기존의 값들을 복사하고 i 크기의 메모리는 할당 해제     
1. ``` int *list = malloc(i * sizeof(int)); ``` 정수 자료형 i개로 이루어진 메모리를 malloc 함수로 할당하여 배열 list 정의      
2. 크기 조정하고 싶다면, realloc 함수를 사용하여 메모리 재할당 및 기존 값 복사     
3. list와 재할당한 배열이 같은 곳을 가리키도록 저장한 후 새로운 값 저장   
```
int *tmp = realloc(list, j * sizeof(int));    // tmp에 j 크기만큼 메모리 재할당 및 기존 값 복사     
if (tmp == NULL)    // 혹시 메모리 부족하면 표시하도록 명령   
{ return 1; } 
list = tmp;     // list가 tmp와 같은 곳 가리키도록 저장   
list[3] = 2;    // 새로운 값 있으면 이렇게 저장   
~ 작업 ~   
free(list);    // 마지막엔 메모리 초기화   

``` 
</br>   

## 3. 트리   
###### 연결 리스트 기반의 자료 구조, 2차원 연결 리스트    
###### 이진 탐색의 실행 시간은 O(n)인 연결리스트에서 발전하여 다시 배열처럼 O(log n)로 단축.    
   
#### - 이진 탐색 트리 구조체 정의   

``` 
typedef struct node
{ int number;
  struct node *left;     // 연결 리스트는 next 포인터 1개 존재, 트리는 left, right 포인터 2개 존재    
  struct node *right; }   // 이진 탐색 트리여서 노드들은 최대 2개의 자식 노드를 가질 수 있으므로 포인터 2개 존재
node;   
```   
   
- 트리의 제일 처음, 맨 위 노드를 **루트** 라고 한다.   
</br>      

## 4. 트라이   
###### 검색(retrieval)의 줄임말, 각 노드가 배열로 이루어진 트리     
###### 알파벳으로 이루어진 문자열을 저장한다면, a-z까지의 값을 가지는 배열이 각 노드가 된다.   
- 어떤 자원을 절약하기 위해 다른 자원을 소비하는 패턴 지님   
 -> 이론적으로 상수 시간의 실행 시간을 제공하기 위해 아주 많은 메모리를 소비한다 (공간을 포기하고 시간을 절약)        
    
- 많은 메모리를 소요하지만, 자료 구조 안의 문자열(이름 혹은 단어)을 찾는 데 일정한 실행 시간 지님       
 -> 다른 알고리즘은 자료구조에 있는 값들의 개수에 따라 실행시간이 길어지는 데 반해,   
 트라이는 해당 문자열 길이만큼의 시간만 걸려서 O(n)이어도 n이 크지 않은 상수값이므로 O(k) = O(1)의 실행시간을 가진다.   
 -> 이름 혹은 단어는 시간이 지날수록 길어지는 것이 아니라, 최대 상한이 정해져있기 때문에 점근적으로 상수로 취급한다.   
   
   
실행 순서   
1. 입력값의 모든 글자를 살펴본다.   
2. 입력값에 해당하는 인덱스로 이동한다. (ex> 분류 기준이 첫 글자이고 입력값이 ABC라면, A 인덱스로 이동한다.)   
3. 해당 인덱스에 자식 노드(다른 트리, 가지)가 없다면 새로운 노드를 할당한다.   
4. 3번을 반복한다. 즉, 각 글자에 대해 하나의 노드 혹은 배열을 저장한다.   
-> young 을 저장한다면, y로 이동해서 새로운 노드 할당하고 할당한 새로운 노드에서 o로 이동하여 다시 노드 할당, 할당한 노드에서 u로 이동하여 다시 할당...반복하여 g까지 이동한 후 불리안 연산식으로 이름 하나가 끝난다는 것을 표기한다.   

</br>     

## 5. 해시 테이블   
###### 자료구조에 값을 삽입하거나 탐색할 때 이론적으로 1단계만에 가능하게 하는 것 = O(1)            
###### 구현 방법이 명확하진 않으나 배열과 연결리스트를 조합한 것, 연결 리스트의 배열          
- 한 문자를 검사할때마다 배열이나 연결리스트를 사용하여 O(n)이나 O(log n)만큼의 시간이 걸린다면 문서를 모두 검사하는 데 너무 오랜 시간이 걸릴 것이다. 하지만 해시테이블을 이용한다면 훨씬 빠르게 실행 가능하다.   
- 입력값에 포함된 문자를 보고 어디에 해당 입력값을 넣을지 결정하는 방식을 흔하게 사용     
- 세로로 배열을 사용하고, 가로로 연결리스트를 사용    
-> 1~10번으로 분류된 배열에 값을 하나씩 넣고, 해당 배열(분류)에 값을 추가하고 싶다면 연결 리스트로 추가   
-> 연결 리스트로 추가하지 않는다면 이미 값이 들어있는 공간에 또 값을 넣으려고 하는 것이므로 충돌 발생   
   
### - 해시 함수      
###### 해시 테이블을 인덱싱 하는데 사용하는 배열+연결 리스트       
###### 입력값이 어느 배열(분류)로 가야하는지 알려주는 함수, 가야하는 배열의 인덱스가 출력값         
    
※ 하지만, 해시 테이블이 얼마나 효율적이든 입력값이 하나의 분류에 몰리는 문제 발생 가능 -> 실행 시간이 O(n)까지 느려질 수 있다.          
-> 분류 기준을 추가하는 등으로 쏠림 현상 방지   
-> 배열(분류)가 늘어나므로 공간이 더 많이 필요하지만, 충돌 확률은 낮아짐   
-> 실행 시간 빠르게 하겠다고 배열(분류)를 계속 늘린다면 필요한 공간이 기하급수적으로 늘어나기 때문에 오히려 느려질 수 있다.        
-> 시간과 공간의 균형을 맞추는 것이 중요!      

</br>    

## 6. 딕셔너리   
###### 키<->값, 단어<->값, 단어<->페이지 번호, 그 외의 다양한 쌍으로 이루어진 자료구조       
- 일반적인 의미에선 해시 테이블이라고도 할 수 있다.     
- 아주 많은 단어를 갖고 있는 영어 사전과 같아서 해당 단어가 올바르다면 사전에 존재할 것이라 탐색 가능      

</br>   

## 7. 스택과 큐       
###### FIFO 선입선출(입력된 순서대로 출력되는 것) <-> LIFO 후입선출(늦게 입력된 값이 먼저 출력되는 것)      
### - 큐     
###### 선입 선출의 특징을 가진 자료구조 (ex> 식당 주문, 프린트 ...)       
- 2가지 연산   
(1) enqueue : 줄에 들어가는 것     
(2) dequeue : 줄을 빠져나오는 것   

### - 스택   
###### 후입 선출의 특징을 가진 자료구조 (ex> 식당 쟁반, 메일함 ...)        
- 2가지 연산   
(1) push : 요소를 추가하는 것           
(2) pop : 가장 위의 요소를 제거하는 것            


