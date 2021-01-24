<template>
<div class="user-actions">
    <div 
      class="action first"
      v-on:click="addComment"
      >
        <span class="comment-action"></span>16
    </div> 
    <span 
        class="action-pipe" 
    ></span>
    <div 
        class="action"
        v-on:click="addLike"
        v-bind:class="{selected: liked}"
        >
        <span class="like-action"></span>{{likedCount}}
    </div> 
    <div class="action" 
        v-on:click="addDisike"
        v-bind:class="{selected: disliked}"
        >
        <span class="dislike-action"></span>{{dislikedCount}}
    </div> 
    <RateDialog
      v-if="liked || disliked"
      v-bind:like="liked"
      v-bind:dislike="disliked"
      />
    <CommentDialog
      v-if="commentForm"
      v-bind:addComment="addComment"
      />
</div>
</template>
<script>
import RateDialog from './RateDialog';
import CommentDialog from './CommentDialog';

export default {
  name: 'UserActions',
  components: {
    RateDialog,
    CommentDialog
  },
  data () {
    return {
      liked: false,
      likedCount: 43,
      dislikedCount: 43,
      disliked: false,
      commentForm: false
    }
  },
  methods: {
    addLike() {
      this.liked = !this.liked;
      this.likedCount = this.liked ? this.likedCount+1 : this.likedCount-1;
      this.dislikedCount = this.liked ? this.likedCount-1 : this.likedCount;
      this.disliked = false;
    }, 
    addDisike() {
      this.disliked = !this.disliked;
      this.dislikedCount = this.disliked ? this.dislikedCount+1 : this.dislikedCount-1;
      this.likedCount = this.disliked ? this.dislikedCount-1 : this.dislikedCount;
      this.liked = false;
    },
    addComment() {
      this.commentForm = !this.commentForm;
    }
  }
}
</script>

<style scoped>
  .user-actions {
    margin-left: auto;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    position: relative;
  }
  .user-actions .action {
    color: #9E9E9E;
    margin: 0 8px;
    cursor: pointer;
    user-select: none;
  }
  .user-actions .action:hover, 
  .user-actions .action:active {
    color: #fff;
  }
  .user-actions .action.first {
    margin-right: 16px;
  } 
  .user-actions .action span {
    margin-right: 8px;
  }
  .user-actions .comment-action {
    background: url("../assets/icon-comment.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 16px;
    height: 14px;
    display: inline-block;
  }
  .user-actions .action:hover .comment-action,
  .user-actions .action:active .comment-action {
    background: url("../assets/icon-comment-active.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  .user-actions .action-pipe {
    display: flex;
    width: 1px;
    height: 24px;

    background-color: #181818;
    margin-left: 8px;
    margin-right: 8px;
  }
  .user-actions .like-action {
    background: url("../assets/icon-thumb-up.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 16px;
    height: 16px;
    display: inline-block;
  }
  .user-actions .action:hover .like-action,
  .user-actions .action:active .like-action {
    background: url("../assets/icon-thumb-up-active.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  .user-actions .action.selected .like-action {
    background: url("../assets/icon-thumb-up-selected.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  .user-actions .dislike-action {
    background: url("../assets/icon-thumb-down.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: 16px;
    height: 16px;
    display: inline-block;
  }
  .user-actions .action:hover .dislike-action,
  .user-actions .action:active .dislike-action {
    background: url("../assets/icon-thumb-down-active.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
  .user-actions .action.selected .dislike-action {
    background: url("../assets/icon-thumb-down-selected.png");
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
  }
</style>