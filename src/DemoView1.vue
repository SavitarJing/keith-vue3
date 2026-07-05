<script></script>

<template>
    <div class="app-shell">
        <div class="sidebar">
            <span>侧边栏</span>
        </div>
        <div class="main">
            <div class="topbar">
                <span>顶部栏</span>
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
    min-height: 100vh;
    display: flex;
}

.sidebar {
    width: 240px;
}

.main {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.topbar {
    height: 64px;
    flex-shrink: 0;
}

.content {
    padding: 24px;
    /* 高度占满main区域剩余空间 */
    flex: 1;
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
</style>