```javascript
/* ==========================================================
HADRON MATCH-UP
app.js
PART 1
==========================================================*/

/* ==========================================================
Global Variables
==========================================================*/

let currentQuestion = 0;
let score = 0;
let playerName = "";
let leaderboard = [];
let feedback = [];

/* ==========================================================
DOM Elements
==========================================================*/

const landingPage = document.getElementById("landingPage");
const registerPage = document.getElementById("registerPage");
const quizPage = document.getElementById("quizPage");
const resultPage = document.getElementById("resultPage");
const leaderboardPage = document.getElementById("leaderboardPage");
const feedbackPage = document.getElementById("feedbackPage");
const certificatePage = document.getElementById("certificatePage");

const startBtn = document.getElementById("startBtn");
const continueBtn = document.getElementById("continueBtn");
const leaderboardBtn = document.getElementById("leaderboardBtn");
const feedbackBtn = document.getElementById("feedbackBtn");
const certificateBtn = document.getElementById("certificateBtn");
const playAgainBtn = document.getElementById("playAgainBtn");

const backResultBtn = document.getElementById("backResultBtn");
const backResultBtn2 = document.getElementById("backResultBtn2");

const playerNameInput = document.getElementById("playerName");

const displayPlayer = document.getElementById("displayPlayer");
const scoreDisplay = document.getElementById("score");

const progressBar = document.getElementById("progress");
const progressText = document.getElementById("progressText");

const questionText = document.getElementById("questionText");
const answerButtons = document.getElementById("answerButtons");
const feedbackMessage = document.getElementById("feedback");
const nextBtn = document.getElementById("nextBtn");

const resultName = document.getElementById("resultName");
const resultScore = document.getElementById("resultScore");
const resultPercent = document.getElementById("resultPercent");
const resultRank = document.getElementById("resultRank");

const leaderboardBody = document.getElementById("leaderboardBody");

const feedbackForm = document.getElementById("feedbackForm");

const certName = document.getElementById("certName");
const certScore = document.getElementById("certScore");
const certRank = document.getElementById("certRank");
const certDate = document.getElementById("certDate");

const downloadCertBtn = document.getElementById("downloadCertBtn");

/* ==========================================================
Navigation
==========================================================*/

const pages = [
landingPage,
registerPage,
quizPage,
resultPage,
leaderboardPage,
feedbackPage,
certificatePage
];

function showPage(page){

pages.forEach(p => p.classList.remove("active"));

page.classList.add("active");

}

/* ==========================================================
Rank
==========================================================*/

function getRank(score){

if(score <= 5)
return "Quark Apprentice";

if(score <= 10)
return "Hadron Builder";

if(score <= 15)
return "Particle Expert";

if(score <= 19)
return "Accelerator Master";

return "Quark Grandmaster";

}

/* ==========================================================
Animated Particle Background
==========================================================*/

function createParticles(){

const container = document.getElementById("particles");

if(!container) return;

container.innerHTML = "";

for(let i=0;i<40;i++){

const particle = document.createElement("div");

particle.className = "particle";

particle.style.left = Math.random()*100 + "%";

particle.style.animationDuration =
(6 + Math.random()*8) + "s";

particle.style.animationDelay =
Math.random()*5 + "s";

particle.style.opacity =
Math.random();

particle.style.transform =
`scale(${0.5 + Math.random()*1.5})`;

container.appendChild(particle);

}

}

createParticles();

/* ==========================================================
Questions
==========================================================*/

const questions = [

{
question:"Proton consists of:",
options:["A udd","B uud","C uds","D uus"],
answer:1
},

{
question:"Neutron consists of:",
options:["A udd","B uud","C uds","D ddd"],
answer:0
},

{
question:"Which particle contains uud?",
options:["A Proton","B Neutron","C Lambda","D Sigma−"],
answer:0
},

{
question:"Which particle contains udd?",
options:["A Proton","B Neutron","C Xi⁰","D Omega−"],
answer:1
},

{
question:"Lambda (Λ⁰):",
options:["A uus","B uds","C dss","D uss"],
answer:1
},

{
question:"Sigma⁺:",
options:["A uus","B uds","C uss","D dss"],
answer:0
},

{
question:"Sigma−:",
options:["A uus","B uds","C dds","D dss"],
answer:2
},

{
question:"Xi⁰:",
options:["A uss","B dss","C uds","D uus"],
answer:0
},

{
question:"Xi−:",
options:["A uus","B uss","C dss","D sss"],
answer:2
},

{
question:"Omega−:",
options:["A dss","B uss","C uds","D sss"],
answer:3
},

{
question:"π⁺:",
options:["A uū","B ud̄","C dū","D ss̄"],
answer:1
},

{
question:"π−:",
options:["A ud̄","B dū","C uū","D dd̄"],
answer:1
},

{
question:"K⁺:",
options:["A us̄","B sū","C ds̄","D sd̄"],
answer:0
},

{
question:"K−:",
options:["A us̄","B ds̄","C sū","D sd̄"],
answer:2
},

{
question:"K⁰:",
options:["A ds̄","B sd̄","C uū","D dd̄"],
answer:0
},

{
question:"Which is a baryon?",
options:["A ud̄","B uū","C uds","D cū"],
answer:2
},

{
question:"Which is a meson?",
options:["A uud","B uds","C uss","D cc̄"],
answer:3
},

{
question:"Three quarks form a:",
options:["A Lepton","B Meson","C Baryon","D Boson"],
answer:2
},

{
question:"One quark and one antiquark form a:",
options:["A Baryon","B Meson","C Lepton","D Fermion"],
answer:1
},

{
question:"Which is NOT a valid hadron?",
options:["A uud","B ud̄","C uds","D uu"],
answer:3
}

];

/* ==========================================================
Event Listeners
==========================================================*/

startBtn.addEventListener("click",()=>{

showPage(registerPage);

});

continueBtn.addEventListener("click",()=>{

playerName = playerNameInput.value.trim();

if(playerName===""){

alert("Please enter your name.");

return;

}

displayPlayer.textContent = playerName;

showPage(quizPage);

// Part 2 begins here:
// loadQuestion();

});

leaderboardBtn.addEventListener("click",()=>{

showPage(leaderboardPage);

});

feedbackBtn.addEventListener("click",()=>{

showPage(feedbackPage);

});

certificateBtn.addEventListener("click",()=>{

showPage(certificatePage);

});

backResultBtn.addEventListener("click",()=>{

showPage(resultPage);

});

backResultBtn2.addEventListener("click",()=>{

showPage(resultPage);

});

playAgainBtn.addEventListener("click",()=>{

currentQuestion = 0;
score = 0;
playerName = "";

playerNameInput.value = "";

scoreDisplay.textContent = "0";

progressBar.style.width = "0%";

progressText.textContent = "Question 1 of 20";

showPage(registerPage);

});

/* ==========================================================
END OF PART 1
PART 2 STARTS WITH:
function loadQuestion()
==========================================================*/
```
```javascript
/* ==========================================================
PART 2
Quiz Engine
==========================================================*/

function loadQuestion() {

nextBtn.style.display = "none";
feedbackMessage.textContent = "";
feedbackMessage.className = "feedback";

const q = questions[currentQuestion];

questionText.textContent = q.question;

answerButtons.innerHTML = "";

progressBar.style.width = `${((currentQuestion + 1) / questions.length) * 100}%`;
progressText.textContent = `Question ${currentQuestion + 1} of ${questions.length}`;

scoreDisplay.textContent = score;

q.options.forEach((option, index) => {

const button = document.createElement("button");

button.className = "answer-btn";
button.textContent = option;

button.addEventListener("click", () => {

selectAnswer(button, index);

});

answerButtons.appendChild(button);

});

}

function selectAnswer(selectedButton, selectedIndex) {

const q = questions[currentQuestion];

const buttons = document.querySelectorAll(".answer-btn");

buttons.forEach(btn => btn.disabled = true);

if (selectedIndex === q.answer) {

selectedButton.classList.add("correct");

feedbackMessage.textContent = "✅ Correct!";
feedbackMessage.classList.add("correct");

score++;

scoreDisplay.textContent = score;

} else {

selectedButton.classList.add("wrong");

buttons[q.answer].classList.add("correct");

feedbackMessage.textContent = "❌ Incorrect!";
feedbackMessage.classList.add("wrong");

}

nextBtn.style.display = "block";

}

nextBtn.addEventListener("click", () => {

currentQuestion++;

if (currentQuestion < questions.length) {

loadQuestion();

} else {

endQuiz();

}

});

function endQuiz() {

showPage(resultPage);

const percentage = Math.round((score / questions.length) * 100);

const rank = getRank(score);

resultName.textContent = playerName;
resultScore.textContent = score;
resultPercent.textContent = percentage;
resultRank.textContent = rank;

const record = {

player_name: playerName,
score: score,
rank: rank,
date: new Date().toLocaleDateString()

};

const existing = JSON.parse(localStorage.getItem("leaderboard")) || [];

existing.push(record);

localStorage.setItem(
"leaderboard",
JSON.stringify(existing)
);

}
```
```javascript
/* ==========================================================
PART 3
Leaderboard, Feedback, Certificate
==========================================================*/

/* ==========================================================
Leaderboard
==========================================================*/

function loadLeaderboard() {

leaderboardBody.innerHTML = "";

const leaderboard =
JSON.parse(localStorage.getItem("leaderboard")) || [];

leaderboard.sort((a, b) => b.score - a.score);

leaderboard.slice(0, 10).forEach((player, index) => {

const row = document.createElement("tr");

row.innerHTML = `
<td>${index + 1}</td>
<td>${player.player_name}</td>
<td>${player.score}</td>
<td>${player.rank}</td>
<td>${player.date}</td>
`;

leaderboardBody.appendChild(row);

});

}

leaderboardBtn.addEventListener("click", () => {

loadLeaderboard();

showPage(leaderboardPage);

});


/* ==========================================================
Feedback
==========================================================*/

feedbackForm.addEventListener("submit", function (e) {

e.preventDefault();

const selects = feedbackForm.querySelectorAll("select");

const record = {

interface: selects[0].value,
relevance: selects[1].value,
understanding: selects[2].value,
recommendation: selects[3].value,
date: new Date().toLocaleDateString()

};

const allFeedback =
JSON.parse(localStorage.getItem("feedback")) || [];

allFeedback.push(record);

localStorage.setItem(
"feedback",
JSON.stringify(allFeedback)
);

alert("Thank you for your feedback!");

feedbackForm.reset();

showPage(resultPage);

});


/* ==========================================================
Certificate
==========================================================*/

function populateCertificate() {

certName.textContent = playerName;

certScore.textContent = score;

certRank.textContent = getRank(score);

certDate.textContent = new Date().toLocaleDateString();

}

certificateBtn.addEventListener("click", () => {

populateCertificate();

showPage(certificatePage);

});


/* ==========================================================
Download Certificate
==========================================================*/

downloadCertBtn.addEventListener("click", () => {

html2canvas(document.getElementById("certificate"))

.then(canvas => {

const link = document.createElement("a");

link.download = "certificate.png";

link.href = canvas.toDataURL("image/png");

link.click();

});

});


/* ==========================================================
Play Again
==========================================================*/

playAgainBtn.addEventListener("click", () => {

currentQuestion = 0;

score = 0;

playerName = "";

feedbackMessage.textContent = "";

feedbackMessage.className = "feedback";

answerButtons.innerHTML = "";

questionText.textContent = "";

scoreDisplay.textContent = "0";

progressBar.style.width = "0%";

progressText.textContent = "Question 1 of 20";

playerNameInput.value = "";

nextBtn.style.display = "none";

showPage(registerPage);

});


/* ==========================================================
Helper Functions
==========================================================*/

function resetQuiz() {

currentQuestion = 0;

score = 0;

scoreDisplay.textContent = "0";

progressBar.style.width = "0%";

progressText.textContent = "Question 1 of 20";

answerButtons.innerHTML = "";

feedbackMessage.textContent = "";

nextBtn.style.display = "none";

}

window.addEventListener("load", () => {

showPage(landingPage);

createParticles();

});


/* ==========================================================
END OF app.js
==========================================================*/
```


