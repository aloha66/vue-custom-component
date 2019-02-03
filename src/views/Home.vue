<template>
  <div class="home">
    <CheckboxGroup v-model="aa">
      <Checkbox label="aa">aa</Checkbox>
      <Checkbox label="ss">ss</Checkbox>
      <Checkbox label="dd">dd</Checkbox>
    </CheckboxGroup>
  </div>
</template>

<script>
import CheckboxGroup from "components/checkbox/checkbox-group";
import Checkbox from "components/checkbox/checkbox";
export default {
  components: { Checkbox, CheckboxGroup },
  name: "home",
  data() {
    return {
      aa: []
    };
  },
  mounted() {},
  computed: {}
};
</script>
