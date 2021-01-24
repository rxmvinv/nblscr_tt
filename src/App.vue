<template>
  <div class="app-container">
    <div class="content-row">
      <SideBar v-bind:counter="newsCounter" />
      <main role="main" class="main-container">
          <Header />
          <div class="content-container">
              <SelectedPost 
                v-if="currentPost.title"
                v-bind:selectPost="selectPost"
                v-bind:postData="currentPost"
                v-bind:index="index"
               />
            <div 
              v-on:scroll="handleScroll" 
              class="post-container"
              v-else
              >
              <Tabs 
                v-bind:header="tabsHeader" 
                v-bind:isFixed="fixedPanel" 
                />
              <div 
                class="post-list"
                v-bind:class="{'post-list-fixed': fixedPanel}"
                >
                <Post
                  v-for="(post, index) in posts" 
                  v-bind="post"
                  v-bind:key="post.title"
                  v-bind:class="{last: index === (posts.length - 1)}"
                  v-bind:index="index"
                  v-bind:showVideo="showVideo"
                  v-bind:selectPost="selectPost" />
              </div>
            </div>
          </div>
        <!-- </div> -->
        <div v-if="playingVideo" class="video-modal">
          <div class="dialog">
            <div class="video-header">
              {{playingVideo.title}}
              <button v-on:click="showVideo({})">x</button>
            </div>
            <video controls autoplay :src="playingVideo.url" />
            <div class="play-button"></div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import SideBar from './components/SideBar.vue'
import Header from './components/Header.vue'
import Tabs from './components/Tabs.vue'
import Post from './components/Post.vue'
import SelectedPost from './components/SelectedPost.vue'

export default {
  name: 'App',
  components: {
    SideBar,
    Header,
    Tabs,
    Post,
    SelectedPost
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
  },
  data() {
    return {
      posts: [
        {
          title: 'October 2020',
          text: `EDA tools have come a long way since the advent of personal computing. 
          Now advanced routing features like auto-routers, 
          interactive routing, length tuning, and...`,
          media: {url: '/someurl', preview: 'assets/video-preview.png'},
          active: false,
          testResults: [
            {
              label: 'Test 1',
              result: 7
            },
            {
              label: 'Test 2',
              result: 15
            },
            {
              label: 'Test 3',
              result: 4
            },
            {
              label: 'Test 4',
              result: 2
            },
          ]
        },
        {
          title: 'September 2020',
          text: `EDA tools have come a long way since the advent of personal computing. 
          Now advanced routing features like auto-routers, 
          interactive routing, length tuning, and...`,
          media: {url: '/someurl', preview: 'assets/video-preview.png'},
          active: true,
          testResults: [
            {
              label: 'Test 1',
              result: 7
            },
            {
              label: 'Test 2',
              result: 15
            },
            {
              label: 'Test 3',
              result: 4
            },
            {
              label: 'Test 4',
              result: 2
            },
          ]
        },
        {
          title: 'August 2020',
          text: `EDA tools have come a long way since the advent of personal computing. 
          Now advanced routing features like auto-routers, 
          interactive routing, length tuning, and...`,
          media: {url: '/someurl', preview: 'assets/video-preview.png'},
          active: false,
          testResults: [
            {
              label: 'Test 1',
              result: 7
            },
            {
              label: 'Test 2',
              result: 15
            },
            {
              label: 'Test 3',
              result: 4
            },
            {
              label: 'Test 4',
              result: 2
            },
          ]
        },
        {
          title: 'July 2020',
          text: `EDA tools have come a long way since the advent of personal computing. 
          Now advanced routing features like auto-routers, 
          interactive routing, length tuning, and...`,
          media: null,
          active: false,
          testResults: [
            {
              label: 'Test 1',
              result: 7
            },
            {
              label: 'Test 2',
              result: 15
            },
            {
              label: 'Test 3',
              result: 4
            },
            {
              label: 'Test 4',
              result: 2
            },
          ]
        }
      ],
      fixedPanel: false,
      newsCounter: 5,
      playingVideo: null,
      tabsHeader: "Latest Updates",
      currentPost: {}
    }
  },
  methods: {
    handleScroll (event) {
      this.fixedPanel = event.target.scrollTop >= 80;
    },
    selectPost(ind, act) {
      console.log(ind, act);
      this.currentPost = (ind >= 0) && this.posts[ind];
    },
    checkUpdates() {

    },
    showVideo({title, url}) {
      this.playingVideo = (url && title) && {title, url};
      console.log(url);
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter&display=swap');

#app {
  font-family: 'Inter', Avenir, Helvetica, Arial, sans-serif;
  font-weight: 500;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  display: flex;
  align-items: center;
  height: 100vh;
  background: #353535;
}
.content-row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
}
.app-container {
  background: #232323;
  max-width: 1308px;
  max-height: 833px;
  height: 100vh;
  margin-right: 8px;
  overflow: hidden;

  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-left: auto;
}
main.main-container {
  padding: 0;
  flex-direction: column;
  align-self: flex-start;
  margin-left: 0;
  justify-content: center;
  display: flex;
  max-width: 81.6%;
  position: relative;
  width: 100%;
}
.content-container {
  height: 100%;
  max-height: 831px;
  overflow-y: hidden;
  margin-right: -20px;
}
.post-container {
  overflow-y: scroll;
  height: calc(100vh - 76px);
  margin-top: 76px;
  height: 100vh;
}
.post-list {
  width: 100%;
  max-width: 1040px;
  margin: auto;
}
.post-list-fixed {
  margin-top: 156px;
}
::-webkit-scrollbar {
  display: none;
}
.custom-centered {
  max-width: 820px;
  display: flex;
  margin: auto;
  justify-content: space-between;
  width: 100%;
}
.video-modal {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(34,34,34,0.96);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 3;
}
.video-modal .dialog {
  width: 751px;
  height: 424px;
  margin: auto;
  position: relative;
}
.video-modal .dialog video {
  width: 100%;
  height: 100%;
}
.video-modal .dialog .video-header {
  background: #484848;
  display: flex;
  justify-content: space-between;
  padding: 0 5px;
  padding-left: 16px;
  align-items: center;
  color: #fff;
  font-size: 12px;
  height: 32px;
}
.video-modal .dialog .video-header button {
  background: url("./assets/icon-cross.png");
  background-size: contain;
  width: 16px;
  height: 16px;
  display: inline-block;
  border: none;
  color: transparent;
}
.video-modal .dialog .play-button {
  background: url('./assets/icon-youtube.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  width: 64px;
  height: 45px;
  position: absolute;
  margin: auto;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
@media screen and (min-width: 1680) {
  .app-container {
    margin-left: 364px;
    max-width: 90%;
  }
}
</style>
