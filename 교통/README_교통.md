## 경기도 남/북부 출퇴근 교통 현황 파악 및 개선
#### 참여자 : 유현동, 박태정, 고현아, 권구희, 김홍서
#### EDA 프로젝트 자료 소개
> * Dataset # 사용한 데이터셋 설명과 url 
>   * [교통카드 빅데이터 시스템](https://stcis.go.kr/wps/main.do) : 국토교통부와 한국교통안전공단에서 제공되는 데이터로 이용량 지표, 노선/정류장 지표 등 버스, 지하철의 다양한 교통 데이터 제공
>   * [티머니 교통카드 통계자료](https://www.t-money.co.kr/ncs/pct/ugd/ReadTrcrStstList.dev?page=1&rows=10) : 버스와 지하철에 대해서 선/후불 및 1회용 교통카드 기준으로 승/하차 승객 수 등의 교통 데이터 제공

<br>


## EDA 프로젝트 요약

1. 프로젝트 주제 및 목적
        - 경기도 남부, 북부의 교통 현황에 유의미한 차이가 있는지 파악

* 남부에서는 수원시와 용인시, 북부에서는 고양시와 남양주시를 선정, 버스와 지하철을 바탕으로 출퇴근 시간에 지역별로 교통 차이가 존재하는지 파악

 * Track1 : 버스 및 지하철 노선을 시각화하여 현 교통 현황을 파악

 * Track2 : 비스 및 지하철 이용량과 혼잡도를 계산하여 남부/북부 간에 유의미한 차이가 있는지 파악(출퇴근 시간 기준)


2. 데이터 전처리
* 각 도시별, 월별 혼잡도를 비롯한 이용량 데이터에 대해서 분석 전 전처리 진행(이용량 데이터의 경우 일반인 탑승자만 데이터에 포함시킴)
* 시각화를 위한 버스정류장과 지하철역의 위치정보 데이터의 경우 해당 데이터에서 x좌표와 y좌표만 추출

 
3. 분석 방법 및 결과
* Track1 : 인구 수를 기준으로 경기도 남부와 북부에서 2개씩 추출함(수원시와 용인시 / 고양시와 남양주시). 버스와 지하철 노선을 folium을 이용하여 시각화하여 현재 존재하는 노선을 파악함. 각 도시와 서울을 잇는 광역버스와 좌석버스를 조사하였고 마찬가지로 서울과 이어진 지하철 노선을 조사하여 이용량과 혼잡도 데이터를 분석함. 버스의 경우 "교통카드 빅데이터 시스템"에 존재하는 혼잡도 데이터를 활용하였고, 지하철의 경우 혼잡도 계산식을 활용하여 각 노선별로 따로 도출함(각 분기마다 한 달씩 1월, 4월 or 5월, 7월, 11월 데이터 추출). 지하철은 승차인원합을 이용하여 혼잡도를 도출하였고 버스는 혼잡도와 이용량 데이터를 활용하여 10분위로 구간을 나누어 비교함. 그 결과, 지하철은 출근시간에(6시-9시) 용인, 수원, 고양, 남양주 순서로 혼잡했고 퇴근시간에(17시-19시) 수원, 용인, 고양, 남양주 순서로 혼잡함. 버스는 출근시간에 수원, 고양, 남양주, 용인 순으로 혼잡하고 퇴근시간에 고양, 수원, 용인, 남양주 순으로 혼잡함.

* Track2 : 남부의 도시들과 북부의 도시들 간에 출퇴근 혼잡도와 교통량에 실제로 유의미한 차이가 존재하는지 파악하기 위해 가설검정을 진행함. 출퇴근 혼잡도의 경우 버스 혼잡도 데이터를 이용하였고 교통량의 경우 목적통행량(발생량과 도착량으로 나뉘며 해당지역에서 출발한 사람, 해당 지역에 도착한 사람 수를 의미)을 이용함. 데이터를 추출한 월별로 남부 도시와 북부 도시 한 곳씩 가설검정을 진행함(정규성 확인, 등분산성 확인, t-test 순서로 진행). 출퇴근 혼잡도의 경우 남양주는 남부 도시들과 유의미한 차이가 존재하지만 고양은 존재하지 않는 것으로 확인됨. 목적통행량의 경우도 마찬가지로 남양주는 남부 도시들과 유의미한 차이가 존재하지만 고양은 그렇지 않은 것으로 확인됨(월별 구체적인 결과는 "목적통행량 분석 및 가설검정.ipynb" 확인). Track1에서 구한 혼잡도와 이용량을 바탕으로 버스와 지하철 각각 top3 정류장과 지하철역을 조사하고 이를 folium을 이용하여 지도로 시각화함. 

      
4. 결론
* 고양시 : 버스 혼잡도와 이용량 그래프가 8~10분위에서 가파름, 대화역 근처에 혼잡도가 몰림 → **출퇴근 인원을 분산시킬 정도의 노선이 부족함**
* 남양주시 : 혼잡도 분위수 그래프를 보았을 때, 8~10분위에서 그래프가 가파름 → **특정 노선에 사람이 몰림, 노선의 배치가 비효율적**
* 수원과 용인 : 혼잡도 시각화를 보았을 때, 상대적으로 혼잡한 지역이 분산되어 있는 것을 확인 → **노선의 배치가 고양, 남양주에 비해 효율적으로 구성됨**
* 출근 시간대에서 북부의 혼잡도가 남부보다 낮기에 버스 대신 지하철을 이용하는 것이 더 유리함. 지하철의 경우 19시가 지나면 혼잡도가 크게 떨어지므로 19시 이후에 퇴근이 유리함. 

    
5. 아쉬운 점
* 데이터 처리의 한계로 경기도 전체가 아닌 일부 4개 도시만으로 진행하게 된 점.
* 운행횟수가 지나치게 적은 일부 노선은 제외된 점.
* 한 정류장에서 다른 정류장으로의 재차인원(기존에 승차해 있는 인원)이 정확하게 계산되지 못하여 혼잡도 계산에 부정확성이 생긴 점.
* 분기별로 한 달씩만 데이터를 추출하였기에 1년 전체를 조사하지 못한 점.

<br>



 ## 각 팀원의 역할
 
|이름|활동 내용| 
|:---:|:---|
|유현동| - (팀장) 팀 일정 관리와 회의 진행<br> - 방향성 설정 및 지하철 데이터 처리, 가설검정 담당<br> - README.md 파일 작성| 
|박태정| - selenium을 이용한 데이터 크롤링 진행<br> - 버스 데이터 처리 및 이용량과 혼잡도의 버스 분위수 그래프 담당| 
|고현아| - 버스 데이터 담당(수원)<br> - 각 도시별 top3 정류장과 지하철역 조사<br> - 발표 및 발표자료 제작|
|권구희| - 버스와 지하철 데이터 담당(용인)<br> - 출/퇴근 시간대별 지하철 혼잡도 계산|
|김홍서| - 버스 데이터 담당(고양)<br> - folium을 활용한 전체적인 시각화 담당|
<br/>

