<template>
    <div class="card-form">
        <label for="title">标题：</label>
        <input type="text" v-bind:value="props.modelValue.title" @input="handleInput('title', $event)" placeholder="请输入卡片标题">
        <label for="value">数值：</label>
        <input type="text" v-bind:value="props.modelValue.value" @input="handleInput('value', $event)" placeholder="请输入卡片数值">
        <label for="desc">说明：</label>
        <input type="text" v-bind:value="props.modelValue.desc" @input="handleInput('desc', $event)" placeholder="请输入卡片说明">
        <a-button type="primary" @click="handleSubmit" size="small" style="margin-left: 10px;">{{ isEdit ? '保存修改' : '新增' }}</a-button>
        <a-button type="primary" @click="handleReset" size="small" style="margin-left: 10px;">清空</a-button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    modelValue: {
        type: Object,
        required: true
    },
    isEdit: {
        type: Boolean,
        default: false
    }
})

const emit = defineEmits(['update:modelValue', 'submit', 'reset'])


const handleSubmit = () => {
    emit('submit')
}

const handleReset = () => {
    emit('reset')
}

const handleInput =(field, event)=> {
    // 获取到当前输入的最新值
    const newFieldValue = event.target.value

    // 通知父组件，title发生变化
    emit('update:modelValue', {
        ...props.modelValue,
        [field]: newFieldValue
    })
}
</script>

<style lang="css" scoped></style>