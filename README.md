# 주제
- 신용등급 분류

# 대회출처
- DACON

# 결과
- log loss 0.76

# 알고리즘 
- catboost 사용
- 로지스틱
- 랜덤포레스트

# 해결문제
1. FLAG_MOBIL 컬럼, 은 value가 1밖에 없음 -> 결과에 영향이 없음으로 삭제
6. **동일한 사람으로 추정되는 데이터 존재 -> 한사람이 여러 카드를 소유**
2. occyp_type 컬럼, 은퇴한 분들만 nan 임 -> 'Unknown'로 대체
3. DAYS_EMPLOYED 컬럼, 현재 일하지 않은 사람들은 양수 & occyp_type 컬럼에서 nan인 사람들 밖에 없음 -> 즉, 은퇴한 사람만 양수
4. 개별 컬럼들은 begin_month, DAYS_EMPLOYED를 제외한 나머지 컬럼은 credit에 크게 관여하지 않음 -> 컬럼간의 파생변수 필요
5. family_size가 childe_num보다 작을 수 있음 -> 출가 고려 -> 부양가족수

모든피쳐가 타겟변수에 크게 유효하지 않아서 변수 한개에 여러 파생변수를 만들어야함
ex) 
  - DAYS_EMPLOYED -> 년, 월, 일
  - DAYS_EMPLOYED / DAYS_BIRTH 비율
