# Kotlin 기본 문법
> Kotlin의 기본 문법에 대해 공부한 것을 기록하는 페이지입니다.

## 변수 선언 방법
> **val / var 변수이름: 데이터타입**

    // data라는 값을 가진 String 변수 value1 선언, 수정 불가
    val value1: String = "data"

    // data라는 값을 가진 String 변수 value2 선언, 수정 가능
    var value2: String = "data"

    // 값을 가지고 데이터 타입을 알아서 유추해 String 타입으로 선언
    val value3 = "data"

    val num1 = 123 // int로 유추
    val num2 = 123L // long으로 유추
    val num3 = 123.0f // float로 유추


## 함수 선언 방법
> **fun 함수명(변수명: 변수타입) { 함수 정의 }**

    //반환 값이 없는 함수, Unit은 생략 가능
    fun 함수명(변수명: 변수타입): Unit {}

    // 반환 값이 있는 함수  
    fun 함수명(변수명: 변수타입): return타입 { return value }

    // "="을 이용해 반환 값을 바로 명시 가능
    fun 함수명(변수명: 변수타입): return타입 = return value

    // return 타입을 명시하지 않아도 값을 이용해 유추
    fun 함수명(변수명: 변수타입) = return value

## for문 비교 (Java vs. Kotlin)
: Java에서는 foreach문에서 :을 사용하고, Kotlin에서는 in을 사용한다.  
Kotlin의 for문에서 x in 1..5는 x가 1부터 5까지 라는 의미이다.

    //Java
    ArrayList<String> arrayList = new ArrayList<>();
    for (String s : arrayList) {
         Log.d("TAG", "string : " + s);
    }
    for (int i = 1; i <= 5; i++) {
         Log.i("TAG", "index : " + i);
    }

    // Kotlin
    val arrayList = ArrayList<String>()
    for (s in arrayList)  {
         Log.d("TAG", "string  : " + s)
    }
    for (x in 1..5) {
         println(x)
    }



## String (Java vs. Kotlin)

### 1. 문자열 참조
: 변수를 문자열에 담을 때 +를 이용해 합치지만, Kotlin에서는 $를 이용해 쉽게 처리 할 수 있다.

    //Java
    String name = "seohyun"
    int age = 19
    String query = "Name: " + name + "/ Age: " + age;

    //Kotlin
    val name = "seohyun"
    val age = 19
    val query = "Name: $name / Age: $age"

    //$의 응용
    val nameLen1 = "${name.length}" // print : 7
    val nameLen2 = "$name.length" // seohyun.length (뒤에 .length는 문자열처리)

### 2. 여러 줄의 문자열
: Kotlin에서 """내에 작성하면 개행이나 공백을 포함한 모든 문자가 여과 없이 그대로 출력된다.

    //Java
    String heroes = "D.Va\n"
              + "Lucio\n"
              + "Mercy\n"
              + "Soldier: 76\n";

    //Kotlin
    val heroes = """
    D.va
    Lucio
    Mercy
    Soldier: 76
    """

## Lambdas 지원

    //No Lambdas
    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            view.setAlpaha(0.5f)
        }
    }

    //Lambdas
    btn.setOnClickListener {
        view -> view.alpha = 0.5f
    }

    //한 번 더 축약, onClick에 받는 변수가 한 개여야 it 사용 가능
    btn.setOnClickListener {
        it.alpha = 0.5f
    }

## NULL
: Kotlin에서는 NonNull을 지향하고 있다. 변수에 null 값을 넣기 위해서는 ?를 사용해야 한다.

    var value: String? = null

#### 주의 사항
: Kotlin에서 타입을 자동으로 유추해준다고, 타입을 지정하지 않으면 타입 오류가 발생하게 된다.

    // type 오류 발생
    var nullValue = null
    nullValue = "널아님"

**자바와 비교**

    //Java
    public void set(@NotNull String a, @Nullable String b) {
         //Do nothing
    }

    //Kotlin
    fun set(a: String, b: String?) {
         //Do nothing
    }
