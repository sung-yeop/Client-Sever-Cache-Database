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
  
#### 1) Redis   ![3-1. Redis 로고 사진](https://user-images.githubusercontent.com/43811124/49564322-759cf080-f966-11e8-82fe-285a4d09f241.PNG)
* 디스크에 데이터를 기록하고 있기 떄문에, Redis 메모리가 날라가도 데이터를 복구할 수 있다.
* Key/Value Store형식이다. + 기본적인 PUT/GET Operation을 지원한다.
  * ![3-1. Key, Value 형식](https://user-images.githubusercontent.com/43811124/49564688-c2cd9200-f967-11e8-8a66-2dd2822dd551.PNG)
* String, List, Set, Sorted sets, Hash 등의 데이터 포맷을 지원한다.
  * 편하게 데이터를 저장하고 사용할 수 있도록 도와준다.
  * ![3-1. 다양한 형태의 데이터 포맷 지원](https://user-images.githubusercontent.com/43811124/49564514-2c00d580-f967-11e8-9be0-21ff4b6e2afc.PNG)
* Memcached보다 더 다양한 API를 지원한다. ex) mset : 여러개의 캐쉬를 한번에 업데이트 할 수 있도록 도와주는 함수/ Memcached에서는 존재하지 않음


#### 2) Memcached    ![3-1. Memcached 로고 사진](https://user-images.githubusercontent.com/43811124/49564338-80f01c00-f966-11e8-9afa-0b542f367b1d.PNG)
* Redis와 동일하게 Key/Value Store 형식이다. 
* 내부적으로 Slab 할당자를 사용하고 있기때문에, 메모리 할당이 빈번히 일어나지 않는다.
* Redis와 비교해서 비교적 적은 데이터를 사용한다. 
* 유일하게 지원하는 데이터 포맷은 String이고, String은 오직 읽기 전용이기떄문에 데이터를 저장하기에 용이하다.

### Q : 어느것이 더 다루기 쉬울까?
A : Memcached와 비교해서 비교적 최근에 나온 Redis가 다루기 더 힘들다.

그 이유는 좀 더 많은 문법이 존재하기 때문, 또한 복잡한 코드의 부분을 캐싱하는 것이 아닐경우에는 Memcached로도 모두 커버가 가능하다.

### Q : Redis에서 제공하는 다양한 데이터 포맷이 어떤 이점을 가져다 주는가?
A : 일단 데이터 포맷부터 정리를 해야한다.
#### 3) 데이터 포맷 종류 및 특성
* String
  * Text 문자열 뿐만 아니라 Integer와 같은 숫자나 JPEG같은 Binary FIle까지 저장이 가능하다
* Set
  * String의 집합이다.
  * 여러개의 값을 하나의 Value에 넣을 수 있다.
  
  ![3-3. Set 데이터 포맷](https://user-images.githubusercontent.com/43811124/49565816-d8dd5180-f96b-11e8-9bd0-784d66276c2d.PNG)
* Sorted Set
  * set에 **score** 필드가 추가된 데이터형
  * Score은 **가중치** 정도로 생각하면 된다.
  * 데이터는 오름차순으로내부 정렬이 되며, 정렬되어있는 score 값 범위에 따른 Range query이 가능하다
  * Top rank에 따른 query가 가능하다.
  
  ![3-3. Sorted set 데이터 포맷](https://user-images.githubusercontent.com/43811124/49566026-a2540680-f96c-11e8-9405-4cc173990a04.PNG)
* Hashes
  * Value내에 field/String Value 쌍으로 이루어진 테이블을 저장하는 데이터 구조체
  
  ![3-3. Hashes 데이터 포맷](https://user-images.githubusercontent.com/43811124/49566038-aaac4180-f96c-11e8-9f05-8bda79342672.PNG)
* List
  * Stirng들의 집합으로 데이터가 저장됨 (Set과 유사)
  * List 앞과 뒤에서 POP/Push 연산을 이용해서 데이터 추가/제거가 용이함
  * 지정된 INDEX값을 이용하여 지정된 위치에 데이터 추가/제거가 용이함
  
  ![3-3. List 데이터 포맷](https://user-images.githubusercontent.com/43811124/49566048-b26be600-f96c-11e8-82e8-abc1622dee48.PNG)
  
  **`다양한 데이터 포맷을 지원한다는 것은 데이터 정리에 유용하다는 것을 알 수 있다.`**
  [출처][1]

## 결론
 * 창의공 프로젝트에서 계획했던 게임은 Volume이 엄청 거대하지 않음
   * 데이터 트래픽이 크게 생기지 않을거라고 생각함
   * 서버의 데이터가 날아가게된다면 DB에 있는 데이터를 다시 Read해서 이용할 수 있다고 생각함
 * 하지만 다양한 API 지원방식이 좀 더 효율적이라고 생각함
   * 직접다뤄보진 않았지만 편리한 함수를 이용하고 싶음
 * Redis는 Memcached보다 더 많은 메모리를 사용하게됨
 * **Memcached** 선택
   * 위에 말했듯이 Volume이 커다란 게임이 아닌데도 불구하고, Cache에서 메모리를 낭비할 필요가 없다고 생각됨
   * Redis의 다양한 API기능과 다양한 데이터 포맷형식이 끌리기는하나, Memcached도 여전히 사용되고 있는 Cache형식이기때문에 Cache 선택
   
   [1]:http://bcho.tistory.com/654
