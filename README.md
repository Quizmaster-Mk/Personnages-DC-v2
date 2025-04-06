<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel personnage de DC êtes-vous ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #f0f0f0;  /* Fond clair */
      color: #333;  /* Texte sombre pour contraste */
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #ffcc00;
      text-shadow: 2px 2px 5px #ff5733;
      font-size: 40px;
      margin-bottom: 30px;
    }

    .question {
      margin: 20px 0;
      background-color: #fff;  /* Fond blanc pour les questions */
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
    }

    .options button {
      background-color: #ff6f61;
      color: #fff;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      box-shadow: 0 0 5px #ff5733;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #ff3b2e;
      transform: scale(1.1);
    }

    .result {
      background-color: #fff;  /* Fond blanc pour le résultat */
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(255, 204, 0, 0.7);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #ffcc00;
    }

    /* Retro animation for the title */
    @keyframes flicker {
      0% {
        opacity: 0.8;
      }
      50% {
        opacity: 1;
      }
      100% {
        opacity: 0.8;
      }
    }

    h1 {
      animation: flicker 1s infinite;
    }

    .question, .options button {
      font-family: 'Courier New', monospace;
      font-size: 18px;
    }

  </style>
</head>
<body>
  <h1>Quel personnage de DC êtes-vous ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <p class="score">Votre résultat est basé sur vos choix !</p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>

  <script>
    const questions = [
      {
        question: "Quelle est votre principale motivation ?",
        options: ["Justice", "Vengeance", "Liberté", "Protection des innocents"],
        result: [0, 1, 2, 3]  // Chaque index mène à un personnage différent
      },
      {
        question: "Quel est votre style de combat préféré ?",
        options: ["Tactique et intelligence", "Force brute", "Vitesse", "Stratégie et technologie"],
        result: [3, 1, 2, 0]
      },
      {
        question: "Quel type d'ennemi vous inspire le plus ?",
        options: ["Des criminels", "Des tyrans", "Des ennemis avec des pouvoirs surhumains", "Des extraterrestres"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Quel est votre plus grand défaut ?",
        options: ["Impulsivité", "Colère", "Doute", "Isolement"],
        result: [1, 0, 3, 2]
      },
      {
        question: "Si vous pouviez choisir un super pouvoir, lequel serait-ce ?",
        options: ["Vol", "Invulnérabilité", "Téléportation", "Super-force"],
        result: [2, 3, 0, 1]
      },
      {
        question: "Que faites-vous en cas de crise ?",
        options: ["Prendre le contrôle et organiser", "Agir sans réfléchir", "Chercher un allié", "Prendre du recul et réfléchir"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Votre principale qualité ?",
        options: ["Dévotion", "Détermination", "Courage", "Intelligence"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Comment gérez-vous les conflits ?",
        options: ["Par la force", "Par des compromis", "Par la diplomatie", "Par des stratégies astucieuses"],
        result: [1, 2, 3, 0]
      }
    ];

    const characters = [
      { name: "Batman", description: "Le détective et maître tacticien. Préfère la stratégie à la force brute." },
      { name: "Superman", description: "L'homme d'acier. Combattant impitoyable pour la justice et la paix." },
      { name: "Flash", description: "Le scarlet speedster. Vitesse incroyable et optimisme à toute épreuve." },
      { name: "Wonder Woman", description: "Princesse amazone. Combattante sans égal, protectrice des innocents." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;
      
      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';  // Clear previous options
      
      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];
      
      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    // Initialisation du quiz
    startQuiz();
  </script>
</body>
</html>
