<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Pietra Miliare Maldives</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background-color: black;
      overflow: hidden;
      height: 100vh;
      font-family: 'Courier New', Courier, monospace;
      color: #00ffff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: relative;
    }

    h1 {
      font-size: 46px;
      font-weight: bold;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: #00ffff;
      text-shadow: 0 0 10px #00ffff, 0 0 20px #00ccff;
      z-index: 10;
      margin-bottom: 20px;
    }

    canvas {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 0;
      display: block;
    }
  </style>
</head>
<body>
  <h1>PIETRA MILIARE MALDIVE</h1>
  <canvas id="matrixCanvas"></canvas>

  <script>
    const canvas = document.getElementById("matrixCanvas");
    const ctx = canvas.getContext("2d");

    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;

    const messages = [
      "until we make it",               // English
      "zitto e nuota zitto e nuota nuota nuota", // Italian
      "一直到我们成功",                // Chinese (Mandarin)
      "जब तक हम सफल न हों",          // Hindi
      "hasta que lo logremos",         // Spanish
      "حتى ننجح",                      // Arabic
      "যতক্ষণ না আমরা সফল হচ্ছি",     // Bengali
      "até conseguirmos",              // Portuguese
      "пока не добьемся этого",        // Russian
      "成功するまで",                  // Japanese
      "jusqu’à ce qu’on y arrive"      // French
    ];

    const fontSize = 20;
    const textSpacing = fontSize + 5;
    const lines = messages.length;

    let offset = 0;

    function draw() {
      ctx.clearRect(0, 0, width, height);
      ctx.font = `${fontSize}px Courier New`;
      ctx.shadowColor = "#00ffff";
      ctx.shadowBlur = 10;

      for (let l = 0; l < lines; l++) {
        const yOffset = (height / lines) * (l + 1);
        const waveAmplitude = 20 + l * 3;
        const waveFrequency = 0.01 + l * 0.002;
        const waveSpeed = 1 + l * 0.2;

        const fullMessage = messages[l].repeat(50);
        const letters = fullMessage.split('');

        for (let i = 0; i < letters.length; i++) {
          const x = ((i * textSpacing) - (offset * waveSpeed)) % (width + letters.length * textSpacing);
          const y = yOffset + Math.sin((x + offset) * waveFrequency) * waveAmplitude;

          const hue = 180 + (l * 10) % 60;
          ctx.fillStyle = `hsl(${hue}, 100%, 60%)`;

          ctx.fillText(letters[i], x < 0 ? x + width : x, y);
        }
      }

      offset += 1.5;
      requestAnimationFrame(draw);
    }

    draw();

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
