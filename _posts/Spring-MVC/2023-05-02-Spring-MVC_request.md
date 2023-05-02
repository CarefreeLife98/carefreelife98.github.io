---
title: "Spring-MVC (4) 요청(Request)"
categories:
  - Spring-MVC
tags:
  - Spring-MVC
toc: true
toc_sticky: true
toc_label: "Carefree to See"
---
<!-- Created by Chae Seungm Min - CarefreeLife
Visit my Programming blog: https://carefreelife98.github.io --> 
---

# @RequestMapping 다중 설정

```java
@RequestMapping({"/carefree/v1", "/carefree/v3"})
```

- @RequestMapping() 은 대부분의 속성을 배열[]로 제공한다. 
  - 따라서 위와 같이 기존 괄호() 안에 중괄호{}를 배치하여 중괄호{} 안에 , 로 분리된 서로 다른 여러 URL을 지정할 수 있다.
  - 그 결과로 <span style="color:green">서로 다른 URL에 요청이 오더라도 같은 메소드를 실행하여 같은 값(뷰 or String)을 반환할 수 있다.</span>

<br><br>

# HTTP 메서드

- `@RequestMapping`에 `method`속성으로 HTTP 메서드를 지정하여 각 HTTP 요청을 분류하여 호출 여부를 정할 수 있다.
  - method 속성의 지정이 없을 경우 모든 HTTP 요청을 허용, 메서드 호출.
  - ```java
    @RequestMapping(value = "/carefree", method = "RequestMethod.GET")
    // 'method = ' 에 특정된 HTTP 메서드 요청만 허용하여 호출됨.
    // GET, HEAD, POST, PUT, PATCH, DELETE 메서드가 있다. 
    ```
    
- 만약 특정된 메서드 외의 요청을 하면 MVC는 HTTP 405 (Method Not Allowed)를 반환한다.

<br><br>

# HTTP 메서드 매핑 간편하게 사용하기

- 위와 같이 특정 HTTP 메서드 마다의 호출 허용을 위해 @RequestMapping(value = , method = ) 
  를 일일히 작성해야 하는 문제의 해결책으로 HTTP 메서드를 축약한 애노테이션이 있다.
  - <span style="color:darkorange">@GetMapping
  - <span style="color:darkorange">@PostMapping
  - <span style="color:darkorange">@PutMapping
  - <span style="color:darkorange">@DeleteMapping
  - <span style="color:darkorange">@PatchMapping
- 이전보다 더 직관적인 코드가 생성되므로 축약 애노테이션을 사용하는 것이 좋다.
<br>
  
    ```java
    /**
    * 편리한 축약 애노테이션 
    * @GetMapping
    * @PostMapping
    * @PutMapping
    * @DeleteMapping
    * @PatchMapping
    */
    @GetMapping(value = "/carefree-v2")
    public String mappingGetV2() {
      log.info("carefree-v2");
      return "ok";
    }
    ```
<br><br>
- 위와 같은 HTTP 축약 메서드의 내부를 보면 @RequestMapping 과 해당 method 형태가 지정되어 있는 것을 볼 수 있다.
    - <img src="/assets/images/Spring/SpringMVC/getmapping.png" alt="getmapping_Procdess" width="100%" min-width="200px" itemprop="image"><br>`@GetMapping의 내부 모습`<br>

<br><br>

# PathVariable(경로 변수)?

- 최근 HTTP API는 다음과 같이 리소스 경로에 식별자를 넣는 스타일을 선호한다.
  - /carefree/user1
  - /members/2

<br><br>

- @RequestMapping은 @PathVariable(경로 변수)를 사용하여 URL 경로를 템플릿화 할 수 있다.

```java
@GetMapping("/carefree/{userId}") // URL 경로 + {경로 변수의 이름}
public String mappingPath(
        @PathVariable("userId") String data // PathVariable("경로 변수의 이름") + 파라미터 
        ) {
    log.info("mappingPath userId={}", data);
    return "ok";
}
```

<br><br>

- 만약 @PathVariable의 이름과 파라미터의 이름이 같으면 아래와 같이 생략이 가능하다.
```java
// "경로 변수의 이름" 과 파라미터의 이름이 같다.
public String mappingPath(@PathVariable("userId") String userId)
// -------------------생략---------------------
public String mappingPath(@PathVariable String userId)
```

<br><br>

# @PathVariable 다중 사용

- @PathVariable 의 다중 사용도 아래와 같이 가능하다.

```java

@GetMapping("/carefree/users/{userId}/orders/{orderId}")
public String mappingPath(
        // @PathVariable 애노테이션은 생략할 수 없다.
        @PathVariable String userId, 
        @PathVariable Long orderId
        ) {
    log.info("mappingPath userId={}, orderId={}", userId, orderId);
    return "ok";
}
```

<br><br>

# 특정 헤더 조건 매핑 

- HTTP 요청에 특정 헤더가 포함되어있는 경우 실행

```java
   /**
   *특정 헤더로 추가 매핑
   * headers="mode",
   * headers="!mode"
   * headers="mode=debug"
   * headers="mode!=debug" (! = )
   */
@GetMapping(value = "/mapping-header", headers = "mode=debug")
public String mappingHeader() {
    log.info("mappingHeader");
    return "ok";
}
```

<br><br>

# 미디어 타입 조건 매핑

- HTTP 요청의 Content-Type 헤더를 기반하여 미디어 타입으로 매핑.
  - 만약 같지 않을 경우 HTTP 415(Unsupported Media Type) 반환.

```java
/**
 * Content-Type 헤더 기반 추가 매핑 Media Type
 * 
 * * consumes="application/json"
 * consumes="!application/json"
 * consumes="application/*"
 * consumes="*\/*"
 * MediaType.APPLICATION_JSON_VALUE
 */
@PostMapping(value = "/mapping-consume", consumes = "application/json")
public String mappingConsumes() {
    log.info("mappingConsumes");
    return "ok";
}
```

<br><br>

- HTTP 요청의 Accept 헤더를 기반하여 미디어 타입으로 매핑.
  - 만약 같지 않을 경우 HTTP 406(Not Acceptable) 반환.

```java
/**
 * Accept 헤더 기반 추가 매핑 Media Type
 * 
 * produces = "text/html"
 * produces = "!text/html"
 * produces = "text/*"
 * produces = "*\/*"
 */
@PostMapping(value = "/mapping-produce", produces = "text/html")
public String mappingProduces(){
    log.info("mappingProduces");
    return"ok"
}
```





    
<!-- > <img src="/assets/images/Spring/SpringMVC/springmvcstruct.png" alt="_Procdess" width="100%" min-width="200px" itemprop="image"><br>``<br>
`참고:`[Inflearn - 김영한님_강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)<br><br>


`사진출처:`[]()
<span style="color:green">``</span>

```

```
> 
{: .notice--danger}
{: style="text-align: center;"}


<details>
<summary><h1><span style="color:blue">(클릭)</span></h1></summary>
<div markdown="1">       

</div>
</details> -->


<br><br>

최대한의 설명을 코드 블럭 내의 주석으로 달아 놓았습니다.<br><br>
혹시 이해가 안가거나 추가적인 설명이 필요한 부분, 오류 등의 피드백은 언제든지 환영합니다!<br><br>
긴 글 읽어주셔서 감사합니다. 포스팅을 마칩니다.<br>
{: .notice--success}
{: style="text-align: center;"}

<br><br>

[처음으로~](#){: .btn .btn--primary }

`참고:`[Inflearn - 김영한님_강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)<br><br>

### Task Lists
> 
- [x] @RequestMapping 다중 설정
- [x] HTTP 메서드
- [x] HTTP 메서드 매핑 간편하게 사용하기
- [x] PathVariable(경로 변수)?
- [x] @PathVariable 다중 사용
- [x] 특정 헤더 조건 매핑
- [x] 미디어 타입 조건 매핑