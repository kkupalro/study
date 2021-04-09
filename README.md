## **1장. 들어가며**

### **스프링이란**
- 의존 주입(Dependency injection; DI) 지원
- AOP(Aspect-Oriented Programming) 지원
- MVC 웹 프레임워크 제공
- JDBC, JPA 연동 기술 및 선언적 트랜잭션 처리 등 DB 연동 지원

### **참조한 책의 범위**
- 메이븐을 이용한 스프링 프로젝트 생성
- 스프링을 이용한 객체 생성 및 의존 주입 처리
- XML 설정과 자바 이용 설정
- 스프링을 이용한 AOP 프로그래밍 기초
- JDBC 프로그래밍과 선언적 트랜잭션 처리
- 스프링의 MVC 프레임워크를 이용한 웹 어플리케이션 개발 기초

### **준비물**
- JDK, Maven, Eclipse
- 스프링 4.1 버전
- 자바 8 버전
- 톰캣 9 버전

### **JDK 설치**
![noname01](https://user-images.githubusercontent.com/34331235/114175102-92052980-9974-11eb-865b-b8cbd4d2b324.png)<br>

### **메이븐 설치**
![image](https://user-images.githubusercontent.com/34331235/114175199-af39f800-9974-11eb-9716-bfc8312becd3.png)<br>
- http://maven.apache.org/   -> Download 클릭

### **메이븐 관련 환경 변수 설정 화면**
![image](https://user-images.githubusercontent.com/34331235/114175244-c0830480-9974-11eb-9f71-67be7c0811ef.png)<br>
![image](https://user-images.githubusercontent.com/34331235/114175349-e1e3f080-9974-11eb-9019-980890eca675.png)<br>


### **메이븐 버전 확인**
![image](https://user-images.githubusercontent.com/34331235/114175389-f45e2a00-9974-11eb-85aa-050d8b6c8f26.png)<br>


## **2장. 스프링 시작하기**

### **스프링을 이용한 자바 프로젝트 진행 과정**
- 메이븐으로 프로젝트 생성
- 이클립스에서 메이븐 프로젝트 임포트
- 스프링에 맞는 자바 코드와 설정 파일 작성
- 실행

### **메이븐 프로젝트 생성**
![image](https://user-images.githubusercontent.com/34331235/114175636-1f487e00-9975-11eb-8a9a-1524aad2eee7.png)<br>

### **C:\spring4\sp4-chap02\pom.xml**
![image](https://user-images.githubusercontent.com/34331235/114175641-2079ab00-9975-11eb-9bde-4da71b0d013e.png)<br>
- 08행	프로젝트의 식별 값을 입력함. 프로젝트 폴더와 동일한 이름인 sp4-chap02 사용
- 12-16행	4.1.0.RELEASE 버전인 sping-context 모듈을 사용
- 21-29행	1.8 버전을 기준으로 자바 소스를 컴파일하고 결과 클래스를 생성

### **기본 폴더 구조**
- src\main\java
- src\main\resources

### **메이븐 프로젝트 이클립스 임포트**
![image](https://user-images.githubusercontent.com/34331235/114175737-4606b480-9975-11eb-8a9c-da3e43b9cc0d.png)<br>

### **이클립스에서 메이븐 프로젝트를 임포트 한 결과**
![image](https://user-images.githubusercontent.com/34331235/114175770-5159e000-9975-11eb-81aa-813bf306dc2b.png)<br>

### **예제 코드 작성**
- **Greeter.java**	: 콘솔에 간단한 메시지를 출력하는 자바 클래스
- **applicationContext.xml**	: 스프링 파일 설정
- **Main.java**	: main() 메서드를 통해 스프링과 Greeter를 실행하는 자바 클래스

### **applicationContext.xml**
![image](https://user-images.githubusercontent.com/34331235/114175853-6b93be00-9975-11eb-8b36-36ea25f6ba7f.png)<br>
- **id**	: 빈 객체를 구분할 때 사용할 이름
- **class**	: 빈 객체를 생성할 때 사용할 클래스

### **스프링 설정과 객체 생성 간의 관계**
![image](https://user-images.githubusercontent.com/34331235/114175936-836b4200-9975-11eb-97d3-a3aff84c8df2.png)<br>
![image](https://user-images.githubusercontent.com/34331235/114176276-e361e880-9975-11eb-9279-4dad57abb9fd.png)<br>
- 실제 스프링은 XML 설정 파일을 읽어온 뒤에 자바의 리플렉션(Reflection) 기능을 이용해서 객체를 생성하고 set 메서드를 실행함.

### **실행 결과**
![image](https://user-images.githubusercontent.com/34331235/114176305-ee1c7d80-9975-11eb-9a6d-4e6045794ebd.png)<br>


### **스프링은 객체 컨테이너**
- **GenericXmlApplicationContext**	: XML로부터 객체 설정 정보를 가져옴.
- **AnnotationConfigApplicationContext**	: 자바 애노테이션을 이용한 클래스로부터 객체 설정 정보를 가져옴.
- **GenericGroovyApplicationContext**	: 그루비 코드를 이용해 설정 정보를 가져옴.

### **싱글톤 객체**
![image](https://user-images.githubusercontent.com/34331235/114176371-02607a80-9976-11eb-8864-ea8042024236.png)<br>
- **10-11행**	이름이 greeter인 빈 객체를 구해서 각각 g1과 g변수에 할당함
- **12행**		(g1==g2)의 결과값이 true로 출력
(g1 == g2)의 결과값이 true라는 것은 g1과 g2가 같은 객체라는 것을 의미함. 즉, 아래코드에서 getBean() 메서드는 같은 객체를 리턴하는 것임.

스프링은 별도 설정을 하지 않을 경우 한 개의 빈 객체만을 생성하며, 이들 빈 객체들이 ‘싱글톤(singleton)' 범위를 갖는다고 표현함. 싱글톤은 단일 객체를 의미하는 단어로서, 스프링은 기본적으로 한 개의 <bean> 태그에 대해 한 개의 빈 객체를 생성함. 따라서, 만약 다음과 같이 설정을 사용하다면, 생성 되는 빈 객체는 “greeter"에 해당하는 한 개 객채와 ”greeter1"에 해당하는 한 개 객체, 이렇게 두 개의 빈 객체가 생성됨.
<br>![image](https://user-images.githubusercontent.com/34331235/114176418-12785a00-9976-11eb-8222-67f1ca9cb2b5.png)<br>


## **3장. 스프링 DI**

### **의존 이란?**
- DI는 Dependency Injection의 약자로, 의존 주입이라는 의미로서, 각 객체간의 결합도를 낮추기 위해 나누어서 만들고 나중에 각 객체를 결합시켜서 사용하는 과정임.
- 한 클래스가 다른 클래스의 메서드를 실행할 때, 이를 ‘의존’한다고 표현함.

### **DI를 통한 의존 처리**
- DI는 의존하는 객체를 직접 생성하지 않고, 의존객체를 전달받는 방식을 사용함.
- 변경의 유연함 때문이 큰 장점임.

### **DI와 의존 객체 변경의 유연함**
![image](https://user-images.githubusercontent.com/34331235/114176504-2fad2880-9976-11eb-9cb0-8f87c9ac90ad.png)<br>

### **사용할 클래스 변경에 따른 소스코드 변경**
![image](https://user-images.githubusercontent.com/34331235/114176529-39cf2700-9976-11eb-8ee2-744ad804a531.png)<br>

### **생성할 의존 클래스의 변경에 따른 소스 수정**
![image](https://user-images.githubusercontent.com/34331235/114176556-45225280-9976-11eb-826d-695f9c79db96.png)<br>

### **실제 객체를 생성하는 한 곳만 수정**
![image](https://user-images.githubusercontent.com/34331235/114176577-4b183380-9976-11eb-9ed1-106bc1ad64e6.png)<br>
- 의존 객체를 주입하는 방식을 사용하면, 객체를 생성할 때 사용할 클래스의 변경을 한곳에서만 하면 됨.

### **스프링의 DI 설정**
- 스프링은 조립기 클래스의 생성자 코드처럼 필요한 객체를 생성하고 객체에 의존을 주입해줌.
- XML파일을 이용해 설정 정보를 작성해야 어떤 객체를 생성하고, 의존을 어떻게 주입할지 결정할수 있음.
<br>![image](https://user-images.githubusercontent.com/34331235/114176596-53706e80-9976-11eb-8a0f-7bffadb024b3.png)<br>
- *.xml 파일

### **DI 방식 1 : 생성자 방식 (생성자 주입)**
- 생성자의 피라미터 개수와 순서에 맞게 <constructor-arg> 태그를 작성해야함.
- 빈 객체를 생성하는 시점에 모든 의존 객체가 주입됨.
- **장점)** 빈 객체를 생성하는 시점에 의존한 모든 의존 객체를 주입받기 때문에, 이후 객체를 사용시 완전한 상태로 사용가능함.
- **단점)** 생정자의 피라미터 개수가 많을 경우, 태그가 어떤 의존 객체를 설정하는지 알아내려면 일일이 생성자의 코드를 확인해야함.
<br>![image](https://user-images.githubusercontent.com/34331235/114176620-5f5c3080-9976-11eb-9e03-07112028fc86.png)<br>
- *.java 파일

<br>![image](https://user-images.githubusercontent.com/34331235/114176725-8450a380-9976-11eb-9337-8aa9760d5310.png)<br>
- *.xml 파일

### **DI 방식 2 : 설정 메서드 방식 (세터 주입)**
- set으로 시작하는 프로퍼티 설정 메서드를 통해서 의존 객체를 주입할수 있음.
- **장점)** <property> 태그의 name 속성을 통해 어떤 의존 객체가 주입되는지 알수 있음.
- **단점)** <propety> 태그가 누락되어 도 빈객체가 생성되기 때문에, 객체를 사용하는 시점에 NullPointerException이 발생할 수 있음.
<br>![image](https://user-images.githubusercontent.com/34331235/114176775-97637380-9976-11eb-94b3-b3cfbe176cdc.png)<br>
- *.java 파일

<br>![image](https://user-images.githubusercontent.com/34331235/114176780-992d3700-9976-11eb-8358-9bc685b55bfb.png)<br>
- *.xml 파일


## **4장. 의존 자동 주입**

### **의존 자동 주입이란?**
- DI를 하기 위해서는 <constructor-arg>태그나 <property> 태그를 이용해서 주입할 대상 빈을 지정해야하지만, 의존 주입 기능을 사용하면 태그를 사용하지 않아도 스프링이 알맞은 의존 객체를 찾아 주입해줌.
- @Autowired 애노테이션과 @Resource 애노테이션을 사용하는 방법이 있음.

### **@AutoWired 애노테이션을 이용한 의존 자동 주입**
- 자동 주입 대상에 @Autowired 애노테이션을 사용함
- xml 설정에 <context:annotation-config /> 설정을 추가함
<br>![image](https://user-images.githubusercontent.com/34331235/114176831-a813e980-9976-11eb-9e6b-30274d98d04a.png)<br>
- *.xml 파일

<br>![image](https://user-images.githubusercontent.com/34331235/114176839-ab0eda00-9976-11eb-9dad-485eedcfd242.png)<br>
- *.java 파일

### **<context:annotation-config> 태그의 처리**
- AutowiredAnnotationBeanPostProcessor : @Autowired에 대한 의존 주입 처리를 함.
- RequiredAnnotationBeanPostProcessor : @Require에 대한 의존 주입 처리를 함.
- ConfigurationClassPostProcessor : @Configuration에 대한 설정 처리를 함.
- CommonAnnotationBeanPostProcessor : JSR-250(@PostConstruct 등)에 대한 라이프사이클 처리를 함.

### **@Qualifier 애노테이션을 이용한 의존 객체 선택**
- 이 애노테이션은 사용할 의존 객체를 선택할 수 있도록 해줌. 다음과 같이하여 사용함.
- 설정에서 빈의 한정자 값을 설정함.
- @Autowired 애노테이션이 적용된 주입 대상에 @Qualifier 애노테이션을 설정함.
- 이때, @Qualifier의 값으로 앞서 설정한 한정자를 사용함.
<br>![image](https://user-images.githubusercontent.com/34331235/114176900-b82bc900-9976-11eb-9bca-fc2cc1e1dde0.png)<br>
- *.xml 파일
<br>![image](https://user-images.githubusercontent.com/34331235/114176913-ba8e2300-9976-11eb-8547-7e5605f4039e.png)<br>
- *.java 파일

### **@Autowired의 필수 여부 지정**
- 스프링 컨테이너를 생성하면, @Autowired가 적용된 대상에 주입할 객첼르 찾을 수 없을 때 예외가 발생함.
- @Autowired 애노테이션이 적용된 대상에 꼭 의존 객체를 주입하지 않아도 될 때가 있고, 그럴 때 @Autowired 애노테이션의 required 속성값을 false로 지정하여 사용함.
<br>![image](https://user-images.githubusercontent.com/34331235/114176962-c8dc3f00-9976-11eb-92c7-86611f4f1532.png)<br>
- *.java 파일

### **@Autowired 애노테이션의 적용 순서**
- 타입이 같은 빈객체를 검색함. 한 개면 그 빈객체를 사용함. @Qualifier가 명시되어 있으면, @Qualifier와 같은 값을 갖는 빈객체여야 함.
- 타입이 같은 빈객체가 두 개 이상 존재하면, @Qualifier로 지정된 빈 객체를 찾음. 존재하면 그 객체를 사용함.
- (타입이 같은 빈객체가 두 개이상 존재하고 @Qualifier가 없을 경우) 이름이 같은 빈객체를 찾음. 존재하면, 그객체를 사용함.

### **@Resource 애노테이션을 이용한 의존 자동 주입**
- @Autowired 애노테이션이 타입을 이용해서 주입할 객체를 검색한다면, @Resource 애노테이션은 빈의 이름을 이용해서 주입할 객체를 검색함. 다음과 같이하여 사용함.
- 자동 주입 대상에 @Resource 애노테이션 사용함.
- xml 설정에 <context:annotation-config /> 설정 추가함
<br>![image](https://user-images.githubusercontent.com/34331235/114176984-d265a700-9976-11eb-9d71-3396ddb067c7.png)<br>
- *.xml 파일

<br>![image](https://user-images.githubusercontent.com/34331235/114176990-d42f6a80-9976-11eb-902e-3a94bdbef239.png)<br>
- *.java 파일

### **@Resource 애노테이션의 적용 순서**
- name 속성에 지정한 빈 객체를 찾음. 존재하면, 해당 객체를 주입할 객체로 사용함.
- name 속성이 없을 경우, 동일한 타입을 갖는 빈 객체를 찾음. 존재할 경우 해당 객체를 주입할 객체로 사용함
- (name 속성이 없고 동일한 타입을 갖는 빈 객체가 두 개 이상일 경우) 같은 이름을 가진 빈 객체를 찾음. 존재하면 해당 객체를 주입할 객체로 사용함.
- (name 속성이 없고 동일한 타입을 갖는 빈 객체가 두 개 이상이고 같은 이름을 가진 빈 객체가 없는 경우) @Qualifier를 이용해서 주입할 빈 객체를 찾음.

### **@Autowired vs @Resource**
- 적용 순서는 약간 다르지만, 둘 다 타입, 이름, @Qualifier 애노테이션을 모두 사용함.
- 차이점이라면, @Autowired 애노테이션은 required 애노테이션을 사용해서 필수 여부를 지정 할 수 있고, 타입과 이름 중 무엇을 먼저 사용하는가에 따라 다름.
- (@Autowired) 필드 이름을 바꾸면 그 필드를 사용하는 모든 코드가 영향을 받지만, @Qualifier를 사용하는 경우에는 이 태그의 값만 바꿔주면 된다. 그 만큼 변경의 여파가 작음.

## **5장. 자바 코드를 이용한 설정**

- @Configuration과 @Bean을 이용한 자바 코드 설정
- 자바 설정과 XML 설정의 조합

### **자바 코드 설정 기초**
- 자바 코드를 이용해서 스프링을 설정하는 방식은 XML으로 설정하는 것과 크게 다르지 않음.
- XML문법 대신 자바코드를 이용해 빈 객체를 생성하고 프로퍼티를 설정함.
- GenericXmlApplicationContext 클래스 대신 AnnotationConfigApplicationContext 클래스를 이용해서 컨테이너를 생성함
<br>![image](https://user-images.githubusercontent.com/34331235/114177161-0a6cea00-9977-11eb-8081-796929085edd.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177171-0e007100-9977-11eb-9eba-59e6cd985bb4.png)<br>

- XML설정은 빈 객체를 스프링 컨테이너가 생성하는 반면에 자바 설정에서는 자바 설정 코드에서 직접 객체를 생성함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177191-135dbb80-9977-11eb-959e-7b04078a2ebe.png)<br>

- 의존 객체 주입도 마찬가지임. XML 설정에서는 <property> 태그나 <constructor-arg>태그를 이용해서 설정한 의존 객체도 컨테이너가 주입하는 반면에, 자바 설정에서는 직접 의존 객체를 주입해주어야 함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177206-15c01580-9977-11eb-8f17-9efb28e5e32e.png)<br>

- 다른 빈 객체의 메서드를 호출하는 것은 ref 속성을 사용하는 것과 같음.

### **스프링은 @Configuration 설정 클래스를 상속 받아 새로운 클래스를 만들기 위해 CGLIB라는 기술을 사용함.**
- 클래스가 final 이어서는 안됨.
- 파라미터가 없는 기본 생성자를 제공해야 함.
- 따라서, @Configuration 애노테이션을 적용한 자바 설정 클래스도 위 조건을 충족해야함.

### **자바 코드 설정과 자동 주입**
- XML설정에서 @Autowired 나 @Resource 애노테이션에 대한 자동 주입 기능을 사용하려면 <context:annotation-config> 설정을 추가해야 함.
- 자바 설정을 사용할 경우에는 별도 설정을 하지 않아도 애노테이션을 이용한 자동 주입 기능이 활성화됨.

### **자바 설정에서 자동 주입의 한계**
- 자바 설정을 사용할 경우 자동 주입은 필드나 메서드에 대해서만 동작함.
- 생성자에 @Autowired 애노테이션을 적용하더라도, 생성자를 통한 자동 주입은 적용되지 않음.
- 그 이유는 @Bean 애노테이션을 적용한 메서드에서 객체를 직접 생성하기 때문임.
- 따라서, XML 설정을 사용하는 경우와 달리, 자바 설정을 사용할 때에는 스프링 컨테이너가 객체를 생성할 때 사용자가 생성자를 결정할 수 없고, 생성자를 통한 의존 객체 자동 주입을 적용할 수가 없음.

### **두 개 이상 클래스를 사용한 설정**
- 두  개 이상의 XML 설정 파일을 사용할 수 있는 것처럼 두 개 이상의 자바 설정 클래스를 사용 가능함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177273-296b7c00-9977-11eb-94d5-e7db88a747b8.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177280-2bcdd600-9977-11eb-9880-ab2c33dde62b.png)<br>

### **@Configuration 클래스를 주입받아 의존 설정하기**
- 스프링은 실제로 @Configuration 애노테이션이 적용된 클래스의 객체를 스프링 빈으로 등록함.
- 따라서, 자바 설정 클래스의 필드나 메서드 등에 @Autowired 가 적용되어 있으면, 다른 빈 객체와 마찬가지로 자동 주입을 적용함.

### **@Import 애노테이션 사용**
- 두 개 이상의 자바 설정이 있을 때, 이를 사용하는 또 다른 방법임.
- @Import 애노테이션의 값으로는 자바 설정 클래스의 목록을 지정함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177360-47d17780-9977-11eb-83fb-cfaed349be11.png)<br>

### **자바 코드 설정과 XML 설정의 혼합**
**- 자바 설정에서 XML 설정 임포트하기**
<br>![image](https://user-images.githubusercontent.com/34331235/114177343-41db9680-9977-11eb-906b-9b302db8625c.png)<br>

**- XML 설정에서 자바 설정 임포트하기**
- <context::annotation-config /> 설정 추가
- @Configuration 애노테이션 적용 클래스를 <bean> 태그로 등록
<br>![image](https://user-images.githubusercontent.com/34331235/114177414-57e95700-9977-11eb-87cd-3d8bc81d186b.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177431-5c157480-9977-11eb-9253-88b83c6b2cbf.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177441-5ddf3800-9977-11eb-8bca-f46db67f9bdb.png)<br>


## **6장. 빈 라이프 사이클과 범위**

- 컨테이너 초기화의 종료
- 빈 객체의 라이프사이클
- 싱글톤과 프로토타입 범위

### **01. 컨테이너의 초기화와 종료**
- 컨테이너 초기화 -> 빈 객체의 생성과 의존 객체 주입 및 초기화
- 컨테이너 종료 -> 빈 객체의 소멸
<br>![image](https://user-images.githubusercontent.com/34331235/114177480-6a639080-9977-11eb-96ee-93e1e87abf05.png)<br>


### **02. 빈 객체의 라이프사이클**
[ 객체 생성 ] -> [ 의존 설정 ] -> [ 초기화 ] -> [ 소멸 ]
- 스프링 컨테이너를 초기화 할 때, 스프링 컨테이너는 먼저 빈 객체를 생성함.
- <property> 태그로 지정한 의존을 설정함.
- 모든 의존 설정이 완료되면, 빈 객체의 초기화를 수행함.
- 스프링 컨테이너를 종료하면, 빈 객체의 지정한 메서드를 호출해서 빈 객체의 소멸을 처리함.

### **02. 1 빈객체의 초기화와 소멸 : 스프링 인터페이스**
- org.springframework.beans.factory.InitalizingBean
- org.springframework.beans.factory.DisposableBean
<br>![image](https://user-images.githubusercontent.com/34331235/114177515-73ecf880-9977-11eb-8fd2-3f0d0c80109d.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177519-75b6bc00-9977-11eb-9912-31c43e0a947b.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177525-77807f80-9977-11eb-96cb-40e3c5daf8f8.png)<br>


### **02. 2 빈객체의 초기화와 소멸 : 커스텀 메서드**
- <bean> 태그에서 init-method 속성과 destroy-method 속성을 사용해서 초기화 메서드와 소멸 메서드의 이름을 지정해주기만 하면 됨.
<br>![image](https://user-images.githubusercontent.com/34331235/114177540-7d766080-9977-11eb-84c4-9ac4f8742faa.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177543-80715100-9977-11eb-9bbe-df031c312f6f.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177547-81a27e00-9977-11eb-9958-af52233282cf.png)<br>


### **03. 객체 범위**
- 사용 빈도가 낮긴 하지만 프로토타입 범위의 빈을 설정할 수도 있음.
- 빈의 범위를 프로토타입으로 지정하면, 빈 객체를 구할 때마다 매번 새로운 객체를 생성함.
- 주의할 점은 프로토타입은 빈의 완전한 라이프사이클을 따르지 않는다는 점임.
- 스프링 컨테이너는 프로토타입의 빈 객체를 생성하고 프로피터를 설정하고 초기화 작업을 수행하지만, 컨테이너를 종료한다고 해서 생성한 프로토타입 빈 객체의 소멸 메서드를 실행하지 않음.
- 따라서, 프로토타입 범위의 빈을 사용할 때에는 빈 객체의 소멸 처리를 코드에서 직접 해야 함.

<br>![image](https://user-images.githubusercontent.com/34331235/114177584-8cf5a980-9977-11eb-8518-3ff02e8d79e1.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177595-8e26d680-9977-11eb-92c8-c015e88e56e0.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177601-8ff09a00-9977-11eb-862e-ccb39f3df065.png)<br>


## **7장. AOP 소개**

**- AOP란?**
**- 프록시와 AOP**
**- 스프링의 AOP 구현**

### **01. 프로젝트 준비**
- 스프링 AOP를 구현할 때는 pom.xml 파일에 aspectjweaver 모듈의 의존을 추가함
<br>![image](https://user-images.githubusercontent.com/34331235/114177672-a72f8780-9977-11eb-9351-e326929190e7.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177679-a8f94b00-9977-11eb-879a-6b48ffed1bd6.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177698-adbdff00-9977-11eb-9e27-e2695d7425b5.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177712-b0b8ef80-9977-11eb-9ee1-b8c82dd4d100.png)<br>

### **02. 프록시와 AOP**
- 기존 코드를 변경하지 않고 실행 시간을 출력할 수 있음. ImpleCalculator 클래스나 RecCalculator 클래스의 코드를 변경하지 않고,  이 두 클래스의 factorial() 메서드 실행 시간을 출력할 수 있음.
- 다음과 같이 실행 시간을 구하는 코드의 중복을 제거함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177746-ba425780-9977-11eb-9899-a4f516d7740c.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177761-bca4b180-9977-11eb-99cd-c7ae9b81e3a7.png)

### **02. 1 AOP**
- Aspect Oriented Programming의 약자로, 여러 객채의 공통으로 적용할 수 있는 기능을 구분함으로써 재사용성을 높여주는 프로그래밍 기법임.
- AOP의 핵심 기능과 공통 기능의 구현을 분리함으로써 핵심 기능을 구현한 코드의 수정 없이 공통 기능을 적용할 수 있게 만들어 줌.

**- 핵심 기능에 공통 기능을 삽입하기 위한 방법**
- 1. 컴파일 시점에 코드에 공통 기능을 추가하는 방법
- 클래스 로딩 시점에 바이트 코드에 공통 기능을 추가하는 방법
- 런타임에 프록시 객체를 생성해서 공통 기능을 추가하는 방법


### **03 스프링 AOP 구현**
- 공통 기능을 제공하는 Aspect를 구현함.
- Aspect를 어디(Pointcut)에 적용할지 설정함. 즉, Advice를 설정함.

### **POJO란?**
- Plain Old Java Object의 약자로서, 순수한 자바 객체를 의미함.
- 스프링이 출현하기 이전에 EJB라는 기술이 유행할 당시에는 EJB에 정의된 인터페이스나 클래스를 삭송받은 코드를 작성해야만 했음.
- 즉, 특정 기술에 종속된 코드를 만들어야 했는데, 이에 대한 반대되는 개념으로 EJB 출현 이전의 특정 기술에 종속되지 않은 자바 객체라는 의미로 POJO라는 용어를 사용하기 시작함.

### **03 1 AOP 구현 : XML 스키마 기반**
- XML 스키마를 이용할 경우, XML 설정을 이용해서 Aspect를 어디에 적용할지를 설정함.
<br>![image](https://user-images.githubusercontent.com/34331235/114177844-d645f900-9977-11eb-8de4-d5b7b1bd691e.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177850-d8a85300-9977-11eb-8eae-28353b50456e.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114177859-db0aad00-9977-11eb-9124-f278ee1f2591.png)<br>

### **03. 2 AOP 구현 : @Aspect 애노테이션 이용**
- @Aspect 애노테이션을 이용한 공통 기능의 구현 방법은 POJO 방식과 크게 다르지 않지만, @Aspect 애노테이션을 적용한 클래스에 공통 기능과 Pointcut을 설정한다는 차이점이 있음
<br>![image](https://user-images.githubusercontent.com/34331235/114177887-e5c54200-9977-11eb-9018-8fc2ade873bb.png)<br>
- 클래스에 @Aspect 애노테이션을 적용함.
- @Pointcut 애노테이션을 이용해서 Pointcut을 설정함.
- @Around 애노테이션을 사용해서 메서드가 Around Advice로 사용된다고 설정함.
<br>![image](https://user-images.githubusercontent.com/34331235/114178030-1dcc8500-9978-11eb-922b-3419a0cf4374.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114178036-1f964880-9978-11eb-9be5-4a301192f171.png)<br>


### **03. 3 ProceedingJoinPoint의 메서드**
- Around Advice에서 사용할 공통 기능 메서드는 대부분 파라미터로 전달받은 ProceedingJoinPoint의 proceed() 메서드만 호출하면 됨.

### **Proceeding.JoinPoint 인터페이스가 제공하는 대표적인 메서드**
- Signature getSignature( ) : 호출되는 메서드에 대한 정보를 구함
- Object getTarget( ) : 대상 객체를 구함.
- Object[] getArgs( ) : 파라미터 목록을 구함.

org.aspectj.lang.Signature 인터페이스가 제공하는 대표적인 메서드
- String getName( ) : 메서드의 이름을 구함.
- String toLongString( ) : 메서드를 완전하게 표현한 문장을 구함. (리턴 ,파라미터 타입이 모두 표시됨.)
- String toShortString( ) : 메서드를 축약해서 표현한 문장을 구함. (기본 구현은 메서드의 이름만을 구함.)

### **03. 4 프록시 생성 방식**
- POJO방식 XML 설정
<br>![image](https://user-images.githubusercontent.com/34331235/114178088-2e7cfb00-9978-11eb-948f-5b2b6b11fa17.png)

- @Aspect 방식 XML 설정
<br>![image](https://user-images.githubusercontent.com/34331235/114178093-3046be80-9978-11eb-9679-20a9212e164c.png)

### **03. 5 execution 명시자 표현식 예**
- execution(public void set*(..)) : 리턴 타입이 void이고 메서드 이름이 set으로 시작하고, 파라미터가 0개 이상인 메서드 호출함. 파라미터 부분에 ‘..’을 사용하여 파라미터가 0개 이상인 것을 표현함.
- execution(* spring .. *.*(..)) : spring 패키지의 타입에 속한 파라미터가 없는 모든 메서드 호출함.

### **03. 6 Advice 적용 순서**
- (프록시 적용 순서 ) [ 실행시간측정 프록시 ] -> [ 캐시 프록시 ] -> [ 실제 대상 객체 ]
<br>![image](https://user-images.githubusercontent.com/34331235/114178119-3b015380-9978-11eb-83d4-e905b4b5bb6e.png)<br>
<br>![image](https://user-images.githubusercontent.com/34331235/114178129-3fc60780-9978-11eb-9b7a-ab1f39d80ec2.png)<br>
**...**

