# golf



# 강사조회 페이지

![image](https://user-images.githubusercontent.com/96267331/207213765-2119c09e-c655-45ce-9d34-764b284f63fd.png)<br>

  String sql = "select teacher_code, teacher_name, class_name, to_char(class_price, 'L999,999') class_price, substr(teach_resist_date,1,4) || '년' ||      substr(teach_resist_date,5,2) || '월' || substr(teach_resist_date,7,2)|| '일' teach_resist_date from tbl_teacher_202201";
	
	Connection conn = DBConnect.getConnection();
	PreparedStatement pstmt = conn.prepareStatement(sql);
	ResultSet rs = pstmt.executeQuery();
  
  
sql문을 통해 테이블의 값을 불러오는데 이중 to_char를 사용하여 숫자앞에 ￦표시를 넣어주고 소수점이 찍히게 한다 그리고 날짜 값을 조금씩 뽑아 "년", "월", "일"을 표시되게 하여 값을 가져왔다.<br>


![image](https://user-images.githubusercontent.com/96267331/207216439-73c8bd51-d407-43ab-8aed-13fbf1b793f6.png)<br>

while문의 rs.next()를 이용함으로써 마지막 줄까지 계속 반복하게 되며 이후 rs.getString(컬럼명 또는 줄숫자)이용하여 테이블의 값을 하나씩 만들고 넣어준다.


# 수강신청 페이지
![image](https://user-images.githubusercontent.com/96267331/207217006-9d6597e3-4580-4886-954a-8f8a84aba021.png)<br>
![image](https://user-images.githubusercontent.com/96267331/207218275-1dfb8028-3050-4104-87a7-330ccddfc310.png)<br>
![image](https://user-images.githubusercontent.com/96267331/207218318-a0816ebf-f0ef-4743-823d-c58d5c7169a6.png)<br>


### 유효성 검사

![image](https://user-images.githubusercontent.com/96267331/207217109-d682f767-50ce-493b-a506-55832e64edbb.png)<br>
메세지가 뜨면서 포커스가 빈칸으로 이동하게된다.<br>
![image](https://user-images.githubusercontent.com/96267331/207217373-7c9028b6-ede1-4ead-a4da-ecab3fd21a1f.png)<br>

### 회원명과 강의명

![image](https://user-images.githubusercontent.com/96267331/207217991-4b8b7968-ecc1-4dd1-b71e-663410494743.png)<br>
회원명의 이름을 다른걸로 바꾸었을때 회원번호도 그의 맞는 번호로 바뀌게 된다.<br>
![image](https://user-images.githubusercontent.com/96267331/207218167-f72b890a-14e9-4cb1-a987-fb712a25eed0.png)<br>
옵션의 있는 value값을 받아 그 값을 회원번호 value값에 넣어줌으로써 회원이름과 번호가 맞게 출력해준다 그리고 강의신청과 수강료를 초기화시켜준다.<br>
![image](https://user-images.githubusercontent.com/96267331/207218521-f3fe3e46-428a-4c3a-86c1-4f2f892d41e6.png)<br>
강의명은 강의를 신청할 반을 선택하는데 그의 맞는 수강료 값을 출력해준다 그중 회원 번호가 20000을 넘는 경우에는 메세지를 출력해주며 수강료를 50%할인 하여 출력을 해준다.<br>
![image](https://user-images.githubusercontent.com/96267331/207218792-6c937d39-900a-4abe-92ab-f05844a9c078.png)<br>
![image](https://user-images.githubusercontent.com/96267331/207218817-7275487d-219a-40ce-901d-c2024dcb0d36.png)<br>
![image](https://user-images.githubusercontent.com/96267331/207218866-288d0b6e-f391-47d0-a146-01752f70940c.png)<br>
코드를 보면 스위치 문을 이용하여 입력받은 value값의 맞는 값을 출력해주며 회원번호의 0번째(첫번재) 번호가 2인경우 수강료를 2나누어 출력하게 해준다.

# 수강신청 데이터를 넣는 페이지

![image](https://user-images.githubusercontent.com/96267331/207788252-99e76b31-29fa-4372-bc8b-63aacd8cc1bc.png)<br>
request.setCharacterEncoding를 UTF-8로하여 데이터값이 정상적인 언어로 바꾸어 넣어주도록 해주며 sql문의 insert문을 사용하여 DB테이블의값을 넣어 줄 수 있도록한다<br>
먼저 DB와 연결을 시킨후 테이블 컬럼 순서를 맞추어 준다 그리고 수강신청 페이지의 있는 name값을 컬럼명과 맞게 입력하여 데이터를 ?을 통해 넣어주며 업데이트를 시켜준다.<br>
![image](https://user-images.githubusercontent.com/96267331/207789817-4335f112-c02d-439b-8b6c-914ad2995dc1.png)<br>

# 회원정보조회 페이지

![image](https://user-images.githubusercontent.com/96267331/207789884-b5e944c7-7bda-4c8a-aede-0bf6d4daf21f.png)<br>
수강신청에서 입력한 데이터들이 테이블로 출력되는 페이지로 출력되는부분은 강사조회 페이지와 유사하지만 sql문의 많은 차이를 둔다.<br>
```sql
select substr(c.resist_month,1,4) || '년' || substr(c.resist_month,5,2) || '월' resist_month
, c.c_no, m.c_name, t.class_name, c.class_area, to_char(c.tuition, 'L999,999') tuition, m.grade
from tbl_class_202201 c, tbl_member_202201 m, TBL_TEACHER_202201 t
where c.c_no = m.c_no and c.teacher_code = t.teacher_code
```
이 sql문으로 테이블을 만드는데 이 sql문에서는 먼저 테이블별 명칭을 정해준다음 그 테이블의 기본키를 조인시켜주어야 한다. class테이블을 기본으로 하여 member테이블과 회원번호를 묶어주고 class테이블과 teacher테이블은 강사코드로 묶어준다. 그렇게 묶어준 테이블을 통하여 출력에 필요한값들을 조건에 맞게 데이터를 가져와 테이블로 출력시켜준다.

# 강사매출현황 페이지

```sql
select t.teacher_code, t.class_name, t.teacher_name, to_char(sum(c.tuition), 'L999,999') tuition 
from tbl_teacher_202201 t, tbl_class_202201 c 
where t.teacher_code = c.teacher_code group by t.teacher_code, t.class_name, t.teacher_name order by t.teacher_code asc
```
<br>
이 sql문은 teacher테이블과 class테이블을 사용하기 떄문에 두 테이블을 불러온 후 명칭을 만든다 그리고 강사코드를 이용하여 조인시켜준다.<br>
그리고 테이블의 불러올 강사코드, 강의명, 강사명 하니씩 불러오고 마지막 총 매출은 sum을 이용해 매출을 더해준후 ￦와 ,를 넣어준다.<br>
마지막으로 group by는 중복된 컬럼을 하나로 묶어주는것으로 총매출을 구하기위해서는 하나로 묶어줄 필요가 있기때문에 사용한다. 그리고 강사코드를 오름차순으로 정력하여 테이블의 출력하였다.<br>

![image](https://user-images.githubusercontent.com/96267331/208009951-bf52c309-26e0-4dde-925c-4291b63c3672.png)<br>

