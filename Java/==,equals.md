# [Java] ==과 equals()의 비교

#### Method 비교
- *"=="* 는 객체 자체를 비교
- *equals()* 는 객체의 값을 비교


    String s1 = "abcd";
    String s2 = s1;
    String s3 = new String("abcd");
    String s4 = "abcd";

    s1 == s2; // true
    s2 == s3; // false
    s1.equals(s2); // true
    s2.equals(s3); // true
    s1 == s4; // true

s1과 s2는 같은 주소 값을 참조  
s3는 new String()으로 새로운 객체를 생성  
s4도 s1과 같은 주소 값을 참조함
