| 현대오토에버 모빌리티 임베디드 SW스쿨 과정 |
| ------------------------------------------ |
| **프로젝트 계획서**                        |

| 팀이름                 | FourEver                                                     |
| ---------------------- | ------------------------------------------------------------ |
| 구성원                 | 조장 : 유혜림조원 : 김종욱, 양원필, 여동훈, 이대경, 한상준박스번호없음/NGV18, 박스번호없음/NGV20 |
| 프로젝트 주제          | CAN 통신 기반 엠비언트 라이트 적용 ADAS 시스템               |
| 프로젝트 목표          | 운전자 편의를 위한 Adaptive Cruise Control과 Automated emergency braking system을 시각적 보조(엠비언트 라이트)를 포함하여 구현 |
| 기술스택               | CANoe : 통신 분석, 시뮬레이션, 패널 구현CAPL, Matlab/Simulink : ECU 통신 로직 및 알고리즘 구현 |
| 서비스흐름도(아키텍처) | **1. ECU 아키텍쳐**![img](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4mcc6i72o2LTTl8WlsGS-UBwAKILJ8IzZ15iocYEm3TazcRmq35cG20lcAtGBOAarCym40iWWuisTzYlO-So6ZSHa1tLIIy7vJ0YEfas6dSp7DJTsi_x5cwAlMuq14lZR28eUbVYSJ0qQnYw75_Y?key=dLHJVWuJEtjflCD0eJpR-V3k) 1)VCU ECU: 엔진                  <br />2)AML ECU: 엠비언트 라이트      <br />3)CLU ECU: 클러스터               <br />4)BCU ECU: 바디 유닛 제어(안전벨트, 좌석, 에어벡)   <br />5)CCM ECU: ACC CONTROL UNIT       <br />6)Pannel ECU: 시나리오 테스르를 위한 패널 조작     <br />**2. 서비스 흐름도**![img](https://lh7-rt.googleusercontent.com/docsz/AD_4nXef6gUr4yyVbkHytUOhl0tTiP8VjQbUPof0W7gHx0IpM7TqQ8QXUjUFW5d6GV1Nc4BKAuTtlt2rN68L_KM2CaaepdYpojvtgtwokFeHM-dOi1Kyvc4cD3-ikasFooGFAkaMPLEQAmxr1iae3FZ87A?key=dLHJVWuJEtjflCD0eJpR-V3k)****<br />1단계: 초기화 및 시스템 준비<br />**- 시동이 켜지면 ACC 및 엠비언트 라이트 시스템 초기화.- 센서가 외부 환경 및 차량 상태를 점검. <br />**2단계: ACC 모드 활성화<br />**- 사용자가 ACC를 활성화. 사용자는 원하는 ACC level을 1-3 중에서 설정 가능.![그림입니다. 원본 그림의 이름: CLP00000e980e31.bmp 원본 그림의 크기: 가로 713pixel, 세로 371pixel](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcz3g8vycfZlRw46jUz_VfpRG7moPPhSKn6fAxJbZmxGAGuAFHXn71XTHVc65Xhya23N0fhfOacZ1GZ6LBp9DkUeJX4UdZecPQVer_JerFNzwKmdQxmik_lKeWXVjDhrAuQnwyR5GtcF_ECKBGx_oE?key=dLHJVWuJEtjflCD0eJpR-V3k)- 일반제어/정지제어/오버라이드제어 모드 제공 **<br />3단계: 실시간 주행 제어<br />**- ACC: 차량 앞쪽의 레이더를 통해 차량 간 거리 및 속도 조정.- 엠비언트 라이트: 주행 중 조명 색상 및 밝기를 속도에 맞게 변경. **<br />4단계: 이벤트 처리<br />**- 비상 상황(급정지): ACC가 즉각 반응하며, 엠비언트 라이트가 시각적 경고 제공  (빨간색 점등 등).<br />- 사용자 개입 시 시스템이 제어를 해제하며 정상 모드로 전환. <br />**5단계: 시스템 종료**<br />- 차량 주행 종료 시, 모든 기능이 안전하게 비활성화되며 엠비언트 라이트는 꺼짐. |
| 기능                   | **1. 차량 기본 조작(시동, 기본 주행-정지,가속,감속)<br />** **2. 차량 속도 유지 제어 (Cruise Control, 선행 차량이 없을 경우)**<br /> **3. 선행 차량과 차간거리 제어(1~4단계)** <br />a. 단계에 따른 차간거리 조절 (e.g. 1이면 150m, 2면 120m 등) <br />b. 선행 차 정지 시 출발 제어 <br /> **4. 엠비언트 라이트**<br /> a. ACC 위험상황(선행 차량 급제동, 정지차량 주의) 표시 <br />b. ACC 단계마다 엠비언트 라이트 색을 다르게해서 시각화 <br />**5. 차량 안전** <br />a. 충돌 시 에어백 작동 조건 감지 후 에어백 작동  <br />b. 운전자 존재여부 판단, 안전벨트 안하면 알람/붉은 조명 <br />**6. 클러스터 구현** <br />a. 속도, RPM, 시동 상태 표시 <br />b. ACC 설정 속도 상태(목표속도) 표시<br />c. ACC 모드 상태(거리 민감도 Level) 표시   <br />d. 시스템 경고등 표시  <br />e. 크루즈 컨트롤 모드 표시 (Cruise / Nothing) <br />**7. HMI 구현** <br />a. ACC 작동 ON/OFF <br />b. ACC 속도 단계 버튼 (상/하) <br />c. ACC 모드 단계 버튼 (상/하)  <br />d. 시동 ON/OFF 버튼 구현 |
| 사용기술               | Jira : 프로젝트 일정 관리Confluence : 산출물 관리git (Github) : CAPL 소스코드 형상관리, 협업Discord : 자료 공유, 프로젝트 업무 분장, 대화 |
| 기대효과               | 1. 운전자의 피로도 감소<br />2. 차량 운행 시 위험 상황 시각적 인지<br />3. 승객 보호 |
