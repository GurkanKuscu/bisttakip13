# bisttakip13[bist_ird_takip_v3.html](https://github.com/user-attachments/files/25968399/bist_ird_takip_v3.html)
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BIST IRD — Canlı Takip Paneli</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #F5F4F1;
  --surface: #FFFFFF;
  --border: #E0DED8;
  --border-strong: #C5C3BC;
  --text: #18171A;
  --muted: #6A6870;
  --hint: #9A98A0;
  --green: #1A6B3C;
  --green-bg: #EEF7F2;
  --green-border: #B8DEC8;
  --red: #8B1A1A;
  --red-bg: #FDF0F0;
  --red-border: #EFBCBC;
  --gold: #8B6800;
  --gold-bg: #FDF8EE;
  --gold-border: #E8D5A0;
  --blue: #1B4F8A;
  --blue-bg: #EEF4FC;
  --blue-border: #BDD1EF;
  --amber: #7A4F00;
  --amber-bg: #FDF5E8;
  --amber-border: #EDD9A3;
  --mono: 'IBM Plex Mono', monospace;
  --sans: 'IBM Plex Sans', sans-serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: var(--sans); background: var(--bg); color: var(--text); font-size: 14px; min-height: 100vh; }

/* HEADER */
.header {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 14px 28px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 50;
}
.header-left { display: flex; align-items: center; gap: 16px; }
.logo { font-family: var(--mono); font-size: 13px; font-weight: 500; }
.logo span { color: var(--muted); font-weight: 400; }
.status-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--green); animation: pulse 2s infinite; }
.status-dot.loading { background: var(--amber); animation: none; }
.status-dot.error { background: var(--red); animation: none; }
@keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.4; } }
.status-text { font-family: var(--mono); font-size: 11px; color: var(--muted); }
.refresh-btn {
  font-family: var(--mono); font-size: 11px; padding: 5px 14px;
  border: 1px solid var(--border); border-radius: 4px;
  background: transparent; color: var(--muted); cursor: pointer;
  transition: all 0.15s;
}
.refresh-btn:hover { background: var(--bg); color: var(--text); }

/* SUMMARY BAR */
.summary-bar {
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  padding: 10px 28px;
  display: flex;
  gap: 32px;
  overflow-x: auto;
}
.sum-item { display: flex; flex-direction: column; align-items: center; gap: 2px; white-space: nowrap; }
.sum-label { font-family: var(--mono); font-size: 10px; color: var(--hint); text-transform: uppercase; letter-spacing: 0.05em; }
.sum-val { font-family: var(--mono); font-size: 14px; font-weight: 500; }
.sum-pos { color: var(--green); }
.sum-neg { color: var(--red); }
.sum-neu { color: var(--text); }

/* MAIN */
.main { padding: 20px 28px 60px; max-width: 1200px; }

/* TABLE */
.table-wrap { background: var(--surface); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; }
table { width: 100%; border-collapse: collapse; }
thead tr { background: var(--bg); }
th {
  padding: 10px 14px;
  font-family: var(--mono); font-size: 10px; color: var(--hint);
  text-transform: uppercase; letter-spacing: 0.06em;
  text-align: left; font-weight: 500;
  border-bottom: 1px solid var(--border);
  white-space: nowrap;
}
th.r { text-align: right; }
td { padding: 0; border-bottom: 1px solid var(--border); vertical-align: middle; }
tr:last-child td { border-bottom: none; }
tr:hover td { background: #FAFAF8; }

.cell { padding: 13px 14px; }
.cell.r { text-align: right; }

/* Ticker */
.ticker-wrap { display: flex; align-items: center; gap: 10px; }
.ticker { font-family: var(--mono); font-size: 14px; font-weight: 500; color: var(--text); }
.score-badge {
  font-family: var(--mono); font-size: 10px; font-weight: 500;
  padding: 2px 7px; border-radius: 3px;
}
.badge-gold { background: var(--gold-bg); color: var(--gold); border: 1px solid var(--gold-border); }
.badge-blue { background: var(--blue-bg); color: var(--blue); border: 1px solid var(--blue-border); }
.badge-gray { background: var(--bg); color: var(--muted); border: 1px solid var(--border); }
.signal-icon { font-size: 14px; }
.badges-row { display: flex; gap: 4px; flex-wrap: wrap; margin-top: 4px; }
.tag {
  font-family: var(--mono); font-size: 9px; padding: 1px 6px;
  border-radius: 2px; color: var(--muted); background: var(--bg);
  border: 1px solid var(--border);
}
.tag-blue { color: var(--blue); background: var(--blue-bg); border-color: var(--blue-border); }
.tag-gold { color: var(--gold); background: var(--gold-bg); border-color: var(--gold-border); }
.tag-red { color: var(--red); background: var(--red-bg); border-color: var(--red-border); }
.tag-amber { color: var(--amber); background: var(--amber-bg); border-color: var(--amber-border); }

/* Price */
.price-current { font-family: var(--mono); font-size: 15px; font-weight: 500; }
.price-current.loading { color: var(--hint); }
.price-entry { font-family: var(--mono); font-size: 11px; color: var(--hint); margin-top: 2px; }

/* PnL */
.pnl-val { font-family: var(--mono); font-size: 14px; font-weight: 500; }
.pnl-sub { font-family: var(--mono); font-size: 11px; color: var(--muted); margin-top: 2px; }
.pos { color: var(--green); }
.neg { color: var(--red); }
.neu { color: var(--muted); }

/* Progress bar */
.progress-wrap { width: 100%; min-width: 120px; }
.progress-labels { display: flex; justify-content: space-between; margin-bottom: 4px; }
.progress-label { font-family: var(--mono); font-size: 10px; color: var(--hint); }
.progress-track { height: 5px; background: var(--border); border-radius: 3px; position: relative; overflow: hidden; }
.progress-fill { height: 100%; border-radius: 3px; transition: width 0.4s ease; }
.fill-green { background: var(--green); }
.fill-red { background: var(--red); }
.fill-amber { background: #E8A000; }
.progress-marker { position: absolute; top: 0; height: 100%; width: 2px; background: var(--border-strong); }

/* Stop / Target */
.level-val { font-family: var(--mono); font-size: 12px; }
.level-sub { font-family: var(--mono); font-size: 10px; color: var(--hint); margin-top: 2px; }

/* Status badge */
.status-badge {
  font-family: var(--mono); font-size: 10px; font-weight: 500;
  padding: 3px 10px; border-radius: 3px;
}
.st-hold { background: var(--blue-bg); color: var(--blue); border: 1px solid var(--blue-border); }
.st-target { background: var(--green-bg); color: var(--green); border: 1px solid var(--green-border); }
.st-stop { background: var(--red-bg); color: var(--red); border: 1px solid var(--red-border); }
.st-warn { background: var(--amber-bg); color: var(--amber); border: 1px solid var(--amber-border); }

/* Spinner */
.spinner {
  display: inline-block; width: 12px; height: 12px;
  border: 2px solid var(--border); border-top-color: var(--muted);
  border-radius: 50%; animation: spin 0.8s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

@media (max-width: 900px) {
  .header { flex-direction: column; gap: 10px; align-items: flex-start; padding: 12px 16px; }
  .summary-bar { padding: 10px 16px; gap: 20px; }
  .main { padding: 16px; }
  th, .cell { padding: 10px 10px; }
  .hide-mobile { display: none; }
}
</style>
</head>
<body>

<div class="header">
  <div class="header-left">
    <div class="logo">BIST IRD <span>v7.4</span> — Canlı Takip</div>
    <div style="display:flex;align-items:center;gap:6px">
      <div class="status-dot loading" id="statusDot"></div>
      <span class="status-text" id="statusText">Yükleniyor...</span>
    </div>
  </div>
  <div style="display:flex;align-items:center;gap:10px">
    <span class="status-text" id="lastUpdate">—</span>
    <button class="refresh-btn" onclick="fetchAllPrices()">↻ Yenile</button>
  </div>
</div>

<div class="summary-bar" id="summaryBar">
  <div class="sum-item"><div class="sum-label">Takip</div><div class="sum-val sum-neu" id="sumTotal">—</div></div>
  <div class="sum-item"><div class="sum-label">Kazanan</div><div class="sum-val sum-pos" id="sumWin">—</div></div>
  <div class="sum-item"><div class="sum-label">Kaybeden</div><div class="sum-val sum-neg" id="sumLoss">—</div></div>
  <div class="sum-item"><div class="sum-label">Hedefe yakın</div><div class="sum-val sum-pos" id="sumNearTarget">—</div></div>
  <div class="sum-item"><div class="sum-label">Stopa yakın</div><div class="sum-val sum-neg" id="sumNearStop">—</div></div>
  <div class="sum-item"><div class="sum-label">Ort. P&L</div><div class="sum-val" id="sumAvgPnl">—</div></div>
</div>

<div class="main">
  <div class="table-wrap">
    <table id="mainTable">
      <thead>
        <tr>
          <th>Hisse / Sinyal</th>
          <th class="r">Alış</th>
          <th class="r">Güncel</th>
          <th class="r">P&L%</th>
          <th class="hide-mobile">Stop → Hedef</th>
          <th class="hide-mobile">İlerleme</th>
          <th class="r">Durum</th>
        </tr>
      </thead>
      <tbody id="tableBody"></tbody>
    </table>
  </div>
  <div style="margin-top:10px; font-family:var(--mono); font-size:10px; color:var(--hint); padding: 0 4px;">
    Fiyatlar Yahoo Finance üzerinden çekiliyor. Borsa açıkken ~60sn gecikme. Otomatik yenileme: 90 saniye.
  </div>
</div>

<script>
const STOCKS = [
  { ticker:'ARASE', score:100, signal:'🏆', signalText:'Institutional Rally', entry:91.80, stop:84.10, target:107.20, pos:2.5,  tags:['Early Rally','Inst.Entry'], weekly:'bull', squeeze:'16bar' },
  { ticker:'DITAS', score:85,  signal:'💎', signalText:'Strong Swing',        entry:49.60, stop:43.27, target:62.25,  pos:1.5,  tags:['Inst.Entry'],             weekly:'bull', squeeze:'7bar'  },
  { ticker:'SEKFK', score:74,  signal:'📋', signalText:'Watchlist',           entry:10.13, stop:9.29,  target:11.82,  pos:0.4,  tags:['Early Rally','SPEK'],      weekly:'bull', squeeze:'7bar'  },
  { ticker:'BRKSN', score:73,  signal:'📋', signalText:'Watchlist',           entry:9.00,  stop:8.23,  target:10.54,  pos:0.4,  tags:['Early Rally','SPEK'],      weekly:'bull', squeeze:'11bar' },
  { ticker:'TURSG', score:72,  signal:'📋', signalText:'Watchlist',           entry:12.90, stop:12.06, target:14.58,  pos:0.9,  tags:['Early Rally'],             weekly:'bull', squeeze:'6bar'  },
  { ticker:'HURGZ', score:72,  signal:'💎', signalText:'Strong Swing',        entry:5.99,  stop:5.45,  target:7.07,   pos:1.5,  tags:['Inst.Entry'],             weekly:'bear', squeeze:'Released' },
  { ticker:'FORTE', score:71,  signal:'📋', signalText:'Watchlist',           entry:96.50, stop:87.86, target:113.79, pos:0.8,  tags:[],                          weekly:'bull', squeeze:'10bar' },
  { ticker:'OZSUB', score:71,  signal:'📋', signalText:'Watchlist',           entry:23.06, stop:20.55, target:28.08,  pos:0.8,  tags:['Inst.Entry'],             weekly:'bull', squeeze:'-', pump:75 },
  { ticker:'PRZMA', score:71,  signal:'📋', signalText:'Watchlist',           entry:15.60, stop:13.99, target:18.82,  pos:0.4,  tags:['Inst.Entry','SPEK'],       weekly:'bull', squeeze:'-'    },
  { ticker:'INDES', score:68,  signal:'📋', signalText:'Watchlist',           entry:8.65,  stop:7.89,  target:10.17,  pos:0.8,  tags:['Inst.Entry'],             weekly:'bull', squeeze:'-'    },
];

let prices = {};

function scoreBadgeClass(s) {
  if (s >= 85) return 'badge-gold';
  if (s >= 70) return 'badge-blue';
  return 'badge-gray';
}

function tagClass(t) {
  if (t === 'Early Rally') return 'tag-blue';
  if (t === 'Inst.Entry')  return 'tag-gold';
  if (t === 'SPEK')        return 'tag-amber';
  if (t === 'Pump')        return 'tag-red';
  return '';
}

function progressColor(pct) {
  if (pct >= 80) return 'fill-green';
  if (pct <= 0)  return 'fill-red';
  return 'fill-amber';
}

function statusInfo(s, entry, stop, target) {
  if (!s) return { label:'Yükleniyor', cls:'st-hold' };
  const range = target - stop;
  const pos = s - stop;
  const pct = pos / range;
  if (s >= target) return { label:'🎯 Hedefe ulaştı', cls:'st-target' };
  if (s <= stop)   return { label:'🛑 Stop tetiklendi', cls:'st-stop' };
  if (pct >= 0.85) return { label:'⚡ Hedefe yakın', cls:'st-target' };
  if (pct <= 0.10) return { label:'⚠️ Stopa yakın', cls:'st-warn' };
  return { label:'◉ Tutulabilir', cls:'st-hold' };
}

function buildRows() {
  const tbody = document.getElementById('tableBody');
  tbody.innerHTML = '';
  STOCKS.forEach(st => {
    const tr = document.createElement('tr');
    tr.id = 'row-' + st.ticker;

    const allTags = [...st.tags];
    if (st.weekly === 'bear') allTags.push('W-Bear');
    if (st.pump && st.pump >= 50) allTags.push('Pump' + st.pump + '%');

    const tagsHtml = allTags.map(t =>
      `<span class="tag ${tagClass(t)}">${t}</span>`
    ).join('');

    tr.innerHTML = `
      <td><div class="cell">
        <div class="ticker-wrap">
          <span class="signal-icon">${st.signal}</span>
          <span class="ticker">${st.ticker}</span>
          <span class="score-badge ${scoreBadgeClass(st.score)}">${st.score}</span>
        </div>
        <div class="badges-row">${tagsHtml}</div>
      </div></td>
      <td><div class="cell r">
        <div class="level-val">${st.entry.toFixed(2)} TL</div>
        <div class="level-sub">Pos: %${st.pos}</div>
      </div></td>
      <td><div class="cell r" id="price-${st.ticker}">
        <div class="price-current loading"><span class="spinner"></span></div>
        <div class="price-entry">Baz: ${st.entry.toFixed(2)}</div>
      </div></td>
      <td><div class="cell r" id="pnl-${st.ticker}">
        <div class="pnl-val neu">—</div>
      </div></td>
      <td class="hide-mobile"><div class="cell" id="levels-${st.ticker}">
        <div style="display:flex;gap:16px">
          <div><div class="level-val neg">${st.stop.toFixed(2)}</div><div class="level-sub">Stop</div></div>
          <div><div class="level-val pos">${st.target.toFixed(2)}</div><div class="level-sub">Hedef</div></div>
        </div>
      </div></td>
      <td class="hide-mobile"><div class="cell" id="prog-${st.ticker}">
        <div class="progress-wrap">
          <div class="progress-labels">
            <span class="progress-label">${st.stop.toFixed(2)}</span>
            <span class="progress-label" id="pct-label-${st.ticker}">—</span>
            <span class="progress-label">${st.target.toFixed(2)}</span>
          </div>
          <div class="progress-track">
            <div class="progress-fill fill-amber" id="pbar-${st.ticker}" style="width:0%"></div>
          </div>
        </div>
      </div></td>
      <td><div class="cell r" id="status-${st.ticker}">
        <span class="status-badge st-hold">Yükleniyor</span>
      </div></td>
    `;
    tbody.appendChild(tr);
  });
}

function updateRow(st, price) {
  if (!price) return;

  const pnlPct = ((price - st.entry) / st.entry * 100);
  const pnlTl = price - st.entry;
  const range = st.target - st.stop;
  const pos = Math.max(0, Math.min(1, (price - st.stop) / range));
  const posPct = pos * 100;

  // Price cell
  const priceCell = document.getElementById('price-' + st.ticker);
  const pnlClass = pnlPct > 0 ? 'pos' : pnlPct < 0 ? 'neg' : 'neu';
  priceCell.innerHTML = `
    <div class="price-current ${pnlClass}">${price.toFixed(2)} TL</div>
    <div class="price-entry">Baz: ${st.entry.toFixed(2)}</div>
  `;

  // PnL cell
  const pnlCell = document.getElementById('pnl-' + st.ticker);
  const sign = pnlTl >= 0 ? '+' : '';
  pnlCell.innerHTML = `
    <div class="pnl-val ${pnlClass}">${sign}${pnlPct.toFixed(2)}%</div>
    <div class="pnl-sub">${sign}${pnlTl.toFixed(2)} TL</div>
  `;

  // Progress bar
  const pbar = document.getElementById('pbar-' + st.ticker);
  const pctLabel = document.getElementById('pct-label-' + st.ticker);
  if (pbar) {
    pbar.style.width = Math.max(0, Math.min(100, posPct)) + '%';
    pbar.className = 'progress-fill ' + progressColor(posPct);
  }
  if (pctLabel) {
    pctLabel.textContent = price.toFixed(2);
  }

  // Status
  const statusCell = document.getElementById('status-' + st.ticker);
  const { label, cls } = statusInfo(price, st.entry, st.stop, st.target);
  statusCell.innerHTML = `<span class="status-badge ${cls}">${label}</span>`;
}

function updateSummary() {
  const loaded = STOCKS.filter(s => prices[s.ticker]);
  if (!loaded.length) return;

  const wins = loaded.filter(s => prices[s.ticker] > s.entry);
  const losses = loaded.filter(s => prices[s.ticker] <= s.entry);
  const nearTarget = loaded.filter(s => {
    const p = prices[s.ticker];
    const range = s.target - s.stop;
    return p && (p - s.stop) / range >= 0.8;
  });
  const nearStop = loaded.filter(s => {
    const p = prices[s.ticker];
    const range = s.target - s.stop;
    return p && (p - s.stop) / range <= 0.1;
  });
  const avgPnl = loaded.reduce((acc, s) => {
    return acc + ((prices[s.ticker] - s.entry) / s.entry * 100);
  }, 0) / loaded.length;

  document.getElementById('sumTotal').textContent = loaded.length;
  document.getElementById('sumWin').textContent = wins.length;
  document.getElementById('sumLoss').textContent = losses.length;
  document.getElementById('sumNearTarget').textContent = nearTarget.length;
  document.getElementById('sumNearStop').textContent = nearStop.length;
  const avgEl = document.getElementById('sumAvgPnl');
  avgEl.textContent = (avgPnl >= 0 ? '+' : '') + avgPnl.toFixed(2) + '%';
  avgEl.className = 'sum-val ' + (avgPnl > 0 ? 'sum-pos' : avgPnl < 0 ? 'sum-neg' : 'sum-neu');
}

async function fetchPrice(ticker) {
  const sym = ticker + '.IS';
  // Try multiple approaches
  const attempts = [
    // 1. corsproxy.io with query1
    () => fetch(`https://corsproxy.io/?${encodeURIComponent('https://query1.finance.yahoo.com/v8/finance/chart/' + sym + '?interval=1m&range=1d')}`, { signal: AbortSignal.timeout(10000) }),
    // 2. corsproxy.io with query2
    () => fetch(`https://corsproxy.io/?${encodeURIComponent('https://query2.finance.yahoo.com/v8/finance/chart/' + sym + '?interval=1m&range=1d')}`, { signal: AbortSignal.timeout(10000) }),
    // 3. Direct with no-cors mode fallback via different proxy
    () => fetch(`https://api.allorigins.win/get?url=${encodeURIComponent('https://query1.finance.yahoo.com/v8/finance/chart/' + sym + '?interval=1m&range=1d')}`, { signal: AbortSignal.timeout(10000) }),
    // 4. codetabs proxy
    () => fetch(`https://api.codetabs.com/v1/proxy?quest=${encodeURIComponent('https://query1.finance.yahoo.com/v8/finance/chart/' + sym + '?interval=1m&range=1d')}`, { signal: AbortSignal.timeout(10000) }),
    // 5. htmldriven proxy
    () => fetch(`https://yacdn.org/proxy/https://query1.finance.yahoo.com/v8/finance/chart/${sym}?interval=1m&range=1d`, { signal: AbortSignal.timeout(10000) }),
  ];

  for (const attempt of attempts) {
    try {
      const res = await attempt();
      if (!res.ok) continue;
      const raw = await res.json();
      // allorigins wraps in {contents: "..."}
      const data = raw.contents ? JSON.parse(raw.contents) : raw;
      const price = data?.chart?.result?.[0]?.meta?.regularMarketPrice;
      if (price && price > 0) return price;
    } catch(e) {}
  }
  return null;
}

async function fetchAllPrices() {
  const dot = document.getElementById('statusDot');
  const statusText = document.getElementById('statusText');
  dot.className = 'status-dot loading';
  statusText.textContent = 'Fiyatlar güncelleniyor...';

  const results = await Promise.allSettled(
    STOCKS.map(s => fetchPrice(s.ticker).then(p => ({ ticker: s.ticker, price: p })))
  );

  let loaded = 0;
  results.forEach(r => {
    if (r.status === 'fulfilled' && r.value.price) {
      const { ticker, price } = r.value;
      prices[ticker] = price;
      const st = STOCKS.find(s => s.ticker === ticker);
      if (st) updateRow(st, price);
      loaded++;
    }
  });

  updateSummary();

  const now = new Date();
  const timeStr = now.toLocaleTimeString('tr-TR', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
  document.getElementById('lastUpdate').textContent = 'Son: ' + timeStr;

  if (loaded === STOCKS.length) {
    dot.className = 'status-dot';
    statusText.textContent = 'Canlı — ' + loaded + '/' + STOCKS.length + ' hisse';
  } else if (loaded > 0) {
    dot.className = 'status-dot';
    statusText.textContent = loaded + '/' + STOCKS.length + ' yüklendi';
  } else {
    dot.className = 'status-dot error';
    statusText.textContent = 'Bağlantı hatası';
  }
}

// Init
buildRows();
fetchAllPrices();
setInterval(fetchAllPrices, 90000);
</script>
</body>
</html>
