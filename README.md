## 🛠️ Expert Spring Project

> ### 👨‍🏫 프로젝트 소개

#### 이 프로젝트는 Spring Boot 기반의 기존 애플리케이션에서 발생한 오류를 분석하고, 인증 처리 구조, 코드 품질, Validation, JPA 조회 성능, 테스트 코드를 개선한 과제 프로젝트이다.

#### 단순 기능 구현보다는 기존 코드의 문제점을 파악하고, 더 안정적이고 유지보수하기 쉬운 구조로 리팩토링하는 데 중점을 두었다.

#### 주요 개선 사항으로는 프로젝트 실행 오류 해결, ArgumentResolver 복구, Early Return 적용, DTO Validation 분리, `@EntityGraph`를 활용한 N+1 문제 개선, 실패 테스트 코드 수정이 있다.

---

> ### 📐 과제 진행 내용

#### Lv 0. 프로젝트 세팅 - 에러 분석
- 프로젝트 실행 시 발생한 `Application run failed` 에러를 분석했다.
- 에러 로그를 기준으로 원인을 추적하고, 애플리케이션이 정상 실행될 수 있도록 수정했다.
- Spring Boot 실행 오류는 단순히 마지막 에러 메시지만 보는 것이 아니라, `Caused by` 흐름을 따라 실제 원인을 확인해야 한다는 점을 학습했다.
- 에러 분석 및 해결 과정은 트러블 슈팅에 링크 첨부
---

#### Lv 1. ArgumentResolver 복구
- 삭제되어 정상 동작하지 않던 `AuthUserArgumentResolver` 로직을 복구했다.
- `@Auth AuthUser` 형태로 컨트롤러에서 인증 사용자 정보를 받을 수 있도록 수정했다.
- `supportsParameter()`와 `resolveArgument()`의 역할을 다시 정리하며 ArgumentResolver의 동작 흐름을 학습했다.

---

#### Lv 2. 코드 개선

##### 1. Early Return 적용
- 회원가입 로직에서 이메일 중복 여부를 먼저 확인하도록 코드 순서를 개선했다.
- 이미 존재하는 이메일인 경우 불필요하게 비밀번호 암호화가 실행되지 않도록 수정했다.

##### 2. 불필요한 if-else 제거
- `WeatherClient`의 중첩된 `if-else` 구조를 제거했다.
- 예외 상황을 먼저 처리하고 정상 흐름을 아래로 이어지게 하여 코드 가독성을 개선했다.

##### 3. Validation 책임 분리
- 비밀번호 검증 로직을 Service 계층에서 Request DTO로 이동했다.
- `spring-boot-starter-validation`을 활용하여 요청값 검증 책임을 DTO에서 처리하도록 개선했다.
- Service는 비즈니스 로직에 더 집중할 수 있도록 구조를 정리했다.

---

#### Lv 3. N+1 문제 개선
- Todo 목록 조회 시 연관된 User 데이터를 조회하는 과정에서 N+1 문제가 발생할 수 있는 구조를 확인했다.
- 기존 JPQL `fetch join` 기반 조회 방식을 `@EntityGraph` 기반으로 변경했다.
- 연관 엔티티 조회 전략을 선언적으로 지정하는 방식에 대해 학습했다.

---

#### Lv 4. 테스트 코드 수정
- 실패하던 테스트 코드들을 실제 서비스 로직과 일치하도록 수정했다.
- BCrypt 비밀번호 검증 테스트는 단순 문자열 비교가 아니라 `matches()`를 사용하도록 수정했다.
- 예외 테스트에서는 실제 발생하는 예외 타입과 메시지에 맞게 테스트 코드를 수정했다.
- 테스트 메서드명도 검증 내용과 일치하도록 정리했다.

---

> ### 📌 주요 개선 사항

#### 1. 실행 오류 해결
- 애플리케이션 실행 실패 원인 분석
- Spring Boot 설정 및 코드 오류 수정

#### 2. 인증 사용자 주입 구조 개선
- `AuthUserArgumentResolver` 복구
- 컨트롤러에서 인증 사용자 정보를 간결하게 사용할 수 있도록 개선

#### 3. 코드 가독성 개선
- Early Return 적용
- 불필요한 `else` 제거
- 예외 흐름과 정상 흐름 분리

#### 4. Validation 구조 개선
- Service 내부 검증 로직을 DTO Validation으로 분리
- 요청 데이터 검증 책임 명확화

#### 5. JPA 조회 성능 개선
- N+1 문제 발생 가능 지점 확인
- `@EntityGraph`를 활용한 연관 엔티티 조회 개선

#### 6. 테스트 코드 정비
- 실패 테스트 수정
- 예외 타입 및 메시지 검증 보완
- 테스트 메서드명과 검증 내용 일치

---

> ### ⏲️ 개발기간

- 2026.05.09 ~ 2026.05.10

---

> ### 📚️ 기술스택

#### ✔️ Language
- Java 17

#### ✔️ Framework
- Spring Boot
- Spring Web
- Spring Data JPA

#### ✔️ Database
- MySQL

#### ✔️ Library
- Lombok
- Spring Boot Validation

#### ✔️ Test
- JUnit 5
- Mockito

#### ✔️ IDE
- IntelliJ IDEA

#### ✔️ Version Control
- Git
- GitHub

---

> ### 🔥 Trouble Shooting

#### 1. 프로젝트 실행 실패 문제

#### 문제
프로젝트 실행 시 `Application run failed`가 발생하여 애플리케이션이 정상적으로 실행되지 않았다.

#### 원인
에러 로그를 확인한 결과, 일부 설정 또는 코드 누락으로 인해 Spring ApplicationContext가 정상적으로 생성되지 못하고 있었다.

#### 해결
에러 로그의 `Caused by`를 기준으로 실제 원인을 추적하고, 실행에 필요한 설정과 코드를 수정하여 애플리케이션이 정상 실행되도록 개선했다.

#### 느낀 점
Spring Boot 실행 오류는 겉으로 보이는 메시지만 보고 판단하면 원인을 찾기 어렵다.  
앞으로는 로그의 흐름을 따라 실제 원인이 되는 부분을 먼저 확인하는 습관을 가져야겠다고 느꼈다.

👉 자세한 정리

https://velog.io/@gpekd5/Spring-%EC%8B%AC%ED%99%94-%EA%B3%BC%EC%A0%9C%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0-%EC%A0%95%EB%A6%AC

---

> ### 📘 개념 학습

#### 1. ArgumentResolver
`HandlerMethodArgumentResolver`는 컨트롤러 메서드의 특정 파라미터를 원하는 객체로 변환하여 주입해주는 기능이다.  
이번 과제에서는 인증 사용자 정보를 `@Auth AuthUser` 형태로 받을 수 있도록 구현했다.

#### 2. Early Return
조건에 맞지 않는 경우 먼저 예외를 던지거나 리턴하여 불필요한 로직 실행을 막는 방식이다.  
코드의 흐름을 단순하게 만들고 가독성을 높이는 데 도움이 된다.

#### 3. DTO Validation
요청값 검증을 Service가 아닌 DTO에서 처리하도록 분리하는 방식이다.  
이를 통해 Service는 비즈니스 로직에 집중할 수 있고, 검증 책임도 명확해진다.

#### 4. EntityGraph
`@EntityGraph`는 JPA에서 특정 연관 엔티티를 함께 조회하도록 지정하는 기능이다.  
N+1 문제를 개선할 때 사용할 수 있으며, JPQL fetch join보다 선언적인 방식으로 작성할 수 있다.

#### 5. 테스트 코드
테스트 코드는 실제 로직의 결과와 예외 흐름을 검증하는 역할을 한다.  
테스트 메서드명, given-when-then 구조, 기대 예외 타입이 실제 코드와 일치해야 한다.

---

> ### ✅ 회고

이번 과제는 새로운 기능을 추가하기보다는 기존 코드의 문제를 분석하고 개선하는 데 초점이 있었다.

실행 오류 분석, ArgumentResolver 복구, Validation 분리, N+1 문제 개선, 테스트 코드 수정을 진행하면서 Spring 애플리케이션의 흐름을 다시 정리할 수 있었다.

특히 코드를 단순히 동작하게 만드는 것뿐만 아니라, 책임을 분리하고 읽기 쉬운 구조로 개선하는 것이 중요하다는 점을 느꼈다.