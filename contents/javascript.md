# JAVASCRIPT

**:Contents**
* [이벤트전파방식](#이벤트전파방식)
* [클로저](#클로저)
* [promise](#promise)
* [async await](#async await)
* [var let const](#var_let_const)
* [JavaScript에서 undefined와 null의 차이점](#undefined와_null의_차이점)



### 이벤트전파방식

`이벤트 버블링`<br>
>>  하위에서 상위 요소로의 이벤트 전파 방식을 이벤트 버블링(Event Bubbling)

`이벤트 캡쳐`<br>
>> 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식

`stopPropagation`<br>
 ```javascript
    div.addEventListener('click', event, {
		capture: true // default 값은 false입니다.
	});
```


그렇다면 전체적으로 이벤트를 전달하는게 아니고 해당요소에 이벤트만 주고 싶다면?<br>
`stopPropagation`<br>
 ```javascript
function logEvent(event) {
	event.stopPropagation();
}
```


`이벤트 위임`<br>
>> 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식

- cf) https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/

### 클로저
> 클로저란 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미한다.
> 자바 스크립트의 함수는 생성될 당시의 환경을 기억하고 저장하며 이를 통해 외부 렉시컬 환경에 대한 참조가 가능하므로, 모든 함수가 클로저라고 할 수 있다.
* 함수와 렉시컬 환경의 조합
* 함수가 생성될 당시의 외부 변수를 기억
* 생성 이후에도 계속 접근가능


https://velog.io/@winz/Javascript-%EB%A0%89%EC%8B%9C%EC%BB%AC%ED%99%98%EA%B2%BD%EA%B3%BC-%ED%81%B4%EB%A1%9C%EC%A0%80Closure-Javascript-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90-8


### undefined와 null의 차이점

`undefined`<br>
* undefined은 변수를 선언하고 값을 할당하지 않은 상태
* undefined는 자료형이 없는 상태이다.
* typeof를 통해 자료형을 확인해보면 undefined는 undefined가 출력

 ```javascript
var un =undefined;

typeof un
```

`null`<br>
*  typeof를 통해 자료형을 확인해보면 null은 object
* null은 변수를 선언하고 빈 값을 할당한 상태(빈 객체)이다
* typeof를 통해 자료형을 확인해보면 null은 object가 출력

 ```javascript
var n = null;

typeof n
```

`JavaScript에서 undefined와 null 모두를 판단하는 방법`<br>
>> if (!변수명) 

 ```javascript
if(!un){console.log(1)}

if(!n){console.log(1)}
```
