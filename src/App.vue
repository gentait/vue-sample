<template>
  <c-theme-provider>
    <c-reset />
    <Main />
  </c-theme-provider>
</template>

<script>
import Main from "./pages/Main.vue";

export default {
  name: "App",
  components: { Main },
};
</script>
