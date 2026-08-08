<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>少年同盟 - 校园友情物语</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <div id="game-container">
        <!-- 开始菜单 -->
        <div id="start-menu" class="menu-screen">
            <div class="menu-title">
                <h1>少年同盟</h1>
                <p class="subtitle">校园友情物语</p>
            </div>
            <div class="menu-buttons">
                <button id="btn-new-game" class="menu-btn">开始游戏</button>
                <button id="btn-load-game" class="menu-btn">继续游戏</button>
                <button id="btn-settings" class="menu-btn">游戏设置</button>
                <button id="btn-about" class="menu-btn">关于游戏</button>
            </div>
            <div class="menu-footer">
                <p>轻松沙雕 · 青春少年友情 · 无虐心悲剧</p>
            </div>
        </div>

        <!-- 设置界面 -->
        <div id="settings-screen" class="menu-screen hidden">
            <h2>游戏设置</h2>
            <div class="settings-panel">
                <div class="setting-item">
                    <label>文字速度</label>
                    <input type="range" id="text-speed" min="1" max="10" value="5">
                </div>
                <div class="setting-item">
                    <label>背景音乐音量</label>
                    <input type="range" id="bgm-volume" min="0" max="100" value="50">
                </div>
                <div class="setting-item">
                    <label>音效音量</label>
                    <input type="range" id="sfx-volume" min="0" max="100" value="70">
                </div>
                <div class="setting-item">
                    <label>自动保存</label>
                    <input type="checkbox" id="auto-save" checked>
                </div>
            </div>
            <button id="btn-settings-back" class="menu-btn">返回</button>
        </div>

        <!-- 关于界面 -->
        <div id="about-screen" class="menu-screen hidden">
            <h2>关于游戏</h2>
            <div class="about-content">
                <h3>少年同盟 - 校园友情物语</h3>
                <p>一款轻松沙雕的青春校园友情向游戏</p>
                <p>在校园中自由探索，与三位性格各异的少年建立深厚的友情羁绊。</p>
                <p>通过对话、送礼、小游戏提升好感度，解锁丰富的剧情和结局。</p>
                <br>
                <h4>操作说明：</h4>
                <p>WASD / 方向键 - 移动</p>
                <p>鼠标点击 - 移动到目标位置 / 交互</p>
                <p>空格键 / E键 - 与NPC/物品交互</p>
                <p>ESC键 - 打开菜单</p>
                <p>M键 - 打开地图</p>
                <p>I键 - 打开背包</p>
            </div>
            <button id="btn-about-back" class="menu-btn">返回</button>
        </div>

        <!-- 读档界面 -->
        <div id="load-screen" class="menu-screen hidden">
            <h2>读取存档</h2>
            <div id="save-slots" class="save-slots">
                <!-- 存档槽位动态生成 -->
            </div>
            <button id="btn-load-back" class="menu-btn">返回</button>
        </div>

        <!-- 游戏主画面 -->
        <div id="game-screen" class="hidden">
            <!-- 游戏画布 -->
            <canvas id="game-canvas" width="960" height="640"></canvas>
            
            <!-- 顶部状态栏 -->
            <div id="top-bar">
                <div class="status-item">
                    <span class="status-label">第</span>
                    <span id="day-display">1</span>
                    <span class="status-label">天</span>
                </div>
                <div class="status-item">
                    <span id="time-display">清晨</span>
                </div>
                <div class="status-item">
                    <span id="location-display">教室</span>
                </div>
                <button id="btn-menu" class="icon-btn">☰</button>
            </div>

            <!-- 底部好感度栏 -->
            <div id="affection-bar">
                <div class="affection-item" id="aff-tiam">
                    <span class="char-name">TIAM</span>
                    <div class="affection-bar-bg">
                        <div class="affection-bar-fill" style="width: 0%"></div>
                    </div>
                    <span class="affection-level">陌生</span>
                </div>
                <div class="affection-item" id="aff-zize">
                    <span class="char-name">紫啧</span>
                    <div class="affection-bar-bg">
                        <div class="affection-bar-fill" style="width: 0%"></div>
                    </div>
                    <span class="affection-level">陌生</span>
                </div>
                <div class="affection-item" id="aff-liudai">
                    <span class="char-name">硫代硫酸钠</span>
                    <div class="affection-bar-bg">
                        <div class="affection-bar-fill" style="width: 0%"></div>
                    </div>
                    <span class="affection-level">陌生</span>
                </div>
            </div>

            <!-- 对话框 -->
            <div id="dialogue-box" class="hidden">
                <div id="dialogue-speaker"></div>
                <div id="dialogue-text"></div>
                <div id="dialogue-continue">▼ 点击继续</div>
            </div>

            <!-- 选项框 -->
            <div id="choice-box" class="hidden">
                <div id="choice-list"></div>
            </div>

            <!-- 交互提示 -->
            <div id="interact-hint" class="hidden">
                <span>按 [空格] 交互</span>
            </div>

            <!-- 物品获得提示 -->
            <div id="item-popup" class="hidden">
                <div class="item-popup-content">
                    <span id="item-popup-icon">📦</span>
                    <span id="item-popup-text">获得物品</span>
                </div>
            </div>
        </div>

        <!-- 游戏内菜单 -->
        <div id="game-menu" class="menu-screen hidden">
            <h2>游戏菜单</h2>
            <div class="menu-buttons">
                <button id="btn-resume" class="menu-btn">继续游戏</button>
                <button id="btn-save" class="menu-btn">保存游戏</button>
                <button id="btn-load" class="menu-btn">读取存档</button>
                <button id="btn-inventory" class="menu-btn">背包</button>
                <button id="btn-map" class="menu-btn">地图</button>
                <button id="btn-gallery" class="menu-btn">CG图鉴</button>
                <button id="btn-game-settings" class="menu-btn">设置</button>
                <button id="btn-quit" class="menu-btn">返回标题</button>
            </div>
        </div>

        <!-- 背包界面 -->
        <div id="inventory-screen" class="menu-screen hidden">
            <h2>背包</h2>
            <div id="inventory-grid" class="inventory-grid">
                <!-- 物品格子动态生成 -->
            </div>
            <div id="item-detail" class="item-detail">
                <p>选择物品查看详情</p>
            </div>
            <button id="btn-inventory-back" class="menu-btn">返回</button>
        </div>

        <!-- 地图界面 -->
        <div id="map-screen" class="menu-screen hidden">
            <h2>校园地图</h2>
            <div id="world-map" class="world-map">
                <!-- 地图点动态生成 -->
            </div>
            <button id="btn-map-back" class="menu-btn">返回</button>
        </div>

        <!-- CG图鉴 -->
        <div id="gallery-screen" class="menu-screen hidden">
            <h2>CG图鉴</h2>
            <div id="gallery-grid" class="gallery-grid">
                <!-- CG格子动态生成 -->
            </div>
            <button id="btn-gallery-back" class="menu-btn">返回</button>
        </div>

        <!-- 小游戏界面 -->
        <div id="minigame-screen" class="hidden">
            <div id="minigame-container">
                <!-- 小游戏内容动态生成 -->
            </div>
        </div>

        <!-- 结局画面 -->
        <div id="ending-screen" class="menu-screen hidden">
            <div id="ending-content">
                <h2 id="ending-title"></h2>
                <p id="ending-text"></p>
            </div>
            <button id="btn-ending-continue" class="menu-btn">继续</button>
        </div>
    </div>

    <!-- 游戏脚本 -->
    <script src="js/config.js"></script>
    <script src="js/data.js"></script>
    <script src="js/save.js"></script>
    <script src="js/time.js"></script>
    <script src="js/player.js"></script>
    <script src="js/npc.js"></script>
    <script src="js/map.js"></script>
    <script src="js/dialogue.js"></script>
    <script src="js/affection.js"></script>
    <script src="js/minigames.js"></script>
    <script src="js/events.js"></script>
    <script src="js/ui.js"></script>
    <script src="js/game.js"></script>
    <script src="js/main.js"></script>
</body>
</html>
