<template>
  <div class="home">
    <CheckboxGroup v-model="test">
      <Checkbox label="test">aa</Checkbox>
      <Checkbox label="test2">ss</Checkbox>
    </CheckboxGroup>
  </div>
</template>

<script>
import Checkbox from "components/checkbox/checkbox";
import CheckboxGroup from "components/checkbox/checkbox-group";
export default {
  components: { Checkbox, CheckboxGroup },
  name: "home",
  data() {
    return {
      test: ["test"]
    };
  },
  mounted() {},
  computed: {}
};
</script>
