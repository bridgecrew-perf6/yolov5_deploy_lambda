# yolov5-lambda

커스텀 학습한 yolov5모델을 도커로 컨테이너화 하여<\n>
AWS ECR에 푸시후
lambda 와 api gateway를 통하여 
배포까지 하는 스타팅 작업



# 1. 현재 리포지토리 다운로드
!git clone https://github.com/wkdoekofekfoekf/yolov5_depoly_lambda.git

# 2.커스텀 모델 변경 및 실행

![image](https://user-images.githubusercontent.com/62790857/171796213-294fe880-f912-491b-ae86-916092410a28.png)
yolov5/tests 폴더에 자신이 학습한 yolov5 pt파일로 변경



# 3. app.py 파일 수정 
![image](https://user-images.githubusercontent.com/62790857/171796423-012201ee-c2b7-46b1-879e-1d565b04ea0c.png)



자신이 예측하고 싶은 사진을 data 폴더에 넣고 
app.py의 코드 이미지 디렉토리 변경.


# 3. 쉘 창에서 python app.py 실행
로컬 cmd에서 실행함.

# 4. 실행 확인 후 yolov5 flask+aws.ipynb 실행, 주피터 에서 진행
쉘은 종료하지 않고 아래에 aws cli때 사용
노트북 실행
# 5. configure 템플릿 파일 변경

!move conf.json.template conf.json을 사용하여 템플릿 파일 conf.json으로 변경 그 뒤 셀창의 aws configure list를 이용하여 conf.json의 프로파일 명 : 현재 사용하는 이름으로 변경

![image](https://user-images.githubusercontent.com/62790857/171797819-0a0329b9-c40d-4cbb-8f0c-5a7e7ab766dc.png)


# 6. 노트북 스텝을 따라간 뒤 추론 부분에서 제대로 작업이 되는지 확인후 AWS 콘솔로이동
## 참고 : 노트북 스텝중 추론 부분에서 이미지 파일을 바이너리 형식으로 읽어오는 부분이 있음. 이 부분을 출력하여 나오는 이진 형식을 복사 해두면 편함.

# 7.aws lambda
## 노트북에서 생성한 lambda 함수 테스트 
![image](https://user-images.githubusercontent.com/62790857/171799081-303ac9fd-ba6c-4543-8229-a0b0fd2614bd.png)
템플릿을 위 사진과 같이 변경하고
밑줄 친 body부분을 아까 이진 형식의 이미지 데이터 9/로 시작하는 값을 넣음.



# 8. api gateway

aws api gateway에서 REST API 새로 만들기.
이름 제공하는 것 말고는 다른 설정할 필요 X
## 리소스생성
![image](https://user-images.githubusercontent.com/62790857/171799706-bc138a5d-925e-439e-b44c-3f737ec3e5eb.png)
작업 버튼을 누른 뒤 리소스를 생성
리소스 이름 지정후 생성
## 메소드 생성
![image](https://user-images.githubusercontent.com/62790857/171799817-98d4ae3d-4273-4430-8a6c-4cbe5f9f2dde.png)
작업을 눌러 POST 생성

Lambda 프록시 통합 사용 체크 후 7번에서 작업한 lambda 함수의 이름을 기입
권한 추가도 ok


![image](https://user-images.githubusercontent.com/62790857/171800102-86327026-a69b-4859-8564-e9e2f9978956.png)
## 메소드 요청 탭의 HTTP 요청 헤더에 Content-Type 추가


![image](https://user-images.githubusercontent.com/62790857/171800200-39003f81-af94-4fc7-a078-1a927bba00aa.png)
## 화면 왼쪽 메뉴에 설정 클릭후 아래 부분에 이진 미디어 형식 위 사진과 같이 변경


## 테스트  

![image](https://user-images.githubusercontent.com/62790857/171800564-5673d060-2a24-40f8-9038-904a76f4fe1b.png)
테스트 클릭후 요청 본문에 아까 사용하였던 이진 형식의 데이터 기입

그리고 요청

## 여기까지 완료 하였으면, api 배포후 url을 사용할 수 있음.
!curl --data-binary @i.jpg 발행된 url/detect


출처:
[こちらの記事](https://zenn.dev/nakamura196/articles/db3162950c5b6a)
