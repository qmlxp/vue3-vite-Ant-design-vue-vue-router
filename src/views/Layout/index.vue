<template>
    <div class="wrap">
        <div class="title">
            <el-button type="danger" text @click="loginOut">退出</el-button>
            <menu-part></menu-part>
        </div>
        <div class="content">
            <div class="contain">
                <router-view></router-view>
            </div>
            <div class="footer">
                底部@copy alaner出品
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
import { reactive, ref } from "@vue/reactivity";
import { computed, onMounted } from "@vue/runtime-core";
import { useRoute, useRouter } from "vue-router";
import menuPart from './menu.vue'
import { ElMessage, ElMessageBox } from 'element-plus'

let route = useRouter();
function loginOut() {
    ElMessageBox.confirm(
        '是否要退出该系统?',
        '二次确认',
        {
            confirmButtonText: '确认',
            cancelButtonText: '取消',
            type: 'warning',
            center: true,
        }
    )
        .then(() => {
            route.push('/login');
        })
        .catch(() => {
            ElMessage({
                type: 'info',
                message: '取消退出',
            })
        })
}
</script>
<style lang="scss" scoped>
.wrap {
    display: flex;
    flex-direction: flex;
    height: 100vh;
}

.title {
    // width: 200px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    cursor: pointer;
}

.content {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.contain {
    flex: 1;
    position: relative;
}


.footer {
    line-height: 3vh;
    background: rgb(201, 192, 192);
    width: 100%;
}
</style>