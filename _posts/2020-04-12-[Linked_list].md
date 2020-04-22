---
    title: "[자료구조,Python] 파이썬으로 만들어보는 링크드 리스트 (linked list)"

    categories : 
        자료구조
        
    description : "[자료구조,Python] 파이썬으로 구현하는 링크드 리스트(Linked List) 자료구조"
    
    toc : true
    toc_label: "목차"
    
    tags:
        python
        자료구조
        List
        
    last_modified_at: 2020-04-12
---
# Linked List

연결리스트 (Linked List)는 말 그대로 멀리 떨어져있는 리스트를 연결한다고 생각하면 이해하기 쉽다. 
<br/>
<br/>
지금부터 컴퓨터내부 데이터처리를 예로들어 내가 이해한 Linked List를 해볼것이다.
<br/>
<br/>
우리 컴퓨터는 모든 메모리를 딱딱 규격에 맞추어 저장하지 않는다. 그러다보니 아래의 그림처럼 데이터와 데이터 사이에 빈 공간이 생기기 마련이다.
![]({{ site.url }}/assets/images/dataStructure/Linked_List/LinkedList.png    )
<br/>
<br/>
우리가 저장하고 싶은 데이터가 빨간색 블록이라고 생각해보자. 우리가 이 블록을 메모리에 저장하기 위해서는 빨간색 블록을 실로 연결하여 어디에 저장되어있든 빨간색 블록의 위치로 가서 다음값을 찾아가는수밖에 없다.즉 빨간색 데이터 블록들을 꿰매는 것 이다. 만약 실로 연결하지 않으면 다음데이터가 어디에 있는지모르게되니 이는 곧 메모리에 쓰레기가 될 것이다.
![]({{ site.url }}/assets/images/dataStructure/Linked_List/LinkedList_2.png    )
<br/>
<br/>
빨간색 데이터 블록을 실로연결하는것. 우리는 그것을 **"링크드 리스트"** 라고 부른다.



## Singly Linked List
위에서 링크드리스트에 대한 개념에 대해서 내가 이해한대로 적어보았다. 자 이제 구현을 하귀해서 조금 더 깊게 살펴보자. 

위에서 링크드 리스트는 실로 각 데이터 블록을 꿰맨다고 이야기했다. 실로 데이터 블록을 다 꿰맸으면 그 순서가 있을것이다. 그리고 빨간색 데이터 블록의 '**첫번째 블록**'과 '**마즈막 블록**'그리고 **빨간색 데이터 블록의 수** 가 있을것이다. 

Singly Linked Listd에서는 **시작**을 **Header**라고 이야기하고 **끝**을 **tail** 이라고 이야기한다. 그리고 **빨간색 데이터 블록의 수**를 **size**라고 이야기한다.

아래의 그림을 보고 이해해보자

![]({{ site.url }}/assets/images/dataStructure/Linked_List/Linked_list_3.png   )

자 이제 다시 정리해보자. Singly Linked List 에는 특정 데이터 블록(Node)를 가르키는  **Header, Tail** 가 있고, 데이터 블록의 수(전체 Node의 수) 를 나타내는 **size**라는 요소가 있다. 자 이제 이것을 활용하여 데이터를 추가하는 메소드, 검색하는 메소드, 추출하는 메소드 , 삭제하는 메소드를 구현해 보자. 
### class Node
```python
class Node:
    def __init__(self,data):    
        self.data = data
        self.next = None
        #파이썬의 특징중 하나로, 클래스를 선언한 후 반드시 초기화를 해야한다. 
        #그래서 이 메소드를 initialize method라고 이야기한다. 
        #이 method 에서는 후에 클래스에서 객체가 만들어질 때 자동으로 호출되어 그 객체가 갖게될 
        #여러가지 성질들을 정해준다.
        
def get_data(self):
    return self.data
    # 현재 data를 return 하는 메소드

def get_next(self):
    return self.next
    # 다음 노드에 있는 data를 return 하는 메소드

def set_next(self,next):
    self.next = next
    # 다음 노드의 data를 정하는 메소드 self.next에 저장해야할 값이 필요하기 때문에 parameter next값을 갖는다.(파라미터의 이름은 편하신대로 정하셔도 되요!)

```
### class Singly_Linked_List 

우리는 앞으로 연결리스트 중 Singly linked list를 이해하며 총 4가지 메소드를 만들어 볼 것이다. 그 메소드의 이름은 각각 append , get_at , search , Delete_at 이며 각각의 메소드는 데이터 추가 , 검색 , 추출 , 삭제의 역할을 한다.

자 이제 위에서 설명한 요소들을 객체로 만들어주고 각각의 동작을 수행하는 메소드를 만들어보자.

```python 
class singly_linked_list:

    def __init__(self):
        self.header = None
        self.tail = None
        self.size = 0
        #현재 빨간색 데이터 블록이 아무것도없다 .
        #즉 링크드 리스트에는 어떤것도 추가되어있지않은 텅 빈 상태이다.
        #그래서 header도 tail도 None 값으로 지정하고 size도 0으로 지정한다.
```



# append Method

우리가 데이터를 받아서 링크드 리스트에 데이터를 추가하는 동작을 수행할 때 경우의 수는 총 2가지 이다.
아무것도 꽤매어져 있지 않은 상태 인가? or 이미 실에 빨간색 데이터 블록이 꿰매어져 있는가?  즉 **Header가 가르키는 값이 None인가? or Header가 가르키는 노드가 있는가?** 와 같은 말이다.

**Header 가 가르키는 노드가 None일때**
------------------------------------
Header가 가르키는 노드가 때None일때는 추가될 데이터를 Header와 tail이 가르키게 하면 된다. 실에 빨간색 데이터 블록을 꿰매는데 실에 데이터 블록이 하나밖에 없으니 실의 시작과 끝 둘다 방금 들어온 데이터 블록인것과 같은 맥락이다.

**Header 가 가르키는 노드가 None이 아닐때**
------------------------------------
Header가 가르키는 노드가 None이 아닐때는 끝 데이터를 가르키고 있는 tail 뒤에 새로운 노드를 추가하면 된다. 그리고 추가된 노드를 tail 로 지정해 주면 된다. 

**구현**
------------------------------------
```python
    def append(self,data):
    #추가할 데이터값을 받아야하기 때문에 parameter가 있어야한다. 
        self.size += 1
        new_node = Node(data)
        if self.header == None:
            self.header = new_node
            #현재 Header의 값이 None이면
            #추가한 데이터를 header 가 가르키게함.
        else:
            self.tail.set_next(new_node)
            #현재 Header의 값이 None이 아니면 tail의 뒤에 세팅함.
        self.tail = new_node
        #방금 추가된 데이터가 맨 마즈막이 됬으므로 tail이 가르키게함
```
# Get_at Method
get_at Method는 index번호를 받아서 그 번호에는 어떤 값이 있는지를 알아보기 위한 메소드 이다. 이 메소드의 경우에도 발생할 수 있는 경우가 2가지가 있다.
'알려고하는 n 번째 빨간색 블록의 가 현재 있는 블록의 수보다 클 때 ' or '알려고하는 n 번째 빨간색 블록의 수가 전체 블록의 수보다 작을 때' 즉 **입력받은 index의 값이 size의 값보다 크거나 같을 때(index는 0번부터 출발하지만 size는 1부터 출발함으로) or 입력받은 index의 값이 size의 값보다 작을때** 이다.

**size <= index**
------------------------------------
당연히 이와같은 상황은 오류다. 오류임을 알려주거나 아무 값도 return 하지 않으면 된다.

**size > index**
------------------------------------
빨간색 데이터 블록의 시작부터 찾고자 하는 빨간색 데이터 블록까지 실을 타고가서 만나면, 그 값을 확인하면 된다. 즉 입력받은 index까지 계속해서 데이터값을 받는다. 그러다가 입력받은 index에서 동작을 멈추고, 그 다음 값을 return 해주면된다.

**구현**
------------------------------------
```python

def get_at(self,index):
    #검색할 index번호를 받아야 하기 때문에 index를 parameter로 지정한다.
    if self.size <= index :
        return None
        #오류가 발생한 사항이기때문에 none값을 리턴한다
    else:
        header = self.header            
        for i in range(0,index):
            header = header.get_next()
        return header
        #실을 따라가면서 데이터 블록값을 확인하는 과정이다.
```
# Search Method
search 메소드는 링크드 리스트 안에 검색한 데이터가 있는지 확인할 때 사용하는 메소드이다. search 메소드는 get_at 메소드와 상당히 유사하다. 실을 따라가다 찾고자하는 데이터와 똑같은게 있으면 알려주면 끝나는 것 이다.

**구현**
------------------------------------
```python
    def search(self,data):
    #비교할 데이터 값이 필요하기 때문에 data parameter 가 있어야 한다.
        node = self.header
        for i in range(self.size):
        #데이터를 연결한 실을 잡고 시작부터 끝까지 이동하며 확인한다는 의미이다.
        #즉 링크드 리스트 전체를 확인한다는 의미이다.
            if node.get_data() == data:
                return node
                #확인하던 도중에 검색한 데이터와 동일한게 나오면 현제 값을 return 하게한것이다.
            node = self.header.get_next()
            #시작이 header였기때문에 (시작 값이 0 이였기때문에) 현재 가르키고 있는것은 
            #data와 동일한 곳에 있는게 아닌 그 전 노드에 있다.
            #그렇기 때문에 get_next() 로 노드값을 받아야 한다.
        return node    
```

# Delete_at Method
delete_at은 구현하기 버거웠다. 만약 이 글을 읽으신다면 본인스타일로 꼭 이 메소드를 구현해 보는걸 추천한다. 

우리가 특정 index의 노드값을 삭제할 경우에는 총 4가지 경우의 수가 발생한다. 

1. 존재하지 않는 빨간색 데이터 블럭을 삭제하라고 하는 경우
2. 제일 첫번째 즉 시작 부분의 빨간색 데이터 블럭을 삭제하라고 하는 경우
3. 중간 (시작과 끝 사이)에 있는 빨간색 데이터 블럭을 삭제하라고 하는 경우
4. 끝에있는 빨간색 데이터 블럭을 삭제하라고 하는 경우

위 4가지 경우를 링크드 리스트 용어들로 바꾸어 보겠다.

1. index + 1 > size
2. index == 0 
3. size >= 1 and indext +1 < size
4. index == size -1 

**index + 1 > size**
------------------------------------
오류다. 에러가 났음을 알려주거나, None값을 return 해주면 된다.
**index == 0**
------------------------------------
시작 지점에 있는 빨간색 데이터 블럭을 빼주기만 하면 된다. 그렇게 되면 원래 시작 지점에 있던 빨간색 블럭의 다음 블럭이 시작 지점이 된다. 즉 **header 의 값을 header 의 다음으로 지정한 후 size를 줄여주면 된다.**

**size >= 1 and indext +1 < size**
------------------------------------
singly linked list의 꽃이다. 
나는 이 문제를 해결하기 위해 '빨간색 데이터 블럭 뿌시기'라는 생각으로 문제에 접근했다. 실에 연결되어있는 빨간색 벽돌을 빼내려면 시작부분부터 전부다 빼거나 끝 부분부터 전부다 빼거나 둘중 한가지를 택해야 한다. 하지만 링크드리스트에서는 그럴 수 없다. 그렇기에 지정한 빨간색 데이터 블럭을 뿌시고, **지정한 빨간색 데이터 블럭의 양옆에 데이터를 이어 붙인다.** 라고 생각했다.

이해하기 쉽게 설명하자면 실에 1,2,3,4,5 번의 빨간색 데이터 블록이 있다. 그리고 우리는 3번 빨간색 데이터 블록을 다른 블록들에게 피해가 가지 않게 실에서 빼야한다. 이때 방법은 한가지이다 3번 빨간색 데이터 블록을 뿌시는것. 이렇게 3번 빨간색 데이터 블록을 뿌시면 더이상 2번 빨간색 데이터 블록의 다음은 3번 빨간색 데이터 블록이 아니다. **즉 빨간색 데이터 블록이1,2,3,4,5 번 이었다면 -> 1,2,4,5번 빨간색 데이터 블록으로 된것이다 -> 3번 데이터 블록의 전 블록인 2 번과 다음 블록인 4번 데이터 블록을 연결해 준것이다.**

header부터 지정되어있는 index전과 다음 의 값까지 이동하여, **전**에 저장되어있는 값, **다음**에 저장되어있는 값을 설정한다. 이 과정에서 이전 메소드 들에서는 사용하지 않은 **전** 과 **다음** 이라는 요소가 추가되어야 한다. 
그리고 그 두 값을 이어 붙이기만 하면 된다.

**index == size -1 **
------------------------------------
실의 끝에 있는 빨간색 데이터 블록을 빼는것 이다. 실의 끝에있는 빨간색 데이터 블록을 빼면 끝에서 2번째에 있던 빨간색 데이터 블록이 이제 실의 끝에있는 빨간색 데이터 블록이 된다.

즉 tail이 가르키는 값을 tail 전 값으로 지정해주면 된다.



**구현**
------------------------------------
```python

def delete_at(self,index):
#몇번 index의 노드를 삭제할지 입력받아야 하기때문에 index parameter 가 필요하다.
    prev = self.header
    next_data = None
    node = self.header
    if index + 1 > self.size:
        print("index error")
        #에러인 경우
    elif index == 0:
        self.header = node.get_next()
        self.size -= 1
        #첫번째 노드를 삭제하는 경우
    else:
        for i in range (index - 1):
            node = node.get_next()
            prev = node
             #for문을 통해서 index의 prev 값을 지정한다.
        node = self.header
        #next_data 값을 지정하기위해 node를 초기화 해준다.
       
        for i in range (index + 1):
            node = node.get_next()
            next_data = node
            #for문을 통햇서 index의 다음값을 지정한다.
        prev.set_next(next_data)
        #둘이 합체시킨다.
        #index == size - 1인 경우에는 next 가 none값이되어
        #prev 와 합체된다.
        node = self.header
        #합체 후 tail의 위치를 지정해준다.
        while node.get_next() != None:
            node = self.header.get_next()
        self.tail = node
```
# Singly_Linked_List 전체 소스코드
```python
'''
Created on 2020. 4. 4.

@author: yangdongjae
'''
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None
        
    def get_data(self):
        return self.data
    
    def get_next(self):
        return self.next
    
    def set_next(self,next):
        self.next = next
    


        
        
    
class singly_linked_list:
    
    def __init__(self):
        self.header = None
        self.tail = None
        self.size = 0


    def append(self,data):
        self.size += 1
        new_node = Node(data)
        if self.header == None:
            self.header = new_node
        else:
            self.tail.set_next(new_node)
        self.tail = new_node
    
    def print_list(self):
        node = self.header
        while node != None:
            print(node.get_data())
            node = node.get_next()
        
    def get_at(self,index):
        if self.size <= index :
            return None
        else:
            header = self.header            
            for i in range(0,index):
                header = header.get_next()
            return header
        
    def search(self,data):
        node = self.header
        for i in range(self.size):
            if node.get_data() == data:
                return node
            node = self.header.get_next()
        return node
    
    def delete_at(self,index):
        prev = self.header
        next_data = None
        node = self.header
        if index + 1 > self.size:
            print("index error")
        elif index == 0:
            self.header = node.get_next()
            self.size -= 1
        else:
            for i in range (index - 1):
                node = node.get_next()
                prev = node
            node = self.header
            for i in range (index + 1):
                node = node.get_next()
                next_data = node
            prev.set_next(next_data)
            
            node = self.header
            while node.get_next() != None:
                node = self.header.get_next()
            self.tail = node
                
            
#테스트 코드
sll = singly_linked_list()

sll.append("chicken")
sll.append("coffee")
sll.append("USA")
sll.print_list()

print("-----------")
sll.delete_at(2)
sll.print_list()
print("-----------")
sll.append("airpods")
sll.print_list()
print("-----------")

node = sll.get_at(0)
if node != None:
    print(node.get_data())
else:
    print("index error")
print("-----------")    
node = sll.get_at(2)
if node != None:
    print(node.get_data())
else:
    print("index error")
    
print("-----------")
    
node = sll.search("USA")
if node != None:
    print("we have it!")
else:
    print("We don't have it!")
    
```
