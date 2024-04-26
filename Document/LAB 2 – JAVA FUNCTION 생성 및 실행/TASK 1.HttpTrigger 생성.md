# HTTPTrigger
    HTTP 트리거는 외부에서 HTTP요청시 함수를 트리거하는 메커니즘으로 동작합니다.
    주요 특징으로 HTTP 메서드를 지원하기 때문에 다양한 유형의 요청에 대응이 가능하며 
    개발자 입장에서 서버 관리에 대한 부담 없이 신속하게 확장 가능한 
    웹 애플리케이션을 구축할 수 있습니다

# TASK 1.HttpTrigger 생성

1.	WORKSPACE에 있는 `Create Function` 아이콘을 클릭합니다.

![img](./img/task1/1.png)

2.	작업할 위치 디렉토리를 선택합니다

![img](./img/task1/2.png)

3.	Java를 선택합니다.

![img](./img/task1/3.png)

4.	설치된 JDK버전에 따라 Java 버전을 선택합니다.

![img](./img/task1/4.png)

5.	사용할 그룹 아이디를 지정합니다.(패키지명과 동일)
- com.function.<사용할 임의의 값 입력>

![img](./img/task1/5.png)

6.	사용할 Functions의 id를 입력합니다.

![img](./img/task1/6.png)

7.	스냅샷 파일명을 지정합니다.

![img](./img/task1/7.png)

8.	Java 패키지명을 지정합니다.

![img](./img/task1/8.png)

9.	Functions에서 사용할 App Name을 지정합니다.

![img](./img/task1/9.png)

10.	Maven을 선택합니다.

![img](./img/task1/10.png)

11.	Maven 빌드가 완료될 때까지 기다립니다.

![img](./img/task1/11.png)

12.	아래 이미지와 같이 Local Project가 생성되면 성공입니다.

![img](./img/task1/12.png)