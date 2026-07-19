<template>
    <div class="card-form">
        <label for="title">标题：</label>
        <input type="text" v-model="childForm.value.title" placeholder="请输入卡片标题">
        <label for="value">数值：</label>
        <input type="text" v-model="childForm.value.value" placeholder="请输入卡片数值">
        <label for="desc">说明：</label>
        <input type="text" v-model="childForm.value.desc" placeholder="请输入卡片说明">
        <a-button type="primary" @click="handleSubmit" size="small" style="margin-left: 10px;">新增</a-button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
    modelValue: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['update:modelValue', 'submit'])


const childForm = ref({
    title: '',
    value: '',
    desc: ''
})

const handleSubmit = () => {
    if (!childForm.value.title.trim()) {
        console.log('请输入内容')
        return
    }
    emit('submit', {
        ...props.modelValue,
        title: childForm.value.title,
        value: childForm.value.value,
        desc: childForm.value.desc
    })

    clearCardForm()

}

// const handleTitleInput =(event)=> {
//     // 获取到当前输入的最新值
//     const newTitle = event.target.value

//     // 通知父组件，title发生变化
//     emit('update:modelValue', {
//         ...props.cardForm,
//         title: newTitle
//     })
// }
</script>

<style lang="css" scoped></style>