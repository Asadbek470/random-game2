# random-game
..07
<!DOCTYPE html>
<html lang="ru">
<head>
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
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Угадай число</h1>
            <div class="subtitle">Проверь свою интуицию и попади в глобальный рейтинг!</div>
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
                            <th width="40%">Игрок</th>
                            <th width="25%">Страна</th>
                            <th width="25%">Рекорд</th>
                        </tr>
                    </thead>
                    <tbody id="leaderboard-body">
                        <tr>
                            <td colspan="4" style="text-align: center;">Загрузка рейтинга...</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // API endpoints (в реальном приложении должны быть защищены)
        const API_URL = 'https://jsonblob.com/api/jsonBlob';
        // Для демонстрации используем JSONBin, но в реальном приложении нужен собственный сервер
        
        // Хранилище данных
        let users = {};
        let currentUser = null;
        let targetNumber = 0;
        let attempts = 0;
        let gameStarted = false;
        
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

        // Загрузка рейтинга с сервера
        async function loadLeaderboard() {
            try {
                document.getElementById('leaderboard-body').innerHTML = `
                    <tr>
                        <td colspan="4" style="text-align: center;">
                            <div class="loading"></div> Загрузка рейтинга...
                        </td>
                    </tr>
                `;
                
                // В реальном приложении здесь должен быть запрос к вашему серверу
                // Для демонстрации используем localStorage, но с имитацией задержки сети
                await new Promise(resolve => setTimeout(resolve, 1000));
                
                // Получаем данные из localStorage (в реальном приложении - с сервера)
                const storedUsers = JSON.parse(localStorage.getItem('guessNumberUsers')) || {};
                users = storedUsers;
                
                updateLeaderboard();
            } catch (error) {
                console.error('Ошибка загрузки рейтинга:', error);
                document.getElementById('leaderboard-body').innerHTML = `
                    <tr>
                        <td colspan="4" style="text-align: center; color: #e74c3c;">
                            Ошибка загрузки рейтинга. Попробуйте позже.
                        </td>
                    </tr>
                `;
            }
        }

        // Сохранение данных на сервер
        async function saveData() {
            try {
                // В реальном приложении здесь должен быть запрос к вашему серверу
                // Для демонстрации используем localStorage
                localStorage.setItem('guessNumberUsers', JSON.stringify(users));
                
                // Имитация отправки на сервер
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
                btn.style.display = show ? 'inline-block' : 'none';
            });
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
                        bestScore: users[username].bestScore
                    });
                }
            }
            
            // Сортируем по рекорду (меньше попыток = лучше)
            usersWithRecords.sort((a, b) => a.bestScore - b.bestScore);
            
            // Заполняем таблицу (только топ-10)
            const topUsers = usersWithRecords.slice(0, 10);
            
            if (topUsers.length === 0) {
                leaderboardBody.innerHTML = '<tr><td colspan="4" style="text-align: center;">Пока нет записей в рейтинге</td></tr>';
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
            
            users[username] = { password, country, bestScore: null };
            
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
            
            document.getElementById('game-info').textContent = 'Я загадал число от 1 до 100. Попробуй угадать!';
            document.getElementById('attempts').textContent = 'Попытки: 0';
            document.getElementById('result').textContent = '';
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
                showMessage(document.getElementById('result'), `Поздравляем! Вы угадали число ${targetNumber} за ${attempts} попыток!`, 'success');
                
                // Загружаем актуальные данные перед обновлением
                await loadLeaderboard();
                
                // Обновляем рекорд, если он лучше предыдущего
                if (users[currentUser].bestScore === null || attempts < users[currentUser].bestScore) {
                    users[currentUser].bestScore = attempts;
                    
                    const saved = await saveData();
                    if (saved) {
                        updateLeaderboard();
                        
                        if (users[currentUser].bestScore === attempts) {
                            showMessage(document.getElementById('result'), 
                                      `Новый рекорд! Вы вошли в глобальный рейтинг с результатом ${attempts} попыток!`, 
                                      'success');
                        }
                    } else {
                        showMessage(document.getElementById('result'), 
                                  'Ошибка сохранения рекорда. Попробуйте позже.', 
                                  'error');
                    }
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

        // Показать сообщение
        function showMessage(element, message, type) {
            element.textContent = message;
            element.className = 'message ' + type;
        }
    </script>
</body>
</html>
