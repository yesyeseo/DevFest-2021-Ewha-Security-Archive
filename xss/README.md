# 1. XSS(cross-site-scripting) 공격 개요

### 정의
XSS는 HTML 인젝션의 일종으로 웹페이지의 내용을 변경하거나 피해자의 웹브라우저에 임의의 자바 스크립트를 실행하는 공격이다.  공격자가 상대방의 브라우저에 Script를 실행할 수 있게 하여 사용자 Session을 가로채거나 웹 사이트 변조, 악의적 컨텐츠 삽입, 피싱 공격을 할 수 있다. 웹사이트에서 메일 주소, 사용자 ID, 블로그 댓글, 우편번호 등과 같은 사용자의 정보를 입력 받은 후 이를 다시 보여주는 과정에서 발생한다.

![image](https://user-images.githubusercontent.com/90726898/140513871-54b2be64-ff64-41e7-aa22-b593d08c41d9.png)

### <OWASP에서 발표한 웹 애플리케이션 보안 위협 목록>

XSS(cross-site-scripting)은 2021년도 기준으로 injection 카테고리에 합쳐져 3번째에 위치해 있다.

![image](https://user-images.githubusercontent.com/90726898/140456607-adcc00a5-5678-4ca1-b10a-8a7d3a2a8410.png) <br>
*OWASP(The Open Web Application Security Project) <br> 

# 2. XSS(cross-site-scripting) 공격 유형

### 1) 저장 XSS (Stored XSS)

**1-1) 정의**

웹 사이트의 게시판, 코멘트 필드, 사용자 프로필 등의 입력 form을 통해 악성 스크립트를 삽입하여 DB에 저장되면, 사용자가 사이트를 방문하여 저장되어 있는 페이지에 정보를 요청할 때, 서버는 악성 스크립트를 사용자에게 전달하여 사용자 브라우저에서 스크립트가 실행되면서 공격한다.

![image](https://user-images.githubusercontent.com/90726898/140505375-9c2afd13-c572-41fe-b7d0-43d9bda64e97.png) <br>

**1-2) 예시 공격 코드**
```html
<script>alert(document.cookie)</script>
```
이 코드가 포함되어 있는 어떤 페이지를 사용자가 읽을 때마다, 브라우저는 이 스크립트를 실행하면서 쿠키 값을 보여주게 된다.


### 2) 반사 XSS (Reflected XSS)

**2-1) 정의**

검색 결과, 에러 메시지 등을 통해 서버가 외부에서 입력 받은 악성 스크립트가 포함된 URL 파라미터 값을 사용자 브라우저에서 응답할 때 발생한다. 공격 스크립트가 삽입된 URL을 사용자가 쉽게 확인할 수 없도록 변형하여, 이메일, 메신저, 파일등을 통해 실행을 유도하는 공격이다.

![image](https://user-images.githubusercontent.com/90726898/140514026-f992023d-88c3-44a5-a6da-00e583ee0097.png)
 
**2-2) 예시 공격 코드**
XSS 공격용 URL : `http://www.server.com/search/?q=<script>alert(document.cookie)</script>&x=0&y=0`

```html
<html> <br>
 <body> <br>
  <div id="pageTitleTxt"> <br>
  <h2><span class="highlight">Search Results</span><br /> <br>
  Search: "<script>alert(document.cookie)</script>"</h2> <br>
 </body> <br>
</html> //서버가 반사한 HTML 데이터 , 사용자가 URL 링크를 열면 브라우저에서 이 스크립트의 내용이 실행된다. 
```

### 3) DOM기반 XSS

**3-1) 정의**

외부에서 입력 받은 악성 스크립트가 포함된 URL 파라미터 값이 서버를 거치지 않고, DOM 생성의 일부로 실행되면서 공격한다. Reflected XSS 및 Stored XSS 공격은 서버 애플리케이션 취약점으로 인해, 응답 페이지에 악성 스크립트가 포함되어 브라우저로 전달되면서 공격하는 것인 반면, DOM기반 XSS는 서버와 관계없이 발생하는 것이 차이점이다.  일반적으로 DOM 기반 XSS 취약점 있는 브라우저를 대상으로 조작된 URL을 이메일을 통해 사용자에게 전송하면, 피해자는 이 URL 링크를 클릭하는 순간 공격 피해를 입게 된다. 
 
 ![image](https://user-images.githubusercontent.com/90726898/140514222-4143991c-7bfc-44ed-8fe7-36680fec4784.png)

**3-2) 예시 공격 코드**
DOM 스크립트 (정상적으로 동작) 
```html
<HTML> <br>
 <TITLE>Welcome!</TITLE> <br>
 Hi <br>
 <script> <br>
  var pos=document.URL.indexOf("name=")+5; <br>
  document.write(document.URL.substring(pos,document.URL.length)); <br>
 </script> <br>
 <br>
 Welcome to our system <br>
 This demo borrowed from http://www.webappsec.org/projects/articles/071105.shtml <br>
</HTML>
```

DOM 기반 XSS 공격 URL, 사용자가 URL 링크를 열면 브라우저에서 이 스크립트의 내용이 실행된다.

`http://www.server.com/page.html?name=<script>alert(document.cookie)</script>` 

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
<a href="./JAVA">Java 시큐어 코드</a>   
<a href="./C">C 시큐어 코드</a>
   
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
- - - 
## References
<a href="https://scienceon.kisti.re.kr/srch/selectPORSrchArticle.do?cn=JAKO201306464554241&dbt=NART">XSS 공격과 대응방안, 디지털정책연구 = The Journal of digital policy & management v.11 no.12, 2013년, pp.327 – 332, 홍성혁 (백석대학교, 정보통신학부 정보보호 전공)</a><br>

<a href="https://scienceon.kisti.re.kr/srch/selectPORSrchArticle.do?cn=JAKO201509057414156&dbt=NART">크로스 사이트 스크립팅(XSS) 취약점에 대한 공격과 방어, 디지털융복합연구 = Journal of digital convergence v.13 no.2 , 2015년, pp.177 – 183, 최은정 (서울여자대학교 정보보호학과 )</a><br>

행정안전부, 전자정부 SW 개발·운영자를 위한 소프트웨어 개발보안 가이드, 2019. 11 <br>
