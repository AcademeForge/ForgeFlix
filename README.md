
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
    3: [
        { question: "What is 5 x 5?", options: ["10", "20", "25", "30"], answer: "25" },
        { question: "Who discovered America?", options: ["Christopher Columbus", "Albert Einstein", "Isaac Newton", "Alexander Graham Bell"], answer: "Christopher Columbus" },
        { question: "What is the capital of France?", options: ["Berlin", "Madrid", "Paris", "Rome"], answer: "Paris" },
        { question: "Which is the longest river in the world?", options: ["Amazon", "Nile", "Yangtze", "Mississippi"], answer: "Nile" },
        { question: "Who is the author of 'Harry Potter'?", options: ["J.K. Rowling", "J.R.R. Tolkien", "George Orwell", "Mark Twain"], answer: "J.K. Rowling" }
    ],
    4: [
        { question: "What is 12 x 8?", options: ["96", "88", "72", "104"], answer: "96" },
        { question: "What is the square root of 64?", options: ["6", "7", "8", "9"], answer: "8" },
        { question: "Which country is known as the Land of the Rising Sun?", options: ["India", "Japan", "China", "Thailand"], answer: "Japan" },
        { question: "Who was the first President of the United States?", options: ["Abraham Lincoln", "George Washington", "Thomas Jefferson", "John Adams"], answer: "George Washington" },
        { question: "What is the chemical symbol for water?", options: ["H2O", "CO2", "O2", "H2O2"], answer: "H2O" }
    ],
    5: [
        { question: "What is 14 x 9?", options: ["128", "132", "142", "126"], answer: "126" },
        { question: "Which planet is known as the Red Planet?", options: ["Earth", "Mars", "Jupiter", "Saturn"], answer: "Mars" },
        { question: "Who invented the light bulb?", options: ["Nikola Tesla", "Thomas Edison", "Albert Einstein", "Isaac Newton"], answer: "Thomas Edison" },
        { question: "Which is the largest mammal?", options: ["Elephant", "Blue Whale", "Giraffe", "Shark"], answer: "Blue Whale" },
        { question: "Who wrote 'The Diary of a Young Girl'?", options: ["Anne Frank", "Charlotte Brontë", "Jane Austen", "Harper Lee"], answer: "Anne Frank" }
    ],
    6: [
        { question: "What is the value of pi to two decimal places?", options: ["3.14", "3.15", "3.16", "3.12"], answer: "3.14" },
        { question: "What is the boiling point of water in Celsius?", options: ["100", "90", "80", "110"], answer: "100" },
        { question: "Who painted the Mona Lisa?", options: ["Pablo Picasso", "Leonardo da Vinci", "Vincent van Gogh", "Claude Monet"], answer: "Leonardo da Vinci" },
        { question: "What is the tallest mountain in the world?", options: ["Mount Kilimanjaro", "Mount Everest", "Mount Fuji", "Mount McKinley"], answer: "Mount Everest" },
        { question: "Who is known as the father of modern physics?", options: ["Albert Einstein", "Isaac Newton", "Niels Bohr", "Max Planck"], answer: "Albert Einstein" }
    ],
    7: [
        { question: "What is the capital of Japan?", options: ["Tokyo", "Seoul", "Beijing", "Bangkok"], answer: "Tokyo" },
        { question: "What is the chemical symbol for gold?", options: ["Au", "Ag", "Cu", "Fe"], answer: "Au" },
        { question: "Who is the author of 'The Hobbit'?", options: ["J.K. Rowling", "J.R.R. Tolkien", "C.S. Lewis", "George R.R. Martin"], answer: "J.R.R. Tolkien" },
        { question: "What is the largest country by land area?", options: ["United States", "China", "Russia", "Canada"], answer: "Russia" },
        { question: "Which element has the atomic number 6?", options: ["Oxygen", "Carbon", "Nitrogen", "Hydrogen"], answer: "Carbon" }
    ],
    8: [
        { question: "What is the value of 2^10?", options: ["1024", "512", "2048", "256"], answer: "1024" },
        { question: "Who developed the theory of relativity?", options: ["Isaac Newton", "Albert Einstein", "Niels Bohr", "Galileo Galilei"], answer: "Albert Einstein" },
        { question: "What is the capital of Italy?", options: ["Rome", "Paris", "Berlin", "Madrid"], answer: "Rome" },
        { question: "Which gas do plants absorb from the atmosphere for photosynthesis?", options: ["Oxygen", "Carbon Dioxide", "Nitrogen", "Hydrogen"], answer: "Carbon Dioxide" },
        { question: "Who was the first man to walk on the moon?", options: ["Yuri Gagarin", "Neil Armstrong", "Buzz Aldrin", "John Glenn"], answer: "Neil Armstrong" }
    ],
    9: [
        { question: "What is the value of 9^2?", options: ["81", "72", "63", "99"], answer: "81" },
        { question: "What is the capital of Australia?", options: ["Canberra", "Sydney", "Melbourne", "Brisbane"], answer: "Canberra" },
        { question: "Who wrote 'Romeo and Juliet'?", options: ["William Shakespeare", "Charles Dickens", "Jane Austen", "Leo Tolstoy"], answer: "William Shakespeare" },
        { question: "What is the chemical symbol for sodium?", options: ["Na", "K", "Ca", "Mg"], answer: "Na" },
        { question: "Which element is the main component of natural gas?", options: ["Hydrogen", "Carbon", "Oxygen", "Methane"], answer: "Methane" }
    ],
    10: [
        { question: "What is the derivative of x^2?", options: ["2x", "x^2", "2", "x"], answer: "2x" },
        { question: "Who is known as the father of modern chemistry?", options: ["Dmitri Mendeleev", "Marie Curie", "Robert Boyle", "John Dalton"], answer: "Dmitri Mendeleev" },
        { question: "What is the capital of Russia?", options: ["Moscow", "St. Petersburg", "Kiev", "Warsaw"], answer: "Moscow" },
        { question: "What is the chemical formula for methane?", options: ["CH4", "C2H6", "CO2", "C3H8"], answer: "CH4" },
        { question: "Who was the first president of India?", options: ["Jawaharlal Nehru", "Dr. Rajendra Prasad", "Indira Gandhi", "Sardar Patel"], answer: "Dr. Rajendra Prasad" }
    ]
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