# 3weeks
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>두더지 잡기 게임</title>
    <style>
        body {
            background-image: url('background.jpg'); 
            background-size: cover;
            background-repeat: no-repeat;
            background-attachment: fixed;
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 10px;
        }
        .cell {
            width: 100px;
            height: 100px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
        }
        .mole {
            width: 80px;
            height: 80px;
        }
    </style>
</head>
<body>
    <h1>두더지 잡기 게임</h1>
    <p>남은 시간: <span id="timer">10</span> 초</p>
    <p>점수: <span id="score">0</span></p>
    <div class="grid" id="game-grid"></div>

    <script>
        const grid = document.getElementById("game-grid");
        const timerDisplay = document.getElementById("timer");
        const scoreDisplay = document.getElementById("score");

        let score = 0;
        let timer = 10; // 게임 시간 (초)

        function updateGrid() {
            grid.innerHTML = "";
            for (let row = 0; row < 3; row++) {
                for (let col = 0; col < 3; col++) {
                    const cell = document.createElement("div");
                    cell.className = "cell";
                    cell.dataset.row = row;
                    cell.dataset.col = col;

                    const moleImage = document.createElement("img");
                    moleImage.src = "mole.png"; 
                    moleImage.alt = "두더지";
                    moleImage.className = "mole";
                    moleImage.style.display = "none"; 

                    cell.appendChild(moleImage);
                    grid.appendChild(cell);
                }
            }
        }

        function startGame() {
            score = 0;
            timer = 10;
            scoreDisplay.textContent = score;
            timerDisplay.textContent = timer;
            updateGrid();
            playGame();
        }

        function getRandomCell() {
            const randomRow = Math.floor(Math.random() * 3);
            const randomCol = Math.floor(Math.random() * 3);
            return document.querySelector(`[data-row="${randomRow}"][data-col="${randomCol}"]`);
        }

        function playGame() {
            const moleCell = getRandomCell();
            const moleImage = moleCell.querySelector(".mole");

            moleImage.style.display = "block"; 

            const showTime = 1000; 

            setTimeout(() => {
                moleImage.style.display = "none"; 
                if (timer > 0) {
                    playGame();
                }
            }, showTime);

            timer--;
            timerDisplay.textContent = timer;

            if (timer === 0) {
                alert(`게임 종료! 당신의 점수는 ${score}점입니다.`);
            }
        }

        grid.addEventListener("click", () => {
            if (timer > 0) {
                score++;
                scoreDisplay.textContent = score;
            }
        });

        startGame();
    </script>
</body>
</html>
