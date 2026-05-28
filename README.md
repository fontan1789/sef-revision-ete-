<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quiz SEF 2024 – Situations réelles</title>
  <style>
    :root{
      --bg:#f3f6fb;
      --card:#ffffff;
      --text:#1f2a37;
      --muted:#64748b;
      --primary:#2563eb;
      --primary-dark:#1d4ed8;
      --ok:#16a34a;
      --bad:#dc2626;
      --border:#dbe4f0;
      --chip:#e8eefc;
      --shadow:0 10px 25px rgba(15, 23, 42, .08);
      --radius:18px;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background:linear-gradient(180deg,#eef4ff 0%,#f8fbff 100%);
      color:var(--text);
    }
    .app{
      max-width:860px;
      margin:0 auto;
      padding:16px 14px 40px;
    }
    .hero{
      background:var(--card);
      border:1px solid var(--border);
      border-radius:24px;
      padding:18px;
      box-shadow:var(--shadow);
      margin-bottom:16px;
    }
    h1{
      margin:0 0 8px;
      font-size:clamp(1.35rem, 3.2vw, 2rem);
      line-height:1.15;
    }
    .sub{
      color:var(--muted);
      font-size:.98rem;
      line-height:1.5;
    }
    .toolbar{
      display:flex;
      flex-wrap:wrap;
      gap:10px;
      margin-top:14px;
    }
    .chip{
      border:none;
      background:var(--chip);
      color:var(--text);
      padding:10px 14px;
      border-radius:999px;
      font-weight:700;
      cursor:pointer;
      transition:.2s;
    }
    .chip.active{
      background:var(--primary);
      color:#fff;
    }
    .panel{
      background:var(--card);
      border:1px solid var(--border);
      border-radius:24px;
      padding:16px;
      box-shadow:var(--shadow);
    }
    .topline{
      display:flex;
      justify-content:space-between;
      gap:12px;
      align-items:center;
      margin-bottom:10px;
      flex-wrap:wrap;
    }
    .badge{
      display:inline-flex;
      align-items:center;
      gap:8px;
      background:#eff6ff;
      color:#1d4ed8;
      border:1px solid #bfdbfe;
      font-weight:700;
      padding:8px 12px;
      border-radius:999px;
    }
    .progress-wrap{
      width:100%;
      background:#e5edf8;
      border-radius:999px;
      overflow:hidden;
      height:12px;
      margin:12px 0 8px;
    }
    .progress{
      height:100%;
      width:0%;
      background:linear-gradient(90deg, var(--primary), #60a5fa);
      transition:width .25s ease;
    }
    .meta{
      color:var(--muted);
      font-size:.95rem;
      margin-bottom:10px;
    }
    .scenario{
      background:#f8fbff;
      border:1px solid #dbeafe;
      border-radius:18px;
      padding:14px;
      font-size:1rem;
      line-height:1.6;
      margin:12px 0 16px;
    }
    .question{
      font-size:1.12rem;
      font-weight:800;
      margin-bottom:12px;
      line-height:1.4;
    }
    .answers{
      display:grid;
      gap:10px;
    }
    .answer{
      padding:14px;
      border:1px solid var(--border);
      border-radius:16px;
      background:#fff;
      text-align:left;
      font-size:1rem;
      cursor:pointer;
      transition:.18s;
      color:var(--text);
      font-weight:600;
    }
    .answer:hover{ transform:translateY(-1px); border-color:#93c5fd; }
    .answer.correct{
      background:#ecfdf5;
      border-color:#86efac;
      color:#166534;
    }
    .answer.wrong{
      background:#fef2f2;
      border-color:#fca5a5;
      color:#991b1b;
    }
    .feedback{
      margin-top:14px;
      padding:14px;
      border-radius:16px;
      line-height:1.6;
      display:none;
    }
    .feedback.show{ display:block; }
    .feedback.ok{
      background:#f0fdf4;
      border:1px solid #bbf7d0;
    }
    .feedback.bad{
      background:#fef2f2;
      border:1px solid #fecaca;
    }
    .comment{
      margin-top:8px;
      color:#374151;
    }
    .controls{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-top:18px;
    }
    .btn{
      flex:1 1 180px;
      padding:14px 16px;
      border:none;
      border-radius:16px;
      cursor:pointer;
      font-weight:800;
      font-size:1rem;
    }
    .btn-primary{
      background:var(--primary);
      color:white;
    }
    .btn-primary:hover{
      background:var(--primary-dark);
    }
    .btn-secondary{
      background:#e5edf8;
      color:#0f172a;
    }
    .scorecard{
      margin-top:18px;
      display:none;
      background:#f8fafc;
      border:1px solid var(--border);
      border-radius:18px;
      padding:16px;
    }
    .scorecard.show{ display:block; }
    .scoreline{
      font-size:1.15rem;
      font-weight:800;
      margin-bottom:8px;
    }
    .small{
      color:var(--muted);
      font-size:.95rem;
      line-height:1.5;
    }
    .footer-note{
      margin-top:16px;
      color:var(--muted);
      font-size:.92rem;
      line-height:1.5;
    }
  </style>
</head>
<body>
  <div class="app">
    <section class="hero">
      <h1>Quiz SEF 2024 – Situations réelles</h1>
      <div class="sub">
        Version mobile avec deux parcours : <strong>Niveau moyen</strong> et <strong>Niveau expert</strong>.
        Chaque question est une situation de table réaliste, avec correction immédiate et commentaire pédagogique.
      </div>
      <div class="toolbar">
        <button class="chip active" data-level="moyen">Niveau moyen</button>
        <button class="chip" data-level="expert">Niveau expert</button>
      </div>
    </section>

    <section class="panel">
      <div class="topline">
        <div class="badge" id="levelBadge">Mode : Niveau moyen</div>
        <div class="badge" id="scoreBadge">Score : 0</div>
      </div>

      <div class="progress-wrap">
        <div class="progress" id="progressBar"></div>
      </div>
      <div class="meta" id="metaLine">Question 1 / 12</div>

      <div class="scenario" id="scenarioBox"></div>
      <div class="question" id="questionBox"></div>
      <div class="answers" id="answersBox"></div>

      <div class="feedback" id="feedbackBox"></div>

      <div class="controls">
        <button class="btn btn-secondary" id="restartBtn">Recommencer</button>
        <button class="btn btn-primary" id="nextBtn" disabled>Question suivante</button>
      </div>

      <div class="scorecard" id="scoreCard"></div>

      <div class="footer-note">
        Astuce mobile : les boutons sont dimensionnés pour le tactile, et tu peux faire repasser un joueur sur le même niveau via « Recommencer ».
      </div>
    </section>
  </div>

  <script>
    const quizSets = {
      moyen: [
        {
          scenario: "Tournoi par paires. Vous êtes donneur, personne n’est intervenu. Votre main est régulière avec 16H.",
          question: "Quelle est l’ouverture correcte en SEF 2024 ?",
          answers: ["1♣", "1SA", "2SA", "2♣"],
          correct: 1,
          explanation: "1SA en SEF montre une main équilibrée de 15 à 17H. Avec 16H réguliers, l’ouverture correcte est 1SA."
        },
        {
          scenario: "Votre partenaire ouvre 1SA. Vous avez 5 cartes à cœur et une force quelconque.",
          question: "Quelle enchère standard devez-vous utiliser ?",
          answers: ["2♣ Stayman", "2♦ Texas pour les cœurs", "2♥ Texas pour les piques", "3♥ barrage"],
          correct: 1,
          explanation: "Sur 1SA, 2♦ est un Texas vers les cœurs. C’est la réponse standard avec 5+ cœurs, quelle que soit la force."
        },
        {
          scenario: "Votre partenaire ouvre 1SA. Vous n’avez pas encore trouvé de fit majeur et vous voulez savoir s’il possède une majeure quatrième.",
          question: "Quelle convention employez-vous ?",
          answers: ["4♣ Gerber", "2♣ Stayman", "2SA invitation", "4SA quantitatif"],
          correct: 1,
          explanation: "Le Stayman 2♣ sert à rechercher une majeure quatrième chez l’ouvreur de 1SA."
        },
        {
          scenario: "Votre partenaire ouvre 1♥. Vous avez 7H et 3 atouts cœur.",
          question: "Quelle réponse correspond au système ?",
          answers: ["1SA", "2♥", "2SA", "3♥"],
          correct: 1,
          explanation: "Après 1♥, la réponse 2♥ montre un soutien direct avec 3+ atouts et environ 6–9H."
        },
        {
          scenario: "Votre partenaire ouvre 1♥. Vous détenez 4 piques et 6H.",
          question: "Quelle est la réponse naturelle et forcing d’un tour ?",
          answers: ["1♠", "1SA", "2♠", "3♠"],
          correct: 0,
          explanation: "Après 1♥, 1♠ montre 4+ piques avec 6+H et force l’enchère pour un tour."
        },
        {
          scenario: "Votre partenaire ouvre 1♦. Vous avez une main régulière de 8H, sans majeure quatrième.",
          question: "Quelle réponse est correcte ?",
          answers: ["1SA", "2♣", "2♦", "2SA"],
          correct: 0,
          explanation: "Après 1♦, la réponse 1SA montre une main équilibrée de 7 à 10H sans majeure quatrième."
        },
        {
          scenario: "Votre camp ouvre un barrage de 2♠. Vous êtes fort et voulez demander la qualité de l’ouverture faible.",
          question: "Quelle enchère interrogative utilisez-vous ?",
          answers: ["3♣ Stayman", "2SA Ogust", "Contre", "4SA RKCB"],
          correct: 1,
          explanation: "Après un barrage de 2♥/2♠, l’enchère 2SA est la demande Ogust."
        },
        {
          scenario: "Votre partenaire ouvre 2♣ fort artificiel. Vous êtes faible, 0 à 7H, quelle que soit votre distribution.",
          question: "Quelle réponse négative devez-vous donner ?",
          answers: ["2♦", "2♥", "2SA", "3♣"],
          correct: 0,
          explanation: "Sur l’ouverture 2♣ forte artificielle, 2♦ est la réponse négative artificielle avec 0–7H."
        },
        {
          scenario: "Vous êtes donneur avec 20H réguliers.",
          question: "Quelle ouverture naturelle du SEF convient ?",
          answers: ["1SA", "2♣", "2SA", "3SA"],
          correct: 2,
          explanation: "2SA montre 20–21H réguliers dans ce système."
        },
        {
          scenario: "Partenaire a passé d’entrée, puis ouvre 1♠ en 3e position. Vous avez 11H et 3 cartes à pique.",
          question: "Quelle convention d’ajustement utilisez-vous ?",
          answers: ["2♣ Drury", "2♦ négatif", "2SA invitation", "3♠ barrage"],
          correct: 0,
          explanation: "En 3e/4e position après passe, 2♣ Drury montre 10–12H avec 3+ atouts en majeure."
        },
        {
          scenario: "Votre partenaire ouvre 1♣. Vous avez 5 carreaux et 11H.",
          question: "Quelle réponse est forcing de manche selon le tableau ?",
          answers: ["1♦", "2♦", "2♣", "1SA"],
          correct: 1,
          explanation: "Après 1♣, 2♦/2♥/2♠ montrent 5+ cartes et 10+H, forcing de manche."
        },
        {
          scenario: "Votre partenaire ouvre 1SA. Vous avez 9H réguliers, sans projet de fit majeur particulier.",
          question: "Quelle enchère d’invitation est indiquée ?",
          answers: ["2SA", "3SA", "4SA", "Passe"],
          correct: 0,
          explanation: "Après 1SA, 2SA est une invitation avec 8–9H équilibrés."
        }
      ],

      expert: [
        {
          scenario: "Séquence : 1♣ – 1♥ – 1♠ – ? Vous avez une main forte sans fit clair et vous voulez demander une description complémentaire.",
          question: "Quelle est la 4e couleur forcing dans cette séquence ?",
          answers: ["2♣", "2♦", "2♥", "2SA"],
          correct: 1,
          explanation: "Dans la séquence 1♣ – 1♥ – 1♠, l’enchère de 2♦ est la 4e couleur forcing."
        },
        {
          scenario: "Séquence compétitive : 1♦ – (1♥) – ?. Vous détenez 4 piques et 7+H.",
          question: "Quelle action du répondant correspond au tableau compétitif ?",
          answers: ["1♠ obligatoire", "Contre négatif", "2♠ barrage", "1SA"],
          correct: 1,
          explanation: "Après 1♦ – (1♥), le contre négatif montre notamment 4+ piques avec 7+H."
        },
        {
          scenario: "Séquence compétitive : 1♥ – (1♠) – ?. Vous avez un arrêt à pique et 10+H.",
          question: "Quel type d’enchère est prévu par le tableau ?",
          answers: ["Une enchère à Sans-Atout", "Un cue-bid forcé", "Un barrage", "Un Drury"],
          correct: 0,
          explanation: "Après 1♥ – (1♠), une enchère à SA montre un arrêt à pique et 10+H."
        },
        {
          scenario: "Votre camp a fixé l’atout et utilise RKCB 1430. Vous posez 4SA et votre partenaire répond 5♣.",
          question: "Que signifie exactement cette réponse ?",
          answers: ["0 ou 3 Key Cards", "1 ou 4 Key Cards", "2 Key Cards sans la Dame d’atout", "2 Key Cards avec la Dame d’atout"],
          correct: 1,
          explanation: "En RKCB 1430, la réponse 5♣ montre 1 ou 4 Key Cards."
        },
        {
          scenario: "L’adversaire ouvre 1♥. Vous intervenez par un cue-bid Michaels.",
          question: "Quelle distribution promettez-vous ?",
          answers: ["5+ cœurs et 5+ mineure", "5+ piques et 5+ mineure", "5+ piques et 5+ cœurs", "Une main régulière 15-18H"],
          correct: 1,
          explanation: "Sur 1♥, Michaels promet 5+ piques et 5+ mineure non précisée."
        },
        {
          scenario: "L’adversaire ouvre au palier de 1. Vous intervenez à 2SA selon l’Unusual Notrump.",
          question: "Que montrez-vous dans ce système ?",
          answers: ["Une main régulière avec arrêt", "Unicolore fort", "Bicolore 5-5 mineures", "Deux majeures"],
          correct: 2,
          explanation: "L’Unusual 2SA montre les deux mineures en 5-5."
        },
        {
          scenario: "Séquence : 1SA – 2♦ – 2♥ – 3SA.",
          question: "Que montre le répondant dans ce développement Texas ?",
          answers: ["6–7H et arrêt en cœur", "8–9H avec 6+ cœurs", "10+H avec 5 cœurs et choix partiel", "10+H avec 5 cœurs, laissant l’ouvreur choisir entre 3SA et 4♥"],
          correct: 3,
          explanation: "Dans cette séquence, 3SA montre 10+H avec 5 cœurs ; l’ouvreur choisit 3SA ou 4♥."
        },
        {
          scenario: "Séquence Drury : après passe, ouverture majeure en 3e/4e position, puis 2♣ Drury. L’ouvreur répond 2♦.",
          question: "Que signifie ce 2♦ dans le Drury inversé ?",
          answers: ["Ouverture standard 12-14H", "Ouverture légère, refuse la manche", "Main très forte", "Fit de 4 cartes obligatoire"],
          correct: 1,
          explanation: "En Drury inversé, 2♦ indique une ouverture légère et refuse la manche."
        },
        {
          scenario: "Après l’intervention adverse sur votre ouverture, l’ouvreur contre avec 15–17H et 3+ atouts en majeure pour son partenaire.",
          question: "Comment s’appelle ce contre ?",
          answers: ["Contre d’appel", "Contre négatif", "Contre de support", "Contre de pénalité"],
          correct: 2,
          explanation: "Le contre de support est défini par 3+ cartes de soutien en majeure et 15–17H."
        },
        {
          scenario: "Votre partenaire ouvre 2♦ forcing manche artificiel. Vous répondez 2♠.",
          question: "Quelle information précise donne cette réponse ?",
          answers: ["As de trèfle", "Deux As", "As d’une majeure non précisée", "6+ piques avec Roi-Dame sans As"],
          correct: 2,
          explanation: "Sur 2♦ forcing manche, 2♠ montre l’As d’une majeure, sans préciser laquelle."
        },
        {
          scenario: "Séquence Stayman : 1SA – 2♣ – 2♦. Le répondant poursuit par 2♥.",
          question: "Que montre ce 2♥ dans le tableau de développement ?",
          answers: ["Une simple préférence", "5 cœurs", "Un fit forcing à cœur", "Un contrôle pour le chelem"],
          correct: 1,
          explanation: "Après 1SA – 2♣ – 2♦ (pas de majeure 4e), 2♥ du répondant montre une majeure 5e, ici 5 cœurs."
        },
        {
          scenario: "Situation de sacrifice : vous êtes non vulnérable contre vulnérable, et l’adversaire vise une manche vulnérable valorisée à 600.",
          question: "Selon le tableau de la règle de 500, quelle perte maximale rend le sacrifice acceptable ?",
          answers: ["300", "420", "500", "620"],
          correct: 2,
          explanation: "Le tableau indique qu’en non-vulnérable contre vulnérable, le sacrifice est acceptable si les pertes restent inférieures à 500."
        }
      ]
    };

    let currentLevel = "moyen";
    let currentIndex = 0;
    let score = 0;
    let answered = false;

    const levelBadge = document.getElementById("levelBadge");
    const scoreBadge = document.getElementById("scoreBadge");
    const metaLine = document.getElementById("metaLine");
    const scenarioBox = document.getElementById("scenarioBox");
    const questionBox = document.getElementById("questionBox");
    const answersBox = document.getElementById("answersBox");
    const feedbackBox = document.getElementById("feedbackBox");
    const nextBtn = document.getElementById("nextBtn");
    const restartBtn = document.getElementById("restartBtn");
    const scoreCard = document.getElementById("scoreCard");
    const progressBar = document.getElementById("progressBar");
    const chips = document.querySelectorAll(".chip");

    function getCurrentSet(){
      return quizSets[currentLevel];
    }

    function renderQuestion(){
      const set = getCurrentSet();
      const item = set[currentIndex];

      answered = false;
      nextBtn.disabled = true;
      feedbackBox.className = "feedback";
      feedbackBox.innerHTML = "";
      scoreCard.className = "scorecard";

      levelBadge.textContent = currentLevel === "moyen" ? "Mode : Niveau moyen" : "Mode : Niveau expert";
      scoreBadge.textContent = "Score : " + score;
      metaLine.textContent = `Question ${currentIndex + 1} / ${set.length}`;
      scenarioBox.innerHTML = "<strong>Situation :</strong> " + item.scenario;
      questionBox.textContent = item.question;
      answersBox.innerHTML = "";

      item.answers.forEach((ans, idx) => {
        const btn = document.createElement("button");
        btn.className = "answer";
        btn.textContent = ans;
        btn.addEventListener("click", () => selectAnswer(idx));
        answersBox.appendChild(btn);
      });

      const pct = ((currentIndex) / set.length) * 100;
      progressBar.style.width = pct + "%";
    }

    function selectAnswer(index){
      if(answered) return;
      answered = true;

      const set = getCurrentSet();
      const item = set[currentIndex];
      const buttons = [...document.querySelectorAll(".answer")];

      buttons.forEach((btn, idx) => {
        if(idx === item.correct) btn.classList.add("correct");
        if(idx === index && idx !== item.correct) btn.classList.add("wrong");
        btn.disabled = true;
      });

      const ok = index === item.correct;
      if(ok) score++;

      scoreBadge.textContent = "Score : " + score;
      feedbackBox.className = `feedback show ${ok ? "ok" : "bad"}`;
      feedbackBox.innerHTML = `
        <strong>${ok ? "✅ Bonne réponse" : "❌ Réponse incorrecte"}</strong>
        <div class="comment">${item.explanation}</div>
      `;

      nextBtn.disabled = false;
      const pct = ((currentIndex + 1) / set.length) * 100;
      progressBar.style.width = pct + "%";
    }

    function nextQuestion(){
      const set = getCurrentSet();
      currentIndex++;
      if(currentIndex >= set.length){
        showFinalScore();
      } else {
        renderQuestion();
      }
    }

    function showFinalScore(){
      const set = getCurrentSet();
      const percent = Math.round((score / set.length) * 100);
      let mention = "À retravailler";
      if(percent >= 85) mention = "Excellent niveau";
      else if(percent >= 65) mention = "Bon niveau";
      else if(percent >= 50) mention = "Base solide mais perfectible";

      scenarioBox.innerHTML = "Parcours terminé.";
      questionBox.textContent = "Résultat final";
      answersBox.innerHTML = "";
      feedbackBox.className = "feedback";
      feedbackBox.innerHTML = "";
      nextBtn.disabled = true;

      scoreCard.className = "scorecard show";
      scoreCard.innerHTML = `
        <div class="scoreline">${score} / ${set.length} — ${percent}%</div>
        <div class="small">${mention}</div>
        <div class="small" style="margin-top:8px;">
          Conseil : refais le mode expert après plusieurs passages sur le mode moyen pour automatiser Stayman, Texas, 2/1, Drury, 4CF et les enchères compétitives.
        </div>
      `;
    }

    function restartQuiz(){
      currentIndex = 0;
      score = 0;
      renderQuestion();
    }

    chips.forEach(chip => {
      chip.addEventListener("click", () => {
        chips.forEach(c => c.classList.remove("active"));
        chip.classList.add("active");
        currentLevel = chip.dataset.level;
        restartQuiz();
      });
    });

    nextBtn.addEventListener("click", nextQuestion);
    restartBtn.addEventListener("click", restartQuiz);

    renderQuestion();
  </script>
</body>
</html>
