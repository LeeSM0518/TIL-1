# 계층 별 역할 및 요구사항

<img src="https://user-images.githubusercontent.com/42791260/44824909-eedbc780-ac42-11e8-8dc2-c4b806b2b073.png" width="50%">

[![npm](https://img.shields.io/badge/version-2018.38-brightgreen.svg)]()

## 표현영역

* 사용자 요청에 알맞은 응용 서비스를 호출
* 사용자 요청을 응용 서비스가 요구하는 형식으로 변환 및 전달
  * 폼 데이터 -> 객체
* 응용 서비스가 반환한 실행결과를 사용자에 알맞은 형식으로 응답
  * 객체 -> HTML
  * 객체 -> JSON
* 사용자의 세션관리 -> 추가적인 공부가 필요
* 필수 값, 값의 형식, 범위 등을 검증해야함
  * 주문할 상품이 기입되어야 합니다.
  * 주문량은 1개 이상이어야합니다.
  * 입력 값이 없거나 띄어쓰기로만 되어있는 경우를 처리해야함
* 권한 검증 -> 추가적인 공부가 필요



## 응용영역

* 사용자 요청을 처리하기 위한 도메인 객체를 리포지터리로 부터 구하고 도메인 객체에게 실행을 위임
* 도메인 로직을 구현하면 안됨
* 하나의 클래스가 모든 응용 서비스를 제공하지 않고 클래스로 분류
* 꼭 필요한 상황이 아닌이상 인터페이스 사용하지 않기
  * 구현 클래스가 다수 존재하는 경우에는 사용될 수 있음
* 사용자 요청 값 전달을 위한 별도의 데이터 클래스를 사용할 수 도 있음
* 서비스 메서드의 파라미터와 리턴 타입으로 표현 영역의 구현 기술 사용하지 않기
  * HttpServletRequest, HttpSession 사용 x
* 이벤트 핸들러 등록
  * 핸들러 등록 코드 아래에 위치한 이벤트 생성 주체를 사용하는 코드에서 발생하는 이벤트를 처리하는 이벤트 핸들러라는 것을 예상 할 수 있음
* 데이터의 존재 유무와 같은 논리적 오류를 검증
  * 사용자가 구매 요청한 물품이 존재하지 않음