<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
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
  isolation: isolate; /* migliora il blending del logo */
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
  pointer-events: none;
}

/* Canvas behind text */
canvas {
  position: absolute;
  inset: 0;
  width: 100%; height: 100%;
  z-index: 0;
  display: block;
}

/* Logo PNG: rende il bianco “trasparente” sul fondo nero */
#logo {
  width: clamp(120px, 20vw, 200px);
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 15;
  opacity: 0.95;
  mix-blend-mode: multiply;      /* il bianco sparisce sul nero */
  pointer-events: none;
  image-rendering: -webkit-optimize-contrast;
}

/* Shark GIF: centrata e grande su tutti i device */
#sharkGif {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: clamp(240px, 55vw, 900px);
  z-index: 5;
  opacity: 0.85;
  animation: floatShark 10s ease-in-out infinite;
  pointer-events: none;
}

/* Simple floating animation */
@keyframes floatShark {
  0%, 100% { transform: translate(-50%, -50%) translateY(0) rotate(0deg); }
  50%      { transform: translate(-50%, -50%) translateY(-18px) rotate(2deg); }
}

/* Mobile optimization */
@media (max-width: 768px) {
  h1 { font-size: 30px; }
  #logo { width: clamp(100px, 28vw, 160px); }
  #sharkGif { width: clamp(260px, 70vw, 720px); }
}
</style>
</head>

<body>
  <!-- Usa il tuo PNG originale; il bianco verrà “assorbito” dal fondo nero -->
  <img id="logo" src="logo.png" alt="Pietra Miliare Logo" />

  <h1>PIETRA MILIARE MALDIVES</h1>
  <canvas id="matrixCanvas"></canvas>

  <!-- GIF centrata e grande -->
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

function dra
