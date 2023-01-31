<template>
  <div>
    <div>
      <div class="commentReplys--wraper my-6" v-for="(item, index) in Replys" :key="index">
        <div class="d-flex">
          <Avatar class="mr-6" :Src="item.user.avatar" :Name="item.user.name" />
          <div class="column">
            <div class="d-flex mb-3">
              <h3 class="comment--name mr-2">{{ item.user.name }}</h3>
              <span class="comment--date">{{ changeTime(item.date) }}</span>
            </div>
            <p class="comment--text mb-3">{{ item.text }}</p>
            <Like :ILikedIt="item.iLikedIt" :Likes="item.likes" @Liked="liked(index)" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Avatar from "@/components/Avatar.vue";
import Like from "@/components/Like.vue";
import { formatTime } from "@/assets/js/Global";
export default {
  name: "CommentReplys",
  components: {
    Avatar,
    Like,
  },
  props: {
    Replys: {
      type: Array,
      defult: [],
    },
    ParentIndex: {
      type: Number,
      defult: 0,
    },
    ReplyActiveIndex: {
      type: Number,
      defult: 0,
    },
  },
  // watch: {
  //   // if another reply key is clicked,This is changing
  //   ReplyActiveIndex: {
  //     deep: true,
  //     handler: function (newVal, oldVal) {
  //       this.checkReplyActive();
  //     },
  //   },
  // },
  data() {
    return {
      // replyActive: false,
    };
  },
  mounted() {
    // this.checkReplyActive();
  },
  methods: {
    changeTime(time) {
      return formatTime(time);
    },
    // checkReplyActive() {
    //   if (this.ReplyActiveIndex == this.ParentIndex) {
    //     this.replyActive = true;
    //   } else {
    //     this.replyActive = false;
    //   }
    // },
    liked(index) {
      // emit to comments component for change
      this.$emit("childLiked", index);
    },
  },
};
</script>
