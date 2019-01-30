<template>
  <div id="app"><router-view /></div>
</template>
<script>
export default {
  provide() {
    return {
      app: this
    };
  },
  data() {
    return {};
  },
  methods: {},
  computed: {}
};
</script>

<style lang="scss"></style>
