<template>
  <div>
    <el-button @click="userLogout">退出登录</el-button>
  </div>
</template>

<script setup lang="ts">
import { logout } from "@/net";
import router from "@/router";

function userLogout() {
  logout(() => router.push("/"));
}
</script>

<style></style>
