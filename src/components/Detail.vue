<template>
  <div>
    <keep-alive>
      <c-input
        v-if="isEditMode"
        placeholder="Basic usage"
        v-model="inputTitle"
      />
      <c-heading v-else>{{ inputTitle }}</c-heading>
    </keep-alive>
    <c-button variant-color="blue" size="md" @click="togglePreview">{{
      this.isEditMode ? "Preview" : "Edit"
    }}</c-button>
    <keep-alive>
      <c-textarea v-if="isEditMode" v-model="inputText" :value="inputText" />
      <c-box v-else p="10px">
        <mark-down-viewer :rawtext="inputText" />
      </c-box>
    </keep-alive>
    <c-button variant-color="blue" size="md" @click="save">Save</c-button>
  </div>
</template>

<script>
import MarkDownViewer from "./MarkDownViewer.vue";
export default {
  components: { MarkDownViewer },
  props: ["title", "text", "editMode"],
  data: function () {
    return {
      inputTitle: this.title,
      inputText: this.text,
      isEditMode: this.editMode ?? false,
    };
  },
  watch: {
    text: function () {
      this.inputText = this.text;
      this.isEditMode = false;
    },
    title: function () {
      this.inputTitle = this.title;
      this.isEditMode = false;
    },
  },
  methods: {
    togglePreview() {
      this.isEditMode = !this.isEditMode;
    },
    save() {
      this.$emit("save", { title: this.inputTitle, content: this.inputText });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>