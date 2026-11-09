
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Bharat</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f1f4fb;color:#20243a;transition:.2s}
header{background:linear-gradient(120deg,#4936c9,#087bdc);color:white;padding:22px 16px;border-radius:0 0 25px 25px}
header h1{margin:0;font-size:27px}
header p{margin:7px 0 0}
.top{display:flex;justify-content:space-between;align-items:center;gap:10px}
select,input,textarea,button{font:inherit;padding:11px;border-radius:10px;border:1px solid #ccd2e2}
button{background:#5142cf;color:white;border:0;cursor:pointer;margin:4px}
button:active{opacity:.7}
main{padding:15px;max-width:700px;margin:auto}
.card{background:white;padding:16px;margin:12px 0;border-radius:16px;box-shadow:0 3px 12px #0000000c}
h2{font-size:19px;margin-top:4px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.tile{background:#fff;padding:17px 10px;border-radius:15px;text-align:center;box-shadow:0 2px 9px #0000000c;cursor:pointer}
.tile b{display:block;margin-top:7px}
input,textarea{width:100%;margin:5px 0;background:transparent;color:inherit}
textarea{min-height:90px}
.item{padding:10px;background:#f0f2fa;border-radius:9px;margin:7px 0;display:flex;justify-content:space-between;gap:8px;align-items:center}
.item button{padding:6px 9px}
.page{display:none}
.page.active{display:block}
.small{font-size:13px;color:#777}
.points{font-size:25px;font-weight:bold;color:#ff9b00}
nav{display:flex;gap:5px;overflow:auto;padding:8px 0}
nav button{white-space:nowrap}
.option{display:block;width:100%;text-align:left;background:#eef0ff;color:#25254a;margin:8px 0}
.option:disabled{opacity:.75}
#result{font-weight:bold;margin:12px 0}
body.dark{background:#171a27;color:#f4f4f8}
body.dark .card,body.dark .tile{background:#252a3b;color:#f4f4f8}
body.dark .item,body.dark .option{background:#343b52;color:white}
body.dark .small{color:#bbb}
</style>
</head>
<body>

<header>
 <div class="top">
  <div><h1>🇮🇳 Smart Bharat</h1><p id="tagline">Your smart digital companion</p></div>
  <select id="language" onchange="changeLanguage()" style="width:105px">
   <option value="mr">मराठी</option>
   <option value="hi">हिंदी</option>
   <option value="en">English</option>
  </select>
 </div>
</header>

<main>
<nav>
 <button onclick="showPage('home')" id="navHome">Home</button>
 <button onclick="showPage('profile')" id="navProfile">Profile</button>
 <button onclick="toggleDark()" id="darkBtn">🌙 Dark</button>
</nav>

<section id="home" class="page active">
 <div class="card">
  <h2 id="welcome">नमस्कार!</h2>
  <p id="homeText">Smart Bharat मध्ये तुमचे स्वागत आहे.</p>
  <div class="points">⭐ <span id="points">0</span> <span id="pointLabel">Points</span></div>
  <button onclick="claimDaily()" id="dailyBtn">🎁 Daily Points मिळवा</button>
  <p class="small" id="dailyStatus"></p>
 </div>

 <h2 id="toolsTitle">तुमची Tools</h2>
 <div class="grid">
  <div class="tile" onclick="showPage('calculator')">🧮<b id="tileCalc">Calculator</b></div>
  <div class="tile" onclick="showPage('tasks')">✅<b id="tileTasks">To-Do List</b></div>
  <div class="tile" onclick="showPage('notes')">📝<b id="tileNotes">Notes</b></div>
  <div class="tile" onclick="showPage('quiz')">🎮<b id="tileQuiz">Quiz Game</b></div>
  <div class="tile" onclick="showPage('study')">📚<b id="tileStudy">Study</b></div>
  <div class="tile" onclick="showPage('profile')">👤<b id="tileProfile">Profile</b></div>
 </div>
</section>

<section id="profile" class="page">
 <div class="card">
  <h2 id="profileTitle">👤 Profile</h2>
  <label id="nameLabel">Your name</label>
  <input id="userName" placeholder="Enter your name">
  <button onclick="saveProfile()" id="saveProfileBtn">Save Profile</button>
  <p id="profileMessage"></p>
  <p><span id="totalPointsLabel">Total Points:</span> <b id="profilePoints">0</b> ⭐</p>
 </div>
</section>

<section id="calculator" class="page">
 <div class="card">
  <h2 id="calcTitle">🧮 Calculator</h2>
  <input type="number" id="num1" placeholder="First number">
  <select id="operation">
   <option value="+">+</option><option value="-">−</option>
   <option value="*">×</option><option value="/">÷</option>
  </select>
  <input type="number" id="num2" placeholder="Second number">
  <button onclick="calculate()" id="calcBtn">Calculate</button>
  <h3 id="answer"></h3>
 </div>
</section>

<section id="tasks" class="page">
 <div class="card">
  <h2 id="tasksTitle">✅ To-Do List</h2>
  <input id="taskInput" placeholder="Write a task">
  <button onclick="addTask()" id="addTaskBtn">Add Task</button>
  <div id="taskList"></div>
 </div>
</section>

<section id="notes" class="page">
 <div class="card">
  <h2 id="notesTitle">📝 My Notes</h2>
  <input id="noteTitle" placeholder="Note title">
  <textarea id="noteBody" placeholder="Write your note here..."></textarea>
  <button onclick="saveNote()" id="saveNoteBtn">Save Note</button>
  <div id="notesList"></div>
 </div>
</section>

<section id="quiz" class="page">
 <div class="card">
  <h2 id="quizTitle">🎮 Quiz Game</h2>
  <label id="categoryLabel">Category</label>
  <select id="category">
   <option value="all">All</option>
   <option value="gk">General Knowledge</option>
   <option value="science">Science</option>
   <option value="math">Math</option>
  </select>
  <button onclick="startQuiz()" id="startQuizBtn">Start Quiz</button>
  <div id="quizArea"></div>
 </div>
</section>

<section id="study" class="page">
 <div class="card">
  <h2 id="studyTitle">📚 Study Section</h2>
  <p id="studyText">Learn something new every day!</p>
  <ul id="studyList">
   <li>Mathematics practice</li>
   <li>Science facts</li>
   <li>General Knowledge</li>
   <li>Language learning</li>
  </ul>
  <p class="small" id="studyNote">Study content can be expanded in future updates.</p>
 </div>
</section>
</main>

<script>
const translations={
mr:{
tagline:"तुमचा स्मार्ट डिजिटल साथीदार",welcome:"नमस्कार!",homeText:"Smart Bharat मध्ये तुमचे स्वागत आहे.",
pointLabel:"पॉइंट्स",dailyBtn:"🎁 आजचे पॉइंट्स मिळवा",toolsTitle:"तुमची Tools",
navHome:"होम",navProfile:"प्रोफाइल",dark:"🌙 डार्क",light:"☀️ लाईट",
tileCalc:"कॅल्क्युलेटर",tileTasks:"कामांची यादी",tileNotes:"नोट्स",tileQuiz:"क्विझ गेम",tileStudy:"अभ्यास",tileProfile:"प्रोफाइल",
profileTitle:"👤 प्रोफाइल",nameLabel:"तुमचे नाव",saveProfileBtn:"प्रोफाइल सेव्ह करा",totalPointsLabel:"एकूण पॉइंट्स:",
calcTitle:"🧮 कॅल्क्युलेटर",calcBtn:"उत्तर काढा",tasksTitle:"✅ कामांची यादी",taskPlaceholder:"काम लिहा",addTaskBtn:"काम जोडा",
notesTitle:"📝 माझ्या नोट्स",noteTitlePlaceholder:"नोटचे शीर्षक",noteBodyPlaceholder:"इथे नोट लिहा...",saveNoteBtn:"नोट सेव्ह करा",
quizTitle:"🎮 क्विझ गेम",categoryLabel:"विषय",startQuizBtn:"क्विझ सुरू करा",studyTitle:"📚 अभ्यास विभाग",
studyText:"दररोज काहीतरी नवीन शिका!",studyNote:"अभ्यासाचे साहित्य पुढील अपडेटमध्ये वाढवता येईल.",
saved:"सेव्ह झाले!",deleted:"डिलीट झाले!",correct:"बरोबर! 🎉",wrong:"चुकीचे उत्तर.",next:"पुढचा प्रश्न",finish:"क्विझ पूर्ण! गुण:",
restart:"पुन्हा खेळा",empty:"अजून काही नाही.",done:"झाले",delete:"डिलीट",dailyDone:"आजचे पॉइंट्स आधीच मिळाले!",dailySuccess:"आजचे 10 पॉइंट्स मिळाले! ⭐",
all:"सर्व विषय",gk:"सामान्य ज्ञान",science:"विज्ञान",math:"गणित",nameSaved:"प्रोफाइल सेव्ह झाले!"
},
hi:{
tagline:"आपका स्मार्ट डिजिटल साथी",welcome:"नमस्ते!",homeText:"Smart Bharat में आपका स्वागत है।",
pointLabel:"पॉइंट्स",dailyBtn:"🎁 आज के पॉइंट्स पाएं",toolsTitle:"आपके Tools",
navHome:"होम",navProfile:"प्रोफाइल",dark:"🌙 डार्क",light:"☀️ लाइट",
tileCalc:"कैलकुलेटर",tileTasks:"कामों की सूची",tileNotes:"नोट्स",tileQuiz:"क्विज गेम",tileStudy:"पढ़ाई",tileProfile:"प्रोफाइल",
profileTitle:"👤 प्रोफाइल",nameLabel:"आपका नाम",saveProfileBtn:"प्रोफाइल सेव करें",totalPointsLabel:"कुल पॉइंट्स:",
calcTitle:"🧮 कैलकुलेटर",calcBtn:"गणना करें",tasksTitle:"✅ कामों की सूची",taskPlaceholder:"काम लिखें",addTaskBtn:"काम जोड़ें",
notesTitle:"📝 मेरे नोट्स",noteTitlePlaceholder:"नोट का शीर्षक",noteBodyPlaceholder:"यहाँ नोट लिखें...",saveNoteBtn:"नोट सेव करें",
quizTitle:"🎮 क्विज गेम",categoryLabel:"विषय",startQuizBtn:"क्विज शुरू करें",studyTitle:"📚 पढ़ाई विभाग",
studyText:"हर दिन कुछ नया सीखें!",studyNote:"पढ़ाई की सामग्री अगले अपडेट में बढ़ाई जा सकती है।",
saved:"सेव हो गया!",deleted:"डिलीट हो गया!",correct:"सही जवाब! 🎉",wrong:"गलत जवाब।",next:"अगला सवाल",finish:"क्विज पूरा! स्कोर:",
restart:"फिर से खेलें",empty:"अभी कुछ नहीं है।",done:"हो गया",delete:"डिलीट",dailyDone:"आज के पॉइंट्स पहले ही मिल चुके हैं!",dailySuccess:"आज के 10 पॉइंट्स मिल गए! ⭐",
all:"सभी विषय",gk:"सामान्य ज्ञान",science:"विज्ञान",math:"गणित",nameSaved:"प्रोफाइल सेव हो गया!"
},
en:{
tagline:"Your smart digital companion",welcome:"Hello!",homeText:"Welcome to Smart Bharat.",
pointLabel:"Points",dailyBtn:"🎁 Claim Daily Points",toolsTitle:"Your Tools",
navHome:"Home",navProfile:"Profile",dark:"🌙 Dark",light:"☀️ Light",
tileCalc:"Calculator",tileTasks:"To-Do List",tileNotes:"Notes",tileQuiz:"Quiz Game",tileStudy:"Study",tileProfile:"Profile",
profileTitle:"👤 Profile",nameLabel:"Your name",saveProfileBtn:"Save Profile",totalPointsLabel:"Total Points:",
calcTitle:"🧮 Calculator",calcBtn:"Calculate",tasksTitle:"✅ To-Do List",taskPlaceholder:"Write a task",addTaskBtn:"Add Task",
notesTitle:"📝 My Notes",noteTitlePlaceholder:"Note title",noteBodyPlaceholder:"Write your note here...",saveNoteBtn:"Save Note",
quizTitle:"🎮 Quiz Game",categoryLabel:"Category",startQuizBtn:"Start Quiz",studyTitle:"📚 Study Section",
studyText:"Learn something new every day!",studyNote:"Study content can be expanded in future updates.",
saved:"Saved!",deleted:"Deleted!",correct:"Correct! 🎉",wrong:"Wrong answer.",next:"Next Question",finish:"Quiz complete! Score:",
restart:"Play Again",empty:"Nothing here yet.",done:"Done",delete:"Delete",dailyDone:"You already claimed today's points!",dailySuccess:"You got 10 points today! ⭐",
all:"All Categories",gk:"General Knowledge",science:"Science",math:"Math",nameSaved:"Profile saved!"
}
};

let lang=localStorage.getItem("smartLang")||"mr";
let points=Number(localStorage.getItem("smartPoints")||0);
let tasks=JSON.parse(localStorage.getItem("smartTasks")||"[]");
let notes=JSON.parse(localStorage.getItem("smartNotes")||"[]");
let userName=localStorage.getItem("smartName")||"";
let dark=localStorage.getItem("smartDark")==="true";

function tr(key){return translations[lang][key]||key}
function changeLanguage(){
 lang=document.getElementById("language").value;
 localStorage.setItem("smartLang",lang);
 applyLanguage();
}
function applyLanguage(){
 document.getElementById("language").value=lang;
 const ids=["tagline","welcome","homeText","pointLabel","dailyBtn","toolsTitle","navHome","navProfile","profileTitle","nameLabel","saveProfileBtn","totalPointsLabel","calcTitle","calcBtn","tasksTitle","addTaskBtn","notesTitle","saveNoteBtn","quizTitle","categoryLabel","startQuizBtn","studyTitle","studyText","studyNote"];
 ids.forEach(id=>{let el=document.getElementById(id);if(el)el.textContent=tr(id)});
 const tileIds={tileCalc:"tileCalc",tileTasks:"tileTasks",tileNotes:"tileNotes",tileQuiz:"tileQuiz",tileStudy:"tileStudy",tileProfile:"tileProfile"};
 Object.keys(tileIds).forEach(id=>document.getElementById(id).textContent=tr(id));
 document.getElementById("taskInput").placeholder=tr("taskPlaceholder");
 document.getElementById("noteTitle").placeholder=tr("noteTitlePlaceholder");
 document.getElementById("noteBody").placeholder=tr("noteBodyPlaceholder");
 document.getElementById("darkBtn").textContent=dark?tr("light"):tr("dark");
 document.querySelectorAll("#category option").forEach(o=>o.textContent=tr(o.value));
 renderTasks();renderNotes();updatePoints();document.getElementById("userName").value=userName;
 document.getElementById("quizArea").innerHTML="";
}
function showPage(id){
 document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
 document.getElementById(id).classList.add("active");
}
function toggleDark(){
 dark=!dark;document.body.classList.toggle("dark",dark);
 localStorage.setItem("smartDark",dark);
 document.getElementById("darkBtn").textContent=dark?tr("light"):tr("dark");
}
function updatePoints(){
 document.getElementById("points").textContent=points;
 document.getElementById("profilePoints").textContent=points;
 localStorage.setItem("smartPoints",points);
}
function claimDaily(){
 let today=new Date().toDateString();
 if(localStorage.getItem("smartDaily")===today){
  document.getElementById("dailyStatus").textContent=tr("dailyDone");return;
 }
 points+=10;localStorage.setItem("smartDaily",today);
 document.getElementById("dailyStatus").textContent=tr("dailySuccess");
 updatePoints();
}
function saveProfile(){
 userName=document.getElementById("userName").value.trim();
 localStorage.setItem("smartName",userName);
 document.getElementById("welcome").textContent=userName?tr("welcome")+" "+userName:tr("welcome");
 document.getElementById("profileMessage").textContent=tr("nameSaved");
}
function calculate(){
 let a=Number(document.getElementById("num1").value);
 let b=Number(document.getElementById("num2").value);
 let op=document.getElementById("operation").value;
 if(document.getElementById("num1").value===""||document.getElementById("num2").value===""){
  document.getElementById("answer").textContent="Enter both numbers";return;
 }
 if(op==="/"&&b===0){document.getElementById("answer").textContent="Cannot divide by zero";return;}
 let result=op==="+"?a+b:op==="-"?a-b:op==="*"?a*b:a/b;
 document.getElementById("answer").textContent="Answer: "+result;
}
function addTask(){
 let value=document.getElementById("taskInput").value.trim();
 if(!value)return;
 tasks.push({text:value,done:false});
 document.getElementById("taskInput").value="";
 localStorage.setItem("smartTasks",JSON.stringify(tasks));renderTasks();
}
function renderTasks(){
 let box=document.getElementById("taskList");if(!box)return;box.innerHTML="";
 if(!tasks.length){box.textContent=tr("empty");return;}
 tasks.forEach((task,i)=>{
  let div=document.createElement("div");div.className="item";
  let span=document.createElement("span");span.textContent=(task.done?"✓ ":"")+task.text;
  let done=document.createElement("button");done.textContent=tr("done");
  done.onclick=()=>{tasks[i].done=!tasks[i].done;localStorage.setItem("smartTasks",JSON.stringify(tasks));renderTasks()};
  let del=document.createElement("button");del.textContent=tr("delete");
  del.onclick=()=>{tasks.splice(i,1);localStorage.setItem("smartTasks",JSON.stringify(tasks));renderTasks()};
  div.append(span,done,del);box.appendChild(div);
 });
}
function saveNote(){
 let title=document.getElementById("noteTitle").value.trim();
 let body=document.getElementById("noteBody").value.trim();
 if(!title&&!body)return;
 notes.push({title:title||"Note",body});
 localStorage.setItem("smartNotes",JSON.stringify(notes));
 document.getElementById("noteTitle").value="";
 document.getElementById("noteBody").value="";
 renderNotes();
}
function renderNotes(){
 let box=document.getElementById("notesList");if(!box)return;box.innerHTML="";
 if(!notes.length){box.textContent=tr("empty");return;}
 notes.forEach((note,i)=>{
  let div=document.createElement("div");div.className="item";
  let content=document.createElement("div");
  let strong=document.createElement("b");strong.textContent=note.title;
  let p=document.createElement("p");p.textContent=note.body;
  content.append(strong,p);
  let del=document.createElement("button");del.textContent=tr("delete");
  del.onclick=()=>{notes.splice(i,1);localStorage.setItem("smartNotes",JSON.stringify(notes));renderNotes()};
  div.append(content,del);box.appendChild(div);
 });
}

/* Quiz question bank */
const bank={
mr:[
{c:"gk",q:"भारताची राजधानी कोणती?",o:["मुंबई","नवी दिल्ली","पुणे","जयपूर"],a:1},
{c:"gk",q:"भारताचा राष्ट्रीय प्राणी कोणता?",o:["सिंह","वाघ","हत्ती","घोडा"],a:1},
{c:"gk",q:"भारताचा स्वातंत्र्यदिन कधी असतो?",o:["२६ जानेवारी","१५ ऑगस्ट","२ ऑक्टोबर","१४ नोव्हेंबर"],a:1},
{c:"science",q:"वनस्पती अन्न तयार करण्याच्या प्रक्रियेला काय म्हणतात?",o:["श्वसन","प्रकाशसंश्लेषण","पचन","बाष्पीभवन"],a:1},
{c:"science",q:"पाण्याचे रासायनिक सूत्र काय आहे?",o:["CO2","O2","H2O","NaCl"],a:2},
{c:"science",q:"सौरमालेतील सर्वात मोठा ग्रह कोणता?",o:["पृथ्वी","मंगळ","गुरू","शुक्र"],a:2},
{c:"history",q:"छत्रपती शिवाजी महाराजांचा जन्म कोणत्या किल्ल्यावर झाला?",o:["रायगड","शिवनेरी","प्रतापगड","सिंहगड"],a:1}
],
hi:[
{c:"gk",q:"भारत की राजधानी क्या है?",o:["मुंबई","नई दिल्ली","पुणे","जयपुर"],a:1},
{c:"gk",q:"भारत का राष्ट्रीय पशु कौन है?",o:["शेर","बाघ","हाथी","घोड़ा"],a:1},
{c:"gk",q:"भारत का स्वतंत्रता दिवस कब है?",o:["26 जनवरी","15 अगस्त","2 अक्टूबर","14 नवंबर"],a:1},
{c:"science",q:"पौधे भोजन बनाने की प्रक्रिया को क्या कहते हैं?",o:["श्वसन","प्रकाश संश्लेषण","पाचन","वाष्पीकरण"],a:1},
{c:"science",q:"पानी का रासायनिक सूत्र क्या है?",o:["CO2","O2","H2O","NaCl"],a:2},
{c:"science",q:"सौरमंडल का सबसे बड़ा ग्रह कौन है?",o:["पृथ्वी","मंगल","बृहस्पति","शुक्र"],a:2},
{c:"history",q:"छत्रपति शिवाजी महाराज का जन्म किस किले पर हुआ?",o:["रायगढ़","शिवनेरी","प्रतापगढ़","सिंहगढ़"],a:1}
],
en:[
{c:"gk",q:"What is the capital of India?",o:["Mumbai","New Delhi","Pune","Jaipur"],a:1},
{c:"gk",q:"What is the national animal of India?",o:["Lion","Tiger","Elephant","Horse"],a:1},
{c:"gk",q:"When is India's Independence Day?",o:["26 January","15 August","2 October","14 November"],a:1},
{c:"science",q:"What is the food-making process in plants called?",o:["Respiration","Photosynthesis","Digestion","Evaporation"],a:1},
{c:"science",q:"What is the chemical formula of water?",o:["CO2","O2","H2O","NaCl"],a:2},
{c:"science",q:"Which is the largest planet in our solar system?",o:["Earth","Mars","Jupiter","Venus"],a:2},
{c:"history",q:"Where was Chhatrapati Shivaji Maharaj born?",o:["Raigad","Shivneri","Pratapgad","Sinhagad"],a:1}
]
};
let quizQuestions=[],quizIndex=0,quizScore=0,answered=false;
function startQuiz(){
 let cat=document.getElementById("category").value;
 quizQuestions=bank[lang].filter(q=>cat==="all"||q.c===cat).map(q=>({...q,o:[...q.o]}));
 if(cat==="all"||cat==="math"){
  for(let i=0;i<25;i++){
   let a=Math.floor(Math.random()*20)+1,b=Math.floor(Math.random()*20)+1;
   let answer=a+b,opts=[answer,answer+2,Math.max(0,answer-3),answer+5];
   opts.sort(()=>Math.random()-.5);
   quizQuestions.push({c:"math",q:lang==="mr"?`${a} + ${b} = किती?`:lang==="hi"?`${a} + ${b} = कितना?`:`What is ${a} + ${b}?`,o:opts.map(String),a:opts.indexOf(answer)});
  }
 }
 quizQuestions.sort(()=>Math.random()-.5);
 quizQuestions=quizQuestions.slice(0,10);
 quizIndex=0;quizScore=0;showQuestion();
}
function showQuestion(){
 let area=document.getElementById("quizArea");
 if(!quizQuestions.length){area.textContent=tr("empty");return;}
 answered=false;
 let q=quizQuestions[quizIndex];
 area.innerHTML=`<p>Question ${quizIndex+1} / ${quizQuestions.length}</p><h3 id="questionText"></h3><div id="options"></div><p id="result"></p>`;
 document.getElementById("questionText").textContent=q.q;
 q.o.forEach((opt,i)=>{
  let btn=document.createElement("button");btn.className="option";btn.textContent=opt;
  btn.onclick=()=>checkAnswer(i);document.getElementById("options").appendChild(btn);
 });
}
function checkAnswer(i){
 if(answered)return;answered=true;
 let q=quizQuestions[quizIndex];
 document.querySelectorAll("#options button").forEach((b,index)=>{
  b.disabled=true;
  if(index===q.a)b.textContent="✓ "+b.textContent;
 });
 if(i===q.a){quizScore+=10;document.getElementById("result").textContent=tr("correct")}
 else{document.getElementById("result").textContent=tr("wrong")+" Answer: "+q.o[q.a]}
 let next=document.createElement("button");
 next.textContent=quizIndex===quizQuestions.length-1?tr("finish"):tr("next");
 next.onclick=nextQuestion;document.getElementById("quizArea").appendChild(next);
}
function nextQuestion(){
 quizIndex++;
 if(quizIndex>=quizQuestions.length){
  points+=quizScore;updatePoints();
  document.getElementById("quizArea").innerHTML=`<h3>${tr("finish")} ${quizScore}/100</h3>`;
  let btn=document.createElement("button");btn.textContent=tr("restart");btn.onclick=startQuiz;
  document.getElementById("quizArea").appendChild(btn);
 }else showQuestion();
}
document.body.classList.toggle("dark",dark);
applyLanguage();
if(userName)document.getElementById("welcome").textContent=tr("welcome")+" "+userName;
</script>
</body>
</html>
