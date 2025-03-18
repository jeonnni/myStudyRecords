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

@Entity 어노테이션
JPA에서 제공하는 어노테이션으로 이 어노테이션이 붙은 클래스를 기반으로 DB 속 테이블이 생성된다 

---

#### 리포지터리를 사용하는 이유?
> 👉 데이터를 DB에 안전하게 저장하고 관리하기 위해!
#### ✅ DTO를 엔티티로 변환하는 이유?
> 👉 웹 요청 데이터(DTO)와 DB 엔티티(Entity)를 분리해서 관리하려고!
#### 📌 기본 흐름:
> 웹 요청 → DTO → 엔티티 변환 → DB 저장 🚀

#### 📌 세부 정리
> ✅ 1. 리포지터리를 사용해서 엔티티를 DB에 저장하는 이유
데이터를 DB에 저장해야 영구적으로 보관 가능 (서버 종료돼도 유지)
JPA 리포지터리를 사용하면 간단한 코드로 DB 저장 가능 <br>
✅ 2. DTO를 엔티티로 변환하는 이유
DTO (Data Transfer Object) → 웹 요청 데이터 전달용
Entity → 실제 DB 테이블과 연결된 객체
DTO를 그대로 DB에 저장하면 보안 문제 발생 가능 (ex. 비밀번호, 불필요한 데이터 등)
#### 👉 결론:
> ✅ 리포지터리는 DB 관리를 쉽게 해주고,<br>
> ✅ DTO는 웹 요청 데이터와 DB 데이터를 분리하는 역할을 한다! 🚀


---

#### 📌 ArticleRepository란?
> ArticleRepository는 JPA에서 제공하는 CrudRepository 인터페이스를 상속받아 엔티티(Article)를 관리하는 리포지터리

> 이를 통해 데이터 생성(Create), 조회(Read), 수정(Update), 삭제(Delete) 기능을 쉽게 구현할 수 있다 

```
package com.example.firstproject.repository;

import com.example.firstproject.entity.Article;
import org.springframework.data.repository.CrudRepository;

public interface ArticleRepository extends CrudRepository<Article, Long> {
}

```
#### ✅ CrudRepository<T, ID>란?
> JPA에서 제공하는 인터페이스로 기본적인 CRUD 기능(생성, 조회, 수정, 삭제)을 자동으로 제공

#### ✅ 제네릭(<>) 안의 두 가지 요소
> Article → 관리할 엔티티 클래스

> Long → 엔티티의 고유 식별자(id) 타입

#### ✅ 이점
> SQL 없이 간단한 코드만으로 데이터 관리 가능

> 직접 구현할 필요 없이 JPA가 자동으로 처리

#### 👉 결론: CrudRepository를 상속하면 DB 조작이 간편해진다! 🚀

#### 즉 ArticleRepository는 CrudRepository 가 제공하는 기능을 별도 정의 없이 그대로 사용할 수 있다
#### DB에서 데이터를 생성하고 읽고 수정하고 삭제하는 기본 동작을 추가 코드로 구현할 필요없이 CrudRepository 에서 상속받아 사용가능 

<br>

#### @Autowired
> 스프링 부트에서 제공하는 어노테이션으로 이를 컨트롤러의 필드에 붙이면 스프링 부트가 만들어 놓은 객체를 가져와 주입해 준다. 이를 의존성 주입 (DI, Dependency Injection)

<br>

#### H2 DB 접속하는 방법
1. 설정 파일 수정
    > src/main/resources/application.properties 파일에서 H2 웹 콘솔을 활성화
    ```
    # H2 DB에 웹 콘솔로 접근할 수 있도록 허용
    spring.h2.console.enabled=true
    ```
2. 서버 재시작 & 웹 브라우저 접속
    > 변경 사항을 반영하기 위해 서버 재시작 하고 웹 브라우저에서 localhost:8080/h2-console 접속

3. JDBC URL 확인 및 입력
    >   JDBC URL은 서버 실행마다 변경되므로 최신 값 입력 필요<br>
        JDBC URL 찾는 방법:<br>
        인텔리제이 RUN 탭 열기<br>
        command + F로 jdbc 검색<br>
        jdbc:h2:mem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 값을 복사<br>
        H2 콘솔 (localhost:8080/h2-console)의 JDBC URL에 붙여넣기<br>

<br>

## 롬복
> 롬복 lombok → 자바 코드의 간소화를 위해 getter, setter, constructor, toString 등의 필수 메서드를 자동으로 생성해주는 라이브러리로, 로깅 기능을 통해 println() 문을 개선할 수 있다.

> 로깅 logging → 프로그램의 수행 과정을 기록으로 남기는 것을 말한다 

> 리팩터링 refactoring → 코드의 기능은 변함이 없이 코드 구조 또는 성능을 개선하는 작업

##  리팩터링하기

1. build.gradle 코끼리 모양의 파일을 클릭한다 
2. 코드 중간에 `dependencies` 여기 안에 아래 코드 추가한다
    
    `compileOnly 'org.projectlombok:lombok'annotationProcessor 'org.projectlombok:lombok'`
    
3. 편집에 나타난 코끼리를 누른다. 그럼 자동으로 롬복관련 라이브러리를 인터넷에서 자동으로 다운로드됨
    
    

DTO 리팩터링 하는 법

1. `Constructor` 간소화 하기 
    1. **기존 생성자 삭제**
        - `Generate -> Constructor` 로 추가한 생성자 전체 제거
    2. **어노테이션 추가**
        - `@AllArgsConstructor` 추가
    3. **자동 생성자 적용**
        - 클래스 내부 모든 필드를 포함하는 생성자가 자동 생성됨
    
    ```java
    @AllArgsConstructor //어노테이션 추가
    public class ArticleForm {
     private String title;  
     private String content; 
     
    //    public ArticleForm(String content, String title) {
    //        this.content = content;
    //        this.title = title;
    //    } 생성자 삭제
    }
    
    ```
    

 2. `toString()` 간소화 하기 

1. **기존 `toString()` 메서드 삭제**
2. **`@ToString` 어노테이션 추가**
    - 클래스 내부 모든 필드를 자동으로 문자열 변환

```java
@AllArgsConstructor
@ToString //어노테이션 추가 
public class ArticleForm {
    private String title;
    private String content;

    // 데이터를 잘 받았는지 확인할 toString() 메서드 (Generate.. -> toString)
//    @Override
//    public String toString() {
//        return "ArticleForm{" +
//                "title='" + title + '\'' +
//                ", content='" + content + '\'' +
//                '}';
//    }  메서드 전체 삭제 
}

```

#### 엔티티도 마찬가지로 리팩터링한다.
> @AllArgsConstructor → 생성자를 대채하는 어노테이션 추가 작업

> @ToString → 메서드를 대체하는 어노테이션 추가 작업


<br>
<br>
<br>


## 📌 `println()` 대신 로깅 기능 사용하기

### 🔹 로깅이란?

로깅은 **자동차 블랙박스**와 같다.

🚗 블랙박스가 자동차에서 일어나는 모든 순간을 기록하듯이,

🖥 서버에서도 **로깅 기능**을 이용하면 **발생한 모든 이벤트를 기록**할 수 있다.

### 🧐 `println()`과 로깅의 차이

| 구분 | `println()` | 로깅 (`log.info()`) |
| --- | --- | --- |
| 출력 방식 | 콘솔에 즉시 출력 | 로그 파일 또는 콘솔에 기록 |
| 데이터 저장 | X (다시 볼 수 없음) | O (나중에도 확인 가능) |
| 활용도 | 단순 확인용 | 디버깅, 에러 추적, 성능 분석 |

---

## 📝 코드 변경: `println()` → 로깅

### 📌 기존 코드 (`println()` 사용)

```java
java
복사편집
System.out.println(form.toString()); // DTO에 폼 데이터가 잘 담겼는지 확인
System.out.println(article.toString()); // 엔티티 변환 확인
System.out.println(saved.toString()); // DB 저장 후 반환된 엔티티 확인

```

### ✅ 변경 코드 (`log.info()` 사용)

```java
java
복사편집
log.info(form.toString()); // DTO에 폼 데이터가 잘 담겼는지 확인
log.info(article.toString()); // 엔티티 변환 확인
log.info(saved.toString()); // DB 저장 후 반환된 엔티티 확인

```

## 🛠 전체 코드 (로깅 적용 완료)

```java
java
복사편집
package com.example.firstproject.controller;

import com.example.firstproject.dto.ArticleForm;
import com.example.firstproject.entity.Article;
import com.example.firstproject.repository.ArticleRepository;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;

@Slf4j // 로깅 기능 추가
@Controller
public class ArticleController {

    @Autowired // 스프링이 자동으로 Repository 객체 주입
    private ArticleRepository articleRepository;

    @GetMapping("/articles/new")
    public String newArticleForm() {
        return "articles/new";
    }

    @PostMapping("/articles/create")
    public String createArticle(ArticleForm form) {
        // 📝 1. DTO에 폼 데이터가 잘 담겼는지 확인
        log.info(form.toString());

        // 📝 2. DTO → 엔티티 변환
        Article article = form.toEntity();
        log.info(article.toString());

        // 📝 3. DB에 엔티티 저장
        Article saved = articleRepository.save(article);
        log.info(saved.toString());

        return "";
    }
}

```

---

## 🎯 정리

- `println()` 대신 `log.info()` 사용하면 **데이터를 기록하고 나중에도 확인 가능**
- `@Slf4j` 어노테이션을 추가하면 `log.info()` 사용 가능
- 로그는 **디버깅, 에러 분석, 성능 모니터링** 등에 유용하게 활용됨

이제 서버에서 무슨 일이 일어났는지 **블랙박스처럼 기록하고 확인할 수 있음!** 🚀

## 마무리 
1. 롬복 → 코드를 간소화해 주는 라이브러리. 롬복을 사용하면 여러 필수 코드가 반복되는 것을 최소화할 수 있고 println() 문을 로깅 기능으로 대체할 수 있다
2. 로깅 → 프로그램의 수행 과정을 기록으로 남기는 것. 일종의 자동차 블랙박스와 같다
3. 리팩터링 → 코드 기능 변함없이 구조 또는 성능을 개선하는 작업. 장점은 가독성이 좋아지고 개발 시간단축됨
4. @AllArgsConstructor → 클래스 안쪽의 모든 필드를 매개변수로 하는 생성자를 만드는 어노테이션. 이를 사용하면 클래스 내의 별도의 생성자를 만들지 않아도 된다 
5. @ToString → toString() 메서드를 사용하는 것과 동일. 별도의 toString() 메서드를 사용하지 않아도 됨
6. @Slf4j → Simple Logging Facade for java의 약자로 로깅할때 사용됨. 로깅 기능으로 로그를 찍으면 나중에라도 그동안 찍힌 로그를 찾아볼 수 있다. 로그를 찍을 때는 log.info() 문을 사용함

---


<br>
<br>
<br>


* ### 뷰 페이지에서 머스테치 문법인 이중중괄호를 이용해 출력한다 {{}}
    * `#`으로 열고 `/`를 이용해 닫는다 HTML의 시작태그와 종료태그처럼!

```
        {{#article}}
        <tr>
            <th>{{id}}</th>
            <td>{{title}}</td>
            <td>{{content}}</td>
        </tr>
        {{/article}}
```

* ### 기본생성자
    *  기본 생성자란 생성자인데 매개변수가 아무것도 없는 생성자를 말함 
        > 기본 생성자 역시 롬복으로 간단하게 줄일 수 있음 `@NoArgsConstructor`
```
    @NoArgsConstructor <!--기본 생성자 추가 어노테이션-->
    @ToString
    @AllArgsConstructor
    @Entity
    public class Article {

        // 기본 생성자 
        <!-- Article(){
            
        } -->    
    }
    
```

* ### 데이터 조회 요청 접수
    * 1. @PathVariable -> URL 요청으로 들어온 전달값을 컨트롤러의 매개변수로 가져오는 어노테이션
    * 2. 매개변수로 id 받아오기 */

```
/*
    @GetMapping("/articles/{id}")
    public String show(@PathVariable Long id, Model model){
        log.info("id :"+ id);


        <!-- 리파지터리에서 DB에 저장된 데이터를 id로 조회할 때 findById() 메서드를 사용한다. id 값이 없으면 null 반환되도록 -> orElse(null) 메서드 -->
        Article articleEntity = articleRepository.findById(id).orElse(null);


        <!-- 모델에 데이터 등록하기 (id로 DB에서 조회한 데이터는 article 이라는 이름으로 articleEntity 등록) -->
        model.addAttribute("article", articleEntity);


        return "articles/show";
    }
```

---

<br>
<br>
<br>
<br>

#### findAll() 메서드가 반환하는 데이터 타입은 Iterable인데 작성한 타입은 List다.
#### 불일치 하기 떄문에 오류가 발생해서 `Iterable<Article>` -> `List<Article>` 로 다운 캐스팅 해야 된다.
```
List<Article> articleEntityList = articleRepository.findAll(); 

```

> 캐스팅(casting) 이란 데이터 타입을 변환하는 것을 말하며 형변환이라고도 한다. 
넓은 범위를 업캐스팅(upcasting) 좁은 범위를 다운캐스팅(downcasting)이라 한다

> 오버라이딩(Overriding) 이란 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용하는 것을 말한다.

<br>

해결 방법 [1] Iterable 을 List로 다운캐스팅 하기.
```
List<Article> articleEntityList = (List<Article>) articleRepository.findAll(); 
```


해결 방법 [2] List를 Iterable로 업캐스팅 하기.
```
Iterable<Article> articleEntityList = articleRepository.findAll(); 
```

해결 방법 [3] Iterable 이 아닌 ArrayList 타입을 반환하도록 수정하기.
> repository > ArticleRepository 열고 블록 공간안에 마우스 오른쪽 클릭 -> Generate -> Override Methods 클릭 후 findAll():Iterable<T> 선택 하고 아래처럼 코드 수정 
```
public interface ArticleRepository extends CrudRepository <Article, Long>{
    @Override
    ArrayList<Article> findAll();
    //Iterable<Article> findAll(); 위 코드로 수정!
}
```

<br/>

## findAll()
findAll() 메서드는 JPA의 CrudRepository가 기본적으로 제공하는 메서드 중 하나로, 해당 엔티티를 `*모두*` 가져와 Iterable<T> 타입으로 반환한다.