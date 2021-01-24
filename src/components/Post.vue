<template>
  <div class="post-wrapper">
    <div v-if="isActive" class="custom-tooltip">
      You are here 
      <span class="tooltipt-right-icon"></span>
    </div>
    <div class="custom-centered one-post"
      v-bind:class="{ active: isActive }"
    >
      <div class="post-content-section" 
        v-bind:class="{full: !postMedia}"
        v-on:click="selectPost(index, isActive)"
        >
        <div class="post-top-section">
          <div class="post-title">
            {{postTitle}}
          </div>
          <div class="post-text">
            {{postText}}
          </div>
        </div>
        <div class="post-bottom-section">
          <div class="tests-list">
            <div 
              class="test" 
              v-for="(test, index) in postTestResults" 
              v-bind="test"
              v-bind:key="test.label"
              v-bind:class="{first: index === 0}"
              v-on:click="onSwitchAction(index)"
            >
              <span>
                {{test.label}} {{test.result}}
              </span>
            </div>
          </div>
        </div>
      </div>
      <div v-if="postMedia" class="media-section" v-on:click="showVideo({url: postMedia.url, title: postTitle})">
        <img :src="`../${postMedia.preview}`" v-bind:alt="img" />
        <div class="play-icon"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Post',
  props: {
    title: String,
    text: String,
    media: Object,
    active: Boolean,
    index: Number,
    testResults: Array,
    showVideo: Function,
    selectPost: Function
  },
  data () {
    return {
      postTitle: this.title,
      postText: this.text,
      isActive: this.active,
      postMedia: this.media,
      postTestResults: this.testResults
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.post-wrapper {
  display: inline-flex;
}
.one-post {
  color: #fff;
  background-color: #282828;
  height: 156px;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;
}
.one-post.active {
  margin-right: 110px;
}
.post-wrapper.last {
  margin-bottom: 236px;
}
.post-content-section {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  flex-basis: 80%;
  cursor: pointer;
}
.post-content-section.full {
  flex-basis: 100%;
}
.post-top-section {
  display: flex;
  flex-direction: column;
  flex-basis: 70%;
  justify-content: space-evenly;
  padding-left: 24px;
}
.post-title {
  font-size: 16px;
  display: flex;
}
.post-text {
  text-align: left;
  font-size: 12px;
  display: flex;
}
.post-bottom-section {
  display: flex;
  align-items: center;
  padding-left: 24px;
  border-top: 1px solid #181818;
  flex-basis: 30%;
}
.tests-list {
  display: flex;
  color: #64D2FF;
  font-size: 12px;
  font-weight: 400;
}
.test::before {
  content: "\2022";
  color: #64D2FF;
  padding: 0 8px;
}
.test.first::before {
  display: none;
}
.media-section {
  display: flex;
  flex-basis: 20%;
  cursor: pointer;
  position: relative;
}
.media-section img {
  width: 100%;
}
.media-section .play-icon {
  background: url('../assets/icon-youtube.png');
  background-size: contain;
  display: block;
  width: 50px;
  height: 50px;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
}
.media-section:hover .play-icon {
  background: url('../assets/icon-youtube-active.png');
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}
.custom-tooltip {
  width: 102px;
  height: 32px;
  border: 1px solid #484848;
  border-radius: 26px;
  font-size: 11px;
  color: #fff;
  opacity: 1;
  margin-right: 8px;
  margin-top: 8px;
  font-size: 11px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.custom-tooltip:hover {
  border: 1px solid #9E9E9E;
}
.tooltipt-right-icon {
  background: url('../assets/icon-right.png');
  background-size: contain;
  display: inline-block;
  width: 12px;
  height: 8px;
  margin-left: 5px;
}
</style>
