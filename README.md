<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Capybara Memory Game 💖</title>
<style>
  body {
    background-color: #ffeef7;
    font-family: "Comic Sans MS", cursive;
    text-align: center;
    padding-top: 40px;
  }

  h1 {
    color: #ff6fb5;
    text-shadow: 2px 2px #fff;
  }

  .game-board {
    display: grid;
    grid-template-columns: repeat(4, 100px);
    gap: 15px;
    justify-content: center;
    margin-top: 30px;
  }

  .card {
    width: 100px;
    height: 100px;
    background-color: #ffd8eb;
    border-radius: 15px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    cursor: pointer;
    font-size: 2em;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.4s, background-color 0.4s;
  }

  .card.flipped {
    background-color: #ffb8d2;
    transform: rotateY(180deg);
  }

  .card.matched {
    background-color: #d4ffd7;
    cursor: default;
  }

  #score {
    margin-top: 20px;
    color: #ff62a5;
    font-size: 1.3em;
  }

  footer {
    margin-top: 40px;
    color: #888;
  }
</style>
</head>
<body>

<h1>Capybara Memory Game 💖</h1>
<p id="score">Score: 0</p>

<div class="game-board" id="gameBoard"></div>

<footer>Made with 🩷 by Ngọc & Capybara</footer>

<script>
  const emojis = ['💖', '🌸', '🍓', '⭐', '🐾', '🦋', '🌈', '🍉'];
  let cards = [...emojis, ...emojis].sort(() => 0.5 - Math.random());
  const board = document.getElementById('gameBoard');
  let firstCard = null;
  let lockBoard = false;
  let score = 0;

  function createBoard() {
    cards.forEach((emoji) => {
      const card = document.createElement('div');
      card.classList.add('card');
      card.dataset.emoji = emoji;
      card.addEventListener('click', flipCard);
      board.appendChild(card);
    });
  }

  function flipCard() {
    if (lockBoard || this.classList.contains('flipped') || this.classList.contains('matched')) return;

    this.classList.add('flipped');
    this.textContent = this.dataset.emoji;

    if (!firstCard) {
      firstCard = this;
    } else {
      lockBoard = true;
      setTimeout(() => {
        if (this.dataset.emoji === firstCard.dataset.emoji) {
          this.classList.add('matched');
          firstCard.classList.add('matched');
          score++;
          document.getElementById('score').textContent = `Score: ${score}`;
          if (score === emojis.length) alert("🎉 You win! Capybara is proud of you 💗");
        } else {
          this.classList.remove('flipped');
          this.textContent = '';
          firstCard.classList.remove('flipped');
          firstCard.textContent = '';
        }
        firstCard = null;
        lockBoard = false;
      }, 800);
    }
  }

  createBoard();
</script>

</body>
</html>
