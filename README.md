# /24-08-18

## 프로젝트 생성하기

# /24-08-19

## 타임리프 소개

### 타임리프 특징
- 서버 사이드 HTML 렌더링 (SSR)
- 네츄럴 템플릿
- 스프링 통합 지원

#### 서버 사이드 HTML 렌더링 (SSR)
타임 리프는 백엔드 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용한다.

네츄럴 템플릿
타임리프는 순수 HTML을 최대한 유지하는 특징이 있다.
타임리프로 작성한 파일은 HTML을 유지하기 때문에 웹 브라우저에서 파일을 직접 열어도 내용을 확인할 수 있고,
서버를 통해 뷰 템플릿을 거치면 동적으로 변경된 결과를 확인할 수 있다.
JSP를 포함한 다른 뷰 템플릿은 해당 파일을 열면, 예를 들어서 JSP 파일 자체를 그대로 웹 브라우저에서 열어보면 JSP 소스코드와 
HTML이 뒤죽박죽 섞여서 웹 브라우저에서 정상적인 HTML 결과를 확인할 수 있다.
오직 서버를 통해서 JSP가 렌더링 되고 HTML 응답 결과를 받아야 화면을 확인할 수 있다.
반면에 타임리프로 작성된 파일은 해당 파일을 그대로 웹 브라우저에서 열어도 정상적인 HTML 결과를 확인할 수 있다.
물론 이 경우 동적으로 결과가 렌더링 되지는 않는다.
하지만 HTML 마크업 결과가 어떻게 되는지 파일만 열어도 바로 확인할 수 있다.
이렇게 순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있는 타임리프의 특징을 네츄럴 템플릿(natural templates)이라 한다.

#### 스프링 통합 지원
타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 지원한다.

# /24-09-12

## 텍스트 - text, utext

타임리프는 기본적으로 HTML 태그의 속성에 기능을 저의해서 동작한다.
HTML의 콘텐츠에 데이터를 출력할 때는 다음과 같이 th:text를 사용하면 된다.
<span th:text="${data}">

HTML 태그의 속성이 아니라 HTML 콘텐츠 영역안에서 직접 데이터를 출력하고 싶으면 다음과 같이 [[...]]를 사용하면 된다.
컨텐츠 안에서 직접 출력하기 = [[${data}]]

# /24-09-13

### Escape
HTML 문서는 '<', '>' 같은 특수 문자를 기반으로 정의된다.
따라서 뷰 템플릿으로 HTML 화면을 생성할 때는 출력하는 데이터에 이러한 특수 문자가 있는 것을 주의해서 사용해야 한다.

### HTML엔티티
웹 브라우저는 '<'를 HTML 태그의 시작으로 인식한다. 
따라서 '<'를 태그의 시작이 아니라 문자로 표현할 수 있는 방법이 필요한데, 이것을 HTML 엔티티라 한다.
그리고 이렇게 HTML에서 사용하는 특수 문자를 HTML 엔티티로 변경하는 것을 이스케이프(escape)라 한다.
그리고 타임리프가 제공하는 'th:text', '[[...]]' 는 기본적으로 이스케이프(escape)를 제공한다.

### Unescape
타임리프는 다음 두 기능을 제공한다. 
- th:text -> th:utext
- [[...]] -> [(...)]

### 주의
실제 서비스를 개발하다 보면 escape를 사용하지 않아서 HTML이 정상 렌더링 되지 않는 수 많은 문제가 발생한다.
escape를 기본으로 하고, 꼭 필요할 때만 unescape를 사용하자

# /24-09-15

## 변수 - SpringEL

타임리프에서 변수를 변수를 사용할 때는 변수 표현식을 사용한다.

### 변수 표현식 : ${...}

### 지역변수 선언
th:with 를 사용하면 지역 변수를 선언해서 사용할 수 있다. 
지역 변수는 선언한 태그 안에서만 사용할 수 있다.

# /24-09-16

## 기본 객체들

# /24-09-18

## 유틸리티 객체와 날짜
타임리프는 문자, 숫자, 날짜, URI등을 편리하게 다루는 다양한 유틸리티 객체들을 제공한다.

### 타임리프 유틸리티 객체들
- #message : 메시지, 국제화 처리
- #uris : URI 이스케이프 지원
- #dates : java.util.Date 서식 지원
- #calendars : java.util.Calendar 서식 지원
- #temporals : 자바8 날짜 서식 지원
- #numbers : 숫자 서식 지원
- #strings : 문자 관련 편의 기능
- #objects : 객체 관련 기능 제공
- #bools : boolean 관련 기능 제공
- #arrays : 배열 관련 기능 제공
- #lists, #sets, #maps : 컬렉션 관련 기능 제공
- #ids : 아이디 저리 관련 기능 제공

# /24-09-20

## URL링크

## 리터럴
리터럴은 소스 코드상에 고정된 값을 말하는 용어이다.
타임리프는 다음과 같은 리터럴이 있다.
- 문자
- 숫자
- 불린
- null

타임리프에서 문자 리터럴은 항상 ' (작은 따옴표)로 감싸야 한다.
ex) <span th:text="'hello'">
그런데 문자를 항상 ' 로 감싸는 것은 너무 귀찮은 일이다.
공백없이 쭉 이어진다면 하나의 의미있는 토큰으로 인지해서 다음과 같이 작은 따옴표를 생략할 수 있다.
<span th:text="hello">

### 오류
ex) <span th:text="hello world!"></span>
문자리터럴은 원칙상 ' 로 감싸야 한다 중간에 공백이 있어 하나의 의미있는 토큰으로 인식하지 않는다 
따라서 <span th:text="'hello world!'"></span> 이렇게 수정해 주어야 한다.

# /24-09-21

## 연산



