# benny
 時空膠囊與未來信件產生器
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chronos 時空膠囊與未來信件產生器</title>
    <!-- 引入 Tailwind CSS -->
    <script src="https://jsdelivr.net"></script>
    <!-- 引入 Animate.css 動畫庫 -->
    <link rel="stylesheet" href="https://cloudflare.com"/>
    <!-- 引入 FontAwesome 圖標 -->
    <link rel="stylesheet" href="https://cloudflare.com">
    <!-- 引入 彩帶特效庫 -->
    <script src="https://jsdelivr.net"></script>
    <style>
        .gradient-bg {
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 50%, #311042 100%);
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
    </style>
</head>
<body class="gradient-bg min-h-screen text-slate-100 font-sans antialiased pb-12">

    <!-- 隱藏的音頻元素 (使用免版權合法音訊串流) -->
    <audio id="bg-music" loop src="https://mixkit.co"></audio>

    <!-- 導覽列 -->
    <nav class="max-w-6xl mx-auto px-4 py-6 flex justify-between items-center border-b border-slate-800 mb-8">
        <div class="flex items-center gap-3">
            <div class="bg-indigo-600 p-2.5 rounded-xl shadow-lg shadow-indigo-500/30">
                <i class="fa-solid fa-hourglass-half text-xl text-white"></i>
            </div>
            <span class="text-xl font-bold bg-gradient-to-r from-indigo-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">Chronos 時空膠囊</span>
        </div>
        <div class="flex items-center gap-3">
            <!-- 沉浸式音樂按鈕 -->
            <button onclick="toggleMusic()" id="music-btn" class="text-xs bg-slate-900 border border-slate-800 px-3 py-1.5 rounded-full hover:bg-slate-800 transition-colors flex items-center gap-1.5 cursor-pointer">
                <i class="fa-solid fa-music text-slate-400"></i> <span>播放寫信 BGM</span>
            </button>
            <div class="text-xs text-slate-400 bg-slate-900/80 px-3 py-1.5 rounded-full border border-slate-800 hidden sm:block">
                <i class="fa-solid fa-circle text-emerald-400 mr-1.5 animate-pulse"></i> 本機加密儲存中
            </div>
        </div>
    </nav>

    <!-- 主要內容區 -->
    <main class="max-w-6xl mx-auto px-4 grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        <!-- 左側：撰寫膠囊 -->
        <section class="lg:col-span-5 glass-card p-6 rounded-2xl shadow-xl flex flex-col gap-5">
            <div class="border-b border-slate-800 pb-3">
                <h2 class="text-lg font-semibold text-indigo-300 flex items-center gap-2">
                    <i class="fa-solid fa-pen-fancy"></i> 撰寫一封未來信件
                </h2>
                <p class="text-xs text-slate-400 mt-1">寫下此時的心情，寄給未來的自己或重要的人。</p>
            </div>

            <!-- 表單欄位 -->
            <div class="flex flex-col gap-1.5">
                <label class="text-xs font-medium text-slate-400">寄件人 / 暱稱</label>
                <input type="text" id="sender" placeholder="例如：二十歲的自己" class="w-full bg-slate-950/50 border border-slate-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500 transition-colors">
            </div>

            <div class="flex flex-col gap-1.5">
                <label class="text-xs font-medium text-slate-400">此時此刻的心情氛圍</label>
                <div class="grid grid-cols-5 gap-2" id="mood-selector">
                    <button onclick="selectMood('🚀', 'indigo')" class="mood-btn p-2.5 rounded-xl bg-slate-950/40 border border-slate-800 text-xl hover:scale-105 transition-all text-center">🚀</button>
                    <button onclick="selectMood('☕', 'amber')" class="mood-btn p-2.5 rounded-xl bg-slate-950/40 border border-slate-800 text-xl hover:scale-105 transition-all text-center">☕</button>
                    <button onclick="selectMood('🌱', 'emerald')" class="mood-btn p-2.5 rounded-xl bg-slate-950/40 border border-slate-800 text-xl hover:scale-105 transition-all text-center">🌱</button>
                    <button onclick="selectMood('🌧️', 'blue')" class="mood-btn p-2.5 rounded-xl bg-slate-950/40 border border-slate-800 text-xl hover:scale-105 transition-all text-center">🌧️</button>
                    <button onclick="selectMood('❤️', 'pink')" class="mood-btn p-2.5 rounded-xl bg-slate-950/40 border border-slate-800 text-xl hover:scale-105 transition-all text-center">❤️</button>
                </div>
            </div>

            <div class="flex flex-col gap-1.5">
                <label class="text-xs font-medium text-slate-400">信件內容</label>
                <textarea id="content" rows="5" placeholder="寫點什麼吧... 你現在在煩惱什麼？你希望未來的你達成了什麼目標？" class="w-full bg-slate-950/50 border border-slate-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500 transition-colors resize-none"></textarea>
            </div>

            <div class="flex flex-col gap-1.5">
                <label class="text-xs font-medium text-slate-400">設定開啟時間</label>
                <!-- 快捷鍵 -->
                <div class="grid grid-cols-3 gap-2 mb-2">
                    <button onclick="setTimeShortcut(1)" class="text-[11px] py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 transition-colors cursor-pointer">1 分鐘後 (測試)</button>
                    <button onclick="setTimeShortcut(1440)" class="text-[11px] py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 transition-colors cursor-pointer">1 天後</button>
                    <button onclick="setTimeShortcut(525600)" class="text-[11px] py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 transition-colors cursor-pointer">1 年後</button>
                </div>
                <input type="datetime-local" id="unlock-time" class="w-full bg-slate-950/50 border border-slate-800 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-indigo-500 transition-colors text-slate-300">
            </div>

            <button onclick="sealCapsule()" class="w-full mt-2 bg-gradient-to-r from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white font-medium py-3 rounded-xl shadow-lg shadow-indigo-500/20 active:scale-[0.98] transition-all flex items-center justify-center gap-2 cursor-pointer">
                <i class="fa-solid fa-box-archive"></i> 注入能量，封存時空膠囊
            </button>
        </section>

        <!-- 右側：時光庫清單 -->
        <section class="lg:col-span-7 flex flex-col gap-4">
            <div class="glass-card p-4 rounded-xl flex justify-between items-center">
                <h2 class="text-md font-semibold text-purple-300 flex items-center gap-2">
                    <i class="fa-solid fa-vault"></i> 我的時光地下室
                </h2>
                <div class="flex items-center gap-2">
                    <!-- 匯出匯入按鈕 -->
                    <button onclick="exportCapsules()" class="text-[11px] bg-slate-800 hover:bg-slate-700 px-2 py-1 rounded border border-slate-700 cursor-pointer" title="匯出備份檔案"><i class="fa-solid fa-download"></i> 匯出</button>
                    <button onclick="document.getElementById('import-file').click()" class="text-[11px] bg-slate-800 hover:bg-slate-700 px-2 py-1 rounded border border-slate-700 cursor-pointer" title="從檔案還原膠囊"><i class="fa-solid fa-upload"></i> 匯入</button>
                    <input type="file" id="import-file" class="hidden" accept=".json" onchange="importCapsules(this)">
                    <span id="capsule-count" class="text-xs bg-purple-950 text-purple-300 border border-purple-800 px-2.5 py-0.5 rounded-full">0 個膠囊</span>
                </div>
            </div>

            <!-- 膠囊清單容器 -->
            <div id="capsules-container" class="flex flex-col gap-4 overflow-y-auto max-h-[600px] pr-1">
                <!-- 動態注入內容 -->
            </div>
        </section>
    </main>

    <!-- 信件閱讀彈窗 (Modal) -->
    <div id="read-modal" class="fixed inset-0 bg-black/80 backdrop-blur-md flex items-center justify-center p-4 hidden z-50">
        <div class="glass-card w-full max-w-xl rounded-2xl border border-amber-500/30 overflow-hidden animate__animated animate__zoomIn">
            <div class="bg-gradient-to-r from-amber-950/40 to-purple-950/40 p-4 border-b border-slate-800 flex justify-between items-center">
                <span class="text-amber-400 font-bold text-sm"><i class="fa-solid fa-envelope-open-text mr-1.5"></i> 成功解鎖時空密信</span>
                <button onclick="closeModal()" class="text-slate-400 hover:text-white cursor-pointer"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div class="p-6 bg-slate-900/60 flex flex-col gap-4">
                <div class="flex justify-between items-center text-xs text-slate-400">
                    <span>來自：<strong id="modal-sender" class="text-slate-200"></strong></span>
                    <span>封存於：<span id="modal-created"></span></span>
                </div>
                <div class="bg-amber-50/5 text-slate-200 p-5 rounded-xl border border-amber-500/10 min-h-[150px] whitespace-pre-wrap text-sm leading-relaxed tracking-wide shadow-inner" id="modal-content"></div>
                <div class="flex justify-between items-center mt-2">
                    <span id="modal-mood" class="text-sm bg-slate-800 px-3 py-1.5 rounded-xl text-slate-300"></span>
                    <button onclick="closeModal()" class="bg-slate-800 hover:bg-slate-700 px-5 py-2 text-xs rounded-xl font-medium transition-colors cursor-pointer">關閉並妥善收藏</button>
                </div>
            </div>
        </div>
    </div>

    <!-- 提示框元件 (Toast) -->
    <div id="toast" class="fixed bottom-6 left-1/2 transform -translate-x-1/2 bg-slate-900 border border-slate-700 px-5 py-3 rounded-xl text-sm hidden shadow-2xl z-50 flex items-center gap-2"></div>

    <!-- JavaScript 業務邏輯 -->
