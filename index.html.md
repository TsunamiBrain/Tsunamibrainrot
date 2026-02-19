<!DOCTYPE html>  
<html>  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">  
    <title>🧸 TSUNAMI BRAIN · Telegram</title>  
    <!-- Подключаем Telegram Web App SDK -->  
    <script src="https://telegram.org/js/telegram-web-app.js"></script>  
    <style>  
        * {  
            margin: 0;  
            padding: 0;  
            box-sizing: border-box;  
            user-select: none;  
            -webkit-tap-highlight-color: transparent;  
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;  
        }  
  
        body {  
            background: var(--tg-theme-bg-color, #0a0f1a);  
            color: var(--tg-theme-text-color, #ffffff);  
            min-height: 100vh;  
            display: flex;  
            justify-content: center;  
            align-items: center;  
            padding: 8px;  
        }  
  
        .game-container {  
            max-width: 500px;  
            width: 100%;  
            background: var(--tg-theme-secondary-bg-color, #1a2538);  
            border-radius: 40px;  
            padding: 20px 16px;  
            box-shadow: 0 10px 20px rgba(0,0,0,0.3);  
        }  
  
        /* Верхняя панель с пользователем */  
        .user-header {  
            display: flex;  
            align-items: center;  
            gap: 15px;  
            background: var(--tg-theme-section-bg-color, #253a55);  
            border-radius: 30px;  
            padding: 12px 18px;  
            margin-bottom: 20px;  
        }  
  
        .user-avatar {  
            width: 50px;  
            height: 50px;  
            border-radius: 50%;  
            background: #ffaa33;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
            font-size: 30px;  
        }  
  
        .user-info {  
            flex: 1;  
        }  
  
        .user-name {  
            font-weight: 700;  
            font-size: 18px;  
        }  
  
        .brain-balance {  
            background: #ffaa33;  
            color: #1a1a1a;  
            padding: 8px 16px;  
            border-radius: 40px;  
            font-weight: 700;  
            display: flex;  
            align-items: center;  
            gap: 5px;  
        }  
  
        /* Энергия */  
        .energy-bar {  
            background: #2a405c;  
            border-radius: 30px;  
            height: 25px;  
            margin: 15px 0;  
            overflow: hidden;  
            position: relative;  
        }  
  
        .energy-fill {  
            background: linear-gradient(90deg, #4d7cff, #8ab5ff);  
            height: 100%;  
            width: 100%;  
            border-radius: 30px;  
            transition: width 0.2s;  
        }  
  
        .energy-text {  
            position: absolute;  
            top: 50%;  
            left: 50%;  
            transform: translate(-50%, -50%);  
            color: white;  
            font-weight: 600;  
            font-size: 14px;  
            text-shadow: 0 1px 2px black;  
        }  
  
        /* ТАПЕР */  
        .tap-area {  
            background: #ffb347;  
            border-radius: 80px;  
            padding: 30px 20px;  
            margin: 20px 0;  
            text-align: center;  
            border: 4px solid white;  
            box-shadow: 0 10px 0 #b36b00;  
            transform: translateY(0);  
            transition: 0.05s;  
            cursor: pointer;  
        }  
  
        .tap-area:active {  
            transform: translateY(5px);  
            box-shadow: 0 5px 0 #b36b00;  
        }  
  
        .brain-emoji {  
            font-size: 120px;  
            filter: drop-shadow(0 8px 0 #b36b00);  
            transition: 0.1s;  
        }  
  
        .tap-area:active .brain-emoji {  
            transform: scale(1.1);  
        }  
  
        .tap-power {  
            font-size: 18px;  
            color: white;  
            font-weight: 700;  
            margin-top: 5px;  
        }  
  
        /* Статистика */  
        .stats-row {  
            display: flex;  
            gap: 8px;  
            margin: 15px 0;  
        }  
  
        .stat-card {  
            flex: 1;  
            background: #253a55;  
            border-radius: 30px;  
            padding: 12px 5px;  
            text-align: center;  
            border: 2px solid #4a6380;  
        }  
  
        .stat-value {  
            font-size: 24px;  
            font-weight: 700;  
            color: #ffd966;  
        }  
  
        /* Вкладки */  
        .tabs {  
            display: flex;  
            gap: 5px;  
            margin: 20px 0 10px;  
            flex-wrap: wrap;  
        }  
  
        .tab {  
            flex: 1;  
            min-width: 60px;  
            background: #253a55;  
            padding: 10px 5px;  
            border-radius: 30px;  
            border: 2px solid #4a6380;  
            text-align: center;  
            font-weight: 600;  
            font-size: 13px;  
            cursor: pointer;  
        }  
  
        .tab.active {  
            background: #ffaa33;  
            color: #1a1a1a;  
            border-color: white;  
        }  
  
        /* Контент вкладок */  
        .tab-content {  
            background: #1e3147;  
            border-radius: 30px;  
            padding: 15px;  
            min-height: 250px;  
            max-height: 350px;  
            overflow-y: auto;  
        }  
  
        /* Сетка брейнротов */  
        .brains-grid {  
            display: grid;  
            grid-template-columns: repeat(3, 1fr);  
            gap: 8px;  
        }  
  
        .brain-card {  
            background: #2a405c;  
            border-radius: 25px;  
            padding: 10px 5px;  
            text-align: center;  
            border: 2px solid #5f7fb0;  
            cursor: pointer;  
        }  
  
        .brain-card:active {  
            transform: scale(0.95);  
        }  
  
        .brain-emoji-small {  
            font-size: 35px;  
        }  
  
        .brain-name-small {  
            font-size: 12px;  
            font-weight: 600;  
            margin: 5px 0;  
        }  
  
        .brain-price {  
            background: #ffaa33;  
            color: #1a1a1a;  
            padding: 3px;  
            border-radius: 20px;  
            font-size: 11px;  
            font-weight: 700;  
        }  
  
        .owned-badge {  
            background: #4caf50;  
            color: white;  
            border-radius: 50%;  
            width: 22px;  
            height: 22px;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
            margin: 0 auto 5px;  
            font-size: 12px;  
        }  
  
        /* Квесты */  
        .quest-item {  
            background: #253a55;  
            border-radius: 25px;  
            padding: 12px;  
            margin-bottom: 10px;  
            display: flex;  
            align-items: center;  
            gap: 10px;  
            border-left: 8px solid #ffaa33;  
        }  
  
        .quest-icon {  
            font-size: 30px;  
            width: 50px;  
            height: 50px;  
            background: #1e3147;  
            border-radius: 50%;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
        }  
  
        .quest-info {  
            flex: 1;  
        }  
  
        .quest-progress-bar {  
            height: 8px;  
            background: #1e3147;  
            border-radius: 10px;  
            margin: 5px 0;  
        }  
  
        .quest-progress-fill {  
            height: 100%;  
            background: #4caf50;  
            border-radius: 10px;  
            width: 0%;  
        }  
  
        .quest-reward {  
            color: #ffd966;  
            font-weight: 700;  
        }  
  
        /* Лидеры */  
        .leader-item {  
            display: flex;  
            align-items: center;  
            gap: 10px;  
            background: #253a55;  
            border-radius: 30px;  
            padding: 8px 15px;  
            margin-bottom: 8px;  
        }  
  
        .leader-rank {  
            font-size: 20px;  
            font-weight: 800;  
            color: #ffaa33;  
            width: 35px;  
        }  
  
        .leader-avatar {  
            width: 35px;  
            height: 35px;  
            background: #ffaa33;  
            border-radius: 50%;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
        }  
  
        .leader-name {  
            flex: 1;  
            font-weight: 600;  
        }  
  
        .leader-score {  
            background: #1e3147;  
            padding: 5px 12px;  
            border-radius: 30px;  
            font-weight: 600;  
        }  
  
        .footer {  
            text-align: center;  
            color: #5f7fb0;  
            margin-top: 15px;  
            font-size: 12px;  
        }  
  
        .floating-number {  
            position: fixed;  
            color: #ffd966;  
            font-size: 40px;  
            font-weight: 800;  
            text-shadow: 2px 2px 0 #b36b00;  
            pointer-events: none;  
            z-index: 9999;  
            animation: floatUp 1s ease-out forwards;  
        }  
  
        @keyframes floatUp {  
            0% { opacity: 1; transform: translateY(0); }  
            100% { opacity: 0; transform: translateY(-100px); }  
        }  
    </style>  
</head>  
<body>  
    <div class="game-container">  
        <!-- Шапка с пользователем Telegram -->  
        <div class="user-header" id="userHeader">  
            <div class="user-avatar" id="userAvatar">🧸</div>  
            <div class="user-info">  
                <div class="user-name" id="userName">Загрузка...</div>  
                <div style="font-size: 12px; color: #aac5ff;">ID: <span id="userId">...</span></div>  
            </div>  
            <div class="brain-balance" id="balanceDisplay">🧠 0</div>  
        </div>  
  
        <!-- Энергия -->  
        <div class="energy-bar">  
            <div class="energy-fill" id="energyFill" style="width: 100%"></div>  
            <div class="energy-text" id="energyText">1000/1000</div>  
        </div>  
  
        <!-- ГЛАВНЫЙ ТАПЕР -->  
        <div class="tap-area" id="tapButton" onclick="handleTap(event)">  
            <div class="brain-emoji" id="mainBrainEmoji">🧠</div>  
            <div class="tap-power" id="tapPowerDisplay">+1 за тык</div>  
        </div>  
  
        <!-- Статистика -->  
        <div class="stats-row">  
            <div class="stat-card">  
                <div>⏱️/сек</div>  
                <div class="stat-value" id="profitPerSec">0</div>  
            </div>  
            <div class="stat-card">  
                <div>📊 всего</div>  
                <div class="stat-value" id="totalEarned">0</div>  
            </div>  
            <div class="stat-card">  
                <div>👥 друзья</div>  
                <div class="stat-value" id="friendsCount">0</div>  
            </div>  
        </div>  
  
        <!-- Вкладки -->  
        <div class="tabs">  
            <div class="tab active" onclick="switchTab('brains')" id="tabBrains">🧠 Брейнроты</div>  
            <div class="tab" onclick="switchTab('boosts')" id="tabBoosts">⚡ Бусты</div>  
            <div class="tab" onclick="switchTab('quests')" id="tabQuests">📋 Квесты</div>  
            <div class="tab" onclick="switchTab('leaders')" id="tabLeaders">🏆 Лидеры</div>  
        </div>  
  
        <!-- Контент -->  
        <div class="tab-content" id="tabContent"></div>  
  
        <div class="footer">  
            🧸 TSUNAMI BRAIN · игра в Telegram  
        </div>  
    </div>  
  
    <script>  
        // ==================== TELEGRAM INIT ====================  
        let tg = window.Telegram?.WebApp;  
        let user = tg?.initDataUnsafe?.user;  
          
        // ==================== БАЗА БРЕЙНРОТОВ ====================  
        const BRAINS = [  
            { id: 'b1', name: 'Мозгоша', emoji: '🧠', profit: 1, price: 10 },  
            { id: 'b2', name: 'Зомбик', emoji: '🧟', profit: 2, price: 30 },  
            { id: 'b3', name: 'Скелетик', emoji: '💀', profit: 3, price: 50 },  
            { id: 'b4', name: 'Слаймик', emoji: '🟢', profit: 4, price: 80 },  
            { id: 'b5', name: 'Привид', emoji: '👻', profit: 5, price: 120 },  
            { id: 'b6', name: 'Оборотень', emoji: '🐺', profit: 10, price: 250 },  
            { id: 'b7', name: 'Вампир', emoji: '🧛', profit: 15, price: 400 },  
            { id: 'b8', name: 'Инопланетянин', emoji: '👽', profit: 20, price: 600 },  
            { id: 'b9', name: 'Дракон', emoji: '🐉', profit: 40, price: 1200 },  
            { id: 'b10', name: 'Кракен', emoji: '🐙', profit: 50, price: 1500 },  
            { id: 'b11', name: 'Инфинити', emoji: '♾️', profit: 100, price: 4000 },  
            { id: 'b12', name: 'Ктулху', emoji: '👾', profit: 300, price: 20000 }  
        ];  
  
        // ==================== ИГРОВЫЕ ДАННЫЕ ====================  
        let balance = 500;  
        let totalEarned = 0;  
        let tapPower = 1;  
        let energy = 1000;  
        let maxEnergy = 1000;  
        let ownedBrains = [];  
        let friends = [  
            { name: 'Мозгоед', emoji: '🧸', profit: 5 },  
            { name: 'Тапатель', emoji: '🐼', profit: 8 }  
        ];  
        let profitPerSec = 0;  
        let currentTab = 'brains';  
          
        // Квесты  
        let quests = [  
            { id: 1, name: 'Тапатель', desc: 'Сделай 100 тапов', icon: '👆', goal: 100, progress: 0, reward: 200, completed: false },  
            { id: 2, name: 'Коллекционер', desc: 'Купи 3 брейнрота', icon: '🧠', goal: 3, progress: 0, reward: 300, completed: false },  
            { id: 3, name: 'Друзья', desc: 'Пригласи 2 друзей', icon: '👥', goal: 2, progress: 0, reward: 400, completed: false },  
            { id: 4, name: 'Миллионер', desc: 'Заработай 1000 мозгов', icon: '💰', goal: 1000, progress: 0, reward: 500, completed: false }  
        ];  
  
        // Лидеры  
        let leaders = [  
            { name: 'BrainLucker', emoji: '🦊', score: 15420 },  
            { name: 'TsunamiKing', emoji: '🐉', score: 12350 },  
            { name: 'TapMaster', emoji: '🐼', score: 9870 },  
            { name: 'CandyGirl', emoji: '🦄', score: 8540 },  
            { name: 'МозгоБот', emoji: '🤖', score: 7210 },  
            { name: user?.first_name || 'Ты', emoji: '🧸', score: 0 }  
        ];  
  
        // ==================== ЗАГРУЗКА ====================  
        function loadGame() {  
            // Загружаем из localStorage (для каждого пользователя свой ключ)  
            const userId = user?.id || 'guest';  
            const saved = localStorage.getItem(`tsunami_tg_${userId}`);  
              
            if (saved) {  
                const data = JSON.parse(saved);  
                balance = data.balance || 500;  
                totalEarned = data.totalEarned || 0;  
                tapPower = data.tapPower || 1;  
                energy = data.energy || 1000;  
                maxEnergy = data.maxEnergy || 1000;  
                ownedBrains = data.ownedBrains || [];  
                quests = data.quests || quests;  
            }  
              
            // Стартовый набор  
            if (ownedBrains.length === 0) {  
                ownedBrains.push({ id: 'b1', count: 1 });  
            }  
  
            // Показываем информацию о пользователе  
            if (user) {  
                document.getElementById('userName').innerHTML = user.first_name + (user.last_name ? ' ' + user.last_name : '');  
                document.getElementById('userId').innerHTML = user.id;  
                if (user.photo_url) {  
                    document.getElementById('userAvatar').innerHTML = `<img src="${user.photo_url}" style="width:50px; height:50px; border-radius:50%;">`;  
                }  
            }  
  
            // Растягиваем на весь экран в Telegram  
            if (tg) {  
                tg.expand();  
                tg.enableClosingConfirmation();  
            }  
  
            calculateProfit();  
            updateUI();  
            startAutoProfit();  
        }  
  
        function saveGame() {  
            const userId = user?.id || 'guest';  
            const data = { balance, totalEarned, tapPower, energy, maxEnergy, ownedBrains, quests };  
            localStorage.setItem(`tsunami_tg_${userId}`, JSON.stringify(data));  
        }  
  
        // ==================== ТАП ====================  
        function handleTap(event) {  
            if (energy < tapPower) {  
                tg?.showAlert('⚡ Нет энергии! Жди восстановления');  
                return;  
            }  
  
            energy -= tapPower;  
            const earned = tapPower;  
            balance += earned;  
            totalEarned += earned;  
  
            // Всплывашка  
            const rect = event.target.getBoundingClientRect();  
            const floating = document.createElement('div');  
            floating.className = 'floating-number';  
            floating.innerHTML = `+${earned} 🧠`;  
            floating.style.left = (event.clientX || rect.left + rect.width/2) + 'px';  
            floating.style.top = (event.clientY || rect.top) + 'px';  
            document.body.appendChild(floating);  
            setTimeout(() => floating.remove(), 1000);  
  
            // Анимация  
            const brainEmoji = document.getElementById('mainBrainEmoji');  
            brainEmoji.style.transform = 'scale(1.2)';  
            setTimeout(() => brainEmoji.style.transform = 'scale(1)', 100);  
  
            // Вибрация (Telegram поддерживает)  
            tg?.HapticFeedback?.impactOccurred('light');  
  
            // Обновляем квесты  
            quests.forEach(q => {  
                if (q.id === 1) q.progress = Math.min(q.goal, q.progress + earned);  
                if (q.id === 4) q.progress = Math.min(q.goal, totalEarned);  
            });  
  
            checkQuests();  
            saveGame();  
            updateUI();  
        }  
  
        // ==================== ПОКУПКА ====================  
        function buyBrain(brainId) {  
            const brain = BRAINS.find(b => b.id === brainId);  
            const owned = ownedBrains.find(b => b.id === brainId);  
            let price = brain.price;  
            if (owned) price = Math.floor(brain.price * (1 + owned.count * 0.3));  
  
            if (balance < price) {  
                tg?.showAlert('❌ Не хватает мозгов!');  
                return;  
            }  
  
            balance -= price;  
  
            if (owned) {  
                owned.count++;  
            } else {  
                ownedBrains.push({ id: brainId, count: 1 });  
            }  
  
            // Квест на покупку  
            const totalBrains = ownedBrains.reduce((acc, b) => acc + b.count, 0);  
            quests.forEach(q => {  
                if (q.id === 2) q.progress = Math.min(q.goal, totalBrains);  
            });  
  
            tg?.HapticFeedback?.notificationOccurred('success');  
            calculateProfit();  
            checkQuests();  
            saveGame();  
            updateUI();  
        }  
  
        // ==================== БУСТЫ ====================  
        function buyBoost(boostType) {  
            const costs = { 'tap2': 200, 'tap5': 500, 'energy': 300, 'full': 100 };  
              
            if (balance < costs[boostType]) {  
                tg?.showAlert('❌ Мало мозгов!');  
                return;  
            }  
  
            balance -= costs[boostType];  
  
            switch(boostType) {  
                case 'tap2': tapPower *= 2; break;  
                case 'tap5': tapPower *= 5; break;  
                case 'energy': maxEnergy += 200; energy = maxEnergy; break;  
                case 'full': energy = maxEnergy; break;  
            }  
  
            tg?.HapticFeedback?.notificationOccurred('success');  
            saveGame();  
            updateUI();  
        }  
  
        // ==================== ДРУЗЬЯ ====================  
        function addFriend() {  
            if (balance < 100) {  
                tg?.showAlert('❌ Нужно 100 мозгов');  
                return;  
            }  
              
            balance -= 100;  
            friends.push({  
                name: 'Новичок',  
                emoji: ['🐥','🐣','🦊','🐸'][Math.floor(Math.random()*4)],  
                profit: Math.floor(Math.random() * 10) + 5  
            });  
  
            quests.forEach(q => {  
                if (q.id === 3) q.progress = Math.min(q.goal, friends.length);  
            });  
  
            calculateProfit();  
            checkQuests();  
            saveGame();  
            updateUI();  
        }  
  
        // ==================== КВЕСТЫ ====================  
        function checkQuests() {  
            quests.forEach(q => {  
                if (q.progress >= q.goal && !q.completed) {  
                    q.completed = true;  
                    balance += q.reward;  
                    tg?.showAlert(`✅ Квест выполнен! +${q.reward} 🧠`);  
                    tg?.HapticFeedback?.notificationOccurred('success');  
                }  
            });  
        }  
  
        // ==================== ДОХОД ====================  
        function calculateProfit() {  
            profitPerSec = 0;  
            ownedBrains.forEach(owned => {  
                const brain = BRAINS.find(b => b.id === owned.id);  
                if (brain) profitPerSec += brain.profit * owned.count;  
            });  
            friends.forEach(f => profitPerSec += f.profit);  
            return profitPerSec;  
        }  
  
        function startAutoProfit() {  
            setInterval(() => {  
                if (profitPerSec > 0) {  
                    balance += profitPerSec;  
                    totalEarned += profitPerSec;  
                    energy = Math.min(maxEnergy, energy + 2);  
                      
                    quests.forEach(q => {  
                        if (q.id === 1) q.progress = Math.min(q.goal, q.progress + profitPerSec);  
                        if (q.id === 4) q.progress = Math.min(q.goal, totalEarned);  
                    });  
                      
                    leaders[5].score = totalEarned;  
                    checkQuests();  
                    saveGame();  
                    updateUI();  
                }  
            }, 1000);  
        }  
  
        // ==================== ИНТЕРФЕЙС ====================  
        function switchTab(tab) {  
            currentTab = tab;  
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));  
            document.getElementById(`tab${tab.charAt(0).toUpperCase() + tab.slice(1)}`).classList.add('active');  
            updateTabContent();  
        }  
  
        function updateTabContent() {  
            const content = document.getElementById('tabContent');  
              
            if (currentTab === 'brains') {  
                let html = '<div class="brains-grid">';  
                BRAINS.forEach(brain => {  
                    const owned = ownedBrains.find(b => b.id === brain.id);  
                    const count = owned ? owned.count : 0;  
                    let price = brain.price;  
                    if (owned) price = Math.floor(brain.price * (1 + owned.count * 0.3));  
                      
                    html += `  
                        <div class="brain-card" onclick="buyBrain('${brain.id}')">  
                            ${count > 0 ? `<div class="owned-badge">${count}</div>` : ''}  
                            <div class="brain-emoji-small">${brain.emoji}</div>  
                            <div class="brain-name-small">${brain.name}</div>  
                            <div class="brain-price">🧠 ${Math.floor(price)}</div>  
                        </div>  
                    `;  
                });  
                html += '</div>';  
                content.innerHTML = html;  
            }  
              
            else if (currentTab === 'boosts') {  
                content.innerHTML = `  
                    <div style="display:grid; gap:10px;">  
                        <div class="brain-card" onclick="buyBoost('tap2')">  
                            <div class="brain-emoji-small">✌️</div>  
                            <div class="brain-name-small">ТАП x2</div>  
                            <div class="brain-price">🧠 200</div>  
                        </div>  
                        <div class="brain-card" onclick="buyBoost('tap5')">  
                            <div class="brain-emoji-small">🖐️</div>  
                            <div class="brain-name-small">ТАП x5</div>  
                            <div class="brain-price">🧠 500</div>  
                        </div>  
                        <div class="brain-card" onclick="buyBoost('energy')">  
                            <div class="brain-emoji-small">🔋</div>  
                            <div class="brain-name-small">+200 энергии</div>  
                            <div class="brain-price">🧠 300</div>  
                        </div>  
                        <div class="brain-card" onclick="buyBoost('full')">  
                            <div class="brain-emoji-small">⚡</div>  
                            <div class="brain-name-small">Полная энергия</div>  
                            <div class="brain-price">🧠 100</div>  
                        </div>  
                    </div>  
                `;  
            }  
              
            else if (currentTab === 'quests') {  
                let html = '';  
                quests.forEach(q => {  
                    const percent = (q.progress / q.goal) * 100;  
                    html += `  
                        <div class="quest-item">  
                            <div class="quest-icon">${q.icon}</div>  
                            <div class="quest-info">  
                                <div style="font-weight:700;">${q.name}</div>  
                                <div style="font-size:12px;">${q.desc}</div>  
                                <div class="quest-progress-bar">  
                                    <div class="quest-progress-fill" style="width:${percent}%"></div>  
                                </div>  
                                <div class="quest-reward">+${q.reward} 🧠</div>  
                            </div>  
                            ${q.completed ? '✅' : ''}  
                        </div>  
                    `;  
                });  
                content.innerHTML = html;  
            }  
              
            else if (currentTab === 'leaders') {  
                let html = '';  
                leaders.sort((a,b) => b.score - a.score).forEach((l, idx) => {  
                    html += `  
                        <div class="leader-item">  
                            <div class="leader-rank">#${idx+1}</div>  
                            <div class="leader-avatar">${l.emoji}</div>  
                            <div class="leader-name">${l.name}</div>  
                            <div class="leader-score">${formatNumber(l.score)}</div>  
                        </div>  
                    `;  
                });  
                content.innerHTML = html;  
            }  
        }  
  
        function updateUI() {  
            document.getElementById('balanceDisplay').innerHTML = `🧠 ${formatNumber(balance)}`;  
            document.getElementById('totalEarned').innerHTML = formatNumber(totalEarned);  
            document.getElementById('profitPerSec').innerHTML = formatNumber(profitPerSec);  
            document.getElementById('tapPowerDisplay').innerHTML = `+${tapPower} за тык`;  
            document.getElementById('friendsCount').innerHTML = friends.length;  
              
            const energyPercent = (energy / maxEnergy) * 100;  
            document.getElementById('energyFill').style.width = energyPercent + '%';  
            document.getElementById('energyText').innerHTML = `${Math.floor(energy)}/${maxEnergy}`;  
              
            leaders[5].score = totalEarned;  
            updateTabContent();  
        }  
  
        function formatNumber(num) {  
            if (num >= 1e6) return (num/1e6).toFixed(1) + 'M';  
            if (num >= 1e3) return (num/1e3).toFixed(1) + 'K';  
            return num;  
        }  
  
        // Глобальные функции  
        window.handleTap = handleTap;  
        window.buyBrain = buyBrain;  
        window.buyBoost = buyBoost;  
        window.addFriend = addFriend;  
        window.switchTab = switchTab;  
  
        // Запуск  
        loadGame();  
    </script>  
</body>  
</html>  
