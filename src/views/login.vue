<template>
    <div class="form-wrap">
        <el-form ref="ruleFormRef" :model="ruleForm" status-icon :rules="rules" class="demo-ruleForm">
            <el-form-item label="账户" prop="name">
                <el-input placeholder="请输入账户名" v-model="ruleForm.name" type="text" autocomplete="off" />
            </el-form-item>
            <el-form-item label="密码" prop="password">
                <el-input placeholder="请输入密码" show-password  v-model="ruleForm.password" type="password" autocomplete="off" />
            </el-form-item>
            <div>
                <el-button type="primary" @click="submitForm(ruleFormRef)">登录</el-button>
                <el-button @click="resetForm(ruleFormRef)">重置</el-button>
            </div>
        </el-form>
    </div>
</template>
<script setup lang="ts">
import { useRouter } from "vue-router";
import { reactive, ref } from 'vue'
import type { FormInstance } from 'element-plus'

const ruleFormRef = ref<FormInstance>()

const validateInput = (rule: any, value: any, callback: any) => {
    if (value === '') {
        callback(new Error(''))
    } else {
        callback()
    }
}

const ruleForm = reactive({
    name: '',
    password: ''
})
const rules = reactive({
    name: [{ validator: validateInput, message: '账户名不能为空！', trigger: 'blur' }],
    password: [{ validator: validateInput, message: '密码不能为空！', trigger: 'blur' }],
})

let route = useRouter();
const submitForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    formEl.validate((valid) => {
        if (valid) {
            route.push('/');
        } else {
            console.log('error submit!')
            return false
        }
    })
}

const resetForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    formEl.resetFields()
}

</script>
<style lang="scss" scoped>
.form-wrap {
    width: 300px;
    margin: 20vh auto;
}
</style>
