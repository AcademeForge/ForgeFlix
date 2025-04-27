
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>AcademeForge TV</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      display: flex;
      min-height: 100vh;
      background: #f4f4f4;
    }

    .sidebar {
      background-color: #202020;
      width: 250px;
      height: 100vh;
      position: fixed;
      top: 0;
      left: 0;
      overflow-y: auto;
      transition: transform 0.3s ease;
    }

    .sidebar ul {
      list-style: none;
      padding: 20px 0;
    }

    .sidebar ul li {
      padding: 15px 20px;
    }

    .sidebar ul li a {
      text-decoration: none;
      color: white;
      font-size: 18px;
      display: block;
    }

    .sidebar ul li:hover {
      background: #383838;
    }

    .main-content {
      margin-left: 250px;
      padding: 20px;
      width: 100%;
    }

    .toggle-btn {
      display: none;
      position: absolute;
      top: 10px;
      left: 10px;
      background: #202020;
      color: white;
      padding: 10px;
      cursor: pointer;
      z-index: 1000;
      border: none;
    }

    h2 {
      margin: 20px 0;
      text-align: center;
    }

    .video-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
      margin-top: 20px;
    }

    .video-item iframe {
      width: 300px;
      height: 200px;
    }

    footer {
      text-align: center;
      padding: 20px;
      background: #202020;
      color: white;
      margin-top: 40px;
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      .sidebar {
        transform: translateX(-100%);
      }

      .sidebar.active {
        transform: translateX(0);
      }

      .main-content {
        margin-left: 0;
      }

      .toggle-btn {
        display: block;
      }
    }
  </style>
</head>
<body>

<button class="toggle-btn" onclick="toggleSidebar()">☰</button>

<div class="sidebar" id="sidebar">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">Motivation</a></li>
    <li><a href="#">Study Tips</a></li>
    <li><a href="#">AST Updates</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</div>

<div class="main-content">
  <h2>Featured Videos</h2>
  <div class="video-container">

    <!-- YouTube Long Videos -->
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed/Xb6AXnZTbF8" frameborder="0" allowfullscreen></iframe>
    </div>
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed/Tg19heqR7Mg" frameborder="0" allowfullscreen></iframe>
    </div>
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed/uBc0GYZV7yk" frameborder="0" allowfullscreen></iframe>
    </div>

    <!-- YouTube Shorts -->
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed/MGJLNrh5Af4" frameborder="0" allowfullscreen></iframe>
    </div>
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed/ZbACYMkPLjI" frameborder="0" allowfullscreen></iframe>
    </div>

    <!-- Instagram Reels -->
    <div class="video-item">
      <blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/reel/DIonRVKyunG/?igsh=dnA1OTZjdWRmY2N2" data-instgrm-version="14" style="background:#FFF; border:0; margin:0; padding:0;" ></blockquote>
    </div>
    <div class="video-item">
      <blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/reel/DI3eVacSxQG/?igsh=eDZsMTlndWVqdzRx" data-instgrm-version="14" style="background:#FFF; border:0; margin:0; padding:0;" ></blockquote>
    </div>

    <!-- Twitter Posts -->
    <div class="video-item">
      <blockquote class="twitter-tweet">
        <a href="https://x.com/AcademeForge/status/1913901410950713651?t=T3O1cGHp3FIxhy5vq9yc8w&s=19"></a>
      </blockquote>
    </div>
    <div class="video-item">
      <blockquote class="twitter-tweet">
        <a href="https://x.com/AcademeForge/status/1914317258240782497?t=T3O1cGHp3FIxhy5vq9yc8w&s=19"></a>
      </blockquote>
    </div>

  </div>

  <h2>Community Post</h2>
  <div class="video-container">
    <div class="video-item">
      <iframe src="https://www.youtube.com/embed?listType=playlist&list=UUkxcumD9empruyZDu2Q7idRTr9VJJApNIG8" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>

</div>

<footer>
  &copy; 2025 AcademeForge. All rights reserved.
</footer>

<!-- JavaScript -->
<script>
  function toggleSidebar() {
    document.getElementById('sidebar').classList.toggle('active');
  }
</script>

<!-- Instagram Embedding Script -->
<script async src="//www.instagram.com/embed.js"></script>

<!-- Twitter Embedding Script -->
<script async src="https://platform.twitter.com/widgets.js"></script>

</body>
</html>