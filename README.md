<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>1 Minute Countdown with Automatic Popups</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f3f4f6;
            color: #333;
        }
        #countdown {
            font-size: 2em;
            margin: 20px 0;
        }
        .popup {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgb(0,0,0);
            background-color: rgba(0,0,0,0.4);
            padding-top: 60px;
        }
        .popup-content {
            background-color: #fff;
            margin: 5% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
        }
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
        }
        .close:hover, .close:focus {
            color: black;
            text-decoration: none;
            cursor: pointer;
        }
    </style>
</head>
<body>

<h1>Countdown Timer</h1>
<div id="countdown"></div>

<div id="video1" class="popup">
  <div class="popup-content">
    <span class="close" onclick="hidePopup('video1')">&times;</span>
    <video id="video1Element" width="100%" controls>
      <source src="path/to/your/video1.mp4" type="video/mp4">
      Your browser does not support the video tag.
    </video>
  </div>
</div>

<div id="photo" class="popup">
  <div class="popup-content">
    <span class="close" onclick="hidePopup('photo')">&times;</span>
    <img src="path/to/your/photo.jpg" alt="Your Photo" width="100%">
  </div>
</div>

<div id="video2" class="popup">
  <div class="popup-content">
    <span class="close" onclick="hidePopup('video2')">&times;</span>
    <video id="video2Element" width="100%" controls>
      <source src="path/to/your/video2.mp4" type="video/mp4">
      Your browser does not support the video tag.
    </video>
  </div>
</div>

<script>
    const countdown = document.getElementById('countdown');
    const targetDate = new Date();
    targetDate.setMinutes(targetDate.getMinutes() + 1); // Countdown to 1 minute from now

    function updateCountdown() {
        const now = new Date();
        const timeRemaining = targetDate - now;

        const minutes = Math.floor((timeRemaining % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((timeRemaining % (1000 * 60)) / 1000);

        countdown.innerHTML = `${minutes}m ${seconds}s`;

        if (timeRemaining < 0) {
            clearInterval(interval);
            countdown.innerHTML = "EXPIRED";
            showSequence();
        }
    }

    const interval = setInterval(updateCountdown, 1000);

    function showPopup(id) {
        document.getElementById(id).style.display = "block";
    }

    function hidePopup(id) {
        document.getElementById(id).style.display = "none";
    }

    function showSequence() {
        showPopup('video1');
        const video1Element = document.getElementById('video1Element');
        video1Element.play();

        video1Element.onended = () => {
            hidePopup('video1');
            showPopup('photo');

            setTimeout(() => {
                hidePopup('photo');
                showPopup('video2');
                const video2Element = document.getElementById('video2Element');
                video2Element.play();
            }, 5000); // Show photo for 5 seconds
        };
    }
</script>

</body>
</html>
