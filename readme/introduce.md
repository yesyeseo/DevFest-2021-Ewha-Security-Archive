
---

SQL 삽입

SQL 삽입 공격

크로스 사이드 스크립트

Xquery 삽입

사용자 중요 정보 평문 저장

패스워드 평문 저장

---

## `오류 메시지`를 통한 정보 도출 방지

**과도하게 많은 정보**나 민감한 정보를 포함하는 **에러 메시지를 출력**하면, **공격자가 이를 악용**할 수 있기 때문에 보안 취약점이 발생할 수 있습니다. [🚀 Learn More](./error_messgae/readme.md)


|JAVA|C|
|:---:|:---:|
| [📖](./error_message/javaexposure.md) | [📖](./error_message/cexposure.md) |
| [스택 트레이스 출력 취약점](./error_message/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | [환경 변수 정보 출력 취약점](./error_message/cexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) |
| [예외 내용 출력 취약점](./error_message/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | [발생 위치 정보 출력 취약점](./error_message/cexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) |
| [에러 페이지 redirect 취약점](./error_message/javaexposure.md#-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%A0%95%EB%B3%B4-%EC%B6%9C%EB%A0%A5--%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AC%B8%EC%A0%9C-%ED%8C%8C%EC%9D%BC-%EB%85%B8%EC%B6%9C-%EA%B0%80%EB%8A%A5) | |

---

## 보안 속성 미적용으로 인한 쿠키 노출