<template>
  <c-box>
    <c-box pos="fixed" w="100%" h="100px">ヘッダー</c-box>
    <c-flex pt="100px" minH="100vh">
      <c-box w="300px" minH="100%">
        <c-list spacing="10px">
          <c-list-item
            v-for="memo in memoList"
            :key="memo.title"
            pl="20px"
            fontSize="20px"
            fontWeight="bold"
          >
            <div @click="select(memo)">
              {{ memo.title }}
            </div>
          </c-list-item>
        </c-list>
      </c-box>
      <c-box w="100%">
        <detail @save="onSave" :title="current.title" :text="current.content" />
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
    return {
      memoList: [
        { id: 1, title: "foo", content: "foo content" },
        { id: 2, title: "bar", content: "bar content" },
      ],
      selectedId: "",
    };
  },
  computed: {
    current: function () {
      return this.memoList.find((item) => item.id === this.selectedId);
    },
  },
  created: function () {
    if (this.memoList.length) {
      this.selectedId = this.memoList[0].id;
    }
  },
  methods: {
    onSave(memo) {
      const currentMemo = this.memoList.find(
        (item) => item.id === this.selectedId
      );
      (currentMemo.title = memo.title), (currentMemo.content = memo.content);
    },
    select(item) {
      this.selectedId = item.id;
    },
  },
};
</script>

<style scoped>
</style>