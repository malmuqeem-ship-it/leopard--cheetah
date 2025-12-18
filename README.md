<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>صحيح أم غير صحيح – الفهد والنمر العربي</title>

<style>
html, body {width:100%; height:100%;}
body{
  margin:0;
  font-family:"Noto Kufi Arabic", sans-serif;
  background: linear-gradient(#f9f6ee, #e8dcc3);
  display:flex; justify-content:center; align-items:center;
  min-height:100vh;
  text-align:center;
  color:#203228;
}
main{
  background: rgba(255,249,240,0.95);
  padding:22px 28px;
  border-radius:18px;
  box-shadow:0 6px 16px rgba(0,0,0,.15);
  width:90%;
  max-width:600px;
}
h1{color:#2f6f4f; font-size:22px; margin:0 0 8px;}
button{
  margin:8px;
  padding:12px 18px;
  border:0;
  border-radius:10px;
  cursor:pointer;
  font-size:18px;
  font-weight:700;
}
.b-true{background:#2d9d62;color:#fff;}
.b-false{background:#c85151;color:#fff;}
#feedback{
  margin-top:12px;
  padding:10px;
  border-radius:10px;
  display:none;
  background:#fff;
  border:1px solid #e6dec9;
}
#nextBtn{display:none; background:#2f6f4f; color:#fff;}
#end{display:none; margin-top:15px;}
</style>
</head>

<body>
<main>
  <h1>صحيح أم غير صحيح – الفهد والنمر العربي</h1>
  <p id="question">اضغطي "ابدئي" لعرض أول سؤال</p>

  <div>
    <button class="b-true" id="btnTrue" disabled>صحيح</button>
    <button class="b-false" id="btnFalse" disabled>غير صحيح</button>
  </div>

  <div id="feedback"></div>

  <button id="nextBtn">التالي ↻</button>

  <!-- 👇 onclick مباشر (حل مضمون) -->
  <button id="startBtn" onclick="startGame()">ابدئي ▶</button>

  <div id="end">
    <h3>انتهت اللعبة 🎉</h3>
    <p>نتيجتك: <span id="score"></span> من 3</p>
    <button onclick="location.reload()">إعادة</button>
  </div>
</main>

<script>
/* نخلي الدوال Global عشان onclick يشتغل */
const questions = [
  { q:"الفهد هو أسرع حيوان بري على اليابسة.", a:true,
    ex:"صحيح ✅ الفهد يُعد الأسرع بين جميع الحيوانات البرية." },

  { q:"النمر لديه خطوط سوداء واضحة على الوجه من العين إلى الفم.", a:false,
    ex:"غير صحيح ❌ هذه الخطوط توجد عند الفهد (خطوط الدموع) وتساعده على تقليل وهج الشمس أثناء الجري والصيد." },

  { q:"بقع الفهد تكون غالبًا على شكل وريدات وليست نقاط.", a:false,
    ex:"غير صحيح ❌ بقع الفهد نقاط دائرية، أما الوريدات فهي تميّز النمر." }
];

let index = -1;
let score = 0;

let q, fb, t, f, n, s, endBox;

function init(){
  q = document.getElementById("question");
  fb = document.getElementById("feedback");
  t = document.getElementById("btnTrue");
  f = document.getElementById("btnFalse");
  n = document.getElementById("nextBtn");
  s = document.getElementById("startBtn");
  endBox = document.getElementById("end");

  t.onclick = () => check(true);
  f.onclick = () => check(false);
  n.onclick = showQuestion;
}

function startGame(){
  // تهيئة لو ما كانت جاهزة
  if(!q) init();

  // منع تكرار التشغيل لو ضغطت مرتين
  s.style.display = "none";
  showQuestion();
}

function showQuestion(){
  index++;
  if(index >= questions.length){ endGame(); return; }

  const cur = questions[index];
  q.textContent = cur.q;

  fb.style.display = "none";
  t.disabled = f.disabled = false;
  n.style.display = "none";
}

function check(ans){
  const cur = questions[index];
  const correct = ans === cur.a;

  fb.style.display = "block";
  fb.textContent = cur.ex;

  if(correct) score++;

  t.disabled = f.disabled = true;
  n.style.display = "inline-block";
}

function endGame(){
  q.textContent = "أحسنتِ! انتهت الأسئلة.";
  t.style.display = f.style.display = n.style.display = s.style.display = "none";
  fb.style.display = "none";
  endBox.style.display = "block";
  document.getElementById("score").textContent = score;
}

document.addEventListener("DOMContentLoaded", init);
</script>
</body>
</html>
