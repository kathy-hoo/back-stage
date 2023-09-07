<!--快速生成模版 -->
<template>
  <div class="login-box">
    <el-form
      ref="ruleFormRef"
      :model="ruleForm"
      status-icon
      :rules="rules"
      label-width="120px"
      class="demo-ruleForm"
    >
      <h3 class="title">登 录</h3>
      <el-form-item label="username" prop="username">
        <el-input v-model="ruleForm.username" autocomplete="off" />
      </el-form-item>
      <el-form-item label="password" prop="password">
        <el-input
          v-model="ruleForm.password"
          type="password"
          autocomplete="off"
        />
      </el-form-item>
      <el-form-item>
        <el-button
          class="btn"
          style="background-color: rgb(4, 161, 145); border: none"
          type="primary"
          @click="submitForm(ruleFormRef)"
          >Submit</el-button
        >
        <el-button class="btn" @click="resetForm(ruleFormRef)">Reset</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, toRefs, ref } from "vue";
import { loginData } from "../type/login";
import { login } from "../request/api";
import { useRouter } from "vue-router";
import type { FormInstance } from "element-plus";

export default defineComponent({
  setup() {
    const data = reactive(new loginData());
    const rules = {
      username: [
        {
          required: true,
          message: "请输入账户名",
          trigger: "blur",
        },
        {
          min: 3,
          max: 10,
          message: "长度为3-10位",
          trigger: "blur",
        },
      ],
      password: [
        {
          required: true,
          message: "请输入密码",
          trigger: "blur",
        },
        {
          min: 3,
          max: 10,
          message: "长度为3-10位",
          trigger: "blur",
        },
      ],
    };
    const router = useRouter(); //相当于vue2的$router
    const ruleFormRef = ref<FormInstance>();
    const submitForm = (formEl: FormInstance | undefined) => {
      if (!formEl) return;
      formEl.validate((valid) => {
        if (valid) {
          login(data.ruleForm).then((res) => {
            // 请求成功，保存token
            localStorage.setItem("token", res.data.token);
            // 跳转页面
            router.push("/");
          });
        } else {
          console.log("error submit!");
          return false;
        }
      });
    };
    const resetForm = (formEl: FormInstance | undefined) => {
      if (!formEl) return;
      formEl.resetFields();
    };
    return {
      ...toRefs(data),
      rules,
      ruleFormRef,
      submitForm,
      resetForm,
    };
  },
});
</script>
<style lang="scss" scoped>
.login-box {
  background-color: rgb(4, 161, 145);
  width: 100%;
  height: 100%;
}
.demo-ruleForm {
  position: absolute;
  top: 30%;
  left: 65%;
  padding: 50px;
  border-radius: 10px;
  background: #fff;
}
.btn {
  width: 46%;
}
.title {
  margin-bottom: 20px;
  text-align: center;
}
</style>
