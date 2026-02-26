<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>菩薩戒勇者修行之路</title>
<style>
body{
font-family:-apple-system,BlinkMacSystemFont;
background:linear-gradient(#f4f1e8,#e8dcc7);
text-align:center;
padding:20px;
margin:0;
}
.card{
background:white;
padding:25px;
border-radius:20px;
box-shadow:0 10px 25px rgba(0,0,0,.15);
max-width:420px;
margin:auto;
}
h2{color:#8c6239}
button{
display:block;
width:100%;
padding:14px;
margin:8px 0;
border-radius:12px;
border:none;
background:#8c6239;
color:white;
font-size:16px;
}
button:hover{opacity:.9}
.progress{
height:8px;
background:#ddd;
border-radius:10px;
margin-bottom:15px;
overflow:hidden;
}
.bar{
height:8px;
background:#4caf50;
width:0%;
}
.result{margin-top:10px;font-weight:bold}
</style>
</head>
<body>

<div class="card">
<h2>🧘 菩薩戒勇者修行之路</h2>
<div class="progress"><div class="bar" id="bar"></div></div>
<p id="question"></p>
<div id="answers"></div>
<p class="result" id="result"></p>
</div>

<script>
const quiz = [
{q:"睡袋或棉被要自備嗎？",a:["要","不用"],c:0},
{q:"可以攜帶個人電腦嗎？",a:["可以","不可以"],c:1},
{q:"起板時間是？",a:["4:10","6:00"],c:0},
{q:"戒期間可以聊天嗎？",a:["可以","不可以"],c:1},
{q:"進齋堂應該？",a:["念佛依序入","邊走邊聊天"],c:0},
{q:"作息依什麼為準？",a:["自己決定","法器訊號"],c:1},
{q:"可以私自換床位嗎？",a:["可以","不可以"],c:1},
{q:"吃完飯要？",a:["默念佛號","滑手機"],c:0}
];

let index=0;
let score=0;

function load(){
if(index>=quiz.length){
document.getElementById("question").innerHTML=
"🎉 圓滿受戒勇者！<br>得分："+score+"/"+quiz.length+
"<br><br><button onclick='restart()'>重新挑戰</button>";
document.getElementById("answers").innerHTML="";
document.getElementById("bar").style.width="100%";
return;
}

document.getElementById("question").innerText=quiz[index].q;
let html="";
quiz[index].a.forEach((text,i)=>{
html+=`<button onclick="answer(${i})">${text}</button>`;
});
document.getElementById("answers").innerHTML=html;
document.getElementById("result").innerText="";
document.getElementById("bar").style.width=
((index/quiz.length)*100)+"%";
}

function answer(i){
if(i===quiz[index].c){
score++;
document.getElementById("result").innerText="✅ 正確！";
}else{
document.getElementById("result").innerText="❌ 再想想";
}
index++;
setTimeout(load,800);
}

function restart(){
index=0;
score=0;
load();
}

load();
</script>

</body>
</html>
