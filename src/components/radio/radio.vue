<template>
  <label>
    <span>
      <input
        v-if="group"
        @change="change"
        v-model="model"
        :value="label"
        :disabled="disabled"
        type="radio"
      />
      <input
        v-else
        :checked="currentValue"
        @change="change"
        type="radio"
        :disabled="disabled"
      />
    </span>
    <slot></slot>
  </label>
</template>
<script>
import Emitter from "mixins/emitter";
import { findComponentUpward } from "utils/assist";
export default {
  name: "iRadio",
  mixins: [Emitter],
  mounted() {
    this.parent = findComponentUpward(this, "iRadioGroup");
    if (this.parent) {
      this.group = true;
    }
    if (this.group) {
      this.parent.updateModel(true);
    } else {
      this.updateModel();
    }
  },
  data() {
    return {
      currentValue: this.value,
      model: this.value,
      group: false,
      parent: null
    };
  },
  methods: {
    change(event) {
      if (this.disabled) return false;
      const checked = event.target.checked;
      this.currentValue = checked;
      const value = checked ? this.trueValue : this.falseValue;
      this.$emit("input", value);
      if (this.group) {
        this.parent.change(this.model);
      } else {
        this.$emit("on-change", value);
        this.dispatch("iFormItem", "on-form-change", value);
      }
    },
    updateModel() {
      this.currentValue = this.value === this.trueValue;
    }
  },
  watch: {
    value(val) {
      if (val === this.trueValue || val === this.falseValue) {
        this.updateModel();
      } else {
        throw "Value should be trueValue or falseValue";
      }
    }
  },
  props: {
    label: {
      type: [String, Number, Boolean]
    },
    value: {
      type: [String, Number, Boolean],
      default: false
    },
    trueValue: {
      type: [String, Number, Boolean],
      default: true
    },
    falseValue: {
      type: [String, Number, Boolean],
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  }
};
</script>
