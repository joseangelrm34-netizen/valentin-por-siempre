# valentin-por-siempre
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aura Elissa 💖 ¿Quieres ser mi San Valentín?</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: radial-gradient(circle at top, #ffd1dc, #ff9a9e, #fad0c4);
      color: #5a1a2a;
      text-align: center;
    }

    .card {
      position: relative;
      background: rgba(255, 255, 255, 0.92);
      padding: 2.5rem 2rem 2.8rem;
      border-radius: 24px;
      max-width: 460px;
      box-shadow: 0 25px 50px rgba(0, 0, 0, 0.18);
      animation: fadeIn 1.6s ease;
      z-index: 2;
    }

    h1 {
      font-size: 2.2rem;
      margin-bottom: 0.6rem;
    }

    h2 {
      font-size: 1.1rem;
      font-weight: 500;
      margin-top: 0;
      color: #8b1e3f;
    }

    p {
      font-size: 1.05rem;
      line-height: 1.65;
      margin: 0.8rem 0 1.4rem;
    }

    .heart {
      font-size: 3.2rem;
      animation: beat 1.2s infinite;
      margin-bottom: 0.4rem;
    }

    .buttons {
      display: flex;
      gap: 1rem;
      justify-content: center;
      margin-top: 1.2rem;
    }

    button {
      background: #e63956;
      border: none;
      color: white;
      padding: 0.75rem 1.5rem;
      font-size: 1.05rem;
      border-radius: 30px;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
      box-shadow: 0 10px 22px rgba(230, 57, 86, 0.45);
    }

    button.secondary {
      background: #bbb;
      box-shadow: 0 8px 18px rgba(0,0,0,0.25);
    }

    button:hover {
      transform: scale(1.06);
      box-shadow: 0 14px 28px rgba(230, 57, 86, 0.6);
    }

    .message {
      display: none;
      margin-top: 1.6rem;
      font-size: 1.2rem;
      font-weight: bold;
      color: #b5173a;
      animation: fadeIn 0.8s ease;
    }

    .surprise {
      display: none;
      margin-top: 1rem;
      font-size: 1.05rem;
      color: #6a0f2b;
      animation: fadeIn 1s ease;
    }

    /* Falling hearts */
    .heart-fall {
      position: absolute;
      top: -10vh;
      font-size: 1.4rem;
      animation: fall linear forwards;
      opacity: 0.9;
      pointer-events: none;
    }

    @keyframes fall {
      to { transform: translateY(110vh) rotate(360deg); opacity: 0; }
    }

    @keyframes beat {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.25); }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes glow {
      0% { transform: scale(1); text-shadow: 0 0 5px #ff9a9e; }
      50% { transform: scale(1.08); text-shadow: 0 0 18px #e63956; }
      100% { transform: scale(1); text-shadow: 0 0 5px #ff9a9e; }
    }

    .animated-question {
      display: inline-block;
      animation: glow 1.6s infinite ease-in-out;
    }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <!-- Música romántica (puedes cambiar el archivo por uno propio) -->
  <audio id="music" loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/02/23/audio_0b1b8a8b3f.mp3?filename=romantic-ambient-112191.mp3" type="audio/mpeg">
  </audio>

  <div class="card">
    <div class="heart">❤️</div>
    <h1>Aura Elissa</h1>
    <h2>Mi pica pollo rica 🤤 💕</h2>

    <p>
      Desde que llegaste a mi vida, cada día tiene más sentido,
      más risas y más amor. No imagino a nadie más a mi lado que tú.
    </p>
    <p>
      Eres mi compañera, mi hogar y mi persona favorita.
      Hoy quiero hacerte una pregunta muy especial...
    </p>

    <p style="font-size:1.35rem; font-weight:800; color:#b5173a;">
      <span class="animated-question">¿Quieres ser mi Valentín por siempre? 💘</span>
    </p>
    </p>

    <div class="buttons" id="question">
      <button onclick="sayYes()">Sí, claro que sí 😍</button>
      <button class="secondary" id="noBtn" onmouseover="moveNo()">No 🙈</button>
    </div>

    <div class="message" id="message">
      ¡Gracias por decir que sí!💖
    </div>

    <div class="surprise" id="surprise">
      Prometo una cita llena de amor, risas, piques y besos.
      Gracias por ser mi San Valentín hoy, mañana y siempre.
      Love you to the moon and back 🌹
    </div>
  </div>

  <script>
    const music = document.getElementById('music');

    // Intentar reproducir música tras la primera interacción
    document.body.addEventListener('click', () => {
      if (music.paused) music.play().catch(() => {});
    }, { once: true });

    function sayYes() {
      document.getElementById('question').style.display = 'none';
      document.getElementById('message').style.display = 'block';
      document.getElementById('surprise').style.display = 'block';
      launchHearts(30);
      heartFireworks();
    }

    function moveNo() {
      const btn = document.getElementById('noBtn');
      const x = Math.random() * 240 - 120;
      const y = Math.random() * 160 - 80;
      btn.style.transform = `translate(${x}px, ${y}px)`;
    }

    function launchHearts(count) {
      for (let i = 0; i < count; i++) {
        const h = document.createElement('div');
        h.className = 'heart-fall';
        h.textContent = '❤️';
        h.style.left = Math.random() * 100 + 'vw';
        h.style.animationDuration = (3 + Math.random() * 3) + 's';
        h.style.fontSize = (1 + Math.random() * 1.5) + 'rem';
        document.body.appendChild(h);
        setTimeout(() => h.remove(), 6000);
      }
    }

    // Corazones suaves de fondo
    setInterval(() => launchHearts(2), 1200);

    function heartFireworks() {
      for (let i = 0; i < 6; i++) {
        setTimeout(() => explode(), i * 400);
      }
    }

    function explode() {
      const centerX = Math.random() * window.innerWidth;
      const centerY = Math.random() * window.innerHeight * 0.6;
      for (let i = 0; i < 18; i++) {
        const h = document.createElement('div');
        h.className = 'heart-fall';
        h.textContent = '💖';
        const angle = (Math.PI * 2 / 18) * i;
        const distance = 120 + Math.random() * 60;
        h.style.left = centerX + 'px';
        h.style.top = centerY + 'px';
        h.style.fontSize = (1.2 + Math.random()) + 'rem';
        document.body.appendChild(h);

        const x = Math.cos(angle) * distance;
        const y = Math.sin(angle) * distance;
        h.animate([
          { transform: 'translate(0,0)', opacity: 1 },
          { transform: `translate(${x}px, ${y}px)`, opacity: 0 }
        ], {
          duration: 1200,
          easing: 'ease-out'
        });

        setTimeout(() => h.remove(), 1300);
      }
    }
  </script>
</body>
</html>
