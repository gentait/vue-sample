<template>
  <c-box>
    <c-box pos="fixed" w="100%" h="100px">ヘッダー</c-box>
    <c-flex pt="100px" minH="100vh">
      <c-box w="300px" minH="100%">サイド</c-box>
      <c-box w="100%">
        <detail @save="onSave" />
      </c-box>
    </c-flex>
  </c-box>
</template>

<script>
import Detail from "../components/Detail.vue";

export default {
  name: "Main",
  components: { Detail },
  data: function () {
    return {};
  },
  methods: {
    onSave(input) {
      alert(input);
    },
  },
};
</script>

<style scoped>
</style>