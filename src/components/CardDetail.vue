<script setup>
const props = defineProps({
    card: {
        type: Object,
        default: null
    }
})
</script>

<template>
    <div class="card-detail">
        <div v-if="!card">
            请选择一张统计卡片查看详情
        </div>
        <div v-else>
            <div>当前查看：{{ card.title }}</div>
            <div>数值：{{ card.value }}</div>
            <div>说明：{{ card.desc }}</div>
        </div>
    </div>
</template>

<style lang="css" scoped>
    .card-detail {
        padding: 20px;
        min-height: 100px;
        background-color: white;
        border-radius: 10px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
</style>