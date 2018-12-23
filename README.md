<div align=center>

<img src="https://cdn-images-1.medium.com/max/2000/1*CNeQyaChrTh0H3ovOd9Dgg.png">

</div>

# 📖 웹팩 튜토리얼
웹팩 튜토리얼을 작성합니다. 처음에 웹팩을 처음 접했을 때 어려웠던 부분들을 하나씩 체크해보며 개념들을 짚고 넘어갑니다. 이 저장소는 보일러플레이트로 이용할 수 있습니다. :)  

## 🚀 목표
가볍게 웹팩설정을 하며 웹팩의 주요 개념을 알아보고 빌드와 개발서버까지 설정하는 방법을 익히는것을 목표로 합니다. 추가적으로 ES6 이상의 문법들을 ES5로 변환하여 작동이 정상적으로 되는지 확인해봅니다.

## 📝 목차

#### 웹팩에 관하여
* [웹팩이란?](#웹팩이란)
* [웹팩의 4가지 주요개념](#웹팩의-4가지-주요개념)

#### 웹팩 설정하기
* [1단계 : 프로젝트 초기화](#1단계--프로젝트-초기화)
* [2단계 : 필요한 모듈들 설치하기](#2단계--필요한-모듈들-설치하기)
* [3단계 : 웹팩 설정파일 작성하기](#3단계--웹팩-설정파일-작성하기)
* [빌드해보기](#빌드해보기)
* [개발서버 열어보기](#개발서버-열어보기)


---


# 웹팩에 관하여
웹팩이란 무엇인지 알아보고 웹팩의 4가지 주요개념들을 알아봅니다.

## 웹팩이란?
웹팩이란 모듈 번들러입니다.  
**모듈(Module)** 이란 구현 세부사항을 캡슐화하고 공개 API를 노출하여 다른 코드에서 쉽게 로드하고 사용할 수 있도록 재사용 가능한 코드조각입니다.  
**번들(Bundle)** 이란 소프트웨어 및 일부 하드웨어와 함께 작동하는데 필요한 모든것을 포함하는 패키지 입니다.


**모듈번들러** 란 우리가 만들려는 '프로젝트'에 필요한 모든 코드조각(모듈)들을 포함시켜주는 도구입니다.  


**웹팩** 은 프로젝트에 필요한 모든 의존성파일들을 하나의 번들파일로 만들어 주어 배포하기 쉽게 빌드해주는 도구입니다.

> 모듈번들러에 대한 자세한 글은 [자바스크립트 모듈, 모듈 포맷, 모듈 로더와 모듈 번들러에 대한 10분 입문서
](https://github.com/codepink/codepink.github.com/wiki/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%AA%A8%EB%93%88,-%EB%AA%A8%EB%93%88-%ED%8F%AC%EB%A7%B7,-%EB%AA%A8%EB%93%88-%EB%A1%9C%EB%8D%94%EC%99%80-%EB%AA%A8%EB%93%88-%EB%B2%88%EB%93%A4%EB%9F%AC%EC%97%90-%EB%8C%80%ED%95%9C-10%EB%B6%84-%EC%9E%85%EB%AC%B8%EC%84%9C#%EC%9A%B0%EB%A6%AC%EB%8A%94-%EB%AA%A8%EB%93%88%EC%9D%B4-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%9C%EA%B0%80)를 읽어보시기 바랍니다.


## 웹팩의 4가지 주요개념
웹팩에서 빌드를 할 때 주요개념이 크게 4가지가 존재합니다. 각각을 단계적으로 알아보고 다음 스텝에서 실제로 설정을 해보겠습니다.

* entry
* module
* plugins
* output


#### 1단계 : entry
프로젝트가 구동되기 위해서는 다양한 의존성파일(모듈)들(js, html, css, img 등)이 존재하는데 이를 통해 의존성그래프가 생기기 마련입니다. 의존성 그래프의 시작점이 되는 부분이 **entry** 이며 보통 `main.js` 또는 `index.js` 라고 설정합니다.

#### 2단계 : module
다양한 모듈들은 각각의 파일유형을 갖게됩니다. 이 단계에서는 각 모듈들을 모듈유형에 따라 어떻게 처리할지를 설정해줍니다. 유형들은 로더 라는것을 통해 처리되어 최종적으로 js 파일로 만들어집니다.

#### 3단계 : plugins
2단계의 과정을 거치게되면 js 파일이 나오게됩니다. 해당 js 파일을 그대로 쓸 수도 있지만 최소화(minify), 난독화(uglify) 같은 기능들을 이용할 수 있는 재정련단계라고 볼 수 있습니다.

#### 4단계 : output
3단계까지 끝나게되면 이름 그대로 출력입니다. 최종적으로 번들링되어 나올 파일에 대한 파일이름, 경로같은 것들을 지정해 줄 수 있습니다.

---

# 웹팩 설정하기
웹팩이 무엇인지, 어떤 컨셉을 잡고있는지에 대해 살펴봤습니다. 이 단계에서는 실제로 어떻게 웹팩을 구성하는지에 대해 실습을 합니다.

## 준비물
* 마음가짐
* [npm](https://www.npmjs.com/get-npm)

## 1단계 : 프로젝트 초기화
먼저 프로젝트가 될 폴더를 만들고 초기화 시켜줍니다.
```bash
$mkdir my-project
$cd my-project
$npm init
```

`$npm init` 을 입력하였으면 다음과 같은 화면을 볼 수 있습니다.
```text
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (webpack-tutorial)
version: (1.0.0)
description: webpack-tutorial
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
```
뭐 계속 엔터 치셔도 상관 없습니다만 중요한거 몇 개만 짚고 넘어가자면
* package name : 패키지 이름
* version : 패키지 버젼
* description : 설명
* entry point: 시작점

여기까지 오셨으면 `package.json` 이라는 파일이 프로젝트 폴더에 생성이 되는것을 볼 수 있습니다.

> **package.json 이란?**  
간단히 우리가 만들 패키지(프로젝트 또는 앱)에 대한 설명서와 같은 파일이다. 자세한 내용은 [다음 글](https://programmingsummaries.tistory.com/385)을 통해 알 수 있습니다.

## 2단계 : 필요한 모듈들 설치하기
우리의 프로젝트의 목표는 간단합니다.
* 빌드하기
* 개발 서버 열어보기
* ES6 를 ES5로 변환하기

그럼 필요한 각 모듈들을 설치합니다.

```bash
$npm install -g webpack
$npm install --save-dev webpack@3.11.0 webpack-dev-server@2.11.0
$npm install --save-dev @babel/core @babel/preset-env babel-loader
$npm install --save-dev html-webpack-plugin
```
> 모듈 뒤에 @숫자 는 해당 모듈의 특정버젼을 나타냅니다. webpack은 3.11.0버젼, webpack-dev-server은 2.11.0 버젼을 설치합니다.  
@babel/core 와 @babel/preset-env 에 붙은 @babel 은 babel 7버젼부터 생긴 네임스페이스입니다.

잠깐 명령어들을 짚고 넘어가겠습니다.

#### 패키지 설치 명령어
``` bash
# 지역설치 & 배포설치
$npm install <package name>

# 전역설치
$npm install -g <package name>

# 개발설치
$npm install --save-dev <package name>
```

#### 개발설치와 배포설치
개발시에만 필요한 모듈들은 `--save-dev` 옵션을 통해 설치한다. 이렇게 옵션을 붙여서 설치한 경우에는 `package.json` 파일에 `devDependencies`의 목록에 추가된다.

배포시에 필요한 모듈들은 `--save` 옵션을 통해 설치되는데 생략할 수 있습니다. `package.json` 파일에 `dependencies`의 목록에 추가된다.

#### 지역설치와 전역설치
지역(local)설치와 전역(global)설치가 있습니다. 옵션을 별도로 지정하지않으면 기본값은 지역설치로 됩니다. 그리고 설치된 모듈들은 해당 프로젝트 내의 `node_modules` 라는 디렉토리에 설치됩니다. 지역설치는 해당 프로젝트 내에서만 사용할 수 있다는 특징이 있습니다.

전역설치는 `$npm install` 명령어 뒤에 `-g` 라는 옵션을 붙여줍니다. 전역으로 설치된 경우 모든 프로젝트에서 사용할 수 있습니다. 전역으로 설치된 모듈들은 각 OS 마다 다릅니다.


#### 각 모듈들 살펴보기

* webpack : 모듈번들러
* webpack-dev-server : 개발 시 실시간 빌드를 해줍니다.
* @babel/core : 바벨의 핵심 파일
* @babel/preset-env : ES6 이상의 자바스크립트 파일을 각 브라우저에 맞는 코드로 변환시켜주는 모듈
* babel-loader : 자바스크립트 파일을 웹팩에서 번들링하기위해 사용하는 로더
* html-webpack-plugin : 번들된 파일들을 script 태그를 통해 추가해줘야 하는데 이를 자동적으로 해줍니다.


이제 모듈들을 설치했으면 다시 `package.json` 파일을 살펴봅니다.

```json
"devDependencies": {
    "@babel/core": "^7.2.2",
    "@babel/preset-env": "^7.2.3",
    "babel-loader": "^8.0.4",
    "webpack": "^3.11.0",
    "webpack-dev-server": "^2.11.0"
  }
```
`devDependencies` 에 추가된 목록들이 나오는것을 확인할 수 있습니다.

> 다른 프로젝트들이 어떻게 구성되어있나 확인하려면 가장먼저 `package.json` 파일을 살펴보는 것이 좋습니다 :)

## 3단계 : 웹팩 설정파일 작성하기
이제 설정파일을 작성해봅니다. 먼저 루트 디렉토리에 `webpack.config.js` 파일을 생성합니다.  
이 파일은 웹팩의 설정이 들어있는 파일입니다. 이 설정을 통해 어떻게 빌드할 것인지에 대해 커스터마이징 할 수 있습니다.


웹팩의 4가지 개념을 떠올리면 대략 다음과 같은 형태입니다. plugins 는 배열형태로 작성한다는것에 주의하세요!
```js
// webpack.config.js
module.exports = {
  entry: {

  },
  output: {

  },
  module: {

  },
  plugins: [

  ],
};
```

단계별로 다시 적용해보기 전에 폴더구조를 한번 짚고 넘어가겠습니다.
#### 폴더구조
```
my-project
├── node_modules/
├── src/
│   └── index.js
├── package.json
├── package-lock.json
└── webpack.config.js
```

#### entry 설정하기
```js
// webpack.config.js
module.exports = {
  entry: {
    bundle: './src/index.js',
  }
  // ...
};
```
의존성 그래프의 시작점이 되는 index.js 의 경로를 잡아줍니다. bundle 이라는 key로 지정한 이유는 번들파일이 여러개 있을 경우 이렇게 `key: value` 형태로 작성합니다. 위의 코드는 아래 코드와 동일합니다.

```js
// webpack.config.js
module.exports = {
  entry: './src/index.js',
  // ...
};
```
#### output 설정하기
output 은 출력이 될 경로와 파일 이름을 지정해줍니다.
```js
// webpack.config.js
const path = require('path');

module.exports = {
  entry: {
    bundle: './src/index.js',
  },
  output: {
    filename: '[name].js',
    path: path.join(__dirname, 'dist'),
  },
  // ...
};
```
먼저 `filename` 속성에는 출력할 파일의 이름을 설정합니다. 여러개의 번들파일이 필요한 경우 `[name].js` 로 작성을 하면 각 번들파일의 이름에 맞게 출력됩니다.

`path` 에는 번들링 될 출력파일이 위치할 경로를 정해줍니다. `nodejs`의 내장모듈인 `path` 를 읽어들여 사용합니다.

> `path.resolve` 와 `path.join` 라는 메서드는 차이가 있습니다 하지만 `__dirname` 을 사용하면 의도하는 값을 반환할 수 있습니다. - [Jbee 님의 글중 일부 인용](https://jaeyeophan.github.io/2017/05/05/webpack-tutorial-1/)

> `__dirname` 이란?  
간단히 말해 현재 위치를 가리키는 nodejs 의 전역변수. 자세한내용은 [다음 글](https://github.com/heecheolman/TIL/blob/master/module/CHECK.md#__dirname-%EA%B3%BC--%EC%9D%98-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)을 참고하세요


#### module 설정하기
```js
// webpack.config.js
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: '[name].js',
    path: path.join(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: '/node_modules/',
        include: path.join(__dirname, 'src'),
      },
    ],
  },
  // ...
};
```
module 에서는 rules 라는 속성으로 한번 더 들어갑니다. rules 는 객체배열형태임을 주의하세요!

규칙들(rules)은 객체형태로 존재하는데 내부를 살펴보겠습니다.

* test: 로더를 적용시킬 파일들에 대해 정규식으로 표현. `.js` 파일들은 다음 로더 사용
* loader: 로더 명시. `.js` 파일은 `babel-loader` 를 타고 트랜스파일됩니다.
* exclude: 로더가 실행될 때 제외시킬 파일들을 명시, `/node_modules/` 에 존재하는 모든 파일 제외
* include: 로더가 실행될 때 포함시킬 파일들을 명시, 'src' 폴더에 있는 모든 `.js` 파일 포함

바벨을 사용할 때 한가지 더 해줘야하는 작업이있다. ES6 이상의 자바스크립트 파일을 ES5 형태로 바꿔주는 설정인데, 루트디렉토리에 `.babelrc` 라는 파일을 만들고 다음과 같이 작성합니다.
```json
{
  "presets": ["@babel/preset-env"]
}
```

#### plugins 설정하기
플러그인은 여러가지를 사용할 수 있지만 여기서는 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) 을 이용합니다.

이용하기 전에 루트디렉토리에 `index.html` 을 생성해 작성하자. 해당 파일은 `body` 태그가 닫히는 부분 뒤에 `bundle.js` 를 import 하지 않는다는것에 주의를 기울여줍니다.
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack Tutorial</title>
</head>
<body>
    Hello Webpack!
</body>
</html>
```

이제 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) 을 통해 `bundle.js` 를 빌드시에 자동 import 되게 해봅니다.


```js
// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: '[name].js',
    path: path.join(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: '/node_modules/',
        include: path.join(__dirname, 'src'),
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'index.html'),
      filename: 'index.html',
      inject: true,
    }),
  ],
};
```
`html-webpack-plugin` 을 가져와 `HtmlWebpackPlugin` 에 담고 plugins 배열 안에서 new 를 해준다. 내부를 살펴보자면

* template: 기존에 작성한 html 파일이 있다면 불러옵니다.
* filename: 최종적으로 작성될 html 파일 이름입니다. 기본값은 `index.html` 입니다.
* inject: true 로 하면 자동적으로 `bundle.js` 를 import 해줍니다.

## 빌드해보기
설정을 다했으니 빌드르 해보는 단계이다. 빌드하기전 폴더구조를 확인해봅니다.

#### 폴더구조
```text
my-project
├── node_modules/
├── src/
│   └── index.js
├── index.html
├── .babelrc
├── package.json
├── package-lock.json
└── webpack.config.js
```
이렇게 되어있다면 해당 프로젝트의 루트디렉토리로 이동하여 명령어를 입력합니다.
```bash
$webpack --config webpack.config.js
```
성공했다면 `built` 라는 메세지와 함께 `dist` 라는 폴더가 생성되고 그 안에는 `bundle.js` 가 생성되었음을 확인합니다.

#### 명령어 줄이기
명령어를 입력하기 너무 긴 것 같습니다. `package.json` 의 `scripts` 를 약간만 수정하여 편리하게 이용할 수 있습니다. 다음을 추가해주세요.
```json
"scripts": {
    "build": "webpack --config webpack.config.js"
},
```

그리고 빌드합니다.

```bash
$npm run build

# npm run build 는 다음과 같이 치환됩니다.
$webpack --config webpack.config.js
```
#### 빌드 확인하기

빌드가 완료되면 `dist` 폴더에 `bundle.js` 와 `index.html` 이 빌드된 것을 확인할 수 있습니다. `src/index.js` 에 ES6 문법을 작성하고 번들링된 파일과 비교해봅니다.
```js
// src/index.js

class Person {
  constructor() {
    console.log('hello!');
  }
}

new Person();
```

bundle.js 의 맨 아래만 주목해보면 `.js` 파일이 `babel-loader` 를 통해 다음과 같이 트랜스파일 되었음을 확인할 수 있습니다.

```js
// dist/bundle.js

// ... 생략
(function(module, exports) {

function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError("Cannot call a class as a function"); } }

var Person = function Person() {
  _classCallCheck(this, Person);

  console.log('hello!');
};

new Person();
```

## 개발서버 열어보기
빌드를 마쳤습니다. 하지만 개발 할 때 소스코드 수정을 할 때마다 빌드를 하여 확인할 수는 없는 노릇입니다. 그래서 내부 개발서버를 열고 소스코드의 변경사항을 변경 시 자동으로 컴파일하여 올려주는 [webpack-dev-server](https://github.com/webpack/webpack-dev-server) 를 이용합니다.

우리는 모듈을 설치했으므로 명령어만 입력하면 됩니다.

```bash
$node_modules/.bin/webpack-dev-server --inline --hot
```

그러면 브라우저를 열고 localhost:8080 를 입력하면 Hello Webpack 과 함께 콘솔창에는 hello 가 찍혀있는것을 확인할 수 있습니다.

#### 명령어 줄이기
위의 명령어도 줄일 수 있습니다.
`package.json` 파일을 열고 `scripts` 안에 다음을 추가해줍니다.
```json
"scripts": {
    "build": "webpack --config webpack.config.js",
    "start": "webpack-dev-server --hot --inline"
},
```
이제 더 편하게 이용할 수 있습니다.

```bash
$npm run start

#npm run start 는 다음과 같이 치환됩니다.
$node_modules/.bin/webpack-dev-server --inline --hot
```

#### inline, hot 옵션
webpack-dev-server 를 이용할 때 옵션을 줄 수 있는데  
**inline** 옵션은 전체 페이지 실시간 로딩이며,  
**hot** 옵션은 파일이 수정될 경우 그 부분에 대해 리로드를 해주는 옵션

더 자세한 사항은 [공식문서 참고](https://webpack.js.org/configuration/dev-server/#devserver-hot)


## 마무리 지으며

목표에 필요한 간단한 설정들은 끝이났습니다. 웹팩을 커스터마이징 하는 방법은 입맛따라 다르고 다양합니다. 적재적소에 맞게 설정하는것이 가장 좋은 설정이 아닐까 싶습니다. 해당 저장소를 boilerplate 처럼 사용해도 되고 playground 로 사용하셔도 됩니다. 개인적으로 이 글을 작성하며 웹팩에 대해 좀 더 정리가 되어서 얻어가는게 많습니다. 잘못된 사항이 있다면 풀리퀘 부탁드리겠습니다.

## 참고문헌
* [모듈화와 npm(node package manger)](https://poiemaweb.com/nodejs-npm)
* [Webpack2와 모듈번들링을 위한 초보자 가이드](https://github.com/FEDevelopers/tech.description/wiki/Webpack2%EC%99%80-%EB%AA%A8%EB%93%88%EB%B2%88%EB%93%A4%EB%A7%81%EC%9D%84-%EC%9C%84%ED%95%9C-%EC%B4%88%EB%B3%B4%EC%9E%90-%EA%B0%80%EC%9D%B4%EB%93%9C)
* [웹팩 튜토리얼1 - Jbee](https://jaeyeophan.github.io/2017/05/05/webpack-tutorial-1/)
