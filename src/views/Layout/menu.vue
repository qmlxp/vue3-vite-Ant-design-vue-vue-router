<template>
    <div class="menu-wrap">
        <el-radio-group v-model="isCollapse" style="margin-bottom: 20px">
            <el-radio-button :label="false">expand</el-radio-button>
            <el-radio-button :label="true">collapse</el-radio-button>
        </el-radio-group>
        <el-menu class="el-menu-vertical-demo" :collapse="isCollapse">
            <template v-for="item in titleOptions">
                <template v-if="item.children">
                    <el-sub-menu>
                        <template #title>
                            <el-icon>
                                <location />
                            </el-icon>
                            <span>{{ item.title }}</span>
                        </template>
                        <el-menu-item :class="{ 'issub-active': route.currentRoute.value.path === `/${opt.path}` }"
                            @click="handleRoute(opt)" v-for="opt in item.children">

                            {{ opt.title }}
                        </el-menu-item>
                    </el-sub-menu>
                </template>
                <!-- <template v-else>
                    <el-menu-item :class="{ 'is-active': isActive }" @click="handleRoute(item)">{{ item.title }}
                    </el-menu-item>
                </template> -->
            </template>
        </el-menu>
    </div>
</template>

<script lang="ts" setup>
import { computed, onMounted, ref } from 'vue'
import {
    Document,
    Menu as IconMenu,
    Location,
    Setting,
} from '@element-plus/icons-vue'
import { useRouter } from 'vue-router';

let titleOptions = ref([]);
let route = useRouter();
let isActive = computed(() => {
    return true

})

const isCollapse = ref(true)
function handleRoute(item) {
    if (route.currentRoute.value.path != `/${item.path}`) {
        route.push(item.path);
    }
}
onMounted(() => {
    titleOptions.value = route.options.routes;
})
</script>

<style lang="scss" scoped>
.el-menu-item:hover {
    background: rgb(212, 213, 208);
}


.menu-wrap {
    border-right: solid 1px var(--el-menu-border-color);
    height: 100%;

    .el-menu {
        border: none;
    }

    .el-menu-item {
        color: black;

        &.issub-active {
            background: rgb(128, 179, 182);
            color: rgb(69, 42, 160);
        }
    }
}
</style>
