<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0b2545,50:13315c,100:1f6feb&height=190&section=header&text=Ahn%20Je-won&fontSize=48&fontColor=ffffff&fontAlignY=36&desc=Robotics%20%C2%B7%20Embedded%20Software%20Engineer&descAlignY=58&descSize=18" width="100%" />

**센서에서 제어까지, 로봇이 실제로 움직이게 만드는 쪽을 해 왔습니다.**

증상을 덮는 대신 원인을 수치로 규명하고, 계층을 분리해 재발을 막는 방식으로 일합니다.

<a href="mailto:inno505@naver.com"><img src="https://img.shields.io/badge/Email-inno505@naver.com-EA4335?style=flat-square&logo=gmail&logoColor=white" /></a>
<img src="https://img.shields.io/badge/Focus-Equipment%20SW%20%C2%B7%20Robotics%20%C2%B7%20Embedded-1f6feb?style=flat-square" />

</div>

---

## About

- 충북대학교 컴퓨터공학과 졸업 · **SSAFY 15기 임베디드 트랙** 수료
- ROS2 자율주행 스택과 MCU 펌웨어를 오가며, 인식·제어·통신을 한 사슬로 붙이는 일을 주로 했습니다
- 관심 분야 — 반도체·디스플레이 **장비 SW**, **로보틱스 / 자율주행**, **임베디드 · AIoT**

<br/>

## Skills

![ROS2](https://img.shields.io/badge/ROS2%20Humble-22314E?style=flat-square&logo=ros&logoColor=white)
![Nav2](https://img.shields.io/badge/Nav2%20%C2%B7%20SLAM%20%C2%B7%20Fast%20DDS-22314E?style=flat-square)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch%20%C2%B7%20TensorRT-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![Jetson](https://img.shields.io/badge/Jetson%20Orin%20%C2%B7%20Pico%20W%20%C2%B7%20ESP32-76B900?style=flat-square&logo=nvidia&logoColor=white)
![Linux](https://img.shields.io/badge/Linux%20%C2%B7%20Docker%20%C2%B7%20Git-E95420?style=flat-square&logo=linux&logoColor=white)

| | |
|---|---|
| **Robotics** | ROS2 Humble · Nav2 · slam_toolbox · Fast DDS · 센서 융합(LiDAR · ToF · IMU) |
| **Embedded** | C · MicroPython · Jetson Orin Nano · Pico W · ESP32-S3 / FreeRTOS · I2C · UART · BLE |
| **AI · Data** | PyTorch · TensorRT · OpenCV · scikit-learn · XGBoost / LightGBM / CatBoost |
| **App · Etc** | C++ / MFC · Flutter · Android · Django · MQTT · Docker · Git · Jira |

<br/>

## Projects

### 🚜 F.A.S.T. — AIoT 무인 지게차 물류 자동화

1/10 스케일 지게차가 자율주행으로 파렛트에 포크를 꽂아 화물을 이송하는 디지털 트윈 제어 시스템<br/>
`2026.07~08` · 6인 팀 (SSAFY 공통 프로젝트 **우수상**) · **자율주행 파트** — LiDAR · SLAM · Nav2 · 센서 융합

> 데모 3일 전 통신이 조용히 끊기던 장애를 Fast DDS 공유메모리 결함으로 규명해 **유실률 0%** 로 되돌렸고,
> 저속 구간 헌팅은 제어기를 다시 설계해 **속도 오차를 37%에서 4%** 로 줄였습니다.

<details>
<summary>기술적 판단 3가지</summary>

- **DDS 전송 방식 전환** — 캐시 삭제로 넘기지 않고 `/dev/shm`에 남는 세마포어 잔여물을 원인으로 추적했습니다. 단일 보드 통신임에 착안해 UDPv4 로컬 루프백으로 전환 → 공유메모리 세그먼트 109개 → 4개
- **적분(I) 전용 속도 제어** — 정지마찰 문턱을 넘지 못해 차량이 멈추던 구간에서, 오차가 커져야 반응하는 P 제어를 폐기하고 멈춘 동안 듀티를 축적하는 제어기로 재설계
- **costmap 레이어 격리** — ToF의 clearing 판단이 LiDAR가 잡은 정면 장애물을 지워 회피 루프에 빠지던 현상을 Maximum 병합 특성까지 추적해 레이어를 분리

`ROS2 Humble` `Nav2` `slam_toolbox` `Fast DDS` `Jetson Orin Nano` `ESP32-S3` `C++/Python`

</details>

<br/>

### 🔭 [Serendipity Engine](https://github.com/AhnJewon/serendipity_engine) — 역발상 AI 검색 엔진

관심사의 의미적 대척점을 계산해, 그 사이를 지식 그래프와 벡터 보간으로 이어 주는 필터 버블 탈출 검색기<br/>
`2025.10~2026.02` · **1인 개발** (학부 연구 연계)

> 한글 위키백과 **표제어 124만 건**을 벡터 DB로 세우고, 무관한 단어가 아니라 납득 가능한 경로로
> 낯선 주제까지 데려가는 탐색 알고리즘을 설계했습니다.

<details>
<summary>기술적 판단 2가지</summary>

- **K-Means 군집 기반 대척 테마 선정** — 유사도 최하위만 뽑으면 문맥 없는 고립 단어가 나오므로, 후보군을 군집화(k=5)해 중심에서 안정적인 테마를 고르도록 변경
- **Gap-Filling 재귀 평탄화** — 경로 중간에서 인접 노드 유사도가 0.5 미만으로 떨어지면 두 벡터의 내분점을 재귀 삽입해 의미적 비약을 완화

`Python` `Ko-SBERT` `KeyBERT` `Vector DB` `Wikidata SPARQL` `Streamlit`

</details>

<br/>

### 🧤 Power Up — 재활 스마트 글러브

편마비 환자의 손가락 압력과 손목 자세를 계측해 재활 게임과 실시간 연동하는 웨어러블<br/>
`2024` · 4인 팀 (**CEDC 2024 은상**) · **하드웨어 전반 및 BLE 펌웨어**

> 점퍼선 없이 동일 주소 ToF 센서들을 분리하고, BLE 패킷이 잘려 파싱이 조용히 실패하던 문제를
> MTU 협상으로 해결해 고주파 구간 **패킷 보존율 100%** 를 확보했습니다.

<details>
<summary>기술적 판단 2가지</summary>

- **I2C 주소 런타임 재할당** — 같은 기본 주소(0x29)를 쓰는 다중 VL6180X를 부팅 시 GPIO로 순차 전원 인가하며 레지스터 주소를 하나씩 재설정
- **지자기 자체 캘리브레이션** — 부팅 시 100 샘플을 수집해 하드/소프트 아이언 왜곡을 보정, 방위각 신뢰도 확보

`MicroPython` `Raspberry Pi Pico W` `MPU9250` `VL6180X` `BLE`

</details>

<br/>

### 그 외

| 프로젝트 | 한 줄 | 역할 |
|---|---|---|
| **Kaggle 산림 피복 예측** | 58만 행 환경 변량으로 7종 피복을 분류, 3종 부스팅 앙상블로 CV 88.58% | 1인 |
| **C++ MFC 프로토콜 스택 · SW 라우터** | Ethernet/IP/ARP 계층을 직접 설계하고 패킷을 포워딩하는 장비 모사기 | 1인 |
| **RC카 라인 트레이싱 자율주행** | 비전 차선 인식과 LiDAR/Sonar를 융합한 30Hz 제어 루프 | 1인 |
| **야금야금 — AI 복약 관리** | 고령층 복약 실수를 줄이는 앱 (충청권 ICT 공모전 최우수상) | 카메라 · 알람 · UI |
| **[오공파 — 미세먼지 모니터링](https://github.com/AhnJewon/Open_Source_Project_DustSensor)** | 센서 값을 BLE로 받아 지도에 뿌리는 Android 대시보드 | 1인 |

<br/>

## Education & Awards

**충북대학교** 컴퓨터공학과 학사 · 2020.03 ~ 2026.02 · 4.08 / 4.5 · 석차 3 / 50<br/>
**SSAFY 15기** 임베디드 트랙 925시간 · **정보처리기사** (2025.09) · **OPIc** IH

**수상** — SSAFY 공통 프로젝트 우수상 (2026) · CEDC 2024 국제 창의설계 경진대회 은상 · 충청권 ICT 이노베이션 SW개발 공모전 최우수상 (2024)

<br/>

## GitHub

<div align="center">

<img src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username=AhnJewon&theme=github_dark" height="200" />

<img src="https://ghchart.rshah.org/1f6feb/AhnJewon" width="88%" alt="AhnJewon contribution chart" />

</div>

> 팀 프로젝트와 산학 과제는 사내망 GitLab과 비공개 저장소에서 진행했습니다. 필요하시면 코드와 발표자료를 함께 공유하겠습니다.

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1f6feb,50:13315c,100:0b2545&height=110&section=footer" width="100%" />

</div>
