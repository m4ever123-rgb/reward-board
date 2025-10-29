<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>لوحة التعزيز التفاعلية</title>
  <style>
    body {
      font-family: "Tajawal", sans-serif;
      background: #f5f7fa;
      color: #333;
      text-align: center;
      padding: 20px;
    }
    h1 {
      color: #444;
      margin-bottom: 20px;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 20px;
      margin: 20px auto;
      max-width: 1000px;
    }
    .group {
      background: white;
      border-radius: 20px;
      padding: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      transition: transform 0.2s ease;
    }
    .group:hover { transform: scale(1.03); }

    .group h2 {
      margin-bottom: 10px;
      font-size: 1.3em;
    }

    .emoji {
      font-size: 2em;
      margin-bottom: 10px;
    }

    .progress-container {
      background: #eee;
      border-radius: 10px;
      overflow: hidden;
      height: 20px;
      margin: 10px 0;
    }

    .progress {
      height: 100%;
      width: 0%;
      transition: width 0.4s ease;
    }

    .controls {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-top: 10px;
    }

    button {
      border: none;
      border-radius: 10px;
      padding: 8px 14px;
      font-size: 1.1em;
      cursor: pointer;
      color: white;
    }

    .reset {
      margin-top: 30px;
      background: #444;
      color: white;
      padding: 10px 20px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 1.1em;
    }

    /* ألوان المجموعات */
    .yellow { background-color: #ffeb3b; }
    .blue { background-color: #2196f3; }
    .red { background-color: #f44336; }
    .green { background-color: #4caf50; }
    .purple { background-color: #9c27b0; }
  </style>
</head>
<body>
  <h1>🌟 لوحة التعزيز التفاعلية 🌟</h1>
  <div class="board">
    <div class="group" data-group="yellow">
      <div class="emoji">⭐</div>
      <h2 style="color:#fdd835;">النجوم</h2>
      <div class="progress-container"><div class="progress yellow"></div></div>
      <p>النجوم: <span class="score">0</span> / 10</p>
      <div class="controls">
        <button style="background:#fdd835;" onclick="addStar('yellow')">➕</button>
        <button style="background:#fdd835;" onclick="removeStar('yellow')">➖</button>
      </div>
    </div>

    <div class="group" data-group="blue">
      <div class="emoji">🦸‍♂️</div>
      <h2 style="color:#2196f3;">الأبطال</h2>
      <div class="progress-container"><div class="progress blue"></div></div>
      <p>النجوم: <span class="score">0</span> / 10</p>
      <div class="controls">
        <button style="background:#2196f3;" onclick="addStar('blue')">➕</button>
        <button style="background:#2196f3;" onclick="removeStar('blue')">➖</button>
      </div>
    </div>

    <div class="group" data-group="red">
      <div class="emoji">🎨</div>
      <h2 style="color:#f44336;">المبدعون</h2>
      <div class="progress-container"><div class="progress red"></div></div>
      <p>النجوم: <span class="score">0</span> / 10</p>
      <div class="controls">
        <button style="background:#f44336;" onclick="addStar('red')">➕</button>
        <button style="background:#f44336;" onclick="removeStar('red')">➖</button>
      </div>
    </div>

    <div class="group" data-group="green">
      <div class="emoji">🤝</div>
      <h2 style="color:#4caf50;">المتعاونون</h2>
      <div class="progress-container"><div class="progress green"></div></div>
      <p>النجوم: <span class="score">0</span> / 10</p>
      <div class="controls">
        <button style="background:#4caf50;" onclick="addStar('green')">➕</button>
        <button style="background:#4caf50;" onclick="removeStar('green')">➖</button>
      </div>
    </div>

    <div class="group" data-group="purple">
      <div class="emoji">🏆</div>
      <h2 style="color:#9c27b0;">المتفوقون</h2>
      <div class="progress-container"><div class="progress purple"></div></div>
      <p>النجوم: <span class="score">0</span> / 10</p>
      <div class="controls">
        <button style="background:#9c27b0;" onclick="addStar('purple')">➕</button>
        <button style="background:#9c27b0;" onclick="removeStar('purple')">➖</button>
      </div>
    </div>
  </div>

  <button class="reset" onclick="resetAll()">🔄 تصفير الجميع</button>

  <script>
    const maxStars = 10;

    function loadScores() {
      document.querySelectorAll('.group').forEach(group => {
        const name = group.dataset.group;
        const saved = localStorage.getItem(name) || 0;
        updateDisplay(name, parseInt(saved));
      });
    }

    function addStar(name) {
      let score = parseInt(localStorage.getItem(name) || 0);
      if (score < maxStars) {
        score++;
        localStorage.setItem(name, score);
        updateDisplay(name, score);
      }
    }

    function removeStar(name) {
      let score = parseInt(localStorage.getItem(name) || 0);
      if (score > 0) {
        score--;
        localStorage.setItem(name, score);
        updateDisplay(name, score);
      }
    }

    function updateDisplay(name, score) {
      const group = document.querySelector(`.group[data-group="${name}"]`);
      group.querySelector('.score').textContent = score;
      group.querySelector('.progress').style.width = (score / maxStars * 100) + '%';
    }

    function resetAll() {
      if (confirm("هل تريدين تصفير جميع النقاط؟")) {
        document.querySelectorAll('.group').forEach(group => {
          const name = group.dataset.group;
          localStorage.setItem(name, 0);
          updateDisplay(name, 0);
        });
      }
    }

    loadScores();
  </script>
</body>
</html>
