<template>
  <div  >
    <div class="comments--wraper" v-for="(item, index) in comments" :key="index">
      <div class="d-flex">
        <div class="relative line-h mr-6">
          <Avatar class="mr-6" :Src="item.user.avatar" :Name="item.user.name" />
        </div>
        <div class="column">
          <div class="d-flex mb-3">
            <h3 class="comment--name mr-2">{{ item.user.name }}</h3>
            <span class="comment--date">{{ changeTime(item.date) }}</span>
          </div>
          <p class="comment--text mb-3">{{ item.text }}</p>
          <div class="d-flex align-items-center">
            <Like :ILikedIt="item.iLikedIt" :Likes="item.likes" @Liked="liked(index)" />
            <span class="btn-reply" @click="reply(index)">Reply</span>
          </div>
          <CommentReplys v-if="item.replies.length > 0" :Replys="item.replies"  @ChildLiked="childLiked($event, index)" />
          <div v-if="replyActiveIndex == index" class="d-flex mt-8">
            <Avatar class="mr-6" Me="true" />
            <input type="text" placeholder="Reply" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Avatar from "@/components/Avatar.vue";
import Like from "@/components/Like.vue";
import CommentReplys from "@/components/CommentReplys.vue";
import json from "@/assets/data/data.json";
import { formatTime } from "@/assets/js/Global";
export default {
  name: "Comments",
  components: {
    Avatar,
    CommentReplys,
    Like,
  },
  data() {
    return {
      comments: [],
      replyActiveIndex: 0,
    };
  },
  mounted() {
    this.comments_get();
  },
  methods: {
    changeTime(time) {
      return formatTime(time);
    },
    reply(index) {
      // for active replay for item was clicked
      this.replyActiveIndex = index;
    },
    async comments_get() {
      this.comments = json;
    },
    liked(index) {
      if (this.comments[index].iLikedIt == true) {
        this.comments[index].iLikedIt = false;
        this.comments[index].likes = this.comments[index].likes - 1;
      } else {
        this.comments[index].iLikedIt = true;
        this.comments[index].likes = this.comments[index].likes + 1;
      }
    },
    childLiked($event, index) {
      // $event =  child index
      if (this.comments[index].replies[$event].iLikedIt == true) {
        this.comments[index].replies[$event].iLikedIt = false;
        this.comments[index].replies[$event].likes = this.comments[index].replies[$event].likes - 1;
      } else {
        this.comments[index].replies[$event].iLikedIt = true;
        this.comments[index].replies[$event].likes = this.comments[index].replies[$event].likes + 1;
      }
    },
  },
};
</script>
