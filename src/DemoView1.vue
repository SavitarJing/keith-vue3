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
    display: flex;
    gap: 16px;

    .card {
        width: 100px;
        height: 40px;
        background-color: white;
        border-radius: 10px;
        /* 文字居中 */
        display: flex;
        align-items: center;
        justify-content: center;
    }
    margin-bottom: 20px;
}

.panel-grid {
    display: flex;
    
    .data-area {
        width: 66.667%;
    }
}
</style>