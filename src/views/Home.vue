<template>
  <div class="home">
    <i-form ref="form" :model="formValidate" :rules="ruleValidate">
      <i-form-item label="用户名" prop="name">
        <i-input v-model="formValidate.name"></i-input>
      </i-form-item>
      <i-form-item label="邮箱" prop="mail">
        <i-input v-model="formValidate.mail"></i-input>
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

export default {
  inject: ["app"],
  name: "home",
  components: { iForm, iFormItem, iInput },
  data() {
    return {
      formValidate: { name: "", mail: "" },
      ruleValidate: {
        name: [{ required: true, message: "用户名不能为空", trigger: "blur" }],
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
