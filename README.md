
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Body Quest Academy: A&P Study Game</title>
<style>
*{box-sizing:border-box}
:root{
  --pink:#ff8fc6; --pink2:#ffd7ec; --blue:#a9dcff; --green:#b9f6d3;
  --yellow:#fff0a8; --purple:#d8c7ff; --orange:#ffd1a8; --mint:#d5fff1;
  --ink:#3f3346; --bad:#ff6f91; --good:#42b883;
}
body{
  margin:0;
  font-family:"Trebuchet MS", Arial, sans-serif;
  background:linear-gradient(135deg,#fff4fb,#ecfaff);
  color:var(--ink);
}
header{
  text-align:center;
  padding:16px;
  background:linear-gradient(90deg,var(--pink2),var(--blue),var(--green));
  border-bottom:4px solid white;
}
h1{margin:0;font-size:34px}
header p{margin:6px 0 0}
.game{
  max-width:1250px;
  margin:14px auto;
  padding:0 12px;
  display:grid;
  grid-template-columns:265px 1fr 330px;
  gap:14px;
}
.panel{
  background:rgba(255,255,255,.93);
  border:3px solid white;
  border-radius:24px;
  box-shadow:0 10px 24px rgba(90,50,100,.14);
  padding:14px;
}
.stats{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.stat{
  border:2px solid var(--pink2);
  background:white;
  border-radius:15px;
  padding:9px;
  text-align:center;
  font-weight:bold;
}
.map{
  min-height:720px;
  position:relative;
  overflow:hidden;
  background:linear-gradient(#eefaff 0 58%,#fff1f8 58% 100%);
}


.map-title{
  position:absolute;
  left:50%;
  top:4%;
  transform:translateX(-50%);
  background:white;
  border:3px solid var(--pink2);
  border-radius:999px;
  padding:10px 18px;
  font-weight:bold;
  box-shadow:0 8px 16px rgba(0,0,0,.08);
  z-index:1;
}
.map-road{
position:absolute;
left:50%;
top:10%;
transform:translateX(-50%);
width:18px;
height:76%;
background:#ffe5c6;
border-radius:999px;
border:4px dashed white;
opacity:.8;
z-index:0;
}
.zone{z-index:2}


.zone{
  position:absolute;
  width:142px;height:105px;
  border:4px solid white;
  border-radius:25px;
  display:grid;place-items:center;
  text-align:center;
  font-weight:bold;
  cursor:pointer;
  transition:.15s;
  box-shadow:0 8px 18px rgba(0,0,0,.12);
}
.zone:hover{transform:translateY(-5px) scale(1.03)}
.zone span{font-size:31px;display:block}
.zone small{display:block;font-size:11px}
#cells{left:18%;top:12%;background:var(--mint)}
#skeletal{right:18%;top:12%;background:var(--yellow)}
#muscular{left:8%;top:34%;background:var(--green)}
#nervous{left:41%;top:34%;background:var(--purple)}
#circulatory{right:8%;top:34%;background:var(--pink2)}
#respiratory{left:18%;top:58%;background:var(--blue)}
#digestive{right:18%;top:58%;background:#caffbf}
#endocrine{left:18%;bottom:7%;background:#e8dcff}
#urinary{left:50%;top:58%;transform:translateX(-50%);background:#d8f7ff}
#injury{left:50%;bottom:7%;transform:translateX(-50%);background:var(--orange)}
#integumentary{right:18%;bottom:7%;background:#ffe2f2}
.player{
  position:absolute;left:45%;top:44%;
  width:76px;height:76px;border-radius:50%;
  background:white;border:4px solid var(--pink);
  display:grid;place-items:center;font-size:39px;
  transition:.45s;box-shadow:0 8px 18px rgba(0,0,0,.14);z-index:4;
}
.speech{
  position:absolute;left:50%;bottom:10px;transform:translateX(-50%);
  width:88%;background:white;border:3px solid var(--pink2);
  border-radius:18px;padding:10px;text-align:center;font-weight:bold;
}
button{font-family:inherit;font-weight:bold;cursor:pointer}
.main{
  border:0;border-radius:999px;padding:10px 13px;background:var(--pink);
  color:white;margin:4px 2px;box-shadow:0 4px 0 #db65a2;
}
.main:active{transform:translateY(3px);box-shadow:0 1px 0 #db65a2}
.secondary{
  border:2px solid var(--blue);border-radius:14px;padding:9px;background:white;
  width:100%;margin:5px 0;text-align:left;
}
.secondary:hover{background:#f1fbff}
.quest{border:2px dashed var(--pink);border-radius:18px;background:#fff9fd;padding:12px}
.progress{width:100%;height:18px;background:#eee;border-radius:999px;overflow:hidden;border:2px solid white;margin-top:8px}
.fill{height:100%;width:0%;background:linear-gradient(90deg,var(--pink),var(--yellow),var(--green))}
.badges,.cards{display:flex;flex-wrap:wrap;gap:7px;margin-top:8px}
.badge,.cardbit{border:2px solid white;border-radius:999px;padding:7px 9px;font-size:12px;background:var(--purple)}
.cardbit{background:var(--green)}
.log{height:135px;overflow:auto;border:2px solid var(--pink2);border-radius:15px;padding:8px;background:white;font-size:13px}
.mode{display:grid;grid-template-columns:1fr;gap:6px}
.lesson{background:white;border:2px solid var(--pink2);border-radius:15px;padding:10px;margin:8px 0}
.explain{background:#f7fcff;border:2px solid var(--blue);border-radius:14px;padding:9px;margin-top:8px;font-size:14px}
.correct{background:#dffff0!important;border-color:var(--good)}
.wrong{background:#ffe1e8!important;border-color:var(--bad)}
select{
  width:100%;padding:9px;border-radius:12px;border:2px solid var(--pink2);
  background:white;font-weight:bold;color:var(--ink);
}
.modal{display:none;position:fixed;inset:0;background:rgba(40,25,45,.38);place-items:center;z-index:10;padding:18px}
.modal-card{
  background:white;max-width:780px;width:100%;max-height:85vh;overflow:auto;
  border:4px solid white;border-radius:26px;padding:18px;box-shadow:0 12px 30px rgba(0,0,0,.22);
}
.close{float:right;width:34px;height:34px;border:0;border-radius:50%;background:var(--pink);color:white}
.flash{border:2px solid var(--blue);border-radius:18px;padding:16px;background:#f7fcff;min-height:130px;display:grid;place-items:center;text-align:center;font-weight:bold}
.casebox{background:#fff7df;border:2px solid #ffd35a;border-radius:16px;padding:10px;margin:8px 0}
@keyframes pop{from{opacity:1;transform:translateY(0) scale(1)}to{opacity:0;transform:translateY(-55px) scale(1.8)}}
.spark{position:absolute;pointer-events:none;animation:pop .8s forwards;font-size:26px;z-index:8}

.tutorial{
  position:fixed;
  inset:0;
  background:linear-gradient(135deg,#fff4fb,#ecfaff);
  z-index:99;
  display:grid;
  place-items:center;
  padding:18px;
}
.tutorial-card{
  background:white;
  max-width:760px;
  width:100%;
  border:4px solid white;
  border-radius:28px;
  padding:22px;
  box-shadow:0 14px 34px rgba(90,50,100,.2);
}
.tutorial-card h2{margin-top:0}
.tutorial-step{
  background:#fff9fd;
  border:2px solid var(--pink2);
  border-radius:18px;
  padding:12px;
  margin:10px 0;
}


/* --- Fun learning upgrade --- */
.adventure-strip{display:grid;grid-template-columns:repeat(5,1fr);gap:8px;width:min(760px,96%);position:relative;z-index:3;margin-bottom:4px}
.world{background:white;border:2px solid var(--pink2);border-radius:16px;padding:8px;text-align:center;font-weight:bold;font-size:12px;box-shadow:0 5px 12px rgba(0,0,0,.08)}
.world.active{background:#fff0a8;border-color:#ffd35a;transform:scale(1.04)}
.objective-box{background:#fff7df;border:2px solid #ffd35a;border-radius:18px;padding:10px;margin:10px 0;font-size:14px}
.xpbar{width:100%;height:15px;background:#eee;border-radius:999px;overflow:hidden;border:2px solid white;margin-top:6px}
.xpfill{height:100%;width:0%;background:linear-gradient(90deg,var(--purple),var(--pink),var(--yellow))}
.chest{background:#fff7df;border:2px solid #ffd35a;border-radius:16px;padding:10px;margin-top:10px;text-align:center;font-weight:bold}
.cardbit.rare{background:#fff0a8;border-color:#ffd35a}
.tipbox{background:#f7fcff;border:2px solid var(--blue);border-radius:15px;padding:10px;margin:8px 0;font-size:14px}
.boss-title{font-size:22px;text-align:center;background:#fff0a8;border:3px solid #ffd35a;border-radius:18px;padding:10px;margin:8px 0}

.picture-card{
  background:white;
  border:3px solid var(--blue);
  border-radius:18px;
  padding:10px;
  margin:8px 0 10px;
  text-align:center;
  cursor:zoom-in;
  box-shadow:0 7px 16px rgba(0,0,0,.08);
}
.picture-card svg{
  width:100%;
  max-height:325px;
  display:block;
}
.picture-caption{
  font-size:12px;
  font-weight:bold;
  margin-top:6px;
  color:#6b5b72;
}
.zoom-picture svg{
  width:100%;
  max-height:70vh;
  display:block;
}

.picture-card img.anatomy-image{
  width:100%;
  max-height:325px;
  object-fit:contain;
  display:block;
  margin:auto;
  border-radius:16px;
}
.anatomy-img-wrap{
  position:relative;
  width:100%;
  min-height:300px;
  display:grid;
  place-items:center;
  overflow:hidden;
  background:#fff;
  border-radius:16px;
}
.target-circle{
  display:none !important;

  position:absolute;
  transform:translate(-50%,-50%);
  border:5px dashed #ff285f;
  border-radius:50%;
  box-shadow:0 0 0 999px rgba(255,255,255,.08);
  pointer-events:none;
}
.target-arrow{
  display:none !important;

  position:absolute;
  right:8%;
  top:10%;
  color:#ff285f;
  font-size:58px;
  font-weight:bold;
  transform:rotate(145deg);
  text-shadow:0 2px 0 white, 0 0 8px white;
  pointer-events:none;
}

@media(max-width:970px){.game{grid-template-columns:1fr}.map{min-height:700px}.zone{width:130px}}

.map{
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:flex-start;
  gap:22px;
  padding:74px 28px 34px;
}
.map-grid{
  width:min(760px, 96%);
  display:grid;
  grid-template-columns:repeat(6, 1fr);
  gap:22px;
  position:relative;
  z-index:2;
}
.zone{
  position:relative !important;
  left:auto !important;
  right:auto !important;
  top:auto !important;
  bottom:auto !important;
  transform:none !important;
  width:100% !important;
  min-height:104px;
}
.span-2{grid-column:span 3}
.span-3{grid-column:span 2}
.center-2-left{grid-column:2 / span 2}
.center-2-right{grid-column:4 / span 2}
.center-single{grid-column:3 / span 2}
.player{display:none}
.speech{
  position:relative !important;
  left:auto !important;
  bottom:auto !important;
  transform:none !important;
  width:min(760px, 96%) !important;
  margin-top:6px;
}
.map-title{
  top:18px !important;
}
.map-road{
  display:none;
}
@media(max-width:760px){
  .map-grid{
    grid-template-columns:1fr;
    gap:14px;
  }
  .span-2,.span-3,.center-2-left,.center-2-right,.center-single{
    grid-column:auto;
  }
  .map{
    padding:78px 16px 24px;
  }
}

</style>
</head>
<body>
<header>
  <h1>🧠 Body Quest Academy: A&P Study Game 🩺</h1>
  <p>Learn anatomy, physiology, medical vocab, and injury reasoning through Easy, Normal, and Difficult levels.</p>
</header>

<div class="tutorial" id="tutorial">
  <div class="tutorial-card">
    <h2>Welcome to Body Quest Academy!</h2>
    <div class="tutorial-step"><b>1. Pick your level.</b><br>Choose Easy, Normal, or Difficult. Easy is simple, Normal is class-level, and Difficult adds deeper A&P thinking.</div>
    <div class="tutorial-step"><b>2. Click a body system.</b><br>Each zone teaches a short lesson and gives you 10 questions pulled from a much larger 150-question bank.</div>
    <div class="tutorial-step"><b>3. Learn from the “Why.”</b><br>After every answer, the game explains why the answer is correct.</div>
    <div class="tutorial-step"><b>4. Use study modes.</b><br>Try Case Missions, Flashcards, Match Vocab, Review Missed, and the Final Exam.</div>
    <button class="main" onclick="closeTutorial()">Start Game</button>
  </div>
</div>


<div class="game">
  <aside class="panel">
    <h2>Student Stats</h2>
    <div class="stats">
      <div class="stat">⭐ Score<br><span id="score">0</span></div>
      <div class="stat">💖 Hearts<br><span id="hearts">7</span></div>
      <div class="stat">📚 Mastery<br><span id="mastery">0</span>%</div>
      <div class="stat">🏅 Rank<br><span id="rank">Rookie</span></div>
      <div class="stat">⚡ XP<br><span id="xp">0</span></div>
      <div class="stat">🎓 Level<br><span id="level">1</span></div>
      <div class="stat">🔥 Streak<br><span id="streak">1</span></div>
      <div class="stat">🎁 Chests<br><span id="chests">0</span></div>
    </div>
    <div class="progress"><div class="fill" id="fill"></div></div>
    <div class="xpbar"><div class="xpfill" id="xpfill"></div></div>
    <div class="chest" id="dailyQuest">Daily Quest: Get 5 correct answers to open a mystery chest.</div>

    <h3>Difficulty</h3>
    <select id="difficulty" onchange="setDifficulty()">
      <option value="easy">Easy: simple basics</option>
      <option value="normal">Normal: class level</option>
      <option value="difficult">Difficult: deeper A&P</option>
    </select>

    <h3>Question Style</h3>
    <select id="questionStyle" onchange="setQuestionStyle()">
      <option value="mixed">Mixed: regular + picture</option>
      <option value="regular">Regular questions only</option>
      <option value="picture">Image questions only</option>
    </select>


    <h3>Game Modes</h3>
    <div class="mode">
      <button class="main" onclick="randomQuestion()">🎲 Random Question</button>
      <button class="main" onclick="startCase()">🩹 Patient Diagnosis</button>
      <button class="main" onclick="startBossBattle()">👾 Boss Battle</button>
      <button class="main" onclick="openBodyDex()">🃏 Organ Dex</button>
      <button class="main" onclick="reviewWeak()">🔁 Review Missed</button>
      <button class="main" onclick="startFlashcards()">📚 Flashcards</button>
      <button class="main" onclick="startMatchGame()">🧩 Match Vocab</button>
      <button class="main" onclick="startFinalExam()">🏥 Final Exam</button>
      <button class="main" onclick="openGuide()">📖 Study Guide</button>
      <button class="main" onclick="document.getElementById('tutorial').style.display='grid'">❔ Tutorial</button>
      <button class="main" onclick="restart()">🔄 Restart</button>
    </div>

    <h3>Collected Cards</h3>
    <div class="cards" id="cards"></div>
  </aside>

  <main class="panel map" id="map">
    <div class="map-title">A&P Learning Path<br><small>Follow the path from top to bottom</small></div>
    <div class="adventure-strip" id="adventureStrip">
      <div class="world active">🏫 Year 1</div><div class="world">🧪 Lab</div><div class="world">🩺 Clinic</div><div class="world">🚑 ER</div><div class="world">🎓 Final</div>
    </div>
    <div class="map-grid">
      <div class="zone span-2" id="cells" onclick="visit('Cells')"><div><span>🔬</span>Cells<small>membranes + ATP</small></div></div>
      <div class="zone span-2" id="skeletal" onclick="visit('Skeletal')"><div><span>🦴</span>Skeletal<small>bones + joints</small></div></div>

      <div class="zone span-3" id="muscular" onclick="visit('Muscular')"><div><span>💪</span>Muscular<small>movement</small></div></div>
      <div class="zone span-3" id="nervous" onclick="visit('Nervous')"><div><span>🧠</span>Nervous<small>control</small></div></div>
      <div class="zone span-3" id="circulatory" onclick="visit('Circulatory')"><div><span>🫀</span>Circulatory<small>blood flow</small></div></div>

      <div class="zone span-2" id="respiratory" onclick="visit('Respiratory')"><div><span>🫁</span>Respiratory<small>gas exchange</small></div></div>
      <div class="zone span-2" id="digestive" onclick="visit('Digestive')"><div><span>🥣</span>Digestive<small>nutrients</small></div></div>

      <div class="zone span-3" id="endocrine" onclick="visit('Endocrine')"><div><span>⚗️</span>Endocrine<small>hormones</small></div></div>
      <div class="zone span-3" id="urinary" onclick="visit('Urinary')"><div><span>💧</span>Urinary<small>fluid balance</small></div></div>
      <div class="zone span-3" id="integumentary" onclick="visit('Integumentary')"><div><span>🧴</span>Skin<small>barrier</small></div></div>

      <div class="zone center-single" id="injury" onclick="visit('Injuries')"><div><span>🩹</span>Injuries<small>sports + trauma</small></div></div>
    </div>
    <div class="player" id="player">🧑‍⚕️</div>
    <div class="speech" id="speech">Pick a body system. Each topic has a large no-repeat question bank.</div>
</main>

  <aside class="panel">
    <h2 id="questTitle">Quest</h2>
    <div class="objective-box" id="objective">Goal: pick a system, learn the mini lesson, then beat 10 questions to earn its organ card.</div>
    <div class="quest">
      <div id="lesson" class="lesson">Choose a topic on the map.</div>
      <h3 id="question">Question will appear here.</h3>
      <div id="choices"></div>
      <div id="explain" class="explain" style="display:none"></div>
    </div>
    <h3>Badges</h3>
    <div class="badges" id="badges"><span class="badge">🌱 Study Rookie</span></div>
    <h3>Log</h3>
    <div class="log" id="log"></div>
  </aside>
</div>

<div class="modal" id="modal">
  <div class="modal-card">
    <button class="close" onclick="closeModal()">×</button>
    <div id="modalContent"></div>
  </div>
</div>

<script>
const data = {
Cells:{
 emoji:"🔬", pos:[7,7], card:"Cell Specialist",
 lesson:{
  easy:"Cells are the basic unit of life. The cell membrane controls what enters and leaves.",
  normal:"Cells use ATP for energy. The membrane is selectively permeable, meaning only some substances pass easily.",
  difficult:"Homeostasis depends on transport across membranes, cell signaling, and energy production through ATP."
 },
 qs:{
  easy:[
   ["What is the basic unit of life?","Cell",["Cell","Bone","Organ system"],"Cells make up tissues, tissues make organs, and organs make body systems."],
   ["What controls what enters and leaves a cell?","Cell membrane",["Cell membrane","Rib cage","Tendon"],"The membrane acts like a selective border."],
   ["What part of the cell contains DNA?","Nucleus",["Nucleus","Alveoli","Ligament"],"The nucleus stores genetic instructions."]
  ],
  normal:[
   ["ATP is mainly used for...","Cell energy",["Cell energy","Bone protection","Air exchange"],"ATP is the usable energy molecule for many cell processes."],
   ["Diffusion moves particles from...","High to low concentration",["High to low concentration","Low to high concentration","Bone to muscle"],"Diffusion does not require energy."],
   ["Osmosis is diffusion of...","Water",["Water","Oxygen only","Hormones only"],"Osmosis is water movement across a membrane."]
  ],
  difficult:[
   ["Active transport requires...","Energy",["Energy","No ATP","A fracture"],"Active transport moves substances against a concentration gradient."],
   ["Loss of homeostasis means...","Internal balance is disrupted",["Internal balance is disrupted","Bones disappear","Digestion stops forever"],"Homeostasis keeps body conditions within a safe range."],
   ["Receptors are important because they...","Receive signals",["Receive signals","Store urine","Connect bones"],"Cell communication often begins when signals bind to receptors."]
  ]
 }},
Skeletal:{
 emoji:"🦴", pos:[30,7], card:"Bone Builder",
 lesson:{
  easy:"The skeletal system supports the body, protects organs, and helps you move.",
  normal:"Bones store minerals, produce blood cells in marrow, and joints allow motion.",
  difficult:"Bone remodeling responds to stress. Ligaments stabilize joints, while cartilage reduces friction."
 },
 qs:{
  easy:[
   ["What protects the brain?","Skull",["Skull","Rib cage","Femur"],"The skull is the bony structure around the brain."],
   ["What connects bone to bone?","Ligament",["Ligament","Tendon","Neuron"],"Ligaments stabilize joints."],
   ["A fracture means...","Broken or cracked bone",["Broken or cracked bone","Stretched ligament","Torn muscle"],"A fracture is an injury to bone."]
  ],
  normal:[
   ["Where are many blood cells made?","Bone marrow",["Bone marrow","Alveoli","Stomach acid"],"Bone marrow produces blood cells."],
   ["Cartilage helps joints by...","Reducing friction",["Reducing friction","Pumping blood","Making hormones"],"Cartilage cushions and smooths joint movement."],
   ["The femur is found in the...","Thigh",["Thigh","Forearm","Skull"],"The femur is the long bone of the thigh."]
  ],
  difficult:[
   ["Osteoporosis increases risk of...","Fractures",["Fractures","Sprains only","Concussions only"],"Lower bone density makes bones easier to break."],
   ["A joint moving beyond normal range may damage...","Ligaments",["Ligaments","Alveoli","Red blood cells"],"Ligaments are often injured in sprains."],
   ["Bone remodeling is influenced by...","Mechanical stress",["Mechanical stress","Hair color","Lung size"],"Bones adapt to forces placed on them."]
  ]
 }},
Muscular:{
 emoji:"💪", pos:[53,7], card:"Muscle Master",
 lesson:{
  easy:"Muscles contract and relax to move your body.",
  normal:"Tendons connect muscle to bone. Skeletal muscles are voluntary, while smooth and cardiac muscles are involuntary.",
  difficult:"Muscle contraction depends on actin, myosin, calcium, and ATP."
 },
 qs:{
  easy:[
   ["Muscles create movement by...","Contracting and relaxing",["Contracting and relaxing","Filtering blood","Digesting food"],"Muscle contraction pulls on bones."],
   ["What connects muscle to bone?","Tendon",["Tendon","Ligament","Alveolus"],"Tendons attach muscles to bones."],
   ["A strain usually injures a...","Muscle or tendon",["Muscle or tendon","Ligament","Bone only"],"Strains involve muscles or tendons."]
  ],
  normal:[
   ["Which muscle type is found in the heart?","Cardiac muscle",["Cardiac muscle","Skeletal muscle","Smooth muscle"],"Cardiac muscle is specialized heart muscle."],
   ["Which muscle type moves food through intestines?","Smooth muscle",["Smooth muscle","Skeletal muscle","Bone muscle"],"Smooth muscle is involuntary and found in organs."],
   ["Skeletal muscle is usually...","Voluntary",["Voluntary","Always unconscious","Only in the heart"],"You can usually control skeletal muscle."]
  ],
  difficult:[
   ["Calcium helps muscle contraction by allowing...","Actin and myosin interaction",["Actin and myosin interaction","Bone marrow production","Air entry"],"Calcium exposes binding sites for contraction."],
   ["Low ATP would make muscles...","Work poorly",["Work poorly","Turn into bone","Stop needing oxygen"],"Muscle contraction and relaxation both need ATP."],
   ["Delayed soreness after exercise often relates to...","Small muscle stress and repair",["Small muscle stress and repair","Broken skull","Extra alveoli"],"Exercise can cause tiny tissue stress that the body repairs."]
  ]
 }},
Nervous:{
 emoji:"🧠", pos:[76,7], card:"Neuron Navigator",
 lesson:{
  easy:"The nervous system controls body actions and sends messages.",
  normal:"The central nervous system is the brain and spinal cord. The peripheral nervous system includes nerves outside them.",
  difficult:"Neurons use electrical impulses and chemical neurotransmitters to communicate."
 },
 qs:{
  easy:[
   ["A concussion affects the...","Brain",["Brain","Stomach","Ankle"],"A concussion is a brain injury from a hit or jolt."],
   ["What cell sends nerve messages?","Neuron",["Neuron","Platelet","Alveolus"],"Neurons are nerve cells."],
   ["The brain helps control...","Body actions and signals",["Body actions and signals","Bone color","Food labels"],"The brain is the control center."]
  ],
  normal:[
   ["Brain and spinal cord make up the...","Central nervous system",["Central nervous system","Digestive system","Respiratory system"],"CNS means central nervous system."],
   ["A reflex is helpful because it...","Responds quickly",["Responds quickly","Stops oxygen","Breaks down fat"],"Reflexes can protect you before you think."],
   ["Nerves outside the CNS are part of the...","Peripheral nervous system",["Peripheral nervous system","Urinary system","Skeletal system"],"Peripheral nerves connect the CNS to the body."]
  ],
  difficult:[
   ["Neurotransmitters are...","Chemical messengers between neurons",["Chemical messengers between neurons","Bones in the skull","Air sacs"],"They help signals cross synapses."],
   ["The synapse is the...","Gap between nerve cells",["Gap between nerve cells","Center of bone","Blood vessel wall"],"Signals pass across synapses."],
   ["Nerve impulses are partly based on movement of...","Ions",["Ions","Cartilage","Bile"],"Charged particles help create electrical signals."]
  ]
 }},
Circulatory:{
 emoji:"🫀", pos:[7,34], card:"Heart Hero",
 lesson:{
  easy:"The heart pumps blood. Blood carries oxygen and nutrients.",
  normal:"Arteries carry blood away from the heart. Veins return blood to the heart. Capillaries exchange materials with tissues.",
  difficult:"Blood pressure, cardiac output, and vessel resistance affect circulation."
 },
 qs:{
  easy:[
   ["What does the heart do?","Pumps blood",["Pumps blood","Makes oxygen","Stores memories"],"The heart is a muscular pump."],
   ["Red blood cells help carry...","Oxygen",["Oxygen","Bones","Nerve signals"],"Hemoglobin in red blood cells carries oxygen."],
   ["Your pulse is related to your...","Heartbeat",["Heartbeat","Stomach acid","Skin color"],"Pulse reflects heartbeat waves in arteries."]
  ],
  normal:[
   ["What carries blood away from the heart?","Arteries",["Arteries","Veins","Ligaments"],"Arteries carry blood away."],
   ["Where does exchange with tissues happen?","Capillaries",["Capillaries","Tendons","Skull"],"Capillaries are tiny vessels for exchange."],
   ["Veins usually carry blood...","Back to the heart",["Back to the heart","Away from the heart","Into bones only"],"Veins return blood to the heart."]
  ],
  difficult:[
   ["Cardiac output means...","Blood pumped per minute",["Blood pumped per minute","Air in lungs","Calcium in bones"],"Cardiac output = heart rate × stroke volume."],
   ["High blood pressure increases strain on...","Blood vessels and heart",["Blood vessels and heart","Hair follicles only","Ligaments only"],"Pressure affects vessel walls and heart workload."],
   ["Vasoconstriction means blood vessels...","Narrow",["Narrow","Digest food","Become bones"],"Narrower vessels increase resistance."]
  ]
 }},
Respiratory:{
 emoji:"🫁", pos:[76,34], card:"Breath Boss",
 lesson:{
  easy:"The lungs help bring oxygen in and remove carbon dioxide.",
  normal:"Gas exchange occurs in alveoli. The diaphragm helps pull air into the lungs.",
  difficult:"Breathing supports pH balance by controlling carbon dioxide levels."
 },
 qs:{
  easy:[
   ["What do lungs help you do?","Breathe",["Breathe","Pump blood","Move bones"],"Lungs are breathing organs."],
   ["What gas does your body need from air?","Oxygen",["Oxygen","Carbon dioxide","Helium"],"Cells use oxygen to help make ATP."],
   ["What gas do you breathe out as waste?","Carbon dioxide",["Carbon dioxide","Calcium","Insulin"],"Carbon dioxide is produced by cells."]
  ],
  normal:[
   ["Tiny air sacs in lungs are called...","Alveoli",["Alveoli","Neurons","Ligaments"],"Alveoli are where gas exchange happens."],
   ["What muscle helps breathing?","Diaphragm",["Diaphragm","Biceps","Hamstring"],"The diaphragm contracts to help inhale."],
   ["Oxygen moves from alveoli into...","Blood",["Blood","Bone marrow","Tendons"],"Oxygen diffuses into capillaries."]
  ],
  difficult:[
   ["Too much carbon dioxide can make blood more...","Acidic",["Acidic","Bony","Flexible"],"CO2 affects blood pH."],
   ["Ventilation means...","Moving air in and out",["Moving air in and out","Digesting fats","Making urine"],"Ventilation is air movement."],
   ["Gas exchange works best with thin, moist surfaces and...","Many capillaries",["Many capillaries","Thick bones","No blood flow"],"Alveoli have close capillary networks."]
  ]
 }},
Digestive:{
 emoji:"🥣", pos:[23,66], card:"Digestion Detective",
 lesson:{
  easy:"The digestive system breaks food into usable parts.",
  normal:"The small intestine absorbs most nutrients. Enzymes help chemically break down food.",
  difficult:"Accessory organs like the liver, gallbladder, and pancreas support digestion."
 },
 qs:{
  easy:[
   ["Digestion breaks food into...","Usable parts",["Usable parts","Nerve cells","Air sacs"],"Your body absorbs nutrients from broken-down food."],
   ["The stomach helps break down...","Food",["Food","Bones","Air"],"The stomach mixes food with acid and enzymes."],
   ["Which organ absorbs most nutrients?","Small intestine",["Small intestine","Skull","Heart"],"Most absorption happens in the small intestine."]
  ],
  normal:[
   ["Enzymes help...","Break down molecules",["Break down molecules","Connect bones","Send nerve impulses"],"Digestive enzymes speed chemical breakdown."],
   ["Bile helps digest...","Fats",["Fats","Bones","Oxygen"],"Bile helps emulsify fats."],
   ["What organ stores bile?","Gallbladder",["Gallbladder","Lung","Femur"],"The gallbladder stores bile made by the liver."]
  ],
  difficult:[
   ["The pancreas helps digestion by releasing...","Enzymes",["Enzymes","Neurons","Ligaments"],"Pancreatic enzymes digest carbs, proteins, and fats."],
   ["Villi in the small intestine increase...","Surface area",["Surface area","Bone density","Air pressure"],"More surface area improves absorption."],
   ["The liver processes nutrients and helps...","Detoxify substances",["Detoxify substances","Pump air","Connect muscles"],"The liver has many metabolic jobs."]
  ]
 }},
Endocrine:{
 emoji:"⚗️", pos:[64,66], card:"Hormone Helper",
 lesson:{
  easy:"The endocrine system uses hormones as chemical messengers.",
  normal:"Glands release hormones that regulate growth, metabolism, stress, and blood sugar.",
  difficult:"Negative feedback helps keep hormone levels balanced."
 },
 qs:{
  easy:[
   ["Hormones are...","Chemical messengers",["Chemical messengers","Bones","Air sacs"],"Hormones travel through blood to target tissues."],
   ["Which system uses glands?","Endocrine system",["Endocrine system","Skeletal system","Respiratory system"],"Endocrine glands release hormones."],
   ["Insulin helps control...","Blood sugar",["Blood sugar","Bone shape","Lung size"],"Insulin helps cells take up glucose."]
  ],
  normal:[
   ["The thyroid helps regulate...","Metabolism",["Metabolism","Hearing","Joint friction"],"Thyroid hormones affect metabolic rate."],
   ["Adrenaline is linked to...","Fight-or-flight response",["Fight-or-flight response","Digestion only","Bone marrow only"],"Adrenaline prepares the body for stress."],
   ["Hormones travel mainly through...","Blood",["Blood","Hair","Cartilage"],"Blood transports many hormones."]
  ],
  difficult:[
   ["Negative feedback means the body...","Reduces a response when levels are high",["Reduces a response when levels are high","Always increases hormones","Stops homeostasis"],"Negative feedback stabilizes internal conditions."],
   ["Target cells respond to hormones because they have...","Receptors",["Receptors","Fractures","Alveoli"],"Hormones act on cells with matching receptors."],
   ["Glucagon generally raises...","Blood glucose",["Blood glucose","Bone length","Oxygen in air"],"Glucagon works opposite insulin in blood sugar balance."]
  ]
 }},
Urinary:{
 emoji:"💧", pos:[7,84], card:"Kidney Keeper",
 lesson:{
  easy:"The urinary system removes liquid waste and helps balance water.",
  normal:"Kidneys filter blood, regulate water and salts, and make urine.",
  difficult:"Nephrons filter blood and adjust water, electrolytes, and waste levels."
 },
 qs:{
  easy:[
   ["Which organs make urine?","Kidneys",["Kidneys","Lungs","Tendons"],"Kidneys filter blood and form urine."],
   ["The bladder stores...","Urine",["Urine","Oxygen","Hormones"],"Urine is stored before leaving the body."],
   ["The urinary system removes...","Liquid waste",["Liquid waste","Air","Bones"],"Urine carries liquid waste."]
  ],
  normal:[
   ["Urine travels from kidneys to bladder through...","Ureters",["Ureters","Arteries","Ligaments"],"Ureters are tubes from kidneys to bladder."],
   ["Kidneys help balance water and...","Salts",["Salts","Hair color","Tendons"],"Kidneys regulate electrolytes and fluid."],
   ["The urethra carries urine...","Out of the body",["Out of the body","Into lungs","Into bones"],"The urethra is the exit tube."]
  ],
  difficult:[
   ["The functional unit of the kidney is the...","Nephron",["Nephron","Neuron","Alveolus"],"Nephrons filter and process fluid."],
   ["ADH helps the body retain...","Water",["Water","Bone cells","Air"],"ADH increases water reabsorption."],
   ["Kidney problems can disturb...","Fluid and electrolyte balance",["Fluid and electrolyte balance","Only hair growth","Joint cartilage only"],"Kidneys help regulate internal chemistry."]
  ]
 }},
Injuries:{
 emoji:"🩹", pos:[42,84], card:"Injury Expert",
 lesson:{
  easy:"Common injuries include sprains, strains, fractures, dislocations, and concussions.",
  normal:"Sprains involve ligaments. Strains involve muscles or tendons. Fractures involve bones.",
  difficult:"Injury assessment uses mechanism of injury, symptoms, function, and red flags."
 },
 qs:{
  easy:[
   ["A sprain injures a...","Ligament",["Ligament","Tooth","Red blood cell"],"Sprains happen when ligaments stretch or tear."],
   ["A strain injures a...","Muscle or tendon",["Muscle or tendon","Lung air sac","Artery only"],"Strains involve muscle or tendon tissue."],
   ["A fracture means...","Broken or cracked bone",["Broken or cracked bone","Fast heartbeat","Extra hormone"],"A fracture is a bone injury."]
  ],
  normal:[
   ["A dislocation means...","A bone is out of place at a joint",["A bone is out of place at a joint","A muscle is sore","A nerve disappears"],"Dislocations involve joints."],
   ["A concussion should be taken seriously because it affects the...","Brain",["Brain","Toenail","Stomach"],"Brain injuries need caution."],
   ["For a serious injury, you should...","Get adult or medical help",["Get adult or medical help","Ignore it","Keep playing hard"],"Safety matters more than finishing a game."]
  ],
  difficult:[
   ["A red flag after head injury is...","Confusion or worsening symptoms",["Confusion or worsening symptoms","Mild hunger","Normal breathing"],"Worsening neurological signs need urgent help."],
   ["Loss of pulse or numbness after limb injury may suggest...","Circulation or nerve problem",["Circulation or nerve problem","Better healing","Normal digestion"],"Blood flow and nerve function are important after injury."],
   ["Mechanism of injury means...","How the injury happened",["How the injury happened","The organ name","A hormone level"],"Mechanism helps predict possible damaged structures."]
  ]
 }},
Integumentary:{
 emoji:"🧴", pos:[76,84], card:"Skin Shield",
 lesson:{
  easy:"Skin protects the body and helps sense touch.",
  normal:"The integumentary system includes skin, hair, nails, and glands. It helps temperature control.",
  difficult:"Skin barriers help prevent infection and fluid loss."
 },
 qs:{
  easy:[
   ["The largest organ of the body is the...","Skin",["Skin","Heart","Lung"],"Skin covers and protects the body."],
   ["Skin helps you sense...","Touch",["Touch","Blood type","Bone marrow"],"Nerves in skin detect touch, pressure, pain, and temperature."],
   ["Sweating helps the body...","Cool down",["Cool down","Digest faster","Pump blood"],"Sweat evaporation helps reduce body temperature."]
  ],
  normal:[
   ["Skin helps control body...","Temperature",["Temperature","Bone length","Blood type"],"Skin blood flow and sweating help thermoregulation."],
   ["The skin system is called the...","Integumentary system",["Integumentary system","Endocrine system","Urinary system"],"Integumentary means skin, hair, nails, and glands."],
   ["Melanin helps protect against...","UV radiation",["UV radiation","Fractures","Low oxygen"],"Melanin pigment absorbs some UV light."]
  ],
  difficult:[
   ["A break in skin increases risk of...","Infection",["Infection","Extra ATP","More cartilage"],"Skin is a barrier against microbes."],
   ["Severe burns can disturb...","Fluid balance",["Fluid balance","Bone length","Memory only"],"Skin helps prevent fluid loss."],
   ["Inflammation often includes redness, heat, swelling, and...","Pain",["Pain","Better oxygen storage","Bone growth"],"Inflammation is a protective response."]
  ]
 }}
};



// Extra question bank so every topic has 10 unique questions per difficulty.
const extraQuestions = {
Cells:{
 easy:[
  ["Cells are found in...","Living things",["Living things","Only rocks","Only water"],"All living things are made of one or more cells."],
  ["The cell membrane is like a...","Gate",["Gate","Hammer","Bone"],"It controls what can move in and out."],
  ["DNA gives cells...","Instructions",["Instructions","Air","Sweat"],"DNA carries information for how cells work."],
  ["Cells group together to make...","Tissues",["Tissues","Planets","Shoes"],"Similar cells working together form tissues."],
  ["A cell needs energy to...","Do work",["Do work","Disappear","Become air"],"Cells need energy for movement, repair, and transport."],
  ["The nucleus is usually the cell's...","Control center",["Control center","Gas tank","Outer skin"],"It holds DNA and helps control cell activities."],
  ["A selectively permeable membrane lets...","Some things pass",["Some things pass","Everything pass","Nothing ever pass"],"Selective means it chooses what can cross more easily."]
 ],
 normal:[
  ["A selectively permeable membrane means...","Only some substances cross easily",["Only some substances cross easily","Nothing can cross","Only bones can cross"],"Cell membranes control movement to help maintain balance."],
  ["Mitochondria are strongly linked to...","ATP production",["ATP production","Bone growth only","Making urine"],"Mitochondria help release usable energy from food."],
  ["A cell placed in a very salty solution may...","Lose water",["Lose water","Grow bones","Make oxygen"],"Water moves toward the area with more dissolved particles."],
  ["Passive transport requires...","No cell energy",["No cell energy","ATP every time","A tendon"],"Diffusion and osmosis are passive processes."],
  ["Active transport moves substances...","Against a gradient",["Against a gradient","Only into bones","Only through air"],"Moving against a gradient needs energy."],
  ["Cell receptors usually bind to...","Signals",["Signals","Fractures","Cartilage"],"Receptors help cells respond to messages."],
  ["Homeostasis means keeping internal conditions...","Stable",["Stable","Random","Frozen"],"Cells and organs work together to keep balance."]
 ],
 difficult:[
  ["A concentration gradient describes a difference in...","Particle amount",["Particle amount","Bone shape","Muscle size"],"Gradients affect diffusion and transport."],
  ["The sodium-potassium pump is an example of...","Active transport",["Active transport","Simple diffusion","Bone remodeling"],"It uses ATP to move ions across the membrane."],
  ["Cell signaling usually starts when a signal binds a...","Receptor",["Receptor","Ligament","Capillary"],"Receptor binding helps trigger cell responses."],
  ["Membrane proteins can help with...","Transport and signaling",["Transport and signaling","Making bones only","Chewing food"],"Proteins in membranes have many jobs."],
  ["If ATP production drops, active transport may...","Slow down",["Slow down","Get stronger","Stop needing membranes"],"Active transport depends on energy."],
  ["Osmotic imbalance can change cell...","Size",["Size","Species","Skeleton"],"Water movement can make cells shrink or swell."],
  ["Homeostatic failure can affect...","Cell function",["Cell function","Only hair color","Only shoe size"],"Cells need stable conditions to work well."]
 ]},
Skeletal:{
 easy:[["Bones help your body...","Stand and move",["Stand and move","Breathe air only","Digest sugar"],"The skeleton gives shape and support."],["Ribs protect the...","Heart and lungs",["Heart and lungs","Knees","Fingers only"],"The rib cage protects chest organs."],["Joints are where bones...","Meet",["Meet","Make insulin","Turn to muscle"],"Joints allow movement between bones."],["The backbone protects the...","Spinal cord",["Spinal cord","Stomach acid","Skin"],"Vertebrae surround the spinal cord."],["Bones are hard because they store...","Minerals",["Minerals","Air","Sweat"],"Minerals like calcium help bones stay strong."],["A cast helps a broken bone...","Heal in place",["Heal in place","Pump blood","Make hormones"],"Keeping a fracture still helps healing."],["Cartilage is usually...","Smooth and cushioning",["Smooth and cushioning","Sharp and dry","A nerve cell"],"Cartilage helps protect joints."]],
 normal:[["A ligament mainly stabilizes a...","Joint",["Joint","Alveolus","Stomach"],"Ligaments connect bone to bone around joints."],["Bone marrow is inside many...","Bones",["Bones","Lungs","Nerves only"],"Marrow fills spaces inside certain bones."],["The axial skeleton includes the skull, ribs, and...","Vertebral column",["Vertebral column","Fingers only","Ankle tendons"],"The axial skeleton forms the central body axis."],["The appendicular skeleton includes...","Limbs",["Limbs","Skull only","Lungs"],"Arms, legs, shoulders, and hips are appendicular."],["Synovial joints are usually...","Freely movable",["Freely movable","Never movable","Only in teeth"],"Many body movements happen at synovial joints."],["Cartilage has less blood supply than bone, so it often heals...","Slowly",["Slowly","Instantly","By breathing"],"Less blood flow can slow repair."],["A growth plate is made mostly of...","Cartilage",["Cartilage","Air sacs","Neurons"],"Growth plates help long bones lengthen."]],
 difficult:[["Wolff's law relates bone strength to...","Mechanical stress",["Mechanical stress","Blood sugar","Skin pigment"],"Bone adapts to forces placed on it."],["Osteoblasts are cells that...","Build bone",["Build bone","Break down food","Carry oxygen"],"Osteoblasts form new bone tissue."],["Osteoclasts are cells that...","Break down bone",["Break down bone","Make bile","Send reflexes"],"Bone remodeling needs both breakdown and rebuilding."],["Synovial fluid helps joints by...","Lubricating movement",["Lubricating movement","Making ATP","Filtering urine"],"It reduces friction inside synovial joints."],["A torn ACL is injury to a knee...","Ligament",["Ligament","Alveolus","Hormone"],"The ACL stabilizes the knee joint."],["Low calcium can affect bone and...","Muscle/nerve function",["Muscle/nerve function","Hair length only","Lung shape only"],"Calcium is important in bones and signaling."],["Osteoporosis means bone density is...","Lower",["Lower","Higher always","Unchanged"],"Lower density increases fracture risk."]]},
Muscular:{
 easy:[["Your biceps help bend your...","Elbow",["Elbow","Lung","Skull"],"The biceps crosses the elbow joint."],["Muscles pull on bones using...","Tendons",["Tendons","Alveoli","Hormones"],"Tendons attach muscle to bone."],["Exercise can make muscles...","Stronger",["Stronger","Disappear","Turn into air"],"Muscles adapt to safe repeated use."],["Muscles need oxygen and food to make...","Energy",["Energy","Bones","Hair color"],"Muscle cells need energy to work."],["A muscle cramp is a sudden...","Tightening",["Tightening","Fracture","Breath"],"Cramps are involuntary muscle contractions."],["The heart is made of...","Cardiac muscle",["Cardiac muscle","Bone","Cartilage"],"Cardiac muscle contracts to pump blood."],["Smooth muscle is found in...","Organs",["Organs","Hair only","Teeth only"],"Smooth muscle helps organs move materials."]],
 normal:[["Muscles often work in...","Opposing pairs",["Opposing pairs","Only circles","Air sacs"],"One muscle can contract while another relaxes."],["The hamstrings are located at the back of the...","Thigh",["Thigh","Neck","Forearm"],"Hamstrings bend the knee and extend the hip."],["A tendon transfers force from muscle to...","Bone",["Bone","Air","Blood sugar"],"This lets contraction cause movement."],["Skeletal muscle fibers contain...","Actin and myosin",["Actin and myosin","Alveoli","Nephrons"],"These proteins slide to create contraction."],["Muscle fatigue can happen when energy supply...","Cannot keep up",["Cannot keep up","Turns to bone","Makes extra joints"],"Working muscles need enough ATP and oxygen."],["The diaphragm is skeletal muscle used for...","Breathing",["Breathing","Filtering urine","Making insulin"],"It contracts during inhalation."],["Hypertrophy means muscle cells get...","Larger",["Larger","Smaller always","Replaced by bone"],"Training can increase muscle fiber size."]],
 difficult:[["The sliding filament theory involves actin and...","Myosin",["Myosin","Insulin","Bile"],"Myosin pulls actin filaments during contraction."],["Calcium is stored in muscle cells mainly in the...","Sarcoplasmic reticulum",["Sarcoplasmic reticulum","Alveoli","Bladder"],"It releases calcium for contraction."],["A motor unit includes a motor neuron and...","Muscle fibers it controls",["Muscle fibers it controls","The whole skeleton","A kidney tubule"],"Motor units link nerves to muscle action."],["Acetylcholine is released at the...","Neuromuscular junction",["Neuromuscular junction","Bone marrow","Small intestine"],"It helps start skeletal muscle contraction."],["Eccentric contraction means a muscle contracts while...","Lengthening",["Lengthening","Disappearing","Making bile"],"This happens when controlling a movement against force."],["Fast-twitch fibers are useful for...","Powerful quick actions",["Powerful quick actions","Only digestion","Filtering blood"],"They fatigue faster but produce quick force."],["Isometric contraction means muscle length mostly...","Stays the same",["Stays the same","Triples","Turns liquid"],"Force is produced without obvious movement."]]},
Nervous:{
 easy:[["Nerves help you feel...","Touch and pain",["Touch and pain","Blood type","Bone color"],"Sensory nerves carry information."],["The spinal cord is inside the...","Backbone",["Backbone","Stomach","Arm muscle"],"Vertebrae protect it."],["Your brain helps you...","Think",["Think","Make urine only","Become taller instantly"],"The brain controls thoughts and actions."],["A reflex can happen...","Fast",["Fast","Only next week","Never"],"Reflexes protect the body quickly."],["Eyes send information to the...","Brain",["Brain","Kidney","Tendon"],"The brain interprets sensory information."],["Numbness means reduced...","Feeling",["Feeling","Digestion","Bone length"],"Nerves help create sensation."],["The nervous system sends...","Messages",["Messages","Bile","Cartilage"],"Signals travel through nerves and neurons."]],
 normal:[["Sensory neurons carry information...","Toward the CNS",["Toward the CNS","Only to bones","Out of the body"],"They bring sensory input to the brain/spinal cord."],["Motor neurons carry commands to...","Muscles or glands",["Muscles or glands","Air sacs only","Food"],"Motor signals cause action."],["The autonomic nervous system controls mostly...","Involuntary functions",["Involuntary functions","Only school thoughts","Bone color"],"It affects heart rate, digestion, and more."],["The sympathetic system is linked with...","Fight-or-flight",["Fight-or-flight","Rest-and-digest only","Bone repair only"],"It prepares the body for stress."],["The parasympathetic system supports...","Rest-and-digest",["Rest-and-digest","Sprint response only","Fractures"],"It calms and supports digestion."],["Myelin helps nerve signals travel...","Faster",["Faster","Slower always","Into bones only"],"Myelin insulates axons."],["A synapse lets neurons...","Communicate",["Communicate","Make urine","Store calcium only"],"Signals pass between neurons at synapses."]],
 difficult:[["An action potential travels along the...","Axon",["Axon","Ligament","Alveolus"],"Axons carry electrical signals away from the cell body."],["Depolarization often involves sodium moving...","Into the neuron",["Into the neuron","Into bone marrow","Out of the lungs"],"Ion movement changes membrane voltage."],["The refractory period helps action potentials move...","One direction",["One direction","Both directions forever","Into cartilage"],"It prevents immediate re-firing behind the signal."],["Neurotransmitter reuptake means it is taken back into the...","Sending neuron",["Sending neuron","Kidney","Tendon"],"Reuptake helps end or recycle signals."],["The cerebellum is important for...","Coordination",["Coordination","Blood filtering","Bile storage"],"It helps fine-tune movement."],["The brainstem controls vital functions like...","Breathing and heart rate",["Breathing and heart rate","Hair style","Bone color"],"It supports automatic survival functions."],["A dermatome is an area of skin served by a...","Spinal nerve",["Spinal nerve","Hormone","Bone cell"],"Dermatomes help map sensory nerve patterns."]]},
Circulatory:{
 easy:[["Blood travels through...","Blood vessels",["Blood vessels","Bones only","Hair"],"Vessels are tubes for blood flow."],["The heart has chambers that fill and...","Pump",["Pump","Chew","Think"],"The heart moves blood forward."],["Blood carries nutrients to...","Cells",["Cells","Rocks","Shoes"],"Cells need nutrients and oxygen."],["A heartbeat is made by heart muscle...","Contracting",["Contracting","Melting","Digesting"],"Contraction pumps blood."],["White blood cells help fight...","Germs",["Germs","Bones","Air"],"They are part of immune defense."],["Platelets help blood...","Clot",["Clot","Breathe","Make hormones"],"Platelets help stop bleeding."],["The heart is in the...","Chest",["Chest","Knee","Hand"],"It sits between the lungs."]],
 normal:[["Arteries usually have thicker walls because pressure is...","Higher",["Higher","Zero","Only in veins"],"Arteries carry blood away under pressure."],["Veins have valves to help prevent...","Backflow",["Backflow","Oxygen use","Bone growth"],"Valves help blood return to the heart."],["Capillary walls are thin to allow...","Exchange",["Exchange","Fractures","Nerve storage"],"Thin walls help gases and nutrients move."],["Plasma is the...","Liquid part of blood",["Liquid part of blood","Hard bone shell","Air sac"],"Blood cells travel in plasma."],["Hemoglobin is found in...","Red blood cells",["Red blood cells","Ligaments","Neurons only"],"It binds oxygen."],["Blood returning from the body enters the right...","Atrium",["Atrium","Femur","Alveolus"],"The right atrium receives systemic venous blood."],["The left ventricle pumps blood to the...","Body",["Body","Bladder only","Stomach only"],"It pumps oxygenated blood into the aorta."]],
 difficult:[["Stroke volume means blood pumped per...","Beat",["Beat","Minute only","Breath"],"Cardiac output uses stroke volume times heart rate."],["Vasodilation means vessels...","Widen",["Widen","Narrow","Become bones"],"Wider vessels lower resistance."],["The pulmonary circuit carries blood to the...","Lungs",["Lungs","Kidneys only","Skin only"],"It exchanges carbon dioxide and oxygen."],["The systemic circuit carries blood to the...","Body tissues",["Body tissues","Alveoli only","Bladder only"],"It delivers oxygen to organs."],["Atherosclerosis narrows arteries with...","Plaque",["Plaque","Alveoli","Bile"],"Plaque buildup reduces blood flow."],["Mean arterial pressure depends on cardiac output and...","Resistance",["Resistance","Skin color","Bone length"],"Blood pressure relates to flow and vessel resistance."],["Venous return is helped by skeletal muscle and...","Valves",["Valves","Bile","Cartilage dust"],"Muscle contractions squeeze veins."]]},
Respiratory:{
 easy:[["You inhale to bring in...","Oxygen",["Oxygen","Urine","Bones"],"Oxygen is needed by cells."],["You exhale to remove...","Carbon dioxide",["Carbon dioxide","Calcium bones","Insulin"],"Carbon dioxide is a waste gas."],["The nose helps warm and filter...","Air",["Air","Blood","Urine"],"Air passes through the nose/mouth to lungs."],["The windpipe is also called the...","Trachea",["Trachea","Femur","Neuron"],"The trachea carries air."],["The lungs are in the...","Chest",["Chest","Foot","Wrist"],"The lungs sit inside the rib cage."],["Breathing faster usually brings in more...","Air",["Air","Bone","Bile"],"Faster breathing moves more air."],["The diaphragm moves down when you...","Inhale",["Inhale","Blink","Chew"],"This helps pull air into the lungs."]],
 normal:[["Bronchi branch from the...","Trachea",["Trachea","Femur","Bladder"],"Bronchi carry air into each lung."],["Alveoli are surrounded by...","Capillaries",["Capillaries","Ligaments","Tendons"],"Capillaries allow gas exchange with blood."],["Oxygen moves by diffusion from alveoli to...","Blood",["Blood","Bone marrow","Stomach"],"It moves from higher to lower concentration."],["Carbon dioxide moves from blood into...","Alveoli",["Alveoli","Bones","Muscles only"],"Then it is exhaled."],["The pleura are membranes around the...","Lungs",["Lungs","Kidneys","Brain"],"Pleura reduce friction during breathing."],["External respiration happens between alveoli and...","Blood",["Blood","Food","Bone"],"It is gas exchange in the lungs."],["Internal respiration happens between blood and...","Tissues",["Tissues","Air outside","Cartilage only"],"Tissues receive oxygen and release carbon dioxide."]],
 difficult:[["Surfactant helps alveoli...","Stay open",["Stay open","Become bone","Make insulin"],"It reduces surface tension."],["The medulla helps regulate...","Breathing rate",["Breathing rate","Bone density","Bile storage"],"Brainstem centers respond to CO2 and pH."],["High CO2 often increases breathing drive because it affects...","pH",["pH","Hair color","Ligament length"],"CO2 forms acid-related compounds in blood."],["Tidal volume means air moved in a normal...","Breath",["Breath","Heartbeat","Urination"],"It is the volume of one quiet breath."],["Residual volume is air left after...","Max exhalation",["Max exhalation","Eating","Blinking"],"Some air remains to keep lungs from collapsing."],["Hypoxia means low...","Oxygen",["Oxygen","Calcium only","Skin oil"],"Tissues need oxygen to function."],["Perfusion in lungs refers to...","Blood flow",["Blood flow","Food movement","Bone repair"],"Good gas exchange needs ventilation and perfusion."]]},
Digestive:{
 easy:[["Chewing starts digestion in the...","Mouth",["Mouth","Knee","Lung"],"Mechanical digestion starts with chewing."],["Food travels down the...","Esophagus",["Esophagus","Trachea","Femur"],"The esophagus moves food to the stomach."],["The stomach uses acid to help break down...","Food",["Food","Air","Bone"],"Stomach acid helps digestion."],["Nutrients give the body...","Energy and materials",["Energy and materials","Only dreams","No help"],"Nutrients support cells."],["The large intestine absorbs mostly...","Water",["Water","Oxygen","Bones"],"It helps form solid waste."],["Waste leaves the body as...","Feces",["Feces","Oxygen","Cartilage"],"Undigested material exits the digestive tract."],["Saliva helps make food easier to...","Swallow",["Swallow","Hear","Pump"],"Saliva moistens food and starts digestion."]],
 normal:[["Peristalsis means wave-like muscle...","Contractions",["Contractions","Fractures","Breaths"],"It moves food through the digestive tract."],["Mechanical digestion means physically...","Breaking food apart",["Breaking food apart","Making hormones","Filtering blood"],"Chewing and churning are examples."],["Chemical digestion uses enzymes to break...","Molecules",["Molecules","Bones","Nerves"],"Enzymes break large nutrients into smaller ones."],["Amylase helps break down...","Carbohydrates",["Carbohydrates","Bones","Oxygen"],"Salivary amylase starts starch digestion."],["The liver makes...","Bile",["Bile","Insulin only","Neurons"],"Bile helps fat digestion."],["The pancreas releases digestive enzymes into the...","Small intestine",["Small intestine","Skull","Lungs"],"Pancreatic enzymes work in the small intestine."],["The colon is another name for the...","Large intestine",["Large intestine","Stomach","Esophagus"],"The colon absorbs water and forms feces."]],
 difficult:[["Proteases break down...","Proteins",["Proteins","Oxygen","Bones"],"Proteases digest proteins into smaller pieces."],["Lipase breaks down...","Fats",["Fats","Nerves","Air"],"Lipase digests lipids."],["Bile emulsifies fats, meaning it...","Breaks fat into droplets",["Breaks fat into droplets","Makes red blood cells","Starts reflexes"],"Smaller droplets are easier for enzymes to digest."],["The hepatic portal vein carries absorbed nutrients to the...","Liver",["Liver","Femur","Lung"],"The liver processes many absorbed nutrients."],["Microvilli increase absorption by increasing...","Surface area",["Surface area","Blood pressure","Joint friction"],"More surface gives more space for absorption."],["The pancreas also helps regulate blood sugar with...","Insulin and glucagon",["Insulin and glucagon","Alveoli","Ligaments"],"It has digestive and endocrine jobs."],["Chyme is partly digested food leaving the...","Stomach",["Stomach","Brain","Kidney"],"Chyme enters the small intestine."]]},
Endocrine:{
 easy:[["Glands make...","Hormones",["Hormones","Bones","Air"],"Endocrine glands release chemical messages."],["Hormones travel in the...","Blood",["Blood","Hair","Teeth"],"Blood carries many hormones around the body."],["Insulin helps cells take in...","Glucose",["Glucose","Air","Bone"],"Glucose is blood sugar."],["Adrenaline can make your heart beat...","Faster",["Faster","Never","Backward"],"It prepares the body for action."],["The thyroid is a...","Gland",["Gland","Bone","Nerve gap"],"The thyroid releases hormones."],["Hormones affect target...","Cells",["Cells","Rocks","Shoes"],"Only cells with matching receptors respond."],["The endocrine system helps body...","Control",["Control","Disappear","Float"],"Hormones regulate body processes."]],
 normal:[["A target cell needs the correct...","Receptor",["Receptor","Fracture","Alveolus"],"Hormones bind to matching receptors."],["The pancreas releases insulin when blood sugar is...","High",["High","Always zero","Only in bones"],"Insulin lowers blood glucose."],["Glucagon is released when blood sugar is...","Low",["Low","Very high only","In the lungs"],"Glucagon raises blood glucose."],["The pituitary is often called the master...","Gland",["Gland","Bone","Vessel"],"It controls several other endocrine glands."],["Cortisol is linked to long-term...","Stress response",["Stress response","Bone-to-bone connection","Air exchange"],"Cortisol helps manage stress and metabolism."],["Thyroid hormone affects metabolic...","Rate",["Rate","Bone shape","Skin color only"],"It influences how fast cells use energy."],["Negative feedback helps prevent hormone levels from becoming too...","High or low",["High or low","Colorful","Bony"],"Feedback helps maintain balance."]],
 difficult:[["The hypothalamus connects the nervous system to the...","Endocrine system",["Endocrine system","Skeletal system only","Digestive tract only"],"It controls pituitary hormone release."],["ADH is released by the posterior pituitary and acts on...","Kidneys",["Kidneys","Femur","Alveoli"],"ADH increases water reabsorption."],["TSH stimulates the...","Thyroid",["Thyroid","Bladder","Cartilage"],"Thyroid-stimulating hormone targets the thyroid gland."],["Steroid hormones can pass through cell membranes because they are...","Lipid-soluble",["Lipid-soluble","Made of bone","Always gases"],"They often bind receptors inside cells."],["Peptide hormones usually bind receptors on the cell...","Membrane",["Membrane","Femur","Alveolus"],"They often cannot pass directly through the lipid membrane."],["Type 1 diabetes involves too little...","Insulin",["Insulin","Oxygen","Cartilage"],"The body cannot make enough insulin."],["A feedback loop includes stimulus, response, and...","Control center",["Control center","Fracture","Tendon"],"Control systems compare levels and adjust responses."]]},
Urinary:{
 easy:[["You have two...","Kidneys",["Kidneys","Brains","Hearts"],"Most people have two kidneys."],["Urine is liquid...","Waste",["Waste","Air","Bone"],"Urine carries wastes out."],["Drinking water helps the urinary system...","Work",["Work","Make bones","Stop breathing"],"Water supports filtering and balance."],["The bladder is like a storage...","Bag",["Bag","Bone","Nerve"],"It stores urine."],["Pee leaves through the...","Urethra",["Urethra","Esophagus","Trachea"],"The urethra carries urine out."],["Kidneys clean/filter the...","Blood",["Blood","Air","Food in mouth"],"Kidneys remove wastes from blood."],["The urinary system helps balance body...","Water",["Water","Shoe size","Hair style"],"Fluid balance is a major job."]],
 normal:[["The kidneys regulate electrolytes such as sodium and...","Potassium",["Potassium","Oxygen gas","Cartilage"],"Electrolytes help nerves, muscles, and fluid balance."],["Filtration first happens in the nephron's...","Glomerulus",["Glomerulus","Alveolus","Ligament"],"Blood is filtered at the glomerulus."],["Reabsorption means useful substances move back into the...","Blood",["Blood","Air","Bone"],"The body keeps needed water and nutrients."],["Urea is a waste from protein...","Breakdown",["Breakdown","Breathing","Bone growth"],"The kidneys remove urea in urine."],["Urinalysis can test urine for signs of...","Health problems",["Health problems","Haircuts","Joint names"],"Urine can show clues about hydration or disease."],["The renal artery brings blood to the...","Kidney",["Kidney","Lung","Skin"],"Renal means kidney."],["The renal vein carries filtered blood away from the...","Kidney",["Kidney","Stomach","Brain"],"Blood leaves the kidney through the renal vein."]],
 difficult:[["The glomerular filtration rate measures kidney...","Filtering rate",["Filtering rate","Breathing rate","Bone density"],"GFR estimates how well kidneys filter blood."],["Aldosterone increases sodium reabsorption in the...","Kidney tubules",["Kidney tubules","Alveoli","Tendons"],"Water often follows sodium."],["ADH acts mainly on collecting ducts to increase water...","Reabsorption",["Reabsorption","Digestion","Bone growth"],"More water returns to the blood."],["The loop of Henle helps create a concentration...","Gradient",["Gradient","Fracture","Reflex"],"This helps concentrate urine."],["Electrolyte imbalance can affect heart and...","Muscle function",["Muscle function","Hair color","Teeth shape"],"Ions are important for electrical activity."],["Protein in urine can suggest damage to the kidney...","Filter",["Filter","Ligament","Airway"],"A healthy filtration barrier usually keeps large proteins in blood."],["The kidneys help blood pressure by regulating fluid and...","Renin",["Renin","Bile","Myosin"],"Renin is part of a hormone pathway affecting pressure."]]},
Integumentary:{
 easy:[["Skin covers the...","Body",["Body","Only lungs","Only bones"],"Skin is the outer covering."],["Hair and nails are part of the...","Skin system",["Skin system","Urinary system","Respiratory system"],"They belong to the integumentary system."],["Skin helps keep germs...","Out",["Out","In","Growing faster"],"It is a protective barrier."],["Sweat comes from sweat...","Glands",["Glands","Bones","Alveoli"],"Sweat glands release sweat."],["Goosebumps happen in the...","Skin",["Skin","Kidney","Stomach"],"Tiny muscles in skin cause them."],["Touch receptors are found in the...","Skin",["Skin","Bladder only","Bone marrow"],"They help sense the environment."],["A cut breaks the skin...","Barrier",["Barrier","Bone","Airway"],"Broken skin can let germs enter."]],
 normal:[["The epidermis is the outer layer of...","Skin",["Skin","Bone","Lung"],"It forms the surface barrier."],["The dermis contains nerves, blood vessels, and...","Glands",["Glands","Alveoli","Nephrons"],"The dermis supports skin functions."],["Keratin helps make skin, hair, and nails...","Strong",["Strong","Liquid","Air-filled"],"Keratin is a tough protein."],["Sweating helps thermoregulation through...","Evaporation",["Evaporation","Fracture repair","Bile release"],"Evaporating sweat removes heat."],["Blood vessels in skin widen to lose...","Heat",["Heat","Bone","Oxygen only"],"Vasodilation near skin helps cooling."],["Sebaceous glands make...","Oil",["Oil","Urine","Insulin"],"Oil helps lubricate skin and hair."],["Melanocytes make...","Melanin",["Melanin","Myosin","Urea"],"Melanin gives pigment and some UV protection."]],
 difficult:[["The stratum corneum is mainly dead, keratinized...","Cells",["Cells","Bones","Neurons"],"It forms a tough outer barrier."],["Second-degree burns affect epidermis and part of the...","Dermis",["Dermis","Femur","Bladder"],"They go deeper than first-degree burns."],["Vasoconstriction in skin helps conserve...","Heat",["Heat","Urine","Bile"],"Narrow vessels reduce heat loss."],["The inflammatory response can bring immune cells through...","Blood vessels",["Blood vessels","Tendons","Alveoli only"],"Vessels help deliver immune cells to injured tissue."],["Severe skin damage can increase dehydration because of fluid...","Loss",["Loss","Storage","Creation from bone"],"Skin helps prevent water loss."],["Pressure ulcers happen when blood flow to skin is...","Reduced",["Reduced","Unlimited","Turned into air"],"Long pressure can damage tissue."],["The hypodermis contains fat that helps with cushioning and...","Insulation",["Insulation","Gas exchange","Nerve firing only"],"Fat under skin helps protect and keep heat."]]},
Injuries:{
 easy:[["If someone is badly hurt, first get...","Adult or medical help",["Adult or medical help","A harder workout","More running"],"Safety comes first."],["Pain and swelling after twisting a joint may be a...","Sprain",["Sprain","Cold","Hormone"],"Sprains involve ligaments at joints."],["A bone out of place at a joint is a...","Dislocation",["Dislocation","Strain","Cough"],"Dislocations happen at joints."],["A head hit followed by dizziness may be a...","Concussion",["Concussion","Sprain","Blister"],"Brain injuries need caution."],["Resting an injury can help it...","Heal",["Heal","Get worse","Disappear instantly"],"Rest reduces stress on injured tissues."],["A bruise is bleeding under the...","Skin",["Skin","Air","Bone marrow only"],"Small blood vessels can break under skin."],["Sharp severe pain after falling may mean...","Serious injury",["Serious injury","Nothing ever","More practice needed"],"Severe pain deserves help and assessment."]],
 normal:[["RICE often stands for rest, ice, compression, and...","Elevation",["Elevation","Exercise hard","Eating only"],"It is a common early care idea for minor soft-tissue injuries."],["A strain commonly affects the hamstring because it is a...","Muscle",["Muscle","Bone","Air sac"],"Strains involve muscles or tendons."],["A sprain is graded by severity of ligament...","Damage",["Damage","Color","Taste"],"More tearing usually means a more serious sprain."],["A stress fracture is often caused by repetitive...","Loading",["Loading","Breathing","Hormones only"],"Repeated force can overload bone."],["Swelling happens partly because fluid moves into...","Tissues",["Tissues","Air","Hair"],"Inflammation can increase local fluid."],["Numbness after injury may suggest a...","Nerve problem",["Nerve problem","Normal digestion","Skin pigment issue"],"Nerves are involved in sensation."],["Checking pulse past an injury helps assess...","Circulation",["Circulation","Digestion","Hormones"],"Blood flow is important after limb injuries."]],
 difficult:[["Point tenderness over bone can suggest...","Fracture",["Fracture","Mild hunger","Normal reflex"],"Localized bone pain after injury can be concerning."],["Compartment syndrome involves dangerous pressure inside a muscle...","Compartment",["Compartment","Alveolus","Gland"],"Pressure can reduce blood flow and nerve function."],["A mechanism with twisting plus planted foot can injure knee...","Ligaments",["Ligaments","Alveoli","Hormones"],"Twisting forces can stress knee stabilizers."],["Return-to-play after concussion should be...","Gradual and cleared",["Gradual and cleared","Immediate always","Hidden from adults"],"Brain recovery should be protected."],["Open fractures have higher risk of...","Infection",["Infection","Better oxygen","Extra cartilage"],"Broken skin allows germs to enter."],["Loss of function after injury means the person cannot...","Use the body part normally",["Use the body part normally","Digest sugar","Hear music"],"Function is part of injury assessment."],["Redness, heat, swelling, and pain are signs of...","Inflammation",["Inflammation","Gas exchange","Hormone storage"],"Inflammation is the body's response to damage."]]},
};

Object.keys(extraQuestions).forEach(topic=>{
  ["easy","normal","difficult"].forEach(level=>{
    data[topic].qs[level] = data[topic].qs[level].concat(extraQuestions[topic][level]);
  });
});


/* Bigger, more varied question system.
   Each topic + difficulty now gets 150 prepared questions built from different A&P concepts,
   and each 10-question round avoids repeated questions, repeated answers, and repeated concept types. */
const QUESTION_GOAL_PER_TOPIC_LEVEL = 150;
const ROUND_SIZE = 10;
const usedQuestionMemory = {};

const conceptBank = {
 Cells:[
  ["cell membrane","cell membrane",["rib cage","tendon"],"The cell membrane controls what enters and leaves the cell.","a substance must enter or leave a cell","movement across the cell border","cell border control"],
  ["nucleus","nucleus",["alveoli","ligament"],"The nucleus stores DNA and helps control cell activities.","a cell needs instructions for making proteins","DNA storage","cell control center"],
  ["mitochondria","mitochondria",["cartilage","bladder"],"Mitochondria help make ATP, the cell's usable energy.","a cell needs lots of usable energy","ATP production","energy-making organelle"],
  ["diffusion","diffusion",["fracture","digestion"],"Diffusion moves particles from high concentration to low concentration.","particles spread out without ATP","passive particle movement","high-to-low movement"],
  ["osmosis","osmosis",["cardiac output","reflex"],"Osmosis is the movement of water across a membrane.","water moves across a cell membrane","water balance","water diffusion"],
  ["active transport","active transport",["simple diffusion","joint movement"],"Active transport uses ATP to move substances against a gradient.","a cell moves particles from low to high concentration","ATP-powered transport","against-gradient movement"],
  ["homeostasis","homeostasis",["fracture repair","ventilation"],"Homeostasis means keeping internal body conditions stable.","the body keeps temperature, water, and chemicals balanced","internal balance","stable conditions"],
  ["receptor","receptor",["femur","ureter"],"Receptors let cells receive signals and respond.","a hormone or message must be detected by a cell","cell communication","signal detector"],
  ["DNA","DNA",["bile","plasma"],"DNA carries genetic instructions for cells.","a cell needs inherited instructions","genetic information","instruction molecule"],
  ["ATP","ATP",["melanin","urea"],"ATP is the usable energy molecule for cell work.","a cell needs quick energy for transport or repair","cell energy","energy molecule"]
 ],
 Skeletal:[
  ["skull","skull",["sternum","pelvis"],"The skull protects the brain.","the brain needs bony protection","brain protection","head bone protection"],
  ["rib cage","rib cage",["femur","radius"],"The rib cage protects the heart and lungs.","chest organs need protection","heart and lung protection","chest cage"],
  ["ligament","ligament",["tendon","alveolus"],"Ligaments connect bone to bone and stabilize joints.","a joint needs bone-to-bone support","joint stability","bone-to-bone connector"],
  ["cartilage","cartilage",["neuron","urethra"],"Cartilage cushions joints and reduces friction.","a joint needs smooth cushioning","joint cushioning","smooth joint tissue"],
  ["bone marrow","bone marrow",["pleura","dermis"],"Bone marrow makes many blood cells.","the body needs new blood cells","blood cell production","inside-bone tissue"],
  ["fracture","fracture",["strain","sprain"],"A fracture is a broken or cracked bone.","a fall causes sharp bone pain","bone injury","broken bone"],
  ["osteoblast","osteoblast",["osteoclast","neuron"],"Osteoblasts build new bone tissue.","bone needs rebuilding","bone building","builder bone cell"],
  ["osteoclast","osteoclast",["osteoblast","platelet"],"Osteoclasts break down bone during remodeling.","old bone must be removed","bone breakdown","remodeling cell"],
  ["synovial joint","synovial joint",["alveolus","nephron"],"Synovial joints allow lots of movement and contain lubricating fluid.","a knee or elbow moves freely","movable joint","fluid-filled joint"],
  ["osteoporosis","osteoporosis",["asthma","diabetes"],"Osteoporosis lowers bone density and raises fracture risk.","bones become weaker and easier to break","low bone density","fragile bones"]
 ],
 Muscular:[
  ["tendon","tendon",["ligament","capillary"],"Tendons connect muscle to bone.","muscle force must pull on bone","muscle-to-bone connector","movement attachment"],
  ["skeletal muscle","skeletal muscle",["cardiac muscle","smooth muscle"],"Skeletal muscle is usually voluntary and moves bones.","you choose to lift your arm","voluntary movement","body movement muscle"],
  ["cardiac muscle","cardiac muscle",["skeletal muscle","smooth muscle"],"Cardiac muscle is found in the heart.","the heart contracts to pump blood","heart muscle","pumping muscle"],
  ["smooth muscle","smooth muscle",["skeletal muscle","cartilage"],"Smooth muscle moves materials through organs.","food moves through intestines without you thinking","organ movement","involuntary organ muscle"],
  ["strain","strain",["sprain","fracture"],"A strain injures a muscle or tendon.","a sprint causes a pulled hamstring","muscle/tendon injury","pulled muscle"],
  ["actin and myosin","actin and myosin",["bile and insulin","alveoli and bronchi"],"Actin and myosin slide past each other during contraction.","muscle fibers shorten","contractile proteins","sliding filament parts"],
  ["calcium","calcium",["urea","melanin"],"Calcium helps start muscle contraction.","a muscle fiber must activate contraction","contraction signal","muscle activation ion"],
  ["ATP","ATP",["cartilage","plasma"],"ATP powers muscle contraction and relaxation.","muscle cells need energy to move","muscle energy","energy for contraction"],
  ["motor unit","motor unit",["nephron","villus"],"A motor unit is a motor neuron and the muscle fibers it controls.","a nerve tells muscle fibers to contract","nerve-muscle control","movement command unit"],
  ["diaphragm","diaphragm",["biceps","femur"],"The diaphragm is a muscle that helps breathing.","air is pulled into the lungs","breathing muscle","inhalation muscle"]
 ],
 Nervous:[
  ["neuron","neuron",["platelet","osteoblast"],"Neurons are nerve cells that send messages.","the body needs fast electrical communication","nerve cell","signal-sending cell"],
  ["brain","brain",["kidney","femur"],"The brain controls thinking, movement, and body signals.","the body needs a control center","main control center","thinking organ"],
  ["spinal cord","spinal cord",["esophagus","ureter"],"The spinal cord carries signals between brain and body.","messages travel through the backbone area","signal pathway","central nerve cable"],
  ["central nervous system","central nervous system",["digestive system","urinary system"],"The CNS is the brain and spinal cord.","brain and spinal cord are grouped together","brain/spinal cord system","main nervous system"],
  ["peripheral nervous system","peripheral nervous system",["endocrine system","skeletal system"],"The PNS includes nerves outside the brain and spinal cord.","nerves connect the CNS to the body","outside nerves","body nerve network"],
  ["reflex","reflex",["fracture","osmosis"],"A reflex is a fast automatic response.","you pull away from something hot quickly","quick protection","automatic response"],
  ["synapse","synapse",["capillary","villus"],"A synapse is the gap where neurons communicate.","one nerve cell passes a message to another","neuron gap","message crossing point"],
  ["neurotransmitter","neurotransmitter",["cartilage","bile"],"Neurotransmitters are chemical messengers between neurons.","a signal crosses a synapse","chemical nerve message","synapse chemical"],
  ["myelin","myelin",["melanin","plasma"],"Myelin helps nerve signals travel faster.","a nerve signal needs insulation","nerve insulation","speed helper"],
  ["concussion","concussion",["sprain","strain"],"A concussion is a brain injury after a hit or jolt.","a head hit causes dizziness or confusion","brain injury","head impact injury"]
 ],
 Circulatory:[
  ["heart","heart",["lung","kidney"],"The heart pumps blood through the body.","blood must move to tissues","blood pump","circulation organ"],
  ["artery","artery",["vein","ligament"],"Arteries carry blood away from the heart.","blood leaves the heart under pressure","away vessel","high-pressure vessel"],
  ["vein","vein",["artery","tendon"],"Veins carry blood back to the heart.","blood returns toward the heart","return vessel","back-to-heart vessel"],
  ["capillary","capillary",["neuron","cartilage"],"Capillaries exchange oxygen, nutrients, and wastes with tissues.","cells trade materials with blood","exchange vessel","tiny exchange tube"],
  ["red blood cell","red blood cell",["white blood cell","platelet"],"Red blood cells carry oxygen with hemoglobin.","oxygen must travel through blood","oxygen carrier","RBC job"],
  ["white blood cell","white blood cell",["red blood cell","plasma"],"White blood cells help fight infection.","the body responds to germs","immune blood cell","germ fighter"],
  ["platelet","platelet",["neuron","villus"],"Platelets help blood clot.","a cut needs bleeding to slow","clot helper","bleeding control"],
  ["plasma","plasma",["cartilage","melanin"],"Plasma is the liquid part of blood.","blood cells need a fluid to travel in","blood liquid","transport fluid"],
  ["cardiac output","cardiac output",["tidal volume","filtration rate"],"Cardiac output is the blood pumped per minute.","heart rate and stroke volume determine flow","blood per minute","heart output"],
  ["blood pressure","blood pressure",["bone density","lung volume"],"Blood pressure is force of blood against vessel walls.","vessels feel force from flowing blood","vessel pressure","circulation force"]
 ],
 Respiratory:[
  ["lungs","lungs",["kidneys","femur"],"The lungs bring in oxygen and remove carbon dioxide.","the body exchanges gases with air","breathing organs","gas exchange organs"],
  ["oxygen","oxygen",["urea","bile"],"Oxygen is used by cells to help make ATP.","cells need a gas from air","needed gas","cell energy gas"],
  ["carbon dioxide","carbon dioxide",["calcium","insulin"],"Carbon dioxide is a waste gas breathed out.","cells make a waste gas","waste gas","exhaled gas"],
  ["alveoli","alveoli",["nephrons","ligaments"],"Alveoli are tiny air sacs where gas exchange happens.","oxygen moves into blood in the lungs","air sacs","gas exchange sacs"],
  ["diaphragm","diaphragm",["biceps","femur"],"The diaphragm contracts to help inhale.","air is pulled into the lungs","breathing muscle","inhalation helper"],
  ["trachea","trachea",["esophagus","ureter"],"The trachea carries air to the bronchi.","air moves through the windpipe","windpipe","air tube"],
  ["bronchi","bronchi",["villi","tendons"],"Bronchi branch from the trachea into the lungs.","air enters each lung through branches","air branches","lung airways"],
  ["ventilation","ventilation",["peristalsis","filtration"],"Ventilation is moving air in and out of the lungs.","breathing moves air","air movement","breathing process"],
  ["surfactant","surfactant",["melanin","renin"],"Surfactant helps alveoli stay open.","tiny air sacs need to resist collapse","alveoli support","surface tension reducer"],
  ["hypoxia","hypoxia",["hypertension","hyperglycemia"],"Hypoxia means low oxygen in tissues.","tissues do not receive enough oxygen","low oxygen","oxygen shortage"]
 ],
 Digestive:[
  ["mouth","mouth",["kidney","lung"],"The mouth begins mechanical digestion by chewing.","food is first broken apart","chewing site","digestion start"],
  ["esophagus","esophagus",["trachea","urethra"],"The esophagus moves food from mouth to stomach.","swallowed food travels downward","food tube","swallowing pathway"],
  ["stomach","stomach",["heart","bladder"],"The stomach mixes food with acid and enzymes.","food is churned and chemically broken down","acid organ","food mixer"],
  ["small intestine","small intestine",["large intestine","skull"],"The small intestine absorbs most nutrients.","digested food enters the main absorption area","nutrient absorption","major absorber"],
  ["large intestine","large intestine",["small intestine","alveoli"],"The large intestine absorbs water and forms feces.","leftover material loses water","water absorption","colon function"],
  ["enzyme","enzyme",["ligament","neuron"],"Enzymes chemically break down food molecules.","large food molecules become smaller","chemical digestion helper","breakdown protein"],
  ["bile","bile",["insulin","urea"],"Bile helps digest fats by emulsifying them.","fat needs to be broken into droplets","fat digestion fluid","emulsifier"],
  ["liver","liver",["femur","trachea"],"The liver makes bile and processes nutrients.","nutrients from digestion are processed","bile maker","metabolic organ"],
  ["pancreas","pancreas",["spleen","cartilage"],"The pancreas releases digestive enzymes and hormones.","enzymes enter the small intestine","enzyme organ","digestion helper gland"],
  ["villi","villi",["alveoli","nephrons"],"Villi increase surface area for absorption.","the small intestine needs more absorbing surface","absorption folds","surface area helpers"]
 ],
 Endocrine:[
  ["hormone","hormone",["ligament","alveolus"],"Hormones are chemical messengers.","a gland sends a body message through blood","chemical message","endocrine signal"],
  ["gland","gland",["bone","villus"],"Glands release hormones in the endocrine system.","the body needs to send hormones","hormone maker","endocrine organ"],
  ["insulin","insulin",["glucagon","melanin"],"Insulin lowers blood glucose by helping cells take in glucose.","blood sugar is high after eating","lowers glucose","blood sugar lowering hormone"],
  ["glucagon","glucagon",["insulin","keratin"],"Glucagon raises blood glucose.","blood sugar is low between meals","raises glucose","blood sugar raising hormone"],
  ["thyroid","thyroid",["bladder","femur"],"The thyroid helps regulate metabolism.","body cells adjust energy use rate","metabolism gland","energy-rate control"],
  ["adrenaline","adrenaline",["bile","urea"],"Adrenaline supports fight-or-flight responses.","stress makes heart rate rise","stress hormone","emergency response"],
  ["pituitary gland","pituitary gland",["gallbladder","alveoli"],"The pituitary controls several other endocrine glands.","one gland directs other glands","master gland","hormone controller"],
  ["negative feedback","negative feedback",["positive fracture","osmosis"],"Negative feedback reduces a response when levels get too high or low.","the body turns a process down to keep balance","feedback control","balance loop"],
  ["target cell","target cell",["red blood cell","bone marrow"],"Target cells respond because they have matching receptors.","only certain cells react to a hormone","hormone responder","cell with receptor"],
  ["ADH","ADH",["ATP","DNA"],"ADH helps the kidneys retain water.","the body needs to save water","water-retaining hormone","kidney water signal"]
 ],
 Urinary:[
  ["kidney","kidney",["lung","femur"],"Kidneys filter blood and make urine.","blood needs waste removed","urine maker","blood filter"],
  ["bladder","bladder",["stomach","heart"],"The bladder stores urine.","urine waits before leaving the body","urine storage","storage sac"],
  ["ureter","ureter",["urethra","trachea"],"Ureters carry urine from kidneys to bladder.","urine travels from kidney to storage","kidney-to-bladder tube","urine pathway"],
  ["urethra","urethra",["ureter","esophagus"],"The urethra carries urine out of the body.","urine leaves the body","exit tube","urine outlet"],
  ["nephron","nephron",["neuron","alveolus"],"The nephron is the kidney's functional filtering unit.","the kidney filters and adjusts fluid","kidney unit","filtering unit"],
  ["glomerulus","glomerulus",["villus","synapse"],"The glomerulus is where blood filtration begins.","fluid first leaves blood in the nephron","filter ball","first filtration area"],
  ["reabsorption","reabsorption",["ventilation","peristalsis"],"Reabsorption returns useful substances to blood.","the body keeps water or glucose instead of losing it","keeping useful materials","back-to-blood movement"],
  ["urea","urea",["oxygen","bile"],"Urea is a waste product removed in urine.","protein breakdown creates a waste","urine waste","nitrogen waste"],
  ["electrolyte balance","electrolyte balance",["bone remodeling","gas exchange"],"Kidneys help balance salts and minerals in blood.","sodium and potassium levels need control","salt balance","mineral regulation"],
  ["ADH","ADH",["melanin","surfactant"],"ADH helps the body retain water through the kidneys.","dehydration signals water conservation","water-saving hormone","fluid balance signal"]
 ],
 Integumentary:[
  ["skin","skin",["heart","kidney"],"Skin is the body's largest organ and protective covering.","the body needs an outside barrier","body covering","largest organ"],
  ["epidermis","epidermis",["dermis","alveolus"],"The epidermis is the outer skin layer.","the surface layer protects the body","outer layer","surface skin"],
  ["dermis","dermis",["epidermis","ureter"],"The dermis contains nerves, vessels, glands, and support tissue.","skin needs blood vessels and sensors","deeper skin layer","support layer"],
  ["sweat gland","sweat gland",["thyroid gland","bone marrow"],"Sweat glands release sweat to help cool the body.","the body overheats and needs cooling","cooling gland","sweat maker"],
  ["melanin","melanin",["myosin","urea"],"Melanin helps protect skin from UV radiation.","sunlight reaches the skin","skin pigment","UV protection"],
  ["keratin","keratin",["insulin","plasma"],"Keratin strengthens skin, hair, and nails.","the outer layer needs toughness","strong protein","skin strength"],
  ["inflammation","inflammation",["ventilation","filtration"],"Inflammation can cause redness, heat, swelling, and pain.","skin is injured and the body responds","injury response","red/swollen response"],
  ["infection risk","infection risk",["bone density","tidal volume"],"Broken skin increases infection risk.","a cut opens the body barrier","germ entry risk","barrier break problem"],
  ["thermoregulation","thermoregulation",["digestion","bone remodeling"],"Thermoregulation is body temperature control.","sweat and skin blood flow adjust heat","temperature control","heat balance"],
  ["hypodermis","hypodermis",["brainstem","bronchus"],"The hypodermis contains fat for cushioning and insulation.","the body needs padding under skin","under-skin fat layer","insulation layer"]
 ],
 Injuries:[
  ["sprain","sprain",["strain","fracture"],"A sprain injures a ligament.","a joint twists and swells","ligament injury","twisted joint injury"],
  ["strain","strain",["sprain","dislocation"],"A strain injures a muscle or tendon.","a runner pulls a hamstring","muscle/tendon injury","pulled muscle injury"],
  ["fracture","fracture",["bruise","sprain"],"A fracture is a broken or cracked bone.","a fall causes sharp bone pain","bone break","broken bone injury"],
  ["dislocation","dislocation",["concussion","strain"],"A dislocation means a bone is out of place at a joint.","a shoulder looks out of place after impact","joint out of place","bone alignment injury"],
  ["concussion","concussion",["sprain","bruise"],"A concussion affects the brain after a hit or jolt.","a head hit causes confusion or dizziness","brain injury","head impact problem"],
  ["bruise","bruise",["fracture","asthma"],"A bruise is bleeding under the skin.","small blood vessels break after a bump","under-skin bleeding","purple mark injury"],
  ["swelling","swelling",["digestion","osmosis"],"Swelling often happens when fluid collects in injured tissue.","an injured ankle gets bigger","fluid in tissue","injury puffiness"],
  ["numbness","numbness",["hunger","bile"],"Numbness after injury may suggest nerve involvement.","a hurt limb loses feeling","possible nerve issue","reduced feeling"],
  ["loss of pulse","loss of pulse",["mild soreness","normal sweating"],"Loss of pulse can suggest a serious circulation problem.","blood flow past an injury is hard to find","circulation red flag","blood flow danger"],
  ["RICE","RICE",["ATP","DNA"],"RICE stands for rest, ice, compression, and elevation for many minor soft-tissue injuries.","a minor sprain needs early care","minor injury care","early soft-tissue care"]
 ]
};

const questionTemplates = [
 (x,t,l)=>[`A student sees ${x.clue}. Which A&P term fits best?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Which structure or idea is most connected to ${x.function}?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`In ${t}, what is responsible for ${x.function}?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`A case mentions ${x.problem}. What should you think of first?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Fill in the blank: ${x.answer} is linked to ${x.effect}.`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Which answer best matches this clue: ${x.effect}?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`During an A&P review, the teacher says "${x.function}." Which term is being reviewed?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Which option belongs with the ${t} topic and the clue "${x.clue}"?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`A patient/student example says: ${x.problem}. Pick the best explanation.`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Which pair is correct?`,`${x.answer} — ${x.effect}`,[`${x.answer} — ${x.effect}`,`${x.wrongs[0]} — ${x.effect}`,`${x.answer} — unrelated to ${t}`],x.why,x.name],
 (x,t,l)=>[`What would be most affected if ${x.answer} stopped working properly?`,x.function,[x.function,x.wrongs[0],x.wrongs[1]],x.why,x.name],
 (x,t,l)=>[`Choose the answer that explains ${x.effect}.`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`In a real-life body scenario, ${x.problem}. Which answer is the best match?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Which one is NOT just random for ${t}, but directly related to ${x.effect}?`,x.answer,[x.answer,...x.wrongs],x.why,x.name],
 (x,t,l)=>[`Mini diagnosis: ${x.clue}; ${x.problem}. What is the key term?`,x.answer,[x.answer,...x.wrongs],x.why,x.name]
];

function shuffleChoices(arr){
 const unique=[...new Set(arr)];
 while(unique.length<3) unique.push("None of these");
 return unique.sort(()=>Math.random()-0.5);
}

function levelPrefix(level){
 if(level==="easy") return "Simple check: ";
 if(level==="normal") return "Class-level check: ";
 return "Challenge check: ";
}

function buildQuestionFromConcept(concept, topic, level, templateIndex){
 const x={name:concept[0], answer:concept[1], wrongs:concept[2], why:concept[3], problem:concept[4], function:concept[5], effect:concept[6]};
 const made=questionTemplates[templateIndex % questionTemplates.length](x,topic,level);
 made[0]=levelPrefix(level)+made[0];
 made[2]=shuffleChoices(made[2]);
 made[4]=topic+"|"+level+"|"+x.name+"|"+templateIndex;
 return made;
}


// Concept-based anatomy reference question bank: rich labeled anatomical diagrams with a large,
// non-repeating pool of picture questions per topic (up to 50 each).
function detailedPictureSvg(topic){
 const imageFiles={
  Cells:"https://timvandevall.com/wp-content/uploads/animal-cell-diagram-worksheet-1.png",
  Skeletal:"https://innerbody.imgix.net/skeletal_system.png",
  Muscular:"https://anatomytool.org/sites/default/files/arm-thorax-ant.jpg",
  Nervous:"https://dr282zn36sxxg.cloudfront.net/datastreams/f-d%3Abc3b69daabd4a17514817d66cb93cfcc776c73d57e6c3b146c125474%2BIMAGE_TINY%2BIMAGE_TINY.1",
  Circulatory:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS7IDa3A1qbG-KUeLClW5Fi6HT_GB_gYS1HzyTNZ5pL-xsL6iazoS8SRyc&s=10",
  Respiratory:"https://www.thoughtco.com/thmb/8omUGJESSp-MBRdp06MgJS5pxz0=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/respiratory_system-578d72f73df78c09e96906ff.jpg",
  Digestive:"https://img.magnific.com/free-vector/human-medical-digestive-system_1308-134589.jpg?semt=ais_hybrid&w=740&q=80",
  Endocrine:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRjiJBree_otUtCceslxWDPKiEGPtfgPZhBLUZdrknboG7LKicRK6kHKcI&s=10",
  Urinary:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTvB_nNXVddr2TrvrA8KsaX10Qf9j_I3aBmNoOWeLPNYw&s=10",
  Integumentary:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSn3iPVdPgzDfIC0qnGEkpuKT9oW6sy1QWSXhrJsWmtRqwkIEYSbh-LY1ju&s=10",
  Injuries:"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTy7zmcVYV8o63xExGXxbBoyFL5xtrQo24aXArN3ZhoMvltgnyDVL3UIY7K&s=10"
 };
 const src=imageFiles[topic] || "IMAGES/anatomy_placeholder.png";
 return `<div class="anatomy-img-wrap">
  <img src="${src}" class="anatomy-image" alt="${topic} anatomy reference">
 </div>`;
}

const structureBank = {
 Cells:[
  ["Cell membrane",70,190,25,70,"The cell membrane is the outer boundary that controls what enters and leaves the cell."],
  ["Cytoplasm",300,280,50,35,"Cytoplasm is the jelly-like fluid that fills the cell and holds the organelles."],
  ["Nucleus",230,165,58,58,"The nucleus stores the cell's DNA and controls cell activities."],
  ["Nuclear envelope",230,103,15,10,"The nuclear envelope is the double membrane surrounding the nucleus."],
  ["Nucleolus",245,155,20,20,"The nucleolus, found inside the nucleus, helps build ribosomes."],
  ["Mitochondrion",365,120,40,24,"The mitochondrion is the organelle that produces most of the cell's ATP energy."],
  ["Golgi apparatus",175,140,40,20,"The Golgi apparatus packages and ships proteins to where they are needed."],
  ["Rough endoplasmic reticulum",137,255,40,20,"The rough endoplasmic reticulum is studded with ribosomes and helps make proteins."],
  ["Ribosomes",420,190,15,20,"Ribosomes are tiny structures that build proteins from instructions."],
  ["Lysosome",310,290,18,18,"A lysosome breaks down waste and worn-out cell parts."],
  ["Vacuole",110,230,20,20,"A vacuole stores water, nutrients, or waste inside the cell."],
  ["Centriole",340,90,16,12,"Centrioles help organize the cell during cell division."],
 ],
 Skeletal:[
  ["Head of femur",280,72,36,32,"The rounded head of the femur fits into the hip socket."],
  ["Greater trochanter",225,102,26,30,"The greater trochanter is a bony bump where several muscles attach."],
  ["Lesser trochanter",256,142,16,14,"The lesser trochanter is a smaller bump that anchors hip muscles."],
  ["Neck of femur",262,108,20,24,"The neck connects the femoral head to the long shaft."],
  ["Shaft",280,230,28,95,"The shaft is the long central part of a long bone."],
  ["Articular cartilage",280,72,36,12,"Articular cartilage cushions the joint surface where bones meet."],
  ["Epiphyseal line",280,126,34,6,"The epiphyseal line marks where growth once occurred in a young bone."],
  ["Spongy bone",278,85,26,22,"Spongy bone is the porous tissue found near the ends of long bones."],
  ["Medullary cavity",280,230,13,88,"The medullary cavity is the hollow center of the shaft that holds bone marrow."],
  ["Compact bone",258,230,10,88,"Compact bone is the dense outer layer that gives bones strength."],
  ["Periosteum",253,270,8,40,"The periosteum is the tough outer membrane covering the bone surface."],
  ["Endosteum",267,250,10,30,"The endosteum lines the inside of the medullary cavity."],
  ["Nutrient foramen",280,266,12,12,"The nutrient foramen is a small opening where blood vessels enter the bone."],
  ["Lateral epicondyle",310,344,22,16,"The lateral epicondyle is a bony bump on the outer side near the knee."],
  ["Medial epicondyle",258,344,22,16,"The medial epicondyle is a bony bump on the inner side near the knee."],
 ],
 Muscular:[
  ["Deltoid",130,72,34,28,"The deltoid is the rounded muscle that caps the shoulder."],
  ["Proximal tendon",130,52,18,14,"This tendon anchors the muscle to bone near the shoulder."],
  ["Biceps brachii",200,110,55,35,"The biceps brachii bends the elbow and rotates the forearm."],
  ["Muscle belly",225,155,60,50,"The muscle belly is the thick middle part where contraction happens."],
  ["Triceps brachii",250,210,55,40,"The triceps brachii straightens the elbow."],
  ["Fascicle bundle",210,118,35,15,"A fascicle is a bundle of muscle fibers wrapped together."],
  ["Fascia",230,95,70,25,"Fascia is the connective tissue sheath surrounding a muscle."],
  ["Humerus",353,135,10,75,"The humerus is the upper arm bone the muscles pull on."],
  ["Distal tendon",315,265,18,16,"This tendon connects the muscle to bone near the elbow."],
  ["Blood vessel",175,175,10,40,"Blood vessels supply working muscle with oxygen and nutrients."],
  ["Nerve",270,185,8,40,"A nerve carries signals that tell the muscle when to contract."],
 ],
 Nervous:[
  ["Cerebrum",230,130,110,70,"The cerebrum is the large, wrinkled part of the brain responsible for thought."],
  ["Frontal lobe",170,95,40,30,"The frontal lobe handles planning, decisions, and movement control."],
  ["Temporal lobe",175,165,35,28,"The temporal lobe processes hearing and memory."],
  ["Occipital lobe",320,120,35,28,"The occipital lobe processes visual information."],
  ["Brain folds",185,110,30,15,"Folds in the brain increase surface area for more neurons."],
  ["Cerebellum",336,211,42,30,"The cerebellum coordinates balance and smooth movement."],
  ["Brainstem",330,270,20,35,"The brainstem controls vital functions like breathing and heart rate."],
  ["Spinal cord",330,290,14,20,"The spinal cord carries signals between the brain and body."],
  ["Neuron cell body",420,250,24,20,"The cell body of a neuron contains the nucleus and organelles."],
  ["Dendrites",390,235,20,18,"Dendrites receive signals from other neurons."],
  ["Axon",468,250,30,10,"The axon carries nerve signals away from the cell body."],
  ["Myelin sheath",452,250,10,10,"The myelin sheath insulates the axon and speeds up signals."],
  ["Synapse",505,250,10,10,"A synapse is the tiny gap where signals pass to the next neuron."],
 ],
 Circulatory:[
  ["Right atrium",220,130,42,34,"The right atrium receives oxygen-poor blood returning from the body."],
  ["Left atrium",330,120,38,32,"The left atrium receives oxygen-rich blood from the lungs."],
  ["Right ventricle",228,222,46,54,"The right ventricle pumps blood to the lungs."],
  ["Left ventricle",322,225,48,56,"The left ventricle pumps blood out to the whole body."],
  ["Septum",278,190,10,90,"The septum is the muscular wall separating the left and right sides."],
  ["Aorta",300,70,22,32,"The aorta is the large artery that carries blood away from the heart."],
  ["Pulmonary artery",260,68,20,30,"The pulmonary artery carries oxygen-poor blood to the lungs."],
  ["Pulmonary vein",360,92,18,22,"The pulmonary vein carries oxygen-rich blood back to the heart."],
  ["Vena cava",185,76,18,26,"The vena cava returns oxygen-poor blood from the body to the heart."],
  ["Heart valve",278,172,12,10,"Heart valves keep blood flowing in one direction."],
  ["Coronary vessel",225,255,35,8,"Coronary vessels supply blood to the heart muscle itself."],
  ["Myocardium",278,250,90,40,"The myocardium is the muscular wall of the heart that contracts."],
 ],
 Respiratory:[
  ["Trachea",280,88,25,48,"The trachea, or windpipe, carries air toward the lungs."],
  ["Left bronchus",260,145,28,20,"The left bronchus carries air into the left lung."],
  ["Right bronchus",305,145,28,20,"The right bronchus carries air into the right lung."],
  ["Bronchioles",380,200,22,18,"Bronchioles are small branching airways inside the lungs."],
  ["Alveoli",406,228,54,38,"Alveoli are tiny air sacs where oxygen and carbon dioxide are exchanged."],
  ["Left lung",193,176,79,98,"The left lung brings in oxygen and is slightly smaller than the right."],
  ["Right lung",369,176,79,98,"The right lung is slightly larger and has more lobes."],
  ["Diaphragm",280,292,140,20,"The diaphragm is the muscle that drives breathing."],
  ["Pleura",280,160,179,129,"The pleura is the thin lining that protects and cushions the lungs."],
  ["Lung lobes",150,200,15,8,"Lobes are sections that divide each lung."],
 ],
 Digestive:[
  ["Esophagus",270,85,25,45,"The esophagus moves food from the mouth to the stomach."],
  ["Stomach",270,170,93,55,"The stomach mixes food with acid and enzymes to begin digestion."],
  ["Stomach lining",245,150,35,15,"Rugae are folds inside the stomach lining that expand as it fills."],
  ["Liver",380,140,50,37,"The liver produces bile and processes nutrients absorbed from food."],
  ["Gallbladder",360,152,15,14,"The gallbladder stores bile made by the liver."],
  ["Pancreas",250,225,55,18,"The pancreas releases digestive enzymes and hormones like insulin."],
  ["Duodenum",320,195,25,18,"The duodenum is the first section of the small intestine."],
  ["Small intestine",280,252,80,27,"The small intestine absorbs most nutrients from digested food."],
  ["Large intestine",280,270,115,47,"The large intestine absorbs water and forms waste."],
  ["Rectum",280,330,20,14,"The rectum stores waste before it leaves the body."],
 ],
 Endocrine:[
  ["Pineal gland",312,60,10,10,"The pineal gland helps regulate sleep by releasing melatonin."],
  ["Pituitary gland",280,80,18,18,"The pituitary gland is a master gland that controls other glands."],
  ["Hypothalamus",280,55,22,12,"The hypothalamus links the nervous system to the endocrine system."],
  ["Thyroid gland",280,200,70,45,"The thyroid gland regulates metabolism using hormones."],
  ["Parathyroid glands",240,185,10,8,"Parathyroid glands help control calcium levels in the blood."],
  ["Thymus",280,240,55,30,"The thymus helps the immune system mature, especially in children."],
  ["Adrenal gland",195,255,20,20,"Adrenal glands release stress hormones like adrenaline."],
  ["Pancreas",280,305,70,26,"The pancreas releases insulin and glucagon to control blood sugar."],
 ],
 Urinary:[
  ["Left kidney",196,155,61,84,"The kidneys filter waste and excess water from the blood."],
  ["Right kidney",364,155,61,84,"The kidneys filter waste and excess water from the blood."],
  ["Renal cortex",180,130,30,35,"The renal cortex is the outer region of the kidney."],
  ["Renal medulla",205,175,16,20,"The renal medulla is the inner region of the kidney."],
  ["Renal pelvis",218,154,14,16,"The renal pelvis collects urine before it enters the ureter."],
  ["Left ureter",225,263,15,55,"The ureter carries urine from the kidney to the bladder."],
  ["Right ureter",335,263,15,55,"The ureter carries urine from the kidney to the bladder."],
  ["Bladder",280,311,43,24,"The bladder stores urine until it is released from the body."],
  ["Urethra",280,340,10,10,"The urethra carries urine out of the body."],
  ["Renal artery",213,170,12,25,"The renal artery brings blood into the kidney for filtering."],
 ],
 Integumentary:[
  ["Epidermis",280,100,200,25,"The epidermis is the tough, waterproof outer layer of skin."],
  ["Dermis",280,178,198,48,"The dermis contains nerves, blood vessels, and hair follicles."],
  ["Hypodermis",280,262,198,32,"The hypodermis stores fat and connects skin to muscle."],
  ["Hair follicle",347,205,16,60,"A hair follicle is the pocket in skin where hair grows."],
  ["Hair shaft",355,65,8,20,"The hair shaft is the visible part of hair above the skin."],
  ["Sebaceous gland",340,216,18,18,"Sebaceous glands release oil that keeps skin and hair moisturized."],
  ["Sweat gland",170,200,20,20,"Sweat glands release sweat to help cool the body."],
  ["Nerve ending",230,170,14,12,"Nerve endings in the skin sense touch, pain, and temperature."],
  ["Blood vessel",420,180,10,40,"Blood vessels in the skin help control body temperature."],
  ["Sensory receptor",190,110,10,10,"Sensory receptors detect touch, pressure, and temperature."],
 ],
 Injuries:[
  ["Ankle joint",232,179,75,58,"The ankle joint is where the leg bones meet the foot bones."],
  ["Ligament",253,193,45,28,"Ligaments connect bone to bone and stabilize a joint."],
  ["Tendon",210,110,15,45,"Tendons connect muscle to bone to allow movement."],
  ["Tibia",200,100,18,55,"The tibia is the larger shin bone of the lower leg."],
  ["Fibula",215,130,10,50,"The fibula is the thinner bone alongside the tibia."],
  ["Swollen tissue",255,215,35,22,"Swelling occurs when fluid builds up around an injured area."],
  ["Bruised area",245,230,24,16,"A bruise forms when small blood vessels leak under the skin."],
  ["Cartilage",258,175,25,12,"Cartilage cushions the ends of bones inside a joint."],
 ],
};

const conceptQuestionStems = [
 (topic, clue) => `Which ${topic.toLowerCase()} structure best matches this description: ${clue}`,
 (topic, clue) => `Which answer correctly matches this function or feature: ${clue}`,
 (topic, clue) => `A student is reviewing the ${topic.toLowerCase()} system. Which structure is most directly connected to this fact: ${clue}`,
 (topic, clue) => `Which structure would be most affected if the body could no longer perform this role: ${clue}`,
 (topic, clue) => `Which anatomical term belongs with the following description: ${clue}`,
 (topic, clue) => `During an anatomy review, which structure should be paired with this statement: ${clue}`
];

function cleanStructureClue(name, fact){
 let clue=String(fact).trim();
 const prefixes=[`The ${name} is `,`The ${name} are `,`${name} is `,`${name} are `];
 for(const prefix of prefixes){
  if(clue.toLowerCase().startsWith(prefix.toLowerCase())){
   clue=clue.slice(prefix.length);
   break;
  }
 }
 clue=clue.charAt(0).toLowerCase()+clue.slice(1);
 clue=clue.replace(/[.]$/,'');
 return clue;
}

function buildConceptPictureBank(){
 const bank={};
 Object.keys(structureBank).forEach(topic=>{
  const structs=structureBank[topic];
  const names=structs.map(s=>s[0]);
  const items=[];
  const seen=new Set();

  function sameTopicDistractors(correct, offset){
   const pool=names.filter(n=>n!==correct);
   const picked=[];
   for(let i=0;i<pool.length && picked.length<3;i++){
    const candidate=pool[(i+offset)%pool.length];
    if(!picked.includes(candidate)) picked.push(candidate);
   }
   return picked;
  }

  let round=0;
  while(items.length<50 && round<conceptQuestionStems.length*5){
   const stem=conceptQuestionStems[round % conceptQuestionStems.length];
   structs.forEach((entry,index)=>{
    if(items.length>=50) return;
    const [name,,, ,fact]=entry;
    const clue=cleanStructureClue(name,fact);
    const question=stem(topic,clue)+"?";
    const key=question.toLowerCase();
    if(seen.has(key)) return;
    seen.add(key);
    const choices=shuffleChoices([name,...sameTopicDistractors(name,index+round)]);
    items.push([
      question,
      name,
      choices,
      fact,
      `conceptpicture|${topic}|${name}|${round}|${index}`,
      detailedPictureSvg(topic)
    ]);
   });
   round++;
  }
  bank[topic]=items;
 });
 return bank;
}
const detailedPictureBank = buildConceptPictureBank();

function addDetailedPictureQuestions(){
 Object.keys(detailedPictureBank).forEach(topic=>{
  ['easy','normal','difficult'].forEach(level=>{
   detailedPictureBank[topic].forEach((item,i)=>{
    const copy=[...item];
    copy[4]=`${item[4]}|${level}|${i}`;
    data[topic].qs[level].push(copy);
   });
  });
 });
}
addDetailedPictureQuestions();

function expandQuestionBank(){
 Object.keys(data).forEach(topic=>{
   ["easy","normal","difficult"].forEach(level=>{
     const existing=data[topic].qs[level] || [];
     const concepts=conceptBank[topic] || [];
     const built=[];
     let i=0;
     while(existing.length + built.length < QUESTION_GOAL_PER_TOPIC_LEVEL && concepts.length){
       const concept=concepts[i % concepts.length];
       const templateIndex=Math.floor(i / concepts.length) % questionTemplates.length;
       built.push(buildQuestionFromConcept(concept,topic,level,templateIndex));
       i++;
     }
     const seen=new Set();
     data[topic].qs[level]=existing.concat(built).filter(q=>{
       const key=(q[4] || (q[0]+"|"+q[1])).toLowerCase();
       if(seen.has(key)) return false;
       seen.add(key);
       return true;
     });
   });
 });
}
expandQuestionBank();

function getQuestionStyleLabel(){
 if(questionStyle==="regular") return "regular questions only";
 if(questionStyle==="picture") return "image questions only";
 return "mixed regular + picture questions";
}
function questionMemoryKey(topic, level){ return topic+"|"+level+"|"+questionStyle; }
function getQuestionId(arr){ return String(arr[4] || (arr[0]+"|"+arr[1])).toLowerCase(); }
function getConceptId(arr){
 if(arr[4]) return String(arr[4]).split("|").slice(0,3).join("|").toLowerCase();
 return String(arr[1]).toLowerCase();
}
function drawFreshQuestions(topic, level, count=ROUND_SIZE){
 let bank=[...(data[topic].qs[level]||[]), ...((extraQuestions[topic]&&extraQuestions[topic][level])||[])];
 const pictureBank=bank.filter(q=>q[5]);
 const regularBank=bank.filter(q=>!q[5]);
 if(questionStyle==="regular"){
   bank=regularBank;
 }else if(questionStyle==="picture"){
   // Anatomy-reference mode uses only the concept-based questions paired with the topic image.
   bank=pictureBank;
 }
 const memoryKey=questionMemoryKey(topic,level);
 if(!usedQuestionMemory[memoryKey]) usedQuestionMemory[memoryKey]=new Set();
 let used=usedQuestionMemory[memoryKey];
 let available=bank.filter(q=>!used.has(getQuestionId(q)));
 if(available.length<count){
   usedQuestionMemory[memoryKey]=new Set();
   used=usedQuestionMemory[memoryKey];
   available=[...bank];
 }
 if(questionStyle==="picture"){
   const pics=available.filter(q=>q[5]).sort(()=>Math.random()-0.5);
   const regs=available.filter(q=>!q[5]).sort(()=>Math.random()-0.5);
   available=pics.concat(regs);
 }else{
   available.sort(()=>Math.random()-0.5);
 }
 const chosen=[], roundConcepts=new Set(), roundAnswers=new Set();
 for(const q of available){
   const concept=getConceptId(q), ans=String(q[1]).toLowerCase();
   if(roundConcepts.has(concept) || roundAnswers.has(ans)) continue;
   chosen.push(q); roundConcepts.add(concept); roundAnswers.add(ans); used.add(getQuestionId(q));
   if(chosen.length===count) break;
 }
 for(const q of available){
   if(chosen.length===count) break;
   if(chosen.includes(q)) continue;
   chosen.push(q); used.add(getQuestionId(q));
 }
 return chosen.slice(0,count).map(toQ);
}


const heartQuizImage = `<div class="anatomy-img-wrap"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS7IDa3A1qbG-KUeLClW5Fi6HT_GB_gYS1HzyTNZ5pL-xsL6iazoS8SRyc&s=10" class="anatomy-image" alt="Detailed cross-section of the human heart"></div>`;
const circulatoryHeartQuiz = [
 {q:"How many chambers are in the human heart?",a:"C) Four",c:["A) Two","B) Three","C) Four","D) Five"],why:"The heart has two atria and two ventricles, which help separate oxygenated and deoxygenated blood.",img:heartQuizImage},
 {q:"Which chamber of the heart is responsible for pumping oxygenated blood to the entire body?",a:"D) Left ventricle",c:["A) Right atrium","B) Right ventricle","C) Left atrium","D) Left ventricle"],why:"The left ventricle has the thickest muscular wall because it must create enough pressure to send blood through systemic circulation.",img:heartQuizImage},
 {q:"What is the name of the heart's natural pacemaker, which initiates the electrical signal that makes it beat?",a:"B) SA node",c:["A) AV node","B) SA node","C) Purkinje fibers","D) Bundle of His"],why:"The sinoatrial, or SA, node normally begins the electrical signal for each heartbeat.",img:heartQuizImage},
 {q:"What is the primary purpose of the heart's valves, such as the tricuspid and mitral valves?",a:"B) To prevent the backflow of blood",c:["A) To carry oxygen to the heart muscle","B) To prevent the backflow of blood","C) To separate the left and right sides of the heart","D) To filter out waste products from the blood"],why:"Heart valves keep blood moving in one direction by preventing backflow.",img:heartQuizImage},
 {q:"Which blood vessels supply the heart muscle itself with oxygen and nutrients?",a:"B) Coronary arteries",c:["A) Pulmonary arteries","B) Coronary arteries","C) Carotid arteries","D) Aorta"],why:"The coronary arteries deliver oxygen-rich blood and nutrients directly to the heart muscle.",img:heartQuizImage},
 {q:"Which of the following is the correct path that blood takes as it leaves the heart to go to the lungs?",a:"B) Right ventricle → Pulmonary artery → Lungs",c:["A) Left ventricle → Aorta → Body","B) Right ventricle → Pulmonary artery → Lungs","C) Right atrium → Vena cava → Lungs","D) Left atrium → Pulmonary vein → Lungs"],why:"Deoxygenated blood leaves the right ventricle through the pulmonary artery and travels to the lungs.",img:heartQuizImage}
];

const cases = [
 {case:"A student twists their ankle during basketball. It swells around the joint and hurts to walk.", q:"Most likely injury?", a:"Sprain", c:["Sprain","Concussion","Asthma"], why:"Sprains affect ligaments around joints."},
 {case:"A soccer player gets hit in the head, then feels dizzy and confused.", q:"What injury should be suspected?", a:"Concussion", c:["Concussion","Strain","Fracture only"], why:"Dizziness and confusion after head impact are warning signs."},
 {case:"A runner feels a sharp pull in the back of the thigh after sprinting.", q:"Most likely injury?", a:"Strain", c:["Strain","Sprain","Dislocation"], why:"Strains involve muscles or tendons."},
 {case:"After a fall, someone has strong forearm pain and cannot use the arm normally.", q:"What injury is possible?", a:"Fracture", c:["Fracture","Sprain only","Hormone imbalance"], why:"Severe pain and loss of function after impact can suggest a broken bone."},
 {case:"Someone has trouble breathing during intense exercise and is wheezing.", q:"Which system is most involved?", a:"Respiratory system", c:["Respiratory system","Skeletal system","Urinary system"], why:"Wheezing and breathing trouble relate to air movement."},
 {case:"A person feels shaky and weak after not eating for a long time.", q:"Which physiology topic is most related?", a:"Blood glucose regulation", c:["Blood glucose regulation","Joint cartilage","Alveoli shape"], why:"Blood sugar is regulated by hormones like insulin and glucagon."}
];

const finalExam = [
 ["Ligaments connect...","Bone to bone",["Bone to bone","Muscle to bone","Air to blood"],"Ligaments stabilize joints."],
 ["Tendons connect...","Muscle to bone",["Muscle to bone","Bone to bone","Brain to stomach"],"Tendons transmit muscle force to bones."],
 ["Alveoli are found in the...","Lungs",["Lungs","Bones","Heart"],"Alveoli are tiny air sacs for gas exchange."],
 ["Cardiac output means...","Blood pumped per minute",["Blood pumped per minute","Air in lungs","Calcium in bones"],"Cardiac output equals heart rate times stroke volume."],
 ["The brain and spinal cord are the...","Central nervous system",["Central nervous system","Respiratory system","Skeletal system"],"The CNS is the main control center."],
 ["Small intestine is important for...","Nutrient absorption",["Nutrient absorption","Breathing","Making thoughts"],"Villi increase absorption."],
 ["A concussion involves the...","Brain",["Brain","Toenail","Stomach acid"],"Concussions are brain injuries."],
 ["Hormones are made by glands in the...","Endocrine system",["Endocrine system","Skeletal system","Urinary system"],"Endocrine glands secrete hormones."],
 ["Kidneys help filter...","Blood",["Blood","Air","Sound"],"Kidneys remove wastes and regulate fluid balance."],
 ["Skin helps protect and control...","Temperature",["Temperature","Bone color","Memory"],"Skin helps barrier protection and thermoregulation."]
];

let score=0, hearts=7, mastered={}, cards=[], current=null, examMode=false, examIndex=0, correctExam=0, difficulty="easy", learner="student", missed=[], topicQueue=[], topicIndex=0, topicCorrect=0;
let xp=0, level=1, streak=1, chests=0, dailyCorrect=0, bossMode=false, currentQuestionType="multiple", questionStyle="mixed";
let deferAnswers=false, deferredResults=[];

function closeTutorial(){
 document.getElementById("tutorial").style.display="none";
}

function explainFor(text){
 if(difficulty==="easy"){
   return text
    .replace("homeostasis","body balance")
    .replace("concentration gradient","where there is more or less stuff")
    .replace("cardiac output","how much blood the heart pumps")
    .replace("ventilation","breathing air in and out")
    .replace("electrolyte","salt/mineral")
    .replace("electrolytes","salts/minerals")
    .replace("diffuses","moves")
    .replace("diffusion","movement")
    + " This is the easier version, so it keeps the idea simple.";
 }
 if(difficulty==="difficult"){
   return text + " This level may ask you to connect body structures, functions, and injury clues.";
 }
 return text;
}

function getQ(topic){
 return drawFreshQuestions(topic,difficulty,1)[0];
}
function toQ(arr){return {q:arr[0],a:arr[1],c:arr[2],why:arr[3],img:arr[5]||""};}
function setDifficulty(){
 difficulty=document.getElementById("difficulty").value;
 document.getElementById("speech").textContent="Difficulty changed to: "+difficulty+".";
 log("Difficulty set to "+difficulty+".");
}

function setQuestionStyle(){
 questionStyle=document.getElementById("questionStyle").value;
 const label = questionStyle==="regular" ? "regular questions only" : questionStyle==="picture" ? "image questions only" : "mixed regular + picture questions";
 document.getElementById("speech").textContent="Question style changed to: "+label+".";
 log("Question style set to "+label+".");
}

function visit(topic){
 current=topic; examMode=false;
 deferAnswers = topic === "Circulatory";
 deferredResults = [];
 document.getElementById("explain").style.display="none";
 const d=data[topic];
 document.getElementById("player").style.left=d.pos[0]+"%";
 document.getElementById("player").style.top=d.pos[1]+"%";
 document.getElementById("speech").textContent = deferAnswers
   ? "Welcome to Circulatory! Study the heart image and answer all 6 questions. Answers will appear only at the end."
   : `Welcome to ${topic}! Answer 10 fresh questions. Question style: ${getQuestionStyleLabel()}.`;
 document.getElementById("questTitle").textContent=d.emoji+" "+topic+" Quest";
 document.getElementById("objective").textContent = deferAnswers
   ? "Mission: answer all 6 heart questions. Your choices are locked in, and the answer key appears after the final question."
   : `Mission: master ${topic}. Get 7/10 correct to collect the ${d.card} card. Style: ${getQuestionStyleLabel()}.`;
 document.getElementById("lesson").textContent=explainFor(d.lesson[difficulty]);
 topicQueue = deferAnswers ? circulatoryHeartQuiz.map(q=>({...q,c:[...q.c]})) : drawFreshQuestions(topic,difficulty,ROUND_SIZE);
 topicIndex=0;
 topicCorrect=0;
 askTopicQuestion();
 log("Studying "+topic+" at "+difficulty+" level with "+getQuestionStyleLabel()+".");
}

function askTopicQuestion(){
 if(!current || topicIndex>=topicQueue.length){return;}
 document.getElementById("lesson").textContent=explainFor(data[current].lesson[difficulty]) + `  Question ${topicIndex+1}/${topicQueue.length}`;
 ask(topicQueue[topicIndex]);
}

function openPictureZoom(imgHTML){
 document.getElementById("modalContent").innerHTML='<div class="zoom-picture">'+imgHTML+'</div><p class="picture-caption">Anatomy reference. Click outside this window when finished.</p>';
 document.getElementById("modal").style.display="grid";
}

function ask(q){
 const choices=document.getElementById("choices");
 choices.innerHTML="";
 const oldPic=document.getElementById("pictureQuestion");
 if(oldPic) oldPic.remove();
 document.getElementById("explain").style.display="none";
 if(q.img){
   const pic=document.createElement("div");
   pic.id="pictureQuestion";
   pic.className="picture-card";
   pic.innerHTML=q.img+'<div class="picture-caption">Anatomy reference. Click to zoom in.</div>';
   pic.onclick=()=>openPictureZoom(q.img);
   document.getElementById("question").insertAdjacentElement("beforebegin", pic);
 }
 currentQuestionType = pickQuestionType(q);
 if(currentQuestionType==="truefalse"){
   const statement = Math.random()>.5 ? `${q.a} is the correct answer for: ${q.q}` : `${q.c.find(x=>x!==q.a)} is the correct answer for: ${q.q}`;
   document.getElementById("question").textContent="True or False: "+statement;
   ["True","False"].forEach(choice=>{
     const b=document.createElement("button"); b.className="secondary"; b.textContent=choice;
     const isTrue=statement.startsWith(q.a+" is");
     b.onclick=()=>answer((choice==="True")===isTrue ? q.a : "__wrong__",q,b);
     choices.appendChild(b);
   });
   return;
 }
 if(currentQuestionType==="fill"){
   document.getElementById("question").textContent=q.q+"  Type the answer:";
   choices.innerHTML=`<input id="fillInput" style="width:100%;padding:12px;border-radius:14px;border:2px solid var(--pink2);font-weight:bold" placeholder="Type your answer here"><button class="main" id="submitFill">Check Answer</button>`;
   document.getElementById("submitFill").onclick=()=>{
     const val=document.getElementById("fillInput").value.trim().toLowerCase();
     answer(val===q.a.toLowerCase()?q.a:val,q,document.getElementById("submitFill"));
   };
   return;
 }
 document.getElementById("question").textContent=q.q;
 q.c.forEach(choice=>{
   const b=document.createElement("button");
   b.className="secondary";
   b.textContent=choice;
   b.onclick=()=>answer(choice,q,b);
   choices.appendChild(b);
 });
}
function pickQuestionType(q){
 if(q.img || examMode || bossMode) return "multiple";
 const roll=Math.random();
 if(roll<.18) return "truefalse";
 if(roll<.32 && q.a.length<28) return "fill";
 return "multiple";
}

function answer(choice, q, btn){
 [...document.querySelectorAll(".secondary")].forEach(b=>b.disabled=true);
 const exp=document.getElementById("explain");
 if(deferAnswers && current==="Circulatory" && !examMode && !bossMode){
   const correct = choice===q.a;
   deferredResults.push({q:q.q, chosen:choice, answer:q.a, why:q.why, correct});
   if(correct){
     const gained = difficulty==="easy" ? 10 : difficulty==="normal" ? 15 : 20;
     score += gained; xp += gained; dailyCorrect++; topicCorrect++; checkRewards();
   }else{
     hearts--; missed.push(q);
   }
   exp.style.display="block";
   exp.innerHTML="<b>Answer locked in.</b> The correct answer will be shown after the final question.";
   document.getElementById("speech").textContent=`Answer ${topicIndex+1} saved. Keep going to see the answer key at the end.`;
   update();
   setTimeout(nextTopicQuestion,700);
   return;
 }
 exp.style.display="block";
 if(choice===q.a){
   btn.classList.add("correct");
   const gained = difficulty==="easy" ? 10 : difficulty==="normal" ? 15 : 20;
   score += gained; xp += gained; dailyCorrect++; checkRewards();
   exp.innerHTML="<b>Why:</b> "+explainFor(q.why);
   sparkle("✨");
   if(examMode){ correctExam++; setTimeout(nextExam,900); }
   else {
     topicCorrect++;
     setTimeout(nextTopicQuestion,900);
   }
 }else{
   btn.classList.add("wrong");
   hearts--;
   missed.push(q);
   exp.innerHTML=`<b>Correct answer:</b> ${q.a}<br><b>Why:</b> ${explainFor(q.why)}`;
   document.getElementById("speech").textContent="Missed question saved for review.";
   log("Missed: "+q.q);
   if(examMode) setTimeout(nextExam,1100);
   else setTimeout(nextTopicQuestion,1100);
 }
 update();
 if(hearts<=0){
   document.getElementById("speech").textContent="Out of hearts. Restart and try again.";
   document.getElementById("choices").innerHTML='<button class="main" onclick="restart()">Restart</button>';
 }
}

function nextTopicQuestion(){
 topicIndex++;
 if(topicIndex < topicQueue.length){
   askTopicQuestion();
 }else{
   if(bossMode){
     const won=topicCorrect>=4;
     document.getElementById("question").textContent=won?`Boss defeated: ${topicCorrect}/5 correct!`:`Boss escaped: ${topicCorrect}/5 correct.`;
     document.getElementById("lesson").textContent=won?"You won bonus XP and a boss badge.":"Practice this topic, then try the boss again.";
     document.getElementById("choices").innerHTML='<button class="main" onclick="startBossBattle()">Try Another Boss</button><button class="main" onclick="visit(current)">Practice Topic</button>';
     if(won){score+=75; xp+=75; document.getElementById("badges").innerHTML += `<span class="badge">👾 ${current} Boss</span>`; sparkle("👾");}
     bossMode=false; update(); return;
   }
   const oldPic=document.getElementById("pictureQuestion");
   if(oldPic) oldPic.remove();
   if(deferAnswers && current==="Circulatory"){
     const answerKey=deferredResults.map((r,i)=>`<div class="lesson"><b>${i+1}. ${r.q}</b><br>Your answer: ${r.chosen || "No answer"}<br><b>Correct answer: ${r.answer}</b><br>${r.why}</div>`).join("");
     document.getElementById("lesson").innerHTML=`<b>Heart Quiz Complete: ${topicCorrect}/${topicQueue.length} correct</b><br>The answers were hidden until now.`;
     document.getElementById("question").textContent="Answer Key";
     document.getElementById("choices").innerHTML=answerKey+`<button class="main" onclick="visit('Circulatory')">Try the Heart Quiz Again</button><button class="main" onclick="randomQuestion()">Try Another Topic</button>`;
     document.getElementById("explain").style.display="none";
     document.getElementById("speech").textContent="Heart quiz finished. The full answer key is now shown.";
     if(topicCorrect >= 4) masterTopic(current);
     deferAnswers=false;
     return;
   }
   if(topicCorrect >= 7){
     masterTopic(current);
     document.getElementById("choices").innerHTML='<button class="main" onclick="visit(current)">Practice This Topic Again</button><button class="main" onclick="randomQuestion()">Try Random Topic</button>';
     document.getElementById("question").textContent=`Quest complete: ${topicCorrect}/10 correct.`;
   }else{
     document.getElementById("speech").textContent="Quest finished, but try again to earn the card.";
     document.getElementById("question").textContent=`Quest complete: ${topicCorrect}/10 correct. Get 7/10 to master it.`;
     document.getElementById("choices").innerHTML='<button class="main" onclick="visit(current)">Retry This Topic</button><button class="main" onclick="reviewWeak()">Review Missed</button>';
   }
   document.getElementById("explain").style.display="none";
 }
}

function masterTopic(topic){
 if(!topic) return;
 if(!mastered[topic]){
   mastered[topic]=true;
   cards.push(data[topic].emoji+" "+data[topic].card);
   xp+=50; checkRewards();
   document.getElementById("speech").textContent="Correct! You earned a study card.";
   document.getElementById("badges").innerHTML += `<span class="badge">${data[topic].emoji} ${topic}</span>`;
   log("Mastered "+topic+".");
 }else{
   document.getElementById("speech").textContent="Correct! Extra practice points earned.";
 }
 update();
}

function randomQuestion(){
 const topics=Object.keys(data);
 visit(topics[Math.floor(Math.random()*topics.length)]);
}

function reviewWeak(){
 if(missed.length===0){
   document.getElementById("speech").textContent="No missed questions yet. Nice!";
   return;
 }
 current=null; examMode=false;
 document.getElementById("questTitle").textContent="🔁 Review Missed Questions";
 document.getElementById("lesson").textContent="This mode repeats questions you missed so you can fix weak spots.";
 ask(missed.shift());
 log("Started review mode.");
}

function startCase(){
 examMode=false; current="Injuries";
 const c=cases[Math.floor(Math.random()*cases.length)];
 document.getElementById("questTitle").textContent="🩹 Clinical Case Mission";
 document.getElementById("lesson").innerHTML=`<div class="casebox"><b>Case:</b> ${c.case}</div>`;
 ask({q:c.q,a:c.a,c:c.c,why:c.why});
 log("Opened a case mission.");
}

function startFinalExam(){
 examMode=true; examIndex=0; correctExam=0; current=null;
 document.getElementById("questTitle").textContent="🏥 Final A&P Exam";
 document.getElementById("lesson").textContent="Answer 10 mixed questions. Goal: 8/10.";
 document.getElementById("speech").textContent="Final exam started!";
 ask(toQ(finalExam[0]));
}

function nextExam(){
 examIndex++;
 if(examIndex>=finalExam.length){
   const passed=correctExam>=8;
   document.getElementById("question").textContent= passed ? "You passed the final exam!" : "Exam complete. Keep practicing!";
   document.getElementById("lesson").textContent=`Score: ${correctExam}/${finalExam.length}. ${passed ? "You earned the A&P Scholar Badge." : "Try again for 8/10 or higher."}`;
   document.getElementById("choices").innerHTML='<button class="main" onclick="startFinalExam()">Retry Exam</button>';
   document.getElementById("explain").style.display="none";
   if(passed){
     score+=100;
     document.getElementById("badges").innerHTML += '<span class="badge">🏆 A&P Scholar</span>';
     sparkle("🏆");
   }
   update();
 }else{
   document.getElementById("lesson").textContent=`Final Exam Question ${examIndex+1}/10`;
   ask(toQ(finalExam[examIndex]));
 }
}

function startFlashcards(){
 const all=[];
 Object.keys(data).forEach(t=>{
   all.push({front:t+" — "+difficulty+" lesson", back:explainFor(data[t].lesson[difficulty])});
   data[t].qs[difficulty].forEach(q=>all.push({front:q[0], back:q[1]+" — "+explainFor(q[3])}));
 });
 let i=0;
 document.getElementById("modal").style.display="grid";
 const content=document.getElementById("modalContent");
 function render(showBack=false){
   content.innerHTML=`
     <h2>📚 Flashcards</h2>
     <div class="flash">${showBack ? all[i].back : all[i].front}</div>
     <button class="main" id="flip">Flip</button>
     <button class="main" id="next">Next</button>
     <p>${i+1}/${all.length}</p>
   `;
   document.getElementById("flip").onclick=()=>render(!showBack);
   document.getElementById("next").onclick=()=>{i=(i+1)%all.length;render(false)};
 }
 render(false);
}

function startMatchGame(){
 const pairs=[
  ["Ligament","Connects bone to bone"],["Tendon","Connects muscle to bone"],
  ["Alveoli","Tiny air sacs"],["Neuron","Nerve cell"],["Fracture","Broken or cracked bone"],
  ["Sprain","Ligament injury"],["Strain","Muscle or tendon injury"],["Nephron","Kidney functional unit"],
  ["Insulin","Lowers blood glucose"],["ATP","Cell energy molecule"]
 ];
 let i=0, points=0;
 document.getElementById("modal").style.display="grid";
 const content=document.getElementById("modalContent");
 function round(){
   const correct=pairs[i], opts=[correct[1]];
   while(opts.length<3){
     const r=pairs[Math.floor(Math.random()*pairs.length)][1];
     if(!opts.includes(r)) opts.push(r);
   }
   opts.sort(()=>Math.random()-0.5);
   content.innerHTML=`<h2>🧩 Match Vocab</h2><p><b>${correct[0]}</b> means...</p>
   ${opts.map(o=>`<button class="secondary match">${o}</button>`).join("")}
   <p>Round ${i+1}/${pairs.length} | Points: ${points}</p>`;
   [...document.querySelectorAll(".match")].forEach(b=>{
     b.onclick=()=>{
       if(b.textContent===correct[1]){points++; score+=5; b.classList.add("correct");}
       else{hearts--; b.classList.add("wrong");}
       update();
       setTimeout(()=>{i++; if(i<pairs.length) round(); else done();},550);
     }
   });
 }
 function done(){
   content.innerHTML=`<h2>Match Game Complete</h2><p>You got ${points}/${pairs.length}.</p><button class="main" onclick="startMatchGame()">Play Again</button>`;
   if(points>=8){document.getElementById("badges").innerHTML += '<span class="badge">🧩 Vocab Pro</span>';}
 }
 round();
}


function startBossBattle(){
 const available=Object.keys(data).filter(t=>mastered[t]);
 const topic=available.length?available[Math.floor(Math.random()*available.length)]:Object.keys(data)[Math.floor(Math.random()*Object.keys(data).length)];
 bossMode=true; examMode=false; current=topic;
 document.getElementById("questTitle").textContent="👾 Boss Battle: "+topic;
 document.getElementById("lesson").innerHTML=`<div class="boss-title">Defeat the ${data[topic].emoji} ${topic} Boss</div><div class="tipbox">Boss rule: answer 5 questions. Get 4 correct to win bonus XP and a badge.</div>`;
 document.getElementById("objective").textContent="Boss Battle: use what you learned, not just memorizing.";
 topicQueue=drawFreshQuestions(topic,difficulty,5); topicIndex=0; topicCorrect=0;
 ask(topicQueue[topicIndex]);
 log("Started a boss battle for "+topic+".");
}

function openBodyDex(){
 document.getElementById("modal").style.display="grid";
 const owned=new Set(cards.map(c=>c.replace(/^\S+\s/,'')));
 document.getElementById("modalContent").innerHTML=`<h2>🃏 Organ Dex</h2><p>Collect cards by mastering topics. Each card is a tiny study sheet.</p>`+
 Object.keys(data).map(t=>`<div class="lesson"><b>${data[t].emoji} ${data[t].card}</b><br><b>Topic:</b> ${t}<br><b>Status:</b> ${mastered[t]?"Unlocked ✅":"Locked 🔒"}<br><b>Study note:</b> ${data[t].lesson[difficulty]}</div>`).join("");
}

function openGuide(){
 document.getElementById("modal").style.display="grid";
 document.getElementById("modalContent").innerHTML=`
 <h2>📖 A&P Study Guide</h2><p><b>Question Bank:</b> Each topic now has 150 prepared questions per difficulty. Every round pulls 10 fresh questions and avoids repeated answers/concepts when possible.</p>
 <p><b>Cells:</b> membranes control movement; ATP = energy; homeostasis = internal balance.</p>
 <p><b>Skeletal:</b> bones support/protect; ligaments connect bone to bone; cartilage reduces friction.</p>
 <p><b>Muscular:</b> tendons connect muscle to bone; contraction needs calcium and ATP.</p>
 <p><b>Nervous:</b> CNS = brain/spinal cord; neurons signal through synapses.</p>
 <p><b>Circulatory:</b> arteries away, veins back, capillaries exchange; cardiac output = HR × stroke volume.</p>
 <p><b>Respiratory:</b> alveoli exchange gases; diaphragm drives ventilation; CO₂ affects pH.</p>
 <p><b>Digestive:</b> enzymes break food down; small intestine absorbs; liver/pancreas/gallbladder assist.</p>
 <p><b>Endocrine:</b> hormones are chemical messengers; feedback loops keep balance.</p>
 <p><b>Urinary:</b> kidneys filter blood; nephrons regulate waste, water, and electrolytes.</p>
 <p><b>Skin:</b> barrier protection, sensation, temperature control.</p>
 <p><b>Injuries:</b> sprain = ligament, strain = muscle/tendon, fracture = bone, concussion = brain. Serious injuries need adult/medical help.</p>`;
}

function closeModal(){document.getElementById("modal").style.display="none"}

function update(){
 level=Math.floor(xp/100)+1;
 document.getElementById("score").textContent=score;
 document.getElementById("hearts").textContent=hearts;
 document.getElementById("xp").textContent=xp;
 document.getElementById("level").textContent=level;
 document.getElementById("streak").textContent=streak;
 document.getElementById("chests").textContent=chests;
 document.getElementById("xpfill").style.width=(xp%100)+"%";
 const m=Math.round(Object.keys(mastered).length/11*100);
 document.getElementById("mastery").textContent=m;
 document.getElementById("fill").style.width=m+"%";
 document.getElementById("rank").textContent=level<5?"Rookie":level<12?"Anatomy Apprentice":level<20?"Resident":"Medical Master";
 document.getElementById("cards").innerHTML=cards.map((c,i)=>`<span class="cardbit ${i%4===0?'rare':''}">${c}</span>`).join("");
 updateWorlds(m);
}
function updateWorlds(m){
 const worlds=[...document.querySelectorAll('.world')];
 worlds.forEach((w,i)=>w.classList.toggle('active', i<=Math.floor(m/25)));
}
function checkRewards(){
 if(dailyCorrect>0 && dailyCorrect%5===0){
   chests++; hearts=Math.min(10,hearts+1); xp+=25;
   document.getElementById("dailyQuest").textContent="Mystery Chest opened! +25 XP and +1 heart. Next chest in 5 correct answers.";
   sparkle("🎁"); log("Opened a mystery chest.");
 }
 if(xp>0 && xp%100<20){ document.getElementById("objective").textContent="Level up progress: keep answering to unlock higher medical ranks."; }
}

function log(msg){
 const div=document.createElement("div");
 div.textContent="• "+msg;
 document.getElementById("log").prepend(div);
}

function sparkle(symbol){
 const map=document.getElementById("map");
 for(let i=0;i<8;i++){
   const s=document.createElement("div");
   s.className="spark";
   s.textContent=symbol;
   s.style.left=(42+Math.random()*15)+"%";
   s.style.top=(40+Math.random()*15)+"%";
   map.appendChild(s);
   setTimeout(()=>s.remove(),850);
 }
}

function restart(){
 score=0; hearts=7; mastered={}; cards=[]; current=null; examMode=false; examIndex=0; correctExam=0; missed=[]; topicQueue=[]; topicIndex=0; topicCorrect=0; xp=0; level=1; streak=1; chests=0; dailyCorrect=0; bossMode=false;
 document.getElementById("player").style.left="45%";
 document.getElementById("player").style.top="44%";
 document.getElementById("speech").textContent="Pick a body system. Each topic has a large no-repeat question bank.";
 document.getElementById("questTitle").textContent="Quest";
 document.getElementById("lesson").textContent="Choose a topic on the map.";
 document.getElementById("objective").textContent="Goal: pick a system, learn the mini lesson, then beat 10 questions to earn its organ card.";
 document.getElementById("dailyQuest").textContent="Daily Quest: Get 5 correct answers to open a mystery chest.";
 document.getElementById("question").textContent="Question will appear here.";
 document.getElementById("choices").innerHTML="";
 document.getElementById("explain").style.display="none";
 document.getElementById("badges").innerHTML='<span class="badge">🌱 Study Rookie</span>';
 document.getElementById("log").innerHTML="";
 update();
}
update();
</script>
</body>
</html>
