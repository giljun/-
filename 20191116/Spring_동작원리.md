# Spring_동작원리

1. Web.xml
   1. 서버를 돌리기 위해서, 가장 먼저 읽는다.
2. DispatcherServlet
   1. 사용자로부터 url을 통해 서비스를 요청받는다.
   2. HandlerMapping에게 Controller를 찾아달라고 요청한다.
3. HandlerMapping
   1. @RequestMapping을 통해, Controller명을 리턴
4. Controller
   1. 사용자로부터 받은 값을 주면, 비즈니스 로직을 수행하는 Service 요청
   2. 필요한 데이터를 DAO를 통해 DB에서 가지고 온다.
   3. Model을 생성
   4. 이에 맞는 뷰를 Model and View 객체로 넘겨준다.
5. ViewResolver
   1. 어떤 View를 선택할지 찾아달라고 한다.
6. View
   1. 모델을 넘겨준다.
   2. 보여준다.