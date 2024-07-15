# 1. 개요(ECMAScript) 및 프로젝트 초기화

* ECMAScipt(ES, 이크마스크립트): Ecma International이 ECMA-262 기술 규격에 따라 정의하고 있는 표준화된 스크립트 프로그래밍 언어
* ES6는 ES5에 비해 다양한 새로운 기능들이 추가되어, 더 간결하고 효율적인 JavaScript 코드 작성이 가능
	* ES5는 2009년에 발표된 JavaScript 표준으로, 대부분의 브라우저에서 지원됨
	* ES6는 2015년에 발표된 JavaScript 표준으로, 지원하는 브라우저가 ES5에 비해 제한적임
		* IE 11과 같은 구형 브라우저에서는 ES6를 지원하지 않음
	* 그외 [ES5와 ES6의 차이점](https://doozi0316.tistory.com/entry/JavaScript-ECMAScript%EB%9E%80-ES5%EC%99%80-ES6%EC%9D%98-%EC%B0%A8%EC%9D%B4var-const-let-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98-class)
* 구형 브라우저 지원이 필요하다면 ES5 문법을 사용하거나, Transpiler나 Polyfill을 활용해야 함

## 테스트 프로젝트 생성

1. 프로젝트 디렉터리 생성

2. `package.json` 생성
```ternimal
	npm init -y
```

3. 패키지 설치
```ternimal
	npm install parcel-bundler -D
```

4. `package.json`의 `scripts`에 명령어 추가
```json
"scripts": {           // 현재 프로젝트에서 사용할 수 있는 명령어를 생성하는 공간
"dev": "parcel index.html",
"build": "parcel build index.html"
},
```

5. 프로젝트 디렉터리에 `index.html` 파일 생성

6. `index.html`에서 `!(느낌표)` 입력 후 `tab 키`를 눌러 자동완성하기

7. `<title>` 태그 아래에 `<script>` 태그 생성 후 아래와 같이 src 작성하기
```html
	<!-- index.html -->
	<script src="./main.js"></script>
```

8. 프로젝트 디렉터리에 `main.js` 파일 생성
```js
	// main.js
	console.log('hello world');
```

9. `npm run dev` 명령어로 `index.html` 실행
* http:// localhost:1234 클릭시 브라우저로 이동
* `^C` 입력시 종료


# 2. 데이터 타입 확인

> [!NOTE] **코드 컨벤션 (Code Convention)**
> 읽고 관리하기 쉬운 코드를 작성하기 위한 일종의 코딩 스타일 규약(하나의 작성 표준)
> ex. 세미콜론으로 명령이 끝난 것 명시하기, 한줄에 하나의 명령만 작성하기

1. typeof 키워드를 사용해 데이터의 타입을 확인 가능
```js
console.log(typeof 'hello world'); // string
console.log(typeof 1234);          // number
console.log(typeof true);          // boolean
console.log(typeof undefined);     // undefined: 의도하지 않은 비어있는 값
console.log(typeof null);          // object -> null은 의도해서 비워놓은 값
console.log(typeof {});            // object -> {} 객체 데이터는 object
console.log(typeof []);            // object -> [] 배열 데이터는 object
```

2. object 타입의 데이터의 타입을 정확하게 구분하기 위한 함수 만들기
```js
function getType(data) {
	return Object.prototype.toString.call(data);
}

console.log(getType(1234));          // [object Number]
```

```js
function getType(data) {
	return Object.prototype.toString.call(data).slice(8, -1);
}

console.log(getType(1234));          // Number
console.log(getType(false));         // Boolean
console.log(getType(undefined));     // Undefined
console.log(getType(null));          // Null
console.log(getType({}));            // Object
console.log(getType([]));            // Array
```

3. 2번에 만든 함수를 모듈로 만들기 (모듈 내보내고 가져오기)
	1. 모듈 내보내기
		* 변수나 함수, 클래스를 선언할 때 맨 앞에 `export`를 붙이면 내보내기 가능
		* 함수나 클래스 선언 끝에 세미콜론을 붙이지 말것을 권장 -> `export`도 동일
	```js
// getType.js
export default function getType(data) {
	return Object.prototype.toString.call(data).slice(8, -1);
}
	```

	2. 모듈 가져오기
		* `import`를 통해 가져오기 가능
		* `'./getType'`와 같이 정확한 경로를 명시해줄 것
		* `'getType'`와 같이 정확한 상대경로를 정확하게 명시해주지 않으면 `'getType'`를 `node-modules`라는 폴더 안에서 찾아서 오류가 남
	```js
// main.js
import getType from './getType'
	```

* [자세한 정보](https://ko.javascript.info/import-export#ref-4122)


# 3. script 태그
* HTML에서 `<script>` 태그는 JavaScript 코드를 포함하는데 사용
* 이 태그를 사용하면 웹 페이지에 동적인 기능을 추가 가능

**`<script>` 태그의 주요 용도**
1. **JavaScript 코드 삽입**: `<script>` 태그 안에 JavaScript 코드를 작성하여 웹 페이지에 삽입
2. **외부 JavaScript 파일 포함**: `src` 속성을 사용하여 외부 JavaScript 파일 가져오기
3. **스크립트 실행 시점 설정**: `async` 또는 `defer` 속성을 사용하여 스크립트 실행 시점 조절
4. **스크립트 유형 지정**: `type` 속성을 사용하여 스크립트의 유형을 지정, 대부분의 경우 `text/javascript`를 사용
    
## 스크립트 실행 시점 설정
1. `<head>` 태그 안에 `<script src=" ">` 태그를 포함시킨 경우
	```mermaid
	flowchart LR
		A[HTML파싱] -.- B;
		B[파싱 멈춤 / blocked]-.- E;
		A --> C;
		C[JS다운] --> D;
		D[JS실행] --> E;
		E[HTML파싱] --> F[DOM 생성 완료];
	```

	1. 브라우저는 HTML을 쭉 읽다가 `<script>` 태그를 만나면 스크립트를 먼저 실행해야 되므로 HTML 파싱(DOM 생성)을 멈춘다.
	2. 필요한 .js 파일을 서버에서 받아와 다운로드 후 실행한.
	3. 다시 HTML 파싱을 시작한다.
	4. 모든 DOM 생성이 완료된다.
	
	* 스크립트 파일 용량이 크거나 인터넷 환경이 느린 경우에 페이지 로딩이 길어질 수 있는 문제가 발생
	* `<script>` 태그 아래의 DOM 요소를 접근하는 코드가 있을 경우, JavaScript가 먼저 실행됐기 때문에 DOM 요소에 접근이 불가능


2. `<body>` 태그 안에 `<script src=" ">` 태그를 포함시킨 경우
	```mermaid
	flowchart LR
		A[HTML파싱] --> B;
		B[DOM 생성 완료] --> C;
		C[JS다운] --> D[JS실행];
	```
	1. 브라우저가 HTML을 파싱한다.
	2. 모든 DOM 생성이 완료된다.
	3. `<script>` 태그를 읽고 .js 파일을 서버에서 받아와 다운로드 후 실행한다.

	* HTML 문서가 매우 큰 경우, 브라우저가 HTML 문서 전체를 다운로드 한 다음에 스크립트를 다운 받는다면 페이지가 느려진다.
	* 또한 웹 페이지가 JavaScript에 의존적인 페이지라면 이 역시 느려진다.

<font color="#00b050">1번과 2번 문제 해결 방법 -> `async`와 `defer` 사용</font>
3. `<head>` 태그 안에 `<script async src=" ">` 태그를 포함시킨 경우
	```mermaid
	flowchart LR
		A[HTML파싱 + JS다운] -.- B;
		B[파싱 멈춤 / blocked]-.- E;
		A --> D;
		D[JS실행] --> E;
		E[HTML파싱] --> F[DOM 생성 완료];
	```
	1. 브라우저가 HTML을 파싱한다.
	2. `<script>` 태그를 읽고 .js 파일을 서버에서 받아와 '백그라운드'에서 다운로드한다. 따라서 스크립트 파일을 다운로드하는 도중에도 HTML 파싱이 멈추지 않는다.
	3. JavaScript가 실행이 되면 HTML 파싱을 멈춘다.
	4. 실행 후 나머지 HTML을 파싱한다.
	5. 모든 DOM 생성이 완료된다.

	* async(비동기) 속성이 붙은 스크립트는 페이지와 완전히 독립적으로 동작 -> 스크립트 파일을 다운로드하는 동안 HTML 파싱을 하기때문에 다운로드 시간을 줄어든다.
	* 그러나 JavaScript를 실행할 때 HTML 파싱이 멈추기 때문에 페이지가 느릴 수 있다. 
	* 또한 `<script>` 태그의 파일이 여러개인 경우, 실행 순서의 보장 없이 먼저 로드된 것이 먼저 실행된다.
		* `script.async = false`로 설정해주면, 추가한 순서대로 실행된다.

> [!NOTE] 적합한 사례
> 비동기 스크립트는 방문자 수 카운터나 광고 관련 스크립트처럼 각각 독립적인 역할을 하는 서드 파티 스크립트를 현재 개발 중인 스크립트에 통합하려 할 때 아주 유용하다. async 스크립트는 개발 중인 스크립트에 의존하지 않고, 그 반대도 마찬가지이기 때문이다. - 모던 자바스크립트 튜토리얼

4. `<head>` 태그 안에 `<script defer src=" ">` 태그를 포함시킨 경우
	```mermaid
	flowchart LR
		A[HTML파싱 + JS다운] --> B;
		B[DOM 생성 완료] --> C[JS실행];
	```
	1. 브라우저가 HTML을 파싱한다.
	2. async와 마찬가지로 `<script>` 태그를 읽고 .js 파일을 서버에서 받아와 '백그라운드'에서 다운로드한다. 스크립트 파일을 다운로드하는 도중에도 HTML 파싱을 한다.
	3. 모든 DOM 생성이 완료된다.
	4. JavaScript가 실행된다.

	* `<script>` 태그의 파일이 여러개인 경우 순서대로 실행이 된다.
	* 4가지의 경우 중에 defer 속성이 안정적이고 일반적인 경우에 자주 쓰인다고 볼 수 있다.
		
> [!NOTE] async와 defer의 공통점
> async와 defer 스크립트는 다운로드 시 페이지 렌더링을 막지 않는다는 공통점이 있다. 따라서 async와 defer를 적절히 사용하면 사용자가 오래 기다리지 않고 페이지 콘텐츠를 볼 수 있게 할 수 있다. - 모던 자바스크립트 튜토리얼

* [참고자료1](https://onlydev.tistory.com/16)
* [참고자료2](https://jake-seo-dev.tistory.com/400)
