# [Java] Initialize array

## 배열 선언

    //타입[] 변수명으로 선언
    data_type[] arr_name;

    //타입 변수명[]으로 선언
    data_type arr_name [];

    //특정 값 대입하며 배열 선언
    data_type[] arr_name = {value1, value2, value3, ... valueN};
    data_type[] arr_name = new data_type[] {value1, value2};

    //배열 생성해 초기화하면 배열의 주소가 들어가게 된다.
    arr_name = new data_type[n];

    //ex1. booelan 배열 선언 후 초기화
    boolean[] arr1;
    arr = new boolean[10];
    Arrays.fill(arr, false);

    //ex2. "Good"을 arr2에 넣기
    char[] arr2 = "Good".toCharArray();

## 메모리  

#### Heap
- 자바 배열은 Heap영역에 할당된다.
- 자료형이 할당되면 자동으로 초기화가 이루어진다.
- 메모리를 할당하기 위해서는 *"new"* 를 사용해야 한다.
- GC에 의해 자동소멸됨

#### Stack
- Heap에 할당된 주소를 Stack에서 기억한다.

#### ex.

    int[] a = {1,2,3};

**저장되는 정보**
- **스택** 영역 : a라는 배열이 메모리 4byte로 할당, 힙xx번지에 저장
- **힙** 영역 : xx번지부터 1, 2, 3이 각각 4byte로 할당
