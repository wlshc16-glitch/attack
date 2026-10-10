<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>皮克敏 🍄 蘑菇計時器</title>
    <!-- 引入 Tailwind CSS 框架 -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- 引入圓潤可愛的字體 Nunito，符合皮克敏風格 -->
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Nunito', sans-serif;
            background-color: #f4faeb; /* 淺草綠色背景 */
            background-image: 
                radial-gradient(#c6f6d5 2px, transparent 2px),
                radial-gradient(#c6f6d5 2px, transparent 2px);
            background-size: 32px 32px;
            background-position: 0 0, 16px 16px;
        }

        /* 隱藏數字輸入框的上下箭頭，讓畫面更乾淨 */
        input[type="number"]::-webkit-inner-spin-button,
        input[type="number"]::-webkit-outer-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type="number"] {
            -moz-appearance: textfield;
        }

        /* 蘑菇完成時的紅框閃爍動畫 */
        @keyframes alert-pulse {
            0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.7); transform: scale(1); }
            50% { box-shadow: 0 0 0 15px rgba(239, 68, 68, 0); transform: scale(1.02); }
            100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); transform: scale(1); }
        }

        .mushroom-done {
            animation: alert-pulse 1.5s infinite;
            background-color: #fee2e2 !important; /* 淺紅色背景 */
            border-color: #ef4444 !important; /* 紅色邊框 */
        }
        
        /* 童趣按鈕按下特效 */
        .btn-press {
            box-shadow: 0 6px 0px rgba(0,0,0,0.15);
            transition: all 0.1s;
        }
        .btn-press:active:not(:disabled) {
            box-shadow: 0 0px 0px rgba(0,0,0,0.15);
            transform: translateY(6px);
        }
    </style>
</head>
<body class="text-gray-800 min-h-screen p-4 md:p-6 flex flex-col items-center">

    <header class="text-center mb-8 w-full max-w-6xl mt-4">
        <div class="inline-block bg-white/90 backdrop-blur-sm px-10 py-6 rounded-3xl shadow-xl border-b-8 border-green-500 w-full md:w-auto relative overflow-hidden">
            <!-- 裝飾用背景小圖示 -->
            <div class="absolute -top-4 -left-4 text-6xl opacity-20 transform -rotate-12">🌸</div>
            <div class="absolute -bottom-4 -right-4 text-6xl opacity-20 transform rotate-12">🍀</div>
            
            <h1 class="text-3xl md:text-5xl font-black text-green-700 mb-4 flex items-center justify-center gap-3 relative z-10">
                <span class="text-4xl md:text-5xl">🌱</span> 皮克敏蘑菇計時器 <span class="text-4xl md:text-5xl">🍄</span>
            </h1>
            <div class="bg-gray-100 rounded-2xl p-4 inline-block shadow-inner relative z-10">
                <p class="text-gray-500 font-bold mb-1 text-sm tracking-widest">現在時間</p>
                <div id="current-time" class="text-5xl md:text-7xl font-black tracking-wider text-gray-800 font-mono">
                    --:--:--
                </div>
            </div>
        </div>
    </header>

    <main class="w-full max-w-6xl flex flex-col lg:flex-row gap-8 items-start">
        
        <!-- 左側：輸入表單區 -->
        <section class="w-full lg:w-1/3 bg-white rounded-[2rem] shadow-xl p-6 md:p-8 border-t-8 border-yellow-400 flex-shrink-0 sticky top-6">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-black text-gray-700 flex items-center gap-2">
                     ⏱️ 新增蘑菇
                </h2>
                <div id="counter-badge" class="bg-blue-100 text-blue-800 text-sm font-black px-4 py-1.5 rounded-full shadow-sm">
                    0 / 18
                </div>
            </div>

            <form id="mushroom-form" class="space-y-6">
                <!-- 蘑菇名稱 -->
                <div>
                    <label for="m-name" class="block text-base font-bold text-gray-600 mb-2">蘑菇地點</label>
                    <select id="m-name" required 
                        class="w-full px-5 py-4 rounded-2xl bg-gray-50 border-2 border-gray-200 focus:outline-none focus:border-yellow-400 focus:bg-white text-lg font-bold transition-colors cursor-pointer">
                        <option value="" disabled selected>請選擇蘑菇地點...</option>
                        <option value="迦光">迦光</option>
                        <option value="泰味">泰味</option>
                        <option value="樹太">樹太</option>
                        <option value="香蕉">香蕉</option>
                        <option value="水塔">水塔</option>
                        <option value="國際">國際</option>
                        <option value="運動">運動</option>
                        <option value="福德">福德</option>
                        <option value="貓圍">貓圍</option>
                        <option value="晉福">晉福</option>
                        <option value="大戰">大戰</option>
                        <option value="櫻花">櫻花</option>
                        <option value="籃球">籃球</option>
                        <option value="獅身">獅身</option>
                        <option value="康橋">康橋</option>
                    </select>
                </div>
                
                <!-- 預計完成時間 (時/分/秒) -->
                <div>
                    <label class="block text-base font-bold text-gray-600 mb-2">預計完成時間 (時 : 分 : 秒)</label>
                    <div class="flex items-center gap-2">
                        <!-- 時 -->
                        <div class="flex-1 relative">
                            <input type="number" id="m-hour" required min="0" max="23" placeholder="00"
                                class="w-full px-2 py-4 rounded-2xl bg-gray-50 border-2 border-gray-200 focus:outline-none focus:border-blue-400 focus:bg-white text-2xl font-black text-center font-mono transition-colors">
                            <span class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 font-bold text-sm">時</span>
                        </div>
                        <span class="text-2xl font-black text-gray-400">:</span>
                        <!-- 分 -->
                        <div class="flex-1 relative">
                            <input type="number" id="m-minute" required min="0" max="59" placeholder="00"
                                class="w-full px-2 py-4 rounded-2xl bg-gray-50 border-2 border-gray-200 focus:outline-none focus:border-blue-400 focus:bg-white text-2xl font-black text-center font-mono transition-colors">
                            <span class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 font-bold text-sm">分</span>
                        </div>
                        <span class="text-2xl font-black text-gray-400">:</span>
                        <!-- 秒 -->
                        <div class="flex-1 relative">
                            <input type="number" id="m-second" required min="0" max="59" placeholder="00"
                                class="w-full px-2 py-4 rounded-2xl bg-gray-50 border-2 border-gray-200 focus:outline-none focus:border-blue-400 focus:bg-white text-2xl font-black text-center font-mono transition-colors">
                            <span class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 font-bold text-sm">秒</span>
                        </div>
                    </div>
                    <p class="text-xs text-gray-400 mt-2 font-bold bg-blue-50 p-2 rounded-lg inline-block">
                        💡 提示：如果輸入的時間比現在還早，系統會自動判定為「明天」。
                    </p>
                </div>
                
                <!-- 錯誤訊息提示 -->
                <div id="error-message" class="hidden text-red-600 text-center font-black bg-red-100 p-4 rounded-xl border-2 border-red-200">
                    ⚠️ 已達到最高 18 筆上限！
                </div>

                <!-- 提交按鈕 -->
                <button type="submit" id="submit-btn" 
                    class="w-full bg-blue-500 hover:bg-blue-600 text-white font-black text-xl py-4 px-6 rounded-2xl btn-press disabled:opacity-50 disabled:cursor-not-allowed disabled:box-shadow-none disabled:transform-none">
                    ➕ 新增至派兵清單
                </button>
            </form>
        </section>

        <!-- 右側：蘑菇清單區 -->
        <section class="w-full lg:w-2/3 bg-white rounded-[2rem] shadow-xl p-6 md:p-8 border-t-8 border-red-500 min-h-[500px]">
            <div class="flex justify-between items-center mb-6 border-b-2 border-gray-100 pb-4">
                <h2 class="text-2xl font-black text-gray-700 flex items-center gap-2">
                    📋 即將出現的蘑菇
                </h2>
            </div>
            
            <!-- 空狀態提示 -->
            <div id="empty-state" class="text-center py-16 flex flex-col items-center justify-center">
                <span class="text-8xl mb-6 opacity-80 animate-bounce text-gray-300">💤</span>
                <p class="text-gray-500 font-black text-2xl">目前沒有待打的蘑菇</p>
                <p class="text-gray-400 font-bold mt-2">快從左邊輸入任務，派皮克敏出發吧！</p>
            </div>

            <!-- 清單容器 -->
            <ul id="mushroom-list" class="space-y-4">
                <!-- 列表項目將由 JavaScript 動態生成 -->
            </ul>
        </section>

    </main>

    <script>
        const MAX_ITEMS = 18;
        // 從 LocalStorage 載入資料，確保資料持久化
        let mushrooms = JSON.parse(localStorage.getItem('pikminMushrooms_v3')) || [];
        
        // DOM 元素選取
        const form = document.getElementById('mushroom-form');
        const nameInput = document.getElementById('m-name');
        const hourInput = document.getElementById('m-hour');
        const minuteInput = document.getElementById('m-minute');
        const secondInput = document.getElementById('m-second');
        const submitBtn = document.getElementById('submit-btn');
        const errorMessage = document.getElementById('error-message');
        const counterBadge = document.getElementById('counter-badge');
        const mushroomList = document.getElementById('mushroom-list');
        const emptyState = document.getElementById('empty-state');
        const clockElement = document.getElementById('current-time');

        // 主要時鐘更新函數
        function updateMainClock() {
            const now = new Date();
            const h = String(now.getHours()).padStart(2, '0');
            const m = String(now.getMinutes()).padStart(2, '0');
            const s = String(now.getSeconds()).padStart(2, '0');
            clockElement.textContent = `${h}:${m}:${s}`;
        }
        
        // 啟動主時鐘
        updateMainClock();
        setInterval(updateMainClock, 1000);

        // 計算目標時間的時間戳 (包含自動判定明天)
        function calculateTargetTimestamp(h, m, s) {
            const now = new Date();
            // 建立一個今天的該時間點物件
            const targetDate = new Date(now.getFullYear(), now.getMonth(), now.getDate(), h, m, s);
            
            // 關鍵邏輯：如果設定的時間小於現在時間，代表是隔天
            if (targetDate.getTime() <= now.getTime()) {
                targetDate.setDate(targetDate.getDate() + 1);
            }
            
            return targetDate.getTime();
        }

        // 當輸入框失去焦點時，自動補零 (提升 UX)
        [hourInput, minuteInput, secondInput].forEach(input => {
            input.addEventListener('blur', function() {
                if (this.value !== '' && this.value.length === 1) {
                    this.value = '0' + this.value;
                }
            });
        });

        // 處理表單送出
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (mushrooms.length >= MAX_ITEMS) return;

            const name = nameInput.value.trim();
            const h = parseInt(hourInput.value);
            const m = parseInt(minuteInput.value);
            const s = parseInt(secondInput.value);

            if (name && !isNaN(h) && !isNaN(m) && !isNaN(s)) {
                // 計算最終目標時間戳
                const targetTimestamp = calculateTargetTimestamp(h, m, s);

                // 建立新的蘑菇物件
                const newMushroom = {
                    id: 'm_' + Date.now().toString() + Math.floor(Math.random()*100),
                    name: name,
                    targetTime: targetTimestamp,
                    originalTimeStr: `${String(h).padStart(2, '0')}:${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`
                };
                
                mushrooms.push(newMushroom);
                saveAndRender();
                
                // 重置表單
                nameInput.value = '';
                hourInput.value = '';
                minuteInput.value = '';
                secondInput.value = '';
                nameInput.focus();
            }
        });

        // 儲存並重新渲染畫面
        function saveAndRender() {
            // 根據目標時間戳進行排序：越快到來的排在最上面
            mushrooms.sort((a, b) => a.targetTime - b.targetTime);
            
            // 儲存至 LocalStorage
            localStorage.setItem('pikminMushrooms_v3', JSON.stringify(mushrooms));
            
            updateFormState();
            renderList();
        }

        // 更新左側表單區塊狀態 (防呆與上限計算)
        function updateFormState() {
            const count = mushrooms.length;
            counterBadge.textContent = `${count} / ${MAX_ITEMS}`;
            
            if (count >= MAX_ITEMS) {
                submitBtn.disabled = true;
                errorMessage.classList.remove('hidden');
                counterBadge.classList.replace('bg-blue-100', 'bg-red-100');
                counterBadge.classList.replace('text-blue-800', 'text-red-800');
            } else {
                submitBtn.disabled = false;
                errorMessage.classList.add('hidden');
                counterBadge.classList.replace('bg-red-100', 'bg-blue-100');
                counterBadge.classList.replace('text-red-800', 'text-blue-800');
            }
        }

        // 渲染右側蘑菇清單
        function renderList() {
            mushroomList.innerHTML = '';
            
            if (mushrooms.length === 0) {
                emptyState.classList.remove('hidden');
            } else {
                emptyState.classList.add('hidden');
                
                // 皮克敏風格顏色陣列，隨機配給邊框顏色
                const borderColors = ['border-red-400', 'border-yellow-400', 'border-blue-400', 'border-purple-400'];
                
                mushrooms.forEach((mushroom, index) => {
                    const li = document.createElement('li');
                    li.id = `mushroom-${mushroom.id}`;
                    
                    const borderColor = borderColors[index % borderColors.length];
                    
                    li.className = `flex flex-col sm:flex-row justify-between items-start sm:items-center p-5 rounded-2xl border-l-[12px] bg-white shadow-sm transition-all duration-300 gap-4 ${borderColor} border-t-2 border-r-2 border-b-2 border-t-gray-100 border-r-gray-100 border-b-gray-100`;
                    
                    // 判斷是否為「明天」來顯示標籤
                    const targetDateObj = new Date(mushroom.targetTime);
                    const isTomorrow = targetDateObj.getDate() !== new Date().getDate();
                    const dayLabel = isTomorrow ? '<span class="bg-purple-100 text-purple-700 text-xs px-2 py-1 rounded-md ml-2 font-black">明天</span>' : '';

                    li.innerHTML = `
                        <div class="flex-1 w-full">
                            <div class="flex flex-wrap items-center gap-2 mb-2">
                                <h3 class="font-black text-xl text-gray-800">🍄 ${mushroom.name}</h3>
                            </div>
                            <div class="text-sm font-bold text-gray-500 mb-1 flex items-center bg-gray-50 inline-block px-3 py-1 rounded-lg">
                                🎯 設定時間: <span class="font-mono ml-2 text-gray-700">${mushroom.originalTimeStr}</span> ${dayLabel}
                            </div>
                            <div class="text-base font-black flex items-center gap-2 mt-2">
                                ⏳ 剩餘: <span class="countdown-text font-mono text-xl text-blue-600 bg-blue-50 px-3 py-1 rounded-lg shadow-inner" data-target="${mushroom.targetTime}">計算中...</span>
                            </div>
                        </div>
                        <button onclick="deleteMushroom('${mushroom.id}')" 
                            class="w-full sm:w-auto bg-gray-100 hover:bg-red-500 hover:text-white text-gray-600 font-black py-3 px-6 rounded-xl transition-colors shrink-0 btn-press">
                            完成 / 刪除
                        </button>
                    `;
                    mushroomList.appendChild(li);
                });
                
                // 立即更新一次倒數時間
                updateCountdowns();
            }
        }

        // 刪除特定蘑菇的函數 (綁定在全域)
        window.deleteMushroom = function(id) {
            mushrooms = mushrooms.filter(m => m.id !== id);
            saveAndRender();
        }

        // 更新清單中每個蘑菇的倒數計時與狀態
        function updateCountdowns() {
            const countdownElements = document.querySelectorAll('.countdown-text');
            const now = new Date().getTime();

            countdownElements.forEach(el => {
                const targetTime = parseInt(el.getAttribute('data-target'));
                const diff = targetTime - now;
                const listItem = el.closest('li');

                if (diff <= 0) {
                    // 時間到了，觸發完成動畫
                    el.textContent = '✅ 可收成！';
                    el.className = 'countdown-text font-black text-2xl text-red-600 tracking-wide';
                    
                    if (!listItem.classList.contains('mushroom-done')) {
                        listItem.classList.add('mushroom-done');
                        // 替換原本的邊框設定，確保醒目
                        listItem.className = listItem.className.replace(/border-(red|yellow|blue|purple)-400/, '');
                    }
                } else {
                    // 尚未到期，計算剩餘時間
                    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                    const seconds = Math.floor((diff % (1000 * 60)) / 1000);
                    
                    const timeText = `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
                    el.textContent = timeText;
                }
            });
        }

        // 每秒執行一次倒數計時更新
        setInterval(updateCountdowns, 1000);
        
        // 初始載入渲染
        saveAndRender();

    </script>
</body>
</html>
