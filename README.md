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

