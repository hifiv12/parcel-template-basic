# bundler
- 다양한 기능들을 가진 패키지를 bundler에 외부 패키지를 주입시켜 우리가 알고 있는 html5, css, javascript로 변환

  parcel-bundler | webpack
  -- | --
  소/중형 | 중/대형
  구성 없는 단순한 자동 번들링 | 매우 꼼꼼한 구성

## parcel-bundler
- /dist 폴더 안에 해쉬화 하여 서버가 열린다.
- web에서 확인하는 파일은 /dist에 들어있는 파일

1. default setting
  ```npm
    npm i -D parcel-bundler
  ```

  ```package.json
      "scripts": {
      "dev": "parcel index.html",
      "build": "parcel build index.html"
     },
  ```
  - parcel-bundler 패키지 설치 및 명령어 alias
  - index.html 생성 및 양식 완성 후 
  - js/main.js, scss/main.scss 생성
  - index.html에 위의 파일 연결
  - 로고로 사용할 img 하나와 그 img를 favicon을 생성해 배치

2. 정적 파일 연결
  - /dist 파일에 자동으로 넣어줄 수 있는 기능
  - parcel plugin static files copy
    ```terminal
      npm install -D parcel-plugin-static-files-copy
    ```

    ```package.json
      "staticFiles": {
        "staticPath": "static"
      }
    ```
    * 최하단에 기입
  - /static 생성 후 favicon 파일을 옮겨주면 서버를 열게되면 static 폴더에 든 파일은 자동으로 /dist에 추가

3. autoprefixer
  - vander prefix
  - 특정 브라우저에서 동작 할 수 있게 도와주는 기능
    ```console
        npm i -D postcss autoprefixer
    ```
    * postcss, autoprefixer 설치

    ```package.json
      "browserslist": [
        "> 1%", 
        "last 2 versions"
       ]
    ```
    * 하위 1퍼센트 이상
    * 마지막 2개의 버전
  - ESM (ECMA Script Modules)
    * import & export 
  - node.js -> CommonJS
    * node.js에서 사용하는 import와 export를 사용
    * require()
    * module.exports
  - autoprefixer10 와 postcss 8의 버전이 충돌이 일어날 수 있음
    * autoprefixer의 버전은 10일때 9로 내리면 해결
    * 현재 npm상에서는 충돌이 나지 않아 다운그레이드나 업그레이드 하지 않음
  - /dist 폴더 내의 hash화 된 main.js 에서는 줄이 그어진 접두어가 표시가 됨 얏호

4. babel
  - ECMAScript의 구버전으로 컴파일하기 위한 javascript 트랜스컴파일러 
  - 설치법
    ```console
      npm i -D @babel/core @babel/preset-env
    ```
    * .babelrc.js
      ```js
        module.exports = {
          presets: ['@babel/preset-env']
        }
      ```

      ```package.json
        "browserslist": [
          "> 1%", 
          "last 2 versions"
        ]
      ```
      - browserslist를 추가 한적이 없으면 추가
  - 버전 이슈
    * 현재 "@babel/core": "^7.22.5", "@babel/preset-env": "^7.22.5" 
    * 충돌나지 않고 제대로 실행이 된다 
    * 구형버전에서는 콘솔오류가 발생
    * @babel/plugin-transform-runtime을 설치
    * .babelrc.js의 프로퍼티 plugins: [ ['@bable/plugin-transform-runtime'] ] 명시

5. CLI
  - Serve
    * 개발용 서버를 시작 및 빠른 모듈 교체를 지원
    * parcel index.html
  - build
    * 실제 배포를 위한 빌드
    * 코드 최소화 (미니파이케이션)가 활성화
    * parcel build index.html
  - option
    * --out-dir dir/dir : /dist의 이름과 경로를 바꾸려면 parcel build index.html --out-dir dir/dir로 변경
    * --port : defualt : 1234 -> parcel serve index.html --port nnnn
    * --open : 자동으로 빌드 시 열리게 만듦
    * --no hmr : 빠른 모듈 교체 비활성화
      - hmr : Hot Module Replacement 런타임에 페이지 새로고침 없이 수정된내용으로 자동으로 갱신
    * --no-cache : 파일 시스템 캐시 비활성화
      - default 활성화
  