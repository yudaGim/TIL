# JavaScript

## 특징

- 자바의 문법과 비슷한 부분이 많음
- 객체 기반의 언어로 객체(Object) 개념이 있음
- 이미 정의되어 호출하면 사용할 수 있는 내장 객체가 존재
- 속성, 메소드 개념이 있어 객체명.속성명 or 객체명.메소드명()의 방식으로 호출할 수 있음
- new 키워드를 이용해 새로운 객체를 생성할 수 있음
- this 키워드를 통해 현재 객체 안의 속성과 메소드에 접근할 수 있음

## 적용 방법

### 인라인

```html
<element onclick="">content</element>
<!--
	요소에 직접 입력하는 방식
	동작에 맞춰 CSS를 바꾸는 등의 간단한 것만 가능함
-->
```

### 내부 자바스크립트 코드

```html
<script type="text/javascript">
	document.write("<h1 style="color=blue">내부 자바스크립트 코드</h1>");
<script>
<!--
	HTML의 script 태그 안에 코드를 입력하는 방식
	script 태그 안에 HTML과 CSS 모두 사용 가능
-->
```

### 외부 자바스크립트 코드

```html
<!-- HTML -->
<script type="text/javascript" scr="JS 파일 경로">
	<!-- 내부에 입력X: 입력해도 적용안됨 -->
<script>
```

```jsx
/* JavaScript */
<element onclick="">content</element>

/* 	외부 JS파일을 가져오는 방식 */
```

## 변수

### 선언 방법

```jsx
/* JS 변수 선언 방법 */

var 변수이름;
let 변수이름;
const 변수이름 = 값;
변수이름;
/*
	전역 변수의 경우 var, let, const 생략 가능
	지역 변수에서 생략할 경우 전역 변수로 생성됨
	but 변수가 생성된 함수가 호출된 뒤에만 전역 변수로 사용 가능
*/
```

### 특징

- JS는 값이 할당된 뒤에 변수의 타입이 결정됨(하나의 변수에 모든 타입의 변수 입력 가능)
- new로 생성한 변수는 무엇이 들어있든 Object 타입이 됨
- 초기화하지 않은 변수 타입과 값은 undefined로 설정됨
- 선호출 후생성 가능(생성 없이 호출만 할 경우 에러 발생) → 호이스팅 개념
but 선호출할 경우 변수 타입과 값은 undefined로 설정됨
- 호이스팅
    - 브라우저가 파일을 읽을 때 사용 여부와 관계없이 선언된 객체, 변수, 함수를 메모리에 미리 올리는 방식
    - 사용될 때 초기화 문장을 만나면 초기화함
    - 때문에 이름이 같을 경우 객체, 변수, 함수 등이 섞여 호출될 수 있음
    이를 막기 위해 let, const로 변수를 선언함
- let, const
    - let은 값 변경 가능
    - const(상수)는 생성 시 초기화 필수, 값 변경 불가
    - let, const 모두 변수 재선언, 선호출 후생성, 지역 변수 블럭 외 호출 불가
	
## 연산자

### 산술 연산자

```jsx
a + b // a에 b를 더함
a - b // a에서 b를 뺌
a * b // a와 b를 곱함
a / b // a를 b로 나눔
a % b // a를 b로 나눈 나머지를 구함
```

### 연결 연산자

```jsx
"a" + "b" // a에 b를 연결함
```

### 비교 연산자

```jsx
a == b // a와 b가 같으면 true
a != b // a와 b가 다르면 true
a < b // a보다 b가 크면 true
a <= b // a보다 b가 크거나 같으면 true
a > b // a보다 b가 작으면 true
a >= b // a보다 b가 작거나 같으면 true
```

### 대입 연산자

```jsx
a = b // a에 b를 대입
a += b // a에 b를 더해서 a에 대입
a -= b // a에서 b를 빼서 a에 대입
a *= b // a에 b를 곱해서 a에 대입
a /= b // a를 b로 나눠서 a에 대입
a %= b // a를 b로 나눈 나머지를 a에 대입
```

### 논리 연산자

```jsx
a && b // a와 b가 모두 true면 true
a || b // a와 b 중 하나가 true면 true 
a ^ b // a와 b의 값이 다르면 true
```

### 삼항 연산자

```jsx
(조건) ? 참일 때 결과 : 거짓일 때 결과
```

### 증감 연산자

```jsx
a++ // 실행 뒤 a에 1을 더함
++a // a에 1을 더한 뒤 실행
a-- // 실행 뒤 a에 1을 뺌
--a // a에서 1을 뺀 뒤 실행
```

### 연결 연산자

```jsx
`아바바바 ${변수}` 변수와 글자를 함께 쓸 때 사용 템플릿 문자열
```

## 제어문

### 조건문

- if문
    
    ```jsx
    // 자바와 if문 구성이 동일함
    
    if(조건문 1) { // 조건문 1이 true이면 실행문 1 실행
    	실행문 1;
    } else if(조건문 2) { // 조건문 1이 false고 실행문 2가 true면 실행문 2 실행
    	실행문 2;
    } else { // 조건문 1과 2 모두 false면 실행문 3 실행
    	실행문 3;
    }
    ```
    
- switch문
    
    ```jsx
    // 자바와 switch문 구성이 동일함
    
    switch(변수) {
    	case 값: // 변수와 값이 같으면 아래의 실행문 실행
    		실행문 1;
    		break;
    	case 값:
    		실행문 2;
    		break;
    	default: // 변수와 같은 값이 없으면 default 아래의 실행문 실행
    		실행문 3;
    }
    ```
    
### 반복문

- for문
    
    ```jsx
    // 자바와 for문 구성이 동일함
    
    for(초기값; 조건식; 증감식) { // 조건식이 true인 동안 실행
    	실행문;
    }
    ```

- 개선된 for문
    
    ```jsx
    // 자바와 달리 undefined가 아닌(=값이 들어있는) 인덱스의 숫자를 하나씩 꺼내옴
    
    for(let i in 배열명) { // 배열의 인덱스를 하나씩 꺼내옴
    	document.write(배열명[i]); // 배열의 값을 하나씩 꺼내 출력
    }
    ```

- do-while문
    
    ```jsx
    // 자바와 do-while문 구성이 동일함
    
    do { // 조건식이 true인 동안 실행하되, 조건식이 false여도 한 번은 실행
    	실행문;
    } while(조건식)
    ```
    
- switch문
    
    ```jsx
    // 자바와 switch문 구성이 동일함
    
    switch(변수) {
    	case 값:
    		실행문 1;
    		break;
    	case 값:
    		실행문 2;
    		break;
    	default:
    		실행문 3;
    }
    ```
    

## 함수

### 선언&호출 방법

```jsx
// 선언적 함수 선언
function 함수명(매개변수, 매개변수...){
	실행문;
	return 리턴값;
}

// 선언적 함수 호출
함수명; // 함수
함수명(); // 리턴값
// 매개변수의 갯수가 달라도 호출되기 때문에 오버로딩할 필요X
// 오버로딩할 경우 맨 마지막에 생성된 함수만 호출됨
```

```jsx
// 익명 함수 선언
let 변수명 = function(매개변수, 매개변수...){
	실행문;
	return 리턴값;
}

// 익명 함수 호출
result = 변수명; // 함수
result = 변수명(); // 리턴값
```

```jsx
// 람다식 함수 선언
let 변수명 = (매개변수, 매개변수...) => {
	실행문;
	return 리턴값;
}

// 람다식 함수 호출
result = 변수명; // 함수
result = 변수명(); // 리턴값
```

### 대화상자 함수

```jsx
alert("문자열"); // 대화상자로 문자열 출력
prompt("문자열", "초기값") // 프롬프트 창으로 문자열을 출력하고 문자열을 입력받음
confirm("문자열") // 대화상자로 문자열 출력 뒤 확인(true), 취소(false) 입력받음
```

### 문자 → 숫자 변환 함수

```jsx
Number(문자열);
/*
	문자열을 정수형으로 바꾸되, 문자가 섞여있을 경우 NaN(Not a Number)가 도출됨
*/

parseInt(문자열);
/*
	실수를 넣을 경우 소숫점을 머리고 정수형으로 바꿈
	문자열이 숫자일 경우 정수형으로 바꿈
	문자열이 숫자로 시작할 경우 이어지는 숫자만 추출해 정수형으로 바꿈
	문자열이 문자로 시작할 경우 NaN(Not a Number)가 도출됨
*/
```

### 일정 시간마다 특정 함수를 호출해주는 함수

```jsx
window.setTimeout("함수명()", ms);
/*
	입력한 ms가 지나면 입력한 함수를 한 번 호출해주는 함수
	재귀함수로 만들면 일정 시간마다 함수가 반복되도록 설정할 수 있음
*/

window.clearTimeout(대상);
/*
	setTimeout() 함수의 기능을 제거하는 함수
	setTimeout()을 변수에 넣고 그 변수를 clearTimeout()의 매개변수로 넣어야 함
*/

window.setInterval("함수명()", ms)
/*
	입력한 ms마다 입력한 함수를 호출해주는 함수
*/

window.clearInterval(대상);
/*
	setInterval() 함수의 기능을 제거하는 함수
	setInterval()을 변수에 넣고 그 변수를 clearInterval()의 매개변수로 넣어야 함
*/
```

### 날짜 함수

```jsx
let today = new Date(연, 원, 일, 시, 분, 초);
/*
	표준시 방식으로 날짜를 출력하는 함수
	매개변수를 입력하지 않으면 현재 날짜와 시간을 가져옴
*/

today.toLocaleString(); 
/*
	연.월.일 오전|오후 시:분:초 형식으로 날짜와 시간을 출력하는 함수
	today에 연월일 매개변수를 입력했을 경우 시간은 오전 12시 0분 0초로 출력됨
*/

today.getFullYear(); // 연도를 출력하는 함수
today.getMonth(); // 월을 출력하는 함수(0부터 시작)
today.getDay(); // 요일을 출력하는 함수(일=0부터 시작)
today.getDate(); // 일자를 출력하는 함수

today.getHours(); // 시간을 출력하는 함수(24시간제로 출력)
today.getMinutes(); // 분을 출력하는 함수
today.getSecond(); // 초를 출력하는 함수

today.setFullYear(); // 변수에 저장된 연도를 변경하는 함수
today.setMonth(); // 변수에 저장된 월을 변경하는 함수
today.setDay(); // 변수에 저장된 요일을 변경하는 함수
today.setDate(); // 변수에 저장된 일자를 변경하는 함수

today.setHours(); // 변수에 저장된 시간을 변경하는 함수
today.setMinutes(); // 변수에 저장된 분을 변경하는 함수
today.setSecond(); // 변수에 저장된 초를 변경하는 함수
```

### 문자열 → 코드 변환 함수

```jsx
eval("문자열");
/*
	인수로 들어온 문자열을 JS 코드로 만듦
	어떤 코드가 들어가도 JS 코드로 만들기 때문에 보안에 취약해 권장X
*/

new Function("return 문자열")();
/*
	문자열을 JS 코드로 만듦
	eval() 대체용으로 사용
*/
```

## 배열

### 특징

- 배열의 크기가 가변적: 생성 시 크기보다 자료를 적게, 혹은 많이 저장할 수 있음
- 하나의 배열에 모든 타입의 데이터를 혼용해 넣을 수 있음
- 배열 안에 배열을 넣어 2차원 배열로 사용 가능

### 배열 생성 방법

```jsx
배열명 = new Array(n); // 크기가 n인 배열 생성
배열명 = new Array(값, 값, 값); // 값을 초기화하며 크기가 3인 배열 생성
배열명 = [값, 값, 값]; // 값을 초기화하며 크기가 3인 배열 생성
```

### 배열에 값 입력

```jsx
배열명[n] = 값; // 배열의 n번째 자리에 값 입력
배열명.push(값); // 배열의 끝에 값 추가
```

## DOM 접근

### 네임값으로 접근

```jsx
document.name값[.name값 ...]; // name값으로 접근
```

### 속성값으로 접근

```jsx
document.getElementByClass("class값"); // class 값으로 접근
document.getElementById("id값"); // id 값으로 접근
document.getElementsByName("name값"); // name 값으로 접근
document.getElementsByTagName("tagName값"); // tagName 값으로 접근
```

### 특정 노드 기준으로 접근

```jsx
기준 노드.parentNode; // 부모 노드 접근
기준 노드.childNodes; // 자식 노드 리스트 접근
기준 노드.firstChild; // 첫 번째 자식 노드 접근
기준 노드.lastChild; // 마지막 자식 노드 접근
기준 노드.previousSibling; // 이전 형제 노드 접근
기준 노드.nextSibling; // 다음 형제 노드 접근
```

### img 접근

```jsx
document.images[index]; // html 파일 내의 모든 이미지를 선언순대로 배열로 만들어 접근
document.name값; // img name 속성의 값으로 접근 
/* 매개변수로 name값을 받을 때 "name값"으로 따옴표를 사용해 넘기면 new Function을 사용해 변환해야 하므로 주의 */
```

## DOM 생성

### 일반 태그 생성

1. 태그 생성
    
    ```jsx
    let x = document.createElement("tag명");
    // 추가하고 싶은 태그를 생성함
    ```
    
2. text 생성
    
    ```jsx
    let txt = document.createTextNode("문자열");
    // 태그 사이에 입력할 문자열을 생성함
    ```
    
3. 자식 노드 추가
    
    ```jsx
    x.appendChild(txt);
    // 문자열을 태그 안에 추가함
    
    부모 노드.appendChild(x);
    // 태그를 원하는 위치에 추가함
    ```
    
4. 결과
    
    ```html
    <태그명>문자열</태그명>
    <!-- HTML에 나타나는 결과 -->
    ```
    

### 테이블 생성

```jsx
// id값이 있는 테이블에 tr, td 추가

let row = 테이블id값.insertRow(0); // tr행 생성

let td1 = row.insertCell(0); // td열 생성
let td2 = row.insertCell(1); // td열 생성
let td3 = row.insertCell(2); // td열 생성

td2.innerHTML = "두 번째 td";
```

```html
<!-- 결과 -->
<table id="ta">
  <tr>
    <td></td>
    <td>두 번째 td</td>
    <td></td>
  </tr>
</table>
```

## DOM 삭제

```jsx
부모 노드.removeChild(삭제할 노드);
```

## DOM 메소드

```jsx
부모 노드.hasChildNodes() // 자식 노드 존재 여부를 가져옴

부모 노드.removeChild() // 자식 노드 삭제

부모 노드.replaceChild() // 자식 노드를 다른 노드로 교체

노드.settAttribute(속성명, 속성값) // 노드의 속성 추가

노드.getAttribute(속성명) // 노드의 속성 값 조회
```

## HTML 적용

### div, span에 텍스트 입력

```jsx
적용할 대상.innerText = "텍스트"; // 대상에 텍스트를 입력하되, 태그 적용X
적용할 대상.innerHTML = "텍스트"; // 태그를 적용해 텍스트 입력, DOM 생성법 대신 사용 가능
```

### form 조작

- input text
    
    ```jsx
    적용할 대상.value; // input text에 입력된 텍스트 가져오기
    적용할 대상.value = "텍스트"; // input text에 값 입력
    ```
    
- input radio/check
    
    ```jsx
    radioCheckName값; // name값이 같은 라디오/체크 버튼을 리스트로 가져옴
    radioCheckName값[n]; // name값이 같은 라디오/체크 버튼 중 n번째 체크 버튼을 가져옴
    
    radioCheckName값[n].check; // n번째 라디오/체크 버튼의 선택 여부를 가져옴
    radioCheckName값[n].value; // n번째 라디오/체크 버튼의 밸류값을 가져옴
    ```
    
- select
    
    ```jsx
    select.length; // select의 옵션의 갯수를 가져옴
    
    select.value; // select에서 선택한 옵션의 value값을 가져옴
    select[n].value; // select에서 n번째 옵션의 value값을 가져옴
    
    select.selectedIndex; // select에서 선택한 옵션의 index값을 가져옴
    
    select.options[n] = new Option("값", "value값"); // select의 n번째 옵션을 추가/덮어쓰기함
    
    select.options[n] = null; // select의 n번째 옵션을 삭제함
    ```

- submit, reset
    
    ```html
    <form onsubmit="return false" onreset="return false">
    	<input type="submit">
    	<input type="reset">
    	<!--
    		submit과 reset은 input이 아니라 form에 함수를 적용함
    		onsubmit과 onreset에서 false가 리턴되면 submit과 reset을 실행하지 않음
    		(함수에서만 리턴하면 적용X onsubmit, onreset에서 다시 처리해야 적용)
    	-->
    </form>
    ```
    
    ```html
    <!-- button을 submit 버튼, reset 버튼으로 만들기	-->
    <form>
    	<input type="button" onclick="submitBtn(form)">
    	<input type="button" onclick="resetBtn(form)">
    </form>
    	
    <script type="text/javascript">
    	function submitBtn(fr) {
    		fr.action="경로"; // 폼 액션 변경
    		fr.submit(); // 폼 전송
    	}
    	function resetBtn(fr) {
    		fr.reset(); // 폼 초기화
    	}
    </script>
    ```

### image

- img 변경
    
    ```jsx
    적용할 대상.src = "경로"; // 대상 이미지를 경로 이미지로 변경함
    
    적용할 대상.width = "너비"; // 대상 이미지의 html 너비를 변경함
    적용할 대상.height = "높이"; // 대상 이미지를 html 높이를 변경함
    ```

### event 등록

```jsx
onload = function() { // HTML이 로드되었을 때 실행
	document.getElementById("id값").on이벤트종류 = 함수명; // 함수 호출 시 반드시 () 생략

	document.getElementById("id값").on이벤트종류 = function() {
		실행문;
	} // 익명 함수 선언도 가능
}
```

## CSS 적용

```jsx
적용할 대상.style.속성 = "값";
```

## 창 제어

### 새 창 열기

```jsx
window.open("경로", "이름", "속성", replace);
// a 태그와 달리 새 창에 다양한 속성을 부여할 수 있음
```

### 새 창에서 부모창 접근

```jsx
opener.부모창 요소;
// open() 함수를 통해 열린 새 창에서는 opener를 이용해 부모창에 있는 요소에 접근할 수 있음
```

### iframe 창 제어

```html
<a target="name값"></a>
<!-- HTML만 사용할 경우: a 태그의 target값으로 iframe 영역의 name값을 입력하면 해당 iframe에서 경로가 열림 -->

<a onclick="top.name값.location.href='경로'"></a>
<!-- JS에서 location.href를 사용할 경우: 상위 부모 페이지로 올라간 후 name값을 입력해야 해당 iframe에서 경로가 열림 -->
```

## 주요 BOM

### window 객체

```jsx
```

### location 객체

```jsx
location.href;
/*
	현재 페이지의 url을 가져옴
*/

location.replace("경로");
/*
	현재 페이지의 url을 입력한 경로로 변경함
*/

location.reload();
/*
	현재 페이지를 새로고침함
*/
```

### history 객체

```jsx
history.go(n);
/*
	현재 페이지를 기준으로 현재 탭이 기억하고 있는 앞 n단계 페이지로 이동함
	-n을 입력할 경우 뒷 n단계 페이지로 이동함
*/

history.forward();
/*
	현재 탭이 기억하고 있는 앞 페이지로 이동함
*/

history.back();
/*
	현재 탭이 기억하고 있는 뒷 페이지로 이동함
*/
```

### navigator 객체

```jsx
navigator.userAgent;
/*
	현재 브라우저의 정보를 가져옴
*/
```

### screen 객체

```jsx
screen.width;
/*
	현재 스크린(=화면)의 너비를 가져옴
*/

screen.height;
/*
	현재 스크린(=화면)의 높이를 가져옴
*/
```

## Web Storage

### localStorage

- 만료 기간이 없어 평생 유지됨
- 저장
    
    ```jsx
    localStorage.setItem(key, value);
    // 로컬 스토리지에 키와 밸류 저장
    ```
    
- 호출
    
    ```jsx
    localStorage.length;
    // 로컬 스토리지에 저장된 키와 밸류 갯수 가져오기
    
    localStorage.key(i);
    // i번째 키값 가져오기
    
    localStorage.getItem(key);
    // key에 해당하는 밸류값 가져오기
    ```
    
- 삭제
    
    ```jsx
    localStorage.removeItem(key);
    // key값에 해당하는 키와 밸류 삭제
    
    localStorage.clear();
    // 로컬 스토리지에 저장된 키와 밸류 모두 삭제
    ```
    

### sessionStorage

- 세션이 유지되는 동안(해당 탭이나 창을 완전히 종료할 때까지) 유지됨
- 저장
    
    ```jsx
    sessionStorage.setItem(key, value);
    // 세션 스토리지에 키와 밸류 저장
    ```
    
- 호출
    
    ```jsx
    sessionStorage.length;
    // 세션 스토리지에 저장된 키와 밸류 갯수 가져오기
    
    sessionStorage.key(i);
    // i번째 키값 가져오기
    
    sessionStorage.getItem(key);
    // key에 해당하는 밸류값 가져오기
    ```
    
- 삭제
    
    ```jsx
    sessionStorage.removeItem(key);
    // key값에 해당하는 키와 밸류 삭제
    
    sessionStorage.clear();
    // 세션 스토리지에 저장된 키와 밸류 모두 삭제
    ```