<template>
  <div>
    <b-card>
      <div class="content-detail-content-info">
        <div class="content-detail-content-info-left">
          <div class="content-detail-content-info-left-number">
            {{contentId}}
          </div>
          <div class="content-detail-content-info-left-subject">
            {{title}}
          </div>
        </div>
        <div class="content-detail-content-info-right">
          <div class="content-detail-content-info-right-user">
            글쓴이: {{user}}
          </div>
          <div class="content-detail-content-info-right-created">
            등록일: {{created}}
          </div>
        </div>
      </div>
      <div class="content-detail-content">
        {{context}}
      </div>
      <div class="content-detail-button">
        <b-button variant="primary" @click="updateData">수정</b-button>
        <b-button variant="success" @click="deleteData">삭제</b-button>
      </div>
      <div class="content-detail-comment">
        <CommentList :contentId="contentId"/>
      </div>
    </b-card>
  </div>
</template>

<script>
import data from '@/data';
import CommentList from '@/components/CommentList.vue';
import { findContent } from '@/service';

export default {
  name: 'ContentDetail',
  components: {
    CommentList
  },
  async created() {
    /* 게시글 상세내용 service를 통해 DB접근 조회 */
    const ret = await findContent( {content_id: Number(this.$route.params.contentId)} )
    const {data} = ret
    this.title = data.title;
    this.context = data.context;
    this.user = data.user_name;
    this.created = data.created_at;
  },
  data() {
    const contentId = Number(this.$route.params.contentId); // 파라미터 숫자 변환
    const contentData = data.Content.filter(item => item.content_id === contentId)[0] // 일치하는 ID에 해당하는 Content 반환
    return {
      contentId: contentId,
      title: contentData.title,
      context: contentData.context,
      user: data.User.filter(item => item.user_id === contentData.user_id)[0]
        .name,
      created: contentData.created_at
    };
  },
  methods: {
    deleteData() {
      /* findIndex: 해당 조건이 참인 객체의 index값 반환 */
      const contentIndex = data.Content.findIndex(item => item.content_id === this.contentId);
      console.log(contentIndex)
      /* 배열로부터 index 기준 제거 */
      data.Content.splice(contentIndex, 1);
      this.$router.push({
        path:`/board/free`
      })
    },
    updateData() {
      this.$router.push({
        path:`/board/free/create/${this.contentId}`
      })
    }
  }
}
</script>
<style scoped>
.content-detail-content-info {
  border: 1px solid black;
  display: flex;
  justify-content: space-between;
}

.content-detail-content-info-left {
  width: 720px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
}

.content-detail-content-info-right {
  width: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.content-detail-content {
  border: 1px solid black;
  margin-top: 1rem;
  padding-top: 1rem;
  min-height: 720px;
}

.content-detail-button {
  border: 1px solid black;
  margin-top: 1rem;
  padding: 2rem;
}

.content-detail-comment {
  border: 1px solid black;
  margin-top: 1rem;
  padding: 2rem;
}
</style>
