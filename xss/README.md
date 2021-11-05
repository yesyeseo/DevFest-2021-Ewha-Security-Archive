# 3. 보안 대책
## 👉 방법 1. 문자열 치환하기
외부 입력값에 스크립트가 삽입되지 못하도록 **문자열 치환 함수**를 사용한다.   
#### 📌 치환 전 : & < > " ' / ( )
#### 📌 치환 후 : `&amp;` `&lt;` `&gt;` `&quot;` `&#x27;` `&#x2F;` `&#x28;` `&#x29;`로 치환한다.

### 안전하지 않은 코드 예시 (Java)
외부 입력값에 대하여 검증 없이 화면에 출력될 경우 공격스크립트가 포함된 URL을 생성 할 수 있어 안전하지 않다.(Reflected XSS)
```java
<% String keyword = request.getParameter("keyword"); %>

검색어 : <%=keyword%>

```
### 안전한 코드 예시 (Java)
입력값에 대하여 스크립트 공격가능성이 있는 문자열을 치환한다.
```java
<% String keyword = request.getParameter("keyword"); %>

keyword = keyword.replaceAll("&", "&amp;");
keyword = keyword.replaceAll("<", "&lt;");
keyword = keyword.replaceAll(">", "&gt;");
keyword = keyword.replaceAll("￦"", "&quot;");
keyword = keyword.replaceAll("'", "&#x27;");
keyword = keyword.replaceAll("/"", "&#x2F;");
keyword = keyword.replaceAll("(", "&#x28;");
keyword = keyword.replaceAll(")", "&#x29;");
검색어 : <%=keyword%>

```
#### 예시 코드 더보기
<a href="/">Java 시큐어 코드</a>   
<a href="/">C 시큐어 코드</a>
   
## 👉 방법 2. 허용되는 HTML 태그들을 화이트리스트 필터링
사용자가 HTML 코드를 작성할 수 있도록 허용하게 되면 자바스크립트 역시 사용할 수 있게 되므로 XSS공격을 쉽게 할 수 있는 환경이 된다.

HTML코드에서 자바스크립트를 실행할 수 있는 방법은 수도 없이 많으므로 `<script>` 태그와 같은 지정된 특정 패턴을 걸러내는 블랙리스트 방식으로는 XSS를 막기가 어렵다.

HTML 태그를 허용하는 게시판에서는 **허용되는 HTML 태그**들을 **화이트리스트**로 만들어 해당 태그만 지원하도록 한다
### 💡 여기서 잠깐, 
#### 블랙리스트 필터링 VS 화이트리스트 필터링 이란?
입력검증을 위한 방법은 두 가지가 있다. 즉 화이트리스트(white-list)와 블랙리스트(black-list)를 이용하는 방법이다.    
- **블랙리스트 필터링**: 허용되지 않는 입력 값에 대한 리스트 
- **화이트리스트 필터링**: 허용 가능한 입력 값에 대한 리스트   

화이트리스트, 블랙리스트라는 용어 대신 'positive'와 'negative' 보안 방법으로 불려지기도 한다. 

## 👉 방법 3. 라이브러리 활용
JSTL 또는 잘 알려진 크로스 사이트 스크립트 방지 라이브러리를 활용한다. 
### 안전하지 않은 코드 예시 (Java)
외부 입력값에 대하여 검증 없이 브라우저에서 실행되는 경우 서버를 거치지 않는 공격스크립트가 포함된 URL을 생성 할 수 있어 안전하지 않다. (DOM 기반 XSS)
```java
<script type="text/javascript">
  document.write("keyword:" + <%=keyword%>);
</script>
```
### 안전한 코드 예시 (Java)
NAVER Lucy-XSS-Filter, OWASP ESAPI, OWASP Java-Encoder-Project 등의 XSS 방지 라이브러리를 사용한다.
```java
<script type="text/javascript">
  document.write("keyword:" +
  <%=Encoder.encodeForJS(Encoder.encodeForHTML(keyword))%>);
</script>
```
