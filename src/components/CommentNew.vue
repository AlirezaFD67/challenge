<template>
  <div>
    <div class="newComment--wraper">
      <div class="d-flex">
        <Avatar class="mr-6" Me="true" />
        <input type="text" placeholder="Start a discussion" />
      </div>
    </div>
  </div>
</template>

<script>
import Avatar from "@/components/Avatar.vue";
export default {
  name: "Comments",

  components: {
    Avatar,
  },
  data() {
    return {};
  },
  mounted() {},
  methods: {

  },
};
</script>
