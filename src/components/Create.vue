<template>
  <div>
    <b-input 
      v-model="subject" 
      placeholder="제목을 입력해 주세요"
    />
    <b-form-textarea 
      v-model="context" 
      placeholder="내용을 입력해 주세요"
      rows="3"
      max-rows="6"
    />
    <b-button @click="updateMode ? updateContent() : uploadContent()">저장</b-button>
    <b-button @click="cancel">취소</b-button>
  </div>
</template>

<script>
import data from '@/data';
export default {
  name: 'Create',
  data() {
    return {
      subject: null,
      context: null,
      userId: 1,
      createdAt: '2024-07-21 20:27:42',
      updatedAt: null,
      updateObject: null,
      updateMode: this.$route.params.contentId > 0 ? true : false,
    };
  },
  created() {
    if(this.$route.params.contentId > 0) {
      const contentId = Number(this.$route.params.contentId)
      this.updateObject = data.Content.filter(item => item.content_id === contentId)[0]
      this.subject = this.updateObject.title;
      this.context = this.updateObject.context;
    }
  },
  methods: {
    /**
     * 게시글 신규 저장 기능  
     * 로그인 기능이 없으므로 userId는 고정값으로 1을 부여한다.  
     * 게시글 번호의 경우 역순 정렬 된 데이터의 첫번째 요소값 + 1을 한다.  
     * (→ 가장 마지막 글번호 + 1이 됨)
     */
    uploadContent() {
      /* 역순 정렬 (내림차순) */
      let items = data.Content.sort((a,b) => b.content_id - a.content_id)
      /* 역순 정렬의 가장 최신 데이터 + 1 */
      const contentId = items[0].content_id +1;
      data.Content.push({
        content_id: contentId,
        user_id: this.userId,
        title: this.subject,
        context: this.context,
        created_at: this.createdAt,
        updated_at: this.updatedAt,
      })
      this.redirectToBoard();
    },

    updateContent() {
      /* filter를 통해 가져온 데이터는 주소값을 공유하게됨... */
      this.updateObject.title = this.subject;
      this.updateObject.context = this.context;
      this.redirectToBoard();
    },
    
    cancel() {
      this.redirectToBoard();
    },
    
    redirectToBoard() {
      this.$router.push({
        path: '/board/free/'
      })
    }
  },
};
</script>