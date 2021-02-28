<template>
  <div>
    <c-button variant-color="blue" size="md" @click="togglePreview">{{
      this.isEditMode ? "Preview" : "Edit"
    }}</c-button>
    <keep-alive>
      <c-textarea v-if="isEditMode" v-model="input" ref="textarea" />
      <c-box v-else p="10px">
        <mark-down-viewer :rawtext="input" />
      </c-box>
    </keep-alive>
    <c-button variant-color="blue" size="md" @click="save">Save</c-button>
  </div>
</template>

<script>
import MarkDownViewer from "./MarkDownViewer.vue";
export default {
  components: { MarkDownViewer },
  props: ["text"],
  data: function () {
    return { input: this.text, isEditMode: true };
  },
  methods: {
    togglePreview() {
      this.isEditMode = !this.isEditMode;
    },
    save() {
      this.$emit("save", this.input);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>