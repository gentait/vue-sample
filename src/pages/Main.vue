<template>
  <c-box>
    <c-box pos="fixed" w="100%" h="100px">ヘッダー</c-box>
    <c-flex pt="100px" minH="100vh">
      <c-box w="300px" minH="100%">
        <c-button @click="makeNewMemo">NEW</c-button>
        <c-list spacing="10px">
          <c-list-item
            v-for="memo in memoList"
            :key="memo.id"
            pl="20px"
            fontSize="20px"
            fontWeight="bold"
          >
            <folder
              :id="memo.id"
              :title="memo.title"
              :type="memo.type"
              :items="memo.items"
              @click-file="select"
            />
          </c-list-item>
        </c-list>
      </c-box>
      <c-box w="100%">
        <detail
          v-if="current"
          @save="onSave"
          :title="current.title"
          :text="current.content"
        />
      </c-box>
    </c-flex>
  </c-box>
</template>

<script>
import Detail from "../components/Detail.vue";
import Folder from "../components/Folder.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "Main",
  components: { Detail, Folder },
  data: function () {
    return {
      memoList: [
        { id: "1", title: "foo", content: "foo content", type: "file" },
        { id: "2", title: "bar", content: "bar content", type: "file" },
        {
          id: "3",
          title: "folder",
          items: [
            { id: "4", title: "foo", content: "foo content", type: "file" },
            { id: "5", title: "bar", content: "bar content", type: "file" },
          ],
          type: "folder",
        },
      ],
      selectedId: "",
    };
  },
  computed: {
    current: function () {
      return this.searchTree(this.memoList, this.selectedId);
    },
  },
  created: function () {
    this.memoList = JSON.parse(localStorage.getItem("memoList")) ?? [];
    if (this.memoList.length) {
      this.selectedId = this.memoList[0].id;
    }
  },
  methods: {
    searchTree: function (list, id) {
      for (const item of list) {
        if (item.id == id) return item;
        if (item.items) {
          const result = this.searchTree(item.items, id);
          if (result) return result;
        }
      }
      return null;
    },
    onSave(memo) {
      const currentMemo = this.searchTree(this.memoList, this.selectedId);
      if (currentMemo == null) return;
      console.log({ currentMemo, memo });
      (currentMemo.title = memo.title), (currentMemo.content = memo.content);
      localStorage.setItem("memoList", JSON.stringify(this.memoList));
    },
    select(id) {
      this.selectedId = id;
    },
    makeNewMemo: function () {
      const newMemo = {
        id: uuidv4(),
        title: "new memo",
        content: "",
        type: "file",
      };
      this.memoList.push(newMemo);
      this.select(newMemo.id);
    },
  },
};
</script>

<style scoped>
</style>