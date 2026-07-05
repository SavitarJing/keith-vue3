<script></script>

<template>
    <div class="app-shell">
        <div class="sidebar">
            <span>侧边栏</span>
        </div>
        <div class="main">
            <div class="topbar">
                <span>顶部栏111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111</span>
            </div>
            <div class="content">
                <div class="page-header">
                    <div class="page-title">
                        <span>页面标题</span>
                    </div>
                    <div class="page-button">
                        <button>新建按钮</button>
                    </div>
                </div>
                <div class="stat-grid">
                    <div class="card"><span>card1</span></div>
                    <div class="card"><span>card2</span></div>
                    <div class="card"><span>card3</span></div>
                    <div class="card"><span>card4</span></div>
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
    flex-shrink: 0;
    /* 如果要出现滚动条,请设置 overflow-x: auto; */
    display: flex;
    align-items: center;

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

    .card {
        min-height: 120px;
        background: white;
        border-radius: 10px;
        /* 文字居中 */
        display: flex;
        align-items: center;
        justify-content: center;
        /* 阴影四参数：水平偏移 垂直偏移 模糊程度 阴影颜色 */
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
    margin-bottom: 20px;
}

.panel-grid {
    display: grid;
    /* 2:1面板 */
    grid-template-columns: 2fr 1fr;
    gap: 16px;
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