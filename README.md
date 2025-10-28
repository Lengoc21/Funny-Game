<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🐹 Capybara Memory Game 💖</title>
<style>
  body {
    font-family: "Poppins", sans-serif;
    background: linear-gradient(135deg, #ffd6ec, #c6f0ff);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
  }

  h1 {
    color: #ff69b4;
    margin-bottom: 20px;
  }

  .game-board {
    display: grid;
    grid-template-columns: repeat(4, 80px);
    gap: 10px;
  }

  .card {
    width: 80px;
    height: 80px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    cursor: pointer;
    transition: all 0.3s;
  }

  .card.flipped {
    background-color: #ffe6f2;
    transform: rotateY(180deg);
  }

  .card.matched {
    background-color: #bdfcc9;
    cursor: default;
  }

  #score {
    margin-top: 15px;
    font-weight: bold;
    color: #333;
  }
</style>
</head>
<body>
  <h1>🐹 Capybara Memory Game 💖</h1>
  <div class="game-board" id="gameBoard"></div>
  <div id="score">Score: 0</div>

<script>
  const symbols = ["💖","⭐","🥕","🌈","🍓","🍒","🌸","🍉"];
  let cards = [...symbols, ...symbols];
  let firstCard = null, secondCard = null;
  let score = 0;

  // shuffle
  cards.sort(() => Math.random() - 0.5);

  const board = document.getElementById("gameBoard");
  const scoreBoard = document.getElementById("score");

  // create cards
  cards.forEach(symbol => {
    const card = document.createElement("div");
    card.classList.add("card");
    card.dataset.symbol = symbol;
    card.textContent = "❓";
    board.appendChild(card);

    card.addEventListener("click", () => flipCard(card));
  });

  function flipCard(card) {
    if (card.classList.contains("flipped") || card.classList.contains("matched")) return;

    card.classList.add("flipped");
    card.textContent = card.dataset.symbol;

    if (!firstCard) {
      firstCard = card;
    } else {
      secondCard = card;
      setTimeout(checkMatch, 600);
    }
  }

  function checkMatch() {
    if (firstCard.dataset.symbol === secondCard.dataset.symbol) {
      firstCard.classList.add("matched");
      secondCard.classList.add("matched");
      score++;
      scoreBoard.textContent = `Score: ${score}`;
    } else {
      firstCard.classList.remove("flipped");
      secondCard.classList.remove("flipped");
      firstCard.textContent = "❓";
      secondCard.textContent = "❓";
    }
    firstCard = null;
    secondCard = null;
  }
</script>
</body>
</html>
