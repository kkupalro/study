```python
%matplotlib inline
```

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from matplotlib import font_manager,rc
```

```python
# 한글 깨짐 방지 작업
font_info="c:/windows/Fonts/malgun.ttf"
font_name=font_manager.FontProperties(fname=font_info).get_name()
rc('font',family=font_name)
```

```python
# 파일이 utf8 형식으로저장되었기때문에 utf8 형식으로 인코딩해야 에러안뜸
data_2012_2014 = pd.read_csv('data/accident_2012_2014.csv', encoding = 'utf8')
data_2015 = pd.read_csv('data/accident_2015.csv', encoding = 'utf8')
data_2016 = pd.read_csv('data/accident_2016.csv', encoding = 'utf8')
data = pd.concat([data_2012_2014, data_2015, data_2016], ignore_index=True)
data.head(5)
```

```python
data.info()
```

# 1. 지역별 사망자수 분석

```python
# 시별로 교통사고사망자 수를 확인하기 위해 그룹화 작업을 실행하는 d1 객체 생성
d1 = data.groupby(['발생지시도'])
```

```python
# 사망자 수 합계를 확인 경기 지역 사망자수가 제일 많다는것을 알수있음
d1['사망자수'].sum()
```

```python
# 사망자수가 많은 경기지역을 대상으로 다시 분석하기 위해 필터링하여 d1 객체를 생성
d1=data[data.발생지시도=='경기']
d1.head()
```

```python
# 경기지역의 시,군별 그룹화 작업을 실행하는 da1 객체 생성
da1 = d1.groupby(['발생지시군구'])
```

```python
#사망자 수 합계를 요약하여 da2 객체 생성
da2=da1['사망자수'].sum()
da2
```

```python
# 결과를 오름차순으로 정렬함
result=da2.sort_values(ascending=True).tail(5)
result
```

```python
# 결과를 파이차트로 시각화함.
result.plot(kind='pie',title='2012-2016 경기도내 교통사망사고 빈발지역')
```

```python
# matplotlib.pyplot 이용하여 파이차트를 작성함
c=['red', 'orange', 'yellow', 'green', 'blue'] # 색상을 빨 ~파 순으로 지정함
result.plot(kind='pie',title='2012-2016 경기도내 교통사망사고 빈발지역')
result=plt.pie(result,colors=c,autopct='%.2f') # 차지비율을 소숫점 2자리까지 출력
result=plt.title('2012-2016 경기도내 교통사망사고 빈발지역')
```

# 2. 요일별/발생지시도별 교통사고 분석

```python
%matplotlib inline
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from matplotlib import font_manager,rc
# 한글 깨짐 방지 작업
font_info="c:/windows/Fonts/malgun.ttf"
font_name=font_manager.FontProperties(fname=font_info).get_name()
rc('font',family=font_name)
```

```python
# 교차분석 실행하여 요일별 발생지시도별 데이터 건수를 계산하기 위하여 d_pv 객체 실행
d_pv=pd.crosstab(data.요일,data.발생지시도)
d_pv=d_pv.reindex(['월','화','수','목','금','토','일', '' ]) # 인덱스위치를 월~일로 수정후 발생지시도가 겹쳐지기 때문에 공백인덱스를 추가함
d_pv
```

```python
# 각행의 합이 1이 되도록 비율로 설정한 후 그 내용을 누적 막대형 차트로 시각화함
result=d_pv.div(d_pv.sum(1).astype(float),axis=0)
result.plot.bar(stacked=True,figsize=(8, 5), title='2012-2016 지역/요일 교통사고 발생건수')
plt.show()
```

# 3. folium 라이브러리를 이용한 지도표시

```python
# 설치방법 
# Anaconda Prompt 창에 conda install -c conda-forge folium
# 혹은 Prompt에 install folium 
import folium
import pandas as pd
```

```python
font_info="c:/windows/Fonts/malgun.ttf"
font_name=font_manager.FontProperties(fname=font_info).get_name()
rc('font',family=font_name)
```

```python
data_2012_2014 = pd.read_csv('data/accident_2012_2014.csv', encoding = 'utf8')
data_2015 = pd.read_csv('data/accident_2015.csv', encoding = 'utf8')
data_2016 = pd.read_csv('data/accident_2016.csv', encoding = 'utf8')
data = pd.concat([data_2012_2014, data_2015, data_2016], ignore_index=True)
# 2012 ~2016 까지의 교통사고사망정보 csv 파일 합치기
```

```python
# 시흥시를 분석하기위해 경기지역을 대상으로 필터링하여 data2 객체를 생성
data2=data[data.발생지시도=='경기']
```

```python
# 시흥시를 대상으로 필터링하여 data2 객체를 다시 생성
data2=data2[data2.발생지시군구=="시흥시"]
data2.head()
```

```python
data2.info()
```

```python
# 데이터가 너무 많기때문에 사상자수가 3명이상인 경우에만 분석하기위하여 필터링함
data2=data2[(data2.사상자수>=3)]
data2.info()
```

```python
# folium 라이브러리를 사용
# zoom_start 는 줌인으로 초기화면 크기를 지정,
# 1일경우 전세계가 다보이고 높아질수록 더 자세하게 보임
# 좌표 37.38139, 126.80278 은 시흥시 표준좌표
# https://kor.timegenie.com/latitude_longitude/country/kr (대한민국 위도 경도 사이트)

m=folium.Map(location=[37.38139,126.80278],zoom_start=13)
```

```python
# 마커를 생성 위도 경도를 받아 마커의 위치를 표시하고 사고유형을 마커를 클릭할시
# 보여줄 문자열로 전달하고 생성한 folium 객체에 add_to 함수를 사용하여 간단하게 마커를
# 생성할수있음
for lat,lon,name in zip(data2['위도'], data2['경도'], data2['사고유형']):
    folium.Marker(location=[lat,lon],popup=name).add_to(m)
```

```python
# 생성된 지도를 상위 디렉토리 html안에 test.html 파일로 저장함
# 같은경로에 test.html 파일을 만들어도 되는데 따로 html 디렉토리를 생성해서 저장함.
# 상위디렉토리 html 이 없으면 오류가 남.
# m.save("test.html") # 디렉토리가 없을경우 이렇게 저장
m.save("html/test.html")
```

```python
# 쥬피터노트북을 크롬으로 사용할경우 보이지만 인터넷 익스플로우로 사용할 경우 보이지않음
m
```

```python
# 같은경로내에 html 디렉토리가 없을경우 실행
# %%HTML
# <iframe width="100%" height="350" src="test.html"></iframe>
```

```python
%%HTML
<iframe width="100%" height="350" src="html/test.html"></iframe>
```

```python
# 인터넷익스플로우일경우 보이지않기때문에 html 문서를 열어서 볼수있음
```

# 4. seaborn 라이브러리를 응용해서 서울시 교통사고 발생지역 시각화

```python
# 설치방법 conda install -c conda-forge folium
# 서울시 교통사고현황 통계자료에 대한 확인
# heatmap 을 사용하기 위하여 seaborn 을 import함
import folium
import seaborn as sns

font_info="c:/windows/Fonts/malgun.ttf"
font_name=font_manager.FontProperties(fname=font_info).get_name()
rc('font',family=font_name)
```

```python
data.info()
```

```python
# 서울시를 대상으로 분석하기위해 필터링함
data=data[data.발생지시도=='서울']
```

```python
# pivot_table을 사용하여 구별로 데이터를 쉽게 모아볼수있고 각 칼럼의 합을 구함
guDF = pd.pivot_table(data, index='발생지시군구', aggfunc=np.sum)
guDF.head()
# 모든컬럼의값이 더해졌기때문에 필요없는 칼럼을 제거해야함
```

```python
# 사상자수와 각각의 수를 이용하여 퍼센트를 구하고 필요없는 데이터를 지우는 작업을 수행

guDF['경상자율'] = guDF['경상자수']/guDF['사상자수']*100
guDF['부상신고자율'] = guDF['부상신고자수']/guDF['사상자수']*100
guDF['사망자율'] = guDF['사망자수']/guDF['사상자수']*100


del guDF['경도']
del guDF['위도']
del guDF['발생년']
del guDF['발생년월일시']
del guDF['발생분']
del guDF['발생위치X_UTMK']
del guDF['발생위치Y_UTMK']
```

```python
guDF.head()
```

```python
# 칼럼의 글자수가 길어서 표가 넒어지기때문에 칼럼의 이름을 간략화함
guDF.rename(columns = {'경상자수':'경상', 
                       '부상신고자수':'부상', 
                       '사망자수':'사망', 
                       '사상자수':'사상', 
                       '중상자수':'중상'}, inplace=True)
```

```python
# 표의 크기가 줄어들은걸 볼수있음
guDF.head()
```

### (2016년도 전국 인구수 데이터를 가져와서 가공)

```python
korDF = pd.read_csv('data/pop_kor.csv', encoding = 'ANSI')
# http://kosis.kr/index/index.do
# 다운로드하는법 
# (1) kOSIS국가통계포털사이트 접속 
# (2) 통계시각화콘텐츠에 인구로 보는 대한민국 클릭
# (3) 숫자로 보는 인구에 인구와 가구 클릭
# (4) 시군구별 순위 클릭후 통계표 더보기 클릭후 CSV 파일로 다운로드
```

```python
# 구조는 아래와 같음
korDF.head()
```

```python
# 각 칼럼의 이름을 보기쉽게 변경함
korDF.rename(columns = {'행정구역별(시군구)(1)':'시도', 
                       '행정구역별(시군구)(2)':'구별',
                      '2016':'인구수'}, inplace=True)
```

```python
korDF.head()
```

```python
# 서울특별시를 기준으로 필터링함
korDF=korDF[korDF.시도=='서울특별시']
korDF.head()
```

```python
# 0번행에 소계와 모든 인구수가합쳐진값은 필요없기때문에 제거함
korDF=korDF.drop(0)
```

```python
korDF.head()
# 0번행이 제거됨
```

```python
del korDF['시도']
# 서울특별시로 필터링했기때문에 시도도 필요없어서 제거함
```

```python
korDF.to_csv("data/pop_seoul.csv", index=False)
# 가공된 데이터를 상위디렉토리인 data디렉토리에 pop_seoul.csv 로 저장힘
```

### (가공된 데이터를 가져와 기존 데이터프레임과 합침)

```python
# 가공하여 저장한 서울 구별 인구수 데이터를 가져와 사용함.
# 구조는 아래와 같음.
popDF = pd.read_csv('data/pop_seoul.csv', encoding='UTF-8', index_col='구별')
popDF.head()
```

```python
# 교통사고통계데이터와 서울시 구별인구수 데이터의 index 값이 같기때문에 join 명령으로
# 데이터를 합침
guDF = guDF.join(popDF)
```

```python
# 합쳐진걸 확인 가능함
guDF.head()
```

```python
# 합쳐진 데이터가지고 사망자율로 내림차순정렬하여 순위를 매겨봄
guDF.sort_values(by='사망자율', ascending=False, inplace=True)
guDF.head()
```

```python
# 이제 그래프로 각 구별 현황을 확인하기위하여 작업을 수행함

target_col = ['경상', '부상', '사망', '사상', '중상']
weight_col = guDF[target_col].max()

accident_count_norm = guDF[target_col]/weight_col
accident_count_norm.head()
```

```python
# seaborn의 heatmap 을 사용함
# 사상자수를 사망수로 나누어서 교통사고 발생비율을 시각화
plt.figure(figsize = (10,10))
sns.heatmap(accident_count_norm.sort_values(by='사망', ascending=False), annot=True, fmt='f', linewidths=.5)
plt.title('사상자수(사망발생수로 정렬) - 각 항목별 최대값으로 나눠 정규화')
plt.show()
```

```python
# 단순히 교통사고 발생으로 분석하기에는 한계가있어서 인구수로 나눠서 인구대비
# 교통사고사망 발생비율로 시각화함

accident_ratio = accident_count_norm.div(guDF['인구수'], axis=0)*100000

plt.figure(figsize = (10,10))
sns.heatmap(accident_ratio.sort_values(by='사망', ascending=False), annot=True, fmt='f', linewidths=.5)
plt.title('교통사고 발생(사망발생수으로 정렬) - 각 항목을 정규화한 후 인구로 나눔')
plt.show()
```

```python
# 마지막으로 전체발생비율로 정렬하여 시각화함
accident_ratio['전체발생비율'] = accident_ratio.mean(axis=1)

plt.figure(figsize = (10,10))
sns.heatmap(accident_ratio.sort_values(by='전체발생비율', ascending=False), annot=True, fmt='f', linewidths=.5)
plt.title('교통사고 발생(전체발생비율로 정렬) - 각 항목을 정규화한 후 인구로 나눔')
plt.show()
```

# 5. Folium 라이브러리를 응용해서 데이터 합치기

```python
import json
import folium
import warnings
warnings.simplefilter(action = "ignore", category = FutureWarning)

geo_path = 'data/skorea_municipalities_geo_simple.json'
geo_str = json.load(open(geo_path, encoding='utf-8'))

# folium 지도에다가 서울 교통사고 발생수를 시각화하기위해서 서울 지도 데이터를 읽어옴
# 즉, 지도에 데이터를 표현하려고함
# https://github.com/southkorea/southkorea-maps/tree/master/gadm/json (한국 지도 데이터)
```

```python
geo_str # skorea_municipalities_geo_simple.josn 파일의 구조는 다음과 같음
```

```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)

map.choropleth(geo_data = geo_str,
               data = guDF['사망'],
               columns = [guDF.index, guDF['사망']],
               fill_color = 'YlGnBu', #PuRd, YlGnBu
               key_on = 'feature.id')
map.save("html/test2.html")
# folium 지도에다가 사망자율을 표시함
# 크롬에서는 객체를 입력하면 지도를 볼수있지만 인터넷 익스플로우에서는 html 문서에 저장만
# 가능하므로 따로 html 파일에 저장함
```

```python
map
```

```python
%%HTML
<iframe width="100%" height="350" src="html/test2.html"></iframe>
```

```python
# 서울의 각지역에 교통사고 사망수를 시각화함
# 영등포구랑 강서구가 높은걸 확인할수 있음
```

```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=11)

map.choropleth(geo_data = geo_str,
               data = accident_ratio['전체발생비율'],
               columns = [accident_ratio.index, accident_ratio['전체발생비율']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map.save("html/test3.html")
# 인구대비 사상자수로 계산한걸 합산한 전체발생비율로 확인함
# 서울역 근처에 발생비율이 가장 높음
```

```python
%%HTML
<iframe width="100%" height="350" src="html/test3.html"></iframe>
```

```python
# 뿐만아니라 경상, 부상, 사상, 중상 경상자율 ~ 사망자율까지 확인이 가능함 
```

# 전지역 교통사고 발생 분석 지도 시각화

```python
map = folium.Map(location=[37.5502, 126.982], zoom_start=7)

map.choropleth(geo_data = geo_str,
               data = accident_ratio['전체발생비율'],
               columns = [accident_ratio.index, accident_ratio['전체발생비율']],
               fill_color = 'PuRd', #PuRd, YlGnBu
               key_on = 'feature.id')
map.save("html/test4.html")
```

```python
map
```

```python
%%HTML
<iframe width="100%" height="350" src="html/test4.html"></iframe>
```

```python
# 위와 같이 전국을 한눈에 보기 어려움
```

```python
# 참고 http://nbviewer.jupyter.org/gist/hyeshik/cf9f3d7686e07eedbfda?revision=6
# ("버거 지수"는 진짜 도시의 발전 수준을 반영할까?)
# 서울시 교통사고현황에 대한 분석을 하였는데 좀 더 많은 데이터를 서울시 뿐만 아니라
# 전국규모로 분석하고싶었는데 Folium 같이 지리적으로 정확한 지도를 이용하면
# 정보전달력이 약해서 다양한 예제를 검색해 방법을 찾다가 한눈에 들어오는 예제를 찾음
import pandas as pd
import numpy as np

import platform
import matplotlib.pyplot as plt
```

```python
%matplotlib inline
```

```python
# 교통사고데이터 2012_2014년도부터 2016년도까지 하나로 합쳐서 사용함
data_2012_2014 = pd.read_csv('data/accident_2012_2014.csv', encoding = 'utf8')
data_2015 = pd.read_csv('data/accident_2015.csv', encoding = 'utf8')
data_2016 = pd.read_csv('data/accident_2016.csv', encoding = 'utf8')
data = pd.concat([data_2012_2014, data_2015, data_2016], ignore_index=False)
# data.head(5)
```

```python
cityDF = pd.pivot_table(data, index=['발생지시도','발생지시군구'], aggfunc=np.sum)
# 시에따른 구의 각 칼럼의 합을 구하기위해 pivot_table 을 사용함
```

```python
# 사상자수와 각각의 수를 이용하여 퍼센트를 구하고 필요없는 데이터를 지우는 작업을 수행

cityDF['경상자율'] = cityDF['경상자수']/cityDF['사상자수']*100
cityDF['부상신고자율'] = cityDF['부상신고자수']/cityDF['사상자수']*100
cityDF['사망자율'] = cityDF['사망자수']/cityDF['사상자수']*100

del cityDF['경도']
del cityDF['위도']
del cityDF['발생년']
del cityDF['발생년월일시']
del cityDF['발생분']
del cityDF['경상자수']
del cityDF['부상신고자수']
# del cityDF['사상자수']
del cityDF['중상자수']
del cityDF['발생위치X_UTMK']
del cityDF['발생위치Y_UTMK']
```

```python
cityDF.head()
```

```python
# pivot_table로 만든 데이터와 지도를 그리는데 필요한 데이터를 병합하기 위해
# multi_index를 변환하는 작업을 수행함
cityDF.reset_index(inplace=True)  

tmp_coloumns = [cityDF.columns.get_level_values(0)[n]
               for n in range(0,len(cityDF.columns.get_level_values(0)))]

cityDF.columns = tmp_coloumns

cityDF.head()
```

```python
# 데이터를 그리기위해 블록 지도 데이터를 읽어옴
# http://nbviewer.jupyter.org/gist/hyeshik/cf9f3d7686e07eedbfda?revision=6 (블록 지도 데이터)
# 그런다음 데이터를 합치기 위한 작업을 수행 
# draw_korea.csv 의 행정구역칼럼이 교통사고데이터 발생지시군구 칼럼이랑 일치하기때문에
# 별다른 데이터 가공없이 발생지시군구를 기준으로 합치기가 가능함
# 행정구역칼럼의 이름을 변경하고 필요없는 칼럼을 제거

draw_korea = pd.read_csv('data/data_draw_korea.csv', index_col=0, encoding='UTF-8')

draw_korea.rename(columns = {'행정구역':'발생지시군구'},inplace=True)
draw_korea['행정구역']=draw_korea['발생지시군구']
del draw_korea['인구수']
del draw_korea['면적']
del draw_korea['shortName']
# del draw_korea['광역시도']
# del draw_korea['행정구역']
```

```python
# draw_korea.csv 파일의 데이터는 아래와 같음
draw_korea.head()
```

```python
def drawKorea(targetData, blockedMap, d1, d2, cmapname):
    gamma = 0.75

    whitelabelmin = (max(blockedMap[targetData]) - min(blockedMap[targetData])) * 0.25 + min(blockedMap[targetData])

    datalabel = targetData

    vmin = min(blockedMap[targetData])
    vmax = max(blockedMap[targetData])

    # 시도간 경계 그림 데이터를 작성
    BORDER_LINES = [
        [(3, 2), (5, 2), (5, 3), (9, 3), (9, 1)], # 인천
        [(2, 5), (3, 5), (3, 4), (8, 4), (8, 7), (7, 7), (7, 9), (4, 9), (4, 7), (1, 7)], # 서울
        [(1, 6), (1, 9), (3, 9), (3, 10), (8, 10), (8, 9),
         (9, 9), (9, 8), (10, 8), (10, 5), (9, 5), (9, 3)], # 경기도
        [(9, 12), (9, 10), (8, 10)], # 강원도
        [(10, 5), (11, 5), (11, 4), (12, 4), (12, 5), (13, 5),
         (13, 4), (14, 4), (14, 2)], # 충청남도
        [(11, 5), (12, 5), (12, 6), (15, 6), (15, 7), (13, 7),
         (13, 8), (11, 8), (11, 9), (10, 9), (10, 8)], # 충청북도
        [(14, 4), (15, 4), (15, 6)], # 대전시
        [(14, 7), (14, 9), (13, 9), (13, 11), (13, 13)], # 경상북도
        [(14, 8), (16, 8), (16, 10), (15, 10),
         (15, 11), (14, 11), (14, 12), (13, 12)], # 대구시
        [(15, 11), (16, 11), (16, 13)], # 울산시
        [(17, 1), (17, 3), (18, 3), (18, 6), (15, 6)], # 전라북도
        [(19, 2), (19, 4), (21, 4), (21, 3), (22, 3), (22, 2), (19, 2)], # 광주시
        [(18, 5), (20, 5), (20, 6)], # 전라남도
        [(16, 9), (18, 9), (18, 8), (19, 8), (19, 9), (20, 9), (20, 10)], # 부산시
    ]
    # x와 y 값에다가 값을 넣음
    mapdata = blockedMap.pivot(index='y', columns='x', values=targetData)
    masked_mapdata = mapdata
    
    # 색상을 지정하는 부분
    plt.figure(figsize=(8, 13))
    plt.pcolor(masked_mapdata, vmin=vmin, vmax=vmax, cmap=cmapname, edgecolor='#aaaaaa', linewidth=0.5)

    # 지역 이름을 표시함
    for idx, row in blockedMap.iterrows():
        annocolor = 'white' if row[targetData] > whitelabelmin else 'black'

        # 광역시는 구 이름이 겹치는 경우가 많아서 시단위 이름도 같이 표시함. (중구, 서구)
        if row[d1].endswith('시') and not row[d1].startswith('세종'):
            dispname = '{}\n{}'.format(row[d1][:2], row[d2][:-1])
            if len(row[d2]) <= 2:
                dispname += row[d2][-1]
        else:
            dispname = row[d2][:-1]

        # 서대문구, 서귀포시 같이 이름이 3자 이상인 경우에 시각화가 힘들어
        # 작은 글자로 표시함.
        if len(dispname.splitlines()[-1]) >= 3:
            fontsize, linespacing = 9.5, 1.5
        else:
            fontsize, linespacing = 11, 1.2

        plt.annotate(dispname, (row['x']+0.5, row['y']+0.5), weight='bold',
                     fontsize=fontsize, ha='center', va='center', color=annocolor,
                     linespacing=linespacing)
        
    # 시도 경계를 그림.
    for path in BORDER_LINES:
        ys, xs = zip(*path)
        plt.plot(xs, ys, c='black', lw=4)

    plt.gca().invert_yaxis()

    plt.axis('off')

    cb = plt.colorbar(shrink=.1, aspect=10)
    cb.set_label(datalabel)

    plt.tight_layout()
    plt.show()
# 전체적으로 한국 지도를 그리는 방법은 위치 (x,y)를 잡고, 도 혹은 시별 경계선을 그리고,
# 데이터를 배치하고 colormap을 적용시키는 과정을 거침.
# https://matplotlib.org/2.0.2/examples/color/colormaps_reference.html (colormap 값 참고함)
```

```python
df = draw_korea.join(cityDF['사망자율'])
drawKorea('사망자율', df,'광역시도','행정구역','BuPu')
# cityDF의 사망자율 칼럼과 draw_korea 내부 조인을 하여 drawKorea 함수를 호출
# 충청남도 계룡시와 서울역이있는 서울종로구의 사망자율이 높은걸 확인할수 있음
```

```python
df = draw_korea.join(cityDF['사망자수'], how='inner')
drawKorea('사망자수', df,'광역시도','행정구역','Reds')
# 마찬가지로 사망자수를  확인하면 경상남도 창원시가 가장높음
```

```python
df = draw_korea.join(cityDF['사상자수'], how='inner')
drawKorea('사상자수', df,'광역시도','행정구역','Blues')
# 사상자수도 창원,경주,평택,화성시가 높은걸 확인할수있음
# 서울지역에 인구수가 많고 밀접했지만 사상자수와 사망자수도 적음
# 사망자율은 사상자수가 적어 비율이 높게나온것으로 분석됨
```

```python
df = draw_korea.join(cityDF['경상자율'], how='inner')
drawKorea('경상자율', df,'광역시도','행정구역','YlGn')
# 경상자율은 곡성이 가장 높고 그다음으로 영월 서울구로 서울강북 순으로 확인
```

```python
df = draw_korea.join(cityDF['부상신고자율'], how='inner')
drawKorea('부상신고자율', df,'광역시도','행정구역','binary')
# 부상신고자율은 고성이 압도적으로 가장높음
```

#### 끝으로
서울이 교통사고발생이 제일 높을줄 알았는데 경상남도 창원시에 사망자와 사상자수가 가장많다는 결과가 나왔다. 후에 분석을 더 하게된다면 경상남도
창원시를 중점으로 Folium 라이브러리를 활용하여 분석을 하고싶다.

