<template>
  <div>
    <textarea name="" id="" cols="30" rows="10" v-model="text"></textarea>
    <div v-html="mdText"></div>
  </div>
</template>

<script>
import marked from "marked";
export default {
  data: function () {
    return {
      editable: true,
      text: "入力してください",
    };
  },
  computed: {
    mdText() {
      return marked(this.escapeHtml(this.text));
    },
  },
  methods: {
    escapeHtml(str) {
      str = str.replace(/&/g, "&amp;");
      str = str.replace(/</g, "&lt;");
      str = str.replace(/>/g, "&gt;");
      str = str.replace(/"/g, "&quot;");
      str = str.replace(/'/g, "&#39;");
      return str;
    },
  },
};
</script>

<style scoped>
</style>