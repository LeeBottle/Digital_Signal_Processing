# Digital_Signal_Processing
2022년도 2학기  디지털 신호 처리 프로젝트

## 과제의 개요 및 필요성
 음성 신호의 사용량은 각종 스마트기기의 서비스들과 연계되어 증가하고 있다. 대표적인 예로 KT에서는 전화통화를 이용한 24시간 비대면 서비스인 ‘AI통화비서’에 관련한 광고가 진행되기도 하였다. 이러한 서비스들은 주로 일상 소음이 존재하는 생활반경에서 이루어지므로 불필요한 잡음이 들어가는 상황이 산재해있다. 잡음이 섞이게 되면 데이터의 정확도가 떨어지고 신뢰도가 하락하게 되므로 학부생으로서 이러한 문제를 극복하고자 주제를 정하였다. 

 ## 과제 수행방법 및 과정
 음성 파일에 활용하는 언어는 스크립트 언어인 Python을 사용하며 개발은 Jupyter Notebook(anaconda3)를 이용한다. 음성 잡음을 제거하는 작업을 수행하기 위해 다음과 같은 단계를 사용하였다.  

#### ·Windowing
-해밍창을 이용해 windowing을 적용  
　└30m/s를 기준으로 적용  
#### ·Wiener Filtering  
　-고정 신호 및 잡음 스펙트럼과 추가 잡음을 가정하여 선형시불변 필터링을 통해 원하는 또는 목표 임의 프로세스의 추정치를 생성하는 데 사용되는 필터  
![Image](https://github.com/user-attachments/assets/a6ff16d7-2c1d-4dfd-b85a-505eee216f2e)  
![Image](https://github.com/user-attachments/assets/d7ca9f7b-0d69-40b3-b824-29a6da0826bd)  
#### ·Overlap-add
-windowing과정으로 나누었던 Short Time Signal을 통합해줌  
　└Short Time Signal의 50%를 Overlap  
　└전체 앞과 끝에 손실 발생  
  
모든 단계를 끝낸 뒤 라즈베리파이(RaspberryPi)에 포팅하여 실행결과를 확인해본다.  