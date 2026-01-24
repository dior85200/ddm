<!DOCTYPE html>
<html lang="zh-TW">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>11408 福田班第一車點名工具</title>

<style>
body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; padding: 20px; background-color: #f0f2f5; }
h1 { text-align: center; color: #1a73e8; font-size: 28px; margin-bottom: 10px; }

.summary-bar { text-align:center; font-size:20px; font-weight:bold; margin-bottom:15px; color:#0b8043; }

.reset-btn {
    display:block; margin:10px auto 20px; padding:10px 20px;
    font-size:18px; border:none; border-radius:8px;
    background:#d93025; color:#fff;
}

.group-btn {
    font-size:14px;
    padding:6px 10px;
    border:none;
    border-radius:6px;
    background:#1a73e8;
    color:#fff;
}

.leader-section { background:#fff; padding:15px; border-radius:12px; margin-bottom:20px; border-left:8px solid #d93025; box-shadow:0 2px 5px rgba(0,0,0,0.1); }
.leader-title { color:#d93025; font-weight:bold; font-size:22px; margin-bottom:10px; }

.group-card { background:#fff; padding:15px; border-radius:12px; margin-bottom:15px; box-shadow:0 2px 5px rgba(0,0,0,0.1); }
.group-header { display:flex; justify-content:space-between; align-items:center; border-bottom:2px solid #eee; padding-bottom:8px; margin-bottom:12px; gap:10px; flex-wrap:wrap;}
.group-name { font-size:22px; font-weight:bold; }
.group-count { background:#e8f0fe; color:#1967d2; padding:4px 12px; border-radius:20px; font-size:16px; font-weight:bold; }

.member-list { display:flex; flex-wrap:wrap; gap:10px; }
.member-item { display:flex; align-items:center; background:#f8f9fa; border:1px solid #ddd; padding:10px 15px; border-radius:8px; cursor:pointer; transition:0.2s; }
.member-item input { width:22px; height:22px; margin-right:10px; }
.member-item span { font-size:20px; }

.member-item.checked { background:#e6ffed; border-color:#52c41a; color:#2e7d32; text-decoration:line-through; opacity:0.65; }

.leader-text { color:#d93025 !important; font-weight:900 !important; }
.sub-leader-text { color:#f29900 !important; font-weight:bold; }
</style>
</head>

<body>

<h1>🚌 第一車點名清單</h1>
<div class="summary-bar">已到：<span id="totalChecked">0</span> / <span id="totalPeople">0</span></div>
<button class="reset-btn" onclick="resetAll()">🔄 全部清除</button>

<div class="leader-section">
    <div class="leader-title">👑 總指揮 (車長/副車)</div>
    <div class="member-list">
        <label class="member-item"><input type="checkbox"><span class="leader-text">車長：邱瀚生</span></label>
        <label class="member-item"><input type="checkbox"><span class="sub-leader-text">副車：戴長青</span></label>
        <label class="member-item"><input type="checkbox"><span class="sub-leader-text">副車：連吉昌</span></label>
    </div>
</div>

<div id="groups"></div>

<script>
const data = [
    { group:"第 06 組", members:["楊嘉玲","賴瑩臻","姚淑美","林青蓉","楊嘉惠","楊碧秀","陳珮玲"] },
    { group:"第 08 組", members:["劉寶愛","黃昭蓉","胡達俊","謝淑圭","黃俐儷"] },
    { group:"第 12 組", members:["張瑞斌","賴鳳秋","周惠雯","許玳瑛","鄧湘葳","宋佩娟"] },
    { group:"第 13 組", members:["許淑菁","李美甄","柯雅馨","張玉如"] },
    { group:"第 15 組", members:["李權峰","蕭美玲","林癸吟","劉旭三","陳榆鈞","林閭華","張慧千"] },
    { group:"內護組", members:["黃美惠","許玉葉","張瓊元"] }
];

const groupsContainer = document.getElementById('groups');

function createGroups() {
    data.forEach((item, index) => {
        const card = document.createElement('div');
        card.className = 'group-card';
        const total = item.members.length;

        let membersHtml = item.members.map(name => `
            <label class="member-item">
                <input type="checkbox" class="member-checkbox">
                <span>${name}</span>
            </label>
        `).join('');

        card.innerHTML = `
            <div class="group-header">
                <span class="group-name">${item.group}</span>
                <span class="group-count">已到 <span class="checked-count">0</span> / ${total}</span>
                <button class="group-btn" onclick="toggleGroup(${index}, this)">本組全到</button>
            </div>
            <div class="member-list">${membersHtml}</div>
        `;
        groupsContainer.appendChild(card);
    });
    updateTotalPeople();
}

function toggleGroup(groupIndex, btn) {
    const card = document.querySelectorAll('.group-card')[groupIndex];
    const checkboxes = card.querySelectorAll('.member-checkbox');
    const allChecked = [...checkboxes].every(cb => cb.checked);

    checkboxes.forEach(cb => {
        cb.checked = !allChecked;
        cb.parentElement.classList.toggle('checked', cb.checked);
    });

    btn.textContent = allChecked ? "本組全到" : "取消全到";
    updateCounts();
}

function updateCounts() {
    document.querySelectorAll('.group-card').forEach(card => {
        const checkboxes = card.querySelectorAll('.member-checkbox');
        const checked = card.querySelectorAll('.member-checkbox:checked').length;
        card.querySelector('.checked-count').textContent = checked;
    });

    const totalChecked = document.querySelectorAll('input:checked').length;
    document.getElementById('totalChecked').textContent = totalChecked;
}

function updateTotalPeople() {
    const total = document.querySelectorAll('input').length;
    document.getElementById('totalPeople').textContent = total;
}

function resetAll() {
    document.querySelectorAll('input').forEach(cb => cb.checked = false);
    document.querySelectorAll('.member-item').forEach(el => el.classList.remove('checked'));
    document.querySelectorAll('.group-btn').forEach(btn => btn.textContent = "本組全到");
    updateCounts();
}

document.addEventListener('change', function(e) {
    if (e.target.classList.contains('member-checkbox') || e.target.closest('.leader-section')) {
        const label = e.target.parentElement;
        label.classList.toggle('checked', e.target.checked);
        updateCounts();
    }
});

createGroups();
</script>

</body>
</html>