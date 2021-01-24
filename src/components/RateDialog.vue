<template>
  <div class="rate-dialog">
    <span
      v-if="like"
      class="rate-like"></span>

    <span
      v-if="dislike"
      class="rate-dislike"></span>

    <div class="rate-text">
        Like the feature?
        <br />
        <a href="#" >Sign in</a> to appreciate it
    </div>
  </div>
</template>
<script>
export default {
  name: 'RateDialog',
  props: {
    like: Boolean,
    dislike: Boolean
  }
}
</script>

<style scoped>
.rate-dialog {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  position: absolute;
  margin-top: 28px;
  width: 284px;
  height: 96px;
  background: #282828;
  border: 1px solid #181818;
  border-radius: 4px;
}
.rate-text {
  font-size: 12px;
  font-weight: 400;
  line-height: 16px;
  color: #fff;
  width: 174px;
  height: 32px;
  text-align: left;
}
.rate-like {
  background: url("../assets/icon-thumb-up-active.png");
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  width: 32px;
  height: 32px;
  display: inline-block;
}
.rate-dislike {
  background: url("../assets/icon-thumb-down-active.png");
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  width: 32px;
  height: 32px;
  display: inline-block;
}
</style>