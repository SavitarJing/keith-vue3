<template>
    <div class="card-form">
        <label for="title">标题：</label>
        <input type="text" v-model="cardForm.title" id="cardForm.title" name="cardForm.title" placeholder="请输入卡片标题">
        <label for="value">数值：</label>
        <input type="text" v-model="cardForm.value" id="cardForm.value" name="cardForm.value" placeholder="请输入卡片数值">
        <label for="desc">说明：</label>
        <input type="text" v-model="cardForm.desc" id="cardForm.desc" name="cardForm.desc" placeholder="请输入卡片说明">
        <a-button type="primary" @click="handleSubmit" size="small" style="margin-left: 10px;">新增</a-button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

// 表单：新增卡片
const cardForm = ref({
    title: '',
    value: '',
    desc: ''
})

const emit = defineEmits(['submit'])

const handleSubmit = () => {
    if (!cardForm.value.title.trim()) {
        console.log('请输入内容')
        return
    }
    emit('submit', {
        title: cardForm.value.title,
        value: cardForm.value.value,
        desc: cardForm.value.desc
    })

    clearCardForm()

}

const clearCardForm = () => {
    cardForm.value.title = ''
    cardForm.value.value = ''
    cardForm.value.desc = ''
}
</script>

<style lang="css" scoped></style>