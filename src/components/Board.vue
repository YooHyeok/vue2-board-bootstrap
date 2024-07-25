<template>
  <div>
    <b-table 
      striped hover 
      :per-page="perPage"
      :current-page="currentPage"
      :items="items" 
      :fields="fields"
      @row-clicked="rowClick"
    />
    <!-- total-rows에 실제 전체 row수를 저장 -->
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      align="center"
    ></b-pagination>

    <b-button @click="writeContent">글쓰기</b-button>
  </div>
</template>

<script>
  import data from '@/data';

 
  export default {
    name: 'Board',
    data() {

       /* 게시글번호 기준 역순(오름차순) 정렬 */
      let items = data.Content.sort((a,b) => {return b.content_id-a.content_id})
      items = items.map(content => {
          return {  // 순회한 요소 전개 후 user_name 필드 추가 (필터링된 user_name)
            ...content,
            user_name: data.User.filter(user => user.user_id === content.user_id)[0].name
            // 현재 순회요소 content의 user_id와 일치하는 user객체의 user_id 추출 및 배열로 반환
            // 배열 반환이지만 pk 기준 비교라 1개의 데이터만 반환되므로 [0]으로 접근
          }
        }
      )

      return {
        perPage: 10, // 보여질 게시글 수
        currentPage: 1, // 현재 페이지 위치 (표시됨) default 1페이지

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
    methods: {
      rowClick(item, index, event) {
        this.$router.push({
          path: `/board/free/detail/${item.content_id}`
        })
      },
      writeContent() {
      this.$router.push({
          path: '/board/free/create'
        })
      }
    },
    computed: {
      rows() {
        return this.items.length
      }
    }
    
  }
</script>