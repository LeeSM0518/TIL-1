# 예제 코드 분석

<img src="https://user-images.githubusercontent.com/42791260/44824909-eedbc780-ac42-11e8-8dc2-c4b806b2b073.png" width="50%">

[![npm](https://img.shields.io/badge/version-2018.38-brightgreen.svg)]()

## 주문하기

###흐름

<img src="https://user-images.githubusercontent.com/42791260/45610511-1cc06900-ba97-11e8-8ed8-4b9a88321ad3.png" width="100%">



### OrderController

####사용 클래스

* **OrderRequest** in application
* **OrderProduct** in application
* BindingResult
* ModelMap
* User
* **OrderRequestValidator** in application
* **PlaceOrderService** in application
* **MemberRepository** in domain



#### 기능

* 사용자 요청에 대한 유효성 검사
  * OrderRequestValidator().validate(orderRequest, bindingResult);
* DB로 부터 주문자에 대한 정보를 불러와 사용자 요청 객체에 저장 -> 요청 객체 완성
  * orderRequest.setOrderer(createOrderer(user));
* 응용 계층으로 요청객체 전달하고 결과값으로 주문번호를 반환받음
  * OrderNo orderNo = placeOrderService.placeOrder(orderRequest)



#### 의문

* OrderRequest와 OrderProduct는 왜 응용 계층에 위치했는가
  * 도메인의 핵심모델이 아니기 때문에



### PlaceOrderService

####사용 클래스

* **OrderRequest** in application
* **List\<OrderLine>** in domain
* **OrderProduct** in application
* **Product** in domain
* **ProductRepository** in domain
* **OrderRepository** in domain
* **Order **in domain



####기능

* 요청 객체에 필요한 값이 모두 저장되어 있는지 확인
* 주문상품이 DB에 존재하는지 확인 후 주문 항목 리스트에 저장
* 새로운 주문 번호를 할당 받고 이를 이용하여 주문 객체를 생성
  * Order order = new Order(orderNo, orderRequest.getOrderer(), orderLines, orderRequest.getShippingInfo(), OrderState.PAYMENT_WAITING);
* 주문 객체를 DB에 저장
  * orderRepository.save(order);



#### 집고넘어가야할 사항

* 응용 계층은 사용자가 요청한 서비스를 도메인 객체만 이용하여 서비스를 구현
* 도메인 로직에 대한 구현이 존재하지 않아야함



## 주문 취소하기



<img src="https://user-images.githubusercontent.com/42791260/45616514-a6c5fd00-baaa-11e8-8efa-96054250f533.png" width="100%">