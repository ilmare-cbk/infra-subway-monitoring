<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>

### 1단계 - 웹 성능 테스트

- Running Map : https://ilmare-cbk-subway.kro.kr/

#### 경쟁사 성능 비교분석 (Mobile)

| 측정항목 | Running Map | 서울교통공사 | 네이버지도 | 카카오맵  |
|------|-------------|--------|-------|-------|
| FCP  | 15.1s       | 6.3s   | 2.2s  | 1.7s  |
| TTI  | 15.6s       | 8.3s   | 6.1s  | 5.2s  |
| SI   | 15.1s       | 9.5s   | 6.2s  | 7.7s  |
| TBT  | 460ms       | 680ms  | 290ms | 120ms |
| LCP  | 15.6s       | 6.6s   | 7.4s  | 5.5s  |
| CLS  | 0.042       | 0      | 0.03  | 0.005 |

#### 경쟁사 성능 비교분석 (Desktop)

| 측정항목 | Running Map | 서울교통공사 | 네이버지도 | 카카오맵  |
|------|-------------|--------|-------|-------|
| FCP  | 2.7s        | 1.5s   | 0.5s  | 0.5s  |
| TTI  | 2.8s        | 2.1s   | 0.5s  | 0.7s  |
| SI   | 2.7s        | 2.8s   | 2.4s  | 2.6s  |
| TBT  | 50ms        | 320ms  | 0ms   | 0ms   |
| LCP  | 2.8s        | 2.2s   | 1.4s  | 1.1s  |
| CLS  | 0.004       | 0.001  | 0.006 | 0.039 |

1. 웹 성능예산은 어느정도가 적당하다고 생각하시나요

- `CLS`는 성능 분석결과(Mobile, Desktop) 90~100점 (100점 기준) 사이의 결과값을 갖기 때문에 웹 성능예상 항목에서는 제외 했습니다.
- 사용자는 응답시간이 20% 이상일 때(유사 제품군과의 비교 시) 차이를 느끼므로 가장 빠른 경쟁사의 응답결과보다 20% 이상 차이나는 항목에 대해서 웹 성능예산 항목을 선정하였습니다.
- 3개의 경쟁사 중 `서울교통공사`가 전체적으로 가장 낮은 성능을 보여주고 있음으로 이를 제외한 `네이버지도`, `카카오맵` 두 결과값의 평균을 웹 성능예산으로 산정하였습니다.

#### CASE : Mobile

|       | FCP   | TTI   | SI    | TBT   | LCP   |
|-------|-------|-------|-------|-------|-------|
| AS-IS | 15.1s | 15.6s | 15.1s | 460ms | 15.6s |
| TO-BE | 1.95s | 5.65s | 6.95s | 205ms | 6.45s |

#### CASE : Desktop

|       | FCP  | TTI  | SI   | TBT  | LCP   |
|-------|------|------|------|------|-------|
| AS-IS | 2.7s | 2.8s | 2.7s | 50ms | 2.8s  |
| TO-BE | 0.5s | 0.6s | 2.5s | 0ms  | 1.25s |

2. 웹 성능예산을 바탕으로 현재 지하철 노선도 서비스의 서버 목표 응답시간 가설을 세워보세요.

- 텍스트 압축 사용
    - /js/vendors.js (전송크기: 2125kb -> 가능한 절감효과: 1716.5kb)
    - /js/main.js (전송크기: 172kb -> 가능한 절감효과: 143.6kb)
- 사용하지 않는 자바스크립트 줄이기
    - /js/vendors.js (전송크기: 2125kb -> 가능한 절감효과: 637.3kb)
    - /js/main.js (전송크기: 172kb -> 가능한 절감효과: 61.8kb)
- 효율적인 캐시 정책을 사용하여 정적인 애셋 제공하기
    - /js/vendors.js
    - /js/main.js
    - /images/main_logo.png
    - /images/logo_small.png
- 이미지 요소에 명시적인 너비 및 높이를 설정하여 레이아웃 변경 횟수를 줄이고 누적 레이아웃 변경을 개선

---

### 2단계 - 부하 테스트 
1. 부하테스트 전제조건은 어느정도로 설정하셨나요

2. Smoke, Load, Stress 테스트 스크립트와 결과를 공유해주세요

---

### 3단계 - 로깅, 모니터링
1. 각 서버내 로깅 경로를 알려주세요

2. Cloudwatch 대시보드 URL을 알려주세요
