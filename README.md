<!DOCTYPE html>
<html lang="da">
<head>
  <meta charset="UTF-8" />
  <title>Meldingsvælger - iPad Landscape med animation og lyd</title>
  <style>
    html, body {
      margin: 0; padding: 0; height: 100%;
      font-family: "Noto Sans Symbols", "Times New Roman", serif;
      background-color: #004d00 !important;
      overflow: hidden;
    }

    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      padding: 20px;
    }

    .container {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: stretch;
      gap: 80px;
      width: 100%;
      max-width: 1024px;
      height: 450px; /* lidt mere plads til animation */
      box-sizing: border-box;
    }

    .section {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      min-width: 0;
      user-select: none;
      height: 100%;
    }

    .section h2 {
      font-size: 48px;
      margin: 0;
      text-transform: uppercase;
      color: #ffffff;
      flex-shrink: 0;
      line-height: 1;
      height: 75px;
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
    }

    .display {
      font-size: 220px;
      line-height: 220px;
      height: 220px;
      margin: 0;
      user-select: none;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-shrink: 0;
      pointer-events: none;
    }
#numberDisplay {
  color: white; 
}

    .button-group {
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
      flex-shrink: 0;
    }

    button {
      font-size: 30px;
      width: 40px;
      height: 40px;
      border-radius: 10px;
      border: 2px solid #555;
      background-color: #fafafa;
      cursor: pointer;
      transition: background-color 0.3s, border-color 0.3s;
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
    }

    button:hover {
      background-color: #f0e6d2;
      border-color: #333;
    }

    #celebrateBtn {
      font-size: 80px;
      padding: 30px;
      border-radius: 50%;
      background-color: #ffe066;
      border: 3px solid #222;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
      cursor: pointer;
      margin-top: 50px;
      align-self: center;
      transition: transform 0.3s ease, background-color 0.3s;
      user-select: none;
    }

    #celebrateBtn:hover {
      background-color: #ffcd39;
      transform: scale(1.1);
    }

    /* Popup tekst */
    #popupText {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 18vw;
      font-weight: 900;
      color: #0000ff;
      background-color: rgba(255, 255, 255, 0.7);
      padding: 0.2em 0.4em;
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0, 0, 255, 0.6);
      z-index: 1000;
      display: none;
      pointer-events: none;
      user-select: none;
      white-space: nowrap;
    }

    /* Animationer og konfetti */
    .bg-flash {
      animation: bgBlink 3s ease;
    }

    @keyframes bgBlink {
      0%, 100% { background-color: #fff; }
      10% { background-color: #ffe066; }
      20% { background-color: #ffcd39; }
      30% { background-color: #fff3b0; }
      50% { background-color: #fff; }
      70% { background-color: #ffe066; }
      90% { background-color: #ffcd39; }
    }

    .confetti {
      position: fixed;
      top: 0;
      font-size: 40px;
      animation: drop 3s ease forwards;
      pointer-events: none;
      z-index: 998;
      animation-timing-function: ease-in-out;
    }

    .confetti:nth-child(2n) {
      animation-name: dropSwing;
      animation-timing-function: ease-in-out;
    }

    @keyframes drop {
      0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
      50% { opacity: 1; }
      100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
    }

    @keyframes dropSwing {
      0% { transform: translateY(-100px) translateX(0) rotate(0deg); opacity: 1; }
      25% { transform: translateY(25vh) translateX(20px) rotate(90deg); opacity: 1; }
      50% { transform: translateY(50vh) translateX(-20px) rotate(180deg); opacity: 0.9; }
      75% { transform: translateY(75vh) translateX(10px) rotate(270deg); opacity: 0.5; }
      100% { transform: translateY(100vh) translateX(0) rotate(360deg); opacity: 0; }
    }

    .firework {
      position: fixed;
      font-size: 40px;
      animation: explode 1s ease-out forwards;
      z-index: 999;
      pointer-events: none;
    }

    @keyframes explode {
      0% { transform: scale(0.5) rotate(0deg); opacity: 1; }
      50% { transform: scale(2.5) rotate(360deg); opacity: 0.8; }
      100% { transform: scale(3) rotate(720deg); opacity: 0; }
    }

    /* Responsivt for mindre end 1024px bredde */
    @media (max-width: 1024px) {
      .container {
        flex-direction: column;
        height: auto;
        max-width: 100%;
        gap: 40px;
      }
      .section {
        height: auto;
      }
      .display {
        font-size: 140px;
        height: 140px;
        line-height: 140px;
      }
      button {
        font-size: 60px;
        width: 90px;
        height: 90px;
      }
      #celebrateBtn {
        font-size: 50px;
        padding: 15px;
        margin-top: 30px;
      }
      #popupText {
        font-size: 14vw;
      }
    }
/* VENSTRE SIDE KNAPPER */
.left-side {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-right: 80px; /* afstand til hovedcontainer */
}

.left-side button {
  width: 130px;
  height: 130px;
  font-size: 18px;
  font-weight: 700;
  border-radius: 10px;
  border: 2px solid #555;
  background-color: #fafafa;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  user-select: none;
  transition: background-color 0.3s, border-color 0.3s;
  padding: 0;
}

.left-side button:hover {
  background-color: #f0e6d2;
  border-color: #333;
}

.left-side button.active {
  background-color: #ffe066;
  border-color: #222;
  box-shadow: 0 0 8px #ffcd39;
}

/* Flytter celebrate-knappen ind i venstre side */
#celebrateBtn {
  margin-top: 20px;
  align-self: center;
  font-size: 80px;
  width: 130px;
  height: 130px;
  padding: 30px;
  border-radius: 50%;
  background-color: #ffe066;
  border: 3px solid #222;
  box-shadow: 0 0 15px rgba(0,0,0,0.2);
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s;
  user-select: none;
}

#celebrateBtn:hover {
  background-color: #ffcd39;
  transform: scale(1.1);
}

/* Responsivt til venstre knapper på mindre skærm */
@media (max-width: 1024px) {
  .left-side {
    flex-direction: row;
    margin-right: 0;
    gap: 10px;
    margin-bottom: 30px;
  }
  .left-side button {
    font-size: 14px;
    width: 90px;
    height: 90px;
  }
  #celebrateBtn {
    font-size: 50px;
    width: 90px;
    height: 90px;
    padding: 15px;
    margin-top: 0;
  }
}

  </style>
</head>
<body>
  <div class="container">
<div class="left-side">
  <button id="btnAlm" onclick="selectLeftButton(this)">Alm.</button>
  <button id="btnGode" onclick="selectLeftButton(this)">Gode</button>
  <button id="btnVip" onclick="selectLeftButton(this)">Vip</button>
  <button id="btnHalve" onclick="selectLeftButton(this)">Halve</button>
  <button onclick="celebrate13()" id="celebrateBtn">🎉</button>
</div>

    <div class="section">
      <h2>MELDING</h2>
      <div id="numberDisplay" class="display">8</div>
      <div class="button-group">
        <button onclick="setNumber(8)">8</button>
        <button onclick="setNumber(9)">9</button>
        <button onclick="setNumber(10)">10</button>
        <button onclick="setNumber(11)">11</button>
        <button onclick="setNumber(12)">12</button>
        <button onclick="setNumber(13)">13</button>
      </div>
    </div>

    <div class="section">
      <h2>TRUMF</h2>
      <div id="trumpDisplay" class="display suit">♥️</div>
      <div class="button-group">
        <button onclick="setTrump('♥️')">♥️</button>
        <button onclick="setTrump('♣️')">♣️</button>
        <button onclick="setTrump('♦️')">♦️</button>
        <button onclick="setTrump('♠️')">♠️</button>
        <button onclick="setTrump('🃏')">🃏</button>
      </div>
    </div>

    <div class="section">
      <h2>MAKKERES</h2>
      <div id="partnerDisplay" class="display suit">♣️</div>
      <div class="button-group">
        <button onclick="setPartner('♥️')">♥️</button>
        <button onclick="setPartner('♣️')">♣️</button>
        <button onclick="setPartner('♦️')">♦️</button>
        <button onclick="setPartner('♠️')">♠️</button>
      </div>
    </div>
  </div>

   <div id="popupText">13 STIK!</div>

  <script>
    // Sæt værdier
    function setNumber(n) {
      document.getElementById('numberDisplay').textContent = n;
    }
    function setTrump(s) {
      document.getElementById('trumpDisplay').textContent = s;
    }
    function setPartner(s) {
      document.getElementById('partnerDisplay').textContent = s;
    }

    // Audio Context til lyd
    const ctx = new (window.AudioContext || window.webkitAudioContext)();

    function playTone(freq, startTime, duration, vibratoRate = 6, vibratoDepth = 10) {
      const osc = ctx.createOscillator();
      const gainNode = ctx.createGain();
      const vibrato = ctx.createOscillator();
      const vibratoGain = ctx.createGain();

      osc.type = 'sine';
      osc.frequency.setValueAtTime(freq, startTime);

      vibrato.frequency.setValueAtTime(vibratoRate, startTime);
      vibratoGain.gain.setValueAtTime(vibratoDepth, startTime);

      vibrato.connect(vibratoGain);
      vibratoGain.connect(osc.frequency);

      gainNode.gain.setValueAtTime(0, startTime);
      gainNode.gain.linearRampToValueAtTime(0.4, startTime + 0.05);
      gainNode.gain.linearRampToValueAtTime(0, startTime + duration);

      osc.connect(gainNode);
      gainNode.connect(ctx.destination);

      osc.start(startTime);
      vibrato.start(startTime);
      osc.stop(startTime + duration);
      vibrato.stop(startTime + duration);
    }

    // Fejring af 13
    function celebrate13() {
      const now = ctx.currentTime;

      playTone(880, now, 0.3);
      playTone(1108, now + 0.25, 0.3);
      playTone(1318, now + 0.5, 0.3);
      playTone(1760, now + 0.75, 0.6, 8, 20);

      const glideOsc = ctx.createOscillator();
      const glideGain = ctx.createGain();
      glideOsc.type = 'triangle';
      glideOsc.frequency.setValueAtTime(1760, now + 1.3);
      glideOsc.frequency.exponentialRampToValueAtTime(440, now + 2.3);

      glideGain.gain.setValueAtTime(0.3, now + 1.3);
      glideGain.gain.exponentialRampToValueAtTime(0.001, now + 2.3);

      glideOsc.connect(glideGain);
      glideGain.connect(ctx.destination);

      glideOsc.start(now + 1.3);
      glideOsc.stop(now + 2.3);

      // Popup tekst og baggrundsflash
      const popup = document.getElementById('popupText');
      document.body.classList.add('bg-flash');
      popup.style.display = 'inline-block';

      // Fireworks
      for (let i = 0; i < 40; i++) {
        const firework = document.createElement('div');
        firework.className = 'firework';
        firework.textContent = ['🎆', '✨', '💥'][Math.floor(Math.random() * 3)];
        firework.style.top = `${Math.random() * window.innerHeight}px`;
        firework.style.left = `${Math.random() * window.innerWidth}px`;
        firework.style.fontSize = `${20 + Math.random() * 40}px`;
        document.body.appendChild(firework);
        setTimeout(() => firework.remove(), 1000);
      }

      // Confetti
      for (let i = 0; i < 60; i++) {
        const confetti = document.createElement('div');
        confetti.className = 'confetti';
        confetti.textContent = ['🎊', '🎉', '🎈'][Math.floor(Math.random() * 3)];
        confetti.style.top = `-${Math.random() * 50 + 20}px`;
        confetti.style.left = `${Math.random() * window.innerWidth}px`;
        confetti.style.fontSize = `${20 + Math.random() * 20}px`;
        confetti.style.animationDelay = `${Math.random() * 3}s`;
        document.body.appendChild(confetti);
        setTimeout(() => confetti.remove(), 3000);
      }

      setTimeout(() => {
        popup.style.display = 'none';
        document.body.classList.remove('bg-flash');
      }, 3000);
    }
// Markér valgt knap i venstre side (kun én aktiv ad gangen)
function selectLeftButton(button) {
  const buttons = document.querySelectorAll('.left-side button');
  buttons.forEach(btn => btn.classList.remove('active'));
  button.classList.add('active');
}

  </script>
</body>
</html>
