<html lang="ka">
<head>
  <meta charset="UTF-8">
  <title>რამდენჯერ დაარტყამ ხვრინტატორს?</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: #1e1e2f;
      color: white;
      text-align: center;
      margin: 0;
    }
    h1 {
      padding: 20px;
      color: #ff66cc;
    }
    #game {
      display: grid;
      grid-template-columns: repeat(3, 150px);
      grid-gap: 20px;
      justify-content: center;
      margin: 30px auto;
      max-width: 600px;
    }
    .hole {
      width: 150px;
      height: 150px;
      background: #2e2e4e;
      border-radius: 50%;
      position: relative;
      overflow: hidden;
      cursor: pointer;
    }
    .chatlaxi {
      width: 100px;
      height: 100px;
      background: url('https://scontent.ftbs4-2.fna.fbcdn.net/v/t1.15752-9/506775490_620550964395521_4749417062849504107_n.png?_nc_cat=109&ccb=1-7&_nc_sid=9f807c&_nc_ohc=1MdY9GpEE-wQ7kNvwGBTR7e&_nc_oc=AdnxucogiyExaN_DSVaCatyu8xUeBW8_ru-W8CAkZsFQl0MmEHuCx_3Tngt3EvNrOkw&_nc_zt=23&_nc_ht=scontent.ftbs4-2.fna&oh=03_Q7cD2gF36f54Uzr2qQTpaivH5MdSEEjrpHyMx3unmyO_l1Fdrw&oe=6877DB71') no-repeat center center / contain;
      position: absolute;
      bottom: -100px;
      left: 25px;
      transition: bottom 0.3s;
    }
    .up {
      bottom: 10px;
    }
    #score {
      font-size: 24px;
      margin-top: 10px;
    }
    #timer {
      font-size: 18px;
      margin-top: 5px;
    }
    button {
      padding: 10px 20px;
      margin-top: 20px;
      font-size: 16px;
      cursor: pointer;
      background: #ff66cc;
      border: none;
      color: white;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <h1>სიზმრების პორტალები</h1>
  <div id="score">ქულა: 0</div>
  <div id="timer">დრო: 30</div>
  <div id="game"></div>
  <button onclick="startGame()">დაწყება</button>

  <script>
    const game = document.getElementById('game');
    const scoreDisplay = document.getElementById('score');
    const timerDisplay = document.getElementById('timer');
    let score = 0;
    let time = 30;
    let interval;
    let gameInterval;

    function createHoles() {
      for (let i = 0; i < 6; i++) {
        const hole = document.createElement('div');
        hole.classList.add('hole');

        const chatlaxi = document.createElement('div');
        chatlaxi.classList.add('chatlaxi');
        chatlaxi.addEventListener('click', () => {
          if (chatlaxi.classList.contains('up')) {
            score++;
            scoreDisplay.textContent = `ქულა: ${score}`;
            chatlaxi.classList.remove('up');
          }
        });

        hole.appendChild(chatlaxi);
        game.appendChild(hole);
      }
    }

    function randomUp() {
      const holes = document.querySelectorAll('.hole');
      const index = Math.floor(Math.random() * holes.length);
      const chosen = holes[index].querySelector('.chatlaxi');
      chosen.classList.add('up');
      setTimeout(() => chosen.classList.remove('up'), 800);
    }

    function startGame() {
      score = 0;
      time = 30;
      scoreDisplay.textContent = 'ქულა: 0';
      timerDisplay.textContent = 'დრო: 30';

      clearInterval(interval);
      clearInterval(gameInterval);

      interval = setInterval(() => {
        time--;
        timerDisplay.textContent = `დრო: ${time}`;
        if (time === 0) {
          clearInterval(interval);
          clearInterval(gameInterval);
          alert(`თამაში დასრულდა! შენი ქულაა: ${score}`);
        }
      }, 1000);

      gameInterval = setInterval(randomUp, 900);
    }

    createHoles();
  </script>
</body>
