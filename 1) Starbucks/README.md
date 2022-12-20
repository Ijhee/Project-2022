## ☕️&nbsp;&nbsp;&nbsp;Prediction of Starbucks Coordinates Using Coordinates of Other Commercial
> 타 상권의 좌표들을 바탕으로 스타벅스의 최적 입지를 예측
---

### 📌&nbsp;&nbsp;Purpose of Project
- 서울 및 경기도의 상권을 확인해보면 주요 회사 및 업체들이 역 근처와 같이 교통량이 많은 곳에 몰려있는 것을 확인할 수 있다.상권 중에서도 스타벅스의 경우 유동인구가 많은 곳에만 주로 건설되며, 특히 역 근처에 많이 포진되어 있는 것을 경험적으로 알게 되었다.또한 스타벅스 주위에 다이소, 이디야, 올리브영과 같은 대형 브랜드들이 같이 포진되어 있었다.따라서 다이소, 이디야, 올리브영의 위도/경도값과 해당 값들로 얻어낼 수 있는 수리적인 정보들을 바탕으로 스타벅스의 최적 입지(경도/위도)를 찾아내는 것이 본 분석의 목표이다.

### 📌&nbsp;&nbsp;Process
- #### 1) [Raw Data & Crawling](https://github.com/Ijhee/Project-2022/blob/main/1)
  > <img width="800" alt="스크린샷 2022-12-20 오후 10 34 19" src="https://user-images.githubusercontent.com/96717686/208679458-90e51837-a9c1-4c7e-9a16-5893c5aab9b8.png"></br>
  >
  > 먼저 1호선부터 9호선까지의 역 근처에 있는 스타벅스와 이디야,올리브영, 다이소를 기준으로 데이터를 수집했다. 위에 보이는 데이터는 Google Maps에서 제공되는 주소를 직접 따와서 엑셀에 수작업으로 기입했다.</br>
  > 
  > <img width="800" alt="스크린샷 2022-12-20 오후 10 45 23" src="https://user-images.githubusercontent.com/96717686/208693252-5d7f1965-6976-424d-8dcd-11844e133a09.png"></br>
  >
  > 전 그림의 전체 데이터에서 주소만 따온뒤, 크롤링을 통해 위 사이트에서 주소를 기입한 후 해당 주소의 경도와 위도를 새로운 컬럼으로 추가하는 과정을 거친다. 

