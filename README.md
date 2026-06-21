<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BJJ Manager Pro</title>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{--bg:#0a0a12;--s1:#11111c;--s2:#181826;--s3:#1f1f30;--border:rgba(255,255,255,0.07);--accent:#e63946;--green:#2dc653;--yellow:#ffd166;--blue:#4cc9f0;--purple:#9b5de5;--orange:#fb8500;--teal:#06d6a0;--white:#f0f0f8;--muted:#5a5a72}
body{background:var(--bg);color:var(--white);font-family:system-ui,-apple-system,sans-serif;min-height:100vh}
::-webkit-scrollbar{width:4px}::-webkit-scrollbar-thumb{background:var(--accent);border-radius:2px}
.topbar{position:fixed;top:0;left:0;right:0;height:52px;background:var(--s1);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 14px;z-index:100;gap:10px}
.logo{font-weight:800;font-size:16px;letter-spacing:2px;white-space:nowrap;flex-shrink:0}
.logo span{color:var(--accent)}
.topbar-nav{display:flex;gap:2px;overflow-x:auto;flex:1;align-items:center}
.topbar-nav::-webkit-scrollbar{display:none}
.tb{padding:5px 10px;border-radius:5px;border:none;background:transparent;color:var(--muted);font-size:11px;font-weight:500;cursor:pointer;transition:all .15s;white-space:nowrap;flex-shrink:0}
.tb:hover{background:rgba(255,255,255,.06);color:var(--white)}
.tb.on{background:rgba(230,57,70,.15);color:var(--accent)}
.topbar-right{display:flex;gap:6px;align-items:center;flex-shrink:0}
.hamburger{display:none;background:none;border:none;color:var(--white);font-size:22px;cursor:pointer;padding:4px 8px}
.mob-menu{position:fixed;top:52px;left:0;right:0;background:var(--s1);border-bottom:1px solid var(--border);z-index:9999;padding:8px;flex-direction:column;gap:2px;max-height:calc(100vh - 52px);overflow-y:auto;box-shadow:0 8px 32px rgba(0,0,0,.6);display:none}
.mob-menu.open{display:flex}
.mob-tb{display:block;width:100%;padding:13px 16px;border-radius:7px;border:none;background:transparent;color:var(--muted);font-size:14px;font-weight:500;cursor:pointer;text-align:left;transition:background .15s,color .15s}
.mob-tb:hover{background:rgba(255,255,255,.07);color:var(--white)}
.mob-tb.on{background:rgba(230,57,70,.15);color:var(--accent)}
.wrap{max-width:1180px;margin:0 auto;padding:66px 16px 40px}
.page{display:none}.page.on{display:block}
.ph{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:18px;flex-wrap:wrap;gap:10px}
.ph h1{font-size:22px;font-weight:800;letter-spacing:-.5px}
.ph p{font-size:11px;color:var(--muted);margin-top:2px}
.btn-row{display:flex;gap:6px;flex-wrap:wrap}
.btn{display:inline-flex;align-items:center;gap:5px;padding:7px 13px;border-radius:6px;border:none;cursor:pointer;font-size:12px;font-weight:600;transition:all .15s}
.btn:hover{opacity:.88;transform:translateY(-1px)}
.btn-red{background:var(--accent);color:#fff}
.btn-green{background:var(--green);color:#000}
.btn-blue{background:var(--blue);color:#000}
.btn-purple{background:var(--purple);color:#fff}
.btn-orange{background:var(--orange);color:#000}
.btn-ghost{background:transparent;border:1px solid var(--border);color:var(--muted)}.btn-ghost:hover{color:var(--white)}
.btn-sm{padding:5px 10px;font-size:11px}
.stats-grid{display:grid;gap:10px;margin-bottom:14px}
.g5{grid-template-columns:repeat(5,1fr)}.g4{grid-template-columns:repeat(4,1fr)}.g3{grid-template-columns:repeat(3,1fr)}.g2{grid-template-columns:1fr 1fr}
.stat{background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:13px;border-top:3px solid}
.stat.cb{border-top-color:var(--blue)}.stat.cg{border-top-color:var(--green)}.stat.cr{border-top-color:var(--accent)}.stat.cy{border-top-color:var(--yellow)}.stat.cp{border-top-color:var(--purple)}.stat.co{border-top-color:var(--orange)}.stat.ct{border-top-color:var(--teal)}
.sv{font-size:26px;font-weight:800;line-height:1.1}
.cb .sv{color:var(--blue)}.cg .sv{color:var(--green)}.cr .sv{color:var(--accent)}.cy .sv{color:var(--yellow)}.cp .sv{color:var(--purple)}.co .sv{color:var(--orange)}.ct .sv{color:var(--teal)}
.sl{font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:4px}
.ss{font-size:11px;color:var(--muted);margin-top:3px}
.card{background:var(--s1);border:1px solid var(--border);border-radius:9px;overflow:hidden;margin-bottom:14px}
.ch{padding:11px 14px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:8px;flex-wrap:wrap}
.ct{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1.5px;color:var(--muted)}
.cb2{padding:14px}
.two{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:14px}
.tbl-w{overflow-x:auto}
table{width:100%;border-collapse:collapse;min-width:480px}
th{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:1px;color:var(--muted);padding:9px 13px;text-align:left;background:var(--s2)}
td{padding:10px 13px;font-size:12px;border-bottom:1px solid var(--border);vertical-align:middle}
tr:last-child td{border-bottom:none}
tbody tr:hover td{background:rgba(255,255,255,.015)}
.badge{display:inline-block;padding:2px 7px;border-radius:20px;font-size:10px;font-weight:700;letter-spacing:.5px;text-transform:uppercase}
.bg{background:rgba(45,198,83,.15);color:var(--green)}.by{background:rgba(255,209,102,.15);color:var(--yellow)}.br{background:rgba(230,57,70,.15);color:var(--accent)}.bb{background:rgba(76,201,240,.15);color:var(--blue)}.bp{background:rgba(155,93,229,.15);color:var(--purple)}.bt{background:rgba(6,214,160,.15);color:var(--teal)}
.dot{width:8px;height:8px;border-radius:50%;display:inline-block;flex-shrink:0}
.faixa-branca{background:#ddd}.faixa-azul{background:#4cc9f0}.faixa-roxa{background:#9b5de5}.faixa-marrom{background:#a0522d}.faixa-preta{background:#444;border:1px solid #666}
.fbadge{display:inline-flex;align-items:center;gap:5px;padding:3px 8px;border-radius:4px;font-size:11px;font-weight:600}
.fb-branca{background:rgba(240,240,240,.1);color:#ddd}.fb-azul{background:rgba(76,201,240,.15);color:var(--blue)}.fb-roxa{background:rgba(155,93,229,.15);color:var(--purple)}.fb-marrom{background:rgba(160,82,45,.2);color:#c8845a}.fb-preta{background:rgba(255,255,255,.06);color:#aaa}
.av{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;flex-shrink:0}
.av-branca{background:rgba(240,240,240,.1);color:#ccc}.av-azul{background:rgba(76,201,240,.15);color:var(--blue)}.av-roxa{background:rgba(155,93,229,.15);color:var(--purple)}.av-marrom{background:rgba(160,82,45,.2);color:#c8845a}.av-preta{background:rgba(255,255,255,.06);color:#999}
.si{background:var(--s2);border:1px solid var(--border);border-radius:5px;padding:7px 10px;color:var(--white);font-size:12px;outline:none;transition:border-color .15s;font-family:inherit;width:100%}
.si:focus{border-color:rgba(230,57,70,.45)}.si::placeholder{color:var(--muted)}
select.si option{background:var(--s2)}
.fg{display:flex;flex-direction:column;gap:4px}
label{font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:1.5px;color:var(--muted)}
.fg-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fg.full{grid-column:1/-1}
.pills{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:12px}
.pill{padding:4px 11px;border-radius:20px;border:1px solid var(--border);background:transparent;color:var(--muted);font-size:11px;cursor:pointer;transition:all .15s}
.pill:hover{color:var(--white)}.pill.on{background:var(--accent);border-color:var(--accent);color:#fff}
.pp{padding:4px 10px;border-radius:20px;border:1px solid var(--border);background:transparent;color:var(--muted);font-size:11px;cursor:pointer;transition:all .15s}
.pp:hover{color:var(--white)}.pp.on{background:rgba(76,201,240,.15);border-color:var(--blue);color:var(--blue)}
.tab-p{padding:5px 11px;border-radius:5px;border:1px solid var(--border);background:transparent;color:var(--muted);font-size:11px;cursor:pointer;transition:all .15s}
.tab-p:hover{color:var(--white)}.tab-p.on{background:rgba(255,255,255,.07);color:var(--white);border-color:rgba(255,255,255,.15)}
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.8);z-index:200;display:none;align-items:center;justify-content:center;backdrop-filter:blur(4px)}
.overlay.open{display:flex}
.modal{background:var(--s1);border:1px solid var(--border);border-radius:12px;width:500px;max-width:calc(100vw - 20px);padding:22px;animation:mIn .18s ease;max-height:92vh;overflow-y:auto}
.modal-lg{width:680px}
@keyframes mIn{from{opacity:0;transform:scale(.96) translateY(6px)}to{opacity:1;transform:scale(1) translateY(0)}}
.mh{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.mh h2{font-size:14px;font-weight:800;letter-spacing:1px}
.mx{background:none;border:none;color:var(--muted);cursor:pointer;font-size:17px}.mx:hover{color:var(--white)}
.mfoot{display:flex;gap:7px;justify-content:flex-end;margin-top:14px}
.toast{position:fixed;bottom:16px;right:16px;background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:9px 14px;font-size:12px;z-index:400;transform:translateY(60px);opacity:0;transition:all .25s;display:flex;align-items:center;gap:8px;box-shadow:0 8px 28px rgba(0,0,0,.4);pointer-events:none}
.toast.show{transform:translateY(0);opacity:1}
.empty{text-align:center;padding:36px 16px;color:var(--muted)}
.act{display:flex;gap:4px;flex-wrap:wrap}
.ab{background:transparent;border:1px solid var(--border);color:var(--muted);padding:4px 8px;border-radius:4px;cursor:pointer;font-size:11px;transition:all .15s}
.ab:hover{color:var(--white);border-color:rgba(255,255,255,.2)}
.ab.danger:hover{color:var(--accent);border-color:var(--accent)}
.ab.ok:hover{color:var(--green);border-color:var(--green)}
.ab.info:hover{color:var(--blue);border-color:var(--blue)}
.wa-btn{display:inline-flex;align-items:center;gap:4px;padding:5px 10px;background:#25D366;color:#000;border:none;border-radius:5px;cursor:pointer;font-size:11px;font-weight:700;transition:all .15s;text-decoration:none;white-space:nowrap}
.wa-btn:hover{background:#1dbd57;transform:translateY(-1px)}
.bar-w{width:55px;height:3px;background:rgba(76,201,240,.1);border-radius:2px;overflow:hidden}
.bar-f{height:100%;background:var(--blue);border-radius:2px}.bar-g{height:100%;background:var(--green);border-radius:2px}
.msg-box{background:var(--s2);border:1px solid var(--border);border-radius:7px;padding:12px;font-size:12px;line-height:1.65;white-space:pre-wrap}
.hist-item{display:flex;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)}
.hist-item:last-child{border-bottom:none}
.date-nav{display:flex;align-items:center;gap:7px}
.dn{background:var(--s2);border:1px solid var(--border);color:var(--white);padding:4px 10px;border-radius:5px;cursor:pointer;font-size:13px}
.dlbl{font-size:12px;color:var(--blue);min-width:120px;text-align:center;font-family:monospace}
.chk{width:25px;height:25px;border-radius:50%;border:2px solid var(--border);background:transparent;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:11px;transition:all .18s;flex-shrink:0}
.chk.on{background:var(--green);border-color:var(--green);color:#000}
.att{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-bottom:1px solid var(--border)}
.att:last-child{border-bottom:none}.att:hover{background:rgba(255,255,255,.015)}
.att-l{display:flex;align-items:center;gap:9px}
.qr-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:11px}
.stock-card{background:var(--s1);border:1px solid var(--border);border-radius:9px;padding:14px;transition:transform .18s}
.stock-card:hover{transform:translateY(-2px)}
.stock-img{width:100%;height:80px;background:var(--s2);border-radius:5px;display:flex;align-items:center;justify-content:center;font-size:28px;margin-bottom:10px}
.prog-bar{height:5px;background:var(--s3);border-radius:3px;overflow:hidden;margin-top:5px}
.prog-fill{height:100%;border-radius:3px;transition:width .4s}
.kpi-row{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:10px;margin-bottom:14px}
.kpi{background:var(--s2);border-radius:7px;padding:11px;text-align:center}
.kpi-val{font-size:22px;font-weight:800}.kpi-lbl{font-size:10px;color:var(--muted);margin-top:3px}
.sec-title{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:2px;color:var(--muted);margin:18px 0 10px;display:flex;align-items:center;gap:8px}
.sec-title::after{content:'';flex:1;height:1px;background:var(--border)}
.alert{padding:10px 14px;border-radius:7px;font-size:12px;margin-bottom:12px;display:flex;align-items:flex-start;gap:8px}
.alert-warn{background:rgba(255,209,102,.08);border:1px solid rgba(255,209,102,.2);color:var(--yellow)}
.alert-info{background:rgba(76,201,240,.08);border:1px solid rgba(76,201,240,.2);color:var(--blue)}
.alert-success{background:rgba(45,198,83,.08);border:1px solid rgba(45,198,83,.2);color:var(--green)}
.notif-item{display:flex;align-items:center;justify-content:space-between;padding:11px 14px;border-bottom:1px solid var(--border);gap:8px}
.notif-item:last-child{border-bottom:none}
@media(max-width:1100px){.topbar-nav{display:none}.hamburger{display:block}.g5,.g4{grid-template-columns:1fr 1fr}.g3{grid-template-columns:1fr 1fr}.two{grid-template-columns:1fr}}
@media(max-width:540px){.g5,.g4,.g3,.g2{grid-template-columns:1fr 1fr}.fg-grid{grid-template-columns:1fr}.wrap{padding:60px 10px 30px}}
@media print{.topbar,.btn,.act,.pills,.wa-btn,.chk,.hamburger,.mob-menu,.btn-row{display:none!important}.wrap{padding:14px}body{background:#fff;color:#000}.card,.stat,.kpi{background:#fff;border:1px solid #ddd}th{background:#f0f0f0}}
</style>
</head>
<body>

<nav class="topbar">
  <div class="logo">BJJ<span>MGR</span></div>
  <div class="topbar-nav">
    <button class="tb on"  onclick="nav('dashboard',this)">⬡ Dashboard</button>
    <button class="tb"     onclick="nav('financeiro',this)">💰 Financeiro</button>
    <button class="tb"     onclick="nav('alunos',this)">◉ Alunos</button>
    <button class="tb"     onclick="nav('graduacoes',this)">🥋 Graduações</button>
    <button class="tb"     onclick="nav('turmas',this)">📅 Turmas</button>
    <button class="tb"     onclick="nav('presenca',this)">◎ Presença</button>
    <button class="tb"     onclick="nav('estoque',this)">📦 Estoque</button>
    <button class="tb"     onclick="nav('pagamentos',this)">◈ Pgtos</button>
    <button class="tb"     onclick="nav('cobrancas',this)">💬 Cobranças</button>
    <button class="tb"     onclick="nav('notificacoes',this)">🔔 Notif.</button>
    <button class="tb"     onclick="nav('relatorio',this)">▤ Relatório</button>
    <button class="tb"     onclick="nav('configuracoes',this)">⚙ Config</button>
  </div>
  <div class="topbar-right">
    <button class="btn btn-red btn-sm" onclick="openModalAluno()">+ Aluno</button>
    <button class="hamburger" id="hamburger-btn" onclick="toggleMenu()">☰</button>
  </div>
</nav>

<div class="mob-menu" id="mob-menu">
  <button class="mob-tb on" onclick="navM('dashboard',this)">⬡ Dashboard</button>
  <button class="mob-tb"    onclick="navM('financeiro',this)">💰 Financeiro</button>
  <button class="mob-tb"    onclick="navM('alunos',this)">◉ Alunos</button>
  <button class="mob-tb"    onclick="navM('graduacoes',this)">🥋 Graduações</button>
  <button class="mob-tb"    onclick="navM('turmas',this)">📅 Turmas</button>
  <button class="mob-tb"    onclick="navM('presenca',this)">◎ Presença</button>
  <button class="mob-tb"    onclick="navM('estoque',this)">📦 Estoque</button>
  <button class="mob-tb"    onclick="navM('pagamentos',this)">◈ Pagamentos</button>
  <button class="mob-tb"    onclick="navM('cobrancas',this)">💬 Cobranças</button>
  <button class="mob-tb"    onclick="navM('notificacoes',this)">🔔 Notificações</button>
  <button class="mob-tb"    onclick="navM('relatorio',this)">▤ Relatório</button>
  <button class="mob-tb"    onclick="navM('configuracoes',this)">⚙ Configurações</button>
</div>

<div class="wrap">

<!-- DASHBOARD -->
<div class="page on" id="page-dashboard">
  <div class="ph"><div><h1>Dashboard</h1><p id="dash-date"></p></div>
    <div class="btn-row"><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button><button class="btn btn-red" onclick="openModalAluno()">+ Novo Aluno</button></div>
  </div>
  <div class="stats-grid g5">
    <div class="stat cg"><div class="sl">Receita Mês</div><div class="sv" id="d-recmes">R$0</div><div class="ss" id="d-recmes-s"></div></div>
    <div class="stat cr"><div class="sl">Despesas Mês</div><div class="sv" id="d-despmes">R$0</div><div class="ss" id="d-despmes-s"></div></div>
    <div class="stat cb"><div class="sl">Total Alunos</div><div class="sv" id="d-total">0</div><div class="ss" id="d-total-s"></div></div>
    <div class="stat cy"><div class="sl">Inadimplentes</div><div class="sv" id="d-inad">0</div><div class="ss" id="d-inad-s"></div></div>
    <div class="stat cp"><div class="sl">Presença Hoje</div><div class="sv" id="d-pres">0</div><div class="ss">check-ins</div></div>
  </div>
  <div class="kpi-row">
    <div class="kpi"><div class="kpi-val" id="d-ticket" style="color:var(--green)">R$0</div><div class="kpi-lbl">Ticket Médio</div></div>
    <div class="kpi"><div class="kpi-val" id="d-churn" style="color:var(--accent)">0%</div><div class="kpi-lbl">Churn Estimado</div></div>
    <div class="kpi"><div class="kpi-val" id="d-estoque-alerta" style="color:var(--yellow)">0</div><div class="kpi-lbl">Alertas Estoque</div></div>
    <div class="kpi"><div class="kpi-val" id="d-grad-pend" style="color:var(--purple)">0</div><div class="kpi-lbl">Graduações Pend.</div></div>
    <div class="kpi"><div class="kpi-val" id="d-projecao" style="color:var(--blue)">R$0</div><div class="kpi-lbl">Projeção 30d</div></div>
    <div class="kpi"><div class="kpi-val" id="d-resultado" style="color:var(--teal)">R$0</div><div class="kpi-lbl">Resultado Mês</div></div>
  </div>
  <div class="two">
    <div class="card"><div class="ch"><span class="ct">Vencimentos Próximos</span></div><div id="d-vencs" style="max-height:200px;overflow-y:auto"></div></div>
    <div class="card"><div class="ch"><span class="ct">Alertas</span></div><div id="d-alertas" style="max-height:200px;overflow-y:auto"></div></div>
  </div>
  <div class="two">
    <div class="card"><div class="ch"><span class="ct">Top Presenças</span></div><div id="d-top-pres" class="cb2"></div></div>
    <div class="card"><div class="ch"><span class="ct">Estoque Crítico</span></div><div id="d-stock-alerts" style="max-height:200px;overflow-y:auto"></div></div>
  </div>
</div>

<!-- FINANCEIRO -->
<div class="page" id="page-financeiro">
  <div class="ph"><div><h1>Financeiro</h1><p id="fin-date"></p></div>
    <div class="btn-row"><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button><button class="btn btn-green btn-sm" onclick="openModalRec()">+ Receita</button><button class="btn btn-red" onclick="openModalDesp()">+ Despesa</button></div>
  </div>
  <div style="display:flex;gap:5px;flex-wrap:wrap;margin-bottom:14px" id="period-bar">
    <button class="pp on" onclick="setPeriod('dia',this)">Hoje</button>
    <button class="pp" onclick="setPeriod('semana',this)">Semana</button>
    <button class="pp" onclick="setPeriod('mes',this)">Mês</button>
    <button class="pp" onclick="setPeriod('trimestre',this)">Trimestre</button>
    <button class="pp" onclick="setPeriod('semestre',this)">Semestre</button>
    <button class="pp" onclick="setPeriod('ano',this)">Ano</button>
  </div>
  <div class="stats-grid g5">
    <div class="stat cg"><div class="sl">Receita</div><div class="sv" id="k-rec">R$0</div><div class="ss" id="k-rec-s"></div></div>
    <div class="stat cr"><div class="sl">Despesas</div><div class="sv" id="k-desp">R$0</div><div class="ss" id="k-desp-s"></div></div>
    <div class="stat cb"><div class="sl">Resultado</div><div class="sv" id="k-res">R$0</div><div class="ss">líquido</div></div>
    <div class="stat cy"><div class="sl">Alunos Ativos</div><div class="sv" id="k-al">0</div><div class="ss" id="k-al-s"></div></div>
    <div class="stat cp"><div class="sl">Inadimplentes</div><div class="sv" id="k-in">0</div><div class="ss" id="k-in-s"></div></div>
  </div>
  <div class="two">
    <div class="card">
      <div class="ch"><span class="ct">Receita × Despesas</span><span id="chart-lbl" style="font-size:11px;color:var(--muted)"></span></div>
      <div style="padding:12px;position:relative;height:210px"><canvas id="chart-main"></canvas></div>
      <div style="display:flex;gap:12px;padding:0 12px 10px;font-size:11px;color:var(--muted)">
        <span style="display:flex;align-items:center;gap:3px"><span style="width:9px;height:9px;border-radius:2px;background:#2dc653"></span>Receita</span>
        <span style="display:flex;align-items:center;gap:3px"><span style="width:9px;height:9px;border-radius:2px;background:#e63946"></span>Despesas</span>
      </div>
    </div>
    <div class="card">
      <div class="ch"><span class="ct" id="pizza-title">Distribuição</span>
        <div style="display:flex;gap:4px"><button class="tab-p on" id="pz-r" onclick="setPizzaTab('rec')">Receitas</button><button class="tab-p" id="pz-d" onclick="setPizzaTab('desp')">Despesas</button></div>
      </div>
      <div style="position:relative;height:180px;padding:10px"><canvas id="chart-pizza"></canvas></div>
      <div id="pizza-legend" style="padding:0 12px 10px;display:flex;flex-wrap:wrap;gap:6px;font-size:10px;color:var(--muted)"></div>
    </div>
  </div>
  <div class="sec-title">DRE Simplificado — Mês Atual</div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Categoria</th><th>Valor</th><th>% Total</th></tr></thead><tbody id="tb-dre"></tbody></table></div></div>
  <div class="card">
    <div class="ch">
      <div style="display:flex;gap:5px"><button class="tab-p on" id="tab-rec-btn" onclick="setFinTab('rec')">Receitas</button><button class="tab-p" id="tab-desp-btn" onclick="setFinTab('desp')">Despesas</button></div>
      <div style="display:flex;gap:7px;align-items:center;flex-wrap:wrap"><span id="tab-total-lbl" style="font-size:11px;color:var(--muted)"></span><button id="tab-add-btn" class="btn btn-green btn-sm" onclick="openModalRec()">+ Receita</button></div>
    </div>
    <div style="padding:8px 12px 2px;display:flex;gap:4px;flex-wrap:wrap" id="cat-filter-row"></div>
    <div id="tab-rec-tbl" class="tbl-w"><table><thead><tr><th>Descrição</th><th>Categoria</th><th>Valor</th><th>Data</th><th>Forma</th><th>Aluno</th><th>Ações</th></tr></thead><tbody id="tb-rec"></tbody></table></div>
    <div id="tab-desp-tbl" class="tbl-w" style="display:none"><table><thead><tr><th>Descrição</th><th>Categoria</th><th>Valor</th><th>Data</th><th>Recorr.</th><th>Forma</th><th>Ações</th></tr></thead><tbody id="tb-desp"></tbody></table></div>
  </div>
</div>

<!-- ALUNOS -->
<div class="page" id="page-alunos">
  <div class="ph"><div><h1>Alunos</h1><p id="al-sub"></p></div><div class="btn-row"><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button><button class="btn btn-red" onclick="openModalAluno()">+ Novo Aluno</button></div></div>
  <div class="card">
    <div class="ch">
      <input class="si" style="width:200px" type="text" placeholder="🔍 Buscar..." oninput="buscar(this.value)">
      <div style="display:flex;gap:5px;flex-wrap:wrap">
        <button class="pp on" onclick="filtAl('todos',this)">Todos</button>
        <button class="pp" onclick="filtAl('ativo',this)">Ativos</button>
        <button class="pp" onclick="filtAl('inativo',this)">Inativos</button>
        <select class="si" style="width:130px" onchange="filtFaixa(this.value)"><option value="">Todas faixas</option><option>branca</option><option>azul</option><option>roxa</option><option>marrom</option><option>preta</option></select>
      </div>
    </div>
    <div class="tbl-w"><table><thead><tr><th>Aluno</th><th>CPF</th><th>Turma</th><th>Faixa</th><th>Plano</th><th>Vencimento</th><th>Status</th><th>Ações</th></tr></thead><tbody id="tb-al"></tbody></table></div>
  </div>
</div>

<!-- GRADUAÇÕES -->
<div class="page" id="page-graduacoes">
  <div class="ph"><div><h1>Graduações</h1><p>Histórico e cerimônias</p></div>
    <div class="btn-row"><button class="btn btn-purple" onclick="openModalGrad()">+ Registrar</button><button class="btn btn-ghost btn-sm" onclick="openModalCerimonia()">📋 Cerimônia</button></div>
  </div>
  <div class="sec-title">Prontos para Graduar</div>
  <div id="grad-prontos"></div>
  <div class="sec-title">Histórico</div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Aluno</th><th>De</th><th>Para</th><th>Data</th><th>Professor</th><th>Cerimônia</th></tr></thead><tbody id="tb-grad"></tbody></table></div></div>
  <div class="sec-title">Cerimônias</div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Nome</th><th>Data</th><th>Alunos</th><th>Ação</th></tr></thead><tbody id="tb-cerim"></tbody></table></div></div>
</div>

<!-- TURMAS -->
<div class="page" id="page-turmas">
  <div class="ph"><div><h1>Turmas & Horários</h1><p>Grade de aulas</p></div><button class="btn btn-blue" onclick="openModalTurma()">+ Nova Turma</button></div>
  <div id="turmas-grid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:12px"></div>
</div>

<!-- PRESENÇA -->
<div class="page" id="page-presenca">
  <div class="ph"><div><h1>Presença</h1><p id="pres-sub"></p></div>
    <div class="btn-row">
      <select class="si" style="width:170px" id="pres-turma-sel" onchange="rPresenca()"><option value="">Todos os alunos</option></select>
      <button class="btn btn-ghost btn-sm" onclick="toggleManual()">✎ Manual</button>
      <button class="btn btn-green" onclick="salvarChamada()">✓ Salvar</button>
    </div>
  </div>
  <div id="manual-block" style="display:none">
    <div class="card" style="margin-bottom:12px">
      <div class="ch"><span class="ct">Lançamento Manual</span></div>
      <div class="cb2">
        <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;flex-wrap:wrap">
          <div class="fg" style="flex-direction:row;align-items:center;gap:7px"><label style="white-space:nowrap">Data:</label><input type="date" id="m-date" class="si" style="width:150px" onchange="renderManual()"></div>
          <button class="btn btn-blue btn-sm" onclick="salvarManual()">✓ Salvar</button>
        </div>
        <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(185px,1fr));gap:6px" id="manual-list"></div>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="ch" style="justify-content:space-between">
      <div class="date-nav"><button class="dn" onclick="chgDate(-1)">‹</button><div class="dlbl" id="pres-dlbl"></div><button class="dn" onclick="chgDate(1)">›</button></div>
      <span id="pres-cnt" style="font-size:11px;color:var(--muted)"></span>
    </div>
    <div id="chamada-list"></div>
  </div>
</div>

<!-- ESTOQUE -->
<div class="page" id="page-estoque">
  <div class="ph"><div><h1>Estoque</h1><p>Produtos e insumos</p></div>
    <div class="btn-row"><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button><button class="btn btn-orange" onclick="openModalProd()">+ Produto</button><button class="btn btn-ghost btn-sm" onclick="openModalMov()">↕ Movimentação</button></div>
  </div>
  <div class="stats-grid g4">
    <div class="stat cb"><div class="sl">Produtos</div><div class="sv" id="e-total">0</div><div class="ss">cadastrados</div></div>
    <div class="stat cy"><div class="sl">Alertas</div><div class="sv" id="e-alertas">0</div><div class="ss">estoque mínimo</div></div>
    <div class="stat cg"><div class="sl">Valor Custo</div><div class="sv" id="e-valor">R$0</div><div class="ss">em estoque</div></div>
    <div class="stat co"><div class="sl">Potencial Venda</div><div class="sv" id="e-potencial">R$0</div><div class="ss">a preço de venda</div></div>
  </div>
  <div class="pills" id="est-pills">
    <button class="pill on" onclick="filtEst('todos',this)">Todos</button>
    <button class="pill" onclick="filtEst('Kimono',this)">Kimono</button>
    <button class="pill" onclick="filtEst('Faixa',this)">Faixa</button>
    <button class="pill" onclick="filtEst('Rashguard',this)">Rashguard</button>
    <button class="pill" onclick="filtEst('Camiseta',this)">Camiseta</button>
    <button class="pill" onclick="filtEst('Bebida',this)">Bebida</button>
    <button class="pill" onclick="filtEst('Insumo',this)">Insumo</button>
    <button class="pill" onclick="filtEst('Outros',this)">Outros</button>
  </div>
  <div id="estoque-grid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:11px"></div>
  <div class="sec-title">Movimentações</div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Produto</th><th>Tipo</th><th>Qtd</th><th>Data</th><th>Motivo</th><th>Resp.</th></tr></thead><tbody id="tb-mov"></tbody></table></div></div>
</div>

<!-- PAGAMENTOS -->
<div class="page" id="page-pagamentos">
  <div class="ph"><div><h1>Pagamentos</h1><p id="pag-sub"></p></div><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button></div>
  <div class="pills">
    <button class="pill on" onclick="filtPag('todos',this)">Todos</button>
    <button class="pill" onclick="filtPag('em-dia',this)">✓ Em Dia</button>
    <button class="pill" onclick="filtPag('vence-hoje',this)">⚡ Vence Hoje</button>
    <button class="pill" onclick="filtPag('atrasado',this)">✗ Atrasados</button>
  </div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Aluno</th><th>Plano</th><th>Valor</th><th>Vencimento</th><th>Status</th><th>Ação</th></tr></thead><tbody id="tb-pag"></tbody></table></div></div>
</div>

<!-- COBRANÇAS -->
<div class="page" id="page-cobrancas">
  <div class="ph"><div><h1>Cobranças</h1><p>Via WhatsApp</p></div><button class="btn btn-green" onclick="envTodos()">📲 Enviar p/ Todos</button></div>
  <div class="card"><div class="ch"><span class="ct">Mensagem Padrão</span><button class="btn btn-ghost btn-sm" onclick="editMsg('cobr')">✎ Editar</button></div><div class="cb2"><div class="msg-box" id="msg-cobr-preview"></div></div></div>
  <div class="card" id="wa-lista"></div>
</div>

<!-- NOTIFICAÇÕES -->
<div class="page" id="page-notificacoes">
  <div class="ph"><div><h1>Notificações</h1><p>Régua automática</p></div></div>
  <div class="alert alert-info">💡 Mensagens geradas automaticamente com base em vencimentos, aniversários e graduações.</div>
  <div class="sec-title">Régua de Cobrança</div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Gatilho</th><th>Preview</th><th>Status</th><th>Ação</th></tr></thead><tbody id="tb-regua"></tbody></table></div></div>
  <div class="sec-title">Fila de Envio</div>
  <div class="card"><div id="notif-fila"></div></div>
  <div class="sec-title">Templates</div>
  <div id="templates-list"></div>
</div>

<!-- RELATÓRIO -->
<div class="page" id="page-relatorio">
  <div class="ph"><div><h1>Relatório</h1><p id="rel-sub"></p></div><button class="btn btn-ghost btn-sm" onclick="window.print()">⬇ PDF</button></div>
  <div style="display:flex;align-items:center;gap:8px;margin-bottom:14px">
    <div class="date-nav"><button class="dn" onclick="chgMes(-1)">‹</button><div class="dlbl" id="rel-mlbl" style="min-width:170px;font-size:14px;font-weight:700;color:var(--white)"></div><button class="dn" onclick="chgMes(1)">›</button></div>
  </div>
  <div class="stats-grid g3">
    <div class="stat cg"><div class="sl">Receita em Dia</div><div class="sv" id="r-rec">R$0</div><div class="ss" id="r-rec-s"></div></div>
    <div class="stat cb"><div class="sl">Presenças</div><div class="sv" id="r-pres">0</div><div class="ss">no mês</div></div>
    <div class="stat cr"><div class="sl">Inadimplência</div><div class="sv" id="r-inad">0%</div><div class="ss" id="r-inad-s"></div></div>
  </div>
  <div class="card"><div class="tbl-w"><table><thead><tr><th>Aluno</th><th>Faixa</th><th>Plano</th><th>Valor</th><th>Status</th><th>Presenças</th><th>Graduar?</th></tr></thead><tbody id="tb-rel"></tbody></table></div></div>
</div>

<!-- CONFIGURAÇÕES -->
<div class="page" id="page-configuracoes">
  <div class="ph"><div><h1>Configurações</h1></div></div>
  <div class="sec-title">Dados da Academia</div>
  <div class="card cb2">
    <div class="fg-grid">
      <div class="fg full"><label>Nome da Academia</label><input id="cfg-nome" class="si" type="text"></div>
      <div class="fg"><label>Professor Principal</label><input id="cfg-prof" class="si" type="text"></div>
      <div class="fg"><label>Telefone</label><input id="cfg-tel" class="si" type="text"></div>
      <div class="fg"><label>CNPJ</label><input id="cfg-cnpj" class="si" type="text"></div>
      <div class="fg full"><label>Endereço</label><input id="cfg-end" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-green" onclick="salvarConfig()">✓ Salvar</button></div>
  </div>
  <div class="sec-title">Backup & Dados</div>
  <div class="card cb2">
    <div style="display:flex;gap:8px;flex-wrap:wrap">
      <button class="btn btn-blue" onclick="exportarDados()">⬇ Exportar JSON</button>
      <button class="btn btn-ghost" onclick="document.getElementById('import-file').click()">⬆ Importar JSON</button>
      <input type="file" id="import-file" accept=".json" style="display:none" onchange="importarDados(event)">
      <button class="btn btn-ghost btn-sm" onclick="limparDados()">🗑 Limpar Dados</button>
    </div>
    <div class="alert alert-warn" style="margin-top:12px">⚠ Exporte um backup regularmente. Dados armazenados no navegador.</div>
  </div>
  <div class="sec-title">Usuários</div>
  <div class="card cb2"><div id="usuarios-lista"></div><div class="mfoot"><button class="btn btn-purple btn-sm" onclick="openModalUsuario()">+ Usuário</button></div></div>
</div>
</div>

<!-- MODAIS -->
<div class="overlay" id="m-aluno" onclick="ovC(event,'m-aluno')">
  <div class="modal">
    <div class="mh"><h2 id="m-al-t">NOVO ALUNO</h2><button class="mx" onclick="closeM('m-aluno')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Nome *</label><input id="f-nome" class="si" type="text"></div>
      <div class="fg"><label>CPF</label><input id="f-cpf" class="si" type="text" placeholder="000.000.000-00" oninput="fmtCPF(this)"></div>
      <div class="fg"><label>Nascimento</label><input id="f-nasc" class="si" type="date"></div>
      <div class="fg"><label>Telefone</label><input id="f-tel" class="si" type="text"></div>
      <div class="fg"><label>Email</label><input id="f-email" class="si" type="email"></div>
      <div class="fg full"><label>Endereço</label><input id="f-end" class="si" type="text"></div>
      <div class="fg"><label>Cidade</label><input id="f-cid" class="si" type="text"></div>
      <div class="fg"><label>CEP</label><input id="f-cep" class="si" type="text" oninput="fmtCEP(this)"></div>
      <div class="fg"><label>Contato Emergência</label><input id="f-emerg" class="si" type="text"></div>
      <div class="fg"><label>Condição de Saúde</label><input id="f-saude" class="si" type="text"></div>
      <div class="fg"><label>Faixa</label><select id="f-faixa" class="si"><option value="branca">Branca</option><option value="azul">Azul</option><option value="roxa">Roxa</option><option value="marrom">Marrom</option><option value="preta">Preta</option></select></div>
      <div class="fg"><label>Grau</label><select id="f-grau" class="si"><option value="0">Sem grau</option><option value="1">1º</option><option value="2">2º</option><option value="3">3º</option><option value="4">4º</option></select></div>
      <div class="fg"><label>Turma</label><select id="f-turma" class="si"><option value="">— Nenhuma —</option></select></div>
      <div class="fg"><label>Status</label><select id="f-status" class="si"><option value="ativo">Ativo</option><option value="inativo">Inativo</option><option value="licenca">Licença</option></select></div>
      <div class="fg"><label>Plano</label><select id="f-plano" class="si"><option>Mensal</option><option>Trimestral</option><option>Semestral</option><option>Anual</option></select></div>
      <div class="fg"><label>Valor (R$)</label><input id="f-val" class="si" type="number"></div>
      <div class="fg full"><label>Vencimento *</label><input id="f-venc" class="si" type="date"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-aluno')">Cancelar</button><button class="btn btn-red" onclick="salvarAluno()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-grad" onclick="ovC(event,'m-grad')">
  <div class="modal">
    <div class="mh"><h2>REGISTRAR GRADUAÇÃO</h2><button class="mx" onclick="closeM('m-grad')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Aluno *</label><select id="g-aluno" class="si"><option value="">Selecione...</option></select></div>
      <div class="fg"><label>Faixa Atual</label><select id="g-de" class="si"><option value="branca">Branca</option><option value="azul">Azul</option><option value="roxa">Roxa</option><option value="marrom">Marrom</option><option value="preta">Preta</option></select></div>
      <div class="fg"><label>Grau Atual</label><select id="g-grau-de" class="si"><option value="0">Sem grau</option><option value="1">1º</option><option value="2">2º</option><option value="3">3º</option><option value="4">4º</option></select></div>
      <div class="fg"><label>Nova Faixa *</label><select id="g-para" class="si"><option value="branca">Branca</option><option value="azul">Azul</option><option value="roxa">Roxa</option><option value="marrom">Marrom</option><option value="preta">Preta</option></select></div>
      <div class="fg"><label>Novo Grau</label><select id="g-grau-para" class="si"><option value="0">Sem grau</option><option value="1">1º</option><option value="2">2º</option><option value="3">3º</option><option value="4">4º</option></select></div>
      <div class="fg"><label>Data</label><input id="g-data" class="si" type="date"></div>
      <div class="fg"><label>Professor</label><input id="g-prof" class="si" type="text"></div>
      <div class="fg"><label>Cerimônia</label><select id="g-cerim" class="si"><option value="">— Avulsa —</option></select></div>
      <div class="fg full"><label>Observação</label><input id="g-obs" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-grad')">Cancelar</button><button class="btn btn-purple" onclick="salvarGrad()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-cerim" onclick="ovC(event,'m-cerim')">
  <div class="modal">
    <div class="mh"><h2>NOVA CERIMÔNIA</h2><button class="mx" onclick="closeM('m-cerim')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Nome *</label><input id="ce-nome" class="si" type="text"></div>
      <div class="fg"><label>Data *</label><input id="ce-data" class="si" type="date"></div>
      <div class="fg"><label>Local</label><input id="ce-local" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-cerim')">Cancelar</button><button class="btn btn-purple" onclick="salvarCerim()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-turma" onclick="ovC(event,'m-turma')">
  <div class="modal">
    <div class="mh"><h2 id="m-tur-t">NOVA TURMA</h2><button class="mx" onclick="closeM('m-turma')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Nome *</label><input id="t-nome" class="si" type="text"></div>
      <div class="fg"><label>Professor</label><input id="t-prof" class="si" type="text"></div>
      <div class="fg"><label>Horário</label><input id="t-hora" class="si" type="text" placeholder="07:00–08:30"></div>
      <div class="fg full"><label>Dias da Semana</label>
        <div style="display:flex;gap:8px;flex-wrap:wrap;margin-top:4px" id="dias-checks">
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Seg"> Seg</label>
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Ter"> Ter</label>
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Qua"> Qua</label>
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Qui"> Qui</label>
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Sex"> Sex</label>
          <label style="display:flex;align-items:center;gap:4px;font-size:12px;text-transform:none;letter-spacing:0;color:var(--white);cursor:pointer"><input type="checkbox" value="Sáb"> Sáb</label>
        </div>
      </div>
      <div class="fg"><label>Vagas</label><input id="t-vagas" class="si" type="number"></div>
      <div class="fg"><label>Nível</label><select id="t-nivel" class="si"><option>Todas as faixas</option><option>Iniciante</option><option>Intermediário</option><option>Avançado</option><option>Kids</option></select></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-turma')">Cancelar</button><button class="btn btn-blue" onclick="salvarTurma()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-prod" onclick="ovC(event,'m-prod')">
  <div class="modal">
    <div class="mh"><h2 id="m-prod-t">NOVO PRODUTO</h2><button class="mx" onclick="closeM('m-prod')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Nome *</label><input id="p-nome" class="si" type="text"></div>
      <div class="fg"><label>Categoria</label><select id="p-cat" class="si"><option>Kimono</option><option>Faixa</option><option>Rashguard</option><option>Camiseta</option><option>Boné</option><option>Bebida</option><option>Insumo</option><option>Outros</option></select></div>
      <div class="fg"><label>SKU</label><input id="p-sku" class="si" type="text"></div>
      <div class="fg"><label>Tamanho</label><input id="p-tam" class="si" type="text"></div>
      <div class="fg"><label>Custo (R$)</label><input id="p-custo" class="si" type="number" step="0.01"></div>
      <div class="fg"><label>Preço Venda (R$)</label><input id="p-preco" class="si" type="number" step="0.01"></div>
      <div class="fg"><label>Qtd Inicial</label><input id="p-qtd" class="si" type="number"></div>
      <div class="fg"><label>Estoque Mínimo</label><input id="p-min" class="si" type="number"></div>
      <div class="fg full"><label>Emoji</label><input id="p-emoji" class="si" type="text" maxlength="2"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-prod')">Cancelar</button><button class="btn btn-orange" onclick="salvarProd()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-mov" onclick="ovC(event,'m-mov')">
  <div class="modal">
    <div class="mh"><h2>MOVIMENTAÇÃO</h2><button class="mx" onclick="closeM('m-mov')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Produto *</label><select id="mv-prod" class="si"><option value="">Selecione...</option></select></div>
      <div class="fg"><label>Tipo</label><select id="mv-tipo" class="si"><option value="entrada">Entrada</option><option value="saida">Saída (Venda)</option><option value="saida-uso">Saída (Uso Interno)</option><option value="ajuste">Ajuste</option></select></div>
      <div class="fg"><label>Quantidade *</label><input id="mv-qtd" class="si" type="number"></div>
      <div class="fg"><label>Data</label><input id="mv-data" class="si" type="date"></div>
      <div class="fg full"><label>Observação</label><input id="mv-obs" class="si" type="text"></div>
      <div class="fg"><label>Responsável</label><input id="mv-resp" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-mov')">Cancelar</button><button class="btn btn-orange" onclick="salvarMov()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-rec" onclick="ovC(event,'m-rec')">
  <div class="modal">
    <div class="mh"><h2 id="m-rec-t">NOVA RECEITA</h2><button class="mx" onclick="closeM('m-rec')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Descrição</label><input id="r-desc" class="si" type="text"></div>
      <div class="fg"><label>Categoria *</label><select id="r-cat" class="si"><option>Mensalidade Aluno</option><option>Kimono</option><option>Faixa</option><option>Bebidas</option><option>Camisetas</option><option>Bonés</option><option>Rashguard</option><option>Seminários</option><option>Graduação</option><option>Sublocação</option></select></div>
      <div class="fg"><label>Valor (R$) *</label><input id="r-val" class="si" type="number" step="0.01"></div>
      <div class="fg"><label>Data *</label><input id="r-data" class="si" type="date"></div>
      <div class="fg"><label>Forma Pgto</label><select id="r-forma" class="si"><option>Pix</option><option>Dinheiro</option><option>Cartão Débito</option><option>Cartão Crédito</option><option>Boleto</option><option>Transferência</option></select></div>
      <div class="fg"><label>Aluno</label><select id="r-aluno" class="si"><option value="">— Nenhum —</option></select></div>
      <div class="fg full"><label>Obs</label><input id="r-obs" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-rec')">Cancelar</button><button class="btn btn-green" onclick="salvarRec()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-desp" onclick="ovC(event,'m-desp')">
  <div class="modal">
    <div class="mh"><h2 id="m-desp-t">NOVA DESPESA</h2><button class="mx" onclick="closeM('m-desp')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Descrição</label><input id="d-desc" class="si" type="text"></div>
      <div class="fg"><label>Categoria *</label><select id="d-cat" class="si"><option>Aluguel</option><option>Contador</option><option>Luz</option><option>Água</option><option>IPTU</option><option>Telefone</option><option>Internet</option><option>Royalties Tetris</option><option>Material de Limpeza</option><option>Reembolso Compras</option><option>Manutenção</option><option>Aplicativo de Gestão</option><option>Impostos</option><option>Custos com Divulgação</option><option>Compra Material Revenda</option><option>Compra Material Aula</option><option>Introdução Dinheiro Sócios</option><option>Patrocínios</option><option>Taxa Maquininha</option></select></div>
      <div class="fg"><label>Valor (R$) *</label><input id="d-val" class="si" type="number" step="0.01"></div>
      <div class="fg"><label>Data *</label><input id="d-data" class="si" type="date"></div>
      <div class="fg"><label>Recorrente</label><select id="d-rec" class="si"><option value="nao">Não</option><option value="mensal">Mensal</option><option value="anual">Anual</option></select></div>
      <div class="fg"><label>Forma Pgto</label><select id="d-forma" class="si"><option>Pix</option><option>Dinheiro</option><option>Cartão Débito</option><option>Cartão Crédito</option><option>Boleto</option><option>Transferência</option></select></div>
      <div class="fg full"><label>Obs</label><input id="d-obs" class="si" type="text"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-desp')">Cancelar</button><button class="btn btn-red" onclick="salvarDesp()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-msg" onclick="ovC(event,'m-msg')">
  <div class="modal">
    <div class="mh"><h2>EDITAR MENSAGEM</h2><button class="mx" onclick="closeM('m-msg')">✕</button></div>
    <div class="fg" style="margin-bottom:10px"><label>Variáveis: {nome} {valor} {vencimento} {dias} {academia}</label><textarea id="msg-inp" class="si" rows="7"></textarea></div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-msg')">Cancelar</button><button class="btn btn-red" onclick="salvarMsgTpl()">Salvar</button></div>
  </div>
</div>

<div class="overlay" id="m-hist" onclick="ovC(event,'m-hist')">
  <div class="modal modal-lg">
    <div class="mh"><h2 id="m-hist-t">HISTÓRICO</h2><button class="mx" onclick="closeM('m-hist')">✕</button></div>
    <div id="m-hist-body" style="max-height:440px;overflow-y:auto"></div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-hist')">Fechar</button></div>
  </div>
</div>

<div class="overlay" id="m-usuario" onclick="ovC(event,'m-usuario')">
  <div class="modal">
    <div class="mh"><h2>NOVO USUÁRIO</h2><button class="mx" onclick="closeM('m-usuario')">✕</button></div>
    <div class="fg-grid">
      <div class="fg full"><label>Nome</label><input id="u-nome" class="si" type="text"></div>
      <div class="fg"><label>Perfil</label><select id="u-perfil" class="si"><option value="admin">Administrador</option><option value="professor">Professor</option><option value="recepcao">Recepção</option></select></div>
      <div class="fg"><label>Email</label><input id="u-email" class="si" type="email"></div>
    </div>
    <div class="mfoot"><button class="btn btn-ghost" onclick="closeM('m-usuario')">Cancelar</button><button class="btn btn-purple" onclick="salvarUsuario()">Salvar</button></div>
  </div>
</div>

<div class="toast" id="toast"><span id="t-ico">✓</span><span id="t-msg"></span></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
// ── CONSTANTES ──────────────────────────────────────
var CAT_REC=['Mensalidade Aluno','Kimono','Faixa','Bebidas','Camisetas','Bonés','Rashguard','Seminários','Graduação','Sublocação'];
var CAT_DESP=['Aluguel','Contador','Luz','Água','IPTU','Telefone','Internet','Royalties Tetris','Material de Limpeza','Reembolso Compras','Manutenção','Aplicativo de Gestão','Impostos','Custos com Divulgação','Compra Material Revenda','Compra Material Aula','Introdução Dinheiro Sócios','Patrocínios','Taxa Maquininha'];
var CR=['#2dc653','#4cc9f0','#ffd166','#f4a261','#9b5de5','#e63946','#3a86ff','#fb8500','#06d6a0','#ef476f'];
var CD=['#e63946','#f4a261','#ffd166','#4cc9f0','#9b5de5','#2dc653','#3a86ff','#fb8500','#06d6a0','#ef476f','#a8dadc','#457b9d','#e9c46a','#264653','#2a9d8f','#e76f51','#f72585','#7209b7','#560bad'];
var FAIXAS=['branca','azul','roxa','marrom','preta'];
var DIAS_MES={Mensal:1,Trimestral:3,Semestral:6,Anual:12};
var GRAD_CRIT={branca:{minMeses:3,minPres:30},azul:{minMeses:12,minPres:120},roxa:{minMeses:18,minPres:180},marrom:{minMeses:18,minPres:180},preta:{minMeses:24,minPres:240}};

// ── ESTADO ──────────────────────────────────────────
var alunos    = JSON.parse(localStorage.getItem('bjj_a')   || '[]');
var presencas = JSON.parse(localStorage.getItem('bjj_p')   || '{}');
var receitas  = JSON.parse(localStorage.getItem('bjj_r3')  || '[]');
var despesas  = JSON.parse(localStorage.getItem('bjj_d3')  || '[]');
var graduacoes= JSON.parse(localStorage.getItem('bjj_g')   || '[]');
var cerimonias= JSON.parse(localStorage.getItem('bjj_ce')  || '[]');
var turmas    = JSON.parse(localStorage.getItem('bjj_t')   || '[]');
var produtos  = JSON.parse(localStorage.getItem('bjj_pr')  || '[]');
var movEstoque= JSON.parse(localStorage.getItem('bjj_mv')  || '[]');
var usuarios  = JSON.parse(localStorage.getItem('bjj_us')  || '[]');
var cfg       = JSON.parse(localStorage.getItem('bjj_cfg') || '{"nome":"Academia BJJ","prof":"Professor","tel":"","cnpj":"","end":""}');
var msgTpl    = JSON.parse(localStorage.getItem('bjj_tpl') || 'null') || {
  cobr:'Olá {nome}! 👋\n\nSua mensalidade de *R$ {valor}* venceu em *{vencimento}*.\n\nRegularize para continuar treinando! 🥋',
  av7:'Olá {nome}! Sua mensalidade de *R$ {valor}* vence em 7 dias ({vencimento}). 📅',
  av3:'Olá {nome}! Sua mensalidade de *R$ {valor}* vence em 3 dias ({vencimento}). ⚡',
  venc:'Olá {nome}! Sua mensalidade de *R$ {valor}* vence hoje. Regularize! 💳',
  atraso:'Olá {nome}! Mensalidade em atraso há {dias} dias. Valor: *R$ {valor}*. ⚠️',
  aniv:'🎂 Feliz Aniversário, {nome}! A equipe da {academia} deseja tudo de bom!',
  boas:'Bem-vindo(a) à {academia}, {nome}! 🎉 Estamos felizes em ter você!'
};

var editAlId=null, editRecId=null, editDespId=null, editProdId=null, editTurmaId=null;
var pagFilt='todos', presDate=hoje(), relMes=hoje().slice(0,7);
var mTemp={}, cTemp={}, q='', alFilt='todos', alFaixa='';
var period='mes', pizzaTab='rec', finTab='rec';
var catRecFilt='todas', catDespFilt='todas', estCat='todos';
var chartMain=null, chartPizza=null;
var msgEditKey='cobr';

// ── SEED ────────────────────────────────────────────
(function(){
  if(alunos.length) return;
  var t=hoje(), y=t.slice(0,4), m=t.slice(0,7);
  function add(d,n){var x=new Date(d);x.setDate(x.getDate()+n);return x.toISOString().split('T')[0]}
  alunos=[
    {id:1,nome:'Carlos Mendes',cpf:'111.222.333-44',tel:'11991234567',email:'carlos@email.com',nasc:y+'-03-15',endereco:'Rua das Palmeiras, 120',cidade:'São Paulo',cep:'01310-100',emerg:'Maria — 11988880000',saude:'',faixa:'preta',grau:'2',turma:'1',status:'ativo',plano:'Mensal',valor:220,venc:add(t,-5)},
    {id:2,nome:'Ana Ferreira',cpf:'222.333.444-55',tel:'11982345678',email:'ana@email.com',nasc:y+'-07-22',endereco:'Av. Paulista, 900',cidade:'São Paulo',cep:'01310-200',emerg:'',saude:'',faixa:'roxa',grau:'1',turma:'1',status:'ativo',plano:'Mensal',valor:180,venc:add(t,3)},
    {id:3,nome:'Rafael Costa',cpf:'333.444.555-66',tel:'11973456789',email:'rafael@email.com',nasc:y+'-11-08',endereco:'Rua Augusta, 200',cidade:'São Paulo',cep:'01305-000',emerg:'',saude:'',faixa:'azul',grau:'3',turma:'2',status:'ativo',plano:'Trimestral',valor:480,venc:add(t,15)},
    {id:4,nome:'Juliana Lima',cpf:'444.555.666-77',tel:'11964567890',email:'ju@email.com',nasc:y+'-02-14',endereco:'Rua Oscar Freire, 55',cidade:'São Paulo',cep:'01426-000',emerg:'',saude:'Asma leve',faixa:'branca',grau:'1',turma:'2',status:'ativo',plano:'Mensal',valor:150,venc:t},
    {id:5,nome:'Pedro Alves',cpf:'555.666.777-88',tel:'11955678901',email:'pedro@email.com',nasc:y+'-09-01',endereco:'Rua Haddock Lobo, 300',cidade:'São Paulo',cep:'01414-001',emerg:'',saude:'',faixa:'marrom',grau:'0',turma:'1',status:'ativo',plano:'Mensal',valor:200,venc:add(t,-12)},
    {id:6,nome:'Fernanda Silva',cpf:'666.777.888-99',tel:'11946789012',email:'fe@email.com',nasc:y+'-05-30',endereco:'Alameda Santos, 700',cidade:'São Paulo',cep:'01419-001',emerg:'',saude:'',faixa:'azul',grau:'2',turma:'2',status:'ativo',plano:'Semestral',valor:900,venc:add(t,30)}
  ];
  for(var d=1;d<new Date().getDate();d+=2){
    var k=m+'-'+('0'+d).slice(-2);
    if(!presencas[k])presencas[k]=[];
    alunos.forEach(function(a){if(Math.random()>.35&&!presencas[k].includes(a.id))presencas[k].push(a.id)});
  }
  turmas=[
    {id:'1',nome:'Adulto Manhã',prof:'Prof. Carlos',hora:'07:00–08:30',dias:['Seg','Qua','Sex'],vagas:20,nivel:'Todas as faixas'},
    {id:'2',nome:'Adulto Noite',prof:'Prof. Carlos',hora:'19:00–20:30',dias:['Ter','Qui','Sáb'],vagas:25,nivel:'Todas as faixas'}
  ];
  produtos=[
    {id:1,nome:'Kimono Adulto A2',cat:'Kimono',sku:'KIM-A2',tam:'A2',custo:120,preco:280,qtd:5,min:3,emoji:'🥋'},
    {id:2,nome:'Kimono Adulto A3',cat:'Kimono',sku:'KIM-A3',tam:'A3',custo:120,preco:280,qtd:2,min:3,emoji:'🥋'},
    {id:3,nome:'Faixa Branca',cat:'Faixa',sku:'FAI-BR',tam:'M4',custo:15,preco:35,qtd:10,min:5,emoji:'🩹'},
    {id:4,nome:'Rashguard P',cat:'Rashguard',sku:'RG-P',tam:'P',custo:80,preco:160,qtd:4,min:2,emoji:'👕'},
    {id:5,nome:'Camiseta P',cat:'Camiseta',sku:'CAM-P',tam:'P',custo:30,preco:80,qtd:8,min:5,emoji:'👕'},
    {id:6,nome:'Isotônico',cat:'Bebida',sku:'ISO',tam:'500ml',custo:4,preco:10,qtd:24,min:10,emoji:'🧃'},
    {id:7,nome:'Detergente',cat:'Insumo',sku:'DET',tam:'1L',custo:5,preco:5,qtd:3,min:5,emoji:'🧴'},
    {id:8,nome:'Boné',cat:'Boné',sku:'BON-01',tam:'Único',custo:20,preco:65,qtd:6,min:3,emoji:'🧢'}
  ];
  for(var mo=0;mo<6;mo++){
    var ms=y+'-'+('0'+(mo+1)).slice(-2);
    alunos.forEach(function(a){receitas.push({id:uid(),desc:'Mensalidade '+a.nome.split(' ')[0],cat:'Mensalidade Aluno',val:a.valor,data:ms+'-05',forma:'Pix',aluno:a.nome,obs:''})});
    despesas.push({id:uid(),desc:'Aluguel',cat:'Aluguel',val:1800,data:ms+'-01',rec:'mensal',forma:'Boleto',obs:''});
    despesas.push({id:uid(),desc:'Royalties Tetris',cat:'Royalties Tetris',val:500,data:ms+'-01',rec:'mensal',forma:'Pix',obs:''});
    despesas.push({id:uid(),desc:'Luz',cat:'Luz',val:320,data:ms+'-10',rec:'mensal',forma:'Boleto',obs:''});
    despesas.push({id:uid(),desc:'Internet',cat:'Internet',val:150,data:ms+'-05',rec:'mensal',forma:'Boleto',obs:''});
  }
  graduacoes=[
    {id:1,alunoId:1,alunoNome:'Carlos Mendes',de:'marrom',grauDe:'4',para:'preta',grauPara:'0',data:'2022-06-15',prof:'Prof. Mestre',cerim:'',obs:''},
    {id:2,alunoId:2,alunoNome:'Ana Ferreira',de:'azul',grauDe:'4',para:'roxa',grauPara:'1',data:'2023-03-20',prof:'Prof. Carlos',cerim:'',obs:''}
  ];
  salvar();
})();

// ── HELPERS ─────────────────────────────────────────
function uid(){return Date.now()+Math.floor(Math.random()*1e6)}
function hoje(){return new Date().toISOString().split('T')[0]}
function hojeObj(){return new Date(new Date().toDateString())}
function salvar(){
  localStorage.setItem('bjj_a',JSON.stringify(alunos));
  localStorage.setItem('bjj_p',JSON.stringify(presencas));
  localStorage.setItem('bjj_r3',JSON.stringify(receitas));
  localStorage.setItem('bjj_d3',JSON.stringify(despesas));
  localStorage.setItem('bjj_g',JSON.stringify(graduacoes));
  localStorage.setItem('bjj_ce',JSON.stringify(cerimonias));
  localStorage.setItem('bjj_t',JSON.stringify(turmas));
  localStorage.setItem('bjj_pr',JSON.stringify(produtos));
  localStorage.setItem('bjj_mv',JSON.stringify(movEstoque));
  localStorage.setItem('bjj_us',JSON.stringify(usuarios));
  localStorage.setItem('bjj_cfg',JSON.stringify(cfg));
  localStorage.setItem('bjj_tpl',JSON.stringify(msgTpl));
}
function stPag(v){var d=Math.floor((new Date(v+'T12:00:00')-hojeObj())/86400000);return d<0?'atrasado':d===0?'vence-hoje':'em-dia'}
function stLbl(s){return{atrasado:'Atrasado','vence-hoje':'Vence Hoje','em-dia':'Em Dia'}[s]||s}
function stBdg(s){return{atrasado:'br','vence-hoje':'by','em-dia':'bg'}[s]||'bb'}
function fmtDate(d){if(!d)return'—';var p=d.split('-');return p[2]+'/'+p[1]+'/'+p[0]}
function fmtR(v){return'R$ '+parseFloat(v||0).toFixed(2).replace('.',',')}
function ini(n){return n.split(' ').slice(0,2).map(function(x){return x[0]}).join('').toUpperCase()}
function fmtTel(t){var d=(t||'').replace(/\D/g,'');if(d.length===11)return'('+d.slice(0,2)+') '+d.slice(2,7)+'-'+d.slice(7);return t}
function cap(s){return(s||'').charAt(0).toUpperCase()+(s||'').slice(1)}
function grauL(g){return g==='0'?'':' · '+g+'º'}
function fmtCPF(el){var v=el.value.replace(/\D/g,'').slice(0,11);v=v.replace(/(\d{3})(\d)/,'$1.$2').replace(/(\d{3})(\d)/,'$1.$2').replace(/(\d{3})(\d{1,2})$/,'$1-$2');el.value=v}
function fmtCEP(el){var v=el.value.replace(/\D/g,'').slice(0,8);v=v.replace(/(\d{5})(\d)/,'$1-$2');el.value=v}
function presM(id,mes){return Object.entries(presencas).filter(function(e){return e[0].startsWith(mes||relMes)}).filter(function(e){return e[1].includes(id)}).length}
function nomeTurma(id){var t=turmas.find(function(x){return String(x.id)===String(id)});return t?t.nome:'—'}
function catClr(cat,arr,cols){var i=arr.indexOf(cat);return i>=0?cols[i%cols.length]:'#888'}
function inRange(dt,rng){return dt>=rng.ini&&dt<=rng.fim}
function toast(ico,msg){clearTimeout(window._tt);document.getElementById('t-ico').textContent=ico;document.getElementById('t-msg').textContent=msg;document.getElementById('toast').classList.add('show');window._tt=setTimeout(function(){document.getElementById('toast').classList.remove('show')},3200)}
function prontoGraduar(a){var c=GRAD_CRIT[a.faixa]||{minMeses:6,minPres:60};var grds=graduacoes.filter(function(g){return g.alunoId===a.id}).sort(function(x,y){return new Date(y.data)-new Date(x.data)});var desde=grds.length?grds[0].data:(a.dataCadastro||hoje().slice(0,7)+'-01');var meses=Math.floor((hojeObj()-new Date(desde+'T12:00:00'))/(86400000*30));var totPres=Object.values(presencas).filter(function(v){return v.includes(a.id)}).length;return meses>=c.minMeses&&totPres>=c.minPres}
function buildMsgWA(a,key){var dias=Math.floor((hojeObj()-new Date(a.venc+'T12:00:00'))/86400000);return(msgTpl[key]||'').replace(/{nome}/g,a.nome.split(' ')[0]).replace(/{valor}/g,fmtR(a.valor)).replace(/{vencimento}/g,fmtDate(a.venc)).replace(/{dias}/g,String(dias)).replace(/{academia}/g,cfg.nome||'Academia')}
function waLink(a,key){return'https://wa.me/55'+(a.tel||'').replace(/\D/g,'')+'?text='+encodeURIComponent(buildMsgWA(a,key||'cobr'))}

// ── MENU ────────────────────────────────────────────
function toggleMenu(){
  var m=document.getElementById('mob-menu');
  if(m.classList.contains('open')){m.classList.remove('open')}else{m.classList.add('open')}
}
function nav(id,el){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('on')});
  document.getElementById('page-'+id).classList.add('on');
  document.querySelectorAll('.tb').forEach(function(b){b.classList.remove('on')});
  if(el)el.classList.add('on');
  renderPage(id);
}
function navM(id,el){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('on')});
  document.getElementById('page-'+id).classList.add('on');
  document.querySelectorAll('.mob-tb').forEach(function(b){b.classList.remove('on')});
  el.classList.add('on');
  document.getElementById('mob-menu').classList.remove('open');
  renderPage(id);
}
function renderPage(id){
  var fn={dashboard:rDash,financeiro:rFin,alunos:rAlunos,graduacoes:rGrad,turmas:rTurmas,presenca:rPresenca,estoque:rEstoque,pagamentos:rPag,cobrancas:rCobrancas,notificacoes:rNotif,relatorio:rRel,configuracoes:rConfig};
  if(fn[id])fn[id]();
}
// fechar menu ao clicar fora
document.addEventListener('click',function(e){
  var menu=document.getElementById('mob-menu');
  var btn=document.getElementById('hamburger-btn');
  if(menu&&menu.classList.contains('open')&&!menu.contains(e.target)&&e.target!==btn){
    menu.classList.remove('open');
  }
});

// ── DASHBOARD ───────────────────────────────────────
function rDash(){
  document.getElementById('dash-date').textContent=new Date().toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
  var m=hoje().slice(0,7);
  var recMes=receitas.filter(function(r){return r.data&&r.data.startsWith(m)}).reduce(function(s,r){return s+(r.val||0)},0);
  var despMes=despesas.filter(function(d){return d.data&&d.data.startsWith(m)}).reduce(function(s,d){return s+(d.val||0)},0);
  var inad=alunos.filter(function(a){return stPag(a.venc)==='atrasado'});
  var ativos=alunos.filter(function(a){return a.status==='ativo'});
  document.getElementById('d-recmes').textContent=fmtR(recMes);
  document.getElementById('d-recmes-s').textContent=receitas.filter(function(r){return r.data&&r.data.startsWith(m)}).length+' lançamentos';
  document.getElementById('d-despmes').textContent=fmtR(despMes);
  document.getElementById('d-despmes-s').textContent=despesas.filter(function(d){return d.data&&d.data.startsWith(m)}).length+' lançamentos';
  document.getElementById('d-total').textContent=alunos.length;
  document.getElementById('d-total-s').textContent=ativos.length+' ativos';
  document.getElementById('d-inad').textContent=inad.length;
  document.getElementById('d-inad-s').textContent=inad.length?fmtR(inad.reduce(function(s,a){return s+(a.valor||0)},0))+' aberto':'Nenhum';
  document.getElementById('d-pres').textContent=(presencas[hoje()]||[]).length;
  var ticket=ativos.length?Math.round(ativos.reduce(function(s,a){return s+(a.valor||0)},0)/ativos.length):0;
  document.getElementById('d-ticket').textContent=fmtR(ticket);
  document.getElementById('d-churn').textContent=alunos.length?Math.round((inad.length/alunos.length)*100)+'%':'0%';
  var alertasEst=produtos.filter(function(p){return(p.qtd||0)<=(p.min||3)}).length;
  document.getElementById('d-estoque-alerta').textContent=alertasEst;
  var gradPend=alunos.filter(function(a){return prontoGraduar(a)}).length;
  document.getElementById('d-grad-pend').textContent=gradPend;
  var proj30=alunos.filter(function(a){if(!a.venc)return false;var d=Math.floor((new Date(a.venc+'T12:00:00')-hojeObj())/86400000);return d>=0&&d<=30}).reduce(function(s,a){return s+(a.valor||0)},0);
  document.getElementById('d-projecao').textContent=fmtR(proj30);
  var res=recMes-despMes;
  var elR=document.getElementById('d-resultado');
  elR.textContent=fmtR(res);elR.style.color=res>=0?'var(--teal)':'var(--accent)';
  var prox=alunos.filter(function(a){var d=Math.floor((new Date(a.venc+'T12:00:00')-hojeObj())/86400000);return d>=-3&&d<=7}).sort(function(a,b){return new Date(a.venc)-new Date(b.venc)});
  document.getElementById('d-vencs').innerHTML=prox.length?prox.map(function(a){
    return'<div style="display:flex;align-items:center;justify-content:space-between;padding:9px 14px;border-bottom:1px solid var(--border)">'
      +'<div style="display:flex;align-items:center;gap:8px"><span class="dot faixa-'+a.faixa+'"></span>'
      +'<div><div style="font-size:12px;font-weight:600">'+a.nome+'</div>'
      +'<div style="font-size:11px;color:var(--muted)">'+fmtDate(a.venc)+'</div></div></div>'
      +'<span class="badge '+stBdg(stPag(a.venc))+'">'+stLbl(stPag(a.venc))+'</span></div>';
  }).join(''):'<div class="empty"><div style="font-size:11px">Nenhum vencimento próximo ✅</div></div>';
  var alerts=[];
  if(inad.length)alerts.push({ico:'🔴',txt:inad.length+' inadimplente'+(inad.length!==1?'s':'')});
  if(alertasEst)alerts.push({ico:'📦',txt:alertasEst+' produto'+(alertasEst!==1?'s':'')+' abaixo do mínimo'});
  if(gradPend)alerts.push({ico:'🥋',txt:gradPend+' aluno'+(gradPend!==1?'s':'')+' pronto'+(gradPend!==1?'s':'')+' para graduar'});
  var anivH=alunos.filter(function(a){if(!a.nasc)return false;var p=a.nasc.split('-'),tp=hoje().split('-');return p[1]===tp[1]&&p[2]===tp[2]});
  if(anivH.length)alerts.push({ico:'🎂',txt:'Aniversário: '+anivH.map(function(a){return a.nome.split(' ')[0]}).join(', ')});
  document.getElementById('d-alertas').innerHTML=alerts.length?alerts.map(function(a){
    return'<div class="notif-item"><span style="font-size:15px">'+a.ico+'</span><span style="font-size:12px">'+a.txt+'</span></div>';
  }).join(''):'<div class="empty"><div style="font-size:11px">Tudo em dia! ✅</div></div>';
  var ranked=alunos.map(function(a){return{nome:a.nome,cnt:presM(a.id,m)}}).sort(function(a,b){return b.cnt-a.cnt}).slice(0,6);
  var mx=Math.max.apply(null,ranked.map(function(a){return a.cnt}).concat([1]));
  document.getElementById('d-top-pres').innerHTML=ranked.map(function(a){
    return'<div style="display:flex;align-items:center;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--border)">'
      +'<div style="font-size:12px;font-weight:500">'+a.nome.split(' ')[0]+'</div>'
      +'<div style="display:flex;align-items:center;gap:7px">'
      +'<div class="bar-w"><div class="bar-g" style="width:'+(a.cnt/mx*100)+'%"></div></div>'
      +'<span style="font-size:11px;color:var(--blue);font-family:monospace">'+a.cnt+'x</span></div></div>';
  }).join('');
  var low=produtos.filter(function(p){return(p.qtd||0)<=(p.min||3)});
  document.getElementById('d-stock-alerts').innerHTML=low.length?low.map(function(p){
    return'<div style="display:flex;align-items:center;justify-content:space-between;padding:9px 14px;border-bottom:1px solid var(--border)">'
      +'<div style="font-size:12px">'+(p.emoji||'📦')+' '+p.nome+'</div>'
      +'<span class="badge '+((p.qtd||0)===0?'br':'by')+'">'+(p.qtd||0)+' un.</span></div>';
  }).join(''):'<div class="empty"><div style="font-size:11px">Estoque OK ✅</div></div>';
}

// ── FINANCEIRO ──────────────────────────────────────
function periodoRange(p){
  var now=new Date(),t=hoje();
  if(p==='dia')return{ini:t,fim:t};
  if(p==='semana'){var d=new Date(now);d.setDate(d.getDate()-6);return{ini:d.toISOString().split('T')[0],fim:t}}
  if(p==='mes')return{ini:t.slice(0,7)+'-01',fim:t};
  if(p==='trimestre'){var d=new Date(now);d.setMonth(d.getMonth()-2);d.setDate(1);return{ini:d.toISOString().split('T')[0],fim:t}}
  if(p==='semestre'){var d=new Date(now);d.setMonth(d.getMonth()-5);d.setDate(1);return{ini:d.toISOString().split('T')[0],fim:t}}
  return{ini:t.slice(0,4)+'-01-01',fim:t};
}
function setPeriod(p,el){period=p;document.querySelectorAll('#period-bar .pp').forEach(function(b){b.classList.remove('on')});el.classList.add('on');rFin()}
function rFin(){
  document.getElementById('fin-date').textContent=new Date().toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
  var rng=periodoRange(period);
  var lbls={dia:'Hoje',semana:'Últimos 7 dias',mes:'Este mês',trimestre:'Último trimestre',semestre:'Último semestre',ano:'Este ano'};
  document.getElementById('chart-lbl').textContent=lbls[period]||'';
  var rArr=receitas.filter(function(r){return inRange(r.data,rng)});
  var dArr=despesas.filter(function(d){return inRange(d.data,rng)});
  var totR=rArr.reduce(function(s,r){return s+(r.val||0)},0);
  var totD=dArr.reduce(function(s,d){return s+(d.val||0)},0);
  var res=totR-totD;
  document.getElementById('k-rec').textContent=fmtR(totR);
  document.getElementById('k-rec-s').textContent=rArr.length+' lançamentos';
  document.getElementById('k-desp').textContent=fmtR(totD);
  document.getElementById('k-desp-s').textContent=dArr.length+' lançamentos';
  var elR=document.getElementById('k-res');elR.textContent=fmtR(res);elR.style.color=res>=0?'var(--green)':'var(--accent)';
  var at=alunos.filter(function(a){return a.status==='ativo'});
  document.getElementById('k-al').textContent=at.length;
  document.getElementById('k-al-s').textContent=alunos.filter(function(a){return stPag(a.venc)==='em-dia'}).length+' em dia';
  var in2=alunos.filter(function(a){return stPag(a.venc)==='atrasado'});
  document.getElementById('k-in').textContent=in2.length;
  document.getElementById('k-in-s').textContent=in2.length?fmtR(in2.reduce(function(s,a){return s+(a.valor||0)},0))+' aberto':'Nenhum';
  buildMainChart(rng);buildPizzaChart(rng);renderDRE();renderTabFin();
}
function buildMainChart(rng){
  var ctx=document.getElementById('chart-main');
  if(chartMain){chartMain.destroy();chartMain=null}
  var labels=[],rD=[],dD=[],now=new Date();
  if(period==='dia'){
    ['00h','04h','08h','12h','16h','20h'].forEach(function(h){labels.push(h);rD.push(0);dD.push(0)});
    receitas.filter(function(r){return r.data===hoje()}).forEach(function(r){var s=Math.floor(Math.random()*6);rD[s]+=(r.val||0)});
    despesas.filter(function(d){return d.data===hoje()}).forEach(function(d){var s=Math.floor(Math.random()*6);dD[s]+=(d.val||0)});
  } else if(period==='semana'){
    for(var i=6;i>=0;i--){var d=new Date(now);d.setDate(d.getDate()-i);var k=d.toISOString().split('T')[0];labels.push(['Dom','Seg','Ter','Qua','Qui','Sex','Sáb'][d.getDay()]);rD.push(receitas.filter(function(r){return r.data===k}).reduce(function(s,r){return s+(r.val||0)},0));dD.push(despesas.filter(function(d2){return d2.data===k}).reduce(function(s,d2){return s+(d2.val||0)},0))}
  } else {
    var n={mes:1,trimestre:3,semestre:6,ano:12}[period]||12;
    for(var i=n-1;i>=0;i--){var d=new Date(now.getFullYear(),now.getMonth()-i,1);var ms=d.getFullYear()+'-'+('0'+(d.getMonth()+1)).slice(-2);labels.push(['Jan','Fev','Mar','Abr','Mai','Jun','Jul','Ago','Set','Out','Nov','Dez'][d.getMonth()]);rD.push(receitas.filter(function(r){return r.data&&r.data.startsWith(ms)}).reduce(function(s,r){return s+(r.val||0)},0));dD.push(despesas.filter(function(d2){return d2.data&&d2.data.startsWith(ms)}).reduce(function(s,d2){return s+(d2.val||0)},0))}
  }
  chartMain=new Chart(ctx,{type:'bar',data:{labels:labels,datasets:[{label:'Receita',data:rD,backgroundColor:'rgba(45,198,83,.65)',borderColor:'#2dc653',borderWidth:1},{label:'Despesas',data:dD,backgroundColor:'rgba(230,57,70,.55)',borderColor:'#e63946',borderWidth:1}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{x:{ticks:{color:'#5a5a72',maxRotation:30},grid:{color:'rgba(255,255,255,.03)'}},y:{ticks:{color:'#5a5a72',callback:function(v){return'R$'+v}},grid:{color:'rgba(255,255,255,.04)'}}}}});
}
function buildPizzaChart(rng){
  var ctx=document.getElementById('chart-pizza');
  if(chartPizza){chartPizza.destroy();chartPizza=null}
  var bycat={},arr,colors;
  if(pizzaTab==='rec'){arr=CAT_REC;colors=CR;receitas.filter(function(r){return inRange(r.data,rng)}).forEach(function(r){bycat[r.cat]=(bycat[r.cat]||0)+(r.val||0)})}
  else{arr=CAT_DESP;colors=CD;despesas.filter(function(d){return inRange(d.data,rng)}).forEach(function(d){bycat[d.cat]=(bycat[d.cat]||0)+(d.val||0)})}
  var cats=Object.keys(bycat).filter(function(c){return bycat[c]>0});
  var total=cats.reduce(function(s,c){return s+bycat[c]},0);
  if(!cats.length){document.getElementById('pizza-legend').innerHTML='<span>Nenhum lançamento</span>';return}
  chartPizza=new Chart(ctx,{type:'doughnut',data:{labels:cats,datasets:[{data:cats.map(function(c){return bycat[c]}),backgroundColor:cats.map(function(c){return catClr(c,arr,colors)}),borderWidth:0}]},options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},cutout:'60%'}});
  document.getElementById('pizza-legend').innerHTML=cats.map(function(c){return'<span style="display:flex;align-items:center;gap:3px"><span style="width:8px;height:8px;border-radius:2px;background:'+catClr(c,arr,colors)+'"></span>'+c+' '+Math.round((bycat[c]/total)*100)+'%</span>'}).join('');
}
function setPizzaTab(t){pizzaTab=t;document.getElementById('pz-r').classList.toggle('on',t==='rec');document.getElementById('pz-d').classList.toggle('on',t==='desp');buildPizzaChart(periodoRange(period))}
function renderDRE(){
  var m=hoje().slice(0,7);
  var bR={},bD={};
  CAT_REC.forEach(function(c){bR[c]=receitas.filter(function(r){return r.cat===c&&r.data&&r.data.startsWith(m)}).reduce(function(s,r){return s+(r.val||0)},0)});
  CAT_DESP.forEach(function(c){bD[c]=despesas.filter(function(d){return d.cat===c&&d.data&&d.data.startsWith(m)}).reduce(function(s,d){return s+(d.val||0)},0)});
  var tR=Object.values(bR).reduce(function(s,v){return s+v},0);
  var tD=Object.values(bD).reduce(function(s,v){return s+v},0);
  var html='<tr style="background:rgba(45,198,83,.05)"><td colspan="3" style="font-weight:700;color:var(--green);font-size:12px">RECEITAS</td></tr>';
  CAT_REC.forEach(function(c){if(bR[c]>0)html+='<tr><td style="color:'+catClr(c,CAT_REC,CR)+'">'+c+'</td><td style="font-family:monospace;color:var(--green)">'+fmtR(bR[c])+'</td><td style="color:var(--muted)">'+(tR?Math.round(bR[c]/tR*100)+'%':'—')+'</td></tr>'});
  html+='<tr style="background:rgba(45,198,83,.08)"><td style="font-weight:700">Total Receita</td><td style="font-family:monospace;font-weight:700;color:var(--green)">'+fmtR(tR)+'</td><td></td></tr>';
  html+='<tr style="background:rgba(230,57,70,.05)"><td colspan="3" style="font-weight:700;color:var(--accent);font-size:12px;padding-top:12px">DESPESAS</td></tr>';
  CAT_DESP.forEach(function(c){if(bD[c]>0)html+='<tr><td style="color:'+catClr(c,CAT_DESP,CD)+'">'+c+'</td><td style="font-family:monospace;color:var(--accent)">'+fmtR(bD[c])+'</td><td style="color:var(--muted)">'+(tD?Math.round(bD[c]/tD*100)+'%':'—')+'</td></tr>'});
  html+='<tr style="background:rgba(230,57,70,.08)"><td style="font-weight:700">Total Despesa</td><td style="font-family:monospace;font-weight:700;color:var(--accent)">'+fmtR(tD)+'</td><td></td></tr>';
  var res=tR-tD;
  html+='<tr style="background:rgba(6,214,160,.08)"><td style="font-weight:700;color:var(--teal)">RESULTADO LÍQUIDO</td><td style="font-family:monospace;font-weight:700;color:'+(res>=0?'var(--teal)':'var(--accent)')+'">'+fmtR(res)+'</td><td style="color:var(--muted)">'+(tR?Math.round(res/tR*100)+'%':'')+'</td></tr>';
  document.getElementById('tb-dre').innerHTML=html;
}
function renderTabFin(){
  if(finTab==='rec'){
    var cats=['todas'].concat(CAT_REC);
    document.getElementById('cat-filter-row').innerHTML=cats.map(function(c){return'<button class="tab-p '+(catRecFilt===c?'on':'')+'" onclick="setCatF(\'rec\',\''+c+'\')" style="margin-bottom:5px;font-size:10px">'+(c==='todas'?'Todas':c)+'</button>'}).join('');
    var data=(catRecFilt==='todas'?receitas:receitas.filter(function(r){return r.cat===catRecFilt})).slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
    document.getElementById('tab-total-lbl').textContent=data.length+' lançs. · '+fmtR(data.reduce(function(s,r){return s+(r.val||0)},0));
    document.getElementById('tb-rec').innerHTML=data.length?data.map(function(r){
      return'<tr><td style="font-weight:500">'+( r.desc||'—')+'</td>'
        +'<td><span style="color:'+catClr(r.cat,CAT_REC,CR)+';font-size:11px;font-weight:600">'+r.cat+'</span></td>'
        +'<td style="font-family:monospace;color:var(--green);font-weight:700">'+fmtR(r.val)+'</td>'
        +'<td style="font-family:monospace;font-size:11px">'+fmtDate(r.data)+'</td>'
        +'<td style="color:var(--muted);font-size:11px">'+(r.forma||'—')+'</td>'
        +'<td style="color:var(--muted);font-size:11px">'+(r.aluno||'—')+'</td>'
        +'<td><div class="act">'
        +'<button class="ab info" onclick="verHistR('+r.id+')">📋</button>'
        +'<button class="ab" onclick="editRec('+r.id+')">✎</button>'
        +'<button class="ab danger" onclick="delRec('+r.id+')">✕</button>'
        +'</div></td></tr>';
    }).join(''):'<tr><td colspan="7"><div class="empty"><div style="font-size:11px">Nenhuma receita</div></div></td></tr>';
  } else {
    var cats=['todas'].concat(CAT_DESP);
    document.getElementById('cat-filter-row').innerHTML=cats.map(function(c){return'<button class="tab-p '+(catDespFilt===c?'on':'')+'" onclick="setCatF(\'desp\',\''+c+'\')" style="margin-bottom:5px;font-size:10px">'+(c==='todas'?'Todas':c)+'</button>'}).join('');
    var data=(catDespFilt==='todas'?despesas:despesas.filter(function(d){return d.cat===catDespFilt})).slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
    document.getElementById('tab-total-lbl').textContent=data.length+' lançs. · '+fmtR(data.reduce(function(s,d){return s+(d.val||0)},0));
    document.getElementById('tb-desp').innerHTML=data.length?data.map(function(d){
      return'<tr><td style="font-weight:500">'+(d.desc||'—')+'</td>'
        +'<td><span style="color:'+catClr(d.cat,CAT_DESP,CD)+';font-size:11px;font-weight:600">'+d.cat+'</span></td>'
        +'<td style="font-family:monospace;color:var(--accent);font-weight:700">'+fmtR(d.val)+'</td>'
        +'<td style="font-family:monospace;font-size:11px">'+fmtDate(d.data)+'</td>'
        +'<td>'+(d.rec!=='nao'?'<span class="badge bb">'+cap(d.rec)+'</span>':'<span style="color:var(--muted);font-size:10px">—</span>')+'</td>'
        +'<td style="color:var(--muted);font-size:11px">'+(d.forma||'—')+'</td>'
        +'<td><div class="act">'
        +'<button class="ab info" onclick="verHistD('+d.id+')">📋</button>'
        +'<button class="ab" onclick="editDesp('+d.id+')">✎</button>'
        +'<button class="ab danger" onclick="delDesp('+d.id+')">✕</button>'
        +'</div></td></tr>';
    }).join(''):'<tr><td colspan="7"><div class="empty"><div style="font-size:11px">Nenhuma despesa</div></div></td></tr>';
  }
}
function setFinTab(t){
  finTab=t;
  document.getElementById('tab-rec-btn').classList.toggle('on',t==='rec');
  document.getElementById('tab-desp-btn').classList.toggle('on',t==='desp');
  document.getElementById('tab-rec-tbl').style.display=t==='rec'?'block':'none';
  document.getElementById('tab-desp-tbl').style.display=t==='desp'?'block':'none';
  document.getElementById('tab-add-btn').textContent=t==='rec'?'+ Receita':'+ Despesa';
  document.getElementById('tab-add-btn').onclick=t==='rec'?openModalRec:openModalDesp;
  document.getElementById('tab-add-btn').className='btn btn-sm '+(t==='rec'?'btn-green':'btn-red');
  renderTabFin();
}
function setCatF(type,cat){if(type==='rec')catRecFilt=cat;else catDespFilt=cat;renderTabFin()}
function verHistR(id){
  var r=receitas.find(function(x){return x.id===id});if(!r)return;
  var grupo=receitas.filter(function(x){return x.cat===r.cat}).slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
  var total=grupo.reduce(function(s,x){return s+(x.val||0)},0);
  document.getElementById('m-hist-t').textContent='HISTÓRICO · '+r.cat;
  document.getElementById('m-hist-body').innerHTML='<div style="padding:0 0 10px;font-size:11px;color:var(--muted);border-bottom:1px solid var(--border);margin-bottom:10px">Total: <strong style="color:var(--green)">'+fmtR(total)+'</strong> · '+grupo.length+' lançamentos</div>'
    +grupo.map(function(x){return'<div class="hist-item"><div><div style="font-size:12px;font-weight:500">'+(x.desc||'—')+'</div><div style="font-size:10px;color:var(--muted)">'+fmtDate(x.data)+' · '+(x.forma||'—')+(x.aluno?' · '+x.aluno:'')+'</div></div><span style="font-size:12px;font-weight:700;color:var(--green)">'+fmtR(x.val)+'</span></div>'}).join('');
  openM('m-hist');
}
function verHistD(id){
  var d=despesas.find(function(x){return x.id===id});if(!d)return;
  var grupo=despesas.filter(function(x){return x.cat===d.cat}).slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
  var total=grupo.reduce(function(s,x){return s+(x.val||0)},0);
  document.getElementById('m-hist-t').textContent='HISTÓRICO · '+d.cat;
  document.getElementById('m-hist-body').innerHTML='<div style="padding:0 0 10px;font-size:11px;color:var(--muted);border-bottom:1px solid var(--border);margin-bottom:10px">Total: <strong style="color:var(--accent)">'+fmtR(total)+'</strong> · '+grupo.length+' lançamentos</div>'
    +grupo.map(function(x){return'<div class="hist-item"><div><div style="font-size:12px;font-weight:500">'+(x.desc||'—')+'</div><div style="font-size:10px;color:var(--muted)">'+fmtDate(x.data)+' · '+(x.rec!=='nao'?cap(x.rec):'Avulso')+'</div></div><span style="font-size:12px;font-weight:700;color:var(--accent)">'+fmtR(x.val)+'</span></div>'}).join('');
  openM('m-hist');
}

// ── ALUNOS ──────────────────────────────────────────
function rAlunos(){
  var data=alunos.filter(function(a){
    var mQ=a.nome.toLowerCase().includes(q.toLowerCase())||(a.cpf&&a.cpf.includes(q));
    var mF=alFilt==='todos'||(alFilt==='ativo'&&a.status==='ativo')||(alFilt==='inativo'&&a.status!=='ativo');
    var mFa=!alFaixa||a.faixa===alFaixa;
    return mQ&&mF&&mFa;
  });
  document.getElementById('al-sub').textContent=data.length+' aluno'+(data.length!==1?'s':'')+' · '+alunos.filter(function(a){return a.status==='ativo'}).length+' ativos';
  document.getElementById('tb-al').innerHTML=data.length?data.map(function(a){
    return'<tr>'
      +'<td><div style="display:flex;align-items:center;gap:8px"><div class="av av-'+a.faixa+'">'+ini(a.nome)+'</div>'
      +'<div><div style="font-weight:600;font-size:12px">'+a.nome+'</div>'
      +'<div style="font-size:10px;color:var(--muted)">'+fmtTel(a.tel)+'</div></div></div></td>'
      +'<td style="font-family:monospace;font-size:11px;color:var(--muted)">'+(a.cpf||'—')+'</td>'
      +'<td style="font-size:11px;color:var(--muted)">'+nomeTurma(a.turma)+'</td>'
      +'<td><span class="fbadge fb-'+a.faixa+'"><span class="dot faixa-'+a.faixa+'"></span>'+cap(a.faixa)+grauL(a.grau)+'</span></td>'
      +'<td style="color:var(--muted);font-size:11px">'+a.plano+'</td>'
      +'<td style="font-family:monospace;font-size:11px">'+fmtDate(a.venc)+'</td>'
      +'<td><span class="badge '+stBdg(stPag(a.venc))+'">'+stLbl(stPag(a.venc))+'</span>'+(a.status!=='ativo'?' <span class="badge by">'+cap(a.status)+'</span>':'')+'</td>'
      +'<td><div class="act">'
      +'<button class="ab" onclick="editAluno('+a.id+')">✎</button>'
      +'<button class="ab ok" onclick="renovar('+a.id+')">↻</button>'
      +'<button class="ab info" onclick="verFicha('+a.id+')">👤</button>'
      +'<button class="ab" style="color:#25D366" onclick="envWA('+a.id+')">📲</button>'
      +'<button class="ab danger" onclick="delAluno('+a.id+')">✕</button>'
      +'</div></td></tr>';
  }).join(''):'<tr><td colspan="8"><div class="empty"><div style="font-size:11px">Nenhum aluno</div></div></td></tr>';
}
function buscar(v){q=v;rAlunos()}
function filtAl(f,el){alFilt=f;document.querySelectorAll('#page-alunos .pp').forEach(function(b){b.classList.remove('on')});el.classList.add('on');rAlunos()}
function filtFaixa(v){alFaixa=v;rAlunos()}
function verFicha(id){
  var a=alunos.find(function(x){return x.id===id});if(!a)return;
  var grds=graduacoes.filter(function(g){return g.alunoId===id}).slice().sort(function(x,y){return new Date(y.data)-new Date(x.data)});
  var totP=Object.values(presencas).filter(function(v){return v.includes(id)}).length;
  document.getElementById('m-hist-t').textContent='FICHA — '+a.nome.toUpperCase();
  var gHtml=grds.length?grds.map(function(g){
    return'<div class="hist-item"><div><div style="font-size:12px;font-weight:500">'+fmtDate(g.data)+'</div>'
      +'<div style="font-size:10px;color:var(--muted)">'+cap(g.de)+' → '+cap(g.para)+' · '+(g.prof||'—')+'</div></div>'
      +'<span class="fbadge fb-'+g.para+'"><span class="dot faixa-'+g.para+'"></span>'+cap(g.para)+'</span></div>';
  }).join(''):'<div style="color:var(--muted);font-size:11px;padding:8px 0">Nenhuma graduação registrada</div>';
  document.getElementById('m-hist-body').innerHTML=
    '<div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px">'
    +'<div><div style="font-size:10px;color:var(--muted)">FAIXA</div><span class="fbadge fb-'+a.faixa+'"><span class="dot faixa-'+a.faixa+'"></span>'+cap(a.faixa)+grauL(a.grau)+'</span></div>'
    +'<div><div style="font-size:10px;color:var(--muted)">PLANO</div><div style="font-size:12px;font-weight:600">'+a.plano+' · '+fmtR(a.valor)+'</div></div>'
    +'<div><div style="font-size:10px;color:var(--muted)">PRESENÇAS TOTAL</div><div style="font-size:18px;font-weight:800;color:var(--blue)">'+totP+'</div></div>'
    +'<div><div style="font-size:10px;color:var(--muted)">PRESENÇAS MÊS</div><div style="font-size:18px;font-weight:800;color:var(--green)">'+presM(id,hoje().slice(0,7))+'</div></div>'
    +(a.emerg?'<div style="grid-column:1/-1"><div style="font-size:10px;color:var(--muted)">EMERGÊNCIA</div><div style="font-size:12px">'+a.emerg+'</div></div>':'')
    +(a.saude?'<div style="grid-column:1/-1"><div style="font-size:10px;color:var(--accent)">SAÚDE</div><div style="font-size:12px">'+a.saude+'</div></div>':'')
    +'</div>'
    +'<div style="font-size:10px;font-weight:700;letter-spacing:1px;color:var(--muted);margin-bottom:8px">GRADUAÇÕES</div>'
    +gHtml
    +(prontoGraduar(a)?'<div class="alert alert-success" style="margin-top:12px">✅ Pronto para graduação!</div>':'');
  openM('m-hist');
}

// ── GRADUAÇÕES ──────────────────────────────────────
function rGrad(){
  var prontos=alunos.filter(function(a){return prontoGraduar(a)});
  if(!prontos.length){
    document.getElementById('grad-prontos').innerHTML='<div class="alert alert-info">Nenhum aluno atingiu todos os critérios ainda.</div>';
  } else {
    document.getElementById('grad-prontos').innerHTML='<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:10px;margin-bottom:14px">'
      +prontos.map(function(a){
        var grds=graduacoes.filter(function(g){return g.alunoId===a.id}).slice().sort(function(x,y){return new Date(y.data)-new Date(x.data)});
        var desde=grds.length?grds[0].data:(a.dataCadastro||hoje().slice(0,7)+'-01');
        var meses=Math.floor((hojeObj()-new Date(desde+'T12:00:00'))/(86400000*30));
        var totP=Object.values(presencas).filter(function(v){return v.includes(a.id)}).length;
        return'<div class="card" style="border-color:rgba(155,93,229,.3)">'
          +'<div class="cb2">'
          +'<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px">'
          +'<div style="font-size:13px;font-weight:700">'+a.nome+'</div><span class="badge bp">Pronto</span></div>'
          +'<span class="fbadge fb-'+a.faixa+'" style="display:inline-flex;margin-bottom:8px"><span class="dot faixa-'+a.faixa+'"></span>'+cap(a.faixa)+grauL(a.grau)+'</span>'
          +'<div style="font-size:11px;color:var(--muted);margin-top:4px">'+meses+' meses · '+totP+' presenças</div>'
          +'<div class="prog-bar"><div class="prog-fill" style="width:100%;background:var(--purple)"></div></div>'
          +'<button class="btn btn-purple btn-sm" style="margin-top:8px;width:100%" onclick="abrirGradAluno('+a.id+')">Registrar</button>'
          +'</div></div>';
      }).join('')+'</div>';
  }
  var gSorted=graduacoes.slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
  document.getElementById('tb-grad').innerHTML=gSorted.length?gSorted.map(function(g){
    return'<tr>'
      +'<td style="font-weight:600;font-size:12px">'+g.alunoNome+'</td>'
      +'<td><span class="fbadge fb-'+g.de+'"><span class="dot faixa-'+g.de+'"></span>'+cap(g.de)+'</span></td>'
      +'<td><span class="fbadge fb-'+g.para+'"><span class="dot faixa-'+g.para+'"></span>'+cap(g.para)+'</span></td>'
      +'<td style="font-family:monospace;font-size:11px">'+fmtDate(g.data)+'</td>'
      +'<td style="color:var(--muted);font-size:11px">'+(g.prof||'—')+'</td>'
      +'<td style="color:var(--muted);font-size:11px">'+(g.cerim||'Avulsa')+'</td>'
      +'</tr>';
  }).join(''):'<tr><td colspan="6"><div class="empty"><div style="font-size:11px">Nenhuma graduação</div></div></td></tr>';
  var cSorted=cerimonias.slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)});
  document.getElementById('tb-cerim').innerHTML=cSorted.length?cSorted.map(function(c){
    var qtd=graduacoes.filter(function(g){return g.cerim===c.nome}).length;
    return'<tr>'
      +'<td style="font-weight:600;font-size:12px">'+c.nome+'</td>'
      +'<td style="font-family:monospace;font-size:11px">'+fmtDate(c.data)+'</td>'
      +'<td style="color:var(--muted);font-size:11px">'+qtd+' alunos</td>'
      +'<td><button class="ab danger" onclick="delCerim('+c.id+')">✕</button></td>'
      +'</tr>';
  }).join(''):'<tr><td colspan="4"><div class="empty"><div style="font-size:11px">Nenhuma cerimônia</div></div></td></tr>';
}
function abrirGradAluno(id){
  openModalGrad();
  var a=alunos.find(function(x){return x.id===id});if(!a)return;
  document.getElementById('g-aluno').value=id;
  document.getElementById('g-de').value=a.faixa;
  document.getElementById('g-grau-de').value=a.grau;
}
function openModalGrad(){
  var sel=document.getElementById('g-aluno');
  sel.innerHTML='<option value="">Selecione...</option>'+alunos.map(function(a){return'<option value="'+a.id+'">'+a.nome+' ('+cap(a.faixa)+')</option>'}).join('');
  document.getElementById('g-data').value=hoje();
  document.getElementById('g-prof').value=cfg.prof||'';
  var selC=document.getElementById('g-cerim');
  selC.innerHTML='<option value="">— Avulsa —</option>'+cerimonias.map(function(c){return'<option value="'+c.nome+'">'+c.nome+'</option>'}).join('');
  openM('m-grad');
}
function salvarGrad(){
  var alunoId=parseInt(document.getElementById('g-aluno').value);if(!alunoId){toast('⚠','Selecione um aluno');return}
  var a=alunos.find(function(x){return x.id===alunoId});if(!a)return;
  var para=document.getElementById('g-para').value;
  var grauPara=document.getElementById('g-grau-para').value;
  graduacoes.push({id:uid(),alunoId:alunoId,alunoNome:a.nome,de:document.getElementById('g-de').value,grauDe:document.getElementById('g-grau-de').value,para:para,grauPara:grauPara,data:document.getElementById('g-data').value,prof:document.getElementById('g-prof').value,cerim:document.getElementById('g-cerim').value,obs:document.getElementById('g-obs').value});
  a.faixa=para;a.grau=grauPara;
  salvar();closeM('m-grad');rGrad();toast('🥋',a.nome.split(' ')[0]+' graduado para '+cap(para)+'!');
}
function openModalCerimonia(){document.getElementById('ce-data').value=hoje();document.getElementById('ce-nome').value='';document.getElementById('ce-local').value='';openM('m-cerim')}
function salvarCerim(){var nome=document.getElementById('ce-nome').value.trim();if(!nome){toast('⚠','Informe o nome');return}cerimonias.push({id:uid(),nome:nome,data:document.getElementById('ce-data').value,local:document.getElementById('ce-local').value});salvar();closeM('m-cerim');rGrad();toast('✓','Cerimônia criada!')}
function delCerim(id){if(!confirm('Remover cerimônia?'))return;cerimonias=cerimonias.filter(function(x){return x.id!==id});salvar();rGrad();toast('✓','Removida.')}

// ── TURMAS ──────────────────────────────────────────
function rTurmas(){
  ['pres-turma-sel','f-turma'].forEach(function(sid){
    var s=document.getElementById(sid);if(!s)return;
    var v=s.value;
    s.innerHTML=(sid==='pres-turma-sel'?'<option value="">Todos os alunos</option>':'<option value="">— Nenhuma —</option>')+turmas.map(function(t){return'<option value="'+t.id+'">'+t.nome+'</option>'}).join('');
    s.value=v;
  });
  var g=document.getElementById('turmas-grid');
  if(!turmas.length){g.innerHTML='<div class="card cb2" style="text-align:center;color:var(--muted)">Nenhuma turma. <button class="btn btn-blue btn-sm" onclick="openModalTurma()">+ Criar</button></div>';return}
  g.innerHTML=turmas.map(function(t){
    var mbrs=alunos.filter(function(a){return String(a.turma)===String(t.id)});
    var pct=t.vagas?Math.min(100,(mbrs.length/t.vagas)*100):50;
    var membHtml=mbrs.slice(0,6).map(function(a){return'<span class="fbadge fb-'+a.faixa+'" style="font-size:10px"><span class="dot faixa-'+a.faixa+'"></span>'+a.nome.split(' ')[0]+'</span>'}).join('');
    if(mbrs.length>6)membHtml+='<span style="font-size:10px;color:var(--muted)">+'+( mbrs.length-6)+'</span>';
    return'<div class="card">'
      +'<div class="ch"><span class="ct">'+t.nome+'</span>'
      +'<div class="act">'
      +'<button class="ab" onclick="editTurma(\''+t.id+'\')">✎</button>'
      +'<button class="ab danger" onclick="delTurma(\''+t.id+'\')">✕</button>'
      +'</div></div>'
      +'<div class="cb2">'
      +'<div style="font-size:12px;margin-bottom:5px">👤 <strong>'+(t.prof||'—')+'</strong></div>'
      +'<div style="font-size:11px;color:var(--muted);margin-bottom:3px">⏰ '+(t.hora||'—')+'</div>'
      +'<div style="font-size:11px;color:var(--muted);margin-bottom:3px">📅 '+(t.dias||[]).join(', ')+'</div>'
      +'<div style="font-size:11px;color:var(--muted);margin-bottom:8px">🎯 '+(t.nivel||'—')+' · '+mbrs.length+'/'+(t.vagas||'∞')+' vagas</div>'
      +'<div class="prog-bar"><div class="prog-fill" style="width:'+pct+'%;background:var(--blue)"></div></div>'
      +'<div style="margin-top:8px;display:flex;flex-wrap:wrap;gap:4px">'+membHtml+'</div>'
      +'</div></div>';
  }).join('');
}
function openModalTurma(){editTurmaId=null;document.getElementById('m-tur-t').textContent='NOVA TURMA';['t-nome','t-prof','t-hora','t-vagas'].forEach(function(i){document.getElementById(i).value=''});document.getElementById('t-nivel').value='Todas as faixas';document.querySelectorAll('#dias-checks input').forEach(function(cb){cb.checked=false});openM('m-turma')}
function editTurma(id){
  var t=turmas.find(function(x){return String(x.id)===String(id)});if(!t)return;
  editTurmaId=id;document.getElementById('m-tur-t').textContent='EDITAR TURMA';
  document.getElementById('t-nome').value=t.nome;document.getElementById('t-prof').value=t.prof||'';document.getElementById('t-hora').value=t.hora||'';document.getElementById('t-vagas').value=t.vagas||'';document.getElementById('t-nivel').value=t.nivel||'Todas as faixas';
  document.querySelectorAll('#dias-checks input').forEach(function(cb){cb.checked=(t.dias||[]).includes(cb.value)});openM('m-turma');
}
function salvarTurma(){
  var nome=document.getElementById('t-nome').value.trim();if(!nome){toast('⚠','Informe o nome');return}
  var dias=Array.from(document.querySelectorAll('#dias-checks input:checked')).map(function(cb){return cb.value});
  var data={nome:nome,prof:document.getElementById('t-prof').value,hora:document.getElementById('t-hora').value,dias:dias,vagas:parseInt(document.getElementById('t-vagas').value)||0,nivel:document.getElementById('t-nivel').value};
  if(editTurmaId){Object.assign(turmas.find(function(t){return String(t.id)===String(editTurmaId)}),data);toast('✓','Turma atualizada!')}
  else{data.id=String(uid());turmas.push(data);toast('✓','Turma criada!')}
  salvar();closeM('m-turma');rTurmas();
}
function delTurma(id){if(!confirm('Remover turma?'))return;turmas=turmas.filter(function(t){return String(t.id)!==String(id)});alunos.forEach(function(a){if(String(a.turma)===String(id))a.turma=''});salvar();rTurmas();toast('✓','Removida.')}

// ── PRESENÇA ────────────────────────────────────────
function rPresenca(){
  var d=new Date(presDate+'T12:00:00');
  document.getElementById('pres-sub').textContent=d.toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
  document.getElementById('pres-dlbl').textContent=fmtDate(presDate);
  rTurmas();
  var tf=document.getElementById('pres-turma-sel').value;
  var lista=tf?alunos.filter(function(a){return String(a.turma)===tf}):alunos;
  var ex=presencas[presDate]||[];cTemp={};ex.forEach(function(id){cTemp[id]=true});
  updCnt(lista);
  var el=document.getElementById('chamada-list');
  if(!lista.length){el.innerHTML='<div class="empty"><div style="font-size:11px">Nenhum aluno nesta turma</div></div>';return}
  el.innerHTML=lista.map(function(a){
    return'<div class="att"><div class="att-l"><div class="av av-'+a.faixa+'">'+ini(a.nome)+'</div>'
      +'<div><div style="font-size:12px;font-weight:600">'+a.nome+'</div>'
      +'<div style="font-size:10px;color:var(--muted)">'+cap(a.faixa)+grauL(a.grau)+' · '+presM(a.id,hoje().slice(0,7))+'x mês</div></div></div>'
      +'<button class="chk '+(cTemp[a.id]?'on':'')+'" id="ck-'+a.id+'" onclick="togP('+a.id+')">'+(cTemp[a.id]?'✓':'')+'</button></div>';
  }).join('');
}
function togP(id){cTemp[id]=!cTemp[id];var b=document.getElementById('ck-'+id);b.classList.toggle('on',cTemp[id]);b.textContent=cTemp[id]?'✓':'';updCnt(null)}
function updCnt(lista){var c=Object.values(cTemp).filter(Boolean).length;document.getElementById('pres-cnt').textContent=c+(lista?' /'+lista.length:'')+' presentes'}
function salvarChamada(){presencas[presDate]=Object.entries(cTemp).filter(function(e){return e[1]}).map(function(e){return parseInt(e[0])});salvar();toast('✓','Chamada de '+fmtDate(presDate)+' salva!')}
function chgDate(n){var dt=new Date(presDate+'T12:00:00');dt.setDate(dt.getDate()+n);presDate=dt.toISOString().split('T')[0];rPresenca()}
function toggleManual(){var s=document.getElementById('manual-block');s.style.display=s.style.display==='none'?'block':'none';if(s.style.display==='block'){document.getElementById('m-date').value=hoje();renderManual()}}
function renderManual(){
  var dt=document.getElementById('m-date').value;var ex=presencas[dt]||[];
  var mT={};ex.forEach(function(id){mT[id]=true});
  document.getElementById('manual-list').innerHTML=alunos.map(function(a){
    var on=!!mT[a.id];
    return'<div onclick="togManualItem(this,'+a.id+')" data-id="'+a.id+'" style="display:flex;align-items:center;gap:7px;padding:8px 11px;background:var(--s2);border:1px solid '+(on?'var(--green)':'var(--border)')+';border-radius:6px;cursor:pointer">'
      +'<div style="width:14px;height:14px;border-radius:50%;border:2px solid '+(on?'var(--green)':'var(--border)')+';background:'+(on?'var(--green)':'transparent')+';display:flex;align-items:center;justify-content:center;font-size:8px;color:#000">'+(on?'✓':'')+'</div>'
      +'<span class="dot faixa-'+a.faixa+'"></span>'
      +'<span style="font-size:11px">'+a.nome+'</span></div>';
  }).join('');
}
function togManualItem(el,id){
  var on=el.style.borderColor==='var(--green)'||el.style.borderColor==='rgb(45, 198, 83)';
  var newOn=!on;
  el.style.borderColor=newOn?'var(--green)':'var(--border)';
  var chk=el.querySelector('div');
  chk.style.borderColor=newOn?'var(--green)':'var(--border)';
  chk.style.background=newOn?'var(--green)':'transparent';
  chk.textContent=newOn?'✓':'';
}
function salvarManual(){
  var dt=document.getElementById('m-date').value;if(!dt){toast('⚠','Selecione data');return}
  var ids=Array.from(document.querySelectorAll('#manual-list [data-id]')).filter(function(el){return el.style.borderColor==='var(--green)'||el.style.borderColor==='rgb(45, 198, 83)'}).map(function(el){return parseInt(el.getAttribute('data-id'))});
  presencas[dt]=ids;salvar();toast('✓','Presença salva para '+fmtDate(dt)+'!');
}

// ── ESTOQUE ─────────────────────────────────────────
function rEstoque(){
  document.getElementById('e-total').textContent=produtos.length;
  var al=produtos.filter(function(p){return(p.qtd||0)<=(p.min||3)}).length;
  document.getElementById('e-alertas').textContent=al;
  document.getElementById('e-valor').textContent=fmtR(produtos.reduce(function(s,p){return s+(p.custo||0)*(p.qtd||0)},0));
  document.getElementById('e-potencial').textContent=fmtR(produtos.reduce(function(s,p){return s+(p.preco||0)*(p.qtd||0)},0));
  var data=estCat==='todos'?produtos:produtos.filter(function(p){return p.cat===estCat});
  document.getElementById('estoque-grid').innerHTML=data.length?data.map(function(p){
    var qtd=p.qtd||0,min=p.min||3,alerta=qtd<=min,sem=qtd===0;
    var mg=p.custo&&p.preco?Math.round(((p.preco-p.custo)/p.preco)*100):0;
    var pct=min?Math.min(100,(qtd/min)*100):100;
    var cor=sem?'var(--accent)':alerta?'var(--yellow)':'var(--green)';
    var bdg=sem?'br':alerta?'by':'bg';
    var brd=alerta?'border-color:'+(sem?'var(--accent)':'var(--yellow)')+';':'';
    return'<div class="stock-card" style="'+brd+'">'
      +'<div class="stock-img">'+(p.emoji||'📦')+'</div>'
      +'<div style="font-size:13px;font-weight:700;margin-bottom:3px">'+p.nome+'</div>'
      +'<div style="font-size:10px;color:var(--muted);margin-bottom:5px">'+p.cat+' · '+(p.sku||'—')+' · '+(p.tam||'—')+'</div>'
      +'<div style="display:flex;justify-content:space-between;margin-bottom:4px">'
      +'<span style="font-size:11px;color:var(--muted)">Custo: <strong style="color:var(--white)">'+fmtR(p.custo||0)+'</strong></span>'
      +'<span style="font-size:11px;color:var(--muted)">Venda: <strong style="color:var(--green)">'+fmtR(p.preco||0)+'</strong></span>'
      +'</div>'
      +'<div style="font-size:10px;color:var(--teal);margin-bottom:7px">Margem: '+mg+'%</div>'
      +'<div style="display:flex;justify-content:space-between;align-items:center">'
      +'<span class="badge '+bdg+'">'+qtd+' un.</span>'
      +'<span style="font-size:10px;color:var(--muted)">mín: '+min+'</span></div>'
      +'<div class="prog-bar"><div class="prog-fill" style="width:'+pct+'%;background:'+cor+'"></div></div>'
      +'<div style="display:flex;gap:5px;margin-top:8px">'
      +'<button class="btn btn-ghost btn-sm" onclick="editProd('+p.id+')" style="flex:1;font-size:10px">✎</button>'
      +'<button class="btn btn-orange btn-sm" onclick="movRapida('+p.id+')" style="flex:1;font-size:10px">↕</button>'
      +'<button class="ab danger" onclick="delProd('+p.id+')">✕</button>'
      +'</div></div>';
  }).join(''):'<div style="grid-column:1/-1;text-align:center;color:var(--muted);padding:40px">Nenhum produto.</div>';
  var mvS=movEstoque.slice().sort(function(a,b){return new Date(b.data)-new Date(a.data)}).slice(0,30);
  document.getElementById('tb-mov').innerHTML=mvS.length?mvS.map(function(m){
    var p=produtos.find(function(x){return x.id===m.prodId});
    var cor=m.tipo==='entrada'?'var(--green)':'var(--accent)';
    return'<tr>'
      +'<td style="font-weight:500;font-size:12px">'+(p?p.nome:'—')+'</td>'
      +'<td><span class="badge '+(m.tipo==='entrada'?'bg':m.tipo.startsWith('saida')?'br':'bb')+'">'+m.tipo+'</span></td>'
      +'<td style="font-family:monospace;font-weight:700;color:'+cor+'">'+(m.tipo==='entrada'?'+':'−')+m.qtd+'</td>'
      +'<td style="font-family:monospace;font-size:11px">'+fmtDate(m.data)+'</td>'
      +'<td style="color:var(--muted);font-size:11px">'+(m.obs||'—')+'</td>'
      +'<td style="color:var(--muted);font-size:11px">'+(m.resp||'—')+'</td>'
      +'</tr>';
  }).join(''):'<tr><td colspan="6"><div class="empty"><div style="font-size:11px">Nenhuma movimentação</div></div></td></tr>';
}
function filtEst(cat,el){estCat=cat;document.querySelectorAll('#est-pills .pill').forEach(function(p){p.classList.remove('on')});el.classList.add('on');rEstoque()}
function openModalProd(){editProdId=null;document.getElementById('m-prod-t').textContent='NOVO PRODUTO';['p-nome','p-sku','p-tam','p-custo','p-preco','p-qtd','p-min','p-emoji'].forEach(function(i){document.getElementById(i).value=''});document.getElementById('p-cat').value='Kimono';openM('m-prod')}
function editProd(id){var p=produtos.find(function(x){return x.id===id});if(!p)return;editProdId=id;document.getElementById('m-prod-t').textContent='EDITAR PRODUTO';document.getElementById('p-nome').value=p.nome;document.getElementById('p-cat').value=p.cat;document.getElementById('p-sku').value=p.sku||'';document.getElementById('p-tam').value=p.tam||'';document.getElementById('p-custo').value=p.custo||'';document.getElementById('p-preco').value=p.preco||'';document.getElementById('p-qtd').value=p.qtd||'';document.getElementById('p-min').value=p.min||'';document.getElementById('p-emoji').value=p.emoji||'';openM('m-prod')}
function salvarProd(){var nome=document.getElementById('p-nome').value.trim();if(!nome){toast('⚠','Informe o nome');return}var data={nome:nome,cat:document.getElementById('p-cat').value,sku:document.getElementById('p-sku').value,tam:document.getElementById('p-tam').value,custo:parseFloat(document.getElementById('p-custo').value)||0,preco:parseFloat(document.getElementById('p-preco').value)||0,qtd:parseInt(document.getElementById('p-qtd').value)||0,min:parseInt(document.getElementById('p-min').value)||3,emoji:document.getElementById('p-emoji').value||'📦'};if(editProdId){Object.assign(produtos.find(function(p){return p.id===editProdId}),data);toast('✓','Atualizado!')}else{data.id=uid();produtos.push(data);toast('✓','Produto cadastrado!')}salvar();closeM('m-prod');rEstoque()}
function delProd(id){if(!confirm('Remover produto?'))return;produtos=produtos.filter(function(x){return x.id!==id});salvar();rEstoque();toast('✓','Removido.')}
function openModalMov(){document.getElementById('mv-data').value=hoje();var sel=document.getElementById('mv-prod');sel.innerHTML='<option value="">Selecione...</option>'+produtos.map(function(p){return'<option value="'+p.id+'">'+p.nome+' ('+( p.qtd||0)+' un.)</option>'}).join('');openM('m-mov')}
function movRapida(id){openModalMov();document.getElementById('mv-prod').value=id}
function salvarMov(){
  var prodId=parseInt(document.getElementById('mv-prod').value);if(!prodId){toast('⚠','Selecione produto');return}
  var qtd=parseInt(document.getElementById('mv-qtd').value)||0;if(qtd<=0){toast('⚠','Informe quantidade');return}
  var tipo=document.getElementById('mv-tipo').value;
  var mov={id:uid(),prodId:prodId,tipo:tipo,qtd:qtd,data:document.getElementById('mv-data').value,obs:document.getElementById('mv-obs').value,resp:document.getElementById('mv-resp').value};
  movEstoque.push(mov);
  var p=produtos.find(function(x){return x.id===prodId});
  if(p){
    if(tipo==='entrada')p.qtd=(p.qtd||0)+qtd;
    else{p.qtd=Math.max(0,(p.qtd||0)-qtd);if(tipo==='saida'){receitas.push({id:uid(),desc:'Venda: '+p.nome,cat:p.cat,val:(p.preco||0)*qtd,data:mov.data,forma:'Pix',aluno:'',obs:qtd+' un.'})}}
  }
  salvar();closeM('m-mov');rEstoque();toast('✓','Movimentação salva!')
}

// ── PAGAMENTOS ──────────────────────────────────────
function rPag(){
  var data=pagFilt==='todos'?alunos:alunos.filter(function(a){return stPag(a.venc)===pagFilt});
  var rec=alunos.filter(function(a){return stPag(a.venc)!=='atrasado'}).reduce(function(s,a){return s+(a.valor||0)},0);
  document.getElementById('pag-sub').textContent='Receita em dia: '+fmtR(rec);
  document.getElementById('tb-pag').innerHTML=data.length?data.map(function(a){
    return'<tr>'
      +'<td><div style="display:flex;align-items:center;gap:7px"><span class="dot faixa-'+a.faixa+'"></span>'
      +'<div><div style="font-weight:600;font-size:12px">'+a.nome+'</div>'
      +'<div style="font-size:10px;color:var(--muted)">'+fmtTel(a.tel)+'</div></div></div></td>'
      +'<td style="color:var(--muted);font-size:11px">'+a.plano+'</td>'
      +'<td style="font-family:monospace;color:var(--green);font-size:12px">'+fmtR(a.valor)+'</td>'
      +'<td style="font-family:monospace;font-size:11px">'+fmtDate(a.venc)+'</td>'
      +'<td><span class="badge '+stBdg(stPag(a.venc))+'">'+stLbl(stPag(a.venc))+'</span></td>'
      +'<td><div style="display:flex;gap:5px">'
      +'<button class="btn btn-ghost btn-sm" onclick="renovar('+a.id+')">↻</button>'
      +'<a class="wa-btn" href="'+waLink(a,'cobr')+'" target="_blank">📲</a>'
      +'</div></td></tr>';
  }).join(''):'<tr><td colspan="6"><div class="empty"><div style="font-size:11px">Nenhum registro</div></div></td></tr>';
}
function filtPag(f,el){pagFilt=f;document.querySelectorAll('#page-pagamentos .pill').forEach(function(p){p.classList.remove('on')});el.classList.add('on');rPag()}
function renovar(id){
  var a=alunos.find(function(x){return x.id===id});if(!a)return;
  var v=new Date(a.venc+'T12:00:00'),base=v<hojeObj()?hojeObj():v;
  base.setMonth(base.getMonth()+(DIAS_MES[a.plano]||1));
  a.venc=base.toISOString().split('T')[0];
  salvar();toast('✓',a.nome.split(' ')[0]+' renovado!');rPag();rAlunos();rDash();
}
function envWA(id){var a=alunos.find(function(x){return x.id===id});if(a)window.open(waLink(a,'cobr'),'_blank')}

// ── COBRANÇAS ───────────────────────────────────────
function rCobrancas(){
  document.getElementById('msg-cobr-preview').textContent=msgTpl.cobr;
  var inad=alunos.filter(function(a){return['atrasado','vence-hoje'].includes(stPag(a.venc))});
  document.getElementById('wa-lista').innerHTML='<div class="ch"><span class="ct">Inadimplentes e Vencendo Hoje ('+inad.length+')</span></div>'
    +(inad.length?inad.map(function(a){
      return'<div style="display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-bottom:1px solid var(--border);gap:8px">'
        +'<div><div style="font-size:12px;font-weight:600">'+a.nome+'</div>'
        +'<div style="font-size:10px;color:var(--muted)">'+fmtTel(a.tel)+' · '+fmtDate(a.venc)+' · '+fmtR(a.valor)+'</div></div>'
        +'<a class="wa-btn" href="'+waLink(a,'cobr')+'" target="_blank">📲</a></div>';
    }).join(''):'<div class="empty"><div style="font-size:11px">Sem inadimplentes! 🎉</div></div>');
}
function envTodos(){alunos.filter(function(a){return stPag(a.venc)==='atrasado'}).forEach(function(a,i){setTimeout(function(){window.open(waLink(a,'cobr'),'_blank')},i*800)})}
function editMsg(key){msgEditKey=key;document.getElementById('msg-inp').value=msgTpl[key]||'';openM('m-msg')}
function salvarMsgTpl(){msgTpl[msgEditKey]=document.getElementById('msg-inp').value;salvar();closeM('m-msg');toast('✓','Mensagem salva!');rCobrancas();rNotif()}

// ── NOTIFICAÇÕES ────────────────────────────────────
var REGUA=[
  {key:'av7',gatilho:'7 dias antes do vencimento'},
  {key:'av3',gatilho:'3 dias antes do vencimento'},
  {key:'venc',gatilho:'No dia do vencimento'},
  {key:'atraso',gatilho:'3 dias após vencimento'},
  {key:'aniv',gatilho:'Aniversário do aluno'},
  {key:'boas',gatilho:'Cadastro de novo aluno'}
];
function rNotif(){
  document.getElementById('tb-regua').innerHTML=REGUA.map(function(r){
    return'<tr>'
      +'<td style="font-size:12px">'+r.gatilho+'</td>'
      +'<td style="font-size:11px;color:var(--muted);max-width:200px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">'+(msgTpl[r.key]||'').slice(0,60)+'...</td>'
      +'<td><span class="badge bg">Ativo</span></td>'
      +'<td><button class="ab info" onclick="editMsg(\''+r.key+'\')">✎</button></td>'
      +'</tr>';
  }).join('');
  var fila=[];
  alunos.forEach(function(a){
    var dias=Math.floor((new Date(a.venc+'T12:00:00')-hojeObj())/86400000);
    if(dias===7)fila.push({tipo:'av7',a:a,ico:'📅',msg:'Vence em 7 dias'});
    if(dias===3)fila.push({tipo:'av3',a:a,ico:'⚡',msg:'Vence em 3 dias'});
    if(dias===0)fila.push({tipo:'venc',a:a,ico:'💳',msg:'Vence hoje'});
    if(dias===-3)fila.push({tipo:'atraso',a:a,ico:'⚠️',msg:'3 dias em atraso'});
    if(a.nasc){var p=a.nasc.split('-'),tp=hoje().split('-');if(p[1]===tp[1]&&p[2]===tp[2])fila.push({tipo:'aniv',a:a,ico:'🎂',msg:'Aniversário hoje'})}
  });
  document.getElementById('notif-fila').innerHTML=fila.length?fila.map(function(f){
    return'<div style="display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-bottom:1px solid var(--border);gap:8px">'
      +'<div style="display:flex;align-items:center;gap:8px"><span style="font-size:15px">'+f.ico+'</span>'
      +'<div><div style="font-size:12px;font-weight:600">'+f.a.nome+'</div>'
      +'<div style="font-size:10px;color:var(--muted)">'+f.msg+'</div></div></div>'
      +'<a class="wa-btn" href="'+waLink(f.a,f.tipo)+'" target="_blank">📲</a></div>';
  }).join(''):'<div class="empty"><div style="font-size:11px">Nenhuma notificação pendente ✅</div></div>';
  document.getElementById('templates-list').innerHTML=Object.entries({cobr:'Cobrança',av7:'7 dias antes',av3:'3 dias antes',venc:'No vencimento',atraso:'Em atraso',aniv:'Aniversário',boas:'Boas-vindas'}).map(function(kv){
    return'<div class="card" style="margin-bottom:10px">'
      +'<div class="ch"><span class="ct">'+kv[1]+'</span><button class="ab info btn-sm" onclick="editMsg(\''+kv[0]+'\')">✎</button></div>'
      +'<div class="cb2"><div class="msg-box" style="font-size:11px">'+(msgTpl[kv[0]]||'—')+'</div></div></div>';
  }).join('');
}

// ── RELATÓRIO ───────────────────────────────────────
function rRel(){
  var meses=['Janeiro','Fevereiro','Março','Abril','Maio','Junho','Julho','Agosto','Setembro','Outubro','Novembro','Dezembro'];
  var parts=relMes.split('-');var y=parts[0],m=parts[1];
  document.getElementById('rel-mlbl').textContent=meses[parseInt(m)-1]+' '+y;
  document.getElementById('rel-sub').textContent='Análise — '+meses[parseInt(m)-1]+' / '+y;
  var rec=alunos.filter(function(a){return stPag(a.venc)!=='atrasado'}).reduce(function(s,a){return s+(a.valor||0)},0);
  document.getElementById('r-rec').textContent=fmtR(rec);
  document.getElementById('r-rec-s').textContent=alunos.filter(function(a){return stPag(a.venc)!=='atrasado'}).length+' em dia';
  var tot=Object.entries(presencas).filter(function(e){return e[0].startsWith(relMes)}).reduce(function(s,e){return s+e[1].length},0);
  document.getElementById('r-pres').textContent=tot;
  var iad=alunos.filter(function(a){return stPag(a.venc)==='atrasado'}).length;
  document.getElementById('r-inad').textContent=alunos.length?Math.round(iad/alunos.length*100)+'%':'0%';
  document.getElementById('r-inad-s').textContent=iad+' de '+alunos.length;
  var dias=Math.max(Object.keys(presencas).filter(function(k){return k.startsWith(relMes)}).length,1);
  document.getElementById('tb-rel').innerHTML=alunos.map(function(a){
    var cnt=presM(a.id,relMes),pct=Math.min(100,Math.round(cnt/dias*100)),s=stPag(a.venc),pr=prontoGraduar(a);
    return'<tr>'
      +'<td><div style="display:flex;align-items:center;gap:7px"><span class="dot faixa-'+a.faixa+'"></span><span style="font-weight:600;font-size:12px">'+a.nome+'</span></div></td>'
      +'<td><span class="fbadge fb-'+a.faixa+'" style="font-size:10px">'+cap(a.faixa)+grauL(a.grau)+'</span></td>'
      +'<td style="color:var(--muted);font-size:11px">'+a.plano+'</td>'
      +'<td style="font-family:monospace;color:var(--green);font-size:11px">'+fmtR(a.valor)+'</td>'
      +'<td><span class="badge '+stBdg(s)+'">'+stLbl(s)+'</span></td>'
      +'<td><div style="display:flex;align-items:center;gap:6px"><div class="bar-w"><div class="bar-g" style="width:'+pct+'%"></div></div><span style="font-family:monospace;font-size:11px;color:var(--blue)">'+cnt+'x</span></div></td>'
      +'<td>'+(pr?'<span class="badge bp">✅ Sim</span>':'<span style="font-size:10px;color:var(--muted)">Não</span>')+'</td>'
      +'</tr>';
  }).join('');
}
function chgMes(n){var parts=relMes.split('-');var dt=new Date(parseInt(parts[0]),parseInt(parts[1])-1+n,1);relMes=dt.getFullYear()+'-'+('0'+(dt.getMonth()+1)).slice(-2);rRel()}

// ── CONFIGURAÇÕES ───────────────────────────────────
function rConfig(){
  document.getElementById('cfg-nome').value=cfg.nome||'';document.getElementById('cfg-prof').value=cfg.prof||'';document.getElementById('cfg-tel').value=cfg.tel||'';document.getElementById('cfg-cnpj').value=cfg.cnpj||'';document.getElementById('cfg-end').value=cfg.end||'';
  document.getElementById('usuarios-lista').innerHTML=usuarios.length?usuarios.map(function(u){
    return'<div style="display:flex;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border)">'
      +'<div><div style="font-size:12px;font-weight:600">'+u.nome+'</div><div style="font-size:10px;color:var(--muted)">'+(u.email||'—')+'</div></div>'
      +'<div style="display:flex;align-items:center;gap:8px"><span class="badge bp">'+cap(u.perfil)+'</span>'
      +'<button class="ab danger" onclick="delUsuario('+u.id+')">✕</button></div></div>';
  }).join(''):'<div style="font-size:11px;color:var(--muted)">Nenhum usuário adicional.</div>';
}
function salvarConfig(){cfg={nome:document.getElementById('cfg-nome').value,prof:document.getElementById('cfg-prof').value,tel:document.getElementById('cfg-tel').value,cnpj:document.getElementById('cfg-cnpj').value,end:document.getElementById('cfg-end').value};salvar();toast('✓','Configurações salvas!')}
function exportarDados(){var data={alunos:alunos,presencas:presencas,receitas:receitas,despesas:despesas,graduacoes:graduacoes,cerimonias:cerimonias,turmas:turmas,produtos:produtos,movEstoque:movEstoque,usuarios:usuarios,cfg:cfg,msgTpl:msgTpl,exportedAt:new Date().toISOString()};var b=new Blob([JSON.stringify(data,null,2)],{type:'application/json'});var u=URL.createObjectURL(b);var a=document.createElement('a');a.href=u;a.download='bjjmgr-backup-'+hoje()+'.json';a.click();URL.revokeObjectURL(u);toast('✓','Backup exportado!')}
function importarDados(e){var f=e.target.files[0];if(!f)return;var r=new FileReader();r.onload=function(ev){try{var d=JSON.parse(ev.target.result);if(d.alunos)alunos=d.alunos;if(d.presencas)presencas=d.presencas;if(d.receitas)receitas=d.receitas;if(d.despesas)despesas=d.despesas;if(d.graduacoes)graduacoes=d.graduacoes;if(d.cerimonias)cerimonias=d.cerimonias;if(d.turmas)turmas=d.turmas;if(d.produtos)produtos=d.produtos;if(d.movEstoque)movEstoque=d.movEstoque;if(d.usuarios)usuarios=d.usuarios;if(d.cfg)cfg=d.cfg;if(d.msgTpl)msgTpl=d.msgTpl;salvar();rDash();toast('✓','Dados importados!')}catch(err){toast('✕','Erro ao importar')}};r.readAsText(f)}
function limparDados(){if(!confirm('ATENÇÃO: Apagar TODOS os dados?\nEsta ação não pode ser desfeita!'))return;['bjj_a','bjj_p','bjj_r3','bjj_d3','bjj_g','bjj_ce','bjj_t','bjj_pr','bjj_mv','bjj_us','bjj_cfg','bjj_tpl'].forEach(function(k){localStorage.removeItem(k)});location.reload()}
function openModalUsuario(){['u-nome','u-email'].forEach(function(i){document.getElementById(i).value=''});document.getElementById('u-perfil').value='professor';openM('m-usuario')}
function salvarUsuario(){var nome=document.getElementById('u-nome').value.trim();if(!nome){toast('⚠','Informe o nome');return}usuarios.push({id:uid(),nome:nome,perfil:document.getElementById('u-perfil').value,email:document.getElementById('u-email').value});salvar();closeM('m-usuario');rConfig();toast('✓','Usuário adicionado!')}
function delUsuario(id){if(!confirm('Remover?'))return;usuarios=usuarios.filter(function(x){return x.id!==id});salvar();rConfig();toast('✓','Removido.')}

// ── MODAIS RECEITA / DESPESA ────────────────────────
function openModalRec(){editRecId=null;document.getElementById('m-rec-t').textContent='NOVA RECEITA';['r-desc','r-val','r-obs'].forEach(function(i){document.getElementById(i).value=''});document.getElementById('r-cat').value='Mensalidade Aluno';document.getElementById('r-data').value=hoje();document.getElementById('r-forma').value='Pix';var sel=document.getElementById('r-aluno');sel.innerHTML='<option value="">— Nenhum —</option>'+alunos.map(function(a){return'<option value="'+a.nome+'">'+a.nome+'</option>'}).join('');openM('m-rec')}
function editRec(id){var r=receitas.find(function(x){return x.id===id});if(!r)return;editRecId=id;document.getElementById('m-rec-t').textContent='EDITAR RECEITA';document.getElementById('r-desc').value=r.desc||'';document.getElementById('r-cat').value=r.cat;document.getElementById('r-val').value=r.val;document.getElementById('r-data').value=r.data;document.getElementById('r-forma').value=r.forma||'Pix';document.getElementById('r-aluno').value=r.aluno||'';document.getElementById('r-obs').value=r.obs||'';openM('m-rec')}
function salvarRec(){var val=parseFloat(document.getElementById('r-val').value);if(!val||val<=0){toast('⚠','Informe valor');return}var data={desc:document.getElementById('r-desc').value.trim(),cat:document.getElementById('r-cat').value,val:val,data:document.getElementById('r-data').value,forma:document.getElementById('r-forma').value,aluno:document.getElementById('r-aluno').value,obs:document.getElementById('r-obs').value.trim()};if(editRecId){Object.assign(receitas.find(function(r){return r.id===editRecId}),data);toast('✓','Receita atualizada!')}else{data.id=uid();receitas.push(data);toast('✓','Receita lançada!')}salvar();closeM('m-rec');rFin();rDash()}
function delRec(id){if(!confirm('Remover?'))return;receitas=receitas.filter(function(x){return x.id!==id});salvar();rFin();rDash();toast('✓','Removida.')}
function openModalDesp(){editDespId=null;document.getElementById('m-desp-t').textContent='NOVA DESPESA';['d-desc','d-val','d-obs'].forEach(function(i){document.getElementById(i).value=''});document.getElementById('d-cat').value='Aluguel';document.getElementById('d-data').value=hoje();document.getElementById('d-rec').value='nao';document.getElementById('d-forma').value='Pix';openM('m-desp')}
function editDesp(id){var d=despesas.find(function(x){return x.id===id});if(!d)return;editDespId=id;document.getElementById('m-desp-t').textContent='EDITAR DESPESA';document.getElementById('d-desc').value=d.desc||'';document.getElementById('d-cat').value=d.cat;document.getElementById('d-val').value=d.val;document.getElementById('d-data').value=d.data;document.getElementById('d-rec').value=d.rec||'nao';document.getElementById('d-forma').value=d.forma||'Pix';document.getElementById('d-obs').value=d.obs||'';openM('m-desp')}
function salvarDesp(){var val=parseFloat(document.getElementById('d-val').value);if(!val||val<=0){toast('⚠','Informe valor');return}var data={desc:document.getElementById('d-desc').value.trim(),cat:document.getElementById('d-cat').value,val:val,data:document.getElementById('d-data').value,rec:document.getElementById('d-rec').value,forma:document.getElementById('d-forma').value,obs:document.getElementById('d-obs').value.trim()};if(editDespId){Object.assign(despesas.find(function(d){return d.id===editDespId}),data);toast('✓','Despesa atualizada!')}else{data.id=uid();despesas.push(data);toast('✓','Despesa lançada!')}salvar();closeM('m-desp');rFin();rDash()}
function delDesp(id){if(!confirm('Remover?'))return;despesas=despesas.filter(function(x){return x.id!==id});salvar();rFin();rDash();toast('✓','Removida.')}

// ── MODAIS ALUNO ────────────────────────────────────
function openModalAluno(){
  editAlId=null;document.getElementById('m-al-t').textContent='NOVO ALUNO';
  ['f-nome','f-cpf','f-tel','f-email','f-end','f-cid','f-cep','f-emerg','f-saude','f-val'].forEach(function(i){document.getElementById(i).value=''});
  document.getElementById('f-nasc').value='';document.getElementById('f-faixa').value='branca';document.getElementById('f-grau').value='0';document.getElementById('f-plano').value='Mensal';document.getElementById('f-status').value='ativo';document.getElementById('f-venc').value=hoje();
  rTurmas();openM('m-aluno');setTimeout(function(){document.getElementById('f-nome').focus()},100);
}
function editAluno(id){
  var a=alunos.find(function(x){return x.id===id});if(!a)return;
  editAlId=id;document.getElementById('m-al-t').textContent='EDITAR ALUNO';
  document.getElementById('f-nome').value=a.nome;document.getElementById('f-cpf').value=a.cpf||'';document.getElementById('f-tel').value=a.tel||'';document.getElementById('f-email').value=a.email||'';document.getElementById('f-nasc').value=a.nasc||'';document.getElementById('f-end').value=a.endereco||'';document.getElementById('f-cid').value=a.cidade||'';document.getElementById('f-cep').value=a.cep||'';document.getElementById('f-emerg').value=a.emerg||'';document.getElementById('f-saude').value=a.saude||'';document.getElementById('f-faixa').value=a.faixa||'branca';document.getElementById('f-grau').value=a.grau||'0';document.getElementById('f-status').value=a.status||'ativo';document.getElementById('f-plano').value=a.plano||'Mensal';document.getElementById('f-val').value=a.valor||'';document.getElementById('f-venc').value=a.venc||'';rTurmas();document.getElementById('f-turma').value=a.turma||'';openM('m-aluno');
}
function salvarAluno(){
  var nome=document.getElementById('f-nome').value.trim();if(!nome){toast('⚠','Informe o nome');return}
  var venc=document.getElementById('f-venc').value;if(!venc){toast('⚠','Informe o vencimento');return}
  var data={nome:nome,cpf:document.getElementById('f-cpf').value.trim(),tel:document.getElementById('f-tel').value.trim(),email:document.getElementById('f-email').value.trim(),nasc:document.getElementById('f-nasc').value,endereco:document.getElementById('f-end').value.trim(),cidade:document.getElementById('f-cid').value.trim(),cep:document.getElementById('f-cep').value.trim(),emerg:document.getElementById('f-emerg').value.trim(),saude:document.getElementById('f-saude').value.trim(),faixa:document.getElementById('f-faixa').value,grau:document.getElementById('f-grau').value,turma:document.getElementById('f-turma').value,status:document.getElementById('f-status').value,plano:document.getElementById('f-plano').value,valor:parseFloat(document.getElementById('f-val').value)||0,venc:venc};
  if(editAlId){Object.assign(alunos.find(function(a){return a.id===editAlId}),data);toast('✓','Aluno atualizado!')}
  else{data.id=uid();data.dataCadastro=hoje();alunos.push(data);toast('✓',nome.split(' ')[0]+' cadastrado!')}
  salvar();closeM('m-aluno');rAlunos();rDash();
}
function delAluno(id){var a=alunos.find(function(x){return x.id===id});if(!confirm('Remover '+a.nome+'?'))return;alunos=alunos.filter(function(x){return x.id!==id});salvar();rAlunos();rDash();toast('✓','Removido.')}

// ── UTILS ────────────────────────────────────────────
function openM(id){document.getElementById(id).classList.add('open')}
function closeM(id){document.getElementById(id).classList.remove('open')}
function ovC(e,id){if(e.target.id===id)closeM(id)}
document.addEventListener('keydown',function(e){
  if(e.key==='Escape')['m-aluno','m-grad','m-cerim','m-turma','m-prod','m-mov','m-rec','m-desp','m-msg','m-hist','m-usuario'].forEach(closeM);
});

// ── INIT ─────────────────────────────────────────────
rDash();rAlunos();
</script>
</body>
</html>
