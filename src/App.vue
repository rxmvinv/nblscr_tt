<template>
  <div class="container-fluid app-container">
    <div class="row">
      <SideBar v-bind:counter="newsCounter" />
      <main role="main" class="main-container ml-sm-auto col-lg-10 d-flex justify-content-center">
        <!-- <div class="row"> -->
          <Header />
        <!-- </div>
        <div class="row"> -->
          <div class="custom-centered">
          <div v-on:scroll="handleScroll" class="post-container">
            <Tabs v-bind:header="tabsHeader" v-bind:isFixed="fixedPanel" />
            <div 
              class="post-list">
              <Post
                v-for="(post, index) in posts" 
                v-bind="post"
                v-bind:key="post.title"
                v-bind:index="index"
                v-bind:showVideo="showVideo"
                v-on:click="selectPost(index, post.active)" />
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

export default {
  name: 'App',
  components: {
    SideBar,
    Header,
    Tabs,
    Post
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
      tabsHeader: "Latest Updates"
    }
  },
  methods: {
    handleScroll (event) {
      this.fixedPanel = event.target.scrollTop >= 80;
    },
    selectPost(ind, act) {
      console.log(ind, act);
      //TODO: 4. tooltip functionality if active index < length increase counter
      
      // let allPosts = this.posts.length - 1;
      // if (!act) { 
      //   allPosts - (ind + 1)
      //   this.newsCounter = ;
      // }

      // TODO: 5. opened post: (route), active switch, dropdown, content:(text, image), comment, like, dislike, scrolling*
      // * back-dropdown-comment-like-dislike panel remaining
      //(6. comment/like/dislike form, warns popups)
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
}
.app-container {
  background: #232323;
}
main.main-container {
  padding: 0;
  flex-direction: column;
  align-self: flex-start;
}
.post-container {
  overflow-y: scroll;
  height: calc(100vh - 76px);
  margin-top: 76px;
  
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
  /* padding: 0 11.5%; */
}
.video-modal {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(34,34,34,0.96);
  display: flex;
  align-items: center;
  justify-content: center;
}
.video-modal .dialog {
  width: 751px;
  height: 424px;
  margin: auto;
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
</style>
