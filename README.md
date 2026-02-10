<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Valentine 💖</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: pink;
      text-align: center;
      padding-top: 60px;
      margin: 0;
    }

    h1 {
      font-size: 40px;
    }

    #letter {
      font-size: 24px;
      line-height: 1.6;
      margin: 20px auto;
      max-width: 600px;
      white-space: pre-wrap; /* keeps line breaks */
      text-align: center;
    }

    button {
      font-size: 20px;
      padding: 15px 30px;
      margin: 10px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }

    #yesBtn {
      background-color: red;
      color: white;
    }

    #noBtn {
      background-color: white;
      color: black;
    }

    #secondPage {
      display: none;
    }

    img {
      width: 300px;
      margin-top: 20px;
      border-radius: 20px;
      opacity: 0;
      transition: opacity 1s;
    }
  </style>
</head>

<body>

  <!-- FIRST PAGE -->
  <div id="firstPage">
    <h1>Will you be my Valentine? 💘</h1>
    <button id="yesBtn">YES</button>
    <button id="noBtn">NO</button>
    <p id="noText"></p>
  </div>

  <!-- SECOND PAGE -->
  <div id="secondPage">
    <h1>Happy Valentine’s Day! 💖</h1>
    <div id="letter"></div>
    <img src="1000003958.jpg" alt="Love image">
    <audio id="loveAudio" loop>
      <source src="Nothing.mp3" type="audio/mpeg">
      Your browser does not support the audio element.
    </audio>
  </div>

  <script>
    const noMessages = [
      "are you sure?",
      "baby u sure",
      "babyyyyyy",
      "just say yes baby",
      "baby pleaseeee"
    ];

    let noCount = 0;
    let yesSize = 20;

    const yesBtn = document.getElementById("yesBtn");
    const noBtn = document.getElementById("noBtn");
    const noText = document.getElementById("noText");

    const audio = document.getElementById("loveAudio");
    const secondPage = document.getElementById("secondPage");
    const secondH1 = secondPage.querySelector("h1");
    const letterDiv = document.getElementById("letter");
    const secondImg = secondPage.querySelector("img");

    const letterText = `Every moment with you makes my life brighter.
Your smile, your laugh, your heart they mean the world to me.

I love you more than words can say, and I’m so grateful for you every single day.
You’re my everything.`;

    noBtn.onclick = () => {
      noText.textContent = noMessages[noCount % noMessages.length];
      noCount++;

      yesSize += 10;
      yesBtn.style.fontSize = yesSize + "px";
      yesBtn.style.padding = yesSize / 2 + "px";
    };

    yesBtn.onclick = () => {
      // Hide first page
      document.getElementById("firstPage").style.display = "none";

      // Show second page
      secondPage.style.display = "block";

      // Fade in music
      audio.volume = 0;
      audio.play().catch(() => console.log("Audio failed to play."));

      let fadeInterval = setInterval(() => {
        if (audio.volume < 1) {
          audio.volume = Math.min(audio.volume + 0.05, 1);
        } else {
          clearInterval(fadeInterval);
        }
      }, 200);

      // Fade in heading
      setTimeout(() => secondH1.style.opacity = 1, 100);

      // Type out letter
      let index = 0;
      function typeLetter() {
        if (index < letterText.length) {
          letterDiv.textContent += letterText.charAt(index);
          index++;
          setTimeout(typeLetter, 50); // adjust typing speed here
        } else {
          // fade in image after letter completes
          secondImg.style.opacity = 1;
        }
      }

      setTimeout(typeLetter, 800); // delay before typing starts
    };
  </script>

</body>
</html>
