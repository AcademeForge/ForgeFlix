
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>AcademeForge Indian Bike Racer</title>
  <style>
    body {
      margin: 0;
      background: #111;
      font-family: Arial, sans-serif;
    }
    canvas {
      display: block;
      margin: 0 auto;
      background: url('https://i.imgur.com/jl3ZtR0.jpg') repeat-x;
      background-size: cover;
    }
    #scoreBoard {
      position: absolute;
      top: 10px;
      left: 20px;
      color: #fff;
      font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>
<div id="scoreBoard">Score: 0</div>
<canvas id="gameCanvas"></canvas>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
canvas.width = 800;
canvas.height = 500;

let keys = {};
let gameSpeed = 5;
let traffic = [];
let score = 0;
let nitroActive = false;
let nitroTimer = 0;

// Load Images
const bikeImg = new Image();
bikeImg.src = 'https://i.imgur.com/qD4Z8yk.png'; // Bike

const carImg = new Image();
carImg.src = 'https://i.imgur.com/5WEdMZ3.png'; // Car

// Load Sounds
const crashSound = new Audio('https://assets.mixkit.co/active_storage/sfx/1006/1006-preview.mp3');
const nitroSound = new Audio('https://assets.mixkit.co/active_storage/sfx/222/222-preview.mp3');
nitroSound.volume = 0.5;

const player = {
  x: 100,
  y: 200,
  width: 100,
  height: 50,
  draw() {
    ctx.drawImage(bikeImg, this.x, this.y, this.width, this.height);
  },
  update() {
    if (keys['ArrowUp'] && this.y > 0) this.y -= 6;
    if (keys['ArrowDown'] && this.y + this.height < canvas.height) this.y += 6;

    if (keys['Shift'] && !nitroActive) {
      activateNitro();
    }

    this.draw();
  }
};

class Car {
  constructor() {
    this.x = canvas.width + Math.random() * 100;
    this.y = Math.random() * (canvas.height - 60);
    this.width = 100;
    this.height = 50;
    this.speed = gameSpeed + Math.random() * 2;
  }

  draw() {
    ctx.drawImage(carImg, this.x, this.y, this.width, this.height);
  }

  update() {
    this.x -= this.speed;
    this.draw();
  }
}

function checkCollision(a, b) {
  return (
    a.x < b.x + b.width &&
    a.x + a.width > b.x &&
    a.y < b.y + b.height &&
    a.y + a.height > b.y
  );
}

function spawnTraffic() {
  if (Math.random() < 0.03) {
    traffic.push(new Car());
  }
}

function activateNitro() {
  nitroActive = true;
  gameSpeed += 4;
  nitroSound.play();
  nitroTimer = 100;

  const interval = setInterval(() => {
    nitroTimer--;
    if (nitroTimer <= 0) {
      gameSpeed -= 4;
      nitroActive = false;
      clearInterval(interval);
    }
  }, 30);
}

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  player.update();
  spawnTraffic();

  for (let i = traffic.length - 1; i >= 0; i--) {
    traffic[i].update();

    if (checkCollision(player, traffic[i])) {
      crashSound.play();
      alert('CRASH! Final Score: ' + score);
      document.location.reload();
    }

    if (traffic[i].x + traffic[i].width < 0) {
      traffic.splice(i, 1);
      score++;
      document.getElementById('scoreBoard').innerText = "Score: " + score;
    }
  }

  requestAnimationFrame(animate);
}

window.addEventListener('keydown', (e) => {
  keys[e.key] = true;
});

window.addEventListener('keyup', (e) => {
  keys[e.key] = false;
});

bikeImg.onload = () => animate();
</script>
</body>
</html>