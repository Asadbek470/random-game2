# random-game
..07
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Игра угадай число</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(270deg, red, orange, yellow, green, blue, indigo, violet);
      background-size: 1400% 1400%;
      animation: rainbow 15s ease infinite;
      color: white;
      text-align: center;
    }
    @keyframes rainbow {
      0% {background-position:0% 50%}
      50% {background-position:100% 50%}
      100% {background-position:0% 50%}
    }
    #leaderboard { margin-top: 20px; }
    table { margin: auto; border-collapse: collapse; }
    th, td { border: 1px solid white; padding: 8px; }
  </style>
</head>
<body>
  <h1>🎲 Угадай число!</h1>

  <div id="login">
    <input type="text" id="nickname" placeholder="Введите никнейм">
    <button onclick="startGame()">Начать игру</button>
  </div>

  <div id="game" style="display:none;">
    <p>Угадай число от 1 до 100</p>
    <input type="number" id="guess" min="1" max="100">
    <button onclick="makeGuess()">Проверить</button>
    <p id="result"></p>
  </div>

  <div id="leaderboard">
    <h2>🏆 Лучшие игроки</h2>
    <table>
      <thead><tr><th>Игрок</th><th>Попытки</th></tr></thead>
      <tbody id="scores"></tbody>
    </table>
  </div>

  <!-- Firebase -->
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

