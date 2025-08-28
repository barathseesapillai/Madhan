<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>A Surprise for You 💝</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap');

    body {
      margin: 0;
      padding: 0;
      height: 100vh;
      background: linear-gradient(135deg, #6a0dad, #b19cd9);
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      font-family: 'Great Vibes', cursive;
      text-align: center;
      overflow: hidden;
    }

    /* Intro Screen */
    #intro {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    #intro h1 {
      font-size: 3em;
      color: #f3e8ff;
      text-shadow: 2px 2px 10px rgba(255,255,255,0.4);
    }

    #intro button {
      margin-top: 20px;
      padding: 15px 30px;
      font-size: 1.5em;
      font-family: 'Great Vibes', cursive;
      border: none;
      border-radius: 30px;
      background: #9b59b6;
      color: #fff;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
      transition: 0.3s;
    }

    #intro button:hover {
      background: #8e44ad;
      transform: scale(1.1);
    }

    /* Surprise Screen */
    #surprise {
      display: none;
      flex-direction: column;
      align-items: center;
      width: 100%;
      height: 100%;
      background: linear-gradient(135deg, #7b2cbf, #c77dff);
      position: absolute;
      top: 0;
      left: 0;
    }

    #surprise h1 {
      font-size: 4em;
      margin-top: 40px;
      text-shadow: 0 0 20px #d8b4fe, 0 0 40px #a855f7;
      color: #f3e8ff;
    }

    #message {
      font-size: 2em;
      margin-top: 30px;
      width: 85%;
      margin-left: auto;
      margin-right: auto;
      border-right: 3px solid #e9d5ff;
      white-space: nowrap;
      overflow: hidden;
      color: #f5f3ff;
    }

    .balloon {
      position: absolute;
      bottom: -150px;
      width: 60px;
      height: 80px;
      border-radius: 50%;
      animation: floatUp 6s linear infinite;
    }

    .balloon::after {
      content: "";
      position: absolute;
      top: 80px;
      left: 50%;
      width: 2px;
      height: 40px;
      background: white;
    }

    @keyframes floatUp {
      0% { transform: translateY(0); opacity: 1; }
      100% { transform: translateY(-110vh); opacity: 0; }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }
  </style>
</head>
<body>
  <!-- Intro Screen -->
  <div id="intro">
    <h1>💝 A Surprise for You 💝</h1>
    <button onclick="showSurprise()">Open Surprise 🎁</button>
  </div>

  <!-- Surprise Screen -->
  <div id="surprise">
    <h1>🎂 Happy Birthday My Love 💖</h1>
    <div id="message"></div>
    <canvas id="confetti"></canvas>
    <audio id="music" loop>
      <source src="your-song.mp3" type="audio/mpeg">
    </audio>
  </div>

  <script>
    function showSurprise() {
      document.getElementById("intro").style.display = "none";
      document.getElementById("surprise").style.display = "flex";
      document.getElementById("music").play();
      typeWriter();
      setInterval(createBalloon, 800);
      setInterval(drawConfetti, 20);
    }

    // ⌨️ Typewriter Message
    const msg = "💜 My love, you make my world brighter each day... 🎂✨ I’m so lucky to have you. Happy Birthday, my everything! 💕";
    let i = 0;
    function typeWriter() {
      if (i < msg.length) {
        document.getElementById("message").innerHTML += msg.charAt(i);
        i++;
        setTimeout(typeWriter, 90);
      }
    }

    // 🎈 Balloons
    function createBalloon() {
      const balloon = document.createElement("div");
      balloon.className = "balloon";
      balloon.style.left = Math.random() * 100 + "vw";
      balloon.style.background = `hsl(${Math.random()*360},70%,70%)`;
      balloon.style.animationDuration = (5 + Math.random()*3) + "s";
      document.body.appendChild(balloon);
      setTimeout(() => balloon.remove(), 8000);
    }

    // 🎉 Confetti
    const canvas = document.getElementById('confetti');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let confetti = [];
    for (let i = 0; i < 150; i++) {
      confetti.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 6 + 4,
        d: Math.random() * 150,
        color: "hsl(" + Math.random()*360 + ",100%,70%)"
      });
    }

    function drawConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      confetti.forEach(p => {
        ctx.beginPath();
        ctx.fillStyle = p.color;
        ctx.fillRect(p.x, p.y, p.r, p.r);
      });
      update();
    }

    function update() {
      confetti.forEach(p => {
        p.y += Math.cos(p.d) + 1;
        p.x += Math.sin(p.d);
        if (p.y > canvas.height) {
          p.x = Math.random() * canvas.width;
          p.y = -10;
        }
      });
    }
  </script>
</body>
</html>

