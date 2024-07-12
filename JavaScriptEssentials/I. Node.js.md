# 1. Node.js
* JavaScript 런타임 환경
* 브라우저 외부에 JavaScript를 실행할 수 있게 해주는 플랫폼

## JavaScript가 동작할 수 있는 환경
* node.js가 설치된 컴퓨터
* 웹 브라우저

## Node.js 버전
* 짝수 버전: LTS(Long Term Supported), 안정되고 신뢰도가 높음 -> 상용화 개발에 적합
* 홀수 버전: 가장 최신 버전 -> 신규 기능을 사용할 수 있으나 업데이트 필요


# 2. NVM(Node Version Manager)
* NVM은 Node.js의 버전을 관리하고 전환할 수 있는 도구
* NVM을 사용하면 시스템에 영향을 주지 않고 Node.js 버전을 독립적으로 관리 가능

## mac nvm 설치하기
1. brew를 사용하여 nvm 설치
	```ternimal
	brew install nvm
	```

2. `.nvm` 디렉터리 생성
	```ternimal
	mkdir ~/.nvm
	```

3. zsh를 사용하는 경우 `.zshrc`에 아래와 같이 경로 연결
	```ternimal
	vim ~/.zshrc
	```
	
	bash를 사용하는 경우 `.bash_profile` 수정
	```ternimal
	vim ~/.bash_profile
	```

	```ternimal
	export NVM_DIR="$HOME/.nvm"
	[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \."/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
	[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion​
	```

4. zsh를 사용하는 경우 `.zshrc` 업데이트
	```ternimal
	source ~/.zshrc
	```
		
	bash를 사용하는 경우 `.bash_profile` 업데이트
	```ternimal
	source ~/.bash_profile
	```

## nvm을 사용하여 node.js 설치 및 활용하기
1. node.js 최신 LTS 버전을 확인하여 설치
	```ternimal
	nvm install 20.15.1
	```

2. 설치된 버전 확인
	```ternimal
	nvm ls
	```

3. 사용할 버전 선택 및 변경
	```ternimal
	nvm use 20.15.1
	```

4. 지금 사용중인 버전 확인
	```ternimal
	node --version
	```

5. node.js 삭제
	```ternimal
	nvm uninstall 20.15.1
	```

<font color="#00b050">* 프로젝트에 따라 적합한 버전을 사용하기</font>


# 3. NPM(Node Package Manager)
* Node.js의 가장 큰 패키지 관리자
* Node.js와 함께 기본적으로 설치되며, 새로운 패키지를 검색하고 설치하는 데 사용

1. `package.json` 생성
```ternimal
	npm init -y
```


```json
// package.json
{
"name": "test",        // 프로젝트명
"version": "1.0.0",    // 프로젝트 버전
//"main": "index.js",    // 현재 프로젝트를 하나의 패키지로 만들 때 사용(웹사이트 개발시 필요X)
"scripts": {           // 현재 프로젝트에서 사용할 수 있는 명령어를 생성하는 공간
"test": "echo \"Error: no test specified\" && exit 1"
},
"keywords": [],        // 키워드(패키지 생성시 검색할 키워드)
"author": "",          // 생성자
"license": "ISC",      // 라이센스(패키지 생성시에는 명시하는 것이 좋음)
"description": ""      // 프로젝트 설명(패키지 생성시 보여줄 설명)
}
```

> [!NOTE] package.json
> 1. 프로젝트 정보 관리
>	- package.json 파일에는 메타데이터가 포함된다. (프로젝트의 이름, 버전, 설명, 저자 등)
>	- 프로젝트에 대한 기본 정보 확인 가능
>2. 종속성 관리
>	- 프로젝트에 필요한 외부 패키지(라이브러리, 프레임워크 등)의 정보 저장
>	- 프로젝트의 종속성 버전을 관리할 수 있어 안정적인 개발 환경을 유지 가능
>3. 스크립트 관리
>	- 프로젝트의 스크립트 명령(npm run 명령) 정의 가능 -> 쉬운 프로젝트 실행과 관리
>4. 배포 및 공유
>	- 프로젝트의 모든 정보를 포함 -> 쉬운 프로젝트 배포와 공유 가능

2. 패키지 설치: -D 사용 (ex. parcel-bundler)
```ternimal
	npm install parcel-bundler -D
```

* node_nodules 디렉터리에 패키지 관련 파일이 생성됨
* 아래와 같이 package.json에 설치한 패키지 내역이 추가됨
	* node_nodules 디렉터리를 삭제하더라도 `npm i` or `npm install` 명령어 입력시 아래의 `devDependencies`의 설치된 패키지 목록을 토대로 패키지가 다시 설치됨
* -D를 붙이면 `devDependencies`에 설치됨
	* 개발용 의존성 패키지 설치(웹브라우저에서 직접 동작X)
	* -D: --save-dev의 약어

```json
// package.json
"devDependencies": {  // 설치된 패키지 목록
"parcel-bundler": "^1.12.5"  // 설치된 패키지명: 버전
}
```

3. 패키지 설치: -D 미사용 (ex. lodash)
```ternimal
	npm install lodash
```

* 아래와 같이 package.json에 설치한 패키지 내역이 추가됨
* -D를 붙이지 않으면 `dependencies`에 설치됨
	* 일반 의존성 패키지 설치(웹브라우저에서 직접 동작O)

```json
// package.json
"dependencies": {  // 설치된 패키지 목록
"lodash": "^4.17.21"  // 설치된 패키지명: 버전
}
```

> [!NOTE] package.json vs package-lock.json
> * package.json : 직접 관리 필요
> * package-lock.json : 자동으로 관리되는 파일, package.json에 명시된 설치된 패키지들이 내부적으로 사용하는 패키지들이 자동으로 관리되는 파일 


# 4. 프로젝트 생성

1. 프로젝트 디렉터리에 `index.html` 파일 생성

2. `index.html`에서 `!(느낌표)` 입력 후 `tab 키`를 눌러 자동완성하기

3. `<title>` 태그 아래에 `<script>` 태그 생성 후 아래와 같이 src 작성하기
```html
	<!-- index.html -->
	<script src="./main.js"></script>
```

4. 프로젝트 디렉터리에 `main.js` 파일 생성
```js
	// main.js
	console.log('hello world');
```

6. `package.json`의 `scripts`에 명령어 추가
```json
"scripts": {           // 현재 프로젝트에서 사용할 수 있는 명령어를 생성하는 공간
"dev": "parcel index.html"
},
```

> [!NOTE] Bundler?
> * 설치한 패키지들을 html, css, javascript 로 변환시켜 주는 역할을 하는 것
> * **parcel-bundler**
> 	* Zero Configuration 지원 -> 설정이 거의 필요하지 않음
> 	* 빠른 번들링 속도 + Hot Module Replacement(HMR) 기능 -> 빠른 개발 속도
> 	* 대부분의 웹 애플리케이션에 필요한 기본적인 기능으로 구성
> 	* 빠른 개발 속도가 필요한 소규모 프로젝트나 개인 개발자에게 적합
> * **webpack**
> 	* 복잡한 설정 파일(webpack.config.js) 필요
> 	* 상대적으로 느린 번들링 속도
> 	* 풍부한 플러그인 생태계 -> 다양한 기능 제공
> 	* 복잡한 프로젝트나 대규모 팀에 적합

7. `npm run dev` 명령어로 `index.html` 실행
```terminal
node-test % npm run dev

> test@1.0.0 dev
> parcel index.html

Server running at http://localhost:1234 
✨  Built in 580ms.

```
* http:// localhost:1234 클릭시 브라우저로 이동
* `^C` 입력시 종료

8. 일반 의존성 패키지 사용하기
	* `main.js`에 아래와 같이 추가하기
```js
	import _ from 'lodash'  
	// node_modules 디렉터리의 
	// lodash 패키지의 package.js 파일에 명시된 main 옵션의 lodash.js를 가져와
	// _(언더바)라는 이름의 변수에 할당해 사용한다
	
	console.log(_.camelCase('hello world'));
	// lodash 패키지의 camelCase() 기능을 출력 -> helloWorld
```

9. 사용자 브라우저 내용 확인하기
	* `package.json`의 `scripts`에 명령어 추가
```json
"scripts": {           // 현재 프로젝트에서 사용할 수 있는 명령어를 생성하는 공간
"build": "parcel build index.html"
},
```

> [!NOTE] parcel vs parcel build
> * parcel: 로컬 환경에서 개발용으로 프로젝트를 열어 확인하는 것
> * parcel build: 사용자가 보는 브라우저 화면을 확인하는 것


```terminal
npm run build

> test@1.0.0 build
> parcel build index.html

✨  Built in 2.46s.

dist/main.430bf9be.js.map    715.81 KB     26ms
dist/main.430bf9be.js         92.81 KB    1.79s
dist/index.html                  221 B    590ms
```
* `dist` 디렉터리가 생성됨
* 디렉터리 안에 `main.430bf9be.js.map` 파일, `main.430bf9be.js` 파일, `index.html` 파일이 생성됨
	* 난독화: 파일들은 공백을 제거해 용량을 줄인 압축 버전으로 사용자에게 제공
	* parcel-bundler의 역할 확인 가능: 개발용으로 활용해서 결과만 사용자에게 제공


# 5. 유의적 버전(Semantic Versioning, SemVer)
* 의존성 네트워크를 관리하는 가장 대표적인 방법
* 유의적 -> 의미가 존재
* 숫자 세 개로 표현, 세 숫자는 차례로 Major, Minor, Patch 버전을 의미
	* **Major**: 새로운 버전 -> 기존 버전과 호환X
	* **Minor**: 새로운 기능이 추가된 버전 -> 기존 버전과 호환O
	* **Patch**: 버그 및 오타 등이 수정된 버전 -> 기존 버전과 호환O
	* ^Major.Minor.Patch: Major 버전 안에서 가장 최신 저번으로 업데이트 가능
		* npm update ->  Major 버전만 유지, Minor와 Patch 버전 업데이트
		* ^: 캐럿 기호
		* 캐럿 기호를 제거하면 버전을 유지할 수 있음
	* ~Major.Minor.Patch: Patch 버전 안에서 자동 업데이트
		* ~: 틸드

* 버전 확인 방법
```terminal
node --version
v20.15.1
// Major: 호환되지 않은 버전이 20개 존재
// Minor: 새로운 기능이 추가된 버전이 15개 존재
// Patch: 1번의 버그 및 오타 등이 수정됨

npm --version
10.7.0
```

* 의존성 패키지의 정보 확인
	* latest 버전은 node_modules > lodash > package.json의 version 정보의 설치된 버전과 다를 수 있음
```terminal
npm info lodash

lodash@4.17.21 | MIT | deps: none | versions: 114
Lodash modular utilities.
https://lodash.com/

keywords: modules, stdlib, util

dist
.tarball: https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz
.shasum: 679591c564c3bffaae8454cf0b3df370c3d6911c
.integrity: sha512-v2kDEe57lecTulaDIuNTPy3Ry4gLGJ6Z1O3vE1krgXZNrsQ+LFTGHVxVjcXPs17LhbZVGedAJv8XZ1tvj5FvSg==
.unpackedSize: 1.4 MB

maintainers:
- mathias <mathias@qiwi.be>
- jdalton <john.david.dalton@gmail.com>
- bnjmnt4n <benjamin@dev.ofcr.se>

dist-tags:
latest: 4.17.21 // 최신 버전

published over a year ago by bnjmnt4n <benjamin@dev.ofcr.se>
```

* ex. 한 단계 낮은 Patch 버전 다운로드
```terminal
npm install lodash@4.17.20
```


# 6. NPM 프로젝트의 버전 관리(.gitignore)
* `.gitgnore` 파일에 추가할 내용
	* 이유: 자동으로 관리되고 있고 용량이 커서 따로 관리할 필요가 없음
	
```
.cache/
dist/
node_modules/
```

## git 파일 관리 시작하기

1. git 초기화
```shell
git init
```

2. git add
```shell
git add 파일명 // 특정 파일만 add
git add .    // 모든 파일 add
```

3. git 상태 확인
```shell
git status
```

4. git commit
```shell
git commit -m "commit message"
```

5. git add & commit
```shell
git commit -am "commit message"
```

6. git log 확인
```shell
git log
```

## github와 연동하기

1. 리모드 저장소 확인
```shell
git remote -v
```

2. 리모드 저장소 추가
```shell
git remote add origin 복사한주소
```

3. 리모드 저장소 변경
```shell
git remote set-url origin 복사한주소
```

4. 리모드 저장소 push 하기
```shell
git push origin main
```

## branch 확인 및 변경

1. 모든 branch 확인
```shell
git branch
```

2. 사용할 branch 변경
```shell
git checkout branch명
```

3. branch명 변경하기
```shell
git branch -m 변경할branch명
git branch -m 원본branch명 변경할branch명
```


# 7. NPM 프로젝트(예제)의 패키지 버전 

1. https://github.com/HeropCode/Svelte-Movie-app 주소에 접속하기
2. `package.json`과 `package-lock.json`을 다운받아서 새폴더에 저장
	*  `package.json`은 수동으로 모듈을 관리하는 파일
	* `package-lock.json`은 `package.json` 모듈에 연결되어 있는 또 다른 외부 모듈의 내역이 들어있는 파일
	* `package-lock.json` 파일이 달라지면 `package.json` 파일의 모듈 버전이 일치하더라도 내부에서 사용되는 모듈의 버전이나 종류가 달라지는 문제가 발생할 수 있음
3. `npm i` or `npm install` 로 설치하기