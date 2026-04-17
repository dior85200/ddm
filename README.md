<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>法鼓山活動行前確認</title>

<style>
body {
  font-family: "Noto Sans TC","Microsoft JhengHei",sans-serif;
  background-image: url('https://fagushan.ddm.org.tw/files/file_pool/1/0M005733797053262001/P75420150204010005s2.jpg');
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  margin: 0;
  padding: 20px;
  line-height: 1.8;
}

/* 毛玻璃卡片 */
.card {
  background: rgba(255,255,255,0.4);
  backdrop-filter: blur(5px);
  border-radius: 18px;
  box-shadow: 0 10px 35px rgba(0,0,0,0.25);
}

/* 長輩模式 */
.elder {
  font-size: 1.3em;
  line-height: 2;
  font-weight: 600;
}

.elder h1 { font-size: 34px; font-weight: 800; }
.elder h2 { font-size: 26px; font-weight: 700; }
.elder h3 { font-size: 22px; font-weight: 700; }

.elder li,
.elder span {
  font-size: 1.2em;
  font-weight: 600;
}

/* 標題 */
h1 { color: #b00020; text-align: center; margin-top: 0; }
h2 { text-align: center; border-bottom: 2px solid #ddd; padding-bottom: 10px; }

h3 {
  background: #f3f3f3;
  padding: 6px 15px;
  border-left: 5px solid #b00020;
  margin-top: 25px;
}

h4 { margin-top: 20px; }

/* 倒數 */
.countdown {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  color: #b00020;
  margin: 15px 0;
}

/* 勾選 */
ul { padding-left: 20px; }
li { margin-bottom: 10px; }

label {
  display: flex;
  align-items: flex-start;
  cursor: pointer;
}

input[type="checkbox"] {
  margin-right: 10px;
  margin-top: 6px;
  transform: scale(1.3);
}

input[type="checkbox"]:checked + span {
  text-decoration: line-through;
  color: #888;
}

/* 按鈕 */
.btn-container {
  text-align: center;
  margin-top: 25px;
}

button {
  background-color: #b00020;
  color: white;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 6px;
  cursor: pointer;
}

/* 底部圖片 */
.footer-img {
  text-align: center;
  margin-top: 30px;
}

.footer-img img {
  width: 100%;
  max-width: 650px;
  border-radius: 12px;
  box-shadow: 0 5px 20px rgba(0,0,0,0.2);
}

.footer-img p {
  font-size: 18px;
  margin-top: 10px;
}
</style>
</head>

<body>

<div class="card" id="mainCard">

<h1>法鼓山寶雲寺 朝山菩薩(通用版)</h1>
<h2>04/18～04/19「朝山・巡禮・憶師恩」</h2>

<div class="countdown" id="countdown"></div>

<div class="btn-container">
  <button onclick="toggleElder()">👴 大字模式</button>
</div>

<h3>📌 行前提醒</h3>
<ul>
<li>
  <span style="color:red; font-weight:bold;">07:00</span> 市議會集合，
  <span style="color:red; font-weight:bold;">07:50</span> 準時出發（逾時不候）
</li>
<li>您為第____車</li>
<li>請用後背包利於走路</li>
</ul>

<h3>✅ 行前確認清單</h3>

<h4>🍱 餐食準備</h4>
<ul>
  <li><label><input type="checkbox"><span>早齋需自理(車上不提供)</span></label></li>
  <li><label><input type="checkbox"><span>已攜帶湯匙或筷子(回程藥石用)(★不必帶便當盒）</span></label></li>
</ul>

<h4>🛏️ 住宿與個人物品</h4>
<ul>
  <li><label><input type="checkbox"><span>已準備後背包 方便朝山・巡禮。</span></label></li>
  <li><label><input type="checkbox"><span>已準備睡袋</span></label></li>
  <li><label><input type="checkbox"><span>已準備拖鞋</span></label></li>
  <li><label><input type="checkbox"><span>已準備沐浴乳、洗髮精(總本山不提供)</span></label></li>
  <li><label><input type="checkbox"><span>已準備牙刷、牙膏</span></label></li>
  <li><label><input type="checkbox"><span>已準備毛巾</span></label></li>
  <li><label><input type="checkbox"><span>已準備水杯</span></label></li>
  <li><label><input type="checkbox"><span>已準備雨具</span></label></li>
  <li><label><input type="checkbox"><span><strong>已準備白色透明雨衣（朝山必備）</strong></span></label></li>
  <li><label><input type="checkbox"><span>已準備遮陽帽</span></label></li>
  <li><label><input type="checkbox"><span>已準備外套與保暖衣物</span></label></li>
  <li><label><input type="checkbox"><span>已準備替換衣物</span></label></li>
  <li><label><input type="checkbox"><span>已攜帶健保卡</span></label></li>
  <li><label><input type="checkbox"><span>已攜帶個人藥品</span></label></li>
</ul>

<h4>👕 服裝確認</h4>
<ul>
  <li><label><input type="checkbox"><span>已準備樸素衣褲</span></label></li>
  <li><label><input type="checkbox"><span>已準備義工服(出坡義工)</span></label></li>
</ul>

<div class="btn-container">
  <button onclick="resetChecks()">清除勾選</button>
</div>


<script>
// 倒數計時
const target = new Date("2026-04-18T07:50:00");

function updateCountdown() {
  const now = new Date();
  const diff = target - now;

  if (diff <= 0) {
    document.getElementById("countdown").innerHTML = "🚍 已出發";
    return;
  }

  const h = Math.floor(diff / (1000 * 60 * 60));
  const m = Math.floor((diff / (1000 * 60)) % 60);
  const s = Math.floor((diff / 1000) % 60);

  document.getElementById("countdown").innerHTML =
    `⏰ 距離出發還有：${h} 小時 ${m} 分 ${s} 秒`;
}

setInterval(updateCountdown, 1000);

// 長輩模式
function toggleElder() {
  document.getElementById("mainCard").classList.toggle("elder");
}

// 清除勾選
function resetChecks() {
  document.querySelectorAll("input[type=checkbox]").forEach(cb => cb.checked=false);
}
</script>
<!-- 日程表 -->
<div class="footer-img">
  <img src="https://raw.githubusercontent.com/dior85200/DDM-checklist/main/朝山日程表.jpg">
  <p>🗓️ 朝山日程表</p>
</div>
