<template>
  <div class="home">
    <i-display :code="code"></i-display>
    <button @click="click">按钮</button>
    <button @click="handleOpen2">打开提示 2</button>
  </div>
</template>

<script>
import iDisplay from "components/display/display";
import defaultCode from "./default-code.js";
export default {
  components: { iDisplay },
  name: "home",
  data() {
    return {
      code: defaultCode
    };
  },
  mounted() {},
  methods: {
    click() {
      this.$Alert.info({
        content: "我是提示信息 1"
      });
    },
    handleOpen2() {
      this.$Alert.info({
        content: "我是提示信息 2",
        duration: 3
      });
    }
  },
  computed: {}
};
</script>
