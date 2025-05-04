
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class Quiz Game</title>
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
        <h1>Welcome to the Class Quiz Game</h1>

        <div id="intro">
            <label for="name">Enter your name:</label>
            <input type="text" id="name" placeholder="Your Name">
            <label for="classSelect">Select your class:</label>
            <select id="classSelect">
                <option value="1">Class 1</option>
                <option value="2">Class 2</option>
                <option value="3">Class 3</option>
                <option value="4">Class 4</option>
                <option value="5">Class 5</option>
                <option value="6">Class 6</option>
                <option value="7">Class 7</option>
                <option value="8">Class 8</option>
                <option value="9">Class 9</option>
                <option value="10">Class 10</option>
            </select>
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
        const questions = {
            1: [
                { question: "What is 2 + 2?", options: ["3", "4", "5", "6"], answer: "4" },
                { question: "What color is the sky?", options: ["Red", "Blue", "Green", "Yellow"], answer: "Blue" },
                { question: "Which is the smallest animal?", options: ["Elephant", "Cat", "Dog", "Ant"], answer: "Ant" },
                { question: "What is 1 + 1?", options: ["1", "2", "3", "4"], answer: "2" }
            ],
            2: [
                { question: "What is 3 + 5?", options: ["7", "8", "9", "10"], answer: "8" },
                { question: "What is the capital of India?", options: ["Delhi", "Mumbai", "Kolkata", "Chennai"], answer: "Delhi" },
                { question: "Which animal barks?", options: ["Cat", "Lion", "Dog", "Tiger"], answer: "Dog" },
                { question: "Which is the largest planet?", options: ["Earth", "Mars", "Jupiter", "Saturn"], answer: "Jupiter" }
            ],
            // Add questions for classes 3 to 10 here...
            // Example: Class 3, 4, etc.
            // You can add 50 questions for each class as per your need.
        };

        let currentQuestionIndex = 0;
        let score = 0;
        let playerName = '';
        let selectedClass = 1;

        // Start game function
        function startGame() {
            playerName = document.getElementById("name").value.trim();
            selectedClass = parseInt(document.getElementById("classSelect").value);
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
            const currentQuestion = questions[selectedClass][currentQuestionIndex];
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
            const currentQuestion = questions[selectedClass][currentQuestionIndex];
            if (selectedOption === currentQuestion.answer) {
                score++;
            }
            document.getElementById("nextBtn").style.display = "block";
        }

        // Go to the next question
        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions[selectedClass].length) {
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