# Logic Apps

## 개념
= 이벤트가 발생할 때 정해둔 작업을 자동으로 실행하는 클라우드 자동화 워크플로 엔진

### Ex.
- 파일 업로드 시 -> 이메일 보내기
- 매일 오전 9시 -> 리포트 메일 보내기
- HTTP 요청 시 -> DB 조회 후 메일 발송

= Microsoft 문서에서도 Logic Apps를 통해 이메일 알림, 파일 이동, 온프레미스/클라우드 시스템 연동 같은 통합 자동화 가능

---

## 용어정리

### 1. trigger : 워크플로의 시작점
Ex. Recurrence(주기실행), when a HTTP request is received (외부 시스템 호출), when a new email arrives, when a blob is added

### 2. action : 트리거 이후 실행되는 작업
Ex. 이메일 보내기. 데이터 조회하기, 조건 분기하기, teams 메시지 보내기

### 3. connector : 외부 서비스와 연결해주는 어댑터
Ex. Outlook, gmail, sharepoint, sql server, sal, azure blob storage  
Microsoft는 logic apps에 1,400개 이상 커넥터가 있다고 함

### 4. connection : 커넥터를 실제로 쓰려면 계정 인증필요
Ex. Outlook 커넥터 사용 시 회사 계정 로그인, gmail 커넥터 사용 시 google 로그인

### 5. workflow & run의 차이
- workflow = 본인이 설계한 자동화 “설계도”
- rum(실행 인스턴스) : 설계도가 실제 한번 실행된 결과

> 디버깅할 때 워크플로가 아니라 run history를 봐야함, 실패 원인도 각 run기준으로 확인

---

## 개발관점 : 백엔드 통합/자동화 워크플로 플랫폼
> API 호출 오케스트레이션(여러 API 순서대로 호출), 조건/반복 처리(if, switch, for each), 예외 처리/재시도, 로그실행 이력 확인, 외부 시스템 통합, 알림/승인 프로세스 자동화

---

## 데이터 흐름 개념 (입력>출력>다음단계 입력)
- 트리거가 데이터를 전달받음 > 액션이 처리해서 결과를 만듦 > 다음 액션이 그 출력을 다시 입력으로 씀
- 단순 자동화가 아니라 데이터를 흘려보내는 파이프라인형 워크플로

---

## control flow 개념
- condition : if/else
- switch : 값에 따라 여러 분기
- for each : 배열/목록 반복
- until : 조건 만족할 때까지 반복
- scope : 액션 묶음(논리적 그룹)

---

## 커넥터 종류 개념 (built-in vs managed)
- built-in(기본제공)과 managed(관리형) 관점으로 이해필요

### Built-in
- 스케줄/구조제어/데이터 조작 같은 워크플로 기본 동작에도 많이 쓰임
- (recurrence, request)

### built-in connector
- logic apps 런타임에 가까운 기본 기능(recurrence(스케줄), request(http요청))

### managed connector
- outlook, gmail, sql, sharepoint같은 외부 서비스 연결용

---

## connection(연결) 과 authentication(인증) 개념
- connector = 기능(예: outlook 메일 보내기)
- connection = 그 기능을 쓰기 위한 실제 인증 연결(계정 로그인, 권한 부여)

> connector를 수행 후 connection 생성/인증이 되어야 실제 실행  
> 실행 실패 원인이 인증/권한 일 수 있음, 환경(dav/test/prod)마다 연결을 따로 관리할 수 있음

---

## expression(표현식) 과 dynamic contect(동적 콘텐츠)
- dynamic content : 이전 단계 결과를 클릭해서 넣는 방식
- expression : 함수/식으로 값 가공하는 방식

---

## 상태 저장(stateful) 관점과 실행 추적 개념
: 실행 이력 추적이 잘 된다는 강점이 있음(어떤 단계가 어떤 입력/출력으로 실패했는지 확인 가능)

---

## error handling 과 retry
- 액션 실패 가능성은 항상 있음(권한, 네트워크, 타임아웃 등)
- logic apps는 재시도 정책(retry policy)개념이 있음
- 실패했을 때 분기 처리(예:실패 메일 보내기) 기능

> 자동화는 성공 로직만이 아니라 실패 시 동작(재시도/알림/종료)을 함께 설계해야함

---

## standard vs consumption 개념
- consumption : 멀티테넌트, 1개 logic app 리소스에 1개 워크플로(빠른시작, 사용량 기반사고)
- standard : 싱글테넌트 기반, 하나의 logic app 리소스에 여러 워크플로 가능(구조적 운영/배포/다중 워크플로 관리에 유리)

---

## 설계 단위 개념 : “트리거 중심 설계” vs “업무 시나리오 중심 설계”
- 업무 시나리오 선 정의 > 트리거 > 처리 > 조건 > 알림으로 쪼개기
- ex. 어떤 이벤트가 시작점인가? 어떤 데이터를 확인해야하는가?, 어떤 조건에서 알림을 보낼까?, 실패하면 어떻게 처리할까?, 중복 발송은 막아야 하나?

---

## 모니터링/운영 관점 개념 (개발과 별개로 꼭 필요)
: 실행 이력 확인, 실패율/성공률 모니터링, 알림 기준 정의, 재실행 필요 여부 판단, 운영 로그 확인

---

## 보안
: 연결 정보(계정/권한)관리, 입력/출력 데이터 노출 주의, 필요한 최소 권한으로 연결 구성, 필요 시 접근 제한(IP 등)고려

---

# 개념 정리

- **Logic Apps**는 이벤트를 기준으로 자동 실행되는 **클라우드 워크플로 엔진**
- 핵심 구성요소는 **Trigger(시작)**, **Action(처리)**, **Connector(외부 연동)**, **Connection(인증 연결)**
- 워크플로는 단순 작업 자동화가 아니라 **데이터가 흐르는 파이프라인형 구조**
- 조건/반복/분기(**control flow**)를 통해 실제 업무 시나리오를 자동화 가능
- 운영 시에는 개발만큼 **run history, 모니터링, 실패 처리, 재시도 정책**이 중요
- 인증/권한/연결 정보 관리 등 **보안 관점**까지 함께 설계해야 안정적으로 운영 가능
- 배포/운영 구조 측면에서 **Consumption vs Standard** 차이를 이해하고 선택해야 함
