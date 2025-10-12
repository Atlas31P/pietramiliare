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
}

/* Titolo */
h1 {
  font-size: clamp(28px, 5vw, 46px);
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #00ffff;
  text-shadow: 0 0 10px #00ffff, 0 0 20px #00ccff;
  z-index: 12;             /* sopra lo squalo */
  margin-top: 100px;       /* spazio sotto il logo */
  margin-bottom: 16px;
  text-align: center;
  pointer-events: none;
}

/* Canvas in background */
canvas {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  z-index: 0;
  display: block;
}

/* LOGO PNG: centrato in alto con "white to alpha" */
#logo {
  position: absolute;
  top: 12px;
  left: 50%;
  transform: translateX(-50%);
  width: clamp(140px, 22vw, 260px);
  z-index: 15;
  pointer-events: none;
  filter: url(#whiteToAlpha);  /* rimuove il bianco come trasparenza */
}

/* SQUALO: centrato, grande, sotto la scritta */
#sharkGif {
  position: absolute;
  left: 50%;
  top: 58%;                         /* sotto il titolo */
  transform: translate(-50%, -50%);
  width: clamp(280px, 60vw, 1000px); /* molto più grande */
