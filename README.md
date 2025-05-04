
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>AcademeForge: Indian Bike Rush</title>
  <style>
    body {
      margin: 0;
      background: #202020;
      font-family: sans-serif;
      overflow: hidden;
    }
    canvas {
      display: block;
      margin: auto;
      background: linear-gradient(to bottom, #444, #111);
    }
  </style>
</head>
<body>
<canvas id="gameCanvas"></canvas>
<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
canvas.width = 800;
canvas.height = 500;

let bikeSpeed = 4;
let traffic = [];
let keys = {};

const player = {
  x: 100,
  y: canvas.height / 2 - 25,
  width: 40,
  height: 50,
  color: "#00e676",
  draw() {
    ctx.fillStyle = this.color;
    ctx.fillRect(this.x, this.y, this.width, this.height);
    ctx.font = "16px Arial";
    ctx.fillStyle = "#fff";
    ctx.fillText("AcademeForge", this.x - 20, this.y - 10);
  },
  update() {
    if (keys["ArrowUp"] && this.y > 0) this.y -= 5;
    if (keys["ArrowDown"] && this.y + this.height < canvas.height) this.y += 5;
    this.draw();
  }
};

class Car {
  constructor() {
    this.x = canvas.width + Math.random() * 100;
    this.y = Math.random() * (canvas.height - 50);
    this.width = 60;
    this.height = 40;
    this.speed = bikeSpeed + Math.random() * 2;
    this.color = "#ff3d00";
  }

  draw() {
    ctx.fillStyle = this.color;
    ctx.fillRect(this.x, this.y, this.width, this.height);
  }

  update() {
    this.x -= this.speed;
    this.draw();
  }
}

function spawnTraffic() {
  if (Math.random() < 0.03) {
    traffic.push(new Car());
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

let frame = 0;
let startTime = Date.now();

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  player.update();
  spawnTraffic();

  for (let i = traffic.length - 1; i >= 0; i--) {
    const car = traffic[i];
    car.update();
    if (checkCollision(player, car)) {
      alert("Bike Crashed! Game Over.");
      document.location.reload();
    }
    if (car.x + car.width < 0) traffic.splice(i, 1);
  }

  const timeElapsed = (Date.now() - startTime) / 1000;
  if (timeElapsed > 30) bikeSpeed = 6;
  if (timeElapsed > 60) bikeSpeed = 8;

  requestAnimationFrame(animate);
}

window.addEventListener("keydown", (e) => {
  keys[e.key] = true;
});
window.addEventListener("keyup", (e) => {
  keys[e.key] = false;
});

animate();
</script>
</body>
</html>