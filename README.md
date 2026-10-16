
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Missão Matemática</title>
<style>
:root {
  --bg: #f4f1ff;
  --surface: #ffffff;
  --text: #262044;
  --muted: #665f82;
  --accent: #7048d8;
  --accent2: #4f2caf;
  --border: #e3dcfa;
  --good: #18794e;
  --bad: #b42336;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}
.app { min-height: 100vh; padding: 28px 16px 40px; }
header {
  max-width: 960px; margin: 0 auto 24px;
  display: flex; align-items: center;
  justify-content: space-between; gap: 16px;
}
.brand { display: flex; align-items: center; gap: 12px; font-weight: bold; }
.logo {
  width: 48px; height: 48px; display: grid;
  place-items: center; background: var(--accent);
  color: white; border-radius: 15px; font-size: 25px;
}
.tag { color: var(--muted); font-size: 13px; }
.layout {
  max-width: 960px; margin: auto;
  display: grid; grid-template-columns: .8fr 1.2fr; gap: 20px;
}
.intro, .quiz {
  border: 1px solid var(--border); border-radius: 24px;
  background: var(--surface); padding: 30px;
}
.eyebrow {
  text-transform: uppercase; letter-spacing: 1.5px;
  font-size: 12px; color: var(--accent); font-weight: bold;
}
h1 { font-size: clamp(30px, 5vw, 44px); line-height: 1.05; }
p { line-height: 1.6; }
.intro p { color: var(--muted); }
.stats { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 24px; }
.stat { border: 1px solid var(--border); border-radius: 15px; padding: 14px; }
.stat strong { display: block; font-size: 24px; }
.stat span { color: var(--muted); font-size: 12px; }
.topline { display: flex; justify-content: space-between; margin-bottom: 12px; color: var(--muted); }
.progress { height: 8px; background: var(--border); border-radius: 99px; overflow: hidden; margin-bottom: 26px; }
.bar { height: 100%; width: 0%; background: var(--accent); transition: width .25s; }
.question { font-size: 24px; font-weight: bold; line-height: 1.4; min-height: 70px; }
.answers { display: grid; gap: 10px; margin: 22px 0 16px; }
.answer {
  width: 100%; text-align: left; background: white; color: var(--text);
  border: 1px solid var(--border); padding: 15px;
  border-radius: 14px; font-size: 16px; cursor: pointer;
}
.answer:hover:not(:disabled) { border-color: var(--accent); background: #f4f0ff; }
.answer.correct { border-color: var(--good); background: #e8f8ef; }
.answer.wrong { border-color: var(--bad); background: #fff0f1; }
.answer:disabled { cursor: default; }
.feedback { min-height: 48px; color: var(--muted); line-height: 1.5; }
.feedback.good { color: var(--good); }
.feedback.bad { color: var(--bad); }
.actions { display: flex; gap: 10px; flex-wrap: wrap; }
.primary {
  border: 0; border-radius: 13px; padding: 13px 18px;
  background: var(--accent); color: white; font-weight: bold;
  font-size: 15px; cursor: pointer;
}
.primary:hover { background: var(--accent2); }
.primary:disabled { opacity: .45; cursor: not-allowed; }
.hidden { display: none !important; }
.result { text-align: center; padding: 16px 0; }
.trophy { font-size: 54px; }
.result-score { font-size: 42px; font-weight: bold; color: var(--accent); margin: 8px 0; }
footer { max-width: 960px; margin: 18px auto 0; text-align: center; color: var(--muted); font-size: 12px; }
@media (max-width: 720px) {
  .layout { grid-template-columns: 1fr; }
  header { align-items: flex-start; }
  .intro, .quiz { padding: 24px; }
}
</style>
</head>
<body>
<div class="app">
  <header>
    <div class="brand">
      <div class="logo">🚀</div>
      <div>Missão Matemática<div class="tag">Aprender brincando</div></div>
    </div>
    <div class="tag">QUIZ EDUCATIVO · 7 DESAFIOS</div>
  </header>

  <main class="layout">
    <section class="intro">
      <div class="eyebrow">Sua missão começa agora</div>
      <h1>Teste seus conhecimentos.</h1>
      <p>Responda às perguntas, descubra curiosidades matemáticas e conquiste pontos. Cada resposta correta vale 10 pontos!</p>
      <div class="stats">
        <div class="stat"><strong id="scoreStat">0</strong><span>PONTOS</span></div>
        <div class="stat"><strong id="progressStat">0/7</strong><span>RESPONDIDAS</span></div>
      </div>
      <p><strong>Matérias:</strong><br>Operações, geometria, porcentagem e descontos.</p>
    </section>

    <section class="quiz" aria-live="polite">
      <div id="quizView">
        <div class="topline">
          <span id="stepLabel">DESAFIO 1 DE 7</span>
          <span>⭐ <strong id="scoreLabel">0</strong> pontos</span>
        </div>
        <div class="progress"><div class="bar" id="progressBar"></div></div>
        <div class="question" id="question"></div>
        <div class="answers" id="answers"></div>
        <div class="feedback" id="feedback" role="status">Escolha uma resposta para continuar.</div>
        <div class="actions">
          <button class="primary" id="nextBtn" disabled>Próximo desafio →</button>
        </div>
      </div>

      <div id="resultView" class="result hidden">
        <div class="trophy">🏆</div>
        <h2>Missão concluída!</h2>
        <p>Você terminou todos os desafios.</p>
        <div class="result-score" id="finalScore">0/70</div>
        <p id="resultMessage"></p>
        <button class="primary" id="restartBtn">Jogar novamente ↻</button>
      </div>
    </section>
  </main>
  <footer>Uma Viagem Virtual pela Matemática · Ciência e tecnologia na educação</footer>
</div>

<script>
const questions = [
  { q: 'Quanto é 8 × 7?', options: ['54', '56', '64'], correct: 1, explain: '8 × 7 = 56.' },
  { q: 'Quantos lados tem um triângulo?', options: ['3', '4', '5'], correct: 0, explain: 'Um triângulo tem 3 lados e 3 vértices.' },
  { q: 'Quanto é 100 ÷ 4?', options: ['20', '25', '40'], correct: 1, explain: '100 dividido por 4 é 25.' },
  { q: 'Quanto é 50% de 80?', options: ['20', '30', '40'], correct: 2, explain: '50% significa metade. A metade de 80 é 40.' },
  { q: 'Quantas faces tem um cubo?', options: ['4', '6', '8'], correct: 1, explain: 'Um cubo tem 6 faces, 12 arestas e 8 vértices.' },
  { q: 'Quanto é 15 + 27?', options: ['32', '42', '52'], correct: 1, explain: '15 + 27 = 42.' },
  { q: 'Um produto custa R$ 60 e tem 10% de desconto. Qual é o preço final?', options: ['R$ 50', 'R$ 54', 'R$ 56'], correct: 1, explain: '10% de R$ 60 é R$ 6. Então, R$ 60 − R$ 6 = R$ 54.' }
];

let current = 0;
let score = 0;
let answered = 0;
let locked = false;
const $ = id => document.getElementById(id);

function renderQuestion() {
  locked = false;
  const item = questions[current];
  $('stepLabel').textContent = `DESAFIO ${current + 1} DE ${questions.length}`;
  $('question').textContent = item.q;
  $('answers').innerHTML = '';
  $('feedback').textContent = 'Escolha uma resposta para continuar.';
  $('feedback').className = 'feedback';
  $('nextBtn').disabled = true;
  $('nextBtn').textContent = current === questions.length - 1 ? 'Ver resultado →' : 'Próximo desafio →';

  item.options.forEach((option, index) => {
    const button = document.createElement('button');
    button.className = 'answer';
    button.textContent = `${String.fromCharCode(65 + index)}. ${option}`;
    button.addEventListener('click', () => chooseAnswer(index));
    $('answers').appendChild(button);
  });
  updateStats();
}

function chooseAnswer(index) {
  if (locked) return;
  locked = true;
  answered++;
  const item = questions[current];
  const buttons = [...$('answers').querySelectorAll('button')];

  buttons.forEach((button, i) => {
    button.disabled = true;
    if (i === item.correct) button.classList.add('correct');
    else if (i === index) button.classList.add('wrong');
  });

  if (index === item.correct) {
    score += 10;
    $('feedback').textContent = `Correto! +10 pontos. ${item.explain}`;
    $('feedback').className = 'feedback good';
  } else {
    $('feedback').textContent = `Quase! ${item.explain}`;
    $('feedback').className = 'feedback bad';
  }

  $('nextBtn').disabled = false;
  updateStats();
}

function updateStats() {
  $('scoreStat').textContent = score;
  $('scoreLabel').textContent = score;
  $('progressStat').textContent = `${answered}/${questions.length}`;
  $('progressBar').style.width = `${(answered / questions.length) * 100}%`;
}

function next() {
  if (!locked) return;
  if (current < questions.length - 1) {
    current++;
    renderQuestion();
  } else {
    $('quizView').classList.add('hidden');
    $('resultView').classList.remove('hidden');
    $('finalScore').textContent = `${score}/70 pontos`;
    $('resultMessage').textContent = score === 70
      ? 'Perfeito! Você acertou todas as perguntas!'
      : score >= 40
      ? 'Muito bem! Continue praticando para dominar a Matemática.'
      : 'Boa tentativa! Jogue novamente e pratique seus conhecimentos.';
  }
}

function restart() {
  current = 0;
  score = 0;
  answered = 0;
  $('quizView').classList.remove('hidden');
  $('resultView').classList.add('hidden');
  renderQuestion();
}

$('nextBtn').addEventListener('click', next);
$('restartBtn').addEventListener('click', restart);
renderQuestion();
</script>
</body>
</html>

