---
    title: "[java] 초심자도 이해하는 스캐너 (Scanner Class) 를 사용한 입력방법"

    categories:
        Java
    
    description : "[java] 초심자도 이해하는 스캐너 (Scanner Class) 를 사용한 입력방법"
    
    tags:
         Java
         객체지향
        
    last_modified_at: 2020-04-07
---
# Scanner란 무엇일까?
---------------------------------------
<br/>
Java 에서 Scanner 는 객체를 만들기 위한 **클래스** 입니다.

> class 는 object를 만들기 위한 붕어빵 틀!

위에서 이야기 하는것과같이 클래스 는 붕어빵을 만들기 위한 틀 입니다. 

우리는 이처럼 붕어빵 틀을  **클래스** , 이 붕어빵 틀에서 만들어진 붕어빵을 Object 즉 **객체**라고 이야기 하죠.

### 정리
즉 Scanner 클래스는 입력을 받게하는 객체를 만드는 붕어방 틀 입니다.<br/><br/>

---------------------------------------

# Scanner 로 입력받는 방법
<br/>
## Step.1 **Scanner 호출**

클래스를 사용하기위해서는 Scanner 클래스를 import를 통해 호출해야합니다.
```java
import java.util.Scanner;
```
Scanner 클래스는 java.util 패키지에 들어있음으로 위와같이 import를 해주시면 됩니다. 

저 한줄은 **"앞으로 Scanner클래스를 사용할꺼야"** 라고 컴퓨터에게 이야기 해주는 역할을 합니다.
<br/>
<br/>
## Step.2 **Scanner 의 객체 생성**

위에서도 이야기 한것처럼 저희는 Scanner라고 하는 붕어빵 틀에서 객체를 생성해야합니다. 그리고 객체를 생성하는 방법은 아래와 같습니다.

```java
Scanner sc = new Scanner(System.in);
```
저희는 Scanner 클래스에서 sc라는 객체를 생성했습니다. System.in에 입력한 값을 바이트 단위로 읽게합니다.
<br/>
<br/>

## Step.3 **Scanner 로 입력받기! **
```java
import java.util.Scanner;

public class scannerTest {
    public static void main(String[] args) {
        String city1;
        String city2;
        String city3;
        String city4;
        int num1;
        int num2;
        //변수 선언문 ( 자료타입 + 변수 이름)
        
        Scanner sc = new Scanner(System.in);
        //scanner 클래스에서 객체 생성
        System.out.println("도시의 이름을 입력하세요");
        city1 = sc.next();
        System.out.println("도시의 이름을 입력하세요");
        city2 = sc.next();
        System.out.println("도시의 이름을 입력하세요");
        city3 = sc.next();
        System.out.println("도시의 이름을 입력하세요");
        city4 = sc.next();
        System.out.println("숫자를 입력하세요");
        num1 = sc.nextInt();
        System.out.println("숫자를 입력하세요");
        num2 = sc.nextInt();
    
        System.out.println("도시의 이름들은 "+city1+","+city2+","+city3+","+city4+"이고 입력한 숫자의 값은"+num1+","+num2+"입니다.");
    }   
}
```
Scanner를 통하여 도시의 이름들을 입력받았고 그것을 문자열로 리턴했습니다.<br/>
Scanner를 통하여 숫자를 입력받았고 그것들을 Int 타입으로 리턴하였습니다.
## Step.4 **Scanner의 특징**

Scanner는 입력받은 값들을 공백문자 (\t , \f , \r , \n , ' ')단위로 읽습니다. 
<br/>
만약 여러분들이 **"서울 대전 대구 부산 123 456"** 이라고 입력을 했다면, Scanner는 서울 , 대전 , 대구 , 부산 , 123 ,456 이라고 읽습니다.
<br/><br/>
아래의 코드 예제를 확인해보면 이해가 수월하실 겁니다.
```java
Scanner scanner = new Scanner(System.in);

String city1 = scanner.next();  //"서울"
String city2 = scanner.next();  //"대전"
String city3 = scanner.next();  //"대구"
String city4 = scanner.next();  //"부산"
int num1 = scanner.nextInt();   //"123"
int num2 = scanner.nextInt();   //"456"
```
Scanner클래스의 next 메소드를 이용하여 입력된 값을 각각 변수에 저장하였습니다. 이때 Scanner 클래스는 띄어쓰기를 단위로 입력된 값들을 읽었기 때문에 각각의 변수에 서울 , 대전 , 대구 , 부산 , 123 , 456 값이 들어간것을 확인할 수 있습니다.

## Step.5 **Scanner의 메소드**

Scanner의 대표적인 메소드 몇가지를 살펴보도록 합시다.
<br/><br/>
### next + 자료형() 메소드
```java
scanner.next(); //문자열로 리턴
scanner.nextInt();  //Int 타입으로 리턴
scanner.nextFloat();    //Float 타입으로 리턴
scanner.nextDouble();   //Double 타입으로리턴
scanner.nextBloolean(); //boolean 타입으로로 리턴
```
위처럼 next + 자료형 () 메소드를 활용하면 입력받은 값을 특정한 타입으로 변환하여 리턴받을 수 있습니다.

### nextLine()

```java
scanner.nextLine();
```
한줄을 통째로 받아오게하는 메소드 입니다. 하지만 nextLine()은 개행문자 (\n과 같이 줄바꿈을 나타내는 문자)까지만 리턴받을 수 있습니다.
    
### next()

```java
scanner.next();
```
띄어쓰기를 기준으로 한 단어를 리턴받습니다.
