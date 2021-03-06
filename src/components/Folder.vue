<template>
  <div v-if="isFolder">
    <details>
      <summary>{{ title }}</summary>
      <ul class="list">
        <li v-for="item in items" :key="item.id">
          <folder
            :id="item.id"
            :title="item.title"
            :type="item.type"
            :items="item.items"
            @click-file="onClickFile"
          />
        </li>
      </ul>
    </details>
  </div>
  <p v-else @click="onClickFile(id)">{{ title }}</p>
</template>

<script>
export default {
  name: "Folder",
  props: {
    id: { type: String },
    title: { type: String, required: true },
    type: { type: String, required: true },
    items: { type: Array },
    content: { type: String },
  },
  computed: {
    isFolder: function () {
      return this.type === "folder";
    },
  },
  methods: {
    onClickFile: function (id) {
      this.$emit("click-file", id);
    },
  },
};
</script>

<style lang="scss" scoped>
.list {
  list-style: none;
  padding-left: 10px;
}
</style>