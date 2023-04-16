
## 📌데이터 타입

|구분|데이터 타입|설명|
|------|---|---|
|원시 타입|숫자 타입|숫자, 정수, 실수 구분 없이 하나의 숫자 타입만 존재|
|원시 타입|문자열 타입|문자열|
|원시 타입|불리언 타입|논리적 참과 거짓|
|원시 타입|undefined 타입|var 키워드로 선언된 변수에 암묵적으로 할당되는 값|
|원시 타입|null 타입|값이 없다는 것을 의도적으로 명시할 때 사용하는 값|
|원시 타입|심벌(symbol) 타입|ES6에서 추가된 7번째 타입|
|객체 타입|객체 타입|`객체, 함수, 배열` 등|

### 📌숫자 타입
- ECMA-262 사양에 따르면 숫자 타입은 `64비트 부동소수점 형식`을 따름.
- 따라서 모든 수를 실수로 처리하며, 정수를 표현하는 데이터 타입은 없음.
- 이외에도 `Infinity, -Infinity, NaN`과 같은 특수 숫자 값도 존재함.

### 📌문자열 타입

- 문자열은 0개 이상의 16비트 유니코드 문자로 구성된 집합을 말함.
- 문자열은 작은 따옴표(''), 큰 따옴표(""), 백틱(``.`템플릿 리터럴`)을 사용하여 표현할 수 있음.
- 문자열을 따옴표로 감싸지 않으면 자바스크립트 엔진은 키워드나 식별자같은 다른 토큰으로 해석함.
- 일반 문자열 내에서는 줄바꿈이 허용되지 않아 `백슬래시(\)`를 사용하여 줄바꿈을 표현할 수 있음.


### 📌불리언 타입
- 불리언 타입은 논리적 참과 거짓을 나타내는 데이터 타입임.
- 불리언 타입은 `true, false` 두 가지 값만을 가짐.
- 주로 조건문, 반복문의 `조건식`에 사용됨.

### 📌undefined 타입
- undefined 타입은 `변수를 선언하고 값을 할당하지 않은 상태`를 말함.
- 개발자가 의도적으로 변수에 undefined를 할당하는 것은 권장하지 않음.
- 명시적으로 값이 없음을 의도할 때는 `null`을 할당하는 것이 좋음.
  
### 📌null 타입
- null 타입은 `값이 없음`을 의도적으로 명시할 때 사용하는 값임.
- 이는 변수가 이전에 참조하던 값을 더는 참조하지 않겠다는 의미임.
- 따라서 이전 할당값에 대한 참조를 명시적으로 제거하는 것을 의미함.  

### 📌심벌 타입
- ES6에서 추가된 7번째 타입으로 변경 불가능한 원시 타입의 값임.
- 다른 값과 중복되지 않는 유일무이한 값으로, 주로 이름의 충돌 위험이 없는 객체의 `유일한 프로퍼티 키`를 만들기 위해 사용됨.
- 심벌 이외의 원시 값은 리터럴을 통해 생성하지만, 심벌은 Symbol 함수를 호출해 생성함.

### 📌객체 타입
- 자바스크립트는 객체 기반의 언어이며, 자바스크립트를 이루는 `거의 모든 것은 객체`임.
- `함수, 배열, 객체` 등은 모두 객체 타입의 값임.

### 📌데이터 타입의 필요성
- 값은 메모리에 저장되는 데이터임.
- 메모리에 값을 저장하려면, 먼저 확보할 메모리 공간의 크기를 결정해야 함.
- 그래야만 메모리 공간을 낭비 없이 효율적으로 사용할 수 있음.
- 값을 저장할때 뿐 아니라 읽어올 때도 메모리 공간의 크기를 알아야 함.
- 저장할때와 마찬가지로 메모리 공간의 낭비 없이 효율적으로 불러올 수 있기 때문임.
- 또 메모리는 데이터를 2진수로 저장하기 때문에, 2진수를 알맞은 데이터로 변환하기 위해서는 데이터 타입이 필요함.

### 📌동적 타이핑
- `동적 타이핑 언어`는 변수에 값을 할당할 때, 할당된 값에 따라 변수의 타입이 동적으로 결정됨.
- 반대로 `정적 타이핑` 언어는 변수를 선언할 때, 변수의 타입을 명시적으로 지정해야 함.
- `정적 타이핑` 언어는 `컴파일 시점`에 `타입 체크`를 수행하여 타입 체크를 통과하지 못했을 경우 `컴파일 에러`를 발생시킴.
- 이는 타입의 일관성을 강제하여 더욱 안정적인 프로그램을 만들 수 있음.
- 자바스크립트는 `동적 타이핑` 언어임.
- `var`, `let`, `const` 통해 변수를 선언하고, 런타임에 값을 할당할때 타입이 결정됨. 
- 이는 자바스크립트의 `유연성`을 높이는 장점이 있지만, `타입 안정성`을 해치는 단점도 있음.