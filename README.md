# mathenglishhistory.github.edu
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Math, English, History, and More!</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#ffe1ef,#dceaff,#dcffe9);
  color: #27324a;
  text-align: center;
}
header { padding: 35px 10px; }
h1 { font-size: 35px; }
section {
  background: white;
  margin: 20px auto;
  padding: 22px;
  border-radius: 20px;
  max-width: 850px;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(150px,1fr));
  gap: 12px;
}
button {
  border: 0;
  border-radius: 14px;
  padding: 18px;
  font-size: 17px;
  font-weight: bold;
  cursor: pointer;
  background: #e6eaff;
}
button:hover { background: #ffd5e7; }
#display {
  font-size: 30px;
  padding: 15px;
  min-height: 35px;
}
.game {
  display: block;
  padding: 15px;
  margin: 8px;
  background: #e9f5ff;
  border-radius: 12px;
  color: #27324a;
  text-decoration: none;
  font-weight: bold;
}
.hidden { display: none; }
</style>
</head>
<body>

<header>
<h1>🌈 Math, English, History, and More!</h1>
<p>Welcome to your fun website!</p>
</header>

<section>
<h2>📚 Subjects</h2>
<div class="grid">
<button>🔢 Math</button>
<button>📖 English</button>
<button>🏛️ History</button>
<button>✨ More</button>
</div>
</section>

<section id="calculator">
<h2>🧮 Secret Calculator</h2>
<p>Enter the secret code to unlock games!</p>
<div id="display"></div>
<div class="grid">
<button onclick="add('1')">1</button>
<button onclick="add('2')">2</button>
<button onclick="add('3')">3</button>
<button onclick="add('4')">4</button>
<button onclick="add('5')">5</button>
<button onclick="add('6')">6</button>
<button onclick="add('7')">7</button>
<button onclick="add('8')">8</button>
<button onclick="add('9')">9</button>
<button onclick="clearCode()">C</button>
<button onclick="add('0')">0</button>
<button onclick="unlock()">OK</button>
</div>
<p id="message"></p>
</section>

<section id="games" class="hidden">
<h2>🎮 Choose a Game Category</h2>
<div class="grid" id="categories"></div>
<div id="gameList" class="hidden">
<h2 id="categoryName"></h2>
<div id="gameOptions"></div>
<button onclick="back()">⬅ Back</button>
</div>
</section>

<script>
let code = "";

function add(n) {
  if(code.length < 4) code += n;
  document.getElementById("display").textContent =
    "•".repeat(code.length);
}

function clearCode() {
  code = "";
  document.getElementById("display").textContent = "";
  document.getElementById("message").textContent = "";
}

function unlock() {
  if(code === "6767") {
    document.getElementById("calculator").classList.add("hidden");
    document.getElementById("games").classList.remove("hidden");
  } else {
    document.getElementById("message").textContent =
      "Wrong code! Try again.";
    clearCode();
  }
}

const games = {
  "🏎️ Racing": [
    ["Drive Mad","https://www.crazygames.com/game/drive-mad"],
    ["Drift Hunters","https://www.drifthunters.com/"],
    ["Moto X3M","https://www.coolmathgames.com/0-moto-x3m"],
    ["Smash Karts","https://smashkarts.io/"],
    ["Drift Boss","https://www.crazygames.com/game/drift-boss"]
  ],
  "🎯 Action": [
    ["Krunker.io","https://krunker.io/"],
    ["Shell Shockers","https://shellshock.io/"],
    ["Venge.io","https://venge.io/"],
    ["1v1.LOL","https://1v1.lol/"],
    ["Deadshot.io","https://deadshot.io/"]
  ],
  "🌐 Multiplayer": [
    ["Slither.io","https://slither.io/"],
    ["Agar.io","https://agar.io/"],
    ["Diep.io","https://diep.io/"],
    ["Bloxd.io","https://bloxd.io/"],
    ["Wormate.io","https://wormate.io/"]
  ],
  "🎉 Party": [
    ["Gartic Phone","https://garticphone.com/"],
    ["Skribbl.io","https://skribbl.io/"],
    ["Codenames","https://codenames.game/"],
    ["Wordle","https://www.nytimes.com/games/wordle/index.html"]
  ],
  "⚽ Sports": [
    ["Basketball Stars","https://www.crazygames.com/game/basketball-stars"],
    ["Retro Bowl","https://www.crazygames.com/game/retro-bowl"],
    ["Soccer Random","https://www.crazygames.com/game/soccer-random"],
    ["8 Ball Pool","https://www.miniclip.com/games/8-ball-pool-multiplayer/en/"]
  ],
  "🧩 Puzzle": [
    ["2048","https://play2048.co/"],
    ["Infinite Craft","https://neal.fun/infinite-craft/"],
    ["Little Alchemy 2","https://littlealchemy2.com/"],
    ["Minesweeper","https://minesweeper.online/"]
  ],
  "🏗️ Building": [
    ["Townscaper","https://oskarstalberg.com/Townscaper/"],
    ["Sandspiel","https://sandspiel.club/"],
    ["Minecraft Classic","https://classic.minecraft.net/"]
  ]
};

const categories = document.getElementById("categories");

Object.keys(games).forEach(name => {
  const button = document.createElement("button");
  button.textContent = name;
  button.onclick = () => showGames(name);
  categories.appendChild(button);
});

function showGames(name) {
  categories.classList.add("hidden");
  document.getElementById("gameList").classList.remove("hidden");
  document.getElementById("categoryName").textContent = name;

  const options = document.getElementById("gameOptions");
  options.innerHTML = "";

  games[name].forEach(game => {
    const link = document.createElement("a");
    link.className = "game";
    link.href = game[1];
    link.textContent = "🎮 " + game[0];
    options.appendChild(link);
  });
}

function back() {
  document.getElementById("gameList").classList.add("hidden");
  categories.classList.remove("hidden");
}
</script>
</body>
</html>
