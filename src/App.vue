<template>
  <Header />
  <div class="container text-center mx-auto">
    <router-view />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";

export default {
  components: {
    Header,
  },
};
</script>
