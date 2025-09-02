#randomgame5
....7
<!DOCTYPE html>
<html lang="ru">
<head>
    <style>
    body { font-family: Arial, sans-serif; background:#0b0c10; color:#e6e6e6; margin:0; padding:20px; }
    textarea {
      width:100%; height:120px; padding:10px; font-size:15px;
      border-radius:8px; border:1px solid #444; background:#111; color:#fff;
    }
    button { margin-top:10px; padding:10px 15px; border-radius:6px; border:0; cursor:pointer;
      background:#e63946; color:white; font-weight:bold;
    }
    #blocker {
      position:fixed; inset:0; z-index:99999;
      display:none; align-items:center; justify-content:center;
      background:rgba(0,0,0,0.85);
      backdrop-filter: blur(4px);
    }
    .panel {
      background:#111217; padding:28px; border-radius:12px; box-shadow:0 10px 40px rgba(0,0,0,0.6);
      border:1px solid rgba(255,255,255,0.03); text-align:center;
    }
    .panel h1 { color:#e63946; margin-bottom:10px; }
  </style>
</head>
<body>
  <h2>📝 Напиши заметку</h2>
  <textarea id="note" placeholder="Введите текст..."></textarea><br>
  <button id="saveNote">Сохранить</button>

  <!-- Блокировка -->
  <div id="blocker">
    <div class="panel">
      <h1>🚫 Доступ временно ограничен</h1>
      <p>Вы нарушили правила: запрещены оскорбления и плохие слова.</p>
    </div>
  </div>

  <script>
    const badWords = ["лох","тупица","плохой","дурак","идиот","асадбек плохой","асадбек лох","мат"]; 
    // можно расширять список

    const noteInput = document.getElementById("note");
    const saveBtn = document.getElementById("saveNote");
    const blocker = document.getElementById("blocker");

    saveBtn.addEventListener("click", () => {
      let text = noteInput.value.toLowerCase();

      for (let word of badWords) {
        if (text.includes(word)) {
          // Показываем блокировку
          blocker.style.display = "flex";
          return;
        }
      }

      alert("Заметка сохранена ✅");
      noteInput.value = "";
    });
  </script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Угадай число - Глобальный рейтинг</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #333;
        }
        
        .container {
            width: 100%;
            max-width: 900px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(90deg, #4b6cb7 0%, #182848 100%);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .content {
            display: flex;
            flex-direction: column;
            padding: 20px;
        }
        
        .auth-section, .game-section, .leaderboard-section {
            margin-bottom: 30px;
        }
        
        h2 {
            color: #2c3e50;
            margin-bottom: 15px;
            padding-bottom: 5px;
            border-bottom: 2px solid #3498db;
        }
        
        .input-group {
            margin-bottom: 15px;
        }
        
        input, select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        input:focus, select:focus {
            border-color: #3498db;
            outline: none;
        }
        
        .btn {
            padding: 12px 20px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        
        .btn:hover {
            background: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .btn-success {
            background: #2ecc71;
        }
        
        .btn-success:hover {
            background: #27ae60;
        }
        
        .btn-danger {
            background: #e74c3c;
        }
        
        .btn-danger:hover {
            background: #c0392b;
        }
        
        .btn-warning {
            background: #f39c12;
        }
        
        .btn-warning:hover {
            background: #e67e22;
        }
        
        .btn-info {
            background: #17a2b8;
        }
        
        .btn-info:hover {
            background: #138496;
        }
        
        .message {
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            text-align: center;
        }
        
        .success {
            background: #d4edda;
            color: #155724;
        }
        
        .error {
            background: #f8d7da;
            color: #721c24;
        }
        
        .info {
            background: #d1ecf1;
            color: #0c5460;
        }
        
        .game-info {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            text-align: center;
            font-size: 18px;
        }
        
        .attempts {
            font-weight: bold;
            color: #e74c3c;
        }
        
        .leaderboard {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .leaderboard th, .leaderboard td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        
        .leaderboard th {
            background: #f8f9fa;
            font-weight: 600;
        }
        
        .leaderboard tr:hover {
            background: #f1f8ff;
        }
        
        .rank {
            font-weight: bold;
            text-align: center;
        }
        
        .top-1 { background: #fff9c4; }
        .top-2 { background: #e1f5fe; }
        .top-3 { background: #ffebee; }
        
        .flag {
            width: 24px;
            height: 16px;
            margin-right: 10px;
            vertical-align: middle;
            display: inline-block;
            background-size: cover;
            border-radius: 2px;
        }
        
        .section-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .user-info {
            font-size: 16px;
            color: #7f8c8d;
        }
        
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .currency-display {
            background: linear-gradient(135deg, #ffd700 0%, #ffec8b 100%);
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            color: #8b7500;
            display: inline-flex;
            align-items: center;
            margin-left: 10px;
        }
        
        .currency-icon {
            margin-right: 5px;
            font-size: 1.2em;
        }
        
        .hint-section {
            background: #f0f8ff;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
            border-left: 4px solid #3498db;
        }
        
        .hint-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 10px;
        }
        
        @media (max-width: 768px) {
            .content {
                padding: 15px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .btn {
                width: 100%;
                margin-bottom: 10px;
            }
            
            .hint-buttons {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Угадай число</h1>
            <div class="subtitle">Проверь свою интуицию и зарабатывай эски!</div>
        </header>
        
        <div class="content">
            <!-- Секция авторизации -->
            <div class="auth-section">
                <div class="section-title">
                    <h2>Вход / Регистрация</h2>
                    <div class="user-info" id="user-info"></div>
                </div>
                <div class="input-group">
                    <input type="text" id="username" placeholder="Придумайте логин">
                </div>
                <div class="input-group">
                    <input type="password" id="password" placeholder="Придумайте пароль">
                </div>
                <div class="input-group">
                    <select id="country">
                        <option value="">Выберите страну</option>
                        <option value="ru">Россия</option>
                        <option value="us">США</option>
                        <option value="de">Германия</option>
                        <option value="fr">Франция</option>
                        <option value="br">Бразилия</option>
                        <option value="cn">Китай</option>
                        <option value="jp">Япония</option>
                        <option value="in">Индия</option>
                        <option value="kr">Корея</option>
                        <option value="mx">Мексика</option>
                        <!-- Страны Средней Азии -->
                        <option value="kz">Казахстан</option>
                        <option value="uz">Узбекистан</option>
                        <option value="tj">Таджикистан</option>
                        <option value="kg">Кыргызстан</option>
                        <option value="tm">Туркменистан</option>
                    </select>
                </div>
                <button class="btn" onclick="login()">Войти</button>
                <button class="btn btn-success" onclick="register()">Зарегистрироваться</button>
                <div id="auth-message" class="message"></div>
            </div>
            
            <!-- Секция игры -->
            <div class="game-section">
                <h2>Игра</h2>
                <div id="game-info" class="game-info">Я загадал число от 1 до 100. Попробуй угадать!</div>
                <div id="attempts" class="attempts">Попытки: 0</div>
                <div class="input-group">
                    <input type="number" id="guess-input" placeholder="Введите число от 1 до 100" min="1" max="100">
                </div>
                <button class="btn" onclick="startGame()">Новая игра</button>
                <button class="btn btn-success" onclick="checkGuess()">Проверить</button>
                
                <!-- Секция подсказок -->
                <div class="hint-section">
                    <h3>Подсказки</h3>
                    <p>Купи подсказку, чтобы легче отгадать число!</p>
                    <div class="hint-buttons">
                        <button class="btn btn-info" onclick="buyHint('range')">Купить подсказку диапазона (5 эски)</button>
                        <button class="btn btn-info" onclick="buyHint('evenodd')">Купить подсказку четности (3 эски)</button>
                        <button class="btn btn-info" onclick="buyHint('multiple')">Купить подсказку кратности (7 эски)</button>
                    </div>
                    <div id="hint-result" class="message"></div>
                </div>
                
                <div id="result" class="message"></div>
            </div>
            
            <!-- Таблица лидеров -->
            <div class="leaderboard-section">
                <div class="section-title">
                    <h2>Глобальный рейтинг игроков</h2>
                    <button class="btn btn-warning" onclick="loadLeaderboard()">Обновить рейтинг</button>
                </div>
                <table class="leaderboard">
                    <thead>
                        <tr>
                            <th width="10%">Место</th>
                            <th width="30%">Игрок</th>
                            <th width="20%">Страна</th>
                            <th width="20%">Рекорд</th>
                            <th width="20%">Эски</th>
                        </tr>
                    </thead>
                    <tbody id="leaderboard-body">
                        <tr>
                            <td colspan="5" style="text-align: center;">Загрузка рейтинга...</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // Хранилище данных
        let users = {};
        let currentUser = null;
        let targetNumber = 0;
        let attempts = 0;
        let gameStarted = false;
        let hintsUsed = [];
        
        // Флаги стран
        const countryFlags = {
            'ru': 'https://flagcdn.com/ru.svg',
            'us': 'https://flagcdn.com/us.svg',
            'de': 'https://flagcdn.com/de.svg',
            'fr': 'https://flagcdn.com/fr.svg',
            'br': 'https://flagcdn.com/br.svg',
            'cn': 'https://flagcdn.com/cn.svg',
            'jp': 'https://flagcdn.com/jp.svg',
            'in': 'https://flagcdn.com/in.svg',
            'kr': 'https://flagcdn.com/kr.svg',
            'mx': 'https://flagcdn.com/mx.svg',
            // Флаги стран Средней Азии
            'kz': 'https://flagcdn.com/kz.svg',
            'uz': 'https://flagcdn.com/uz.svg',
            'tj': 'https://flagcdn.com/tj.svg',
            'kg': 'https://flagcdn.com/kg.svg',
            'tm': 'https://flagcdn.com/tm.svg'
        };
        
        // Названия стран
        const countryNames = {
            'ru': 'Россия',
            'us': 'США',
            'de': 'Германия',
            'fr': 'Франция',
            'br': 'Бразилия',
            'cn': 'Китай',
            'jp': 'Япония',
            'in': 'Индия',
            'kr': 'Корея',
            'mx': 'Мексика',
            // Названия стран Средней Азии
            'kz': 'Казахстан',
            'uz': 'Узбекистан',
            'tj': 'Таджикистан',
            'kg': 'Кыргызстан',
            'tm': 'Туркменистан'
        };

        // Инициализация при загрузке
        window.onload = function() {
            loadLeaderboard();
            showGameElements(false);
            
            // Попытка автоматического входа, если пользователь уже авторизован
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                const userData = JSON.parse(savedUser);
                currentUser = userData.username;
                updateUserInfo();
                showGameElements(true);
            }
        };

        // Загрузка рейтинга
        async function loadLeaderboard() {
            try {
                document.getElementById('leaderboard-body').innerHTML = `
                    <tr>
                        <td colspan="5" style="text-align: center;">
                            <div class="loading"></div> Загрузка рейтинга...
                        </td>
                    </tr>
                `;
                
                // Имитация задержки сети
                await new Promise(resolve => setTimeout(resolve, 1000));
                
                // Получаем данные из localStorage
                const storedUsers = JSON.parse(localStorage.getItem('guessNumberUsers')) || {};
                users = storedUsers;
                
                updateLeaderboard();
            } catch (error) {
                console.error('Ошибка загрузки рейтинга:', error);
                document.getElementById('leaderboard-body').innerHTML = `
                    <tr>
                        <td colspan="5" style="text-align: center; color: #e74c3c;">
                            Ошибка загрузки рейтинга. Попробуйте позже.
                        </td>
                    </tr>
                `;
            }
        }

        // Сохранение данных
        async function saveData() {
            try {
                localStorage.setItem('guessNumberUsers', JSON.stringify(users));
                await new Promise(resolve => setTimeout(resolve, 500));
                return true;
            } catch (error) {
                console.error('Ошибка сохранения данных:', error);
                return false;
            }
        }

        // Показать/скрыть элементы игры
        function showGameElements(show) {
            document.getElementById('game-info').style.display = show ? 'block' : 'none';
            document.getElementById('attempts').style.display = show ? 'block' : 'none';
            document.getElementById('guess-input').style.display = show ? 'block' : 'none';
            document.querySelectorAll('.game-section .btn').forEach(btn => {
                if (!btn.classList.contains('btn-info')) {
                    btn.style.display = show ? 'inline-block' : 'none';
                }
            });
            document.querySelector('.hint-section').style.display = show ? 'block' : 'none';
        }

        // Обновить информацию о пользователе
        function updateUserInfo() {
            if (currentUser && users[currentUser]) {
                const user = users[currentUser];
                const countryCode = user.country || '';
                const countryName = countryNames[countryCode] || '';
                
                let flagHtml = '';
                if (countryCode && countryFlags[countryCode]) {
                    flagHtml = `<span class="flag" style="background-image: url(${countryFlags[countryCode]})"></span>`;
                }
                
                document.getElementById('user-info').innerHTML = `
                    Вы вошли как: <strong>${currentUser}</strong> ${flagHtml} ${countryName}
                    <div class="currency-display">
                        <span class="currency-icon">🪙</span> ${user.eski || 0} эски
                    </div>
                    <button class="btn btn-danger" onclick="logout()" style="padding: 5px 10px; margin-left: 10px;">Выйти</button>
                `;
            } else {
                document.getElementById('user-info').innerHTML = '';
            }
        }

        // Обновить таблицу лидеров
        function updateLeaderboard() {
            const leaderboardBody = document.getElementById('leaderboard-body');
            leaderboardBody.innerHTML = '';
            
            // Создаем массив пользователей с рекордами
            const usersWithRecords = [];
            for (const username in users) {
                if (users[username].bestScore !== undefined && users[username].bestScore !== null) {
                    usersWithRecords.push({
                        username: username,
                        country: users[username].country,
                        bestScore: users[username].bestScore,
                        eski: users[username].eski || 0
                    });
                }
            }
            
            // Сортируем по рекорду (меньше попыток = лучше)
            usersWithRecords.sort((a, b) => a.bestScore - b.bestScore);
            
            // Заполняем таблицу (только топ-10)
            const topUsers = usersWithRecords.slice(0, 10);
            
            if (topUsers.length === 0) {
                leaderboardBody.innerHTML = '<tr><td colspan="5" style="text-align: center;">Пока нет записей в рейтинге</td></tr>';
                return;
            }
            
            topUsers.forEach((user, index) => {
                const row = document.createElement('tr');
                
                // Добавляем классы для первых трех мест
                if (index === 0) row.classList.add('top-1');
                else if (index === 1) row.classList.add('top-2');
                else if (index === 2) row.classList.add('top-3');
                
                const countryCode = user.country || '';
                let flagHtml = '';
                if (countryCode && countryFlags[countryCode]) {
                    flagHtml = `<span class="flag" style="background-image: url(${countryFlags[countryCode]})"></span>`;
                }
                
                row.innerHTML = `
                    <td class="rank">${index + 1}</td>
                    <td>${user.username}</td>
                    <td>${flagHtml} ${countryNames[countryCode] || ''}</td>
                    <td>${user.bestScore} попыток</td>
                    <td>${user.eski} эски</td>
                `;
                
                leaderboardBody.appendChild(row);
            });
        }

        // Регистрация
        async function register() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const country = document.getElementById('country').value;
            const messageEl = document.getElementById('auth-message');
            
            if (!username || !password || !country) {
                showMessage(messageEl, 'Заполните все поля', 'error');
                return;
            }
            
            // Загружаем актуальные данные
            await loadLeaderboard();
            
            if (users[username]) {
                showMessage(messageEl, 'Пользователь уже существует', 'error');
                return;
            }
            
            users[username] = { password, country, bestScore: null, eski: 0 };
            
            const saved = await saveData();
            if (saved) {
                showMessage(messageEl, 'Регистрация успешна! Теперь войдите.', 'success');
            } else {
                showMessage(messageEl, 'Ошибка регистрации. Попробуйте позже.', 'error');
            }
        }

        // Вход
        async function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const messageEl = document.getElementById('auth-message');
            
            // Загружаем актуальные данные
            await loadLeaderboard();
            
            if (!users[username] || users[username].password !== password) {
                showMessage(messageEl, 'Неверный логин или пароль', 'error');
                return;
            }
            
            currentUser = username;
            localStorage.setItem('currentUser', JSON.stringify({ username, password }));
            
            updateUserInfo();
            showGameElements(true);
            showMessage(messageEl, 'Вход выполнен успешно!', 'success');
            startGame();
        }

        // Выход
        function logout() {
            currentUser = null;
            localStorage.removeItem('currentUser');
            document.getElementById('user-info').innerHTML = '';
            showGameElements(false);
            document.getElementById('auth-message').innerHTML = '';
        }

        // Начать игру
        function startGame() {
            targetNumber = Math.floor(Math.random() * 100) + 1;
            attempts = 0;
            gameStarted = true;
            hintsUsed = [];
            
            document.getElementById('game-info').textContent = 'Я загадал число от 1 до 100. Попробуй угадать!';
            document.getElementById('attempts').textContent = 'Попытки: 0';
            document.getElementById('result').textContent = '';
            document.getElementById('hint-result').textContent = '';
            document.getElementById('guess-input').value = '';
            document.getElementById('guess-input').focus();
        }

        // Проверить предположение
        async function checkGuess() {
            if (!gameStarted) {
                showMessage(document.getElementById('result'), 'Сначала начните игру!', 'error');
                return;
            }
            
            if (!currentUser) {
                showMessage(document.getElementById('result'), 'Сначала войдите в систему!', 'error');
                return;
            }
            
            const guess = parseInt(document.getElementById('guess-input').value);
            
            if (isNaN(guess) || guess < 1 || guess > 100) {
                showMessage(document.getElementById('result'), 'Введите число от 1 до 100', 'error');
                return;
            }
            
            attempts++;
            document.getElementById('attempts').textContent = `Попытки: ${attempts}`;
            
            if (guess === targetNumber) {
                let rewardMessage = '';
                
                // Начисляем эски за победу за 1-5 попыток
                if (attempts <= 5) {
                    users[currentUser].eski = (users[currentUser].eski || 0) + 20;
                    rewardMessage = ` Вы получили 20 эски за победу за ${attempts} попытки!`;
                }
                
                showMessage(document.getElementById('result'), `Поздравляем! Вы угадали число ${targetNumber} за ${attempts} попыток!${rewardMessage}`, 'success');
                
                // Обновляем рекорд, если он лучше предыдущего
                let isNewRecord = false;
                if (users[currentUser].bestScore === null || attempts < users[currentUser].bestScore) {
                    users[currentUser].bestScore = attempts;
                    isNewRecord = true;
                }
                
                // Сохраняем данные
                const saved = await saveData();
                if (saved) {
                    updateLeaderboard();
                    updateUserInfo();
                    
                    if (isNewRecord) {
                        showMessage(document.getElementById('result'), 
                                  `Новый рекорд! Вы вошли в глобальный рейтинг с результатом ${attempts} попыток!`, 
                                  'success');
                    }
                } else {
                    showMessage(document.getElementById('result'), 
                              'Ошибка сохранения рекорда. Попробуйте позже.', 
                              'error');
                }
                
                gameStarted = false;
            } else if (guess < targetNumber) {
                showMessage(document.getElementById('result'), 'Загаданное число больше', 'info');
            } else {
                showMessage(document.getElementById('result'), 'Загаданное число меньше', 'info');
            }
            
            document.getElementById('guess-input').value = '';
            document.getElementById('guess-input').focus();
        }

        // Покупка подсказки
        function buyHint(type) {
            if (!gameStarted) {
                showMessage(document.getElementById('hint-result'), 'Сначала начните игру!', 'error');
                return;
            }
            
            if (!currentUser) {
                showMessage(document.getElementById('hint-result'), 'Сначала войдите в систему!', 'error');
                return;
            }
            
            const user = users[currentUser];
            const eski = user.eski || 0;
            let hintCost = 0;
            let hintMessage = '';
            
            // Определяем стоимость и содержание подсказки
            switch(type) {
                case 'range':
                    hintCost = 5;
                    if (hintsUsed.includes('range')) {
                        showMessage(document.getElementById('hint-result'), 'Вы уже использовали эту подсказку!', 'error');
                        return;
                    }
                    const rangeStart = Math.max(1, targetNumber - 10);
                    const rangeEnd = Math.min(100, targetNumber + 10);
                    hintMessage = `Загаданное число находится между ${rangeStart} и ${rangeEnd}`;
                    break;
                    
                case 'evenodd':
                    hintCost = 3;
                    if (hintsUsed.includes('evenodd')) {
                        showMessage(document.getElementById('hint-result'), 'Вы уже использовали эту подсказку!', 'error');
                        return;
                    }
                    hintMessage = `Загаданное число является ${targetNumber % 2 === 0 ? 'четным' : 'нечетным'}`;
                    break;
                    
                case 'multiple':
                    hintCost = 7;
                    if (hintsUsed.includes('multiple')) {
                        showMessage(document.getElementById('hint-result'), 'Вы уже использовали эту подсказку!', 'error');
                        return;
                    }
                    
                    // Находим делители числа
                    const divisors = [];
                    for (let i = 2; i < targetNumber; i++) {
                        if (targetNumber % i === 0) {
                            divisors.push(i);
                            if (divisors.length >= 2) break;
                        }
                    }
                    
                    if (divisors.length > 0) {
                        hintMessage = `Загаданное число делится на ${divisors.join(', ')}`;
                    } else {
                        hintMessage = 'Загаданное число является простым (делится только на 1 и само себя)';
                    }
                    break;
            }
            
            // Проверяем, хватает ли эски
            if (eski < hintCost) {
                showMessage(document.getElementById('hint-result'), `Недостаточно эски! Нужно ${hintCost}, у вас ${eski}.`, 'error');
                return;
            }
            
            // Списание эски и показ подсказки
            user.eski = eski - hintCost;
            hintsUsed.push(type);
            updateUserInfo();
            saveData();
            
            showMessage(document.getElementById('hint-result'), `Подсказка (стоимость: ${hintCost} эски): ${hintMessage}`, 'info');
        }

        // Показать сообщение
        function showMessage(element, message, type) {
            element.textContent = message;
            element.className = 'message ' + type;
        }
    </script>
</body>
</html>
