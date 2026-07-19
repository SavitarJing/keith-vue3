<script setup>

/** 父子组件通信
 * 
 * props：子组件声明“我准备接收父组件给我的哪些数据”
   emit：子组件声明“我准备向父组件发送哪些事件”
 */

// 子组件接收父组件传递过来的数据
const props = defineProps({
    card: {
        type: Object,
        required: true
    },
    isActive: {
        type: Boolean,
        default: false
    }
})


// 父组件接收子组件通知的事件
const emit = defineEmits(['select', 'delete'])
</script>

<template>
    <!-- @click="emit('select', card.id)：我被点击了，告诉父组件：select 事件发生了，并把我的 id 带上去 -->
    <div class="card" @click="emit('select', card.id)" :class="{ cardActive: isActive }">
        <span>{{ card.title }}</span>
        <span>{{ card.value }}</span>
        <span>{{ card.desc }}</span>
        <button @click.stop="emit('delete', card.id)">删除</button>
    </div>
</template>

<style scoped>
.card {
    min-height: 120px;
    background: white;
    border-radius: 10px;
    /* 文字居中 */
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: center;
    justify-content: center;
    /* 阴影四参数：水平偏移 垂直偏移 模糊程度 阴影颜色 */
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);

    cursor: pointer;
    /* 定义悬浮动画 / 状态变化时的过渡规则 */
    /* 浏览器会在 0.2 秒内，从开始状态逐渐变为结束状态。 */
    transition:
        transform 0.2s ease,
        box-shadow 0.2s ease;
    /* 控制过渡动画从开始到结束需要花费的时间 */
    /* transition-duration: 1s; */
}

/* 给当前选中的卡片增加边框颜色 */
.card.cardActive {
    border: 2px solid #1677ff;
}

/* 悬浮动画 */
.card:hover {
    /* Y 表示垂直方向,负数向上移动 */
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
}

/* 点击反馈 */
.card:active {
    transform: translateY(-1px) scale(0.99);
}
</style>