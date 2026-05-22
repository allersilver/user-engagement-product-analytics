# 콘텐츠 품질과 사용자 Retention 분석
## Amazon 리뷰 데이터 기반 Product Analytics 프레임워크 설계

---

##  핵심 질문 
> "콘텐츠 품질과 추천 다양성이 사용자 retention에 미치는 영향은 무엇인가?
>  그리고 이를 개선하기 위한 추천 정책을 어떻게 설계할 수 있는가?"

---

## 핵심 분석 
1. 첫 세션에서 고품질 콘텐츠를 본 사용자의 D7 Retention = 33.7% (저품질 그룹 26.4% 대비 +7.3%p)
2. 추천 다양성 상위 그룹의 D7 Retention = 40.5% (하위 그룹 12.2% 대비 3.3배 높음)
3. 저품질 콘텐츠의 skip_rate = 33.5% (고품질 25.0% 대비 높음)

---

## 실험 설계 (A/B Test)
| 실험 | 효과 | p-value | 결론 |
|------|------|---------|------|
| Quality-First 추천 | +6.1%p | 0.0011 | 전체 적용 권장 o |
| 추천 다양성 Constraint | +28.7%p | <0.0001 | 전체 적용 권장 o |

---

## 기술 스택
Python | Pandas | SQL (SQLite) | 코호트 분석 | A/B Test 설계 | KPI 설계

---

## 분석 구조
| 노트북 | 내용 | 핵심 산출물 |
|--------|------|------------|
| 01_event_schema | 이벤트 로그 설계 및 합성 데이터 생성 | 24,134개 이벤트 로그 |
| 02_cohort_retention | 코호트 분석 및 D7 Retention 측정 | 첫 세션 품질 → retention 관계 |
| 03_recommendation | 추천 다양성 분석 | entropy 기반 다양성 → retention 관계 |
| 04_ab_test_design | A/B Test 설계 및 시뮬레이션 | 두 실험 모두 통계적 유의미 |
| 05_sql_analysis | SQL 기반 데이터 분석 | 세그먼트/카테고리별 행동 패턴 |

---

## 데이터 한계
- Amazon 리뷰 데이터를 콘텐츠 품질 proxy로 활용 (실제 watch_time 로그 없음)
- 사용자 행동은 합성 데이터로 생성 (실제 서비스 로그와 다를 수 있음)
- 카테고리가 3개에 집중되어 다양성 측정에 제한적

---

## 데이터 출처
- Amazon Sales Dataset (Kaggle)
- 사용자 행동 로그: 합성 데이터 

## 참고
- 데이터 전처리 과정: [Amazon Review QA Analysis](https://github.com/allersilver/amazon-review-qa-analysis)