
---

SQL 삽입

SQL 삽입 공격

크로스 사이드 스크립트

Xquery 삽입

---

## ✔️ 사용자 `중요 정보` `평문` 저장

데이터를 **암호화하지 않은 평문**으로 통신 채널을 통해 송수신할 경우, 인증받지 않은 사용자에 의해 발생한 **스니핑**을 통해 보안과 관련된 중요한 **데이터가 노출**될 수 있습니다. [🚀 Learn More](../plaintext/plaintext.md)

|JAVA|ANDROID Java|C|C#|
|:---:|:---:|:---:|:---:|
| [📖](../plaintext/plaintext.md#java-%EC%98%88%EC%A0%9C) | [📖](../plaintext/plaintext.md#android-java-%EC%98%88%EC%A0%9C) |  [📖](../plaintext/plaintext.md#c-%EC%98%88%EC%A0%9C) | [📖](../plaintext/plaintext.md#c-%EC%98%88%EC%A0%9C-1) |

---

## ✔️ `패스워드` `평문` 저장

패스워드를 비롯한 **중요 데이터**가 **암호화되지 않은 평문 텍스트**의 형태로 저장되면 암호가 *외부에 직접* 드러날 수 있어 **기밀성**이 보장되지 못하고 암호가 저장된 파일에 *접근할 수 있는 사람이면 누구*나 암호를 알아낼 수 있어 **무결성** 또한 보장되지 못합니다. [🚀 Learn More](../plaintext/password.md)

|JAVA|C|
|:---:|:---:|
| [📖](../plaintext/password.md#java-%EC%98%88%EC%A0%9C) | [📖](../../plaintext/password.md#c-%EC%98%88%EC%A0%9C) |
| 패스워드 정보 평문으로 DB 저장 취약점 | 패스워드를 파일에서 읽어 직접 DB 연결 취약점 |
| | 패스워드 입력 미검증 취약점 |

---

## ✔️ `오류 메시지`를 통한 정보 도출 방지

**과도하게 많은 정보**나 민감한 정보를 포함하는 **에러 메시지를 출력**하면, **공격자가 이를 악용**할 수 있기 때문에 보안 취약점이 발생할 수 있습니다. [🚀 Learn More](../errormsg/readme.md)


|JAVA|C|
|:---:|:---:|
| [📖](../errormsg/javaexposure.md) | [📖](../error_message/cexposure.md) |
| [스택 트레이스 출력 취약점](../errormsg/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | [환경 변수 정보 출력 취약점](../errormsg/cexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) |
| [예외 내용 출력 취약점](../errormsg/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | [발생 위치 정보 출력 취약점](../error_message/cexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) |
| [에러 페이지 redirect 취약점](../error_message/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | |

---

## ✔️ `쿠키`를 통한 `정보 노출`

개인 정보나 인증 정보 등이 **하드 디스크의 영속 쿠키**에 저장된다면 개인 **정보 유출** 등의 문제로 시스템이 취약해지는 문제가 발생합니다. [🚀 Learn More](../cookie/readme.md)

|JAVA|C|
|:---:|:---:|
| [📖](../cookie/javacookies.md) | |
| [쿠키 유효 기간 설정 시 사용자 미검증 취약점](../cookie/javacookies.md#-%EC%99%B8%EB%B6%80-%EC%9E%85%EB%A0%A5%EC%9D%B4-%EC%BF%A0%ED%82%A4-%EC%9C%A0%ED%9A%A8-%EA%B8%B0%EA%B0%84-%EC%84%A4%EC%A0%95%EC%97%90-%EA%B7%B8%EB%8C%80%EB%A1%9C-%EC%82%AC%EC%9A%A9%EB%90%A8) | |
| [쿠키 유효 기간 상숫값 설정 취약점](../cookie/javacookies.md#-%EC%BF%A0%ED%82%A4-%EC%9C%A0%ED%9A%A8-%EC%8B%9C%EA%B0%84-%EC%84%A4%EC%A0%95%EC%9D%B4-%EC%83%81%EC%88%AB%EA%B0%92%EC%9D%B4-%EB%90%A8) | |

