<template>
  <div id="app">
    <CommentNew />
    <Comments />
  </div>
</template>

<script>
import CommentNew from "@/components/CommentNew.vue";
import Comments from "@/components/Comments.vue";
import { sleep } from "@/assets/js/Global";
export default {
  name: "App",
  components: {
    CommentNew,
    Comments,
  },
  mounted() {
    this.findeMentions();
  },
  methods: {
    async findeMentions() {
      await sleep(10); // delay for run next line
      let p_elements = Array.from(document.getElementsByTagName("p"));
      p_elements.map((p_element) => {
        var textContent = p_element.textContent;
        var pattern = /\B@[a-z0-9_-]+/gi;
        var word = textContent.match(pattern);
        if (word) {
          for (var i = 0; i < word.length; i++) {
            var res = p_element.textContent.replace(word[i], '<span class="badge-mention">' + word[i] + "</span>");
            p_element.innerHTML = res;
          }
        }
      });
    },
  },
};
</script>
