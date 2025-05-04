from flask import Flask, render_template_string, request, redirect, url_for
import random
import csv

app = Flask(__name__)

# Sample questions for Class 1 students (you can extend this list)
questions = [
    {"question": "What is 2 + 2?", "options": ["3", "4", "5", "6"], "answer": "4"},
    {"question": "What is 3 + 3?", "options": ["5", "6", "7", "8"], "answer": "6"},
    {"question": "What is the color of the sky?", "options": ["Red", "Blue", "Green", "Yellow"], "answer": "Blue"},
    {"question": "Which is the smallest animal?", "options": ["Elephant", "Cat", "Dog", "Ant"], "answer": "Ant"}
]

# Function to load the scoreboard from CSV file
def load_scores():
    scores = []
    try:
        with open('scores.csv', mode='r') as file:
            csv_reader = csv.reader(file)
            for row in csv_reader:
                scores.append({"name": row[0], "score": int(row[1])})
    except FileNotFoundError:
        pass
    return scores

# Function to save a score to the CSV file
def save_score(name, score):
    with open('scores.csv', mode='a', newline='') as file:
        csv_writer = csv.writer(file)
        csv_writer.writerow([name, score])

@app.route('/')
def home():
    return render_template_string('''
<!DOCTYPE html>
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

        form input[type="text"] {
            padding: 10px;
            font-size: 16px;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
        }

        form button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        form button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome to the Class 1 Quiz Game</h1>
        <form method="POST" action="/quiz">
            <label for="name">Enter your name:</label>
            <input type="text" id="name" name="name" required>
            <button type="submit">Start Game</button>
        </form>
    </div>
</body>
</html>
    ''')

@app.route('/quiz', methods=['GET', 'POST'])
def quiz():
    if request.method == 'POST':
        player_name = request.form['name']
        return redirect(url_for('play_quiz', player_name=player_name))
    return redirect(url_for('home'))

@app.route('/quiz/<player_name>', methods=['GET', 'POST'])
def play_quiz(player_name):
    score = 0
    if request.method == 'POST':
        # Get the answer from the form
        question_index = int(request.form['question_index'])
        answer = request.form['answer']
        correct_answer = questions[question_index]['answer']

        # Check if the answer is correct
        if answer == correct_answer:
            score += 1

        # Get next question
        next_question_index = question_index + 1

        if next_question_index < len(questions):
            return render_template_string('''
<!DOCTYPE html>
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

        form input[type="text"] {
            padding: 10px;
            font-size: 16px;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
        }

        form button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        form button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome {{ player_name }}</h1>
        <p>Question {{ question_index + 1 }}: {{ question['question'] }}</p>
        <form method="POST">
            <input type="hidden" name="question_index" value="{{ question_index }}">
            {% for option in question['options'] %}
                <label>
                    <input type="radio" name="answer" value="{{ option }}" required>{{ option }}
                </label><br>
            {% endfor %}
            <button type="submit">Next</button>
        </form>
        <p>Score: {{ score }}</p>
    </div>
</body>
</html>
            ''', question=questions[next_question_index], score=score, player_name=player_name, question_index=next_question_index)
        else:
            save_score(player_name, score)  # Save score when quiz finishes
            return redirect(url_for('scoreboard'))

    else:
        question_index = 0
        return render_template_string('''
<!DOCTYPE html>
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

        form input[type="text"] {
            padding: 10px;
            font-size: 16px;
            margin: 10px 0;
            width: 80%;
            max-width: 300px;
        }

        form button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

        form button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome {{ player_name }}</h1>
        <p>Question {{ question_index + 1 }}: {{ question['question'] }}</p>
        <form method="POST">
            <input type="hidden" name="question_index" value="{{ question_index }}">
            {% for option in question['options'] %}
                <label>
                    <input type="radio" name="answer" value="{{ option }}" required>{{ option }}
                </label><br>
            {% endfor %}
            <button type="submit">Next</button>
        </form>
        <p>Score: {{ score }}</p>
    </div>
</body>
</html>
        ''', question=questions[question_index], score=score, player_name=player_name, question_index=question_index)

@app.route('/scoreboard')
def scoreboard():
    scores = load_scores()
    scores.sort(key=lambda x: x['score'], reverse=True)  # Sort by score
    return render_template_string('''
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class 1 Quiz Game - Scoreboard</title>
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

        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        table, th, td {
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
        <h1>Top Scores</h1>
        <table>
            <thead>
                <tr>
                    <th>Rank</th>
                    <th>Name</th>
                    <th>Score</th>
                </tr>
            </thead>
            <tbody>
                {% for idx, score in enumerate(scores) %}
                    <tr>
                        <td>{{ idx + 1 }}</td>
                        <td>{{ score.name }}</td>
                        <td>{{ score.score }}</td>
                    </tr>
                {% endfor %}
            </tbody>
        </table>
        <a href="/">Go to Home</a>
    </div>
</body>
</html>
    ''')

if __name__ == "__main__":
    app.run(debug=True)