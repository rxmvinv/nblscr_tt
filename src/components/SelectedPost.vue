<template>
  <div 
    class="selected-post"
    v-on:scroll="handleScroll" 
    >
      <div class="post-title">
        <button 
          class="return-back"
          v-on:click="selectPost(-1, null)"
          >
          <span class="chevron-left-icon"></span>
        </button>
        <div class="post-title-text">
          {{postData.title}}
        </div>
      </div>
      <PostMenu />
      <div 
        class="post-section"
        v-bind:class="{'post-section-unscrolled': !isFixed}"
        >
          <div 
            class="section-header"
            v-bind:class="{'section-header-fixed': isFixed}"
            >
            <div class="section-header-content">
              <button 
                class="return-back"
                v-on:click="selectPost(-1, null)"
                v-if="isFixed"
                >
                <span class="chevron-left-icon"></span>
              </button>
              <div 
                class="section-title"
                v-if="!isFixed"
                >PCB</div>
              <div class="section-subtitle">
                Project and Design File Renaming
                <button 
                  class="dropdown-button" 
                  v-if="isFixed"
                  v-on:click="expandMenu"
                  >
                  <span 
                    class="dropdown-button-icon"
                    v-bind:class="{expanded: expandedMenu}"
                    ></span>
                </button>
                <PostMenu
                  v-if="expandedMenu && isFixed"
                  v-bind:class="{expanded: expandedMenu}"
                 />
              </div>
              <UserActions />
            </div>
          </div>
          <div class="section-content">
            <div
              class="post-content"
              v-for="(content, index) in postContent"
              v-bind:key="`${index}-selected-post`"
              v-bind:class="{last: index === postContent.length -1}"
            >
              <div class="post-section-text">
                {{content.text}}
              </div>
              <div class="post-section-media">
                <img :src="getPic(content.media)" alt="post-img" />
              </div>
            </div>
          </div>
      </div>
  </div>
</template>

<script>
import PostMenu from './PostMenu.vue'
import UserActions from './UserActions.vue'

export default {
  name: 'SelectedPost',
  components: {
    PostMenu,
    UserActions
  },
  props: {
    selectPost: Function,
    postData: Object,
    index: Number
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
  },
  data () {
    return {
      isFixed: false,
      postContent: [
        {
          text: `A file Rename command is now available from the right-click context menu in the Projects panel, replacing the Save As command. This allows you to directly change the name of a PCB project (*.PrjPcb) or any of its constituent design files (*.PcbDoc, *.SchDoc, etc) and then save the update to local and VCS remote storage (File » Save to Server).
Note that the Save As command remains available from the main File menu, and a design file also can be renamed from the Storage Manager panel right-click options.`,
          media: 'post_1_image_1'
        },
        {
          text: `File rename synchronization is maintained between local storage and remote server-based storage. Additionally, a renamed project file will invoke an alignment with the project Name on the server side, as outlined in the Project Renaming information below.`,
          media: 'post_1_image_2'
        }
      ],
      expandedMenu: false,
    }
  },
  methods: {
    handleScroll (event) {
      this.isFixed = event.target.scrollTop >= 350;
      this.expandedMenu = this.expandedMenu && event.target.scrollTop >= 350;
    },
    getPic(media) {
      const images = require.context('../assets/', false, /\.png$/);
      return images('./' + media + ".png");
    },
    expandMenu() {
      this.expandedMenu = !this.expandedMenu;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .selected-post {
    margin-top: 75px;
    overflow-y: scroll;
    height: 830px;
  }
  .post-title {
    margin-top: 32px;
    margin-bottom: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .return-back {
    width: 32px;
    height: 32px;
    margin-right: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: none;
    border-radius: 50%;
    border: 1px solid #484848;
    outline: none;
  }
  .return-back:hover, .return-back:active {
    border: 1px solid #9E9E9E;
  } 
  .chevron-left-icon {
    background: url("../assets/icon-chevron-left.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 6px;
    height: 10px;
    display: inline-block;
  }
  .post-title-text {
    width: 820px;
    font-size: 32px;
    color: #fff;
    line-height: 40px;
    margin-right: 56px;
    text-align: left;
  }
  .section-header {
    display: flex;
    width: 100%;
  }
  .section-header-fixed {
    position: absolute;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 18px;
    top: 75px;
    height: 80px;
    background: #232323;
    border-bottom: 1px solid #181818;
  }
  .section-header-content {
    max-width: calc(820px + 56px);
    width: 100%;
    margin-bottom: 24px;
  }
  .section-header-fixed .section-header-content {
    display: flex;
    align-content: center;
    margin-right: 40px;
    margin-bottom: 0;
  }
  .section-title {
    text-align: left;
    font-size: 10px;
    font-weight: 400;
    line-height: 16px;
    color: #9E9E9E;
    margin-bottom: 8px;
  }
  .section-subtitle {
    font-size: 16px;
    line-height: 24px;
    font-weight: 400;
    color: #fff;

    float: left;
  }
  .user-actions {
    float: right;
  }
  .dropdown-button {
    background: none;
    border: none;
    outline: none;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    padding: 8px;
  }
  .dropdown-button-icon {
    background: url("../assets/icon-chevron-down.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 10px;
    height: 6px;
    display: inline-block;
  }
  .post-section {
    width: 820px;
    margin: auto;
    height: 100%;
    display: flex;
    justify-content: center;
    margin-bottom: 20%;
  }
  .post-section-unscrolled {
    flex-direction: column;
  }
  .section-content {
    height: 100%;
    display: flex;
    width: 100%;
    flex-direction: column;
  }
  .post-content {
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  .post-content.last {
    margin-bottom: 20%;
  }
  .post-section {
    margin-top: 78px;
  }
  .post-section-text {
    font-weight: 400;
    font-size: 12px;
    line-height: 23px;
    color: #DDDDDD;
    text-align: left;
  }
  .post-section-media img {
    max-width: 580px;
    width: 100%;
  }
  .post-menu.expanded {
    position: absolute;
    margin-top: 8px;
  }
  .dropdown-button-icon .expanded {
    transform: rotateX(180deg);
  }
</style>
