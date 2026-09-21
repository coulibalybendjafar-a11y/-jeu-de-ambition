# -jeu-de-ambition
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>De Zéro à Milliardaire</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  overflow:hidden;
  font-family:Arial,sans-serif;
  background:#111;
  touch-action:none;
}

#game{
  position:relative;
  width:100vw;
  height:100vh;
  overflow:hidden;
  background:#79b85a;
}

/* CIEL */
#sky{
  position:absolute;
  inset:0 0 55% 0;
  background:linear-gradient(#54bdf0,#bdefff);
}

/* SOLEIL */
#sun{
  position:absolute;
  width:90px;
  height:90px;
  border-radius:50%;
  background:#ffd83d;
  right:8%;
  top:7%;
  box-shadow:0 0 45px #fff06b;
}

/* SOL */
#ground{
  position:absolute;
  left:0;
  top:45%;
  width:100%;
  height:55%;
  background:
    radial-gradient(circle,#6cab4e 2px,transparent 3px);
  background-size:35px 35px;
  background-color:#72b653;
}

/* ROUTES */
.road{
  position:absolute;
  background:#555;
  box-shadow:inset 0 0 0 5px #444;
}

#road1{
  width:100%;
  height:115px;
  top:62%;
}

#road2{
  width:125px;
  height:100%;
  left:45%;
  top:0;
}

.line{
  position:absolute;
  background:#f4d03f;
  z-index:2;
}

#road1 .line{
  width:100%;
  height:5px;
  top:55px;
  background:repeating-linear-gradient(
    90deg,#fff 0 35px,transparent 35px 70px
  );
}

#road2 .line{
  height:100%;
  width:5px;
  left:60px;
  background:repeating-linear-gradient(
    0deg,#fff 0 35px,transparent 35px 70px
  );
}

/* BATIMENTS */
.building{
  position:absolute;
  width:150px;
  height:110px;
  border:5px solid #49301f;
  border-radius:8px;
  background:#d58c55;
  box-shadow:8px 10px 0 #0002;
  z-index:3;
}

.building:before{
  content:"";
  position:absolute;
  width:0;
  height:0;
  left:18px;
  top:-45px;
  border-left:52px solid transparent;
  border-right:52px solid transparent;
  border-bottom:45px solid #7b332b;
}

.window{
  position:absolute;
  width:30px;
  height:30px;
  background:#8de5ff;
  border:3px solid #533a2a;
}

.w1{left:15px;top:35px}
.w2{right:15px;top:35px}

.door{
  position:absolute;
  width:30px;
  height:55px;
  bottom:0;
  left:60px;
  background:#59351f;
}

.shop{
  background:#e7bd55;
}

.shop .sign{
  position:absolute;
  top:-30px;
  left:20px;
  width:100px;
  height:28px;
  text-align:center;
  padding:5px;
  background:#fff;
  border:2px solid #333;
  font-size:12px;
  font-weight:bold;
}

/* ARBRES */
.tree{
  position:absolute;
  width:60px;
  height:90px;
  z-index:4;
}

.tree:before{
  content:"";
  position:absolute;
  width:18px;
  height:50px;
  left:21px;
  bottom:0;
  background:#70401f;
}

.tree:after{
  content:"";
  position:absolute;
  width:60px;
  height:60px;
  border-radius:50%;
  left:0;
  top:0;
  background:#267a35;
  box-shadow:
    20px 10px 0 #318d3e,
    -15px 18px 0 #2b8038;
}

/* PERSONNAGE */
#player{
  position:absolute;
  width:38px;
  height:58px;
  left:50%;
  top:52%;
  z-index:20;
  transition:.05s linear;
}

.head{
  position:absolute;
  width:27px;
  height:27px;
  left:5px;
  top:0;
  border-radius:50%;
  background:#9b6038;
  border:2px solid #47291d;
}

.body{
  position:absolute;
  width:30px;
  height:28px;
  left:4px;
  top:26px;
  border-radius:8px 8px 3px 3px;
  background:#1267b1;
}

.leg{
  position:absolute;
  width:9px;
  height:18px;
  background:#202c39;
  top:49px;
}

.l1{left:8px}
.l2{right:8px}

/* NPC */
.npc{
  position:absolute;
  width:30px;
  height:50px;
  z-index:15;
}

.npc .head{
  transform:scale(.8);
}

.npc .body{
  transform:scale(.8);
  top:24px;
}

/* VOITURE */
#car{
  position:absolute;
  width:75px;
  height:38px;
  background:#d72f2f;
  border-radius:12px 18px 8px 8px;
  z-index:12;
  left:30%;
  top:67%;
  border:3px solid #651d1d;
}

#car:before{
  content:"";
  position:absolute;
  width:35px;
  height:20px;
  background:#8ee8ff;
  left:20px;
  top:-14px;
  border:3px solid #651d1d;
  border-radius:8px 8px 0 0;
}

.wheel{
  position:absolute;
  width:17px;
  height:17px;
  border-radius:50%;
  background:#111;
  bottom:-9px;
}

.wheel1{left:8px}
.wheel2{right:8px}

/* INTERFACE */
#hud{
  position:absolute;
  top:12px;
  left:12px;
  z-index:50;
  padding:12px;
  border-radius:15px;
  background:#000b;
  color:#fff;
  min-width:220px;
  backdrop-filter:blur(5px);
}

#money{
  font-size:20px;
  font-weight:bold;
  color:#58ff82;
}

#business{
  margin-top:5px;
  font-size:13px;
}

#mission{
  position:absolute;
  top:12px;
  right:12px;
  z-index:50;
  background:#fff;
  padding:10px;
  border-radius:12px;
  max-width:220px;
  font-size:13px;
  box-shadow:0 4px 15px #0004;
}

#message{
  position:absolute;
  top:100px;
  left:50%;
  transform:translateX(-50%);
  background:#000d;
  color:#fff;
  padding:12px 20px;
  border-radius:20px;
  z-index:100;
  display:none;
}

/* COMMANDES */
#controls{
  position:absolute;
  bottom:20px;
  left:20px;
  z-index:60;
  display:grid;
  grid-template-columns:55px 55px 55px;
  grid-template-rows:55px 55px;
  gap:5px;
}

.btn{
  border:0;
  border-radius:15px;
  background:#000b;
  color:white;
  font-size:23px;
  font-weight:bold;
  user-select:none;
  -webkit-user-select:none;
}

.btn:active{
  background:#ffffff55;
}

.up{grid-column:2}
.left{grid-column:1;grid-row:2}
.down{grid-column:2;grid-row:2}
.right{grid-column:3;grid-row:2}

#actions{
  position:absolute;
  right:20px;
  bottom:25px;
  z-index:60;
  display:flex;
  flex-direction:column;
  gap:10px;
}

.action{
  width:75px;
  height:55px;
  border:0;
  border-radius:16px;
  background:#ffb300;
  color:#111;
  font-weight:bold;
  box-shadow:0 4px 0 #a96f00;
}

/* MINI MAP */
#map{
  position:absolute;
  right:15px;
  bottom:15px;
  width:150px;
  height:95px;
  background:#6eae50;
  border:3px solid white;
  border-radius:10px;
  z-index:50;
  opacity:.9;
}

.maproad{
  position:absolute;
  background:#555;
}

.m1{
  width:100%;
  height:18px;
  top:40px;
}

.m2{
  width:18px;
  height:100%;
  left:65px;
}

#mapdot{
  position:absolute;
  width:8px;
  height:8px;
  background:red;
  border-radius:50%;
  left:72px;
  top:44px;
}

/* RESPONSIVE */
@media(max-width:600px){
  #hud{
    min-width:180px;
    padding:8px;
  }

  #money{
    font-size:16px;
  }

  #mission{
    top:75px;
    right:10px;
    max-width:175px;
  }

  #map{
    display:none;
  }
}
</style>
</head>

<body>

<div id="game">

<div id="sky"></div>
<div id="sun"></div>
<div id="ground"></div>

<div id="road1" class="road"><div class="line"></div></div>
<div id="road2" class="road"><div class="line"></div></div>

<!-- BATIMENTS -->
<div class="building" style="left:5%;top:48%">
  <div class="window w1"></div>
  <div class="window w2"></div>
  <div class="door"></div>
</div>

<div class="building shop" style="right:5%;top:48%">
  <div class="sign">SUPERMARCHÉ</div>
  <div class="window w1"></div>
  <div class="window w2"></div>
  <div class="door"></div>
</div>

<div class="building shop" style="left:5%;top:76%">
  <div class="sign">LAVAGE AUTO</div>
  <div class="window w1"></div>
  <div class="window w2"></div>
  <div class="door"></div>
</div>

<!-- ARBRES -->
<div class="tree" style="left:25%;top:48%"></div>
<div class="tree" style="left:78%;top:76%"></div>
<div class="tree" style="left:28%;top:78%"></div>
<div class="tree" style="right:25%;top:47%"></div>

<!-- VOITURE -->
<div id="car">
  <div class="wheel wheel1"></div>
  <div class="wheel wheel2"></div>
</div>

<!-- NPC -->
<div class="npc" style="left:20%;top:58%">
  <div class="head"></div>
  <div class="body"></div>
</div>

<div class="npc" style="left:70%;top:58%">
  <div class="head"></div>
  <div class="body"></div>
</div>

<!-- JOUEUR -->
<div id="player">
  <div class="head"></div>
  <div class="body"></div>
  <div class="leg l1"></div>
  <div class="leg l2"></div>
</div>

<!-- HUD -->
<div id="hud">
  <div>👤 ENTREPRENEUR</div>
  <div id="money">💰 0 F CFA</div>
  <div id="business">🏪 Entreprise : aucune</div>
</div>

<div id="mission">
  🎯 <b>MISSION</b><br>
  Trouve un travail et gagne tes premiers 10 000 F CFA.
</div>

<div id="message"></div>

<!-- MINI MAP -->
<div id="map">
  <div class="maproad m1"></div>
  <div class="maproad m2"></div>
  <div id="mapdot"></div>
</div>

<!-- COMMANDES -->
<div id="controls">
  <button class="btn up" data-key="ArrowUp">▲</button>
  <button class="btn left" data-key="ArrowLeft">◀</button>
  <button class="btn down" data-key="ArrowDown">▼</button>
  <button class="btn right" data-key="ArrowRight">▶</button>
</div>

<div id="actions">
  <button class="action" id="work">TRAVAIL</button>
  <button class="action" id="buy">ACHETER</button>
  <button class="action" id="save">💾 SAVE</button>
</div>

</div>

<script>

/* =========================
   DONNÉES DU JOUEUR
========================= */

let player = {
  x: window.innerWidth/2,
  y: window.innerHeight*.52,
  money: 0,
  business: "aucune",
  speed: 5
};

let keys = {};

/* =========================
   ELEMENTS
========================= */

const game = document.getElementById("game");
const playerEl = document.getElementById("player");
const moneyEl = document.getElementById("money");
const businessEl = document.getElementById("business");
const messageEl = document.getElementById("message");
const missionEl = document.getElementById("mission");
const mapDot = document.getElementById("mapdot");

/* =========================
   SAUVEGARDE
========================= */

function saveGame(){

  localStorage.setItem(
    "milliardaire_save",
    JSON.stringify(player)
  );

  showMessage("💾 Progression sauvegardée !");
}

function loadGame(){

  const save =
    localStorage.getItem("milliardaire_save");

  if(save){

    player = JSON.parse(save);

    showMessage("📂 Partie chargée !");
  }
}

/* =========================
   AFFICHAGE
========================= */

function updateUI(){

  moneyEl.textContent =
    "💰 " +
    Math.floor(player.money).toLocaleString("fr-FR") +
    " F CFA";

  businessEl.textContent =
    "🏪 Entreprise : " +
    player.business;

  playerEl.style.left =
    player.x + "px";

  playerEl.style.top =
    player.y + "px";

  mapDot.style.left =
    Math.max(
      2,
      Math.min(
        142,
        player.x/window.innerWidth*142
      )
    ) + "px";

  mapDot.style.top =
    Math.max(
      2,
      Math.min(
        87,
        player.y/window.innerHeight*87
      )
    ) + "px";
}

/* =========================
   MESSAGE
========================= */

let messageTimer;

function showMessage(text){

  messageEl.textContent = text;
  messageEl.style.display = "block";

  clearTimeout(messageTimer);

  messageTimer = setTimeout(()=>{
    messageEl.style.display = "none";
  },2500);
}

/* =========================
   MOUVEMENT
========================= */

function move(){

  if(keys.ArrowUp)
    player.y -= player.speed;

  if(keys.ArrowDown)
    player.y += player.speed;

  if(keys.ArrowLeft)
    player.x -= player.speed;

  if(keys.ArrowRight)
    player.x += player.speed;

  const maxX =
    window.innerWidth - 45;

  const maxY =
    window.innerHeight - 65;

  player.x =
    Math.max(0,Math.min(maxX,player.x));

  player.y =
    Math.max(100,Math.min(maxY,player.y));

  updateUI();

  requestAnimationFrame(move);
}

/* =========================
   CLAVIER
========================= */

document.addEventListener(
  "keydown",
  e => {

    keys[e.key] = true;

  }
);

document.addEventListener(
  "keyup",
  e => {

    keys[e.key] = false;

  }
);

/* =========================
   BOUTONS TACTILES
========================= */

document.querySelectorAll(".btn")
.forEach(button => {

  const key =
    button.dataset.key;

  button.addEventListener(
    "touchstart",
    e => {

      e.preventDefault();
      keys[key] = true;

    },
    {passive:false}
  );

  button.addEventListener(
    "touchend",
    e => {

      e.preventDefault();
      keys[key] = false;

    },
    {passive:false}
  );

  button.addEventListener(
    "mousedown",
    () => keys[key] = true
  );

  button.addEventListener(
    "mouseup",
    () => keys[key] = false
  );

});

/* =========================
   TRAVAIL
========================= */

document.getElementById("work")
.onclick = () => {

  const gain =
    Math.floor(
      Math.random()*4000
    ) + 1000;

  player.money += gain;

  showMessage(
    "💼 Travail terminé : +" +
    gain.toLocaleString("fr-FR") +
    " F CFA"
  );

  if(player.money >= 10000){

    missionEl.innerHTML =
      "🎯 <b>NOUVELLE MISSION</b><br>" +
      "Achète ton premier commerce pour devenir entrepreneur.";

  }

  updateUI();
};

/* =========================
   ACHETER UNE ENTREPRISE
========================= */

document.getElementById("buy")
.onclick = () => {

  if(player.business !== "aucune"){

    showMessage(
      "🏢 Tu possèdes déjà une entreprise."
    );

    return;
  }

  if(player.money < 10000){

    showMessage(
      "❌ Il te faut 10 000 F CFA."
    );

    return;
  }

  player.money -= 10000;

  player.business =
    "Lavage Auto";

  missionEl.innerHTML =
    "🎯 <b>NOUVELLE MISSION</b><br>" +
    "Développe ton entreprise jusqu'à 100 000 F CFA.";

  showMessage(
    "🎉 Félicitations ! Tu as créé ton entreprise !"
  );

  updateUI();
};

/* =========================
   REVENUS AUTOMATIQUES
========================= */

setInterval(()=>{

  if(player.business !== "aucune"){

    const income =
      Math.floor(Math.random()*1000)+500;

    player.money += income;

    showMessage(
      "📈 Ton entreprise rapporte +" +
      income.toLocaleString("fr-FR") +
      " F CFA"
    );

    updateUI();
  }

},10000);

/* =========================
   INITIALISATION
========================= */

loadGame();
updateUI();
move();

</script>

</body>
</html>