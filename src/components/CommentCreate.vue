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
        <b-button variant="info" @click="createComment">작성하기</b-button>
      </b-input-group-append>
    </b-input-group>
</div>
</template>

<script>
import data from "@/data"
export default {
  name: 'pCommentCreate',
  props: {
    contentId: Number,
    reloadComment: Function
  },
  data() {
    return {
      name: "유혁스쿨",
      context: ""
    };
  },
  methods: {
    createComment() {
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
      thisreloadComment();
    }
  },
};
</script>