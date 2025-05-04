
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class 1 Quiz Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        .container {
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #333;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .question {
            font-size: 18px;
            margin: 20px 0;
        }

        .option {
            margin: 10px;
        }

        .scoreboard {
            margin-top: 20px;
        }

        .scoreboard table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .scoreboard table, th, td {
            border: 1px solid #ddd;
        }

        th, td {
            padding: 10px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome to the Class 1 Quiz Game</h1>

        <div id="intro">
            <label for="name">Enter your name:</label>
            <input type="text" id="name" placeholder="Your Name">
            <button onclick="startGame()">Start Game</button>
        </div>

        <div id="quiz" style="display: none;">
            <div class="question" id="questionText"></div>
            <div id="options"></div>
            <button onclick="nextQuestion()" id="nextBtn" style="display: none;">Next Question</button>
        </div>

        <div id="gameOver" style="display: none;">
            <h2>Game Over!</h2>
            <p>Your final score is: <span id="finalScore"></span></p>
            <button onclick="restartGame()">Play Again</button>
        </div>

        <div class="scoreboard" style="display: none;">
            <h2>Top Scores</h2>
            <table id="scoreboardTable">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Score</th>
                    </tr>
                </thead>
                <tbody id="scoreboardBody"></tbody>
            </table>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "What is 2 + 2?",
                options: ["3", "4", "5", "6"],
                answer: "4"
            },
            {
                question: "What is 3 + 3?",
                options: ["5", "6", "7", "8"],
                answer: "6"
            },
            {
                question: "What is the color of the sky?",
                options: ["Red", "Blue", "Green", "Yellow"],
                answer: "Blue"
            },
            {
                question: "Which is the smallest animal?",
                options: ["Elephant", "Cat", "Dog", "Ant"],
                answer: "Ant"
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;
        let playerName = '';

        // Start game function
        function startGame() {
            playerName = document.getElementById("name").value.trim();
            if (!playerName) {
                alert("Please enter your name!");
                return;
            }
            document.getElementById("intro").style.display = "none";
            document.getElementById("quiz").style.display = "block";
            loadQuestion();
        }

        // Load question
        function loadQuestion() {
            const currentQuestion = questions[currentQuestionIndex];
            document.getElementById("questionText").textContent = currentQuestion.question;
            const optionsDiv = document.getElementById("options");
            optionsDiv.innerHTML = '';

            currentQuestion.options.forEach(option => {
                const button = document.createElement("button");
                button.textContent = option;
                button.classList.add("option");
                button.onclick = function () { checkAnswer(option); };
                optionsDiv.appendChild(button);
            });
        }

        // Check if the answer is correct
        function checkAnswer(selectedOption) {
            const currentQuestion = questions[currentQuestionIndex];
            if (selectedOption === currentQuestion.answer) {
                score++;
            }
            document.getElementById("nextBtn").style.display = "block";
        }

        // Go to the next question
        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                loadQuestion();
                document.getElementById("nextBtn").style.display = "none";
            } else {
                endGame();
            }
        }

        // End game and display results
        function endGame() {
            document.getElementById("quiz").style.display = "none";
            document.getElementById("gameOver").style.display = "block";
            document.getElementById("finalScore").textContent = score;
            saveScore();
            showScores();
        }

        // Save score to localStorage
        function saveScore() {
            let scores = JSON.parse(localStorage.getItem("scores")) || [];
            scores.push({ name: playerName, score: score });
            localStorage.setItem("scores", JSON.stringify(scores));
        }

        // Show scores on the scoreboard
        function showScores() {
            const scores = JSON.parse(localStorage.getItem("scores")) || [];
            scores.sort((a, b) => b.score - a.score);
            const scoreboardBody = document.getElementById("scoreboardBody");
            scoreboardBody.innerHTML = '';
            scores.forEach((entry) => {
                const row = document.createElement("tr");
                row.innerHTML = `<td>${entry.name}</td><td>${entry.score}</td>`;
                scoreboardBody.appendChild(row);
            });
            document.getElementById("scoreboard").style.display = "block";
        }

        // Restart the game
        function restartGame() {
            currentQuestionIndex = 0;
            score = 0;
            document.getElementById("gameOver").style.display = "none";
            document.getElementById("intro").style.display = "block";
        }
    </script>
</body>
</html>