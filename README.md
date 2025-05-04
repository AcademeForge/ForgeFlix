
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>RunXtreme</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: linear-gradient(to bottom, #0f0c29, #302b63, #24243e);
    }
    canvas {
      display: block;
      margin: 0 auto;
      background: #111;
      border: 2px solid #fff;
    }
  </style>
</head>
<body>
  <canvas id="gameCanvas"></canvas>

  <script>
    const canvas = document.getElementById("gameCanvas");
    const ctx = canvas.getContext("2d");

    canvas.width = 800;
    canvas.height = 400;

    let gameSpeed = 5;
    let gravity = 1;
    let startTime = Date.now();

    class Player {
      constructor() {
        this.x = 50;
        this.y = canvas.height - 60;
        this.width = 40;
        this.height = 50;
        this.dy = 0;
        this.jumpPower = -15;
        this.onGround = true;
      }

      draw() {
        ctx.fillStyle = "#00f2ff";
        ctx.fillRect(this.x, this.y, this.width, this.height);
      }

      update() {
        this.y += this.dy;
        if (this.y + this.height < canvas.height) {
          this.dy += gravity;
          this.onGround = false;
        } else {
          this.dy = 0;
          this.y = canvas.height - this.height;
          this.onGround = true;
        }
        this.draw();
      }

      jump() {
        if (this.onGround) {
          this.dy = this.jumpPower;
        }
      }
    }

    class Obstacle {
      constructor() {
        this.width = 40;
        this.height = Math.random() * 40 + 20;
        this.x = canvas.width;
        this.y = canvas.height - this.height;
      }

      draw() {
        ctx.fillStyle = "#ff2e63";
        ctx.fillRect(this.x, this.y, this.width, this.height);
      }

      update() {
        this.x -= gameSpeed;
        this.draw();
      }
    }

    const player = new Player();
    let obstacles = [];
    let frame = 0;

    function handleObstacles() {
      if (frame % 100 === 0) {
        obstacles.push(new Obstacle());
      }

      for (let i = 0; i < obstacles.length; i++) {
        obstacles[i].update();

        // collision detection
        if (
          player.x < obstacles[i].x + obstacles[i].width &&
          player.x + player.width > obstacles[i].x &&
          player.y < obstacles[i].y + obstacles[i].height &&
          player.y + player.height > obstacles[i].y
        ) {
          alert("Game Over!");
          document.location.reload();
        }
      }
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      player.update();
      handleObstacles();

      const timeElapsed = (Date.now() - startTime) / 1000;
      if (timeElapsed > 60 && gameSpeed < 10) {
        gameSpeed += 0.01;
      }

      frame++;
      requestAnimationFrame(animate);
    }

    window.addEventListener("keydown", (e) => {
      if (e.code === "Space") {
        player.jump();
      }
    });

    animate();
  </script>
</body>
</html>