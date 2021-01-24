<template>
  <div class="comment-dialog">
    <span
      v-on:click="addComment"
      class="close-dialog"></span>

    <textarea 
      name="comment" 
      id="comment-insert" 
      cols="30" 
      ows="10"
      resize="false"
      placeholder="Tell us about your experience with this feature"
      >
    </textarea>

    <button
      class="send-button"
      >Send</button>
  </div>
</template>
<script>
export default {
  name: 'RateDialog',
  props: {
    like: Boolean,
    dislike: Boolean,
    addComment: Function
  }
}
</script>

<style scoped>
.comment-dialog {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  position: absolute;
  margin-top: 28px;
  margin-left: -50px;
  width: 336px;
  height: 237px;
  background: #282828;
  border: 1px solid #181818;
  border-radius: 4px;
}
#comment-insert {
  font-size: 12px;
  font-weight: 400;
  line-height: 16px;
  color: #9E9E9E;
  width: 304px;
  height: 145px;
  text-align: left;
  background-color: #1C1C1C;
  border: 1px solid #64D2FF;
  border-radius: 4px;
  padding: 8px 16px;
  resize: none;
}
.close-dialog {
  background: url("../assets/icon-cross.png");
  background-size: contain;
  width: 16px;
  height: 16px;
  display: inline-block;
  align-self: flex-end;
  cursor: pointer;
  margin-right: 12px;
}
.send-button {
  color: #fff;
  background-color: #3A75AD;
  border: 1px solid #181818;
  border-radius: 4px;
  padding: 8px 16px;
  margin-right: 16px;
  align-self: flex-end;
}
</style>