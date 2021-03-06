# Front-End Architecture



## 초창기 웹
초창기 웹은 HTML페이지를 연결해놓은 수준이었습니다. 당시 자바스크립트의 역할은 `form` 필드 유효성 검사와 이미지 롤오버나 DOM 노드에 기본적인 기능을 부여는 정도로 사용됐습니다.

기술이 발전하고 새로운 브라우저가 등장하면서 웹 페이지 구조는 빠르게 바뀌기 시작했습니다. 브라우저가 늘어나면서 일관성 있는 웹 사이트를 개발하기 힘들어졌습니다. 당시엔 웹 표준이 없었기 때문에 브라우저마다 제각기 다른 동작을 했기 때문이죠. 이런 브라우저간 호완성 문제를 해결하기 위해 jQery같은 라이브러리를 사용하기 시작했습니다. 

그러는 와중에 2005년 웹 구조의 판도를 바꾸는 기술이 등장했습니다. 구글 맵스(ajax를 이용한 애플리케이션)가 나오면서 정적 웹에서 벗어나 동적 웹의 시대가 도래했죠. ajax를 쓰면서 서버에서 페이지를 완전히 re-rendering할 필요가 없어졌습니다. 그 대신 클라이언트 측 애플리케이션 서버 APi와 Rest 앤드포인트에 직접 데이터를 요청하고 DOM을 동적으로 수정했습니다. ajax의 등장을 기점으로 웹에 대한 인식이 완전히 바뀌었습니다.  
하지만 이때까지만 해도 웹 페이지에서 사용되는 자바스크립트 로직이 HTML파일에 전부 작성되어있어 소스 관리와 메모리누수의 문제가 있었습니다. 
시행착오를 겪은 기업은 애플리케이션 구축 방법의 표준화 필요성을 느꼈고 일관성있는 API와 서버 아키텍쳐를 도입하여 개발과 유지비용을 절약했습니다. 
<br><br>


## Intro
애플리케이션 아키텍처는 실제 클래스와 프레임워크 코드로 애플리케이션에 구조와 일관성을 제공합니다. 우수한 아키텍쳐를 구축하면 몇 가지 중요한 혜택을 누릴 수 있습니다.
- 모든 애플리케이션이 동일하게 작동하므로 한 번만 배우면 된다.
- 여러 앱이 어렵지 않게 코드를 공유한다.
- 개발자들이 서로 중복되고 상충되는 기능을 만들기 어려워진다.
(이런 프레임워크의 장점은 대규모 애플리케이션에서 특히 중요합니다.)

애플리케이션 아키텍쳐 패턴은 여러 가지 있지만 가장 많이 사용되는것은 MVC와 MVVM입니다. 이 차이를 이해하는것이 중요하기 때문에 지금부터 각각 알아보겠습니다.
<br><br>

## 1. MVC
애플리케이션의 사용자 인터페이스를 세 가지로 나눔으로써 기능에 따라 코드를 정리해 정보를 논리적으로 표시할 수 있습니다.
MVC의 구성은 다음과 같습니다.

- Model : 애플리케이션에 사용되는 데이터의 일반적인 포맷이다. 비즈니스 규칙, 유효성 검사 논리, 그 밖의 다양한 기능을 포함할 수도 있다.
- View : 사용자에게 데이터를 나타낸다. 다수의 View는 같은 Model 데이터를 다양하게 표시할 수 있다.
- Controller : MVC 애플리케이션의 핵심이다. 애플리케이션의 이벤트를 리스닝해 Model과 View 사이의 명령을 위임한다.

MVC 구조에서 프로그램의 모든 객체는 Model, View, Controller 중 하나 이어야합니다. 사용자는 view와 Interaction을 하고 View는 Model에 있는 데이터를 보여줍니다. controller는 이런 Interaction을 감시하며 필요할 때 view와 Model을 업데이트해야합니다.

업데이트 지시는 전적으로 Controller 역할이기 떄문에 View와 Model은 서로를 독립되어 있습니다. View에는 비지니스 로직이 가능한 적어야하고 Model은 데이터의 단순한 인터페이스이어야 합니다. 서로의 역할이 완벽히 분리 된 구죠죠. 그 말은 MVC구조에서 애플리케이션 내에서 Controller가 애플리케이션 논리를 거의 다 가지고 있다는 말이 됩니다. MVC 아키텍처의 최고 장점은 스파게티 코드로 가득한 파일이 나올리 없다는 것입니다.

### 1.특징
Controller는 여러개의 View를 선택할 수 있는 1:N구조다.  
Controller는 view를 선택할 뿐 직접 업데이트 하지 않습니다.


### 2.단점
- View와 Model사이의 의존성이 높다. View와 Model의 높은 의존성은 어플리케이션이 커질수록 구조를 복잡하게 만들고 유지보수하기 어렵게 만든다.


### 3.동작
1. 사용자의 Action들이 Controller에 들어오게 됩니다.
2. Controller는 사용자의 Action를 확인하고 Model을 업데이트 합니다.
3. Controller는 Model을 나타내줄 View를 선택합니다.
4. View는 Model을 이용하여 화면ㅇ르 나타냅니다.
<br><br>


## 2. MVVM
MVVM은 Model + View + View Model을 합친 용어입니다. 


### 1.구조 
- Model : 어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분.
- View : 사용자에서 보여지는 UI부분.
- View Model : View를 표현하기 위해 만든 View를 위한 Model. View를 나타내 주기 위한 Model이자 View르 ㄹ나타내기 위한 데이터를 처리하는 부분다.


### 2. 동작
1. 사용자의 Action들은 View를통해 들어오게 됩니다.
2. View에 Action이 들어오면, Command패턴으로 View Model에 Action을 전달합니다.
3. View Model은 Model에게 데이터를 요청합니다.
4. Model은 View Model에게 요청받은 데이터를 응답합니다.
5. View Model은 응답 받은 데이터를 가공하여 저장합니다.
6. Viwe는 View Model과 Data Binding하여 화면을 나타냅니다.

### 3. 특징
MVVC팬턴은 Command패턴과 Data Binding 두 가지 패턴을 상요하여 구현되었습니다. 이 두가지 패턴을 이용하여 View와 View 사이의 의존성을 없앴습니다. View MOdel과 view는 1:n 관계입니다.


### 4. 장점
MVVM 패턴은 View와 Model 사이의 의존성이 없습니다. 또한 Command 패턴과 DataBinding을 사용하여 View와 View Model사이의 의존성 또한 없앤 디자인패턴입니다. 각각의 부분은 독립적이기 떄문에 모듈화 하여 개발할 수 있습니다.


## 3.Flux

### 1.특징
Flux의 가장 큰 특징은 단방향 데이터 흐름입니다. 데이터 흐름은 항상 Dispatcher에서 Store로, Store에서 View로 View는 Action을 통해서 다시 Dispatcher로 데이터가 흐르게 됩니다. 이런 단방향 데이터 흐름은 데이터 변화를 예측하기 쉽게 만듭니다.  기존의 MVCModel에서는 양방향 데이터 바인딩 구조이문에 한 Model을 업데이트 한 뒤 다른 Model을 업데이트 해야하는 순차적인 업데이트가 발생하게 된다. 이런 순차적 데이터 업데이트는 대규모 애플리케이션에서 User Interaction을 복잡하게 만든다. 한편 Flux의 단방향 데이터 흐름은 데이터 변화를 예측하기 쉽다.


### 2.구성
#### 1. Dispatcher  
Dispatcher는 Flux의 모든 데이터 흐름을 관리하는 허브 역할을 하는 부분입니다. Action이 발생하명 Dispatcher로전달되는데 Dispatcher는 전달된 Action을 보고 등록된 콜백 함수를 실행하여 Store에 데이터를 전달합니다. Dispatcher는 전체 어플리케이션에서 한 개의 인스턴스를 사용합니다.

#### 2. Store  
Store는 애플리케이션 내의 모든 상태와 그와 관련된 로직을 가지고 있다. 모든 상태변경은 반드시 스토어에 의해서 결정되어야만 하며, 상태 변경을 위한 요청을 스토어에 직접 보낼 순없다. 무조건 Action-Dispatcher를 거쳐서 액션을 전달받아야한다. Store의 내부는 보통 Switch stetement를 사용해서 처리할 액션과 무시할 액션을 결정하게 된다. 만약 처리가 필요한 액션이라면 주어진 액션에 따라서 무엇을 할지 결정하고 상태를 변경하게 된다. 일단 스토어에서 상태를 변경하고 나면 상태값이 변경되었다는 사실을 Controller View에 전달한다.

#### 3. View  
View는 상태를 가져오고 사용자에게 보여주고 입력받을 화면을 렌더링하는 역할을 맡습니다.
View를 Presenter라고 생각하면 좋습니다. 애플리케이션 내부에 대해서 아는것이 없지만 받은 데이터를 처리해서 사람들이 이해할 수 있는 포맷(HTML)로 바꾸는 역할을 하는거죠.  

Flux에서의 View는 Controller의 셩격도 가지고 있습니다. 중첩된 View Layer의 최상단 View는 Store에서 데이터를 가져와 자식 View로 배분하는 역할을 한는데 이 View를 Controller View라고 합니다. Store와 View 사이의 중간관리자 같은 역할을 한다고 볼 수 있습니다. 상태가 변경되었을 떄 Store가 그 사실을 Controller View에게 알려주면 Controler View는 자신의 아래에 있는 모든 View에게 새로운 상태를 넘겨줍니다.

#### 4. Action  
Dispatcher에서 콜백 함수가 실행되면 Store가 업데이트 되게 되는데, 이 콜백 함수를 실행 할 때 데이터가 담겨 있는 객체가 인수로 전달 되어야하니다. 이 전달되는 객체를 Action이라고 하는데, Actoin은 대채로 Action creater에서 만들어집니다.  

#### 5. Action Createer  
액션 생성자는 모든 변경사항과 user Interaction을 거쳐가야 하는 액션의 생성을 담당하고 있다. 언제든 애플리케이션의 상태를 변경하거나 View를 업데이트하고 싶다면 액션을 생성해야한다. 무슨 메세지를 보낼지 알려주면 액션 생성자는 시스템이 이해할 수 있는 포멧으로 변환한다. 액션 생성자는 type과 payLoad를 포함한 액션을 생성한다. 타입은 시스템에 정의된 액션중의 하나이다.  

모든 가능한 액션들을 아는 시스템을 가짐으로써 부차적으로 갖는 멋진 효과가 있다. 새로운 개발자가 프로젝트에 들어와서 행동 생성자 파일을 열면 시스템에서 제공하는 API전체를 바로 확일 할 수있다.


### 3.동작.
사용자 입력으로 액션이 생겼을 떄를 생각해봅시다.
1. View는 Action Creater를 통해 상태값 변경에 대한 정보가 담긴 Action을 생성합니다.
2. Action Creater가 생성한 Action을 Dispatcher에 전달합니다.
3. Dispatcher는 Action이 호출된 순서에 따라 알맞은 스토어로 전달합니다.(Store가 여러개인 구조)
4. Store에서는 Actoin의 정보를 확인해서 상태값 변경을 처리합니다.(경우에 따라 Action을 무시합니다.)
5. 상태 변경이 완료되면 Store는 자신을 subscribe하고 있는 Controller View에게 상태값이 변경됐다는 사실을 전달합니다.
6. Controller view는 Store에게 변경된 상태값을 전달받습니다.
7. 변경된 상태값을 전달받은 Controller View는 자신 아래의 모든 View에게 새로운 상태를 렌더링하라는 신호를 전달합니다.
8. View에서 상태값에 따라 ReRendergin을 수행합니다.





## Ref
- [페이스북이 Flux구조를 선택한 이유](https://blog.coderifleman.com/2015/06/19/mvc-does-not-scale-use-flux-instead/)
- [FaceBook.gitgub](https://facebook.github.io/flux/)
- [카툰으로 이해하는 Flux](https://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/)
- [Flux와 MVC비교](https://beomy.tistory.com/44)
- [MVC와 MVVM비교](https://beomy.tistory.com/43)
- [Front-End Mvc](https://www.miraeweb.com/single-post/2016/11/17/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%9B%B9%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EC%95%84%ED%82%A4%ED%85%8D%EC%B3%90-%EB%B9%84%EA%B5%90%EB%B6%84%EC%84%9D-MVC%EC%99%80-MVVM)