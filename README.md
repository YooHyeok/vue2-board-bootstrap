# *Vue Cli-init & bootstrap-vue*
## *Install*
<details>
<summary>펼치기/접기</summary>
<br>

- ## NPM 방식
  - ### vue/cli-init 설치
    ```bash
    npm i -g @vue/cli-init
    ```

  - ### vue 프로젝트 추가
    ```bash
    vue init webpack {프로젝트명}
    ```
- ## YARN 방식
  - ### yarn 설치
    ```bash
    npm install -g yarn
    ```
  - ### vue 설치
    ```bash
    yarn global add vue
    ```
  - ### vue/cli-init 설치
    일종의 보일러플레이트로 vue.js 프로젝트의 환경 세팅을 자동으로 해준다.
    ```bash
    yarn global add @vue/cli-init
    ```

  - ### vue 프로젝트 추가
    ```bash
    vue init webpack {프로젝트명}
    ```

  - #### 설치 옵션 선택 및 설치 결과
    ```text/plain
    ? Project name {프로젝트명}
    ? Project description {프로젝트 상세설명}
    ? Author 닉네임 <깃허브 계정>
    ? Vue build standalone
    ? Install vue-router? Yes
    ? Use ESLint to lint your code? No
    ? Set up unit tests Yes
    ? Pick a test runner jest
    ? Setup e2e tests with Nightwatch? No
    ? Should we run `npm install` for you after the project has been created? (recommended) npm

      vue-cli · Generated "vue2-board".
      
    Run `npm audit` for details.

    # Project initialization finished!
    # ========================

    To get started:

      cd vue2-board
      npm run dev
    ```
  - ### bootstrap-vue 설치
	<a href = "https://bootstrap-vue.org/docs">bootstrap-vue docs</a>
	
	- #### 프로젝트 디렉토리 변경
		```bash
		cd vue2-board-bootstrap
		```

  -  ### bootstrap dependency 추가
      - #### npm
        ```bash
        npm i vue bootstrap-vue bootstrap
        ```
      - #### yarn 
        ```bash
        yarn add vue bootstrap-vue bootstrap
        ```
      - #### vscode 실행
        ```bash
        code .
        ```
      - main.js
        ```javascript
        import BootstrapVue from 'bootstrap-vue' // dependency 설치시 자동 추가됨
        /* 추가 */
        import 'bootstrap/dist/css/bootstrap.css'
        import 'bootstrap-vue/dist/bootstrap-vue.css'
        ```
</details>

