<template>
  <div>
    <div :key="item.comment_id" v-for="item in comments">
        <CommentListItem :commentObj="item"/>
    </div>
    <CommentCreate 
    :contentId="contentId"
    :reloadComment="reloadComment"
    />
  </div>
</template>
<script>
import data from '@/data'
import CommentListItem from '@/components/CommentListItem.vue';
import CommentCreate from '@/components/CommentCreate.vue';

export default {
  name: 'CommentList',
  components: {
    CommentListItem,
    CommentCreate
  },
  props: {
    contentId: Number,
  },
  data() {
    return {
      comments: data.Comment.filter(item => item.content_id === this.contentId)
    }
  },
  methods: {
    /**
     * 댓글 리스트를 리로드 한다.
     * comments 최신 data로부터 다시 초기화 한다.
     */
    reloadComment() {
      this.comments = data.Comment.filter(item => item.content_id === this.contentId)
    }
  }
}
</script>