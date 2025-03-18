# Henrique-
Para Brenda 
<!DOCTYPE html>
<html lang="pt">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Para a Brenda</title>
  <link href="https://fonts.googleapis.com/css?family=Montserrat:400,700&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      background: linear-gradient(135deg, #000, #434343);
      color: #fff;
      font-family: 'Montserrat', sans-serif;
      text-align: center;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      overflow: hidden;
    }
    h1 {
      font-size: 2em;
      max-width: 80%;
      margin-bottom: 40px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
    }
    .buttons {
      display: flex;
      gap: 20px;
    }
    button {
      padding: 15px 30px;
      font-size: 1.5em;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: font-size 0.3s ease;
    }
    #sim {
      background-color: #28a745;
      color: #fff;
    }
    #nao {
      background-color: #dc3545;
      color: #fff;
    }
    .hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      overflow: hidden;
    }
    .heart {
      position: absolute;
      font-size: 1.8em;
      animation: fall 3s linear infinite, drift 3s ease-in-out infinite;
    }
    @keyframes fall {
      0% { top: -10%; opacity: 1; }
      100% { top: 110%; opacity: 0; }
    }
    @keyframes drift {
      0% { transform: translateX(0); }
      50% { transform: translateX(20px); }
      100% { transform: translateX(0); }
    }
    .move {
      position: fixed;
      animation: moveNao 10s linear infinite;
    }
    @keyframes moveNao {
      0% { top: 50%; left: 50%; }
      25% { top: 10%; left: 80%; }
      50% { top: 90%; left: 70%; }
      75% { top: 30%; left: 20%; }
      100% { top: 50%; left: 50%; }
    }
    .notification {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #dc3545;
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      font-size: 1.2em;
      display: none;
    }
  </style>
</head>
<body>
  <h1>Eu te acho a mulher mais linda do mundo?</h1>
  <div class="buttons">
    <button id="sim" onclick="respostaSim()">Sim</button>
    <button id="nao" onclick="respostaNao()">Não</button>
  </div>

  <div class="hearts" id="hearts"></div>
  
  <!-- Notificação de Erro -->
  <div id="notification" class="notification">Você está errando muito!</div>

  <audio id="naoSound" src="https://www.myinstants.com/media/sounds/erro.mp3"></audio> <!-- Som de erro -->
  <audio id="simMusic" src="https://www.myinstants.com/media/sounds/i-love-you.mp3"></audio>  

  <script>
    let simButton = document.getElementById('sim');
    let naoButton = document.getElementById('nao');
    let heartsContainer = document.getElementById('hearts');
    let notification = document.getElementById('notification');
    let naoSound = document.getElementById('naoSound');
    let simMusic = document.getElementById('simMusic');

    let naoClickCount = 0;

    function respostaNao() {
      // Iniciar animação de movimento no botão "Não"
      naoButton.classList.add('move');
      
      let simSize = parseFloat(window.getComputedStyle(simButton).fontSize);
      let naoSize = parseFloat(window.getComputedStyle(naoButton).fontSize);

      // Sim cresce
      simButton.style.fontSize = (simSize + 4) + 'px'; 

      // Não diminui até um tamanho mínimo
      if (naoSize > 30) {
        naoButton.style.fontSize = (naoSize - 2) + 'px'; // Não diminui até um tamanho mínimo
      }

      // Tocar o som do erro
      if (!naoSound.paused) {
        naoSound.currentTime = 0;
      }
      naoSound.play();

      // Contabilizar cliques no "Não"
      naoClickCount++;

      // Mostrar notificação se o "Não" for clicado 2 ou 3 vezes
      if (naoClickCount >= 2) {
        notification.style.display = 'block';
        setTimeout(() => {
          notification.style.display = 'none';
        }, 3000);  // Esconde a notificação após 3 segundos
      }
    }

    function respostaSim() {
      // Tocar o som do "Sim"
      simMusic.currentTime = 0;
      simMusic.play();
      
      // Criar corações na tela
      for (let i = 0; i < 20; i++) {
        let heart = document.createElement('div');
        heart.classList.add('heart');
        heart.textContent = "❤️";
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.animationDuration = (Math.random() * 2 + 2) + 's';
        heartsContainer.appendChild(heart);
        setTimeout(() => heart.remove(), 3000);
      }
    }
  </script>
</body>
</html>
