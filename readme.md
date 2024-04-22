# Azure Function HOL 가이드
- 문서명 : Azure Function HOL 가이드
- 버전 : 1.2
  
---

## 문서 이력 관리
문서 버전| 작성일      | 작성자 | 변경사항
--------| -----      | ------| -------
1.0     | 2024-03-28 | 김민서 | 초안작성
1.1     | 2024-04-17 | 김민서 | 1. 오타수정<br>2. HttpTrigger추가코드 삭제<br>3. Python QueueTrigger 스토리지 계정 생성 순서 변경<br>4. 목차 페이지 수정
1.2     | 2024-04-18 | 김민서 | Queue 데이터 인입 확인을 위한 http트리거 추가
1.3     | 2024-04-18 | 김민서 | 오타 수정

---

## 목차
- [LAB 0 – HOL 환경 설명]
    - [TASK 1.	HANDS-ON LAB 목표](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%200%20%E2%80%93%20HOL%20%ED%99%98%EA%B2%BD%20%EC%84%A4%EB%AA%85/TASK%201.HANDS-ON%20LAB%20%EB%AA%A9%ED%91%9C.md)
    - [TASK 2.	사전 준비사항](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%200%20%E2%80%93%20HOL%20%ED%99%98%EA%B2%BD%20%EC%84%A4%EB%AA%85/TASK%202.%EC%82%AC%EC%A0%84%20%EC%A4%80%EB%B9%84%EC%82%AC%ED%95%AD.md)
- [LAB 1 – VSCODE 로컬환경 구성]
    - [TASK 1.	VSCode 로컬환경 구성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%201%20%E2%80%93%20VSCODE%20%EB%A1%9C%EC%BB%AC%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%84%B1/TASK%201.VSCode%20%EB%A1%9C%EC%BB%AC%ED%99%98%EA%B2%BD%20%EA%B5%AC%EC%84%B1.md)
- [LAB 2 – JAVA FUNCTION 생성 및 실행]
    - [TASK 1.	HttpTrigger 생성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%202%20%E2%80%93%20JAVA%20FUNCTION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%201.HttpTrigger%20%EC%83%9D%EC%84%B1.md)
    - [TASK 2.	HttpTrigger 로컬환경 실행](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%202%20%E2%80%93%20JAVA%20FUNCTION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%202.httpTrigger%20%EB%A1%9C%EC%BB%AC%ED%99%98%EA%B2%BD%20%EC%8B%A4%ED%96%89.md)
    - [TASK 3.	BlobTrigger 추가](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%202%20%E2%80%93%20JAVA%20FUNCTION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%203.BlobTrigger%20%EC%B6%94%EA%B0%80.md)
    - [TASK 4.	스토리지 계정 리소스 생성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%202%20%E2%80%93%20JAVA%20FUNCTION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%204.%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80%20%EA%B3%84%EC%A0%95%20%EB%A6%AC%EC%86%8C%EC%8A%A4%20%EC%83%9D%EC%84%B1.md)
    - [TASK 5.	BlobTrigger 로컬환경 실행](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%202%20%E2%80%93%20JAVA%20FUNCTION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%205.BlobTrigger%20%EB%A1%9C%EC%BB%AC%ED%99%98%EA%B2%BD%20%EC%8B%A4%ED%96%89.md)
- [LAB 3 –JAVA FUNCTION 배포]
    - [TASK 1.	HttpTrigger, BlobTrigger 코드 수정](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%203%20%E2%80%93JAVA%20FUNCTION%20%EB%B0%B0%ED%8F%AC/TASK%201.HttpTrigger%2C%20BlobTrigger%20%EC%BD%94%EB%93%9C%20%EC%88%98%EC%A0%95.md)
    - [TASK 2.	BlobTrigger 이미지 리사이징 테스트](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%203%20%E2%80%93JAVA%20FUNCTION%20%EB%B0%B0%ED%8F%AC/TASK%202.BlobTrigger%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95%20%ED%85%8C%EC%8A%A4%ED%8A%B8.md)
    - [TASK 3.	HttpTrigger, BlobTrigger 배포](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%203%20%E2%80%93JAVA%20FUNCTION%20%EB%B0%B0%ED%8F%AC/TASK%203.HttpTrigger%2C%20BlobTrigger%20%EB%B0%B0%ED%8F%AC.md)
    - [TASK 4.	Azure Portal BlobTrigger 테스트](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%203%20%E2%80%93JAVA%20FUNCTION%20%EB%B0%B0%ED%8F%AC/TASK%204.Azure%20Portal%20BlobTrigger%20%ED%85%8C%EC%8A%A4%ED%8A%B8.md)
- [LAB 4 – PYTHON FUNCION 생성 및 실행]
    - [TASK 1.	MySQL Database 생성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%201.MySQL%20Database%20%EC%83%9D%EC%84%B1.md)
    - [TASK 2.	QueueTrigger 생성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%202.QueueTrigger%20%EC%83%9D%EC%84%B1.md)
    - [TASK 3.	QueueTrigger 로컬환경 실행](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%203.QueueTrigger%20%EB%A1%9C%EC%BB%AC%ED%99%98%EA%B2%BD%20%EC%8B%A4%ED%96%89.md)
    - [TASK 4.	데이터 인입 확인을 위한 http트리거 추가](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%204.%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%9D%B8%EC%9E%85%20%ED%99%95%EC%9D%B8%EC%9D%84%20%EC%9C%84%ED%95%9C%20http%ED%8A%B8%EB%A6%AC%EA%B1%B0%20%EC%B6%94%EA%B0%80.md)
    - [TASK 5.	코드 수정 및 테스트](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%205.%EC%BD%94%EB%93%9C%20%EC%88%98%EC%A0%95%20%EB%B0%8F%20%ED%85%8C%EC%8A%A4%ED%8A%B8.md)
    - [TASK 6.	QueueTrigger 테스트](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%204%20%E2%80%93%20PYTHON%20FUNCION%20%EC%83%9D%EC%84%B1%20%EB%B0%8F%20%EC%8B%A4%ED%96%89/TASK%206.QueueTrigger%20%ED%85%8C%EC%8A%A4%ED%8A%B8.md)
- [LAB 5 – PYTHON FUNCION 배포]
    - [TASK 1.	Azure Portal Function 생성](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%205%20%E2%80%93%20PYTHON%20FUNCION%20%EB%B0%B0%ED%8F%AC/TASK%201.Azure%20Portal%20Function%20%EC%83%9D%EC%84%B1.md)
    - [TASK 2.	Python QueueTrigger 배포 및 데이터 확인](https://github.com/IIBlackCode/Azure_Function_Hol/blob/master/Document/LAB%205%20%E2%80%93%20PYTHON%20FUNCION%20%EB%B0%B0%ED%8F%AC/TASK%202.Python%20QueueTrigger%20%EB%B0%B0%ED%8F%AC%20%EB%B0%8F%20%EB%8D%B0%EC%9D%B4%ED%84%B0%20%ED%99%95%EC%9D%B8.md)

