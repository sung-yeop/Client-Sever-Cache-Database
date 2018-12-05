# Server
## Django vs Flask
* * * 
### 시작하기에 앞서
Q : 왜 서버가 필요할까?

A : 서버가 없는 스탠드얼론(Stand-alone) 앱도 많다. 예를들어 스도쿠처럼 캐쥬얼게임에는 서버가 필요하지 않다. 하지만 서버가 필요한 경우는 바로 **별도의 회원정보 관리**가 필요한 경우이다.
따라서 무조건적으로 서버를 만들어야 하는게아니라, 자신이 기획한 게임의 특성에 맞춰서 서버의 유무를 선택해야할 필요가 있다.

Q : 서버는 한 개만 있으면 되는 것인가?

A : 물론 한 개의 서버만 있어도 게임을 기획 할 순 있다. 하지만 Volume이 큰 게임같은 경우에는 서버를 추가로 나눠서 운영할 수 있는 것으로 알고 있다.
하지만 일부 게임에서는 서버를 여러개로 나누는 것이 아닌, 클라우드 서버하나와 IDC서버 호스팅으로 나누는 경우가 있는 것으로 알고 있다. 

* 클라우드서버
  * 추가적인 하드웨어 자원들을 런타임 동안에 추가할 수 있다. (CPU, RAM)
    * 트래픽 증가에 능동적으로 대응하기위한 가변성확보가 가능함
  * 서버 실행 중에 서버를 다른 하드웨어로 옮길 수 있다.
    * 분산된 지역에 대한 빠른 데이터 접근이 가능함
  * Q : 클라우드 서버는 언제 사용할까?
  
    A : 주로 데이터량이 순간적으로 늘어날 위험성이 있는 데이터 또는 동시접속의 증가로 access 접근이 급속하게 증가할 우려가 있는 데이터가 있을 때 주로 사용한다.
    
* IDC 서버 호스팅
  * 인터넷 데이터 센터의 준말로, 온라인 게임의 운영에 필요한 서버 컴퓨터와 네트워크 회선등을 제공한다.
  
**안드로이드 서버 구축**
- Q : 서버는 자료를 저장 및 불러오기 용도로 사용 목적일경우에는 어떻게 해야하는가?
- A : 안드로이드 -> 서버측 HTTP 통신/서버 언어 쿼리문 작성 -> DB 데이터 insert, 서버측 언어/DB데이터 select JSON/XML 파싱 -> 안드로이드 JSON/XML 파싱 순서로 진행

`위 내용 정리하기`


### 1) Django
- python 기반 Web application framework.
- MVC 기반 패턴대로 개발할 수 있도록 구조화 되어있음
- ORM 기능도 내장되어있으며 MySQL, PostgreSQL, Oracle 등 다양한 DBMS에 대해서도 Driver 형태로 손쉽게 붙일 수 있음
- 웹 개발에 필요한 session 관리 지원
- 추가 기능마저도 plugin 형태로 설치후 사용할 수 있음
`Plugin기능 : restframework, Web API 서버를 개발하기위한 toolkit, 다양하고 강력한 기능제공으로

 python기반의 API 서버 개발로 쓰면 좋음`

### 2) Flask
- 원하는 라이브러리와 패키지로 나만의 framework를 만들어나갈 수 있음
- DB ORM 구조가 따로 존재하지 않음
- 필요할 경우에 개발자가 직접 패키지를 다운로드하여 이용해야 함

### Django와 Flask를 사용한 대표적인 기업
#### Pinterest
- ![Flask를 사용한 대표적인 기업](https://user-images.githubusercontent.com/43811124/49536573-393ba700-f90a-11e8-82ad-37fd0375a182.PNG)

- Flask를 사용한 이유 : Flask를 이용해서 API 기능 위주로 개발하기 위해서 사용함
- Django를 사용한 이유 : Pinterest의 경우에는 Django를 core application 서버로 사용

#### twilio
- ![twilio가 Flask를 사용한 이유](https://user-images.githubusercontent.com/43811124/49536609-4f496780-f90a-11e8-9811-36d394b4dbde.PNG)

- Flask를 사용한 이유 : API를 자신이 원하는대로 개발할 수 있기 때문
  - ![2-2-1. twilio가 Flask를 사용한 이유(Real)](https://user-images.githubusercontent.com/43811124/49537010-2fff0a00-f90b-11e8-86e6-587685746d24.PNG) 
  
  **<twilio에서 직접적은 이유 원문> 출처 : twilio**
  
#### ![2-2-1. Bitbucket](https://user-images.githubusercontent.com/43811124/49537316-04305400-f90c-11e8-82bd-e2dd19966642.PNG)
- Django를 사용한 이유 : 강력한 Framework를 무료로 사용할 수 있기 때문에 사용

### Django와 Flask의 관심도 변화
![2-2-2. Django와 Flask의 관심도 비교](https://user-images.githubusercontent.com/43811124/49536591-422c7880-f90a-11e8-939e-f4e1aa8554df.PNG)

**출처 : Google Trend**

- Django와 Flask모두 꾸준히 언급되고 있는 Web Framework이다.
- 하지만 위 그래프를 살펴보면 Django가 Flask보다 2배 이상 많이 언급되고 있음을 알 수 있다.
  - `언급된다고해서 무조건 2배이상의 사용을 보여주는 것은 아니나, 언급이 되고있다는 것은 다른사람들에게도 널리 알려진 Framework라고 해석된다.`
  
## 결론 
- Django는 개발하기 위한 대부분의 작업들을 Framework 레벨에서 지원해주는 것이 강점
- Flask는 지원해주는 것이 있는게 아니라, 개발자가 원하는 패키지를 다운로드하여 자신만의 Framework를 만들 수 있다는 것이 강점

- **Django** 선택
- 선택한 근거 
  * 강력한 Framework를 지원해준다는 점이 개발 초보들에게 있어서는 진입장벽이 낮은 것으로 생각됨
  * 2배이상 언급되는 것을 바탕으로, Django에 대한 정보가 훨씬 많다는 것을 알 수 있음
  * Flask와 비교해서는 ORM기능이나 MVC 기반 패턴대로 구조화 되어있기 때문에 편리한 이용이 
  
