# yolov5-lambda

커스텀 학습한 yolov5모델을 도커로 컨테이너화 하여<\n>
AWS ECR에 푸시후
lambda 와 api gateway를 통하여 
배포까지 하는 스타팅 작업



# 1. 현재 리포지토리 다운로드
!git clone https://github.com/wkdoekofekfoekf/yolov5_depoly_lambda.git

# 2.커스텀 모델 변경 및 실행
yolov5/tests 폴더에 자신이 학습한 yolov5 pt파일로 변경



![image](https://user-images.githubusercontent.com/62790857/171796213-294fe880-f912-491b-ae86-916092410a28.png)



# 3. app.py 파일 수정 
![image](https://user-images.githubusercontent.com/62790857/171796423-012201ee-c2b7-46b1-879e-1d565b04ea0c.png)
자신이 예측하고 싶은 사진을 data 폴더에 넣고 
app.py의 코드 이미지 디렉토리 변경.


# 3. 쉘 창에서 python app.py 실행


# 4. 실행 확인 후 yolov5 flask+aws.ipynb 실행, 주피터 에서 진행



# 5. configure 템플릿 파일 변경

!move conf.json.template conf.json을 사용하여 템플릿 파일 conf.json으로 변경
그 뒤 셀창의 aws configure list를 이용하여 
conf.json의 프로파일 명 : 현재 사용하는 이름으로 변경

![image](https://user-images.githubusercontent.com/62790857/171797819-0a0329b9-c40d-4cbb-8f0c-5a7e7ab766dc.png)


# 6. 주피터 노트북 스텝을 따라간 뒤 추론 부분에서 제대로 작업이 되는지 확인후 
AWS 콘솔로이동






출처:
[こちらの記事](https://zenn.dev/nakamura196/articles/db3162950c5b6a)
