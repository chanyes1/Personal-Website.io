# Personal-Website.io
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Change Background and Images</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #778180;
            background-size: cover;
            transition: opacity 0.5s ease, background 0.5s ease;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }

        #container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100%;
        }

        .rectangle {
            width: 400px;
            height: 87%;
            background-color: rgb(43, 39, 39);
            color: white;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 10px;
            box-sizing: border-box;
            font-size: 20px;
            position: relative;
            overflow: hidden;
        }

        #center-image {
            height: 100vh;
            width: auto;
            transition: opacity 0.5s ease;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            position: absolute;
            z-index: 100;
        }

        #start-button {
            top: 20px;
            right: 20px;
        }

        #change-image-button {
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
            /* Initially hidden */
        }

        #link-button {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 14px;
            display: none;
            /* Initially hidden */
        }

        h1 {
            position: absolute;
            top: 60px;
            z-index: 100;
        }

        .hidden {
            display: none;
        }

        .loading-spinner {
            border: 8px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 8px solid #3498db;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            display: none;
        }

        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }

            100% {
                transform: rotate(360deg);
            }
        }
    </style>
</head>

<body>

    <h1> </h1>
    <button id="start-button" onclick="start()">Start</button>

    <div id="container">
        <!-- Left Rectangle for typing text -->
        <div class="rectangle" id="left-rectangle">
            <div id="typing-text"></div>
            <button id="change-image-button" onclick="changeImage()">Change Image</button>
        </div>

        <!-- Center Image -->
        <img id="center-image" src="Gray.png" alt="Center Image">

        <!-- Right Rectangle for loading animation -->
        <div class="rectangle" id="right-rectangle">
            <div id="initial-text">
                Please Press The Button<br>
                <h6>1st site I made :)</h6>
            </div>
            <div id="loading-text" class="hidden">Loading</div>
            <div class="loading-spinner" id="loading-spinner"></div>
            <a href="https://www.facebook.com/yves.chands" id="link-button" target="_blank">Visit My Website</a>
        </div>
    </div>

    <script>
        let typingInterval;
        let centerImageIndex = 0;
        const centerImages = ["Gray.png", "Colored me.png", "real.jpg"]; // Add paths to images here

        function start() {
            // Hide the button
            document.getElementById('start-button').classList.add('hidden');

            // Change center image initially
            changeImage(); // Change to the first image in the array

            // Change background image
            document.body.style.backgroundImage = "url('Space.png')";  // Replace with your background image path
            document.body.style.backgroundColor = "transparent";

            // Change center image
            const centerImage = document.getElementById('center-image');
            centerImage.style.opacity = 0; // Fade out the image
            setTimeout(() => {
                centerImage.src = centerImages[centerImageIndex]; // Set the first image
                centerImage.style.opacity = 1; // Fade in the new image
            }, 500); // Wait for the fade out to complete before changing the image

            // Show loading spinner and start auto-typing in the left rectangle
            document.getElementById('loading-spinner').style.display = 'block';
            document.getElementById('loading-text').classList.remove('hidden');
            document.getElementById('initial-text').classList.add('hidden');
            autoTypeText("typing-text", "Hello, my name is Yves Chandler Castillo, my nickname is Yevyev, as of 2024, I am a 1st year college student of Perpetual Help Dalta - Molino Campus. Studying Computer Science, specialized in Data Science.");
        }

        // Auto-typing function for the left rectangle
        function autoTypeText(elementId, text) {
            const element = document.getElementById(elementId);
            let index = 0;
            element.innerHTML = ''; // Clear existing content

            typingInterval = setInterval(() => {
                if (index < text.length) {
                    element.innerHTML += text[index];
                    index++;
                } else {
                    clearInterval(typingInterval); // Stop typing when complete
                    setTimeout(() => {
                        stopLoading(); // Stop the loading animation
                        showAdditionalElements(); // Show the additional elements
                    }, 500); // Delay to ensure typing effect finishes
                }
            }, 100); // Typing speed: 100ms per character
        }

        // Stop the loading animation and update the right rectangle
        function stopLoading() {
            document.getElementById('loading-spinner').style.display = 'none';
            document.getElementById('loading-text').classList.add('hidden');
            document.getElementById('initial-text').innerHTML = "My philosophy in life is to not take things too seriously, I will do my best, try my hardest and most of all, ignite my passion, like a flame both bright and beautiful, I will be fabulous, truly. Rest is obviously in there by default, for I am in dire need of being healthy. I really like the concept of Computer Science, the fact that we can simulate things is all I need to see to truly be in love by it, an endless path with endless crossroads similar to maths. I may be a beginner, but not for long.";
            document.getElementById('initial-text').classList.remove('hidden'); // Ensure the text is visible
        }

        // Show additional elements after typing is complete
        function showAdditionalElements() {
            document.getElementById('change-image-button').style.display = 'block';
            document.getElementById('link-button').style.display = 'block';
        }

        // Change center image
        function changeImage() {
            centerImageIndex = (centerImageIndex + 1) % centerImages.length;
            document.getElementById('center-image').src = centerImages[centerImageIndex];
        }
    </script>

</body>

</html>
