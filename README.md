# 1.개요
- kaggle Playground Series - Season 3, Episode 2, Tabular Classification with a Stroke Prediction Dataset
- https://www.kaggle.com/competitions/playground-series-s3e2

## 1.1 참가인원
- [우리행복하게해조]
- 강민성 hkmast
- 김태혁 kimtaehyuk1
- 박소훈 [hoonaianooh]: https://github.com/hoonaianooh 
- 이지원 [Wlfjd]: https://github.com/Wlfjd


# 2. 데이터 준비 + EDA 분석
## 2.1 정답비율
<table>
      <tr>
            <td style="text-align:center">정답비율</td>
      </tr>
      <tr>
            <td><img width="300" , height="250", alt="image" src="https://user-images.githubusercontent.com/50509845/220023239-99043806-0057-4a12-a6e2-f73d024e1dda.png"></td>
      </tr>
      <tr>
            <td>-	정답 비율의 차이가 크므로, stratifiedkfold 고려
            </td>
      </tr>
</table>

## 2.2 이진형	
- Residence_type를 제외하고 모든 피처들이 구분이 명확하다.
- Residence_type은 명확히 구분이 안가므로 제거도 고려 해볼만하다.
- gender에서 Other 이상치가 존재한다. 최빈값으로 치환하겠다.

<table>
      <tr>
            <td style="text-align:center", colspan="2">이진형 피쳐의 정답 비율</td>
      </tr>
      <tr>
            <td><img width="196" alt="image" src="https://user-images.githubusercontent.com/50509845/220026606-bcfaca7a-bd5b-4eb1-ae1e-88795dec006b.png"></td>
            <td><img width="188" alt="image" src="https://user-images.githubusercontent.com/50509845/220026737-6e6f0831-49b1-4a79-8350-782c77e48538.png"></td>
      </tr>
      <tr>
            <td><img width="190" alt="image" src="https://user-images.githubusercontent.com/50509845/220026831-4f314993-80ea-4ccb-abbc-a0a2ca96800c.png"></td>
            <td><img width="191" alt="image" src="https://user-images.githubusercontent.com/50509845/220026880-3954a0ca-01ab-42e7-a288-40b38633259a.png"></td>
      </tr>
      <tr>
            <td colspan="2"><img width="197" alt="image" src="https://user-images.githubusercontent.com/50509845/220026937-729df07d-3699-4fe7-92d5-85fa437a7e58.png"></td>
      </tr>
</table>

## 2.3 명목형 데이터
- 타겟비율이 비슷한 도메인이 있어서 이것들을 하나로 묶어보는 방법 사용

<table>
      <tr>
            <td style="text-align:center">명목형 데이터 개요</td>
      </tr>
      <tr>
            <td><img width="452" alt="image" src="https://user-images.githubusercontent.com/50509845/220028007-27af9cbd-dd93-48bf-aecc-df34459fce99.png"></td>
      </tr>
</table>

### 2.3.1 밀도그래프
- 'avg_glucose_level, 'bmi', 'age'는 연속형수치형과 범주형-순서형으로 처리하여 시각화 분석 및 학습 진행
- 바로 스케일링하여 학습했을 때와 결과 차이 비교 => 제출 결과 연속형 수치  데이터는 순서형으로 처리하지 않고 그대로 스케일링하여 학습시켰을 때 높은 성능 결과가 나왔다.

<table>
      <tr>
            <td style="text-align:center", colspan="2">밀도그래프(히스토그램)</td>
      </tr>
      <tr>
            <td><img width="195" alt="image" src="https://user-images.githubusercontent.com/50509845/220029083-01770a64-294f-40e8-9a3b-48775da6cee9.png"></td>
            <td><img width="190" alt="image" src="https://user-images.githubusercontent.com/50509845/220029145-d224d7b5-ae9e-4f80-af7d-39f2d4b1d2f0.png"></td>
      </tr>
      <tr>
            <td colspan="2"><img width="189" alt="image" src="https://user-images.githubusercontent.com/50509845/220029223-d14c0aa9-9211-45b2-8f03-97aebfe5c21c.png"></td>
      </tr>
</table>

### 2.3.2 비율 그래프
- 'avg_glucose_level, 'bmi', 'age' 데이터를 범주형-순서형으로 처리하여 데이터 EDA 2차 분석
- 당뇨병이 없는 혈당수치가 정상인 경우와 당뇨병전단계에서는 뇌졸중 타겟값 비율이 낮게 나온다
- 당뇨병 환자인 경우 뇌졸중 타겟값 비율이 매우 높게 나타났다 => 당뇨병과 뇌졸중 간의 관계가 있음을 생각할 수 있다
- bmi지수가 높을수로 뇌졸중 타겟값 비율이 높게 나타났다
- 나이가 고령일수록 뇌졸중 타겟값 비율이 높게 나타났다

<table>
      <tr>
            <td style="text-align:center", colspan="2">비율 그래프</td>
      </tr>
      <tr>
            <td><img width="211" alt="image" src="https://user-images.githubusercontent.com/50509845/220029678-49cc999e-a19f-43b0-8bcd-bb4d8c243fdb.png"></td>
            <td><img width="212" alt="image" src="https://user-images.githubusercontent.com/50509845/220029730-8b5f908a-9bf3-4798-87ca-81a431880afc.png"></td>
      </tr>
      <tr>
            <td colspan="2"><img width="205" alt="image" src="https://user-images.githubusercontent.com/50509845/220029794-a123bb71-b6f5-436b-8104-ddd116c77411.png"></td>
      </tr>
</table>

# 3. EDA 분석 결과
- 이진형
  - 컬럼
    - gender
    -  hypertension 
    - ever_married
    - heart_disease 
    - Residence_type

  - 인코딩
    - 숫자로 치환 후 OneHotEncoding 인코딩 진행

- 명목형
  - 컬럼
    - work _type
    - smoking_status

  - 인코딩
    - OneHotEncoding 인코딩 진행

- 연속형
  - 컬럼
    - age
    - avg_glucose_level
    - bmi 
  - 스케일러
    - MinMax, Standard, MaxAbs, Robust, Log등 다양하게 조합

# 4. 피처엔지니어링 결과
- 피처의 고유값별 정답값1인 데이터의 비율이 기존 train데이터에 부족하다고 판단.
- 캐글의 해당 에피소드 원본데이터 중 stroke 값이 1인 데이터를 불러와 병합 (학습성능 향상에 도움이 될거라 예측)
- 연속형수치인 피처들은 순서형으로 변환하지 않고 그대로 스케일링하여 학습하는 것이 학습성능이 높게 나왔다.

# 5. 베이스라인 모델 구축 및 기본학습
- XGBoost 모델 선정 
- 조원 모두 XGBoost 모델의 결과가 좋았다
- 원본데이터에는 결측치가 존재 -> XGBoost 모델이 결측치를 자동 처리해주므로  XGBoost 모델로 진행하기로 결정 
- 피처 엔지니어링 단계에서, 각피처들의 특성별로 처리해서 만들 수 있는 모든 조합(1000개)으로 XGBoost 모델에 K-Fold교차검증을 진행
- 검증 결과를 통한 점수를 내림차순으로 정렬하여 상위100개 조합을 엑셀에 저장
- 상위100개 중 높은 빈도의 데이터 엔지니어링 방법을 추출(ex) work_type3 / smoking2 or 3 ) -> 여기서 20개의 조합이 생성
- 20개의 조합을 전부 제출하여 조원 개인별 시도결과보다 점수가 향상되었는지 확인
- 위의 일련의 과정의 결과가 조원들의 개인 시도 결과에 비해 높은 점수가 나왔으므로 방향성이 맞다고 판단, 이에 얻어진 결과에 최적의 하이퍼파라미터를 추가로 구성하고자 함


# 6. 모델 성능 향상
- 최적 XGBoost모델의 최적 파라미터를 찾기위해 우선적으로 베이지안 최적화를 통해 하이퍼파라미터를 추출
- 베이지안이 찾아준 파라미터를 기본베이스로, 다른 파라미터를 넣고, 값도 바꾸어보면서 최적의 파라미터 값을 도출!
- 이렇게 찾은 최적의 모델과 최적의 파라미터들을 가지고 다시 모든 조합(1000개)의 성능 값을 확인한 후 캐글에 제출하는 것까지를 자동화 시켜 진행

# 7. 최적 모델 선정
- TOP100 중 높은 빈도의 데이터 엔지니어링 방법을 추출, 약 20개를 반자동화 학습, 파일생성하여 제출

- 최고 점수
  - private  : 0.90044
  - 770팀중 3등!!

<img width="452" alt="image" src="https://user-images.githubusercontent.com/50509845/220031638-277693cb-e013-4652-bbbf-b6f777d5f83e.png">
