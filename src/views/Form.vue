<template>
  <div class="home">
    <i-form ref="form" :model="formValidate" :rules="ruleValidate">
      <i-form-item label="用户名" prop="name">
        <i-input v-model="formValidate.name"></i-input>
      </i-form-item>
      <i-form-item label="邮箱" prop="mail">
        <i-input v-model="formValidate.mail"></i-input>
      </i-form-item>
      <i-form-item label="选项" prop="right">
        <CheckboxGroup v-model="formValidate.right">
          <Checkbox label="test">aa</Checkbox>
          <Checkbox label="test2">ss</Checkbox>
          <Checkbox label="test3">dd</Checkbox>
        </CheckboxGroup>
      </i-form-item>
      <i-form-item label="单选" prop="single">
        <RadioGroup v-model="formValidate.single">
          <Radio label="demo">1</Radio>
          <Radio label="demo2">2</Radio>
          <Radio label="demo3">3</Radio>
        </RadioGroup>
      </i-form-item>
    </i-form>
    <button @click="handleSubmit">提交</button>
    <button @click="handleReset">重置</button>
  </div>
</template>

<script>
// import { mapState } from "vuex";
import iForm from "components/form/form";
import iFormItem from "components/form/form-item";
import iInput from "components/input/input";
import Checkbox from "components/checkbox/checkbox";
import CheckboxGroup from "components/checkbox/checkbox-group";
import Radio from "components/radio/radio";
import RadioGroup from "components/radio/radio-group";

export default {
  inject: ["app"],
  name: "home",
  components: {
    iForm,
    iFormItem,
    iInput,
    Checkbox,
    CheckboxGroup,
    Radio,
    RadioGroup
  },
  data() {
    return {
      formValidate: {
        name: "",
        mail: "lzcbruce@live.com",
        right: ["test2"],
        single: false
      },
      ruleValidate: {
        name: [{ required: true, message: "用户名不能为空", trigger: "blur" }],
        right: [
          {
            required: true,
            min: 1,
            type: "array",
            message: "Choose at least one hobby",
            trigger: "change"
          },
          {
            type: "array",
            max: 2,
            message: "Choose two hobbies at best",
            trigger: "change"
          }
        ],
        single: [
          {
            required: true,
            // type: "boolean",
            message: "必填",
            trigger: "change"
          }
        ],
        mail: [
          { required: true, message: "邮箱不能为空", trigger: "blur" },
          {
            type: "email",
            message: "邮箱根式不正确",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    handleSubmit() {
      // this.$refs.form.validate(valid => {
      //   if (valid) {
      //     window.alert("成功");
      //   } else {
      //     window.alert("失败");
      //   }
      // });

      const validate = this.$refs.form.validate();
      validate.then(valid => {
        if (valid) {
          window.alert("成功");
        } else {
          window.alert("失败");
        }
      });
    },
    handleReset() {
      this.$refs.form.resetFields();
    }
  },
  mounted() {},
  computed: {}
};
</script>
