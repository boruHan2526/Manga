<template>
  <div style="text-align: center; margin: 0 20px">
    <div style="margin-top: 150px">
      <div
        style="
          font-size: 25px;
          font-weight: bold;
          color: white;
          text-shadow: 0 2px 5px rgba(0, 0, 0, 0.6);
          font-family: STSong;
        "
      >
        登录
      </div>
      <div
        style="
          font-size: 14px;
          color: white;
          text-shadow: 0 2px 5px rgba(0, 0, 0, 0.6);
        "
      >
        在进入系统之前，请先输入用户名和密码进行登录
      </div>
    </div>
    <div style="margin-top: 50px">
      <el-form :model="form" :rules="rule" ref="formRef">
        <el-form-item>
          <el-input
            v-model="form.username"
            maxlength="10"
            type="text"
            placeholder="用户名/邮箱"
          >
            <template #prefix>
              <el-icon><User /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-form-item>
          <el-input
            v-model="form.password"
            type="password"
            maxlength="20"
            placeholder="密码"
          >
            <template #prefix>
              <el-icon><Lock /></el-icon>
            </template>
          </el-input>
        </el-form-item>
        <el-row>
          <el-col :span="12" style="text-align: left">
            <el-form-item>
              <el-checkbox
                v-model="form.remember"
                label="Remember Me"
                style="color: white; text-shadow: 0 2px 5px rgba(0, 0, 0, 0.6)"
              />
            </el-form-item>
          </el-col>
          <el-col :span="12" style="text-align: right">
            <el-link
              style="
                color: white;
                text-shadow: 0 2px 5px rgba(0, 0, 0, 0.6);
                font-weight: bold;
              "
              >忘记密码？</el-link
            >
          </el-col>
        </el-row>
      </el-form>
    </div>
    <div style="margin-top: 40px">
      <el-button @click="userLogin" style="width: 250px" type="success" plain
        >立即登录</el-button
      >
    </div>
    <el-divider>
      <span style="font-size: 13px; color: grey">没有账号</span>
    </el-divider>
    <div>
      <el-button style="width: 250px" type="warning" plain>
        立即注册
      </el-button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue";
import { User, Lock } from "@element-plus/icons-vue";
import { login } from "@/net/index";
import router from "@/router";

const form = reactive({
  username: "",
  password: "",
  remember: false,
});

const rule = {
  username: [{ required: true, message: "请输入用户名" }],
  password: [{ required: true, message: "请输入密码" }],
};

const formRef = ref();

function userLogin() {
  formRef.value.validate((valid) => {
    if (valid) {
      login(form.username, form.password, form.remember, () =>
        router.push("/index")
      );
    }
  });
}
</script>

<style></style>
