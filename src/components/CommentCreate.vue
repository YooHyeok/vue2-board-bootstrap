<template>
  <div>
    <b-input-group :prepend="name" class="mt-3">
      <b-form-textarea
        id="textarea"
        v-model="context"
        :placeholder="'코멘트를 달아주세요~!'"
        rows="3"
        max-rows="6"
      ></b-form-textarea>
      <b-input-group-append>
        <b-button variant="info" @click="isSubComment ? createSubComment() : createComment()">작성하기</b-button>
      </b-input-group-append>
    </b-input-group>
</div>
</template>

<script>
import data from "@/data"
import { addComment, addSubComment } from '@/service';

export default {
  name: 'CommentCreate',
  props: {
    contentId: Number,
    commentId: Number,
    isSubComment: Boolean,
    reloadComment: Function,
    subCommentToggle:Function,
    reloadSubComment: Function
  },
  data() {
    return {
      name: "유혁스쿨",
      context: ""
    };
  },
  methods: {
    createComment_deprecated() {
      data.Comment.push(
        {
          comment_id: data.Comment[data.Comment.length - 1].comment_id+1, // data의 Comment의 마지막 요소를 가지고온 뒤 해당 객체의 comment_id + 1을 한다.
          user_id: 1,
          content_id: this.contentId,
          context: this.context,
          created_at: '2024-07-24 21:55:11',
          updated_at: null,
        }
      )
      this.reloadComment();
    },
    async createComment() {
      await addComment({
        user_id: 1,
        content_id: this.contentId,
        context: this.context,
      })
      this.context = ""
      this.reloadComment();
    },
    createSubComment_deprecated() {
      data.SubComment.push(
        {
          subcomment_id: data.SubComment[data.SubComment.length - 1].subcomment_id+1, // data의 Comment의 마지막 요소를 가지고온 뒤 해당 객체의 comment_id + 1을 한다.
          user_id: 1,
          comment_id: this.commentId,
          context: this.context,
          created_at: '2024-07-24 21:55:11',
          updated_at: null,
        }
      )
      this.subCommentToggle()
      this.reloadSubComment();
    },
    async createSubComment() {
      await addSubComment({
          user_id: 1,
          comment_id: this.commentId,
          context: this.context,
      })
      this.subCommentToggle()
      this.reloadSubComment();
    }
  },
};
</script>