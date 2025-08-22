# random-game
..07
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Угадай число - Международный рейтинг</title>
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
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        input:focus {
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
            <div class="subtitle">Проверь свою интуицию и попади в международный рейтинг!</div>
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
                    <select id="country" style="width: 100%; padding: 12px 15px; border-radius: 8px; border: 2px solid #ddd; font-size: 16px;">
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
                <h2>Международный рейтинг игроков</h2>
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
                        <!-- Данные рейтинга будут загружены здесь -->
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        // Хранилище данных (в реальном приложении нужно использовать сервер)
        let users = JSON.parse(localStorage.getItem('guessNumberUsers')) || {};
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
            'mx': 'https://flagcdn.com/mx.svg'
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
            'mx': 'Мексика'
        };

        // Инициализация при загрузке
        window.onload = function() {
            updateLeaderboard();
            showGameElements(false);
            
            // Попытка автоматического входа, если пользователь уже авторизован
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                const userData = JSON.parse(savedUser);
                if (users[userData.username] && users[userData.username].password === userData.password) {
                    currentUser = userData.username;
                    updateUserInfo();
                    showGameElements(true);
                }
            }
        };

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
            if (currentUser) {
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
                if (users[username].bestScore !== undefined) {
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
            
            // Если нет записей в рейтинге
            if (topUsers.length === 0) {
                const row = document.createElement('tr');
                row.innerHTML = '<td colspan="4" style="text-align: center;">Пока нет записей в рейтинге</td>';
                leaderboardBody.appendChild(row);
            }
        }

        // Регистрация
        function register() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const country = document.getElementById('country').value;
            const messageEl = document.getElementById('auth-message');
            
            if (!username || !password || !country) {
                showMessage(messageEl, 'Заполните все поля', 'error');
                return;
            }
            
            if (users[username]) {
                showMessage(messageEl, 'Пользователь уже существует', 'error');
                return;
            }
            
            users[username] = { password, country, bestScore: null };
            localStorage.setItem('guessNumberUsers', JSON.stringify(users));
            
            showMessage(messageEl, 'Регистрация успешна! Теперь войдите.', 'success');
        }

        // Вход
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const messageEl = document.getElementById('auth-message');
            
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
        function checkGuess() {
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
                
                // Обновляем рекорд, если он лучше предыдущего
                if (users[currentUser].bestScore === null || attempts < users[currentUser].bestScore) {
                    users[currentUser].bestScore = attempts;
                    localStorage.setItem('guessNumberUsers', JSON.stringify(users));
                    updateLeaderboard();
                    
                    if (users[currentUser].bestScore === attempts) {
                        showMessage(document.getElementById('result'), 
                                  `Новый рекорд! Вы вошли в международный рейтинг с результатом ${attempts} попыток!`, 
                                  'success');
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
