# bigproject "화물타고" - 최우수상

2023.12.11 : KT에이블스쿨 4기 빅프로젝트 시작(8명과 한 조)

- 주제: 미들마일 AI 추천 서비스 웹 개발
  
맡은 역할: AI개발  
1. 적정 가격 예측에서 톤 수 별 가격 예측 모델링 만듦(LightGBM)  
2. AI 배차 추천서비스 전처리 및 모델 개발을 함(K-prototype)
3. AI 배차 추천 서비스 파이프라인 구축
4. 음성인식 채팅 서비스 제안
5. 적정 가격 측정을 위한 운송고려사항 파악
6. PPT작성
7. 데이터 수집

- 화물타고의 핵심 AI기술  
1. AI 배차 추천 서비스  
2. 적정 가격 예측  
3. STT를 이용한 음성 채팅

데이터가 없고 찾기 힘들어서 데이터 수집에 많은 시간을 투자  
직접 이메일 돌리고 연락드리면서 거절당하고 한 곳에서 허락받아 데이터 수집함.

- 주제 선정 이유 및 특징:  
디지털 전환의 어려움, 화주, 차주간의 소통의 어려움, 대기시간 고려하지 않은 가격  
지역, 상품 특성, 차량의 종류와 옵션에 따른 매칭 시스템  
stt를 이용한 화주와 차주간의 편리한 채팅 시스템  
AI추천 서비스(kprototype) ai 배차 최적화  
날씨와 심야시간, 공휴일여부, 공차, 차량 종류, 옵션에 따른 적정 가격 측정 - 적정 운임 추천  

- AI추천 서비스:  
변수 선택 및 결측치 제거, 데이터 변환, 네이버 api를 이용해 지오코딩으로 주소를 위도 경도로 변환  
k-prototype 알고리즘사용, kmeans와 비교했지만 차원축소 후 나타낸 그래프와 실루엣 점수를 확인한 결과 14개의 군집을 갖는 kprototype모델 선택 - 실루엣 점수 2.80  
연속형,범주형이 모두 존재하는 데이터에 가장 알맞은 군집 알고리즘  
군집이 형성된 차주 데이터에 새로운 배차 데이터를 삽입  
배차데이터가 속하는 군집을 예측해 이를 기반으로 차주에게 배차를 매칭  
필수요소들은 필터링을 거치고 harversine으로 차주와 현재 위치에서 배차 데이터의 가까운 출발지 거리를 계산  
더 나아가 차주마다 배차 완료 데이터가 여러 건이 쌓이면 차주의 배차 완료 데이터와 새로운 배차 데이터와의 코사인 유사도를 계산하여 배차 데이터를 순위 매김  
군집화보다 더 차주 개인 맞츔형 추천이 가능해짐

- 적정 가격 예측:  
트럭 톤 수별 거리 기본 가격 데이터를 가지고 트럭 톤 수별 가격 예측을 위해 random,xgb,lgbm을 비교해 r2값이 가장 높은 lgmb을 선택  
날씨와 대기시간, 공차여부 가능성을 가지고 적정가격 예측  
지역 및 시간을 모두 고려한 미래의 날씨 데이터를 네이버에서 지역별 오전/오후의 날씨 정보를 크롤링 - 눈/비의 경우 가격 할증  
화주가 원한 출발시간에서 도착시간까지 운전시간, 상차시간, 휴식시간을 제외한 대기시간에 대해 2시간 이후부터 30분당 2만원 추가  
차주 데이터를 활용하여 출발지의 비율이 10%가 넘으면 할인 비율이 5% 이하라면 5%의 할증으로 공차 여부 가격 할증


- STT를 이용한 음성 인식 채팅:  
✔️음성 인식으로 화주와 차주간의 소통  
✔️Google Speech-Recognition 라이브러리 이용

기대효과: 운송 업무 효율성 증대, 적정 운임으로 사용자 만족도 향상, 차주화주 간 소통 편의성 증댕, AI배차를 통한 맞춤형 배차 선택 가능

ai배차 추천서비스 데이터 수집  
차주데이터: 2017 전국 화물통행 실태조사의 원시데이터 수집 - 국가교통DB  
화주데이터: 한국산업단지 공단의 전국산업단지현황통계 중에서 국가산업단지 데이터 수집 - 공공데이터포털
