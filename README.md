<!DOCTYPE html>
<html>
<head>
  <title>Capybara Click!</title>
  <style>
    body {
      text-align: center;
      background: #fffafc;
      font-family: "Comic Sans MS", cursive;
    }
    #capy {
      width: 150px;
      cursor: pointer;
      transition: transform 0.2s;
    }
    #capy:active {
      transform: scale(1.1);
    }
    h1 {
      color: #ff69b4;
    }
  </style>
</head>
<body>
  <h1>Click the Capybara! 🩷</h1>
  <img id="capy" src="https://media3.giphy.com/media/ej4lfadivQe1W/giphy.gif" alt="capybara"/>
  <h2>Score: <span id="score">0</span></h2>

  <script>
    let score = 0;
    const capy = document.getElementById("capy");
    const scoreDisplay = document.getElementById("score");

    capy.addEventListener("click", () => {
      score++;
      scoreDisplay.textContent = score;
    });
  </script>
</body>
</html>
