---
  title : "[자료구조,Python] 파이썬으로 만들어보는 더블리 링크드 리스트 (Doubly Linked List)"
    
  categories : 
            자료구조
            
  description : "[자료구조,Python] 파이썬으로 구현하는 링크드 리스트(Linked List) 자료구조"
        
  toc : true
  toc_label: "목차"
        
  tags:
    python
    자료구조
    Linked_List
            
--- 

#  Doubly Linked List
링크드리스트의 한 종류 더블리 링크드 리스트(Doubly linked list)는 Sngly Linked List와는 다르게 노드의 값에 previous 와 next의 값을 취한다. 
<br/>
<br/>
즉 우리가 Singly_Linked_List에서 Node에 우리가 delete_at에서 활용한 홤용한 Prev 와 Next의 개념이 노드에 추가된 것 이다. 
<br/>
<br/>
아래의 그림처럼 header 는  data1의 prev 를 가르키고 next는 data1을 가르킨다. 

![]({{ site.url }}/assets/images/dataStructure/Doubly_linked_list/그림1.png    )
<br/>
<br/>
<br/>
**일상생활 속 doubly Linked List**<br/>
우리의 일상생활에는 항상 doubly linked list가 있다. 바로 뒤로가기, 앞으로가기 이다. 컴퓨터 , 노트북 , 핸드폰 등에서 우리는 항상 페이지 뒤로가기, 앞으로가기 혹은 되돌리기, 앞으로가기 를 사용한다. 위 기능은 Doubly Linked List를 기본으로 하고있다. 
<br/>
<br/>
더블리 링크드 리스트의 대다수 메소드들은 싱글리 링크드 리스트를 활용하여 쉽게 구현할 수 있다.
Append, get_at, search method 에 대해서는 [[자료구조,Python] 파이썬으로 만들어보는 링크드 리스트 (linked list)](https://yangdongjae.github.io/자료구조/Linked_list/)를 참고하면 된다.

## Get_Near_by Method

get_near_by 메소드는 데이터 값과 원하는 범위를 파라미터로 받아, 지정한 데이터 값의 전과 다음 값을 출력하는 메소드 이다.

```python
def get_near_by(self,data,scope):
    list = [] 
    header= self.header
    prev = None
    nextData = None
    while header.get_data() != data:
        header = header.get_next()
        if header.get_data() == data:
            prev = header.get_prev()
            nextData = header.get_next()
            for i in range (scope):
                if prev == None:
                    break
                list.append(prev.get_data())
                prev = prev.get_prev()
            for i in range(scope):
                if nextData == None:
                    break
                list.append(nextData.get_data())
                nextData = nextData.get_next()
    return list
```
**코드 설명**
<br/>
<br/>
method 의 시그니처는  아래와 같다.
1. 메소드 이름 - get_near_by
2. 리턴타입 - list
3. 파라미터 - data , scope 
<br/><br/>
get near by 메소드를 구현하기위해서 사용자로부터 데이터 (previous , next의 내용을 알고자하는 데이터)값과 그 범위를 받아야 하기때문에 파라미터로 data, scope를 설정하였다.
<br/>
<br/>
또한 여러가지 데이터값을 리턴해야하기때문에 list를 활용하여 리턴하기로했다.
<br/>
<br/>
우선 입력받은 데이터(중심값)으로 이동하기 위하여 while 문을 사용해 header 에 data를 저장했다.
그 후 if문을 활용하여 입력받은 data 값과 현재 header 가 갖고있는 값이 동일한 경우에 prev 와 nextData를 세팅하게 해주었다.
<br/>
<br/>
그 후 for 문을 활용해 scope 까지의 데이터를 list에 추가하고, 만약 데이터가 빈값이면 break을 활용해서 for문을 멈추게 설계하였다.

<br/>
<br/>

**문제점** : 이렇게 코딩을 했을 시 원하는 scope의 데이터 값을 출력할 수 있지만, index에 순차적으로 저장되지 않는다. 이는 소프트웨어 개발로 이루워졌을때 문제가 될 수 있다. 이를 보안하여 새로운 코드를 작성할 필요가 있어보인다.

## Doubly_Linked_list 전체 소스코드
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Tue Apr 14 20:06:58 2020

@author: yangdongjae
"""


class Node:
    def __init__(self,data):
        self.data = data
        self.prev = None
        self.next = None
    
    def set_prev(self,prev):
        self.prev = prev
        
    def set_next(self, nextData):
        self.next = nextData
        
    def get_data(self):
        return self.data
    
    def get_prev(self):
        return self.prev
    
    def get_next(self):
        return self.next
        
        
class Doubly_linked_list:
    def __init__(self):
        self.header = None
        self.tail = None
        self.size = 0
        
    def print_list(self):
        header = self.header
        print(">>>Current List")
        while header != None:
            print(header.get_data())
            header = header.get_next()
        print(">>>>>>>>>>>>>>>>")
        
    def append(self,data):
        new_node = Node(data)
        header = self.header
        self.size += 1
        if self.header == None:
            self.header = new_node
        else:
            self.tail.set_next(new_node)
            new_node.set_prev(self.tail)
        self.tail = new_node
         
    def get_at(self,index):
        header = self.header
        for i in range (index):
            header = header.get_next()
        return header.get_next()
    
    def search(self,data):
        node = self.header
        for i in range(self.size):
            if node.get_data() == data:
                return node
            node = self.header.get_next()
        return node
    
    def get_near_by(self,data,scope):
        list = [] 
        header= self.header
        prev = None
        nextData = None
        while header.get_data() != data:
            header = header.get_next()
            if header.get_data() == data:
                prev = header.get_prev()
                nextData = header.get_next()
                for i in range (scope):
                    if prev == None:
                        break
                    list.append(prev.get_data())
                    prev = prev.get_prev()
                for i in range(scope):
                    if nextData == None:
                        break
                    list.append(nextData.get_data())
                    nextData = nextData.get_next()
        return list

                
    

            
            
        

dll = Doubly_linked_list()
dll.append("Apple")
dll.append("Kiwi")
dll.append("Banana") 
dll.append("Melon")
dll.append("Oranged")
dll.append("Blackberry")   
list = dll.get_near_by("Banana" , 3)
print(list)
   
```
**출력값**
```python
['Kiwi', 'Apple', 'Melon', 'Oranged', 'Blackberry']
```




