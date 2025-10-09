<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Pietra Miliare Maldives</title>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
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

/* Responsive title */
h1 {
  font-size: clamp(28px, 5vw, 46px);
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #00ffff;
  text-shadow: 0 0 10px #00ffff, 0 0 20px #00ccff;
  z-index: 10;
  margin-bottom: 20px;
  text-align: center;
}

/* Canvas behind text */
canvas {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  z-index: 0;
  display: block;
}

/* Logo and shark GIF styling */
#logo {
  width: clamp(120px, 20vw, 200px);
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 15;
}

#sharkGif {
  position: absolute;
  bottom: 10%;
  right: 10%;
  width: clamp(100px, 15vw, 200px);
  z-index: 5;
  opacity: 0.7;
  animation: floatShark 10s ease-in-out infinite;
}

/* Simple floating animation */
@keyframes floatShark {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-15px) rotate(2deg); }
}

/* Mobile optimization */
@media (max-width: 768px) {
  h1 {
    font-size: 30px;
  }
}
</style>
</head>

<body>
<img id="logo" src="logo.png" alt="Pietra Miliare Logo" />
<h1>PIETRA MILIARE MALDIVES</h1>
<canvas id="matrixCanvas"></canvas>
<img id="sharkGif" src="shark.gif" alt="Shark animation" />

<script>
const canvas = document.getElementById("matrixCanvas");
const ctx = canvas.getContext("2d");

let width = canvas.width = window.innerWidth;
let height = canvas.height = window.innerHeight;

const messages = [
  "until we make it",
  "zitto e nuota zitto e nuota nuota nuota",
  "一直到我们成功",
  "जब तक हम सफल न हों",
  "hasta que lo logremos",
  "حتى ننجح",
  "যতক্ষণ না আমরা সফল হচ্ছি",
  "até conseguirmos",
  "пока не добьемся этого",
  "成功するまで",
  "jusqu’à ce qu’on y arrive"
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

