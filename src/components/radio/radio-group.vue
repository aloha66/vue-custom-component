<template>
  <div><slot></slot></div>
</template>
<script>
import { findComponentsDownward } from "utils/assist";
import Emitter from "mixins/emitter";
export default {
  name: "iRadioGroup",
  mixins: [Emitter],
  props: {
    value: {
      type: [String, Number, Boolean]
    }
  },
  data() {
    return {
      currentValue: this.value,
      childrens: []
    };
  },
  methods: {
    updateModel(update) {
      this.childrens = findComponentsDownward(this, "iRadio");
      if (this.childrens) {
        const { value } = this;
        this.childrens.forEach(child => {
          child.model = value;
          if (update) {
            child.currentValue = value;
            child.group = true;
          }
        });
      }
    },
    change(data) {
      this.currentValue = data;
      this.$emit("input", data);
      this.$emit("on-change", data);
      this.dispatch("iFormItem", "on-form-change", data);
    }
  },
  mounted() {
    this.updateModel(true);
  },
  watch: {
    value() {
      this.updateModel(true);
    }
  }
};
</script>
