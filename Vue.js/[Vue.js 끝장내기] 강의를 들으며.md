21.12.22

# 오리엔테이션

## 현대 프런트엔드의 개발 절차와 역할

### 현대 웹 서비스 개발 절차

- 요구사항 → 서비스 기획 → UI, UX 상세 설계 → GUI 디자인 → 퍼블리싱 → 백엔드 API 개발 → 프런트엔드 개발 → QA

### 프런트엔드 개발자의 역할

- 화면단 코드 작성
- 기획, 디자인, 퍼블리싱, 백엔드 개발자와 소통

## 수업에서 사용할 API 문서 소개

### Swagger

- 백엔드 개발자가 정의한 API를 보고 일고 이해해서 개발할 수 있는 능력이 필요하다
- 스웨거를 통해 API 문서를 다룰 것
- API 문서를 보고 백엔드 개발자와 어떻게 소통하고 협업해야하는 지도 배울 것

# 개발 환경 구성

## 개발 환경 소개 및 설정

- joshua1988/vue-til

## 프로그램 설치

- 크롬 설치
- vscode 설치
- node.js 설치
- vue.js 크롬 dev tools 설치

## 수업 소스코드 안내

- joshua1988/learn-vue-js
    - 다른 수업임

## VSCode 플러그인 설치 및 설정

- 확장 탭 클릭
- Vetur 설치 : VSCode에서 지원하는 Vue 플러그인
- material icon theme
- night awl
- Live Server

> 아래는 Vue.js의 기초개념 강의이다 - [Vue.js 시작하기]
> 

# Vue.js 소개

## MVVM 모델에서의 Vue

- MVVM 패턴의 뷰모델 레이어에 해당하는 화면(View)단 라이브러리
    
    ```jsx
                  ViewModel
    View  -----> DOM Listeners -----> Model
          <----- Data Bindings <-----   
     ↓                ↓                 ↓
    DOM              Vue             Plain JS Objects 
    ```
    
- View(화면)에서 사용자가 무언가 입력하면 **DOM Listeners**가 이걸 잡아서 Model(JS)에서 실행한다
- JS의 데이터가 변경되면 **Data Bindings**를 통해 화면에 반영한다


### 💻 MVVM 모델이란? (22.01.05)

- 소프트웨어 아키텍쳐 패턴, Model-View-ViewModel
- 마크업 언어 또는 GUI(뷰) 개발을 비지니스 로직 또는 백엔드 로직(모델)으로부터 분리시켜 뷰가 어느 특정 모델 플랫폼에 종속되지 않도록 한다
- MVVM의 뷰모델은 값 변환기로, **뷰모델이 모델에 있는 데이터 객체를 변환하기 때문에 객체를 관리하고 표현하기 쉬워진다는 것을 의미한다**
- 이러한 점에서, 뷰모델은 뷰보다는 더 모델이라는 것을 의미하고, 모든 뷰의 디스플레이 로직을 제외한 대부분을 처리한다


## Hello Vue.js와 뷰 개발자 도구

- 개발자도구에서 Vue에서 관리하는 데이터를 확인할 수 있다,
- 리액티비티 : 뷰의 데이터 속성이 모두 반영되어 있기 때문에 데이터에 변화에 따라 화면이 자동으로 그려지는 것

# 인스턴스

## 인스턴스 소개

### 뷰 인스턴스

- 필수로 생성해야 하는 코드
- 아래 코드를 실행하면 Vue의 API(기능)과 속성을 볼 수 있다.
    
    ```jsx
    var vm = **new Vue();**
    console.log(vm);
    ```
    
- html 특정 태그에 Vue 인스턴스를 붙여 사용한다
    - element를 지정하고, data를 정의해야 태그 내에서 Vue의 기능과 속성이 유효해진다
    
    ```html
    <body>
        <div id="app">
            <!-- Vue의 기능과 속성이 유효해진다. -->
        </div>
    
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <script>
            var vm = new Vue({
                el : '#app',
                data : {
                    message : 'hi'
                }
            });
            
        </script>
    </body>
    ```
    

## 인스턴스와 생성자 함수

- JS에서 함수를 이용해 인스턴스를 생성하는 방법은 생성자 함수를 작성하는 것이다
- 암묵적으로 함수가 대문자로 시작되면 생성자 함수라고 생각한다

### JS에서 인스턴스를 생성하는 방법

```jsx
function Person(name, job) {
	this.name = name;
	this.job = job;
}

var p = new Person('josh', 'developer');
```

### new Vue()를 사용하는 이유

```jsx
function Vue(){
	this.logText = function() {
		console.log('hello');
		}
}

var vm = new Vue();
vm.logText(); // hello
```

## 인스턴스의 옵션과 속성

- 생성자 함수를 재사용할 수 있는 옵션과 속성을 알아볼 것

### 인스턴스에서 사용할 수 있는 속성과 API

```jsx
new Vue({
	el: ,
	template: ,
	data: ,
	methods: ,
	created: ,
	watch: 
});
```

- key-value형태로 작성한다.
- 객체 리터럴(객체 안에 넣어서 작성) 방식이 가독성이 더 뛰어나고 이렇게들 사용한다

# 컴포넌트

21.12.27

## 컴포넌트 소개

- 최근 모던 프레임워크들은 컴포넌트 기반으로 개발을 하고 있다
- 화면의 영역을 영역별로 구분해서 코드로 관리하는 것을 **컴포넌트**라고 한다.
    - 또 영역을 구분하면 컴포넌트 간의 관계가 생긴다는 것도 알아두자
- 컴포넌트를 사용해 코드를 관리하는 이유 ?  **재 사 용 성**

## [실습 안내] 컴포넌트 등록 및 실습

- 인스턴스를 생성하면 기본적으로 Root 컴포넌트가 된다

### 전역 컴포넌트 생성 방법

```
📄 Vue.component('컴포넌트 이름', 컴포넌트 내용);
```

### 전역 컴포넌트 생성 예시

```jsx
<div id="app">
        <app-header></app-header>
        <app-content></app-content>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.component('app-header', {
            template: '<h1>Header</h1>'
        });

        Vue.component('app-content', {
            template : '<div>Content</div>' 
        })

        new Vue({
            el: '#app'
        });
    </script>
```

- template : 컴포넌트가 표현되는 코드
- 컴포넌트 등록 시 자동으로 루트 컴포넌트 아래에 생성된다
- 위 컴포넌트를 전역 컴포넌트라고 한다

## 지역 컴포넌트 등록

### 지역 컴포넌트 등록 방식

```jsx
new Vue({
            el: '#app',
            components : {
                // '컴포넌트 이름' : 컴포넌트 내용
                'app-footer' : {
                    template : '<footer>footer</footer>'
                }
            }
        });
```

## 전역 컴포넌트와 지역 컴포넌트의 차이점

- 지역 컴포넌트를 생성할 때는 여러 개를 생성할 수 있기 때문에 component**s** 라고 표기한다.
    - 후에 methods도 여러개 생성 할 수 있어 뒤에 s가 붙는다
- 일반적으로는 지역 컴포넌트를 사용하고
- 플러그인이나 라이브러리 같은 전역으로 사용해야 하는 것만 전역 컴포넌트로 생성한다

## 컴포넌트와 인스턴스의 관계

- 전역 컴포넌트는 인스턴스를 새로 생성할 때마다 모든 인스턴스에서 사용 가능하다(등록된다)
- 그런데 지역 컴포넌트는 인스턴스를 새로 생성할 때마다 새로 만들어야한다
- 대부분 인스턴스를 하나 생성하고 컴포넌트를 붙이는 방식으로 진행하기 때문에
- 이 개념은 배경지식 정도로 알아두면 좋다

# 컴포넌트 통신 방법 - 기본

## 컴포넌트 통신

- 컴포넌트는 기본적으로 고유한 데이터 유효 범위를 갖고 각각 관리한다
- 각각의 데이터를 공유하려면 props와 이벤트 속성을 이용해야 한다
- 상위 컴포넌트에서 하위 컴포넌트로 데이터를 내려준다 → props 전달
- 하위 컴포넌트에서 상위 컴포넌트로 데이터를 올려준다 → 이벤트 발생

## 컴포넌트 통신 규칙이 필요한 이유

- 통신 규칙이 없어 복잡한 흐름 때문에 버그가 발생하는 문제를 해결하고 데이터의 흐름을 추적할 수 있다
- 내려가는 데이터는 props 속성에 넣어 관리
- 올라가는 데이터는 Event 속성에 넣어 관리

## props 속성

### 들어가기 전에

- 앞으로 컴포넌트를 많이 생성할 것이기 때문에 객체를 미리 선언해서 사용하는 방식으로 사용하도록 하자
    
    ```jsx
    var appHeader = {
        template : '<h1>header</h1>'
    }
    
    new Vue({
        el : '#app',
        components : {
            'app-header' : appHeader
        }
    });
    ```
    

### props 속성

- props를 사용하지 않았을 때
    
    ```jsx
    var appHeader = {
        template : '<h1>header</h1>'
    }
    
    new Vue({
        el : '#app',
        components : {
            'app-header' : appHeader
        },
        data : {
            message : 'hi'
        }
    });
    ```
    
    - 위의 코드를 동작시키면 인스턴스와 맵핑된 Root 컴포넌트에서만 data(message)를 사용할 수 있다.
- props를 사용했을 때
    
    ```html
    <div id="app">
        <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="message"></app-header>
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var appHeader = {
            template : '<h1>header</h1>',
            props : ['propsdata']
        }
    
        new Vue({
            el : '#app',
            components : {
                'app-header' : appHeader
            },
            data : {
                message : 'hi'
            }
        });
    </script>
    ```
    
    - 전역객체인 appHeader에 props 키를 만들고 이름을 지정한다
    - <app-header> 태그에 v-bind라는 속성을 이용해, props 속성 이름에 상위 컴포넌트의 데이터 이름을 작성한다
    - 이처럼 Root 컴포넌트로부터 아래로 내려가는 데이터는 props를 사용해 작성할 수 있다.
    
    ```
    ❗  v-bind : props 속성 이름 = "상위 컴포넌트의 데이터 이름"
    
    ```
    

## props 속성의 특징

- Root 컴포넌트의 데이터를 변경하면 props로 설정한 데이터도 모두 변경된다

## [실습 안내] props 속성 실습

```html
<div id="app">
        <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="message"></app-header>
        <app-content v-bind:propsdata="num"></app-content>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var appHeader = {
            template : '<h1>{{ propsdata }}</h1>',
            props : ['propsdata']
        }

        var appContent = {
            template : '<div>{{ propsdata }}</div>',
            props : ['propsdata']
        }

        new Vue({
            el : '#app',
            components : {
                'app-header' : appHeader,
                'app-content' : appContent
            },
            data : {
                message : 'hi',
                num : 10
            }
        });
    </script>
```

- {{ }} 안에 props 속성의 이름을 넣으면 data 값이 반영된다

# 개발 환경 소개 (이어서)

## Node.js 버전 관리가 필요한 이유와 버전 변경하는 방법

- 프로젝트마다 node.js 버전 변경을 할 필요가 있다.. 특별한 이유를 알려주지 않음..
- node.js 홈페이지 > 다운로드 > 이전릴리스 > 확장자가 msi 인걸로 다운로드

21.12.29

- 이전릴리스를 받으면 선택해서 사용할 수 있을 줄 알았는데 .. 그건 아닌가보다 *→ nvm을 설치해야 가능*
- 인터넷에서 열심히 찾아서 삭제하는 방법대로 삭제를 했는데도 기존 버전이 존재해서 설치못한다는 에러가..
- 알고보니 윈도우에서는 제어판>프로그램삭제 에서 삭제하면 편하게 삭제가 된다고 한다 ^^..
- 그렇게 node v10.16.1을 다운받았다!

## NVM(Node Version Manager) 소개 및 설치

- nvm 설치 후 command 창에서는 버전이 나오는데 vscode 터미널에선 버전이 안나왔다
- https://github.com/nvm-sh/nvm > installing 아래에 curl 로 시작하는 명령어를 vscode 터미널에 복붙하고 설치한다
- 이때, 터미널 상태를 bash로 맞춰야 다운로드할 수 있다 → 없으면 git 설치해야한다 ([https://git-scm.com/download/win](https://git-scm.com/download/win))
    
    ```html
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```
    
- vscode에서도 nvm 버전을 확인할 수 있다
- 그리고 vi ~/.bashrc 로 들어가 아래 코드를 복붙한다
    
    ```
    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    ```
    
- esc 누르고 :wq 누르면 저장&아웃

## API 서버 실행 및 확인

- 실행 명령어는 package.json에 있다
- npm i 로 설치하고 터미널에 npm run dev를 실행한 후
- 크롬에 [http://localhost:3000/](http://localhost:3000/) 로 들어간다
- Cannot GET / 으로 뜨면 정확히 뜬 것

22.01.05

```
❗ 회사에서 공부하며서 복습~설치해봤는데... 음 먼가 되게 이상하게 설치된 것 같음... 🤔
```

## 데이터베이스 연결 안내

- 기본적으로 Node.js의 애플리케이션은 app.js 기준으로 실행된다
- app.js의 21번째줄부터 ~ mongoose.connect ~ : mongodb를 node.js에 연결하는 부분
- mongodb : nosql db

## MongoDB 인스턴스 생성 후 Node.js에 연결

1. MongoDB 클라우드에 계정 생성하고 클러스터 생성하기
2. SECURITY > Network Access 에서 IP Address 추가 → 0.0.0.0/0 으로 추가
3. SECURITY > Database Access > MongoDB Users → ID/PW 입력 후 Read And Write로 선택 후 추가
4. Atlas > Database > Connect > Connect Your Application 하면 필요한 String 값이 나온다
5. 이 String 값을 복사해 mongoose.connect url에 넣어준다
6. 저장 후 서버 재실행 > npm run dev
7. api/docs 에서 sign up에 들어가 Try it out을 누른 채로 input 값을 입력 후 응답이 제대로 오는지(200) 확인한다
8. VSCode에서도 로그가 찍히면 정상!

## API 문서 보는 법과 사용하는 방법

- 스웨거 API 문서 - 프론트엔드 개발자가 이해할 수 있도록 작성해놓는 문서

### 활용 방법

- API 종류별/성격별로 만든다
- API에 대한 설명을 간단하게 작성한다
- HTTP post 요청이면 파라미터도 추가한다
- 파라미터를 보냈을 때 예상되는 응답들에 대해서도 설명을 작성한다
- 이를 통해 프런트앤드 개발자는
    - url을 확인하고,
    - 어떤 parameter를 보내야하는 지, 필수 값은 무엇인지 확인할 수 있고,
    - 응답코드까지 예상할 수 있다
- 서버가 실행된 상태에서 API 문서가 올라오기 때문에 서버에 직접적인 데이터를 보내보고, 서버의 응답까지 확인해볼 수 있다는 게 스웨거의 장점이다.

# 프로젝트 생성 및 환경 구성

## Vue CLI로 프로젝트 생성

- 크롬에 Vue CLI를 검색 > Get Started > Installation 에 있는 sudo 코드를 터미널에 입력한다
    - `npm install -g @vue/cli`
- 설치가 완료되면 vue 명령어를 사용할 수 있다
- vue create vue-til → 선택 가능한 목록이 나온다
    - preset : 플러그인의 집합
    - Manually select features 선택
    - 이 목록에는 프로젝트에 구성될 수 있는 기능들을 나열한다

## Vue 프로젝트 구조 설명 및 ESLint 에러 확인
21.01.06

- 생성한 vue-til 폴더로 이동한 후 (cd vue-til)
- npm run serve를 실행 → 크롬에 localhost:8080을 입력하면 서버가 실행된다
- 이후 App.vue 폴더에서 코드 작성
- defalut에 created() 함수를 추가하고 저장하면 ESLint 에러가 발생한다

## ESLint 에러가 화면에 표시되지 않게 하는 방법

```jsx
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  created() {
    var a = 10;
  }
};
```

- a가 선언되었으나 사용되지 않았다는 에러가 발생한 것
- ESLint는 에러가 나지 않게 도와주는 도구
- 이 에러를 무시하는 방법을 설정한다
- vue.config.js 라는 파일을 만들고 아래 내용을 작성한다

```jsx
module.exports = {
    devServer: {
        overlay : false
    }
}
```

- 화면에서 에러를 덮어 쓰는 기능을 해제하는 코드 - overlay 속성을 껐구나 라고 인식하면 될 듯

## ESLint 설정 파일 안내

### .eslintrc.js

- js에서 에러가 날 수 있는 가능성을 제거하는 문법 검사기 (보조 도구)

```jsx
rules: {
    "no-console" : process.env.NODE_ENV === "production" ? "warn" : "off",
    "no-debugger": process.env.NODE_ENV === "production" ? "warn" : "off",
  }
```

- 개발 모드일 때 로그가 있으면 에러를 출력하고,
- 일반 프로토타입 모드 일 때는 off로 설정
- 설정 파일을 변경하면 서버를 재실행해야 한다

## Prettier 소개 및 ESLint와 같이 사용해야 하는 이유

- Prettier  : 코드 정리 도구
- 협업 시 코드 작성 기준을 정할 수 있다는 장점이 있다
- [https://prettier.io/docs/en/options.html](https://prettier.io/docs/en/options.html)
- .eslintrc.js 에서 프리티어를 설정해야 하는데, 그 이유는
- eslintrc의 rules와 충돌이 나기 때문에 따로 작성하면 안되고 eslintrc를 먼저 설정해줘야 한다

```jsx
rules: {
    "no-console" : "off",
    "prettier" : {
      printWidth : 80
    }
  }
```

- 이렇게 작성하면, prettier로 정리를 하면서 ESLint 에러도 잡는 효과를 볼 수 있다.
- VSCode에서 ESLint와 Prettier 플러그인을 install하면 기준에 맞지 않는 코드에 빨간 밑줄이 뜨고, 저장 시에 자동 수정된다
- settings.json에 아래 코드를 추가한다

```jsx
{
    "workbench.colorTheme": "Night Owl",
    "eslint.validate": [
        {
            "language": "vue",
            "autoFix": true
        },
        {
            "language": "javascript",
            "autoFix": true
        },
        {
            "language": "javascriptreact",
            "autoFix": true
        },
        {
            "language": "typescript",
            "autoFix": true
        },
        {
            "language": "typescriptreact",
            "autoFix": true
        }
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "eslint.workingDirectories": [
        {
            "mode": "auto"
        }
    ],
}
```

# 라우터 & 컴포넌트 설계

22.01.10

## 깃헙 리포지토리 안내 및 클론

- vue-til 레퍼지토리를 클론해와서 1_setup 브랜치로 체크아웃 하고 설치한다
    
    ```
    git clone https://github.com/joshua1988/vue-til.git
    git checkout 1_setup
    npm i
    ```
    

## 뷰 라우터 설치 및 연결

- 설치하는 동안 src 폴더 아래 routes/index.js 를 추가한다
- 설치가 완료되면 아래 코드를 추가한다
    
    ```jsx
    import Vue from 'vue';
    import VueRouter from 'vue-router';
    
    Vue.use(VueRouter);
    
    export default new VueRouter();
    ```
    
- export를 쓰면 다른 js 파일에서 해당 파일을 import 할 수 있다.

## 페이지 컴포넌트 생성 및 연결

```jsx
import LoginPage from '@/views/LoginPage.vue';
import SignupPage from '@/views/SignupPage.vue';

Vue.use(VueRouter);

export default new VueRouter({
  //라우팅 정보를 담는 배열
  routes: [
    {
      path: '/login',
      component: LoginPage,
    },
    {
      path: '/signup',
      component: SignupPage,
    },
  ],
});
```

- SignupPage.vue, LoginPage.vue 를 만들고 컴포넌트로 연결한다

## 라우팅 동작 확인

- 컴포넌트로 연결한 페이지를 코드 스플릿팅(?)으로 연결할 것	
