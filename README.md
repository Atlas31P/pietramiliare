<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Pietra Miliare Maldives</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
  background-color: #000;
  overflow: hidden;
  height: 100vh;
  font-family: "Courier New", Courier, monospace;
  color: #00ffff;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

/* Titolo */
h1 {
  font-size: clamp(28px, 5vw, 46px);
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #00ffff;
  text-shadow: 0 0 10px #00ffff, 0 0 20px #00ccff;
  z-index: 12;              /* sopra lo squalo */
  margin-top: 110px;        /* spazio sotto il logo */
  margin-bottom: 16px;
  text-align: center;
  pointer-events: none;
}

/* Canvas in background */
canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  display: block;
}

/* LOGO PNG: centrato in alto, bianco -> trasparente */
#logo {
  position: absolute;
  top: 12px;
  left: 50%;
  transform: translateX(-50%);
  width: clamp(140px, 22vw, 260px);
  z-index: 15;
  pointer-events: none;
  filter: url(#whiteToAlpha);
}

/* SQUALO: centrato, grande, sotto il titolo */
#sharkGif {
  position: absolute;
  left: 50%;
  top: 58%;
  transform: translate(-50%, -50%);
  width: clamp(280px, 60vw, 1000px);
  z-index: 11;              /* sotto il titolo, sopra il canvas */
  opacity: 0.9;
  animation: floatShark 10s ease-in-out infinite;
  pointer-events: none;
}

/* Animazione fluttuante */
@keyframes floatShark {
  0%, 100% { transform: translate(-50%, -50%) translateY(0) rotate(0deg); }
  50%      { transform: translate(-50%, -50%) translateY(-18px) rotate(2deg); }
}

/* Mobile */
@media (max-width: 768px) {
  h1 { font-size: 30px; margin-top: 96px; }
  #logo { width: clamp(120px, 28vw, 200px); }
  #sharkGif { width: clamp(300px, 78vw, 860px); top: 60%; }
}
</style>
</head>

<body>
  <!-- Filtro SVG per rendere trasparenti i bianchi del PNG (white-to-alpha) -->
  <svg width="0" height="0" style="position:absolute">
    <filter id="whiteToAlpha" color-interpolation-filters="sRGB">
      <!-- Calcola la luminosità -->
      <feColorMatrix type="matrix" values="
        0.2126 0.7152 0.0722 0 0
        0.2126 0.7152 0.0722 0 0
        0.2126 0.7152 0.0722 0 0
        0       0       0       1 0" result="lumRGB" />
      <!-- Usa il canale di luminosità per modulare l'alpha (bianchi -> trasparenti) -->
      <feComponentTransfer>
        <feFuncR type="identity"/>
        <feFuncG type="identity"/>
        <feFuncB type="identity"/>
        <!-- Soglia: 0.92 aggressiva sui bianchi; abbassa per rendere più trasparente -->
        <feFuncA type="table" tableValues="1 0.92 0"/>
      </feComponentTransfer>
    </filter>
  </svg>

  <!-- Titolo -->
  <h1>PIETRA MILIARE MALDIVES</h1>

  <!-- Canvas effetto onde testuali -->
  <canvas id="matrixCanvas"></canvas>

  <!-- GIF squalo: centrata e grande -->
  <img id="sharkGif" src="shark.gif" alt="Shark animation" />

<script>
const canvas = document.getElementById("matrixCanvas");
const ctx = canvas.getContext("2d");

function resizeCanvas() {
  const dpr = window.devicePixelRatio || 1;
  canvas.width = Math.floor(window.innerWidth * dpr);
  canvas.height = Math.floor(window.innerHeight * dpr);
  canvas.style.width = window.innerWidth + "px";
  canvas.style.height = window.innerHeight + "px";
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
}
resizeCanvas();

let width = window.innerWidth;
let height = window.innerHeight;

const messages = [
  "until we make it",
  "zitto e nuota zitto e nuota nuota nuota",
  "一直到我们成功",
  "जब तक हम सफल न हों",
  "hasta que lo logremos",
  "حتى ننجح",
  "যতক্ষণ না আমরা सफल হচ্ছি",
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
  ctx.font = `${fontSize}px "Courier New", Courier, monospace`;
  ctx.textBaseline = "middle";
  ctx.shadowColor = "#00ffff";
  ctx.shadowBlur = 10;

  for (let l = 0; l < lines; l++) {
    const yOffset = (height / lines) * (l + 1);
    const waveAmplitude = 20 + l * 3;
    const waveFrequency = 0.01 + l * 0.002;
    const waveSpeed = 1 + l * 0.2;
    const fullMessage = messages[l].repeat(50);
    const letters = fullMessage.split("");

    for (let i = 0; i < letters.length; i++) {
      const rawX = (i * textSpacing) - (offset * waveSpeed);
      const totalSpan = width + letters.length * textSpacing;
      // normalizza in [0, totalSpan)
      const xWrapped = ((rawX % totalSpan) + totalSpan) % totalSpan;
      const x = xWrapped < 0 ? xWrapped + width : xWrapped;
      const y = yOffset + Math.sin((x + offset) * waveFrequency) * waveAmplitude;
      const hue = (180 + (l * 10)) % 360;
      ctx.fillStyle = `hsl(${hue}, 100%, 60%)`;
      ctx.fillText(letters[i], x, y);
    }
  }

  offset += 1.5;
  requestAnimationFrame(draw);
}
draw();

window.addEventListener("resize", () => {
  width = window.innerWidth;
  height = window.innerHeight;
  resizeCanvas();
});
</script>
</body>
</html>
