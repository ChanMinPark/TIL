##Spring Framework에서 MyBatis를 이용해서 DB연동하기.
참고 : http://addio3305.tistory.com/62  

###1. 기존의 DB 연동 방법과 MyBatis를 이용한 DB 연동 방법
- 기존에 JDBC를 이용하는 방식은 SQL문을 Java 소스코드 상에 작성한다.  
  - (1) 커넥션을 맺고, (2) select문을 날려서, (3) resultset을 받고, (4) rs.next() 등을 이용해서 하나씩 받아온다.  
  - 이때, 문제점! SQL문 변경시에 프로그램 소스를 건드려야해서 유연성이 떨어진다.  
- MyBitis를 이용하면 SQL문을 xml파일에 작성한다.
  - 그래서 SQL의 변환이 자유롭고, 가독성이 좋다는 장점이 있다.
