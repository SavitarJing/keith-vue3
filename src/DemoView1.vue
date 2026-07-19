<script setup>
import { computed, ref } from 'vue';
import StatCard from './components/StatCard.vue';

// 定义是否展开侧边栏状态，初始为展开true
const isExpand = ref(true)

// 定义按钮点击事件，切换侧边栏状态
const changeSidebarStatus = () => {
    isExpand.value = !isExpand.value
}

// 定义卡片内容
const statCards = ref(
    [
        {
            id: 1,
            title: '今日订单',
            value: '128',
            desc: '较昨日 +12%'
        },
        {
            id: 2,
            title: '今日退款',
            value: '11',
            desc: '较昨日 -20%'
        },
        {
            id: 3,
            title: '今日销售额',
            value: '10000',
            desc: '较昨日 +35%'
        },
        {
            id: 4,
            title: '今日成本',
            value: '3000',
            desc: '较昨日 持平'
        },

    ]
)

// 记录当前选择的卡片id
const selectedCardId = ref(null)

// 处理卡片被选中事件
const handleCardSelected = (id) => {
    // 获取到当前选中card的id
    selectedCardId.value = id
    console.log('当前选中的卡片是', selectedCardId.value)
}

// 利用find函数，根据卡片id反查整个卡片对象
const selectedCard = computed(
    () => {
        return statCards.value.find(card => card.id === selectedCardId.value)
    }
)

// 根据输入关键词展示匹配的卡片
const keyword = ref('')

// 保存符合条件的card
const filterCards = computed(() => {
    // 使用filter函数过滤出匹配的数据
    return statCards.value.filter(
        card => {
            // 字符串函数，用于查询某个字符串中是否包含指定字符串
            return card.title.includes(keyword.value)
        }
    )
})

// 表单：新增卡片
const cardForm = ref({
    id: '',
    title: '',
    value: '',
    desc: ''
})

const addNewCard = () => {
    if (!cardForm.value.title.trim()) {
        console.log('请输入内容')
        return
    }
    // 新增卡片内容到数组中
    statCards.value.push(
        {
            id: Date.now(),
            title: cardForm.value.title,
            value: cardForm.value.value,
            desc: cardForm.value.desc
        }
    )
    // 清空表单
    clearForm()
}

// 清空表单方法
const clearForm = () => {
    cardForm.value.title = ''
    cardForm.value.value = ''
    cardForm.value.desc = ''
}

// 根据id删除卡片
const deleteCard = (id) => {
    if (selectedCardId.value === id) {
        selectedCardId.value = null
    }
    // filter会返回一个新数组，而不是在原数组上更改，因此需要重新赋值
    statCards.value = statCards.value.filter(card => {
        return card.id !== id
    })
}

</script>

<template>
    <div class="app-shell">
        <div class="sidebar" :class="{ shrink: !isExpand }">
            <span>侧边栏</span>
            <div>option112121212</div>
            <div>option2</div>
        </div>
        <div class="main">
            <div class="topbar">
                <span>顶部栏</span>
                <a-button type="primary" @click="changeSidebarStatus">{{ isExpand ? '收起侧边栏' : '展开侧边栏' }}</a-button>
            </div>
            <div class="content">
                <div class="page-header">
                    <div class="page-title">
                        <span style="margin-right: 10px;">页面标题</span>
                        <input type="text" v-model="keyword" placeholder="请输入筛选关键字">
                        <div class="card-form" style="margin-top: 20px;">
                            <div class="card-form">
                                <label for="title">标题：</label>
                                <input type="text" v-model="cardForm.title" id="cardForm.title" name="cardForm.title"
                                    placeholder="请输入卡片标题">
                                <label for="value">数值：</label>
                                <input type="text" v-model="cardForm.value" id="cardForm.value" name="cardForm.value"
                                    placeholder="请输入卡片数值">
                                <label for="desc">说明：</label>
                                <input type="text" v-model="cardForm.desc" id="cardForm.desc" name="cardForm.desc"
                                    placeholder="请输入卡片说明">
                                <a-button type="primary" @click="addNewCard" size="small"
                                    style="margin-left: 10px;">新增</a-button>
                            </div>
                        </div>
                    </div>
                    <div class="page-button">
                        <button>新建按钮</button>
                    </div>
                </div>
                <div class="stat-grid" v-if="filterCards.length > 0">
                    <stat-card v-for="card in filterCards" :key="card.id" :card="card"
                        :is-active="selectedCardId === card.id" @select="handleCardSelected"
                        @delete="deleteCard"></stat-card>
                </div>
                <div v-else>
                    暂无匹配数据
                </div>
                <div class="card-detail">
                    <div v-if="!selectedCard">
                        请选择一张统计卡片查看详情
                    </div>
                    <div v-else>
                        <div>当前查看：{{ selectedCard.title }}</div>
                        <div>数值：{{ selectedCard.value }}</div>
                        <div>说明：{{ selectedCard.desc }}</div>
                    </div>
                </div>
                <div class="panel-grid">
                    <div class="data-area">数据区域</div>
                    <div class="dynamic-area">动态区域</div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="css" scoped>
.app-shell {
    height: 100vh;
    display: flex;
    /* 防止子元素撑出页面，确保只有内容区滚动 */
    overflow: hidden;
}

.sidebar {
    width: 240px;
    /* 不参与压缩 */
    flex-shrink: 0;
    padding: 20px;
    transition: width 0.3s ease;
}

/* 根据状态变化动态显示地样式 */
.sidebar.shrink {
    width: 64px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

.main {
    flex: 1;
    display: flex;
    flex-direction: column;
    /* 防止表格、长文本等把主区域横向撑开 */
    min-width: 0;
}

.topbar {
    height: 64px;
    padding: 0 24px;
    flex-shrink: 0;
    /* 如果要出现滚动条,请设置 overflow-x: auto; */
    display: flex;
    align-items: center;
    justify-content: space-between;

    span {
        min-width: 0;
        /* 隐藏超出部分内容 */
        overflow: hidden;
        /* 不换行 */
        white-space: nowrap;
        /* 用省略号表示超出部分内容 */
        text-overflow: ellipsis;
    }
}

.content {
    padding: 24px;
    /* 高度占满main区域剩余空间 */
    flex: 1;
    /* min-height: 0; */
    overflow: auto;
}

.page-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}

.stat-grid {
    /* 网格布局，等宽排列四个卡片 */
    display: grid;
    /* 1fr表示一份剩余空间，所以四个就是四个等宽列 */
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;

    margin-bottom: 20px;
}

.panel-grid {
    display: grid;
    /* 2:1面板 */
    grid-template-columns: 2fr 1fr;
    gap: 16px;
    margin-top: 20px;
}

.data-area,
.dynamic-area {
    min-height: 280px;
    padding: 20px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* 响应式布局 */
/* 当浏览器视口宽度不超过 1200px 时，使用里面的新规则。 */
@media (max-width: 1200px) {
    .stat-grid {
        grid-template-columns: 1fr 1fr;
    }

    .panel-grid {
        grid-template-columns: 1fr;
    }
}

@media (max-width: 768px) {
    .sidebar {
        display: none;
    }

    .stat-grid {
        grid-template-columns: 1fr;
    }

    .page-header {
        flex-direction: column;
        align-items: flex-start;
        gap: 12px;
    }
}
</style>