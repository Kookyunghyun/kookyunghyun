---
    title: "[java] 조건문(switch / 다중 if else)을 활용한 계산기 만들기"

    categories : 
        잡다한개발일기
        
    description : "Java 조건문 if / 다중 if else / switch 를 활용해서 계산기 만들기"
    
    tags:
        Java
        연습
        일기
        
    last_modified_at: 2020-04-10
---
# 프로그래밍 언어 Java 배우기

## 문제 
**계산식을 입력받아서 계산하는 프로그램**<br/>

### 조건
* Class name : MyCalculator **
* 연산자 : +, -, *, /
* 피연사자 : 실수
* 11/0 -> “0으로 나눌 수 없습니다!”를 출력하고 종료.

### 실행예
계산식>>2 + 4<br/>
2 + 4의 계산결과는 6

## 문제분석
1. 실행 예시를 살펴보면 계산식을 입력받을 때 같은 라인에서 입력받을 수 있어야 함.
2. 피 연산자는 실수이지만 출력된 결과에서는 정수형으로 출력이됨으로 데이터형태의 변환이 필요함.
3. 한줄로 입력받은 문자열을 쪼개서 각각 변수에 알맞은 데이터 타입으로 집어 넣어줘야됨. 



## java 조건문 다중 if else 문 을 활용한 계산기만들기
```java
import java.util.Scanner;   //Scanner 클래스 import
 
public class MyCalculator
{
    public static void main(String[] args){ // main 메소드 생성

        Scanner sc = new Scanner(System.in); //Scanner 객체 생성

        String breaker; // 문자열 변수 선언
        float a;    // 실수형 변수 선언
        float b;    // 실수형 변수 선언

        System.out.print("계산식>>");  // 같은 라인에 입력받기위에 println이 아닌 print 사용
        a = sc.nextFloat(); //실수형 타입으로 리턴
        breaker = sc.next(); //문자열 타입으로 리턴
        b = sc.nextFloat(); //실수형 타입으로 리턴

        int i_a;
        int i_b;
        int i_result_p;
        int i_result_m;
        int i_result_mu;
        int i_result_d;
        i_a = (int)a;
        i_b = (int)b;
        //정수형 타입으로 데이터타입 변환        

        i_result_p = (int) i_a + i_b;
        i_result_m = (int) i_a - i_b;
        i_result_mu = (int) i_a * i_b;

       
        

        if(breaker.equals("+")){
            System.out.println(""+i_a+" " + breaker +" "+i_b +"의 계산결과는" +" " +(i_result_p));
        }
        else if(breaker.equals("-")){
            System.out.print(""+i_a+" " + breaker +" "+i_b +"의 계산결과는" +" " +(i_result_m));
        }
        else if(breaker.equals("*")){
            System.out.print(""+i_a+" " + breaker +" "+i_b +"의 계산결과는" +" " +(i_result_mu));
        }
        else if((breaker.equals("/")) && (b != 0)){
            System.out.print(""+i_a+" " + breaker +" "+i_b +"의 계산결과는" +" " +(a / b));
        }
        else if(b == 0){
            System.out.println("“0으로 나눌 수 없습니다!”");
        }
        else{
            System.out.println("잘못된 수식을 입력하였습니다.");
        }
    }
}

```
## java 조건문 switch 문 을 활용한 계산기만들기
```java
import java.util.Scanner;   //Scanner 클래스 import

public class MyCaculator
{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        String breaker;
        float a;
        float b;

        System.out.print("계산식>>");

        a = sc.nextFloat();
        breaker = sc.next();
        b = sc.nextFloat();

        switch (breaker){
            case ("+"):
            System.out.print(a + b);
            break;

            case ("-"):
            System.out.print(a - b);
            break;

            case ("*"):
            System.out.print(a * b);
            break;
            case ("/"):
            if (b == 0) {
                System.out.print("we can't do it");
                break;
            }
            System.out.print(a / b);
            break;
            default :
            System.out.print("we can't do it");

        }
    }
}
```

자바 조건문을 처음 접해봄. 처음에는 조건문의 조건식에 breaker == ("+") 처럼 equal 기호를 사용하여 작성했음. 결과값이 "잘못된 수식을 입력하였습니다."로만 떳음.<br/><br/>

구글링을통해 이유를 찾음. Java는 value 비교를 할때 **equals** 메소드를 사용함.<br/>

equals() 는 **메소드** 임. 비교하고자 하는 대상의**내용 그 자체를 비교** 함. <br/>
==은 비교를 위한 **연산자**. 비교하고자하는 대상의**주소값을 비교** 함.
<br/>
<br/>

equals 메소드는 Call By Value 를 통하여 값을 할당받은 내용 그 자체를 비교. 
== 는 Call By Reference 를 통하여 대상을 선언했을 때 부여된 객체의 주소값을 비교함.<br/>

```java
String A = "동춘";
String B = A ;
String C = new String("동춘");
```
이라고 하면 A,B,C가 갖는 내용은 모두 "동춘"이지만 **실질적으로 할당되는 주소값은 다름.** 아래 그림 참고.

![]({{ site.url }}/assets/images/Diary/My_Caculator/equlas.png    )

같은 내용이지만 다른 주소값을 할당받은 이유는 "동춘" 라는 문자열에 대입한것이 아닌 new String ("동춘")을 통해 새로운 문자열을 선언했기 때문.

```java
    System.out.println( A.equals(B)); // A 와 B 모두 같은 내용인 "동춘" 갖고있음으로 True
    System.out.println( A==B);  // A 와 B 모두 같은 주소값인 "777" 갖고있음으로 True
    System.out.println( A==C); //A 와 C 가지고 있는 주소값이 다름으로 False
    System.out.println( A.equals(C)); // A 와 C 모두 같은 내용인 "동춘" 갖고있음으로 True
```


