<template>
  <div class="w-max-content">
    <button class="btn-like mr-7" :class="[ILikedIt ? 'btn-iLikedIt' : 'btn-iDoNotLikedIt']" @click="liked(index)">
      <img class="like-img" src="@/assets/img/like.png" />
       <span>{{ Likes }}</span>
    </button>
  </div>
</template>

<script>
export default {
  name: "Avatar",
  props: {
    ILikedIt: {
      type: Boolean,
      defult: false,
    },
    Likes: {
      type: Number,
      defult: null,
    },
  },
  data() {
    return {
      split: "",
    };
  },
  mounted() {},
  methods: {
    liked() {
      this.$emit("Liked");
    },
  },
};
</script>
