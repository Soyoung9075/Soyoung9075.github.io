# 서울 지역 아파트 분석용 최종 데이터 셋 완성


```python
import pandas as pd
import numpy as np
```


```python
# 모든 지역/면적 분양가 리스트 불러오기

df = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\final_merged_apt_data.csv')
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>입주예정월</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ｅ편한세상　운정　어반프라임Ａ２７（파주</td>
      <td>경기도　파주시　운정３지구　Ａ－２７블록（동패동）</td>
      <td>1009세대</td>
      <td>059.6242A</td>
      <td>30,960</td>
      <td>경기</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>대림산업(주)</td>
      <td>2021.07</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ｅ편한세상　운정　어반프라임Ａ２７（파주</td>
      <td>경기도　파주시　운정３지구　Ａ－２７블록（동패동）</td>
      <td>1009세대</td>
      <td>059.3403B</td>
      <td>30,960</td>
      <td>경기</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>대림산업(주)</td>
      <td>2021.07</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ｅ편한세상　운정　어반프라임Ａ２７（파주</td>
      <td>경기도　파주시　운정３지구　Ａ－２７블록（동패동）</td>
      <td>1009세대</td>
      <td>059.9747C</td>
      <td>28,060</td>
      <td>경기</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>대림산업(주)</td>
      <td>2021.07</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ｅ편한세상　운정　어반프라임Ａ２７（파주</td>
      <td>경기도　파주시　운정３지구　Ａ－２７블록（동패동）</td>
      <td>1009세대</td>
      <td>074.7261A</td>
      <td>36,950</td>
      <td>경기</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>대림산업(주)</td>
      <td>2021.07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ｅ편한세상　운정　어반프라임Ａ２７（파주</td>
      <td>경기도　파주시　운정３지구　Ａ－２７블록（동패동）</td>
      <td>1009세대</td>
      <td>084.8864A</td>
      <td>41,390</td>
      <td>경기</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>대림산업(주)</td>
      <td>2021.07</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 서울 데이터만 추출 - 데이터1

df_seoul = df.loc[df['지역'] == '서울']
df_seoul.shape
```




    (1073, 10)




```python
# 실거래가 merge용 아파트명 / 세대수 / 교통 / 학군 데이터 불러오기 - 데이터2

df2 = pd.read_excel(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_apt_list.xlsx')
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>입주예정월</th>
      <th>아파트명2</th>
      <th>시</th>
      <th>구</th>
      <th>세대수</th>
      <th>소형평수세대수</th>
      <th>중형평수세대수</th>
      <th>대형평수세대수</th>
      <th>특이사항</th>
      <th>인근 지하철 호선수</th>
      <th>지하철역</th>
      <th>호선</th>
      <th>지하철도보(분)</th>
      <th>을지로</th>
      <th>강남</th>
      <th>초등학교거리(도보/분)</th>
      <th>중학교배정학군</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>2022.10</td>
      <td>서대문푸르지오센트럴파크</td>
      <td>서울특별시</td>
      <td>서대문구</td>
      <td>832.0</td>
      <td>543.0</td>
      <td>273.0</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
    </tr>
    <tr>
      <th>1</th>
      <td>녹번역　ｅ편한세상　캐슬　２차　（서울）</td>
      <td>서울틀별시　은평구　응암동　３６，３７，５３번지　일대（응암제２구역　주택재개발정비사업）</td>
      <td>2020.05</td>
      <td>녹번역e편한세상캐슬</td>
      <td>서울틀별시</td>
      <td>은평구</td>
      <td>2569.0</td>
      <td>1687.0</td>
      <td>794.0</td>
      <td>88.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>녹번역</td>
      <td>3호선</td>
      <td>6.0</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>8</td>
      <td>서부2학교군</td>
    </tr>
    <tr>
      <th>2</th>
      <td>송파　시그니처　롯데캐슬　（서울）</td>
      <td>서울특별시　송파구　거여동　１８１，　２０２번지　일대</td>
      <td>2022.01</td>
      <td>송파시그니처롯데캐슬</td>
      <td>서울특별시</td>
      <td>송파구</td>
      <td>1945.0</td>
      <td>920.0</td>
      <td>987.0</td>
      <td>38.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>거여역</td>
      <td>5호선</td>
      <td>7.0</td>
      <td>50.0</td>
      <td>40.0</td>
      <td>9</td>
      <td>강동송파4학교군</td>
    </tr>
    <tr>
      <th>3</th>
      <td>이수　푸르지오　더　프레티움　（서울）</td>
      <td>서울시　동작구　사당동　４２번지　일대（사당３　주택재건축정비사업）</td>
      <td>2021.06</td>
      <td>이수푸르지오더프레티움</td>
      <td>서울특별시</td>
      <td>동작구</td>
      <td>514.0</td>
      <td>193.0</td>
      <td>306.0</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>총신대입구역</td>
      <td>4호선</td>
      <td>9.0</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>5</td>
      <td>동작관악2학교군</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ＳＨ　３７차　장기전세　８５초과</td>
      <td>서울특별시　서초구　매헌로１６길４０</td>
      <td>2020.01</td>
      <td>NaN</td>
      <td>서울특별시</td>
      <td>서초구</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SH 장기전세</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 학군데이터 정량화하기


```python
# 학군별 중학교리스트 불러오기 (from 호갱노노)

school = pd.read_excel(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\서울중학교학군통합.xlsx')
school
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>학군명</th>
      <th>학교명</th>
      <th>상위</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서부3학교군</td>
      <td>이화여자대학교사범대학부속이화·금란중학교</td>
      <td>상위 3%</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서부3학교군</td>
      <td>동명여자중학교</td>
      <td>상위 15%</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서부3학교군</td>
      <td>가재울중학교</td>
      <td>상위 15%</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서부3학교군</td>
      <td>인창중학교</td>
      <td>상위 23%</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서부3학교군</td>
      <td>정원여자중학교</td>
      <td>상위 25%</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>250</th>
      <td>북부3학교군</td>
      <td>재현중학교</td>
      <td>상위 49%</td>
    </tr>
    <tr>
      <th>251</th>
      <td>북부3학교군</td>
      <td>중원중학교</td>
      <td>상위 53%</td>
    </tr>
    <tr>
      <th>252</th>
      <td>북부3학교군</td>
      <td>한천중학교</td>
      <td>상위 71%</td>
    </tr>
    <tr>
      <th>253</th>
      <td>북부3학교군</td>
      <td>상계제일중학교</td>
      <td>상위 73%</td>
    </tr>
    <tr>
      <th>254</th>
      <td>북부3학교군</td>
      <td>공릉중학교</td>
      <td>상위 80%</td>
    </tr>
  </tbody>
</table>
<p>255 rows × 3 columns</p>
</div>




```python
# 서울 중학교별 학업성취도, 특목고/자사고 진학률 불러오기

score = pd.read_excel(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\중학교학업성취도.xlsx')
score
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>위치</th>
      <th>학교명</th>
      <th>평균</th>
      <th>특목고 진학률</th>
      <th>특목고 진학수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구 압구정1동</td>
      <td>압구정중학교</td>
      <td>0.976</td>
      <td>0.088</td>
      <td>11명</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강남구 신사동</td>
      <td>신구중학교</td>
      <td>0.826</td>
      <td>0.086</td>
      <td>10명</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강남구 역삼동</td>
      <td>역삼중학교</td>
      <td>0.943</td>
      <td>0.058</td>
      <td>23명</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강남구 도곡동</td>
      <td>도곡중학교</td>
      <td>0.942</td>
      <td>0.057</td>
      <td>12명</td>
    </tr>
    <tr>
      <th>4</th>
      <td>강남구 청담동</td>
      <td>청담중학교</td>
      <td>0.856</td>
      <td>0.055</td>
      <td>6명</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>377</th>
      <td>중랑구 중화동</td>
      <td>중랑중학교</td>
      <td>0.639</td>
      <td>0.013</td>
      <td>2명</td>
    </tr>
    <tr>
      <th>378</th>
      <td>중랑구 중화1동</td>
      <td>장안중학교</td>
      <td>0.637</td>
      <td>0.000</td>
      <td>0명</td>
    </tr>
    <tr>
      <th>379</th>
      <td>중랑구 면목동</td>
      <td>중화중학교</td>
      <td>0.613</td>
      <td>0.005</td>
      <td>1명</td>
    </tr>
    <tr>
      <th>380</th>
      <td>중랑구 망우동</td>
      <td>봉화중학교</td>
      <td>0.542</td>
      <td>0.000</td>
      <td>0명</td>
    </tr>
    <tr>
      <th>381</th>
      <td>중랑구 망우동</td>
      <td>동원중학교</td>
      <td>0.519</td>
      <td>0.009</td>
      <td>1명</td>
    </tr>
  </tbody>
</table>
<p>382 rows × 5 columns</p>
</div>




```python
# 데이터 merge하기 
score.drop(['위치', '특목고 진학수'], axis = 1, inplace = True)

school_merge = pd.merge(school, score, how = 'left', on = '학교명')
school_merge.shape
```




    (255, 5)




```python
# merge한 데이터 NA 확인하기.

school_merge.isna().sum()
```




    학군명        0
    학교명        0
    상위         0
    평균         4
    특목고 진학률    4
    dtype: int64




```python
# 특목고 진학률에 NA가 있는 학교 확인하기

school_merge.loc[school_merge['평균'].isna()]['학교명']
```




    34      위례솔중학교
    47     마곡하늬중학교
    171      한산중학교
    218      신길중학교
    Name: 학교명, dtype: object




```python
# '상위' 컬럼의 데이터 타입을 숫자로 바꾸기
school_merge['상위2'] = school_merge['상위'].str.replace('상위 ', '').str.replace('-', '0').str.rstrip('%')
school_merge['상위2'] = school_merge['상위2'].astype(int)
school_merge['상위2'] = school_merge['상위2'].replace(0, np.nan) # 0을 NaN으로 처리하기 
school_merge.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>학군명</th>
      <th>학교명</th>
      <th>상위</th>
      <th>평균</th>
      <th>특목고 진학률</th>
      <th>상위2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서부3학교군</td>
      <td>이화여자대학교사범대학부속이화·금란중학교</td>
      <td>상위 3%</td>
      <td>0.863</td>
      <td>0.097</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서부3학교군</td>
      <td>동명여자중학교</td>
      <td>상위 15%</td>
      <td>0.900</td>
      <td>0.067</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서부3학교군</td>
      <td>가재울중학교</td>
      <td>상위 15%</td>
      <td>0.854</td>
      <td>0.048</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서부3학교군</td>
      <td>인창중학교</td>
      <td>상위 23%</td>
      <td>0.766</td>
      <td>0.027</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서부3학교군</td>
      <td>정원여자중학교</td>
      <td>상위 25%</td>
      <td>0.855</td>
      <td>0.021</td>
      <td>25.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 학군명에 대해 '평균', '특목고 진학률', '상위2' 평균내기 => 최종형태

school_score = school_merge[['학군명', '평균', '특목고 진학률', '상위2']].groupby('학군명').mean().reset_index()
school_score
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>학군명</th>
      <th>평균</th>
      <th>특목고 진학률</th>
      <th>상위2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남서초1학교군</td>
      <td>0.895000</td>
      <td>0.047429</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강남서초2학교군</td>
      <td>0.909625</td>
      <td>0.029437</td>
      <td>28.562500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강남서초3학교군</td>
      <td>0.902214</td>
      <td>0.021286</td>
      <td>21.285714</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강동송파1학교군</td>
      <td>0.804286</td>
      <td>0.009714</td>
      <td>53.875000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>강동송파4학교군</td>
      <td>0.834615</td>
      <td>0.023615</td>
      <td>31.230769</td>
    </tr>
    <tr>
      <th>5</th>
      <td>강서양천1학교군</td>
      <td>0.772769</td>
      <td>0.017538</td>
      <td>71.083333</td>
    </tr>
    <tr>
      <th>6</th>
      <td>강서양천2학교군</td>
      <td>0.769000</td>
      <td>0.017375</td>
      <td>78.500000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>강서양천4학교군</td>
      <td>0.666444</td>
      <td>0.008000</td>
      <td>86.666667</td>
    </tr>
    <tr>
      <th>8</th>
      <td>남부2학교군</td>
      <td>0.743800</td>
      <td>0.020000</td>
      <td>66.600000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>남부3학교군</td>
      <td>0.676222</td>
      <td>0.005111</td>
      <td>86.857143</td>
    </tr>
    <tr>
      <th>10</th>
      <td>남부4학교군</td>
      <td>0.776364</td>
      <td>0.022545</td>
      <td>46.416667</td>
    </tr>
    <tr>
      <th>11</th>
      <td>동부1학교군</td>
      <td>0.758000</td>
      <td>0.009667</td>
      <td>25.000000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>동부2학교군</td>
      <td>0.732000</td>
      <td>0.013889</td>
      <td>40.777778</td>
    </tr>
    <tr>
      <th>13</th>
      <td>동작관악1학교군</td>
      <td>0.788375</td>
      <td>0.016938</td>
      <td>58.615385</td>
    </tr>
    <tr>
      <th>14</th>
      <td>동작관악2학교군</td>
      <td>0.787857</td>
      <td>0.017571</td>
      <td>47.000000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>동작관악4학교군</td>
      <td>0.716667</td>
      <td>0.016667</td>
      <td>79.200000</td>
    </tr>
    <tr>
      <th>16</th>
      <td>북부1학교군</td>
      <td>0.765769</td>
      <td>0.040154</td>
      <td>34.000000</td>
    </tr>
    <tr>
      <th>17</th>
      <td>북부3학교군</td>
      <td>0.837000</td>
      <td>0.049083</td>
      <td>42.333333</td>
    </tr>
    <tr>
      <th>18</th>
      <td>서부1학교군</td>
      <td>0.751545</td>
      <td>0.013727</td>
      <td>74.363636</td>
    </tr>
    <tr>
      <th>19</th>
      <td>서부2학교군</td>
      <td>0.659571</td>
      <td>0.014857</td>
      <td>71.571429</td>
    </tr>
    <tr>
      <th>20</th>
      <td>서부3학교군</td>
      <td>0.782500</td>
      <td>0.031143</td>
      <td>39.071429</td>
    </tr>
    <tr>
      <th>21</th>
      <td>성동광진2학교군</td>
      <td>0.703167</td>
      <td>0.018667</td>
      <td>63.166667</td>
    </tr>
    <tr>
      <th>22</th>
      <td>성동광진3학교군</td>
      <td>0.797857</td>
      <td>0.021429</td>
      <td>58.142857</td>
    </tr>
    <tr>
      <th>23</th>
      <td>성북강북1학교군</td>
      <td>0.705182</td>
      <td>0.026364</td>
      <td>37.090909</td>
    </tr>
    <tr>
      <th>24</th>
      <td>성북강북2학교군</td>
      <td>0.798091</td>
      <td>0.040727</td>
      <td>36.545455</td>
    </tr>
    <tr>
      <th>25</th>
      <td>중부4학교군</td>
      <td>0.703333</td>
      <td>0.038667</td>
      <td>28.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_score.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\school_score_seoul.csv', index = False, encoding = 'utf-8-sig')
```

## df1, df2, 학군데이터 merge 하기


```python
# df2에서 '아파트명2'에 NA 있는 행 제거하고 불필요한 컬럼 제거

df2_drop = df2.dropna(subset = ['아파트명2'], axis = 0).drop(['공급위치', '입주예정월'], axis = 1)
```


```python
# df2_drop에 학군데이터 (school_score) merge 하기

merge_1 = pd.merge(df2_drop, school_score, how = 'left', left_on = '중학교배정학군', right_on = '학군명')
merge_1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트이름</th>
      <th>아파트명2</th>
      <th>시</th>
      <th>구</th>
      <th>세대수</th>
      <th>소형평수세대수</th>
      <th>중형평수세대수</th>
      <th>대형평수세대수</th>
      <th>특이사항</th>
      <th>인근 지하철 호선수</th>
      <th>...</th>
      <th>호선</th>
      <th>지하철도보(분)</th>
      <th>을지로</th>
      <th>강남</th>
      <th>초등학교거리(도보/분)</th>
      <th>중학교배정학군</th>
      <th>학군명</th>
      <th>평균</th>
      <th>특목고 진학률</th>
      <th>상위2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서대문푸르지오센트럴파크</td>
      <td>서울특별시</td>
      <td>서대문구</td>
      <td>832.0</td>
      <td>543.0</td>
      <td>273.0</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>서부3학교군</td>
      <td>0.782500</td>
      <td>0.031143</td>
      <td>39.071429</td>
    </tr>
    <tr>
      <th>1</th>
      <td>녹번역　ｅ편한세상　캐슬　２차　（서울）</td>
      <td>녹번역e편한세상캐슬</td>
      <td>서울틀별시</td>
      <td>은평구</td>
      <td>2569.0</td>
      <td>1687.0</td>
      <td>794.0</td>
      <td>88.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>3호선</td>
      <td>6.0</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>8</td>
      <td>서부2학교군</td>
      <td>서부2학교군</td>
      <td>0.659571</td>
      <td>0.014857</td>
      <td>71.571429</td>
    </tr>
    <tr>
      <th>2</th>
      <td>송파　시그니처　롯데캐슬　（서울）</td>
      <td>송파시그니처롯데캐슬</td>
      <td>서울특별시</td>
      <td>송파구</td>
      <td>1945.0</td>
      <td>920.0</td>
      <td>987.0</td>
      <td>38.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>5호선</td>
      <td>7.0</td>
      <td>50.0</td>
      <td>40.0</td>
      <td>9</td>
      <td>강동송파4학교군</td>
      <td>강동송파4학교군</td>
      <td>0.834615</td>
      <td>0.023615</td>
      <td>31.230769</td>
    </tr>
    <tr>
      <th>3</th>
      <td>이수　푸르지오　더　프레티움　（서울）</td>
      <td>이수푸르지오더프레티움</td>
      <td>서울특별시</td>
      <td>동작구</td>
      <td>514.0</td>
      <td>193.0</td>
      <td>306.0</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>4호선</td>
      <td>9.0</td>
      <td>40.0</td>
      <td>35.0</td>
      <td>5</td>
      <td>동작관악2학교군</td>
      <td>동작관악2학교군</td>
      <td>0.787857</td>
      <td>0.017571</td>
      <td>47.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>등촌　두산위브　주상복합아파트（서울）</td>
      <td>가양역두산위브</td>
      <td>서울특별시</td>
      <td>강서구</td>
      <td>220.0</td>
      <td>163.0</td>
      <td>56.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>9호선</td>
      <td>8.0</td>
      <td>45.0</td>
      <td>60.0</td>
      <td>15</td>
      <td>강서양천1학교군</td>
      <td>강서양천1학교군</td>
      <td>0.772769</td>
      <td>0.017538</td>
      <td>71.083333</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
merge_1.loc[merge_1['학군명'].isna()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트이름</th>
      <th>아파트명2</th>
      <th>시</th>
      <th>구</th>
      <th>세대수</th>
      <th>소형평수세대수</th>
      <th>중형평수세대수</th>
      <th>대형평수세대수</th>
      <th>특이사항</th>
      <th>인근 지하철 호선수</th>
      <th>...</th>
      <th>호선</th>
      <th>지하철도보(분)</th>
      <th>을지로</th>
      <th>강남</th>
      <th>초등학교거리(도보/분)</th>
      <th>중학교배정학군</th>
      <th>학군명</th>
      <th>평균</th>
      <th>특목고 진학률</th>
      <th>상위2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>63</th>
      <td>둔촌 현대수린나</td>
      <td>현대수린나아파트</td>
      <td>서울특별시</td>
      <td>강동구</td>
      <td>34.0</td>
      <td>0.0</td>
      <td>34.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>...</td>
      <td>9호선</td>
      <td>8.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 21 columns</p>
</div>




```python
# 데이터 1에 데이터2 (아파트이름 기준, 아파트명2 - 중학교배정학군) merge 하기

df_merge = pd.merge(df_seoul, df2_drop, how = 'left', on = '아파트이름')
df_merge.shape
```




    (1073, 26)




```python
# 아파트명2 기준으로 NA 있는 행 drop 
df_merge_drop = df_merge.dropna(subset = ['아파트명2'], axis = 0)
```


```python
# 1차로 저장하기

df_merge_drop.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver1.csv', index = False, encoding = 'utf-8-sig')
```

## 매매가 / 전세가 merge하기

### 매매가 데이터 전처리하기 


```python
# 매매 실거래가 데이터 불러오기
price = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_df_merge.csv')
```


```python
# 전용면적이 소숫점이고 국토교통부 실거래가 자료와 완전히 일치하지 않는 부분이 있음
# => 분양가 데이터와 국토교통부 데이터를 범주형으로 바꾸어 실거래가 매칭

def space_change(x):
    if x < 20 :
        return '20미만'
    elif x < 30 :
        return '20이상 30미만'
    elif x < 40 :
        return '30이상 40미만'
    elif x < 50 :
        return '40이상 50미만'
    elif x < 59 :
        return '50이상 59미만'
    elif x < 60 :
        return '59타입'
    elif x < 70 :
        return '60이상 70미만'
    elif x < 80 :
        return '70이상 80미만'
    elif x < 84 :
        return '80이상 84미만'
    elif x < 90 :
        return '84타입'
    elif x < 100 :
        return '90이상 100미만'
    elif x < 110 :
        return '100이상 110미만'
    elif x < 120 :
        return '110이상 120미만'
    elif x < 130 :
        return '120이상 130미만'
    elif x < 140 :
        return '130이상 140미만'
    elif x < 200 :
        return '140이상 200미만'
    else :
        '200 이상'
```


```python
# 연도별로 별도의 거래금액 컬럼 만들기

# 필요한 컬럼만 선택
price_1 = price[['단지명', '전용면적(㎡)', '계약년월', '거래금액(만원)']]

# 컬럼명 바꾸기
price_1.columns = ['아파트명2', '전용면적', '계약년월', '거래금액']
price_1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>거래금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201906</td>
      <td>134,500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201911</td>
      <td>160,000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>67.28</td>
      <td>201905</td>
      <td>124,000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201906</td>
      <td>141,000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201908</td>
      <td>155,000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 계약년월에서 '년' parse 하기
price_2 = price_1.copy()
price_2['거래연도'] = price_1['계약년월'].astype(str).str[:4].astype(int)
price_2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>거래금액</th>
      <th>거래연도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201906</td>
      <td>134,500</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201911</td>
      <td>160,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>67.28</td>
      <td>201905</td>
      <td>124,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201906</td>
      <td>141,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201908</td>
      <td>155,000</td>
      <td>2019</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 전용면적 분류 바꾸기
price_3 = price_2.copy()
price_3['전용면적_분류'] = price_2['전용면적'].apply(space_change)
price_3.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>거래금액</th>
      <th>거래연도</th>
      <th>전용면적_분류</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201906</td>
      <td>134,500</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201911</td>
      <td>160,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>67.28</td>
      <td>201905</td>
      <td>124,000</td>
      <td>2019</td>
      <td>60이상 70미만</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201906</td>
      <td>141,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포6차우성아파트1동~8동</td>
      <td>79.97</td>
      <td>201908</td>
      <td>155,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
  </tbody>
</table>
</div>




```python
# '거래금액' object => int 로 바꾸기

price_3['거래금액'] = price_2['거래금액'].str.replace(',', '').astype(int)
```


```python
# 아파트명, 거래연도, 전용면적_분류에 따라 거래금액 평균내기

price_group = price_3[['아파트명2', '거래금액', '거래연도', '전용면적_분류']].groupby(['아파트명2', '거래연도', '전용면적_분류']).mean().reset_index()
price_group
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>거래연도</th>
      <th>전용면적_분류</th>
      <th>거래금액</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(1-102)</td>
      <td>2019</td>
      <td>20이상 30미만</td>
      <td>7500.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(1-102)</td>
      <td>2019</td>
      <td>30이상 40미만</td>
      <td>8750.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(1101-1)</td>
      <td>2019</td>
      <td>20미만</td>
      <td>11581.250000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(1101-1)</td>
      <td>2020</td>
      <td>20미만</td>
      <td>12065.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(1101-1)</td>
      <td>2021</td>
      <td>20미만</td>
      <td>10915.384615</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39918</th>
      <td>힐튼빌리지2차</td>
      <td>2019</td>
      <td>140이상 200미만</td>
      <td>85000.000000</td>
    </tr>
    <tr>
      <th>39919</th>
      <td>힐튼빌리지2차</td>
      <td>2020</td>
      <td>140이상 200미만</td>
      <td>87500.000000</td>
    </tr>
    <tr>
      <th>39920</th>
      <td>힐튼빌리지2차</td>
      <td>2022</td>
      <td>140이상 200미만</td>
      <td>141000.000000</td>
    </tr>
    <tr>
      <th>39921</th>
      <td>힐하우스</td>
      <td>2020</td>
      <td>140이상 200미만</td>
      <td>118000.000000</td>
    </tr>
    <tr>
      <th>39922</th>
      <td>힐하우스</td>
      <td>2021</td>
      <td>140이상 200미만</td>
      <td>110000.000000</td>
    </tr>
  </tbody>
</table>
<p>39923 rows × 4 columns</p>
</div>




```python
price_group_wide = price_group.pivot(index = ['아파트명2', '전용면적_분류'], columns = '거래연도', values = '거래금액').reset_index()
price_group_wide
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>거래연도</th>
      <th>아파트명2</th>
      <th>전용면적_분류</th>
      <th>2019</th>
      <th>2020</th>
      <th>2021</th>
      <th>2022</th>
      <th>2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>(1-102)</td>
      <td>20이상 30미만</td>
      <td>7500.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(1-102)</td>
      <td>30이상 40미만</td>
      <td>8750.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(1101-1)</td>
      <td>20미만</td>
      <td>11581.25</td>
      <td>12065.0</td>
      <td>10915.384615</td>
      <td>11150.000000</td>
      <td>11350.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(1487-1)</td>
      <td>20미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>36764.444444</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(1487-1)</td>
      <td>20이상 30미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>42325.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>15041</th>
      <td>힐튼</td>
      <td>100이상 110미만</td>
      <td>43000.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15042</th>
      <td>힐튼</td>
      <td>60이상 70미만</td>
      <td>NaN</td>
      <td>29700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15043</th>
      <td>힐튼빌리지1차</td>
      <td>80이상 84미만</td>
      <td>NaN</td>
      <td>63000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15044</th>
      <td>힐튼빌리지2차</td>
      <td>140이상 200미만</td>
      <td>85000.00</td>
      <td>87500.0</td>
      <td>NaN</td>
      <td>141000.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15045</th>
      <td>힐하우스</td>
      <td>140이상 200미만</td>
      <td>NaN</td>
      <td>118000.0</td>
      <td>110000.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>15046 rows × 7 columns</p>
</div>



### 분양가 데이터 전처리


```python
# 컬럼 순서 조정 (아파트명_2 가 맨 앞으로)
df = df_merge_drop[['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대', '시공사',
       '입주예정월','시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
       '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
       '초등학교거리(도보/분)', '중학교배정학군']]
```


```python
# 분양가 데이터 공급 면적 numeric 으로 바꾸기
df_new = df.copy()
df_new['공급면적_2'] = df['공급면적'].str.replace('[A-Za-z]', '', regex=True).astype(float)
```


```python
# 분양가 데이터에 적용

df_new['전용면적_분류'] = df_new['공급면적_2'].apply(space_change)
df_new.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>...</th>
      <th>인근 지하철 호선수</th>
      <th>지하철역</th>
      <th>호선</th>
      <th>지하철도보(분)</th>
      <th>을지로</th>
      <th>강남</th>
      <th>초등학교거리(도보/분)</th>
      <th>중학교배정학군</th>
      <th>공급면적_2</th>
      <th>전용면적_분류</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>049.5000</td>
      <td>51,020</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>49.50</td>
      <td>40이상 50미만</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>055.2500</td>
      <td>56,870</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>55.25</td>
      <td>50이상 59미만</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9400A</td>
      <td>68,750</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>59.94</td>
      <td>59타입</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9800B</td>
      <td>69,270</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>59.98</td>
      <td>59타입</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>075.2000A</td>
      <td>71,830</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>1.0</td>
      <td>무악재역</td>
      <td>3호선</td>
      <td>3.0</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>75.20</td>
      <td>70이상 80미만</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



### 분양가 데이터와 매매가 데이터와 거래금액 merge 하기


```python
merge_2 = pd.merge(df_new, price_group_wide, how = 'left', on = ['아파트명2', '전용면적_분류'])
merge_2.reset_index(drop = True, inplace = True)
merge_2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>...</th>
      <th>강남</th>
      <th>초등학교거리(도보/분)</th>
      <th>중학교배정학군</th>
      <th>공급면적_2</th>
      <th>전용면적_분류</th>
      <th>2019</th>
      <th>2020</th>
      <th>2021</th>
      <th>2022</th>
      <th>2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>049.5000</td>
      <td>51,020</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>49.50</td>
      <td>40이상 50미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>055.2500</td>
      <td>56,870</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>55.25</td>
      <td>50이상 59미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>80100.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9400A</td>
      <td>68,750</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>59.94</td>
      <td>59타입</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100805.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9800B</td>
      <td>69,270</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>59.98</td>
      <td>59타입</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100805.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>075.2000A</td>
      <td>71,830</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45.0</td>
      <td>3</td>
      <td>서부3학교군</td>
      <td>75.20</td>
      <td>70이상 80미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 33 columns</p>
</div>




```python
merge_2.shape
```




    (484, 33)




```python
# 컬럼명 바꾸기 : 2019 => 매매_2019 (전세가도 연도별로 merge 해야 하므로..)

merge_2.columns = [       '아파트명2',        '아파트이름',         '공급위치',         '공급세대',
               '공급면적',         '공급금액',           '지역',         '주택구분',
              '분양/임대',          '시공사',        '입주예정월',            '시',
                  '구',          '세대수',      '소형평수세대수',      '중형평수세대수',
            '대형평수세대수',         '특이사항',   '인근 지하철 호선수',         '지하철역',
                 '호선',     '지하철도보(분)',          '을지로',           '강남',
       '초등학교거리(도보/분)',      '중학교배정학군',       '공급면적_2',      '전용면적_분류',
                 '매매_2019',           '매매_2020',           '매매_2021',           '매매_2022',
                 '매매_2023']
```

### 전세가 데이터 전처리 하기


```python
# 전 실거래가 데이터 불러오기
rent = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_rent_df_merge.csv')
```

    C:\Users\soyou\AppData\Local\Temp\ipykernel_25848\1637408972.py:2: DtypeWarning: Columns (10,17,18) have mixed types. Specify dtype option on import or set low_memory=False.
      rent = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_rent_df_merge.csv')
    


```python
rent.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>시군구</th>
      <th>번지</th>
      <th>본번</th>
      <th>부번</th>
      <th>단지명</th>
      <th>전월세구분</th>
      <th>전용면적(㎡)</th>
      <th>계약년월</th>
      <th>계약일</th>
      <th>보증금(만원)</th>
      <th>월세(만원)</th>
      <th>층</th>
      <th>건축년도</th>
      <th>도로명</th>
      <th>계약기간</th>
      <th>계약구분</th>
      <th>갱신요구권 사용</th>
      <th>종전계약 보증금 (만원)</th>
      <th>종전계약 월세 (만원)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서울특별시 강남구 개포동</td>
      <td>655-2</td>
      <td>655.0</td>
      <td>2.0</td>
      <td>개포2차현대아파트(220)</td>
      <td>월세</td>
      <td>77.75</td>
      <td>201901</td>
      <td>29</td>
      <td>36,000</td>
      <td>60</td>
      <td>8</td>
      <td>1988.0</td>
      <td>언주로 103</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서울특별시 강남구 개포동</td>
      <td>655-2</td>
      <td>655.0</td>
      <td>2.0</td>
      <td>개포2차현대아파트(220)</td>
      <td>전세</td>
      <td>77.75</td>
      <td>201903</td>
      <td>23</td>
      <td>50,000</td>
      <td>0</td>
      <td>9</td>
      <td>1988.0</td>
      <td>언주로 103</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서울특별시 강남구 개포동</td>
      <td>655-2</td>
      <td>655.0</td>
      <td>2.0</td>
      <td>개포2차현대아파트(220)</td>
      <td>전세</td>
      <td>77.75</td>
      <td>201904</td>
      <td>2</td>
      <td>50,000</td>
      <td>0</td>
      <td>5</td>
      <td>1988.0</td>
      <td>언주로 103</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서울특별시 강남구 개포동</td>
      <td>655-2</td>
      <td>655.0</td>
      <td>2.0</td>
      <td>개포2차현대아파트(220)</td>
      <td>전세</td>
      <td>77.75</td>
      <td>201907</td>
      <td>23</td>
      <td>60,000</td>
      <td>0</td>
      <td>4</td>
      <td>1988.0</td>
      <td>언주로 103</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서울특별시 강남구 개포동</td>
      <td>655-2</td>
      <td>655.0</td>
      <td>2.0</td>
      <td>개포2차현대아파트(220)</td>
      <td>전세</td>
      <td>77.75</td>
      <td>201908</td>
      <td>24</td>
      <td>50,000</td>
      <td>0</td>
      <td>9</td>
      <td>1988.0</td>
      <td>언주로 103</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 연도별로 별도의 거래금액 컬럼 만들기

# 필요한 컬럼만 선택
rent_1 = rent[['단지명', '전용면적(㎡)', '계약년월', '보증금(만원)']]

# 컬럼명 바꾸기
rent_1.columns = ['아파트명2', '전용면적', '계약년월', '보증금']
rent_1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>보증금</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201901</td>
      <td>36,000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201903</td>
      <td>50,000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201904</td>
      <td>50,000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201907</td>
      <td>60,000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201908</td>
      <td>50,000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 계약년월에서 '년' parse 하기
rent_2 = rent_1.copy()
rent_2['거래연도'] = rent_1['계약년월'].astype(str).str[:4].astype(int)
rent_2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>보증금</th>
      <th>거래연도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201901</td>
      <td>36,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201903</td>
      <td>50,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201904</td>
      <td>50,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201907</td>
      <td>60,000</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201908</td>
      <td>50,000</td>
      <td>2019</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 전용면적 분류 바꾸기
rent_2['전용면적_분류'] = rent_1['전용면적'].apply(space_change)
rent_2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>전용면적</th>
      <th>계약년월</th>
      <th>보증금</th>
      <th>거래연도</th>
      <th>전용면적_분류</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201901</td>
      <td>36,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>1</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201903</td>
      <td>50,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>2</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201904</td>
      <td>50,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>3</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201907</td>
      <td>60,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
    <tr>
      <th>4</th>
      <td>개포2차현대아파트(220)</td>
      <td>77.75</td>
      <td>201908</td>
      <td>50,000</td>
      <td>2019</td>
      <td>70이상 80미만</td>
    </tr>
  </tbody>
</table>
</div>




```python
# '보증금' object => int 로 바꾸기

rent_2['보증금'] = rent_1['보증금'].str.replace(',', '').astype(int)
```


```python
# 아파트명, 거래연도, 전용면적_분류에 따라 거래금액 평균내기

rent_group = rent_2[['아파트명2', '보증금', '거래연도', '전용면적_분류']].groupby(['아파트명2', '거래연도', '전용면적_분류']).mean().reset_index()
rent_group
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>거래연도</th>
      <th>전용면적_분류</th>
      <th>보증금</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>((740-23))</td>
      <td>2022</td>
      <td>30이상 40미만</td>
      <td>11350.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>((740-23))</td>
      <td>2023</td>
      <td>30이상 40미만</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(1-10)</td>
      <td>2019</td>
      <td>70이상 80미만</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(1-10)</td>
      <td>2020</td>
      <td>70이상 80미만</td>
      <td>1000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(1-10)</td>
      <td>2021</td>
      <td>70이상 80미만</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>64786</th>
      <td>힐튼빌리지2차</td>
      <td>2020</td>
      <td>140이상 200미만</td>
      <td>35000.0</td>
    </tr>
    <tr>
      <th>64787</th>
      <td>힐하우스</td>
      <td>2019</td>
      <td>140이상 200미만</td>
      <td>40000.0</td>
    </tr>
    <tr>
      <th>64788</th>
      <td>힐하우스</td>
      <td>2020</td>
      <td>140이상 200미만</td>
      <td>75000.0</td>
    </tr>
    <tr>
      <th>64789</th>
      <td>힐하우스</td>
      <td>2021</td>
      <td>140이상 200미만</td>
      <td>42000.0</td>
    </tr>
    <tr>
      <th>64790</th>
      <td>힐하우스</td>
      <td>2023</td>
      <td>140이상 200미만</td>
      <td>42000.0</td>
    </tr>
  </tbody>
</table>
<p>64791 rows × 4 columns</p>
</div>




```python
rent_group_wide = rent_group.pivot(index = ['아파트명2', '전용면적_분류'], columns = '거래연도', values = '보증금').reset_index()
rent_group_wide
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>거래연도</th>
      <th>아파트명2</th>
      <th>전용면적_분류</th>
      <th>2019</th>
      <th>2020</th>
      <th>2021</th>
      <th>2022</th>
      <th>2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>((740-23))</td>
      <td>30이상 40미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11350.0</td>
      <td>2000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>(1-10)</td>
      <td>70이상 80미만</td>
      <td>2000.0</td>
      <td>1000.0</td>
      <td>2000.0</td>
      <td>2000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>(1-102)</td>
      <td>20이상 30미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>(1-102)</td>
      <td>30이상 40미만</td>
      <td>5250.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>(1-102)</td>
      <td>59타입</td>
      <td>NaN</td>
      <td>15000.0</td>
      <td>NaN</td>
      <td>250.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18312</th>
      <td>힐튼</td>
      <td>100이상 110미만</td>
      <td>500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18313</th>
      <td>힐튼빌리지1차</td>
      <td>100이상 110미만</td>
      <td>11250.0</td>
      <td>45000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18314</th>
      <td>힐튼빌리지1차</td>
      <td>80이상 84미만</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45000.0</td>
      <td>2000.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18315</th>
      <td>힐튼빌리지2차</td>
      <td>140이상 200미만</td>
      <td>32500.0</td>
      <td>35000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18316</th>
      <td>힐하우스</td>
      <td>140이상 200미만</td>
      <td>40000.0</td>
      <td>75000.0</td>
      <td>42000.0</td>
      <td>NaN</td>
      <td>42000.0</td>
    </tr>
  </tbody>
</table>
<p>18317 rows × 7 columns</p>
</div>



### 전세가 데이터 merge 하기


```python
merge_3 = pd.merge(merge_2, rent_group_wide, how = 'left', on = ['아파트명2', '전용면적_분류'])
merge_3.reset_index(drop = True, inplace = True)
merge_3.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>...</th>
      <th>매매_2019</th>
      <th>매매_2020</th>
      <th>매매_2021</th>
      <th>매매_2022</th>
      <th>매매_2023</th>
      <th>2019</th>
      <th>2020</th>
      <th>2021</th>
      <th>2022</th>
      <th>2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>049.5000</td>
      <td>51,020</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>29405.000000</td>
      <td>26000.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>055.2500</td>
      <td>56,870</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>80100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45340.909091</td>
      <td>45875.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9400A</td>
      <td>68,750</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100805.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9800B</td>
      <td>69,270</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100805.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>075.2000A</td>
      <td>71,830</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>46592.592593</td>
      <td>45733.333333</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 38 columns</p>
</div>




```python
merge_3.shape
```




    (484, 38)




```python
merge_3.columns
```




    Index([       '아파트명2',        '아파트이름',         '공급위치',         '공급세대',
                   '공급면적',         '공급금액',           '지역',         '주택구분',
                  '분양/임대',          '시공사',        '입주예정월',            '시',
                      '구',          '세대수',      '소형평수세대수',      '중형평수세대수',
                '대형평수세대수',         '특이사항',   '인근 지하철 호선수',         '지하철역',
                     '호선',     '지하철도보(분)',          '을지로',           '강남',
           '초등학교거리(도보/분)',      '중학교배정학군',       '공급면적_2',      '전용면적_분류',
                '매매_2019',      '매매_2020',      '매매_2021',      '매매_2022',
                '매매_2023',           2019,           2020,           2021,
                     2022,           2023],
          dtype='object')




```python
# 컬럼명 바꾸기 : '2022' => '전세_2022'

merge_3.columns = [       '아파트명2',        '아파트이름',         '공급위치',         '공급세대',
               '공급면적',         '공급금액',           '지역',         '주택구분',
              '분양/임대',          '시공사',        '입주예정월',            '시',
                  '구',          '세대수',      '소형평수세대수',      '중형평수세대수',
            '대형평수세대수',         '특이사항',   '인근 지하철 호선수',         '지하철역',
                 '호선',     '지하철도보(분)',          '을지로',           '강남',
       '초등학교거리(도보/분)',      '중학교배정학군',       '공급면적_2',      '전용면적_분류',
            '매매_2019',      '매매_2020',      '매매_2021',      '매매_2022',
            '매매_2023',           '전세_2019',           '전세_2020',           '전세_2021',
                 '전세_2022',           '전세_2023']
```

### 전세가 비율 계산


```python
merge_3_1 = merge_3.copy()
merge_3_1['전세가율_2019'] = merge_3['전세_2019'] / merge_3['매매_2019']
merge_3_1['전세가율_2020'] = merge_3['전세_2020'] / merge_3['매매_2020']
merge_3_1['전세가율_2021'] = merge_3['전세_2021'] / merge_3['매매_2021']
merge_3_1['전세가율_2022'] = merge_3['전세_2022'] / merge_3['매매_2022']
merge_3_1['전세가율_2023'] = merge_3['전세_2023'] / merge_3['매매_2023']
```


```python
merge_3_1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>...</th>
      <th>전세_2019</th>
      <th>전세_2020</th>
      <th>전세_2021</th>
      <th>전세_2022</th>
      <th>전세_2023</th>
      <th>전세가율_2019</th>
      <th>전세가율_2020</th>
      <th>전세가율_2021</th>
      <th>전세가율_2022</th>
      <th>전세가율_2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>049.5000</td>
      <td>51,020</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>29405.000000</td>
      <td>26000.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>055.2500</td>
      <td>56,870</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45340.909091</td>
      <td>45875.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.572722</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9400A</td>
      <td>68,750</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.373358</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9800B</td>
      <td>69,270</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.373358</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>075.2000A</td>
      <td>71,830</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>46592.592593</td>
      <td>45733.333333</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 43 columns</p>
</div>



### 면적별 세대수 비율 계산


```python
merge_3_1.columns
```




    Index(['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대',
           '시공사', '입주예정월', '시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
           '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
           '초등학교거리(도보/분)', '중학교배정학군', '공급면적_2', '전용면적_분류', '매매_2019', '매매_2020',
           '매매_2021', '매매_2022', '매매_2023', '전세_2019', '전세_2020', '전세_2021',
           '전세_2022', '전세_2023', '전세가율_2019', '전세가율_2020', '전세가율_2021',
           '전세가율_2022', '전세가율_2023'],
          dtype='object')




```python
merge_3_1['소형평수비중'] = merge_3['소형평수세대수'] / merge_3['세대수']
merge_3_1['중형평수비중'] = merge_3['중형평수세대수'] / merge_3['세대수']
merge_3_1['대형평수비중'] = merge_3['대형평수세대수'] / merge_3['세대수']
```


```python
merge_3_1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>아파트명2</th>
      <th>아파트이름</th>
      <th>공급위치</th>
      <th>공급세대</th>
      <th>공급면적</th>
      <th>공급금액</th>
      <th>지역</th>
      <th>주택구분</th>
      <th>분양/임대</th>
      <th>시공사</th>
      <th>...</th>
      <th>전세_2022</th>
      <th>전세_2023</th>
      <th>전세가율_2019</th>
      <th>전세가율_2020</th>
      <th>전세가율_2021</th>
      <th>전세가율_2022</th>
      <th>전세가율_2023</th>
      <th>소형평수비중</th>
      <th>중형평수비중</th>
      <th>대형평수비중</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>049.5000</td>
      <td>51,020</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>29405.000000</td>
      <td>26000.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.652644</td>
      <td>0.328125</td>
      <td>0.019231</td>
    </tr>
    <tr>
      <th>1</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>055.2500</td>
      <td>56,870</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>45340.909091</td>
      <td>45875.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.572722</td>
      <td>0.652644</td>
      <td>0.328125</td>
      <td>0.019231</td>
    </tr>
    <tr>
      <th>2</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9400A</td>
      <td>68,750</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.373358</td>
      <td>0.652644</td>
      <td>0.328125</td>
      <td>0.019231</td>
    </tr>
    <tr>
      <th>3</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>059.9800B</td>
      <td>69,270</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>37197.530864</td>
      <td>37636.363636</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.373358</td>
      <td>0.652644</td>
      <td>0.328125</td>
      <td>0.019231</td>
    </tr>
    <tr>
      <th>4</th>
      <td>서대문푸르지오센트럴파크</td>
      <td>서대문　푸르지오　센트럴파크（서울）</td>
      <td>서울특별시　서대문구　홍제동　５７－５번지　일대</td>
      <td>320세대</td>
      <td>075.2000A</td>
      <td>71,830</td>
      <td>서울</td>
      <td>민영</td>
      <td>분양주택</td>
      <td>(주)대우건설</td>
      <td>...</td>
      <td>46592.592593</td>
      <td>45733.333333</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.652644</td>
      <td>0.328125</td>
      <td>0.019231</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 46 columns</p>
</div>



## 지하철 정량화

### 1. 노선별 승하차총객수 계산


```python
merge_3['호선'].unique()
```




    array(['3호선', '5호선', '4호선', '9호선', '6호선', nan, '2호선', '7호선', '경의중앙선',
           '1호선', '수인분당선', '신림선', '우이신설선'], dtype=object)




```python
subway = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\CARD_SUBWAY_MONTH_202306.csv', index_col = False) 
# index_col = False : not to use the first column as the index
subway.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>사용일자</th>
      <th>노선명</th>
      <th>역명</th>
      <th>승차총승객수</th>
      <th>하차총승객수</th>
      <th>등록일자</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20230601</td>
      <td>분당선</td>
      <td>오리</td>
      <td>12873</td>
      <td>10868</td>
      <td>20230604</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20230601</td>
      <td>분당선</td>
      <td>이매</td>
      <td>7079</td>
      <td>6313</td>
      <td>20230604</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20230601</td>
      <td>분당선</td>
      <td>정자</td>
      <td>20381</td>
      <td>21369</td>
      <td>20230604</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20230601</td>
      <td>경의선</td>
      <td>서울역</td>
      <td>5541</td>
      <td>6880</td>
      <td>20230604</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20230601</td>
      <td>분당선</td>
      <td>보정</td>
      <td>3232</td>
      <td>2804</td>
      <td>20230604</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 하차 승차 총객수 합치기
subway1 = subway.copy()
subway1['승하차총객수'] = subway['승차총승객수'] + subway['하차총승객수']
```


```python
# 9호선과 9호선 2~3단계  => 9호선으로 통일 / 수인선과 분당선 => '수인분당선'으로 통일 / 경의선과 중앙성 => '경의중앙선'으로 통일

subway1.loc[subway1['노선명'] == '9호선2~3단계', '노선명'] = '9호선'
subway1.loc[subway1['노선명'] == '수인선', '노선명'] = '수인분당선'
subway1.loc[subway1['노선명'] == '분당선', '노선명'] = '수인분당선'
subway1.loc[subway1['노선명'] == '경의선', '노선명'] = '경의중앙선'
subway1.loc[subway1['노선명'] == '중앙선', '노선명'] = '경의중앙선'
```


```python
subway_group = subway1[['노선명', '승하차총객수']].groupby('노선명').mean().reset_index()
subway_group.sort_values(by = '승하차총객수', ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>노선명</th>
      <th>승하차총객수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2호선</td>
      <td>54346.436667</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1호선</td>
      <td>46590.470000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4호선</td>
      <td>38467.888462</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3호선</td>
      <td>30166.200787</td>
    </tr>
    <tr>
      <th>13</th>
      <td>경인선</td>
      <td>27035.565000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7호선</td>
      <td>26842.727057</td>
    </tr>
    <tr>
      <th>16</th>
      <td>과천선</td>
      <td>25810.308333</td>
    </tr>
    <tr>
      <th>10</th>
      <td>경부선</td>
      <td>23072.849573</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5호선</td>
      <td>22360.652381</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8호선</td>
      <td>20522.801852</td>
    </tr>
    <tr>
      <th>21</th>
      <td>일산선</td>
      <td>20000.180645</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9호선</td>
      <td>19952.466667</td>
    </tr>
    <tr>
      <th>19</th>
      <td>안산선</td>
      <td>18404.717949</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6호선</td>
      <td>17358.947043</td>
    </tr>
    <tr>
      <th>15</th>
      <td>공항철도 1호선</td>
      <td>16918.354762</td>
    </tr>
    <tr>
      <th>17</th>
      <td>수인분당선</td>
      <td>16331.093156</td>
    </tr>
    <tr>
      <th>11</th>
      <td>경원선</td>
      <td>13554.480638</td>
    </tr>
    <tr>
      <th>12</th>
      <td>경의중앙선</td>
      <td>8450.361246</td>
    </tr>
    <tr>
      <th>18</th>
      <td>신림선</td>
      <td>7548.375758</td>
    </tr>
    <tr>
      <th>20</th>
      <td>우이신설선</td>
      <td>6865.943590</td>
    </tr>
    <tr>
      <th>9</th>
      <td>경강선</td>
      <td>5832.684848</td>
    </tr>
    <tr>
      <th>22</th>
      <td>장항선</td>
      <td>4815.747619</td>
    </tr>
    <tr>
      <th>14</th>
      <td>경춘선</td>
      <td>4165.622807</td>
    </tr>
  </tbody>
</table>
</div>



### 2. 역별 총승하차객수 계산


```python
# '역명'에 '역' 붙이기 
subway1['역명'] = subway['역명'] + '역'
```


```python
# 역 기준으로 groupby
subway_group2 = subway1[['역명', '승하차총객수']].groupby('역명').mean().reset_index()
subway_group2.sort_values(by = '역명', ascending = False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>역명</th>
      <th>승하차총객수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>523</th>
      <td>흑석(중앙대입구)역</td>
      <td>18582.600000</td>
    </tr>
    <tr>
      <th>522</th>
      <td>효창공원앞역</td>
      <td>10219.066667</td>
    </tr>
    <tr>
      <th>521</th>
      <td>회현(남대문시장)역</td>
      <td>53233.900000</td>
    </tr>
    <tr>
      <th>520</th>
      <td>회룡역</td>
      <td>25407.933333</td>
    </tr>
    <tr>
      <th>519</th>
      <td>회기역</td>
      <td>52245.366667</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>가양역</td>
      <td>41755.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>가산디지털단지역</td>
      <td>55347.450000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>가락시장역</td>
      <td>16284.166667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>가능역</td>
      <td>12950.100000</td>
    </tr>
    <tr>
      <th>0</th>
      <td>4.19민주묘지역</td>
      <td>6786.633333</td>
    </tr>
  </tbody>
</table>
<p>524 rows × 2 columns</p>
</div>



### 3. 분양가 데이터에 merge 하기


```python
merge_3.columns
```




    Index(['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대',
           '시공사', '입주예정월', '시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
           '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
           '초등학교거리(도보/분)', '중학교배정학군', '공급면적_2', '전용면적_분류', '매매_2019', '매매_2020',
           '매매_2021', '매매_2022', '매매_2023', '전세_2019', '전세_2020', '전세_2021',
           '전세_2022', '전세_2023'],
          dtype='object')




```python
subway_group.columns = ['호선', '승하차총객수']
```


```python
# 노선기준 merge 

merge_4 = pd.merge(merge_3_1, subway_group, how = 'left', on = '호선')
merge_4.shape
```




    (484, 47)




```python
# 지하철 기준 merge 
# merge_4에 역 이름 잘못된거 바로 잡기 (답심리 => 답십리 , 중앙보훈 => 중앙보훈병원)

merge_4.loc[merge_4['지하철역'] == '답심리역', '지하철역'] = "답십리역"
merge_4.loc[merge_4['지하철역'] == '중앙보훈역', '지하철역'] = "중앙보훈병원역"
merge_4.loc[merge_4['지하철역'] == '총신대입구역', '지하철역'] = "총신대입구(이수)역"
merge_4.loc[merge_4['지하철역'] == '아차산역', '지하철역'] = "아차산(어린이대공원후문)역"
merge_4.loc[merge_4['지하철역'] == '화랑대역', '지하철역'] = "화랑대(서울여대입구)역"
merge_4.loc[merge_4['지하철역'] == '새절역', '지하철역'] = "새절(신사)역"
merge_4.loc[merge_4['지하철역'] == '어린이대공원역', '지하철역'] = "어린이대공원(세종대)역"
merge_4.loc[merge_4['지하철역'] == '남부터미널역', '지하철역'] = "남부터미널(예술의전당)역"
merge_4.loc[merge_4['지하철역'] == '교대역', '지하철역'] = "교대(법원.검찰청)역"
merge_4.loc[merge_4['지하철역'] == '고속터미너역', '지하철역'] = "고속터미널역"
merge_4.loc[merge_4['지하철역'] == '수유역', '지하철역'] = "수유(강북구청)역"
```


```python
subway_group2.columns = ['지하철역', '승하차총객수']
merge_5 = pd.merge(merge_4, subway_group2, how = 'left', on = '지하철역')
```


```python
merge_5.shape
```




    (484, 48)




```python
merge_5.columns
```




    Index(['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대',
           '시공사', '입주예정월', '시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
           '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
           '초등학교거리(도보/분)', '중학교배정학군', '공급면적_2', '전용면적_분류', '매매_2019', '매매_2020',
           '매매_2021', '매매_2022', '매매_2023', '전세_2019', '전세_2020', '전세_2021',
           '전세_2022', '전세_2023', '전세가율_2019', '전세가율_2020', '전세가율_2021',
           '전세가율_2022', '전세가율_2023', '소형평수비중', '중형평수비중', '대형평수비중', '승하차총객수_x',
           '승하차총객수_y'],
          dtype='object')




```python
merge_5.columns = ['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대',
       '시공사', '입주예정월', '시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
       '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
       '초등학교거리(도보/분)', '중학교배정학군', '공급면적_2', '전용면적_분류', '매매_2019', '매매_2020',
       '매매_2021', '매매_2022', '매매_2023', '전세_2019', '전세_2020', '전세_2021',
       '전세_2022', '전세_2023', '전세가율_2019', '전세가율_2020', '전세가율_2021',
       '전세가율_2022', '전세가율_2023', '소형평수비중', '중형평수비중', '대형평수비중', '승하차총객수_노선기준', '승하차총객수_역기준']
```


```python
# merge 안된거 있는지 확인
merge_5[['지하철역', '승하차총객수_역기준']].loc[merge_5['승하차총객수_역기준'].isna()]['지하철역'].unique()
```




    array([nan], dtype=object)




```python
# 최종파일 저장

merge_5.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver2.csv', index = False, encoding = 'utf-8-sig')
```

## 중학교 학군 score 다시 결합


```python
df = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver2.csv')
```


```python
school_score.columns = ['중학교배정학군', '평균', '특목고 진학률', '상위']
```


```python
df.columns
```




    Index(['아파트명2', '아파트이름', '공급위치', '공급세대', '공급면적', '공급금액', '지역', '주택구분', '분양/임대',
           '시공사', '입주예정월', '시', '구', '세대수', '소형평수세대수', '중형평수세대수', '대형평수세대수',
           '특이사항', '인근 지하철 호선수', '지하철역', '호선', '지하철도보(분)', '을지로', '강남',
           '초등학교거리(도보/분)', '중학교배정학군', '공급면적_2', '전용면적_분류', '매매_2019', '매매_2020',
           '매매_2021', '매매_2022', '매매_2023', '전세_2019', '전세_2020', '전세_2021',
           '전세_2022', '전세_2023', '전세가율_2019', '전세가율_2020', '전세가율_2021',
           '전세가율_2022', '전세가율_2023', '소형평수비중', '중형평수비중', '대형평수비중', '승하차총객수_노선기준',
           '승하차총객수_역기준'],
          dtype='object')




```python
merge = pd.merge(df, school_score, how = 'left', on = '중학교배정학군')
```


```python
merge[['중학교배정학군', '평균', '특목고 진학률', '상위']].isna().sum()
```




    중학교배정학군    4
    평균         4
    특목고 진학률    4
    상위         4
    dtype: int64




```python
merge.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver2.csv', index = False, encoding = 'utf-8-sig')
```

## 아파트 브랜드 여부 추가


```python
# 아파트 브랜드 데이터 불러오기
brand = pd.read_excel(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\아파트브랜드.xlsx')
```


```python
merge_brand = pd.merge(merge, brand, how = 'left', on = '아파트명2')
```


```python
merge_brand.shape
```




    (484, 54)




```python
merge_brand.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver2.csv', index = False, encoding = 'utf-8-sig')
```

## 둔촌 현대 수린나 정보 추가


```python
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '을지로'] = 55
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '강남'] = 45
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '초등학교거리(도보/분)'] = 6
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '중학교배정학군'] = '강동송파1학교군'
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '평균'] = 0.804286
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '특목고 진학률'] = 0.009714
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '상위'] = 53.875000
merge_brand.loc[merge_brand['아파트명2'] == '현대수린나아파트', '인근 지하철 호선수'] = 2
```


```python
merge_brand.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_ver2.csv', index = False, encoding = 'utf-8-sig')
```

## 비용 모델링 추가


```python
df = pd.read_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_forR.csv')
```


```python
# 취득세
def acq_tax(x) :
    if x <= 60000 :
        return(x * 0.01)
    elif x <= 90000 :
        return(x * ((x/10000) * 2/3 - 3)/100)
    else :
        return(x * 0.03)

# 농어촌특별세
def size_tax(x) :
    if x['공급면적_2']> 85:
        return(x['공급금액'] * 0.002)
    else :
        return(x['공급금액'] * 0)

# 지방교육세
def edu_tax(x) :
    if x <= 60000 :
        return(x * 0.001)
    elif x <= 90000 :
        return((x * ((x/10000) * 2/3 - 3)/100) / 10)
    else :
        return(x * 0.003)
```


```python
# 구매비용_비투기과열지구

def non_spec(x) :
    if x <= 90000 :
        return(x * 0.5 + x * 0.5 * 0.0429 * 2)
    else :
        return(x * 0.7 + x * 0.3 * 0.0429 * 2)

# 구매비용_투기과열지구
def spec(x) :
    if x <= 90000:
        return(x * 0.6 + x * 0.4 * 0.0429 * 2)
    elif x <= 150000:
        return(x * 0.8 + x * 0.2 * 0.0429 * 2)
    else :
        return(x)
```


```python
df_copy = df.copy()

# 세금계산
df_copy['취득세']  = df['공급금액'].apply(acq_tax)
df_copy['농어촌특별세']  = df.apply(size_tax, axis = 1)
df_copy['지방교육세'] = df['공급금액'].apply(edu_tax)

# LTV에 따른 아파트 구매비용 계산
df_copy['비투기과열지구'] = df['공급금액'].apply(non_spec)
df_copy['투기과열지구'] = df['공급금액'].apply(spec)
```


```python
# 투기과열 지구 지정 확률 불러오기
prob = pd.read_excel(r'C:\Users\soyou\Dropbox\대체보고서\투기과열지구확률.xlsx')
prob.columns = ['구', '투기과열_prob']
```


```python
merge = pd.merge(df_copy, prob, how = 'left', on = '구')
```


```python
# 가중평균 구매비용
merge['weighted_cost'] = (merge['투기과열지구'] * merge['투기과열_prob']) + (merge['비투기과열지구'] * (1 - merge['투기과열_prob']))
# 세금
merge['tax'] = merge['취득세'] + merge['농어촌특별세']  + merge['지방교육세']
```


```python
# 총비용
merge['total_cost'] = merge['weighted_cost'] + merge['tax']
```


```python
merge['total_cost']
```




    0       92746.732755
    1       97078.764311
    2      144652.957170
    3       54860.336069
    4       28174.226179
               ...      
    184     41858.396514
    185     36191.018954
    186     46433.083557
    187     74988.761868
    188     79751.327575
    Name: total_cost, Length: 189, dtype: float64




```python
# 저장하기
merge.to_csv(r'C:\Users\soyou\Dropbox\대체보고서\분양 데이터\merge\seoul_merge_forR.csv', index = False, encoding = 'utf-8-sig')
```


```python
# histogram : 매매_분양가 gap NA 제거하기 전
import seaborn as sns
import matplotlib.pyplot as plt
sns.histplot(data=merge, x="total_cost", stat = "density", kde=True, bins = 30)
plt.show()
```


    
![png](output_108_0.png)
    



```python
# histogram : 매매_분양가 gap NA 제거 후
merge2 = merge[merge['매매_분양가gap'].isna() == False]
sns.histplot(data=merge2, x="total_cost", stat = "density", kde=True, bins = 30)
plt.show()
```


    
![png](output_109_0.png)
    



```python
merge2['total_cost_log'] = np.log(merge2['total_cost'])
```

    C:\Users\soyou\AppData\Local\Temp\ipykernel_27516\2437207823.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      merge2['total_cost_log'] = np.log(merge2['total_cost'])
    


```python
sns.histplot(data=merge2, x="total_cost_log", stat = "density", kde=True, bins = 30)
plt.show()
```


    
![png](output_111_0.png)
    

