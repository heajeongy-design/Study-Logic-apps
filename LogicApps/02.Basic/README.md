
# 설정된 시간에 메일 보내기 (Recurrence + Send Email)
---
## [호스팅 옵션]

1. 사용량 – 다중 테넌트 : consumption  
: 빠르게 시작 가능, 사용량 기반 과금

2. 표준 – 워크풀로 서비스 계획 : standard  
: logic app 전용 런타임 처럼 운영하는 방식  
:앱 내 커넥터 + 스케일링 기능 포함된 단일 테넌트 런타임

3. 표준 – app service environment V3 (ASE v3)  
: 기업용 격리/전용 환경에서 앱을 돌리는 옵션/ 네트워크 격리, 보안, 대규모 엔터프라이즈 요구사항 있을 때 고려

4. 표준 – 하이브리드  
: 로컬/Kubernetes 기반 같은 하이브리드 실행 환경 쪽 옵션/ 멀티클라우드,온프레미스,로컬 처리 요구가 있는 경우


<img width="1892" height="761" alt="image" src="https://github.com/user-attachments/assets/86fa82e8-6c99-48d6-a62e-0d46ab4ce64b" />


---
## [기본 정보 입력]

- 리소스 그룹

   => Azure 리소스들을 묶는 폴더(관리 단위), 하나의 프로젝트 단위로 묶어서 관리
  
  => 이용 후 리소스 그룹째 정리 가능(비용/권한/관리 구분 가능)
  
- 인스턴스 정보(논리 앱 이름)
  
  => 현재 사용자가 만드는 Logic App 리소스 이름 (EX. 폴더 안에 들어갈 파일(앱) 이름)


<img width="706" height="799" alt="image" src="https://github.com/user-attachments/assets/53bf6f31-7cbd-4d0a-9fee-93743060fb13" />


---
## [리소스 생성]


<img width="1180" height="77" alt="image" src="https://github.com/user-attachments/assets/7b48c8a1-3830-4394-a441-8da51b5a11bc" />


---

# [Trigger 추가]

## 1.Recurrence
- Recurrence 선택  
: 보통 schedule 계열의 Recurrence 트리거를 선택

- 기본 설정 입력  
: Interval = 1 (초), Frequency = minute(월/주/일/시간/분/초)

<img width="1004" height="672" alt="image" src="https://github.com/user-attachments/assets/f809df5d-16bc-4818-89ae-30ab98e78b06" />


<img width="1130" height="404" alt="image" src="https://github.com/user-attachments/assets/8f66c1c9-df7f-4814-9058-ff6edb6dbca4" />



## 2.메일 보내기(v2)
- 작업 추가
  = Add an agent : 에이전트 관련 기능(별도 기능/미리보기 성격 포함 기능)
- 받는사람, 제목, 본문 작성
- 실행시간 추가 가능 (번개모양 / 동적 콘텐츠(fx) 중 선택)  
 > 동적콘텐츠 기입  
convertTimeZone(utcNow(),'UTC','Korea Standard Time','yyyy-MM-dd HH:mm:ss')


<img width="283" height="146" alt="image" src="https://github.com/user-attachments/assets/5c0ba40d-2549-41eb-8df3-d85ad14ccc32" />


<img width="550" height="432" alt="image" src="https://github.com/user-attachments/assets/a16a5874-1169-426c-bb55-21c376f9e37f" />


<img width="1011" height="406" alt="image" src="https://github.com/user-attachments/assets/bb931ad3-6b06-4c02-b063-95ab3f006aac" />

## 3. Save

<img width="637" height="356" alt="image" src="https://github.com/user-attachments/assets/c91c7928-6940-43a5-9570-5271e9cb88f0" />

## 4. Test
> 수동 실행/트리거 (Run)

<img width="621" height="305" alt="image" src="https://github.com/user-attachments/assets/92ca9239-bb12-4006-972d-0c29174442d4" />








