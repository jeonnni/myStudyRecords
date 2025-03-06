## 용어정리

#### 자바란
> 자바(Java)는 다양한 프로그램을 만들 수 있는 인기 있는 프로그래밍 언어
> 운영체제에 관계없이 실행할 수 있다는 특징

#### 스프링 부트란
> 자바 웹 프로그램을 쉽고 빠르게 만들기 위해 개발된 도구입니다.

#### 스프링 부트 개발 환경
> JDK 설치 -> IDE 설치 -> 프로젝트 만들기

#### JDK(Java Development Kit)
> 자바 프로그램을 개발하고 실행하는 데 필요한 도구 모음. 컴파일러, 실행 환경(JRE) 등이 포함돼 있다 

<br>

___
#### 웹 서비스 동작 원리
> 클라이언트 요청에 따른 서버의 응답으로 동작한다
> 웹 브라우저가 클라이언트로서 동작하고
> 스프링 부트가 서버 역할을 수행한다
> 이때 반드시 서버를 실행해야만 웹 브라우저를 통해 응답받을 수 있다

<br>

___
#### localhost:8080/hello.html 의미
#### ***localhost*** 
> '내 컴퓨터'의 주소인 127.0.0.1 을 고유하게 지칭한 것
#### ***8080***
> 스프링 부트가 동작하는 기본 포트번호
#### ***hello.html***
> 서버에 요청하는 파일

<br>

___
#### MVC 패턴 (Model-View-Controller Pattern)
> 모델 (Model): 데이터를 관리하는 역할을 담당합니다.

> 뷰 (View): 화면을 담당하는 템플릿으로, 간단히 '뷰'라고도 불립니다.

> 컨트롤러 (Controller): 클라이언트의 요청을 받아 서버에서 이를 처리하는 역할을 합니다.

> 이러한 역할 분담을 통해 웹 애플리케이션의 구조를 명확히 하고, 유지보수성을 높이는 기법이 바로 MVC 패턴입니다.

**요청 처리 흐름**
> 클라이언트 → 요청 → 컨트롤러

> 컨트롤러 → 모델 → 데이터 → 모델

> 모델 → 뷰 → 화면 출력 → 클라이언트

<br>
<br>
<br>


## MVC 패턴을 활용한 뷰 템플릿 페이지 만드는 법
> mustache 는 뷰 템플릿을 만드는 도구, 즉 뷰 템플릿 엔진을 의미한다. 
> 머스테치 외의 템플릿 엔진으로는 JSP 등이 있다
>
> 1. resources -> templates 디렉터리에서 마우스 오른쪽 버튼 누르고 New -> File
> 2. 확장자는 -> 파일명.mustache 
> 
> 머스테치 파일의 기본 위치는 src > main > resources > templates 
>
> 
> 1. 머스테치 플러그인을 설치하기 위해 
> 2. File -> Settings 클릭 후, 왼쪽 목록에서 plugins 선택하고 오른쪽에 Marketplace 탭을 클릭 후 mustache 를 검색한다.
> 3. 검색 결과에서 Handlebars/Mustache 선택하고 install
>
> 빈 화면에 파일명.mustache 파일이 뜬다
> 1. 제일 윗줄에 doc 입럭한 후 Tab 키를 누르면 기본 HTML 코드가 자동으로 작성된다

<br>

자바 코드가 바뀔때는 서버를 재시작해야 하지만, 
머스테치 코드가 바뀔 때는 망치 아이콘만 눌러 빌드해도 된다
> MAC 단축키 -> `COMMAND+F9`


<br>
<br>
<br>

___
#### 한글 깨짐 현상
> src > main > resources > application.properties 파일에 아래 코드 추가
```
server.servlet.encoding.force=true
```

<br>

___

#### 어노테이션(Annotation)이란?
> 어노테이션은 소스 코드에 추가하는 메타데이터의 한 종류로, 프로그램이 처리할 데이터가 아니라 컴파일 및 실행 과정에서 코드의 동작을 안내하는 추가 정보이다.
자바에서는 @ 기호를 사용하여 어노테이션을 표시한다.


#### addAttribute() 메서드 
```
model.addAttribute("변수명","변숫값");
```

###### 적용코드

```
@Controller
public class FirstController  {
    @GetMapping("/test")
    public String niceToMeetYou (Model model){ 
        //model 객체 받아오기

        model.addAttribute("username","user");

        return "greetings"; 
        //greetings.mustache 파일 변환
    }
}
```

<br>
<br>
<br>

___
#### 뷰 템플릿
> 웹 페이지를 하나의 틀로 만들고 여기에 변수를 삽입해 서로 다른 페이지로 보여주는 기술

#### MVC 패턴
> 웹 페이지를 화면에 보여주고 view <br>
> 클라이언트의 요청을 받아 처리하고 Controller <br>
> 데이터를 관리하는 Model <br>
> 역할을 영역별로 나누어 하는 기법을 말한다

#### 뷰 템플릿 생성 위치
> src > main > resources > templates 디렉터리에 만든다 <br>
> 뷰 템플릿 확장자는 .mustache

#### 컨트롤러 생성 위치
> src > main > java <br>
> 기본 패키지 안에 컨트롤러 패키지를 만든 후 자바 클래스 파일을 생성하는 방식으로 만든다. 확장자는 .java

#### 모델을 통해 변수 등록하는 방법 
> 모델은 컨트롤러의 메서드에서 매개변수로 받아 온다. 모델에서 변수를 등록할 때는 addAttribute() 메서드를 사용한다

```
model.addAttribute("변수명","변수값");
```


<br>
<br>
<br>

___
#### H2 DB


#### 스프링부트는 자바 언어를 사용하지만 DB는 SQL 언어를 사용한다 그럼 어떻게 DB에 자바로 명령할 수 있을까?
> JPA(Java Persistence API)
JPA는 자바 애플리케이션에서 데이터베이스와 상호작용할 수 있도록 도와주는 API로, 객체지향적인 방식으로 데이터를 관리할 수 있게 해준다

> JPA 의 핵심 도구로는
엔티티 entity - 자바 객체를 DB가 완전히 이해할 수 있게 만든 것으로 이를 기반으로 테이블이 만들어진다
레포지토리 - 엔티티가 DB속 테이블에 저장 및 관리될 수 있게 하는 인터페이스