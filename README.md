
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AcademeForge - Motivational & Study Videos</title>
    
    <!-- Embedded CSS -->
    <style>
        /* Basic Styling */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        nav {
            background-color: #333;
            padding: 10px 0;
            text-align: center;
        }

        nav ul {
            list-style-type: none;
        }

        nav ul li {
            display: inline;
            margin: 0 15px;
        }

        nav ul li a {
            color: white;
            text-decoration: none;
            font-size: 18px;
        }

        h2 {
            text-align: center;
            margin-top: 20px;
            color: #333;
        }

        .video-container {
            text-align: center;
            margin: 20px 0;
        }

        .video-gallery {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            margin-top: 20px;
        }

        .video-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }

        .video-item {
            width: 300px;
            height: auto;
        }

        iframe {
            width: 100%;
            height: 200px;
        }

        blockquote {
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <!-- Navigation Bar -->
    <nav>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">Motivation</a></li>
            <li><a href="#">Study Tips</a></li>
            <li><a href="#">AST Updates</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>

    <!-- Featured Video -->
    <section class="featured-video">
        <h2>Featured Video: Motivation for Success</h2>
        <div class="video-container">
            <!-- YouTube Embed -->
            <iframe width="560" height="315" src="https://www.youtube.com/embed/{video_id}?autoplay=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
        </div>
    </section>

    <!-- Video Gallery -->
    <section class="video-gallery">
        <h2>Video Gallery</h2>
        <div class="video-grid">
            <!-- Embed YouTube or Instagram -->
            <div class="video-item">
                <iframe width="300" height="200" src="https://youtu.be/Xb6AXnZTbF8?si=3YlMcKCl3QEsXAGL" frameborder="0" allowfullscreen></iframe>
            </div>
            <div class="video-item">
                <blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/p/{post_id}/" data-instgrm-version="12"></blockquote>
                <script async src="//www.instagram.com/embed.js"></script>
            </div>
            <!-- More video items can go here -->
        </div>
    </section>

    <!-- Embedded JavaScript -->
    <script>
        // You can add future interactive features here
        console.log("AcademeForge Website Loaded!");

        // You can also use this to dynamically load video content if desired
    </script>

</body>
</html>
