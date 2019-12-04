# Module


## 언제 사용하나?

## 무엇을 해결하나?

## 제안된 문제를 어떻게 해결하나?


## 용도
- 구성요소를 다른 구성요도와 독립적으류 유지하는데 사용된다.
- 느슨한 결합을 제공한다.
- 캡슐화를 할 수 있다.
- 

## First knowledge
- IIFE(Immediately-Invoked-Function-Expressions)
- 클로저
- 비공개 변수 (특권 멤버)
- 캡슐화
- 객체복사
- 네임스페이스




```js
//객체 깊은 복사.
function cloneObject(obj) {
    var clone = {};
    for(var i in obj) {
        if(typeof(obj[i])=="object" && obj[i] != null)
            clone[i] = cloneObject(obj[i]);
        else
            clone[i] = obj[i];
    }
    return clone;
}


var person = (function () {
    
    var firstName = 'Cater';
    var age = 30;

    //read only property
    var personalInfo = {
        tribe    : 'human', 
        gender   : 'M',
        nativeCountry : 'korea'
    }

    return {
        getName : function(){
            return firstName;
        },
        getAge : function(){
            return age
        },
        addAge : function(){
            ++age;
        },
        getPersonalInfo : function(){
            return cloneObject(personalInfo);
        }
    }
})()
```

자바스크립트에는 private 변수가 없다.  
이를 위해 등장하는 패턴이 모듈화 패턴이다.
클로져를 이용해 outter function의 스코프에 접근을 막아 캡슐화를 했다.  
클로저로 정의된 맴버에 대한 접근을 inner function으로 제한하여 데이터가 왜곡되는 것을 막을 수 있다.  
단, 이와 같은 패턴에서 객체를 리턴할 때 문제가 생길 수 있는데 다음과 같은 이유다.
      

## 비공개 변수가 객체 형태일 경우.
![](/resource/img/javascript/desingPattern_module.png)


personalInfo의 값이 얕은 복사되어 수정이 가능한 상황이 발생한다.  
위 상황에선 readOnly 속성인 성별이 바뀌었다.  
이런 오류를 막기 위해 return을 할때 객체복사를 하면 불변성을 유지할 수 있다.