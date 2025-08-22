# random-game
..07
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Угадай число</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: linear-gradient(45deg, red, orange, yellow, green, blue, indigo, violet);
      background-size: 400% 400%;
      animation: rainbow 10s infinite linear;
      color: white;
    }
    @keyframes rainbow {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    #login, #game {
      margin-top: 50px;
      padding: 20px;
      border-radius: 15px;
      background: rgba(0,0,0,0.6);
      display: inline-block;
    }
    input, button {
      padding: 10px;
      margin: 5px;
      border-radius: 10px;
      border: none;
    }
    button {
      background: #00ffcc;
      cursor: pointer;
      font-weight: bold;
    }
    table {
      margin: 20px auto;
      border-collapse: collapse;
      width: 60%;
      background: rgba(255,255,255,0.1);
    }
    th, td {
      padding: 10px;
      border: 1px solid white;
    }
  </style>
</head>
<body>
  <h1>🎮 Угадай число 🎮</h1>

  <div id="login">
    <input type="text" id="nickname" placeholder="Введите никнейм">
    <button onclick="startGame()">Начать игру</button>
  </div>

  <div id="game" style="display:none;">
    <input type="number" id="guess" placeholder="Ваш ответ">
    <button onclick="makeGuess()">Угадать</button>
    <p id="result"></p>

    <h2>🏆 Лучшие игроки</h2>
    <table>
      <thead>
        <tr><th>Никнейм</th><th>Попытки</th></tr>
      </thead>
      <tbody id="scores"></tbody>
    </table>
  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
    import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCQvOVtvW9pvpB_zX8BT8rl3ifq7ccCbWA",
      authDomain: "random-452ad.firebaseapp.com",
      databaseURL: "https://random-452ad-default-rtdb.firebaseio.com",
      projectId: "random-452ad",
      storageBucket: "random-452ad.appspot.com",
      messagingSenderId: "59615060095",
      appId: "1:59615060095:web:85945336fae57ca3021f4a"
    };

    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);

    let randomNumber;
    let attempts = 0;
    let currentNickname = "";

    function startGame() {
      currentNickname = document.getElementById("nickname").value.trim();
      if (!currentNickname) {
        alert("Введите никнейм!");
        return;
      }
      document.getElementById("login").style.display = "none";
      document.getElementById("game").style.display = "block";
      randomNumber = Math.floor(Math.random() * 100) + 1;
      attempts = 0;
    }
    window.startGame = startGame;

    function makeGuess() {
      const guess = parseInt(document.getElementById("guess").value);
      if (isNaN(guess)) {
        alert("Введите число!");
        return;
      }
      attempts++;
      if (guess === randomNumber) {
        document.getElementById("result").innerText =
          `🎉 Правильно! Вы угадали за ${attempts} попыток.`;
        saveScore(currentNickname, attempts);
      } else if (guess < randomNumber) {
        document.getElementById("result").innerText = "Слишком маленькое число!";
      } else {
        document.getElementById("result").innerText = "Слишком большое число!";
      }
    }
    window.makeGuess = makeGuess;

    function saveScore(nickname, attempts) {
      push(ref(db, "scores"), {
        name: nickname,
        attempts: attempts,
        timestamp: Date.now()
      });
    }

    function loadScores() {
      const scoresRef = ref(db, "scores");
      onValue(scoresRef, (snapshot) => {
        const data = snapshot.val();
        const list = [];
        for (let id in data) {
          list.push(data[id]);
        }
        list.sort((a, b) => a.attempts - b.attempts);
        const tbody = document.getElementById("scores");
        tbody.innerHTML = "";
        list.slice(0, 10).forEach((item) => {
          const row = `<tr><td>${item.name}</td><td>${item.attempts}</td></tr>`;
          tbody.innerHTML += row;
        });
      });
    }
    loadScores();
  </script>
</body>
</html>
