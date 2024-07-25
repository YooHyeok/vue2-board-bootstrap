<template>
  <div>
    <div class="comment-list-item">
      <div class="comment-list-item-name">
        <div>{{userName}}</div>
        <div>{{commentObj.created_at}}</div>
      </div>
      <div class="comment-list-item-context">{{commentObj.context}}</div>
      <div class="comment-list-item-button">
        <b-button variant="info">수정</b-button>
        <b-button variant="info">삭제</b-button>
      </div>
    </div>
    <!-- 대댓글 -->
    <template v-if="subCommentList.length > 0">
      <div
        class="comment-list-item-subcomment-list"
        :key="subComment.subcomment_id"
        v-for="subComment in subCommentList"
      >
      <div class="comment-list-item-name">
        <div>{{subComment.user_name}}</div>
        <div>{{subComment.created_at}}</div>
      </div>
      <div class="comment-list-item-context">{{subComment.context}}</div>
      <div class="comment-list-item-button">
        <b-button variant="info">수정</b-button>
        <b-button variant="info">삭제</b-button>
      </div>
      </div>
    </template>
  </div>
</template>

<script>
import data from '@/data'
export default {

  name: 'CommentListItem',
  props: {
    commentObj: Object
  },
  data() {
    return {
      userName: data.User.filter(item => item.user_id === this.commentObj.user_id)[0].name,
      subCommentList: data.SubComment
      .filter(item => item.comment_id === this.commentObj.comment_id) // 대댓글 필터링 - 부모 댓글의 commentId PK와 일치하는 commentId 기준
      .map(subCommentItem => ( // user_id가 일치하는 name 저장 (객체 반환을 위해 괄호로 묶음.)
          {
            ...subCommentItem,
            user_name: data.User.filter(item => item.user_id === subCommentItem.user_id)[0].name
          }
        )
      )
    };
  },

  mounted() {
    
  },

  methods: {
    
  },
};
</script>
<style>
.comment-list-item {
  display: flex;
  justify-content: space-between;
  padding-bottom: 1em;
}

.comment-list-item-name {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 0.5px solid black;
  padding: 1em;
}

.comment-list-item-context {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50em;
  border: 0.5px solid black;
}

.comment-list-item-button {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 0.5px solid black;
  padding: 1em;
}

.btn {
  margin-bottom: 1em;
}

.comment-list-item-subcomment-list {
  display: flex;
  justify-content: space-between;
  padding-bottom: 1em;
  margin-left: 10em;
}
</style>
