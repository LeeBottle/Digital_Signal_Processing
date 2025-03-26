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
-![Image](https://github.com/user-attachments/assets/a6ff16d7-2c1d-4dfd-b85a-505eee216f2e)  
-![Image](https://github.com/user-attachments/assets/d7ca9f7b-0d69-40b3-b824-29a6da0826bd)  
#### ·Overlap-add
-windowing과정으로 나누었던 Short Time Signal을 통합해줌  
　└Short Time Signal의 50%를 Overlap  
　└전체 앞과 끝에 손실 발생  
  
모든 단계를 끝낸 뒤 라즈베리파이(RaspberryPi)에 포팅하여 실행결과를 확인해본다.  

## 수행 결과
### 1)기초 작업
-음성 가져오기  
![Image](https://github.com/user-attachments/assets/c1df0cfb-226d-4e9e-82ac-a7ecc1325503)

-음성 재생

### 2)Windowing
-STFT방식을 이용  
![Image](https://github.com/user-attachments/assets/7a521e07-c4df-4008-a7e3-70d9b7be2831)

### 3)Wiener Filtering
-Wiener 필터링 적용  
![Image](https://github.com/user-attachments/assets/c4be474b-dbea-4170-a6f2-2c9ef9b93207)

### 4)Overlab-add
-ISFTF방식을 이용  

### 5)결과 확인
-음성 재생으로 확인  
-스펙트로그램 형태로 확인  
![Image](https://github.com/user-attachments/assets/c299f396-905e-4324-be8a-fe620c56507d)

-Octave 4.4.1를 사용하여 결과 확인  
-comp_snr  
![Image](https://github.com/user-attachments/assets/911f9200-3249-4e6b-b6df-4d7872020952)  
-comp_cep  
![Image](https://github.com/user-attachments/assets/39cb608f-02b4-413c-ad02-e38ca7ce0a20)  
　└comp_snr, comp_cep로 신호처리한 결과와 잡음섞인 원본 비교  
　　└원본: sp01.wav / 잡음처리 후: test_dt.wav  
　└SNR의 절댓값이 커질수록 잡음 제거가 잘 된 음성  
　└CEP의 절댓값이 커질수록 잡음 제거가 잘 된 음성  

## 기대효과 및 개선방향
필터링 과정을 통해 불필요한 잡음이 섞인 음성 파일에서 잡음을 제거하고 원하는 음성만을 출력할 수 있었다. 이를 통해 다양한 잡음이 섞인 음성에서도 필요한 정보만을 추출하여 사용할 수 있을 것으로 기대된다.  
또한 잡음의 크기별로 동일한 단계를 밟았을 때 다음과 같은 결과를 비교할수 있었다.  

#### 0dB
![Image](https://github.com/user-attachments/assets/0b74fb71-b208-4080-9701-4ac96b446ac9)  
![Image](https://github.com/user-attachments/assets/7546ccaf-3429-42ed-bffd-504d5f3f127f)  
![Image](https://github.com/user-attachments/assets/d97e97b8-e38c-4320-882e-be969e39b3b7)  
▼잡음 섞인 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/a86c3102-1a8e-4eec-9733-ca66e4783d0d)  
▼필터링 된 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/bec94f94-eff8-4f32-8ead-d691340c05ff)  

#### 5dB
![Image](https://github.com/user-attachments/assets/ccf364cb-eb66-4ac3-a21d-e46d74e287d6)  
![Image](https://github.com/user-attachments/assets/eb1c60c0-3e6c-4a04-b9ae-71bda9182901)  
![Image](https://github.com/user-attachments/assets/9f98616c-a656-4d25-ad72-49e523491217)  
▼잡음 섞인 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/65e780d4-4380-4ccd-997e-be03d5f8db8f)  
▼필터링 된 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/d8a08f63-80ff-4248-900b-5195ba74bbfe)  

#### 10dB
![Image](https://github.com/user-attachments/assets/ec65454e-15d3-4117-aa3c-29b17e9a1120)  
![Image](https://github.com/user-attachments/assets/c0bb2c4a-165f-4ca0-a722-eeca812a113b)  
![Image](https://github.com/user-attachments/assets/33855fd0-3510-446a-b5b8-8da507e80520)  
▼잡음 섞인 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/218aae9f-9db1-45ba-a981-c8047317babc)  
▼필터링 된 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/4e343baa-cd7b-4d34-ab25-536cca200af7)  

#### 15dB
![Image](https://github.com/user-attachments/assets/ed8f78d8-b47b-4742-a780-a20fbae58510)  
![Image](https://github.com/user-attachments/assets/00ca2d5a-db11-4f95-b4f2-9b643c1cc02a)  
![Image](https://github.com/user-attachments/assets/886cfc6b-7a67-46bf-bf90-b8c5f4b88af1)  
▼잡음 섞인 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/b2364b7f-f7b8-4c05-b431-6ba2c239b9cf)  
▼필터링 된 신호 스펙트럼  
![Image](https://github.com/user-attachments/assets/22331ad4-4d7f-47e3-8803-f9f334bf8b22)  

위 4가지 결과를 통해 잡음이 많이 들어간 음성일수록 필터의 효과가 뚜렷하게 나타나는 경향을 확인할 수 있었다.  
다만 Wiener Filter는 선형 필터로 불규칙한 잡음에 대해 결과를 내기 힘들며 기준점이 정확하지 않고 예상 기준점을 사용한다는 한계점이 뚜렷하게 드러났다. 또한 학부생의 한계상 100% 명확한 음성을 추출하지 못했고 잡음비가 조금 남았다. 이를 이겨내기 위해 Wiener Filter를 중첩해 여러번 사용함으로서 정확도를 올리는 방안도 생각해 보았다.  
![Image](https://github.com/user-attachments/assets/7fca85f7-bbef-4a14-8a61-b6c189e5c5b9)  


## 기타 사항
RaspberryPi의 활용 화면  
![Image](https://github.com/user-attachments/assets/0e07df8d-f1dd-44c5-a8e0-48cc56959086)  
Octave의 활용 화면  
![Image](https://github.com/user-attachments/assets/7a988051-e319-4d8b-97c3-f5c6860b00e0)  