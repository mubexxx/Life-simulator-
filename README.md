# Life-simulator-
An interactive life simulator that shows how small daily decisions can add up over time.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>What If? — Life Simulator</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  min-height: 100vh;
  color: white;
  background:
    radial-gradient(circle at 10% 10%, #243b80, transparent 35%),
    radial-gradient(circle at 90% 90%, #421b70, transparent 35%),
    #070a15;
  padding: 15px;
}

.container {
  width: 100%;
  max-width: 950px;
  margin: auto;
}

/* HEADER */

header {
  text-align: center;
  padding: 35px 10px;
}

.logo {
  display: inline-block;
  padding: 8px 15px;
  border-radius: 50px;
  background: rgba(255,255,255,.07);
  border: 1px solid rgba(255,255,255,.15);
  font-size: 12px;
  letter-spacing: 3px;
  margin-bottom: 18px;
}

h1 {
  font-size: clamp(45px, 12vw, 80px);
  margin-bottom: 12px;
}

.gradient {
  background: linear-gradient(90deg,#6ee7ff,#9b7cff,#ff72d2);
  -webkit-background-clip: text;
  color: transparent;
}

header p {
  color: #aeb5d0;
  line-height: 1.6;
}

/* CARDS */

.card {
  background: rgba(255,255,255,.06);
  border: 1px solid rgba(255,255,255,.12);
  border-radius: 24px;
  padding: 22px;
  margin-bottom: 18px;
  backdrop-filter: blur(20px);
  box-shadow: 0 20px 60px rgba(0,0,0,.25);
}

.card h2 {
  margin-bottom: 18px;
}

/* DAILY CHALLENGE */

.challenge {
  border: 1px solid rgba(124,140,255,.4);
  background: linear-gradient(
    135deg,
    rgba(88,101,242,.16),
    rgba(155,92,255,.08)
  );
}

.challenge-title {
  font-size: 13px;
  color: #8e9aff;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 10px;
}

.challenge h2 {
  margin-bottom: 8px;
}

.challenge p {
  color: #adb4d0;
  line-height: 1.5;
}

.challenge button {
  margin-top: 15px;
}

/* BUTTONS */

button {
  font-family: inherit;
}

.primary {
  width: 100%;
  border: none;
  border-radius: 14px;
  padding: 15px;
  color: white;
  background: linear-gradient(90deg,#5865f2,#9b5cff);
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  transition: .25s;
}

.primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(100,90,255,.35);
}

.secondary {
  width: 100%;
  padding: 13px;
  border-radius: 13px;
  border: 1px solid rgba(255,255,255,.15);
  background: rgba(255,255,255,.06);
  color: white;
  cursor: pointer;
}

/* SCENARIOS */

.scenarios {
  display: grid;
  grid-template-columns: repeat(2,1fr);
  gap: 12px;
}

.scenario {
  padding: 17px;
  border-radius: 16px;
  border: 1px solid rgba(255,255,255,.1);
  background: rgba(255,255,255,.04);
  color: white;
  cursor: pointer;
  text-align: left;
  transition: .25s;
}

.scenario:hover {
  transform: translateY(-3px);
}

.scenario.active {
  border-color: #7886ff;
  background: rgba(120,134,255,.15);
}

.icon {
  font-size: 25px;
  display: block;
  margin-bottom: 8px;
}

.scenario strong {
  display: block;
  margin-bottom: 5px;
}

.scenario small {
  color: #9da5c2;
}

/* INPUTS */

.input-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}

.input-group {
  margin-bottom: 18px;
}

label {
  display: block;
  color: #cbd1e8;
  font-size: 14px;
  margin-bottom: 8px;
}

input,
select {
  width: 100%;
  padding: 15px;
  border-radius: 13px;
  border: 1px solid rgba(255,255,255,.12);
  background: rgba(0,0,0,.25);
  color: white;
  outline: none;
  font-size: 16px;
}

select option {
  background: #101426;
}

/* RESULT */

.result {
  display: none;
}

.result.show {
  display: block;
  animation: appear .5s ease;
}

@keyframes appear {
  from {
    opacity: 0;
    transform: translateY(15px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.big-number {
  text-align: center;
  font-size: clamp(42px,12vw,80px);
  font-weight: bold;
  margin: 15px 0;
  background: linear-gradient(90deg,#6ee7ff,#a477ff);
  -webkit-background-clip: text;
  color: transparent;
}

.result-description {
  text-align: center;
  color: #aeb5d0;
  line-height: 1.6;
}

.stats {
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 10px;
  margin-top: 22px;
}

.stat {
  padding: 17px;
  text-align: center;
  background: rgba(255,255,255,.05);
  border-radius: 15px;
}

.stat-number {
  font-size: 21px;
  font-weight: bold;
}

.stat-label {
  font-size: 10px;
  color: #929ab7;
  margin-top: 5px;
}

/* TIMELINE */

.timeline {
  margin-top: 30px;
  position: relative;
}

.timeline::before {
  content: "";
  position: absolute;
  left: 13px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: rgba(255,255,255,.12);
}

.timeline-item {
  position: relative;
  padding-left: 45px;
  margin-bottom: 25px;
}

.dot {
  position: absolute;
  left: 6px;
  top: 4px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #7886ff;
  box-shadow: 0 0 20px rgba(120,134,255,.7);
}

.timeline-item p {
  color: #aeb5d0;
  font-size: 14px;
  margin-top: 5px;
}

/* DASHBOARD */

.dashboard {
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 12px;
}

.dashboard-box {
  padding: 18px;
  text-align: center;
  border-radius: 16px;
  background: rgba(255,255,255,.05);
}

.dashboard-icon {
  font-size: 25px;
  margin-bottom: 8px;
}

.dashboard-number {
  font-size: 22px;
  font-weight: bold;
}

.dashboard-label {
  color: #8f97b5;
  font-size: 11px;
  margin-top: 5px;
}

/* ACHIEVEMENTS */

.achievements {
  display: grid;
  grid-template-columns: repeat(2,1fr);
  gap: 10px;
}

.badge {
  padding: 15px;
  border-radius: 15px;
  background: rgba(255,255,255,.04);
  border: 1px solid rgba(255,255,255,.08);
  opacity: .35;
}

.badge.unlocked {
  opacity: 1;
  border-color: rgba(124,140,255,.5);
}

.badge-icon {
  font-size: 25px;
  margin-bottom: 6px;
}

.badge strong {
  display: block;
  margin-bottom: 4px;
}

.badge small {
  color: #999fba;
}

/* SHARE */

.share-area {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin-top: 20px;
}

/* FOOTER */

footer {
  text-align: center;
  padding: 30px 10px;
  color: #737b99;
  font-size: 13px;
  line-height: 1.7;
}

.creator {
  color: #aeb5ff;
  font-weight: bold;
}

/* MOBILE */

@media(max-width:600px) {

  body {
    padding: 10px;
  }

  .card {
    padding: 18px;
  }

  .scenarios,
  .input-row,
  .dashboard,
  .achievements {
    grid-template-columns: 1fr;
  }

  .stats {
    grid-template-columns: 1fr;
  }

  .share-area {
    grid-template-columns: 1fr;
  }
}
</style>
</head>

<body>

<div class="container">

<header>

  <div class="logo">LIFE SIMULATOR v2</div>

  <h1>
    What <span class="gradient">If?</span>
  </h1>

  <p>
    Your future is built from small decisions.
    Simulate them and see where they could lead.
  </p>

</header>


<!-- DAILY CHALLENGE -->

<div class="card challenge">

  <div class="challenge-title">
    🎯 Daily Challenge
  </div>

  <h2 id="challengeText">
    What if you saved ₦500 every day for one year?
  </h2>

  <p>
    Complete today's simulation and keep building your streak.
  </p>

  <button class="primary" onclick="dailyChallenge()">
    🚀 Try Today's Challenge
  </button>

</div>


<!-- STREAK -->

<div class="card">

  <h2>🔥 Your Streak</h2>

  <div class="dashboard">

    <div class="dashboard-box">
      <div class="dashboard-icon">🔥</div>
      <div class="dashboard-number" id="streak">0</div>
      <div class="dashboard-label">DAY STREAK</div>
    </div>

    <div class="dashboard-box">
      <div class="dashboard-icon">🧠</div>
      <div class="dashboard-number" id="simulations">0</div>
      <div class="dashboard-label">SIMULATIONS</div>
    </div>

    <div class="dashboard-box">
      <div class="dashboard-icon">🏆</div>
      <div class="dashboard-number" id="badgeCount">0</div>
      <div class="dashboard-label">BADGES</div>
    </div>

  </div>

</div>


<!-- SCENARIOS -->

<div class="card">

  <h2>Choose Your Future</h2>

  <div class="scenarios">

    <button class="scenario active" data-type="money">

      <span class="icon">💰</span>

      <strong>Save Money</strong>

      <small>Watch your savings grow.</small>

    </button>


    <button class="scenario" data-type="study">

      <span class="icon">📚</span>

      <strong>Study</strong>

      <small>See your study time accumulate.</small>

    </button>


    <button class="scenario" data-type="coding">

      <span class="icon">💻</span>

      <strong>Learn Coding</strong>

      <small>Track your coding hours.</small>

    </button>


    <button class="scenario" data-type="exercise">

      <span class="icon">🏃</span>

      <strong>Exercise</strong>

      <small>Track your activity.</small>

    </button>


    <button class="scenario" data-type="reading">

      <span class="icon">📖</span>

      <strong>Reading</strong>

      <small>See how much you can read.</small>

    </button>


    <button class="scenario" data-type="creative">

      <span class="icon">🎨</span>

      <strong>Creativity</strong>

      <small>Build creative practice time.</small>

    </button>

  </div>

</div>


<!-- RANDOM SCENARIO -->

<div class="card">

  <h2>🎲 Feeling Random?</h2>

  <p style="color:#aeb5d0;line-height:1.6;margin-bottom:15px;">
    Let the simulator choose a challenge for you.
  </p>

  <button class="secondary" onclick="randomScenario()">
    🎲 Give Me a Random Future
  </button>

</div>


<!-- INPUT -->

<div class="card">

  <h2 id="inputTitle">
    Your Saving Plan
  </h2>

  <div class="input-row">

    <div class="input-group">

      <label id="amountLabel">
        Amount saved each day
      </label>

      <input
        type="number"
        id="amount"
        value="500"
        min="1"
      >

    </div>


    <div class="input-group">

      <label>
        Duration
      </label>

      <select id="duration">

        <option value="7">
          1 week
        </option>

        <option value="30">
          1 month
        </option>

        <option value="90">
          3 months
        </option>

        <option value="180">
          6 months
        </option>

        <option value="365" selected>
          1 year
        </option>

        <option value="730">
          2 years
        </option>

      </select>

    </div>

  </div>


  <button class="primary" onclick="calculate()">
    🚀 Show Me What Happens
  </button>

</div>


<!-- RESULT -->

<div class="card result" id="result">

  <h2 id="resultTitle">
    Your Future
  </h2>

  <div class="big-number" id="bigNumber">
    ₦182,500
  </div>

  <p class="result-description" id="resultDescription">
    Small decisions can create big results.
  </p>


  <div class="stats">

    <div class="stat">

      <div class="stat-number" id="dailyStat">
        ₦500
      </div>

      <div class="stat-label">
        PER DAY
      </div>

    </div>


    <div class="stat">

      <div class="stat-number" id="daysStat">
        365
      </div>

      <div class="stat-label">
        DAYS
      </div>

    </div>


    <div class="stat">

      <div class="stat-number" id="totalStat">
        ₦182,500
      </div>

      <div class="stat-label">
        TOTAL
      </div>

    </div>

  </div>


  <div class="timeline" id="timeline"></div>


  <div class="share-area">

    <button class="secondary" onclick="shareResult()">
      📤 Share Result
    </button>

    <button class="secondary" onclick="copyResult()">
      📋 Copy Result
    </button>

  </div>

</div>


<!-- ACHIEVEMENTS -->

<div class="card">

  <h2>🏆 Achievements</h2>

  <div class="achievements">

    <div class="badge" id="badge1">

      <div class="badge-icon">🚀</div>

      <strong>First Step</strong>

      <small>Complete your first simulation.</small>

    </div>


    <div class="badge" id="badge5">

      <div class="badge-icon">🧠</div>

      <strong>Explorer</strong>

      <small>Complete 5 simulations.</small>

    </div>


    <div class="badge" id="badge10">

      <div class="badge-icon">🔥</div>

      <strong>Committed</strong>

      <small>Complete 10 simulations.</small>

    </div>


    <div class="badge" id="badgeStreak">

      <div class="badge-icon">⚡</div>

      <strong>7-Day Streak</strong>

      <small>Visit the simulator 7 days in a row.</small>

    </div>

  </div>

</div>


<footer>

  What If? — Your future is built one small decision at a time.

  <br><br>

  <span class="creator">
    Created by Akosile Mubarak © 2026
  </span>

</footer>

</div>


<script>

/* =========================
   DATA
========================= */

let currentType = "money";

const scenarios = {

  money: {
    title: "Your Saving Plan",
    label: "Amount saved each day",
    defaultAmount: 500,
    resultTitle: "Your Possible Savings",
    description:
      "Small amounts can become significant when you stay consistent."
  },

  study: {
    title: "Your Study Plan",
    label: "Hours studied each day",
    defaultAmount: 1,
    resultTitle: "Your Study Time",
    description:
      "Consistent study time can add up to hundreds of hours."
  },

  coding: {
    title: "Your Coding Journey",
    label: "Hours coding each day",
    defaultAmount: 1,
    resultTitle: "Your Coding Time",
    description:
      "Every hour you practice gives you more experience."
  },

  exercise: {
    title: "Your Activity Plan",
    label: "Minutes active each day",
    defaultAmount: 30,
    resultTitle: "Your Activity Time",
    description:
      "Consistent activity can add up to a surprising amount of time."
  },

  reading: {
    title: "Your Reading Plan",
    label: "Minutes reading each day",
    defaultAmount: 20,
    resultTitle: "Your Reading Time",
    description:
      "A few minutes of reading every day can become many hours."
  },

  creative: {
    title: "Your Creative Journey",
    label: "Minutes creating each day",
    defaultAmount: 30,
    resultTitle: "Your Creative Time",
    description:
      "Small creative sessions can build a large amount of practice."
  }

};


/* =========================
   LOCAL STORAGE
========================= */

let simulations =
  Number(localStorage.getItem("simulations")) || 0;

let streak =
  Number(localStorage.getItem("streak")) || 0;

let lastVisit =
  localStorage.getItem("lastVisit") || "";


/* =========================
   STREAK
========================= */

function updateStreak() {

  const today =
    new Date().toISOString().split("T")[0];

  if (lastVisit !== today) {

    if (lastVisit) {

      const yesterday =
        new Date();

      yesterday.setDate(
        yesterday.getDate() - 1
      );

      const yesterdayString =
        yesterday.toISOString().split("T")[0];

      if (lastVisit === yesterdayString) {

        streak++;

      } else {

        streak = 1;

      }

    } else {

      streak = 1;

    }

    localStorage.setItem(
      "streak",
      streak
    );

    localStorage.setItem(
      "lastVisit",
      today
    );
  }

  document.getElementById("streak")
    .textContent = streak;
}


/* =========================
   SCENARIOS
========================= */

document
.querySelectorAll(".scenario")
.forEach(button => {

  button.addEventListener("click", () => {

    document
    .querySelectorAll(".scenario")
    .forEach(btn =>
      btn.classList.remove("active")
    );

    button.classList.add("active");

    currentType =
      button.dataset.type;

    updateInputs();

  });

});


function updateInputs() {

  const scenario =
    scenarios[currentType];

  document.getElementById(
    "inputTitle"
  ).textContent = scenario.title;

  document.getElementById(
    "amountLabel"
  ).textContent = scenario.label;

  document.getElementById(
    "amount"
  ).value =
    scenario.defaultAmount;

  document.getElementById(
    "resultTitle"
  ).textContent =
    scenario.resultTitle;
}


/* =========================
   RANDOM SCENARIO
========================= */

function randomScenario() {

  const types =
    Object.keys(scenarios);

  const random =
    types[
      Math.floor(
        Math.random() * types.length
      )
    ];

  currentType = random;

  document
  .querySelectorAll(".scenario")
  .forEach(button => {

    button.classList.remove("active");

    if (
      button.dataset.type === random
    ) {

      button.classList.add("active");

    }

  });

  updateInputs();

  window.scrollTo({
    top:
      document
      .querySelector(".card:nth-of-type(4)")
      .offsetTop,

    behavior: "smooth"
  });

}


/* =========================
   DAILY CHALLENGE
========================= */

function dailyChallenge() {

  currentType = "money";

  document
  .querySelectorAll(".scenario")
  .forEach(button => {

    button.classList.remove("active");

    if (
      button.dataset.type === "money"
    ) {
      button.classList.add("active");
    }

  });

  document.getElementById(
    "amount"
  ).value = 500;

  document.getElementById(
    "duration"
  ).value = 365;

  calculate();

}


/* =========================
   CALCULATE
========================= */

function calculate() {

  const amount =
    Number(
      document.getElementById(
        "amount"
      ).value
    );

  const days =
    Number(
      document.getElementById(
        "duration"
      ).value
    );


  if (
    amount <= 0 ||
    isNaN(amount)
  ) {

    alert(
      "Please enter a number greater than 0."
    );

    return;
  }


  const total =
    amount * days;


  const scenario =
    scenarios[currentType];


  let formattedTotal;


  if (
    currentType === "money"
  ) {

    formattedTotal =
      "₦" +
      total.toLocaleString();

  }

  else if (
    currentType === "study" ||
    currentType === "coding"
  ) {

    formattedTotal =
      formatHours(total);

  }

  else {

    formattedTotal =
      formatMinutes(total);

  }


  document.getElementById(
    "bigNumber"
  ).textContent =
    formattedTotal;


  document.getElementById(
    "resultDescription"
  ).textContent =
    scenario.description;


  document.getElementById(
    "dailyStat"
  ).textContent =
    formatDaily(amount);


  document.getElementById(
    "daysStat"
  ).textContent =
    days.toLocaleString();


  document.getElementById(
    "totalStat"
  ).textContent =
    formattedTotal;


  createTimeline(
    amount,
    days
  );


  simulations++;

  localStorage.setItem(
    "simulations",
    simulations
  );


  updateDashboard();


  const result =
    document.getElementById(
      "result"
    );

  result.classList.add("show");


  result.scrollIntoView({
    behavior: "smooth",
    block: "start"
  });

}


/* =========================
   FORMATTING
========================= */

function formatDaily(amount) {

  if (
    currentType === "money"
  ) {

    return (
      "₦" +
      amount.toLocaleString()
    );

  }

  if (
    currentType === "exercise" ||
    currentType === "reading" ||
    currentType === "creative"
  ) {

    return amount + " min";

  }

  return amount + " hr";
}


function formatHours(hours) {

  if (hours < 24) {

    return hours + " hrs";

  }

  const days =
    Math.floor(hours / 24);

  const remaining =
    hours % 24;


  if (remaining === 0) {

    return days + " days";

  }

  return (
    days +
    "d " +
    remaining +
    "h"
  );

}


function formatMinutes(minutes) {

  const hours =
    Math.floor(minutes / 60);

  const remaining =
    minutes % 60;


  if (hours === 0) {

    return minutes + " min";

  }


  if (remaining === 0) {

    return hours + " hrs";

  }


  return (
    hours +
    "h " +
    remaining +
    "m"
  );

}


/* =========================
   TIMELINE
========================= */

function createTimeline(
  amount,
  days
) {

  const timeline =
    document.getElementById(
      "timeline"
    );

  timeline.innerHTML = "";


  let checkpoints = [

    1,

    Math.floor(days * .25),

    Math.floor(days * .5),

    Math.floor(days * .75),

    days

  ];


  checkpoints =
    [...new Set(che
