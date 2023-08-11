# 8장_제어문

## 블록문

블록문은 0개 이상의 문을 중괄호{}로 묶은 것으로 코드 블록 또는 블록이라고 부르기도 한다.

- 자바스크립트는 블록문을 하나의 실행단위로 취급한다.
- 문의 끝에는 세미콜론을 붙이는 것이 일반적이나 블록문은 자체종결성을 갖기 때문에 블록문의 끝에는 **세미콜론을 붙이지 않는다**

```
{
  var foo = 10
}
```

## 조건문

조건문은 주어진 조건식의 평가결과에 따라 코드블록의 실행을 결정한다. 조건식은 불리언 값으로 평가될 수 있는 표현식이다.

### if else 문

if else 문은 논리적 참 또는 거짓에 따라 실행할 코드 블록을 결정한다.

- if문의 조건식은 boolean 값으로 평가되어야 한다. (그렇지 않을경우 자바스크립트 엔진에 의해 암묵적으로 boolean 값으로 변환된다)

<br/>

대부분의 if else 문은 삼항조건연산자로 바꿔 쓸 수 있다.

```js
let x = 10;
let y = 20;
let z = 0;

if (x > y) {
  z = x;
} else {
  if (y > z) {
    z = y;
  } else {
    z = z + 1;
  }
}
```

```js
let x = 10;
let y = 20;
let z = x > y ? x : y > z ? y : z + 1;
```

삼항 조건 연산자 표현식은 값처럼 사용할 수 있어 변수에 할당하는 것이 가능하다. 그렇지만 if else 문은 표현식이 아닌 문이다. 따라서 값처럼 사용할 수 없고 변수에 할당할 수 없다.

### switch문

switch 문은 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다. case 문은 상황을 의미하는 표현식을 지정하고 콜론으로 마친다.

- switch 문은 논리적 참, 거짓보다는 다양한 case 에 따라 실행할 코드 블록을 결정할 때 사용한다.

```js
var weather = "cold";
var season;

switch (weather) {
  case "warm":
    season = "spring";
    break;
  case "hot":
    season = "summer";
    break;
  case "cool":
    season = "fall";
    break;
  case "cold":
    season = "winter";
    break;
  default:
    season = "none";
}
```
- break 키워드로 구성된 break문은 코드 블록에서 탈출하는 역할을 한다.
- default 문은 switch 문의 맨 마지막에 위치하므로 default 문의 실행이 종료되면 switch 문을 빠져나간다. 따라서 별도의 break 문이 필요없다.
- default 문에는 break 문을 생략하는 것이 일반적이다. 

### 반복문
반복문은 조건식의 평가 결과가 참인 경우 코드 블록을 실행한다.

#### for문
for 문은 조건식이 거짓으로 평가될 때까지 코드 블록을 반복 실행한다.

![image](https://velog.velcdn.com/images%2Fssonnni%2Fpost%2Fa18be522-c8b7-4714-8847-bd5101e692cd%2Ffor-statement.png)

#### while 문
while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복실행한다.
- 조건식의 평가 결과가 boolean 이 아니라면 boolena 값으로 강제 변환하여 논리적 참,거짓을 구별한다.

```js
var count = 0;

//count 가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3){
  console.log(count);
  count++;
}
```
```js
while(true){ ... }
```
조건식이 언제가 참으로 평가되도록 설정하면 무한루프를 만들 수 있다.
무한루프에서 탈출하기 위해서는 if 조건을 만들고 break 문을 사용하면된다.

```js
var count = 0;

while(true){
  console.log(count);
  count++

  //count 가 3이면 코드블럭을 탈출한다.
  if(count === 3)break;
}//0 1 2
```

<br>

### do while 문
do while 문은 코드블록을 먼저 실행하고 조건식을 평가한다. 따라서 코드블록은 무조건 한 번 이상 실행된다.
```js
var count = 0;

//count 가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.

do {
  console.log(count);
  count++;
} while(count < 3);
```


### break문
break 문은 레이블문, 반복문 또는 switch 문의 코드블록을 탈출한다. 이 문들 외에 break 문을 사용하면 SyntaxError 가 발생한다.

레이블문 : 식별자가 붙은 문 <br/>
foo 라는 식별자가 붙은 레이블문에서 break 문을 사용한 예시
```js
//레이블 문
foo: {
  console.log(1);
  break foo;
  console.log(2);
}

console.log('Done!');
```
중첩 for 문에서의 break 문 사용예시
```js
outer: for(var i = 0; i<3; i++){
  for(var j=0; j<3; j++){
    // i+j ===3 이면 outer 라는 식별자가 붙은 레이블 for문을 탈출한다.
    if(i+j ===3){
      break outer;
      console.log(`inner [${i}, ${j}]`);
    }
  }
}
console.log('Done!');
```

### continue 문
continue 문은 반복문의 코드블록 실행을 현 지점에서 중단하고 반복문의 조건 검사 위치로 이동한다. break 문처럼 반복문을 탈출하지는 않는다.

![](https://t1.daumcdn.net/cfile/tistory/99AA623359BFB0C31A)

```js
var string = 'Hello World';
var search = 'l';
var count = 0;

for(var i=0; i<string.length; i++){
  //'l' 이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++;//continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count);
```
String.prototype.match 메서드를 사용해도 같은 동작을 한다.
```js
const regxp = new RegExp(search, 'g');
console.log(string.match(regxp).length); //3
```

# 9장_타입변환과 단축 평가

## 타입변환
타입변환이란 기존 원시값을 사용해 다른 타입의 새로운 원시값을 생성하는 것이다.

### 명시적 타입변환
개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입변환** 또는 **타입캐스팅**이라 한다. 
```js
var x = 10;
var str = x.toString();
console.log(typeof str, str);

console.log(typeof x, x);
```

#### 문자열 타입으로 변환
- String 생성자 함수를 new 연산자 없이 호출하는 방법
```js
var number = 1;
var str = String(number);
```
String 생성자 함수는 입력값을 문자열로 변환하고 이를 반환한다. <br/>
`생성자 함수` :  JavaScript에서 객체를 생성하기 위해 사용되는 함수
- Object.prototype.toString 메서드를 사용하는 방법
```js
// 숫자 타입 => 문자열 타입
console.log((1).toString());        // "1"
console.log((NaN).toString());      // "NaN"
console.log((Infinity).toString()); // "Infinity"

// 불리언 타입 => 문자열 타입
console.log((true).toString());     // "true"
console.log((false).toString());    // "false"
```

- 문자열 연결 연산자를 이용하는 방법
```js
// 숫자 타입 => 문자열 타입
console.log(1 + '');        // "1"
console.log(NaN + '');      // "NaN"
console.log(Infinity + ''); // "Infinity"
// 불리언 타입 => 문자열 타입
console.log(true + '');     // "true"
console.log(false + '');    // "false"
```

#### 문자열 타입으로 변환
- Number 생성자 함수를 new 연산자 없이 호출하는 방법
- ParseInt, parseFloat 함수를 사용하는 방법(문자열만 변환가능)
```js
parseInt('0');
parseInt('10.53');
```
`parseInt()`: JavaScript에서 문자열을 정수로 변환하는 데 사용되는 내장 함수. 문자열의 시작 부분부터 숫자로 인식할 수 있는 부분까지만 변환하며, 만약 숫자가 아닌 문자가 나타나면 변환을 멈춘다.
```js
var nonNumericStr = "123abc";
var parsedNonNumeric = parseInt(nonNumericStr);

console.log(parsedNonNumeric); // 123 -> 변환을 멈춤
```
- + 단항 산술 연산자를 이용하는 방법
```js
// 문자열 타입 => 숫자 타입
console.log(+'0');     // 0
console.log(+'-1');    // -1
console.log(+'10.53'); // 10.53
// 불리언 타입 => 숫자 타입
console.log(+true);    // 1
console.log(+false);   // 0
```
-  산술 연산자를 이용하는 방법
```js
// 문자열 타입 => 숫자 타입
console.log('0' * 1);     // 0
console.log('-1' * 1);    // -1
console.log('10.53' * 1); // 10.53
// 불리언 타입 => 숫자 타입
console.log(true * 1);    // 1
console.log(false * 1);   // 0
```

#### boolean 타입으로 변환
- boolean 생성자 함수를 new 연산자 없이 호출하는 방법
```js
// 문자열 타입 => 불리언 타입
console.log(Boolean('x'));       // true
console.log(Boolean(''));        // false
console.log(Boolean('false'));   // true
// 숫자 타입 => 불리언 타입
console.log(Boolean(0));         // false
console.log(Boolean(1));         // true
console.log(Boolean(NaN));       // false
console.log(Boolean(Infinity));  // true
// null 타입 => 불리언 타입
console.log(Boolean(null));      // false
// undefined 타입 => 불리언 타 입
console.log(Boolean(undefined)); // false
// 객체 타입 => 불리언 타입
console.log(Boolean({}));        // true
console.log(Boolean([]));        // true
```

#### 부정연산자를 두번사용 !!
```js
// 문자열 타입 => 불리언 타입
console.log(!!'x');       // true
console.log(!!'');        // false
console.log(!!'false');   // true
// 숫자 타입 => 불리언 타입
console.log(!!0);         // false
console.log(!!1);         // true
console.log(!!NaN);       // false
console.log(!!Infinity);  // true
// null 타입 => 불리언 타입
console.log(!!null);      // false
// undefined 타입 => 불리언 타입
console.log(!!undefined); // false
// 객체 타입 => 불리언 타입
console.log(!!{});        // true
console.log(!![]);        // true
```

### 암묵적 타입변환

개발자의 의도와 상관없이 표현식을 평가하는 도중에  자바스크립트 엔진에 의해 암묵적으로 타입이 자동변환되는 것을 **암묵적 타입 변환** 또는 **타입 강제 변환** 이라 한다.
 - 암묵적 타입변환은 기존 변수 값을 재할당 하는 것이 아니다.
 - 자바스크립트 엔진은 표현식을 에러없이 평가하기 위해 피연산자의 값을 암묵적 타입 변환하여 새로운 타입의 값을 만들어 단 한번 사용하고 버린다.
```js
var str = x + '';
console.log(typeof str, str);
```

#### 문자열 타입으로 변환
```js 
// 숫자 타입
0 + ''              // "0"
-0 + ''             // "0"
1 + ''              // "1"
-1 + ''             // "-1"
NaN + ''            // "NaN"
Infinity + ''       // "Infinity"
-Infinity + ''      // "-Infinity"

// 불리언 타입
true + ''           // "true"
false + ''          // "false"

// null 타입
null + ''           // "null"

// undefined 타입
undefined + ''      // "undefined"

// 심볼 타입
(Symbol()) + ''     // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + ''           // "[object Object]"
Math + ''           // "[object Math]"
[] + ''             // ""
[10, 20] + ''       // "10,20"
(function(){}) + '' // "function(){}"
Array + ''          // "function Array() { [native code] }"
```
#### 숫자 타입으로 변환
```js
1 - '1'    // 0
1 * '10'   // 10
1 / 'one'  // NaN
```
위의 연산자는 산술연잔자이다. 산술연자의 모든 피연산자는 코드 문맥상 모두 숫자 타입이어야 한다.
자바스크립트 엔진은 숫자타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입변환하는데, 이때 타입변환이 불가한 경우 표현식의 평가결과는 NaN이된다.

```js
// 문자열 타입
+''             // 0
+'0'            // 0
+'1'            // 1
+'string'       // NaN

// 불리언 타입
+true           // 1
+false          // 0

// null 타입
+null           // 0

// undefined 타입
+undefined      // NaN

// 심볼 타입
+Symbol()       // TypeError: Cannot convert a Symbol value to a number

// 객체 타입
+{}             // NaN
+[]             // 0
+[10, 20]       // NaN
+(function(){}) // NaN
```

#### boolean 타입으로 변환
if 문이나 for 문 같은 제어문 또는 삼항 조건 연산자의 조건식은 참, 거짓으로 평가되어야하는 표현식이다. 따라서 이때 자바스크립 엔진은 boolean 타입이 아닌 값을 Truthy 한 값 또는 Falsy 한 값으로 구분한다.

* Falsy
  * false
  * undefined
  * null
  * 0, -0
  * NaN
  * ’’ (빈문자열)


### 단축평가
논리합(||) 연산자와 논리곱(&&) 연산자는 논리 연산의 결과를 결정하는 피연산자를 타입변환하지 않고 그대로 반환한다. 이를 단축평가 라고 한다. 단축평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.

#### 논리곱 연산자 (&&)
- 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다.
- 좌항에서 우항으로 평가된다.
```js
'Cat' && 'Dog'  // Dog
false && 'Dog'  // false
'Cat' && false  // false
```
논립곱(&&) 연산자의 if 문 대체
```js
var done = true;
var message = '';

message = done && '완료';
console.log(message); 
```
```js
var done = 0; //falsy
var message = '';

message = done && '완료';
console.log(message);
```
done이 false 로 평가되어 message 에는 0이 할당됨
```js
var falsy1 = 0;
var falsy2 = ''
var falsy3 = null;

var message = '';

message = falsy1 && falsy2 && falsy3 && '완료';
console.log(message); //0
```
논리곱연산자는 좌항에서 우항으로 평가되는데 첫번째로 평가되는 falsy1 이 falsy 한 값이기 때문에 message 에는 falsy1 값이 할당된다.

```js
var falsy1 = 0;
var falsy2 = '';
var falsy3 = null;

var truthy = true;

var message = '';

message = truthy && '완료'; 
console.log(message); //완료
```
모든 항이 true 로 평가되어 가장 우항의 true 값이 반환되었다.

```js
var falsy1 = 0;
var falsy2 = ''
var falsy3 = null;

var truthy = true;

var message = '';

message = truthy && falsy1 && '완료';
console.log(message); // >?
```
message 값은 무엇일까 ?
```js 
{isFetching && (
  <Backdrop open={isFetching}>
    <CircularProgress />
  </Backdrop>
)}
```
논리곱 연산자를 사용해 위와 같이 데이터가 fetching 될 때 (isFetching state 가 true 일때)
Backdrop을 랜더링한는 코드를 작성할 수 있다.

#### 논리합 연산자 (||)
- 두 개의 피연산자 중 하나만 true 로 평가되어도 true 를 반환한다.
- 논리합 연산자도 좌항에서 우항으로 평가가 진행된다.
```js
'Cat' || 'Dog'  // 'Cat'
false || 'Dog'  // 'Dog'
'Cat' || false  // 'Cat'
```

#### 단축평가 사용예제
1. 객체를 가리키는 변수가 null 또는 undefined 가 아닌지 확인
```js
var elem = null;
var value = elem && elem.value;
```

2. 함수 매개변수에 기본값을 설정할 때 <br/>
함수를 호출할 때 인수를 전달하지 않으면 매개변수는 undefined를 갖는다. 이때 단축 평가를 사용하여 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.
```js
function getStringLength(str) {
  str = str || '';
  return str.length;
}

getStringLength();     // 0
getStringLength('hi'); // 2

// ES6의 매개변수의 기본값 설정
function getStringLength(str = '') {
  return str.length;
}

getStringLength();     // 0
getStringLength('hi'); // 2
```

#### 옵셔널 체이닝 연산자
옵셔널 체이닝 연산자 ?. 는 좌항의 피연산자가 null 또는 undefined 인 경우 undefined 를 반환하고 그렇지 않은 경우 우항의 프로퍼티 참조를 이어간다.

```js
var str = '';
var length = str?.length;
console.log(length);
```
문자열 길이(length) 를 참조하는데 이때 좌항 피연산자가 false 로 평가되는 falsy 값이라도 null 또는 undefined 가 아니면 우항의 프로퍼티 참조를 이어간다.

#### null 병합 연산자
null 병합 연산자는 ?? 는 좌항의 피연산자가 null 또는 undefined 인 경우 우항의 피연산자를 반환하고 그렇지 않으면 좌항의 피연산자를 반환한다. 좌항의 피연산자가 false 로 평가되는 Falsy 한 값이라도 null 또는 undefined 가 아니라면 좌항의 피연산자를 그대로 반환한다.

- 변수에 기본값을 설정할 때 유용하다
```js
var foo = null ?? 'default string';
console.log(foo); // "default string"
```

