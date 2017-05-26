# [Data Structure] Simple Linked List

## 기본 구조
- 각 노드들은 다음 노드를 가리키는 하나의 참조만 갖는다.
- 마지막 노드가 가리키는 참조값은 null이다.
- 헤더는 처음 노드의 참조를 갖고 있다.


### 데이터의 삽입
1. 맨 앞(Header) 삽입
  1. 헤더가 가리키고 있는 값을 삽입하고자 하는 노드의 다음 노드를 가리키는 값에 넣어준다.
  2. 헤더가 가리키고 있는 값을 새로 추가한 노드로 바꿔준다.


2. 중간/맨끝 삽입
  1. 삽입하고 싶은 위치 바로 전 노드까지 이동한다.
  2. 이전 노드가 가리키는 값을 삽입하고자 하는 노드의 다음 노드를 가리키는 값에 넣어준다.
  3. 이전 노드가 가리키고 있는 값을 새로 추가한 노드로 바꿔준다.


### 데이터 삭제
1. 맨 앞 삭제
  1. 헤더가 가리키고 있는 값을 삭제하고자 하는 노드가 가리키고 있는 값으로 변경한다.
  2. 삭제하고자 하는 노드에 null 값을 넣는다.


2. 중간/맨끝 삭제
  1. 삭제하고자 하는 노드가 가리키는 값을 이전 노드가 가리키는 값으로 변경한다.
  2. 삭제하고자 하는 노드에 null 값을 넣는다.


### 소스 코드

    public class MyLinkedList {

        private Node header;

        public MyLinkedList(){
            header = new Node(null);
            size = 0;
        }

        private class Node{

            private Object data;
            private Node nextNode;

            Node(Object data){
                this.data = data;
                this.nextNode = null;
            }
        }

        // index 위치에 data를 삽입
        public void add(int index, Object data){

            Node newNode = new Node(data);

            // 맨 처음 삽입
            if(index == 0) {
                newNode.nextNode = header.nextNode;
                header.nextNode = newNode;

                return;
            }

            Node previous = header.nextNode;

            for (int i = 1; i < index; i++) {
                previous = previous.nextNode;
            }

            newNode.nextNode = previous.nextNode;
            previous.nextNode = newNode;
        }


        // index 위치의 노드를 제거
        public void remove(int index){

            if(index == 0) {
                Node firstNode = header.nextNode;
                header.nextNode = firstNode.nextNode;

                return;
            }

            Node previous = header.nextNode;

            for (int i = 1; i < index; i++) {
                previous = previous.nextNode;
            }

            Node removeNode = previous.nextNode;
            previous.nextNode = removeNode.nextNode;

        }
    }
