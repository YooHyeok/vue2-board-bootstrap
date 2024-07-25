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


# b-table 태그
부트스트랩에서 지원하는 Table 렌더링 태그이다.

## :items 속성 , :fields 속성
 - #### items: 요소를 순회해서 출력한다.
 - #### fields: items 요소로부터 보여줄 필드(컬럼)이다.
    - 일반적으로 배열 형태로 보여줄 필드 property의 명 형태로 나열한다.
    - 보여줄 property명을 변경하기 위해서는 key, label property를 갖는 Object로 나열한다.
        - key: 할당될 property명
        - label: 실제 출력될 컬럼명
  
  ### 예시 코드
  ```vue
  <template>
    <div>
      <b-table striped hover :items="items" :fields="fields"/>
    </div>
  </template>
  <script>
  export default {
      name: 'Board',
      data() {
        return {

          // fields: ['content_id', `title`, `created_at`], // items로부터 보여줄 컬럼

          fields: [// items로부터 보여줄 컬럼 key: 실제 컬럼 / label: 보여줄 내용
            {
              key: 'content_id',
              label: '글번호',

            },
            {
              key: 'title',
              label: '제목'
            }, 
            {
              key: `created_at`,
              label: '작성일'
            },
            {
              key: 'user_name',
              label: '글쓴이',

            },
          ], 
          // items: data.Content
          items: items
        }
      },
  }
  </script>
  ```
  ### 실제 출력
  ```html
  <table role="table" aria-busy="false" aria-colcount="4"
      class="table b-table table-striped table-hover" id="__BVID__16">
      <thead role="rowgroup" class="">
        <tr role="row" class="">
          <th role="columnheader" scope="col" aria-colindex="1" class="">
            <div>글번호</div>
          </th>
          <th role="columnheader" scope="col" aria-colindex="2" class="">
            <div>제목</div>
          </th>
          <th role="columnheader" scope="col" aria-colindex="3" class="">
            <div>작성일</div>
          </th>
          <th role="columnheader" scope="col" aria-colindex="4" class="">
            <div>글쓴이</div>
          </th>
        </tr>
      </thead>
      <tbody role="rowgroup"><!---->
        <tr role="row" class="">
          <td aria-colindex="1" role="cell" class="">3</td>
          <td aria-colindex="2" role="cell" class="">생일 축하해주신 여러분 감사합니다!</td>
          <td aria-colindex="3" role="cell" class="">2019-03-29 13:11:42</td>
          <td aria-colindex="4" role="cell" class="">아이린</td>
        </tr>
        <tr role="row" class="">
          <td aria-colindex="1" role="cell" class="">2</td>
          <td aria-colindex="2" role="cell" class="">레드벨벳 많이 사랑해 주세요^^</td>
          <td aria-colindex="3" role="cell" class="">2019-01-02 13:11:42</td>
          <td aria-colindex="4" role="cell" class="">조이</td>
        </tr>
        <tr role="row" class="">
          <td aria-colindex="1" role="cell" class="">1</td>
          <td aria-colindex="2" role="cell" class="">개린이 르라나의 강의 알람표</td>
          <td aria-colindex="3" role="cell" class="">2019-01-01 13:11:42</td>
          <td aria-colindex="4" role="cell" class="">lelana</td>
        </tr>
      </tbody>
    </table>
  ```

# Arrays.findIndex(조건)
특정 조건에 만족하는 요소의 첫번째 index를 찾는다.

```js
const targetId = 2;
const examples = [
  {
    id: 1
  }, 
  {
    id: 2
  }, 
  {
    id: 3
  }
]
const findIndex = examples.findIndex(item => item.id === targetId);
```
위 예시코드는 examples 배열의 요소중 id가 targetId(2)와 일치하는 요소를 찾는다.  
조건이 일치하는 가장 처음 요소를 찾아 인덱스를 반환하므로, 유니크한 키값을 찾는데 사용하는것이 적절하다.  

# Arrays.splice(index, count, item)
특정 index를 기준으로 count수 만큼 제거한다.  
만약 count가 0일 경우 3번째 인자값으로 대체할 새로운 요소를 지정할 수 있다.  
(값 변경)

# Pagenation(BootStrap)

### b-pagination
페이지네이션 버튼들이 생성된다.
#### 필요한 속성 값들
현재 페이지 값(current-page), 출력될 갯수(per-page), 전체 데이터 갯수(:total-rows) 속성들로 구성된다.  
이때 출력될 갯수에 해당하는 per-page 속성과 현재 페이지 값인 current-page 속성은 b-table에서도 사용한다.  
해당 데이터를 기준으로 실제적으로 출력(b-table)과 조작(b-pagination)으로 매핑된다.

```vue
<template>
    <b-table 
      striped hover 
      :per-page="perPage" 
      :current-page="currentPage"
      :items="items" 
      @row-clicked="rowClick"
    />
    <!-- total-rows에 실제 전체 row수를 저장 -->
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      align="center"
    />
</template>
<script>
export default {
  data() {
    return {
      items: [/* 게시글 목록... */]
    }
  },
  computed: {
    rows() {
      return this.items.length
    }
  }
}
</script>
```