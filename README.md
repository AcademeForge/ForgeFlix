
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AcademeForge - Motivational & Study Videos</title>

    <!-- Embedded CSS -->
    <style>
        /* Reset some basic styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            display: flex;
            min-height: 100vh;
        }

        /* Sidebar Styling */
        .sidebar {
            background-color: #111;
            color: white;
            width: 240px;
            padding-top: 20px;
            position: fixed;
            height: 100%;
            top: 0;
        }

        .sidebar ul {
            list-style-type: none;
        }

        .sidebar ul li {
            padding: 20px;
            text-align: center;
        }

        .sidebar ul li a {
            color: white;
            text-decoration: none;
            font-size: 18px;
        }

        .sidebar ul li:hover {
            background-color: #444;
        }

        /* Main content area */
        .main-content {
            margin-left: 260px;
            width: 100%;
            padding: 20px;
        }

        h2 {
            text-align: center;
            color: #333;
        }

        /* Video Container */
        .video-container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
            margin-top: 20px;
        }

        .video-item {
            width: 300px;
            height: auto;
        }

        iframe {
            width: 100%;
            height: 200px;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 20px;
            background-color: #333;
            color: white;
            position: fixed;
            width: 100%;
            bottom: 0;
        }
    </style>
</head>
<body>

    <!-- Sidebar -->
    <div class="sidebar">
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">Motivation</a></li>
            <li><a href="#">Study Tips</a></li>
            <li><a href="#">AST Updates</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </div>

    <!-- Main Content -->
    <div class="main-content">
        <!-- Featured Video -->
        <section class="featured-video">
            <h2>Featured Video: Motivation for Success</h2>
            <div class="video-container">
                <!-- YouTube Embed -->
                <iframe src="https://www.youtube.com/embed/Xb6AXnZTbF8?autoplay=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
            </div>
        </section>

        <!-- Video Gallery -->
        <section class="video-gallery">
            <h2>Video Gallery</h2>
            <div class="video-container">
                <!-- YouTube Shorts -->
                <div class="video-item">
                    <iframe src="https://youtube.com/shorts/MGJLNrh5Af4?si=xZHNtAJv0TCFmxxO" frameborder="0" allowfullscreen></iframe>
                </div>
                <div class="video-item">
                    <iframe src="https://youtube.com/shorts/ZbACYMkPLjI?si=UlWTdFcCKee2xyCS" frameborder="0" allowfullscreen></iframe>
                </div>
                <!-- Instagram Reels -->
                <div class="video-item">
                    <blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/reel/DIonRVKyunG/?igsh=dnA1OTZjdWRmY2N2" data-instgrm-version="12"></blockquote>
                    <script async src="//www.instagram.com/embed.js"></script>
                </div>
                <div class="video-item">
                    <blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/reel/DI3eVacSxQG/?igsh=eDZsMTlndWVqdzRx" data-instgrm-version="12"></blockquote>
                    <script async src="//www.instagram.com/embed.js"></script>
                </div>
                <!-- Twitter Posts -->
                <div class="video-item">
                    <blockquote class="twitter-tweet">
                        <a href="https://x.com/AcademeForge/status/1913901410950713651?t=T3O1cGHp3FIxhy5vq9yc8w&s=19"></a>
                    </blockquote>
                    <script async src="https://platform.twitter.com/widgets.js"></script>
                </div>
                <div class="video-item">
                    <blockquote class="twitter-tweet">
                        <a href="https://x.com/AcademeForge/status/1914317258240782497?t=T3O1cGHp3FIxhy5vq9yc8w&s=19"></a>
                    </blockquote>
                    <script async src="https://platform.twitter.com/widgets.js"></script>
                </div>
                <!-- More Video Items and Links can go here -->
            </div>
        </section>
    </div>

    <!-- Footer -->
    <footer>
        <p>&copy; 2025 AcademeForge. All Rights Reserved.</p>
    </footer>

</body>
</html>