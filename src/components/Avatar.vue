<template>
  <div class="avatar">
    <img v-if="Src" :src="Src" :alt="Name" />
    <img v-if="Me == 'true'" src="@/assets/img/myAvatar.jpg" :alt="Name" />
    <span v-if="!Src && !Me">{{ split }}</span>
  </div>
</template>

<script>
export default {
  name: "Avatar",
  props: {
    // Src exists -> img src = Src
    Src: {
      type: String,
      defult: "",
    },
      // Src does not exists -> img src =  first letter of the name + fname
    Name: {
      type: String,
      defult: "",
    },
    Me: {
      // My account does not have a url or name -> img Src = local image
      type: Boolean,
      defult: false,
    },
  },
  data() {
    return {
      split: "",
    };
  },
  mounted() {
    this.setAvatar();
    // console.log('me=  ',Me);
  },
  methods: {
    setAvatar() {
      if (!this.Src && this.Name) {
        this.split = this.Name.split(" ")
          .map(function (s) {
            return s.charAt(0);
          })
          .join("");
      }
    },
  },
};
</script>
