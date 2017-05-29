# Collection


## ArrayList
- java.util.ArrayList
- 생성자/메서드 :  
  - ArrayList<>()  
  : 초기 용량 10으로 빈 상태의 객체 생성
  - ArrayList<>(Collection c)  
  : 지정된 컬렉션의 요소가 포함되어 있는 리스트 생성
  - ArrayList<>(int capacity)
  : 지정된 초기 사이즈로 빈 상태의 객체 생성
  - boolean add(E e)  
  : element 추가
  - void add(int index, E element)  
  : 해당 인덱스에 지정된 element 추가
  - void clear()  
  : ArrayList를 비움
  - boolean contains(Object o)  
  : 해당 Object가 포함되어있는지 검사
  - void ensureCapacity(int minCapacity)  
  : ArrayList의 용량 증가
  - E get(int index)  
  : 지정된 위치한 원소 반환
  - int indexOf(Object o)  
  - boolean isEmpty()
  : 현재 ArrayList가 비어있는지 확인
  - int lastIndexOf(Object o)  
  : 지정된 Object를 검색하고, 마지막으로 검색된 항목의 0부터 시작하는 인덱스 반환
  - E remove(int index)  
  : 해당 인덱스의 원소 삭제후 삭제된 객체 반환
  - boolean remove(Object o)  
  : 지정된 object 삭제후 결과를 t/f로 반환
  - E set(int index, E element)  
  - int size()  
  : ArrayList의 원소 개수 반환
  - Object[] toArray()
  : ArrayList의 원소들을 Object 배열에 담음
  - void trimToSize()  
  : ArrayList의 앞 뒤 공백 삭제


특징 :
- 동기화 미제공

## Vector
- java.util.Vector
- 생성자/메서드 :
  - Vector()  
  : 10개의 데이터를 저장할 수 있는 객체 생성, 부족할 경우 10개씩 증가
  - Vector(int size)  
  : size개의 데이터를 저장할 수 있는 객체 생성, 부족할 경우 size개씩 증가
  - Vector(int size, int incr)   
  : size개의 데이터를 저장할 수 있는 객체 생성, 부족할 경우 incr개씩 증가
  - void add(int index, Object element)  
  : index 위치에 element 객체 저장
  - boolean add(Object o)  
  : 객체를 저장하고 그 결과 여부를 t/f로 반환
  - int capacity()
  : 용량 반환
  - boolean contains(Object o)  
  : 객체가 있는지 검사해 결과 여부를 t/f로 반환
  - void copyInto(Object[] anArray)  
  : Vector 내용을 Object 배열로 복사
  - Object elementAt(int index)  
  : index 위치의 객체 반환
  - boolean equals(Object o)  
  : Vector의 내용이 같은지 비교
  - Object firstElement()  
  : 첫 번째 요소를 Object 형태로 반환
  - Object get(int index)  
  : index 번째 요소를 Object 형태로 반환
  - boolean isEmpty()  
  : 비어있는지 검사해 결과 여부를 t/f로 반환
  - Object remove(int index)  
  : index 위치의 객체 제거
  - boolean remove(Object o)  
  : 지정된 객체를 찾아 제거
  - void removeAllElements()  
  : 모든 요소 제거
  - int size()  
  : 현재 size 반환
  - Object[] toArray()
  : Vector를 Object 배열로 생성해 반환


- 특징 :
  - 동기화 제공

## LinkedList
- java.util.LinkedList
- 생성자/메서드 :
  - LinkedList()  
  : 비어있는 객체 생성
  - LinkedList(Collection c)  
  : 해당 Collection을 포함한 객체 생성
  - boolean add(E e)  
  : 지정된 element를 추가하고, 결과를 t/f로 반환
  - void add(int index, E element)
  : 지정된 index에 element 추가  
  - void addFirst(E e)  
  : 맨 앞에 element 추가
  - void addLast(E e)
  : 맨 뒤에 element 추가  
  - void clear()  
  : 모든 element 지우기
  - boolean contains(Object o)
  : 지정된 Object가 있는지 검사 후 결과를 t/f로 반환
  - E get(int index)  
  : 지정된 index의 element 반환
  - E getFirst()  
  : 맨 앞의 element 반환
  - E getLast()  
  : 맨 뒤의 element 반환
  - E remove()  
  : 첫 번째 element 삭제
  - E remove(int index)  
  : 지정된 index의 element 삭제 후, 반환
  - E set(int index, E element)  
  - int size()  
  : LinkedList의 사이즈 반환
  - Object[] toArray()  
  : LinkedList를 Object 배열로 변환


- 특징 :
  - 자기 앞 뒤 객체에 대한 정보를 갖고 있음
  - 용량을 늘리고 줄이는 과정이 간단

## Stack
- java.util.Stack
- 생성자/메서드 :
  - Stack()  
  : 객체 생성
  - E pop()  
  : 맨 위의 객체를 제거하고 그 객체를 반환
  - E peek()  
  : 맨 위에 있는 객체를 반환, 객체를 제거하지는 않음
  - E push(E item)  
  : 맨 위에 객체를 추가
  - int serach(Object o)
  : 찾고자 하는 객체의 위치 반환
  - boolean empty()  
  : 현재 스택이 비어있는지를 확인

- 특징 :
  - LIFO(Last In First Out)
  - Vector를 상속받아 만든 클래스

## Queue
- import java.util.Queue

- 생성자/메서드 :
  - bollean offer(E o)  
  : 지정된 요소를 큐에 추가
  - E element()  
  : 큐의 맨 아래 있는 요소 반환, 큐가 비어있으면 예외 발생
  - E peek()  
  : 큐의 맨 아래 있는 요소 반환, 비어있으면 null 반환
  - E poll()  
  : 큐의 맨 아래 있는 요소 반환하며 삭제 , 비어있으면 null 반환

- 특징 :
  - FIFO(First In First Out)

## HashMap
- java.util.HashMap<K, V>

- 생성자/메서드 :
  - HashMap()  
  : 객체 생성
  - HashMap(int capacity)   
  : 주어진 값을 초기 용량으로 하는 객체 생성
  - HashMap(int capacity, float loadFactor)  
  : 주어진 값을 초기용량과 load factor의 객체 생성
  - Object put(Object key, Object value)  
  : key와 value를 저장
  - Object get(Object key)   
  : 주어진 key의 value를 반환
  - Object remove(Object key)   
  : 주어진 key로 저장된 value 제거
  - void clear()   
  : 저장된 모든 객체 제거
  - boolean containsKey(Object key)  
  : 지정된 key가 포함되어있는지 알려줌
  - keySet()  
  : 저장된 모든 키를 Set의 형태로 반환
  - boolean isEmpty()  
  : 비어있는지 알려줌


- 특징 :
  - HashMap은 Map 인터페이스를 기반으로 구현
  - Map의 수행을 모두 지원, key와 value에 null 허용
  - Map의 순서를 보장하지 않음
  - 동기화되지 않음
  - HashMap의 인스턴스에는 성능에 영향을 주는 두 개(초기 용량, 부하계수)의 파라미터 존재


- 초기 용량과 부하계수 :
  - 부하계수 : valeu 개수와 key의 총 수 비율
  - 부하계수↑ : 메모리 절약, 검색이 힘듬, 저장되는 value가 늘어남
  - 부하계수↓ : 메모리 낭비, 검색이 빠름

## HashSet
- java.util.HashSet

- 생성자/메서드 :
  - HashSet()  
  : 객체 생성
  - HashSet(int capacity)  
  : 주어진 값을 초기용량으로 하는 객체 생성
  - HashSet(int capacity, float fillRatio)  
  : 주어진 값을 초기용량과 load factor로 지정된 객체 생성
  - boolean add(Object value)  
  : 새로운 객체를 저장
  - boolean addAll(Collection c)  
  : 주어진 컬렉션에 저장된 모든 객체들을 추가한다.
  - void clear()  
  : 저장된 모든 객체를 삭제한다.
  - boolean contains(Object value)  
  : 지정된 객체를 포함하고 있는지 알려줌
  - boolean remove(Object value)  
  : 지정된 객체 삭제 (t:성공/f:실패)
  - boolean removeAll(Collection c)  
  : 주어진 컬렉션에 저장된 모든 객체와 동일한 것들을 삭제
  - boolean retainAll(Collection c)  
  : 주어진 컬렉션에 저장된 객체와 동일한 것만 남기고 삭제
  - Object[] toArray()  
  : 저장된 객체들을 객체배열의 형태로 반환
  - Object[] toArray(Object[] a)  
  : 저장된 객체들을 주어진 객체배열에 담는다.
  - boolean isEmpty()  
  : 비어있는지 알려줌


- 특징 :
  - 객체 사이에 순서를 제공하지 않음
  - 동기화 미제공

## PriorityQueue

- 메소드
  - peek()
  : head를 가져옴 / 삭제 x / 비어있는 경우 null 반환
  - poll()  
  : head를 가져옴 / 삭제 o / 비어있는 경우 null 반환
  - remove()  
  : head를 가져옴 / 삭제 x / 예외 발생
  - element()  
  : head를 가져옴 / 삭제 o / 예외 발생


- 특징
  - null을 허용하지 않음
  - ASC Ordering 된 상태로 출력
