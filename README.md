# random-game
..07
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Игра — Угадай число</title>
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database-compat.js"></script>
  <style>
    body {
      background: linear-gradient(270deg, red, orange, yellow, green, cyan, blue, violet);
      background-size: 1400% 1400%;
      animation: gradient 15s ease infinite;
      font-family: Arial, sans-serif;
      text-align: center;
      color: white;
    }
    @keyframes gradient {
      0% {background-position:0% 50%}
      50% {background-position:100% 50%}
      100% {background-position:0% 50%}
    }
    h1 {
      font-size: 3em;
      text-shadow: 2px 2px 5px black;
    }
    input, button {
      padding: 10px;
      margin: 5px;
      border-radius: 10px;
      border: none;
      font-size: 1em;
      box-shadow: 2px 2px 8px rgba(0,0,0,0.5);
    }
    button {
      background: linear-gradient(45deg, #ff0080, #7928ca);
      color: white;
      cursor: pointer;
    }
    #leaderboard {
      margin-top: 20px;
      padding: 15px;
      background: rgba(0,0,0,0.4);
      border-radius: 15px;
    }
  </style>
</head>
<body>
  <h1>🎮 Угадай число</h1>

  <div id="loginDiv">
    <input type="text" id="nickname" placeholder="Введите никнейм">
    <button onclick="startGame()">Начать игру</button>
  </div>

  <div id="gameDiv" style="display:none;">
    <p>Мы загадали число от 1 до 100. Попробуй угадать!</p>
    <input type="number" id="guess" min="1" max="100">
    <button onclick="makeGuess()">Угадать</button>
    <p id="message"></p>
  </div>

  <div id="leaderboard">
    <h2>🏆 Лучшие игроки</h2>
    <ol id="scores"></ol>
  </div>

  <script>
    // ТВОИ данные из Firebase Console
    const firebaseConfig = {
      apiKey: "AIzaSyCQvOVtvW9pvpB_zX8BT8rl3ifq7ccCbWA",
      authDomain: "random-452ad.firebaseapp.com",
      databaseURL: "https://random-452ad-default-rtdb.firebaseio.com/",
      projectId: "random-452ad",
      storageBucket: "random-452ad.appspot.com",
      messagingSenderId: "59615060095",
      appId: "1:59615060095:web:85945336fae57ca3021f4a",
      measurementId: "G-G29JVBR978"
    };

    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    let secretNumber;
    let attempts;
    let playerName;

    function startGame() {
      playerName = document.getElementById("nickname").value.trim();
      if (!playerName) {
        alert("Введите никнейм!");
        return;
      }
      document.getElementById("loginDiv").style.display = "none";
      document.getElementById("gameDiv").style.display = "block";
      secretNumber = Math.floor(Math.random() * 100) + 1;
      attempts = 0;
    }

    function makeGuess() {
      const guess = parseInt(document.getElementById("guess").value);
      if (!guess) return;
      attempts++;
      if (guess === secretNumber) {
        document.getElementById("message").innerText =
          `🎉 Ура, ${playerName}! Ты угадал число за ${attempts} попыток!`;
        saveResult(playerName, attempts);
      } else if (guess < secretNumber) {
        document.getElementById("message").innerText = "📉 Загаданное число больше!";
      } else {
        document.getElementById("message").innerText = "📈 Загаданное число меньше!";
      }
    }

    function saveResult(name, score) {
      const scoresRef = db.ref("scores");
      scoresRef.push({ name, score });
    }

    function loadLeaderboard() {
      const scoresRef = db.ref("scores");
      scoresRef.on("value", snapshot => {
        const scoresList = document.getElementById("scores");
        scoresList.innerHTML = "";
        const scores = [];
        snapshot.forEach(child => {
          scores.push(child.val());
        });
        scores.sort((a, b) => a.score - b.score);
        scores.slice(0, 10).forEach(s => {
          const li = document.createElement("li");
          li.textContent = `${s.name} — ${s.score} попыток`;
          scoresList.appendChild(li);
        });
      });
    }

    loadLeaderboard();
  </script>
</body>
</html>
