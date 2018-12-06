# Cache
## Redis vs Memcached
* * *
### 시작하기에 앞서
* Cache란 무엇인가?
  * Cache는 많은 시간과 연산이 필요한 작업에 대한 결과를 저장해두는 곳이다.
  * 데이터를 빠르게 입/출력하기 위해서 Cache를 사용한다.
    * 디스크에서 데이터를 가지고 오는 것 보다 Cache에서 데이터를 가지고 오는 것이 더 빠르기 떄문
    
* Cache란 어디에 적용해야 하는가?
  * 위에서 언급했듯이, Cache는 DB의 Cpu부하와 같은 부작용이 일어나지 않도록 따로 데이터를 저장해주는 곳을 의미한다.
  
  ![3-0. 일반적인 Cache 적용](https://user-images.githubusercontent.com/43811124/49564057-9c0e5c00-f965-11e8-91eb-cb3595351d0b.PNG)
  
  * 위 그림은 Cache의 일반적인 경로이다.. 
  
#### 1) Redis
* 디스크에 데이터를 기록하고 있기 떄문에, Redis 메모리가 날라가도 데이터를 복구할 수 있다.
* Key/Value Store형식이다. + 기본적인 PUT/GET Operation을 지원한다.
  * ![3-1. Key, Value 형식](https://user-images.githubusercontent.com/43811124/49564688-c2cd9200-f967-11e8-8a66-2dd2822dd551.PNG)
* String, List, Set, Sorted sets, Hash 등의 데이터 포맷을 지원한다.
  * 편하게 데이터를 저장하고 사용할 수 있도록 도와준다.
  * ![3-1. 다양한 형태의 데이터 포맷 지원](https://user-images.githubusercontent.com/43811124/49564514-2c00d580-f967-11e8-9be0-21ff4b6e2afc.PNG)
