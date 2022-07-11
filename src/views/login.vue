<template>
    <button @click="showConfirm">登录</button>
</template>
<script setup lang="ts">
import { useRoute, useRouter } from "vue-router";
let route = useRouter();

const showConfirm = () => {
    alert('我要登陆了');
    setTimeout(() => {
        route.push('/');
    }, 1000)
};
</script>
