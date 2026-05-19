<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FitLife Pro</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
:root{--bg:#f0f4f8;--card:#fff;--text:#222;--sub:#888;--border:#e8e8e8;--nav:#fff;--input:#fafafa;--input-border:#e0e0e0;}
body.dark{--bg:#0f0f1a;--card:#1a1a2e;--text:#eee;--sub:#aaa;--border:#2a2a3e;--nav:#16213e;--input:#16213e;--input-border:#2a2a3e;}
body{font-family:'Segoe UI',Arial,sans-serif;background:var(--bg);min-height:100vh;color:var(--text);transition:background .3s,color .3s;}

.auth-wrap{display:flex;align-items:center;justify-content:center;min-height:100vh;background:linear-gradient(135deg,#1a1a2e,#16213e,#0f3460);}
.auth-box{background:#fff;border-radius:22px;padding:38px 34px;width:390px;box-shadow:0 24px 64px rgba(0,0,0,.45);}
.auth-logo{text-align:center;margin-bottom:26px;}
.auth-logo .icon{font-size:50px;}
.auth-logo h1{font-size:27px;font-weight:900;color:#0f3460;margin-top:6px;}
.auth-logo p{font-size:13px;color:#888;margin-top:3px;}
.auth-tabs{display:flex;border-radius:10px;overflow:hidden;border:1px solid #e0e0e0;margin-bottom:22px;}
.auth-tab{flex:1;padding:10px;text-align:center;cursor:pointer;font-weight:700;font-size:14px;color:#888;background:#fafafa;transition:all .2s;}
.auth-tab.active{background:#0f3460;color:#fff;}
.fg{margin-bottom:14px;}
.fg label{display:block;font-size:11px;font-weight:700;color:#555;margin-bottom:5px;text-transform:uppercase;letter-spacing:.5px;}
.fg input,.fg select{width:100%;padding:11px 13px;border:1.5px solid #e0e0e0;border-radius:10px;font-size:14px;outline:none;transition:border .2s;background:#fafafa;}
.fg input:focus,.fg select:focus{border-color:#0f3460;}
.fr{display:grid;grid-template-columns:1fr 1fr;gap:11px;}
.btn-p{width:100%;padding:13px;background:linear-gradient(135deg,#0f3460,#e94560);color:#fff;border:none;border-radius:10px;font-size:15px;font-weight:800;cursor:pointer;margin-top:6px;transition:opacity .2s;}
.btn-p:hover{opacity:.9;}
.auth-err{color:#e94560;font-size:12px;text-align:center;margin-top:7px;min-height:17px;}
.auth-sw{text-align:center;margin-top:14px;font-size:13px;color:#888;}
.auth-sw span{color:#0f3460;font-weight:700;cursor:pointer;}

#app{display:none;min-height:100vh;}
.topbar{background:linear-gradient(135deg,#0f3460,#16213e);color:#fff;padding:13px 20px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100;box-shadow:0 2px 14px rgba(0,0,0,.3);}
.tbl{display:flex;align-items:center;gap:10px;}
.tb-logo{font-size:19px;font-weight:900;}
.tb-greet{font-size:12px;color:rgba(255,255,255,.65);}
.tbr{display:flex;align-items:center;gap:9px;}
.avatar{width:38px;height:38px;border-radius:50%;background:linear-gradient(135deg,#e94560,#f5a623);display:flex;align-items:center;justify-content:center;font-weight:900;font-size:16px;color:#fff;}
.lg-btn{background:rgba(255,255,255,.15);border:none;color:#fff;padding:7px 13px;border-radius:8px;cursor:pointer;font-size:12px;font-weight:700;}
.dark-toggle{background:rgba(255,255,255,.15);border:none;color:#fff;padding:7px 10px;border-radius:8px;cursor:pointer;font-size:15px;}
.nav{display:flex;background:var(--nav);border-bottom:1px solid var(--border);overflow-x:auto;transition:background .3s;}
.nb{padding:13px 16px;border:none;background:transparent;font-size:12px;font-weight:700;color:var(--sub);cursor:pointer;white-space:nowrap;border-bottom:3px solid transparent;transition:all .2s;}
.nb.active{color:#0f3460;border-bottom-color:#0f3460;}
.view{display:none;padding:20px;max-width:960px;margin:0 auto;}
.view.active{display:block;}

/* SHARED */
.banner{background:linear-gradient(135deg,#0f3460,#e94560);border-radius:16px;padding:22px 24px;color:#fff;margin-bottom:18px;position:relative;overflow:hidden;}
.banner::after{content:'💪';position:absolute;right:20px;top:50%;transform:translateY(-50%);font-size:62px;opacity:.18;}
.banner h2{font-size:21px;font-weight:900;}
.banner p{font-size:13px;opacity:.85;margin-top:4px;}
.quote-box{background:linear-gradient(135deg,#667eea,#764ba2);border-radius:13px;padding:15px 18px;color:#fff;margin-bottom:16px;font-style:italic;font-size:14px;line-height:1.5;}
.quote-box span{font-size:11px;opacity:.75;font-style:normal;display:block;margin-top:5px;}
.sr{display:grid;grid-template-columns:repeat(4,1fr);gap:11px;margin-bottom:18px;}
.sc{background:var(--card);border-radius:14px;padding:15px;text-align:center;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:background .3s;}
.sc .sv{font-size:25px;font-weight:900;color:#0f3460;}
.sc .sl{font-size:10px;color:var(--sub);text-transform:uppercase;letter-spacing:.5px;margin-top:2px;}
.sc .si{font-size:21px;margin-bottom:3px;}
.sec{font-size:15px;font-weight:900;color:var(--text);margin-bottom:11px;margin-top:4px;}
.card{background:var(--card);border-radius:14px;padding:18px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:16px;transition:background .3s;}
input,select{background:var(--input)!important;border-color:var(--input-border)!important;color:var(--text)!important;}

/* DASHBOARD TARGETS */
.tg2{display:grid;grid-template-columns:1fr 1fr;gap:13px;margin-bottom:18px;}
.tc{background:var(--card);border-radius:13px;padding:15px;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:background .3s;}
.th{display:flex;align-items:center;justify-content:space-between;margin-bottom:9px;}
.tn{font-weight:800;font-size:13px;}
.tbdg{font-size:10px;padding:3px 8px;border-radius:20px;font-weight:700;}
.tbdg.on-track{background:#e8f5e9;color:#2e7d32;}
.tbdg.behind{background:#fff3e0;color:#e65100;}
.tbdg.done{background:#e3f2fd;color:#1565c0;}
.pb{height:8px;background:#f0f0f0;border-radius:4px;overflow:hidden;margin-bottom:5px;}
.pf{height:100%;border-radius:4px;transition:width .5s;}
.pn{font-size:11px;color:var(--sub);display:flex;justify-content:space-between;}

/* ACTIVITY */
.al{background:var(--card);border-radius:13px;padding:15px;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:background .3s;}
.ai{display:flex;align-items:center;gap:11px;padding:9px 0;border-bottom:1px solid var(--border);}
.ai:last-child{border:none;}
.aico{width:40px;height:40px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;background:#f0f4ff;}
.ain{flex:1;}
.ain .nm{font-weight:700;font-size:14px;}
.ain .dt{font-size:11px;color:var(--sub);margin-top:1px;}
.acal{font-weight:800;font-size:13px;color:#e94560;}

/* WORKOUT */
.wg{display:grid;grid-template-columns:repeat(3,1fr);gap:13px;margin-bottom:18px;}
.wc{background:var(--card);border-radius:13px;padding:17px;box-shadow:0 2px 8px rgba(0,0,0,.06);cursor:pointer;transition:all .2s;border:2px solid transparent;}
.wc:hover{transform:translateY(-3px);box-shadow:0 8px 22px rgba(0,0,0,.12);}
.wc.sel{border-color:#0f3460;background:#f0f4ff;}
.wci{font-size:31px;margin-bottom:7px;}
.wcn{font-weight:900;font-size:15px;}
.wcd{font-size:11px;color:var(--sub);margin-top:2px;}
.wct{display:flex;gap:5px;margin-top:7px;flex-wrap:wrap;}
.tag{font-size:10px;padding:3px 8px;border-radius:20px;font-weight:700;}
.tag.cardio{background:#fce4ec;color:#c62828;}
.tag.strength{background:#e8eaf6;color:#283593;}
.tag.core{background:#e8f5e9;color:#1b5e20;}
.tag.hiit{background:#fff3e0;color:#e65100;}
.tag.custom{background:#f3e5f5;color:#6a1b9a;}
.ss{background:var(--card);border-radius:14px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:18px;transition:background .3s;}
.td{text-align:center;font-size:54px;font-weight:900;color:#0f3460;letter-spacing:2px;margin:10px 0;}
.tc2{display:flex;gap:9px;justify-content:center;flex-wrap:wrap;}
.tbtn{padding:11px 22px;border-radius:10px;border:none;font-weight:800;font-size:13px;cursor:pointer;transition:all .18s;}
.tbtn.go{background:linear-gradient(135deg,#0f3460,#e94560);color:#fff;}
.tbtn.stop{background:#fff;color:#e94560;border:2px solid #e94560;}
.tbtn.rst{background:#f0f0f0;color:#555;}
.tbtn.log{background:linear-gradient(135deg,#2e7d32,#1b5e20);color:#fff;}
.ls{display:grid;grid-template-columns:repeat(3,1fr);gap:9px;margin-top:13px;}
.lsi{text-align:center;background:#f8f9fa;border-radius:10px;padding:11px;}
.lsv{font-size:22px;font-weight:900;color:#0f3460;}
.lsl{font-size:10px;color:#888;text-transform:uppercase;}

/* PR TRACKER */
.pr-row{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:10px;}
.pr-card{background:var(--card);border-radius:12px;padding:13px;text-align:center;box-shadow:0 2px 8px rgba(0,0,0,.06);}
.pr-val{font-size:20px;font-weight:900;color:#e94560;}
.pr-lbl{font-size:10px;color:var(--sub);text-transform:uppercase;margin-top:2px;}
.pr-prev{font-size:10px;color:#4caf50;margin-top:2px;}

/* HEATMAP */
.heatmap{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;margin-bottom:4px;}
.hday{width:100%;aspect-ratio:1;border-radius:3px;background:#f0f0f0;cursor:default;transition:transform .15s;}
.hday:hover{transform:scale(1.2);}
.hday.l1{background:#bbdefb;}
.hday.l2{background:#42a5f5;}
.hday.l3{background:#0f3460;}
.hmap-labels{display:flex;justify-content:space-between;font-size:9px;color:var(--sub);margin-bottom:10px;}

/* FOOD */
.food-wrap{background:var(--card);border-radius:14px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:18px;transition:background .3s;}
.food-form{display:grid;grid-template-columns:2fr 1fr 1fr auto;gap:10px;align-items:end;margin-bottom:16px;}
.food-form .fg{margin:0;}
.food-tabs{display:flex;gap:8px;margin-bottom:13px;}
.meal-tab{padding:6px 14px;border-radius:20px;border:1.5px solid var(--border);font-size:12px;font-weight:700;cursor:pointer;color:var(--sub);background:transparent;transition:all .2s;}
.meal-tab.active{background:#0f3460;color:#fff;border-color:#0f3460;}
.food-list{display:flex;flex-direction:column;gap:8px;}
.food-item{display:flex;align-items:center;gap:12px;padding:10px 13px;background:#f8f9fa;border-radius:10px;}
.food-icon{font-size:22px;}
.food-info{flex:1;}
.food-name{font-weight:700;font-size:14px;}
.food-macros{font-size:11px;color:var(--sub);margin-top:1px;}
.food-cal{font-weight:900;color:#e94560;font-size:14px;}
.del{background:#fff0f0;border:none;color:#e94560;padding:5px 9px;border-radius:7px;cursor:pointer;font-size:12px;}
.macro-row{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:14px;}
.macro-card{background:var(--card);border-radius:13px;padding:14px;text-align:center;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:background .3s;}
.mc-val{font-size:22px;font-weight:900;}
.mc-lbl{font-size:10px;color:var(--sub);text-transform:uppercase;margin-top:2px;}
.calring{display:flex;align-items:center;justify-content:center;gap:20px;background:var(--card);border-radius:14px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:18px;transition:background .3s;}
.ring-info{text-align:center;}
.ring-title{font-size:13px;color:var(--sub);text-transform:uppercase;font-weight:700;}
.ring-num{font-size:32px;font-weight:900;color:#0f3460;}
.ring-sub{font-size:12px;color:#aaa;}

/* WATER */
.water-row{display:flex;align-items:center;gap:12px;flex-wrap:wrap;}
.water-drops{display:flex;gap:6px;flex-wrap:wrap;}
.drop{font-size:24px;cursor:pointer;opacity:.25;transition:opacity .2s;}
.drop.filled{opacity:1;}
.water-lbl{font-size:13px;font-weight:700;color:#0f3460;}

/* WEIGHT LOG */
.wt-row{display:flex;gap:10px;align-items:end;margin-bottom:13px;}
.wt-row .fg{margin:0;flex:1;}
.wt-row button{padding:12px 17px;background:#0f3460;color:#fff;border:none;border-radius:10px;cursor:pointer;font-weight:800;font-size:14px;white-space:nowrap;}
.wt-list{display:flex;flex-direction:column;gap:7px;}
.wt-item{display:flex;justify-content:space-between;align-items:center;padding:9px 13px;background:#f8f9fa;border-radius:10px;font-size:13px;}
.wt-val{font-weight:900;color:#0f3460;}
.wt-diff{font-size:11px;font-weight:700;}
.wt-diff.up{color:#e94560;}
.wt-diff.dn{color:#4caf50;}

/* CHARTS */
.chart-wrap{background:var(--card);border-radius:14px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:16px;transition:background .3s;}
.chart-title{font-size:13px;font-weight:800;color:#0f3460;margin-bottom:14px;text-transform:uppercase;letter-spacing:.5px;}
.bar-chart{display:flex;align-items:flex-end;gap:8px;height:140px;padding-bottom:4px;}
.bar-w{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;}
.bar{width:100%;border-radius:5px 5px 0 0;min-height:4px;cursor:pointer;transition:opacity .2s;}
.bar:hover{opacity:.75;}
.bar-lbl{font-size:9px;color:var(--sub);text-align:center;}
.bar-val{font-size:9px;font-weight:700;color:#0f3460;}
.line-chart{position:relative;height:120px;margin-bottom:4px;}
.lc-svg{width:100%;height:100%;}
.ring-row{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:16px;}
.ring-card{background:var(--card);border-radius:13px;padding:15px;display:flex;flex-direction:column;align-items:center;gap:6px;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:background .3s;}
.rclbl{font-size:10px;color:var(--sub);text-transform:uppercase;letter-spacing:.5px;}
.rcval{font-size:14px;font-weight:900;color:#0f3460;}

/* TARGETS */
.tg-form{background:var(--card);border-radius:14px;padding:20px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:18px;transition:background .3s;}
.tg-form h3{font-size:15px;font-weight:900;margin-bottom:13px;color:#0f3460;}
.fi{display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:10px;align-items:end;}
.fi .fg{margin:0;}
.add-btn{padding:12px 17px;background:#0f3460;color:#fff;border:none;border-radius:10px;cursor:pointer;font-weight:800;font-size:14px;}
.tlist{display:flex;flex-direction:column;gap:11px;}
.tgc{background:var(--card);border-radius:13px;padding:17px;box-shadow:0 2px 8px rgba(0,0,0,.06);display:flex;align-items:center;gap:13px;transition:background .3s;}
.tgico{font-size:28px;width:48px;height:48px;background:#f0f4ff;border-radius:12px;display:flex;align-items:center;justify-content:center;}
.tgi{flex:1;}
.tgn{font-weight:900;font-size:15px;}
.tgs{font-size:11px;color:var(--sub);margin-top:2px;}
.tgpb{height:6px;background:#f0f0f0;border-radius:3px;overflow:hidden;margin-top:7px;}
.tgpf{height:100%;border-radius:3px;transition:width .5s;}
.tgr{text-align:right;}
.tgpct{font-size:20px;font-weight:900;color:#0f3460;}
.tgst{font-size:10px;color:var(--sub);margin-top:1px;}
.del-btn{background:#fff0f0;border:none;color:#e94560;padding:6px 10px;border-radius:8px;cursor:pointer;font-size:12px;margin-top:4px;}

/* PROFILE */
.prof-card{background:var(--card);border-radius:14px;padding:22px;box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:14px;transition:background .3s;}
.ph{display:flex;align-items:center;gap:15px;margin-bottom:19px;}
.pav{width:68px;height:68px;border-radius:50%;background:linear-gradient(135deg,#e94560,#f5a623);display:flex;align-items:center;justify-content:center;font-size:29px;font-weight:900;color:#fff;}
.pnm{font-size:21px;font-weight:900;}
.pem{font-size:12px;color:var(--sub);margin-top:2px;}
.pg{display:grid;grid-template-columns:1fr 1fr;gap:11px;}
.pf2{background:#f8f9fa;border-radius:10px;padding:11px 13px;}
.pfl{font-size:10px;color:#888;text-transform:uppercase;letter-spacing:.5px;margin-bottom:2px;}
.pfv{font-size:15px;font-weight:800;color:#222;}
.bmic{background:linear-gradient(135deg,#0f3460,#16213e);border-radius:13px;padding:19px;color:#fff;text-align:center;margin-top:11px;}
.bmiv{font-size:42px;font-weight:900;}
.bmil{font-size:13px;opacity:.8;margin-top:3px;}
.bmicat{font-size:15px;font-weight:800;margin-top:3px;}
.edit-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px;}
.edit-row .fg{margin:0;}
.save-btn{padding:11px 20px;background:linear-gradient(135deg,#0f3460,#e94560);color:#fff;border:none;border-radius:10px;cursor:pointer;font-weight:800;font-size:13px;}

/* ACHIEVEMENTS */
.ach-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;}
.ach{background:var(--card);border-radius:13px;padding:13px;text-align:center;box-shadow:0 2px 8px rgba(0,0,0,.06);transition:all .2s;}
.ach.earned{border:2px solid #f5a623;background:#fffdf0;}
.ach .aico2{font-size:26px;margin-bottom:5px;}
.ach .an{font-size:11px;font-weight:800;color:var(--text);}
.ach .ad{font-size:10px;color:#aaa;margin-top:2px;}
.ach.earned .an{color:#e65100;}

/* REMINDER */
.rem-row{display:flex;gap:10px;align-items:end;margin-bottom:13px;flex-wrap:wrap;}
.rem-row .fg{margin:0;flex:1;min-width:140px;}
.rem-list{display:flex;flex-direction:column;gap:7px;}
.rem-item{display:flex;justify-content:space-between;align-items:center;padding:10px 14px;background:#f0f4ff;border-radius:10px;font-size:13px;}

/* CUSTOM EXERCISE */
.cex-form{display:grid;grid-template-columns:2fr 1fr 1fr 1fr auto;gap:9px;align-items:end;margin-bottom:13px;}
.cex-form .fg{margin:0;}

.toast{position:fixed;bottom:22px;right:22px;background:#222;color:#fff;padding:12px 19px;border-radius:10px;font-size:14px;font-weight:700;z-index:999;transform:translateY(80px);opacity:0;transition:all .3s;box-shadow:0 4px 20px rgba(0,0,0,.3);}
.toast.show{transform:translateY(0);opacity:1;}
.badge-notif{position:fixed;top:70px;right:22px;background:linear-gradient(135deg,#f5a623,#e94560);color:#fff;padding:14px 18px;border-radius:13px;font-size:14px;font-weight:700;z-index:999;transform:translateX(120%);opacity:0;transition:all .4s;box-shadow:0 4px 20px rgba(0,0,0,.3);max-width:240px;}
.badge-notif.show{transform:translateX(0);opacity:1;}

@media(max-width:600px){
  .sr,.wg,.ach-grid{grid-template-columns:1fr 1fr;}
  .tg2,.pr-row,.ring-row{grid-template-columns:1fr;}
  .fi,.cex-form{grid-template-columns:1fr 1fr;}
  .pg,.edit-row{grid-template-columns:1fr;}
  .macro-row{grid-template-columns:1fr 1fr;}
  .food-form{grid-template-columns:1fr 1fr;}
}
</style>
</head>
<body>

<div id="auth-wrap" class="auth-wrap">
  <div class="auth-box">
    <div class="auth-logo"><div class="icon">🏋️</div><h1>FITLIFE PRO</h1><p>Your Complete Fitness Companion</p></div>
    <div class="auth-tabs">
      <div class="auth-tab active" onclick="switchTab('login')">Login</div>
      <div class="auth-tab" onclick="switchTab('register')">Register</div>
    </div>
    <div id="login-form">
      <div class="fg"><label>Email</label><input type="email" id="li-email" placeholder="you@email.com"></div>
      <div class="fg"><label>Password</label><input type="password" id="li-pass" placeholder="••••••••"></div>
      <button class="btn-p" onclick="doLogin()">LOGIN →</button>
      <div class="auth-err" id="li-err"></div>
      <div class="auth-sw">No account? <span onclick="switchTab('register')">Register free</span></div>
    </div>
    <div id="register-form" style="display:none">
      <div class="fr">
        <div class="fg"><label>First Name</label><input id="rg-fn" placeholder="John"></div>
        <div class="fg"><label>Last Name</label><input id="rg-ln" placeholder="Doe"></div>
      </div>
      <div class="fg"><label>Email</label><input type="email" id="rg-em" placeholder="you@email.com"></div>
      <div class="fg"><label>Password</label><input type="password" id="rg-pw" placeholder="Min 6 chars"></div>
      <div class="fr">
        <div class="fg"><label>Age</label><input type="number" id="rg-age" placeholder="25"></div>
        <div class="fg"><label>Gender</label><select id="rg-gen"><option value="">Select</option><option>Male</option><option>Female</option><option>Other</option></select></div>
      </div>
      <div class="fr">
        <div class="fg"><label>Weight (kg)</label><input type="number" id="rg-wt" placeholder="70"></div>
        <div class="fg"><label>Height (cm)</label><input type="number" id="rg-ht" placeholder="175"></div>
      </div>
      <div class="fg"><label>Fitness Goal</label>
        <select id="rg-gl"><option value="">Select goal</option><option>Lose Weight</option><option>Build Muscle</option><option>Improve Endurance</option><option>Stay Fit</option><option>Increase Flexibility</option></select>
      </div>
      <button class="btn-p" onclick="doRegister()">CREATE ACCOUNT →</button>
      <div class="auth-err" id="rg-err"></div>
      <div class="auth-sw">Have account? <span onclick="switchTab('login')">Login</span></div>
    </div>
  </div>
</div>

<div id="app">
  <div class="topbar">
    <div class="tbl">
      <div class="tb-logo">🏋️ FITLIFE PRO</div>
      <div class="tb-greet" id="greeting"></div>
    </div>
    <div class="tbr">
      <button class="dark-toggle" onclick="toggleDark()" title="Dark Mode">🌙</button>
      <div class="avatar" id="user-av">?</div>
      <button class="lg-btn" onclick="logout()">Logout</button>
    </div>
  </div>
  <div class="nav">
    <button class="nb active" onclick="showView('dashboard',this)">🏠 Home</button>
    <button class="nb" onclick="showView('workout',this)">💪 Workout</button>
    <button class="nb" onclick="showView('food',this)">🍎 Nutrition</button>
    <button class="nb" onclick="showView('progress',this)">📊 Progress</button>
    <button class="nb" onclick="showView('targets',this)">🎯 Targets</button>
    <button class="nb" onclick="showView('profile',this)">👤 Profile</button>
    <button class="nb" onclick="showView('more',this)">⚙️ More</button>
  </div>

  <!-- DASHBOARD -->
  <div class="view active" id="view-dashboard">
    <div class="banner"><h2 id="dash-title">Welcome back!</h2><p id="dash-sub">Ready to crush your goals?</p></div>
    <div class="quote-box" id="quote-box">Loading quote...<span id="quote-auth"></span></div>
    <div class="sr">
      <div class="sc"><div class="si">🔥</div><div class="sv" id="d-cal">0</div><div class="sl">Cal Burned</div></div>
      <div class="sc"><div class="si">🍎</div><div class="sv" id="d-food-cal">0</div><div class="sl">Cal Eaten</div></div>
      <div class="sc"><div class="si">⏱️</div><div class="sv" id="d-min">0</div><div class="sl">Active Min</div></div>
      <div class="sc"><div class="si">📅</div><div class="sv" id="d-streak">0</div><div class="sl">Day Streak</div></div>
    </div>
    <!-- Water on dash -->
    <div class="card" style="margin-bottom:18px;">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;"><div class="sec" style="margin:0;">💧 Water Today</div><div style="font-size:12px;color:var(--sub);" id="water-dash-lbl">0 / 8 glasses</div></div>
      <div class="water-drops" id="water-drops-dash"></div>
    </div>
    <div class="sec">🎯 Active Targets</div>
    <div class="tg2" id="dash-targets"></div>
    <div class="sec">📋 Recent Activity</div>
    <div class="al" id="dash-activity"></div>
  </div>

  <!-- WORKOUT -->
  <div class="view" id="view-workout">
    <div class="sec">Choose Workout</div>
    <div class="wg" id="workout-grid"></div>
    <div class="ss">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:6px;">
        <div><div style="font-weight:900;font-size:16px;" id="sel-name">Select a workout above</div><div style="font-size:12px;color:var(--sub);" id="sel-detail">—</div></div>
        <div style="font-size:30px;" id="sel-icon">🏋️</div>
      </div>
      <div class="td" id="timer-disp">00:00</div>
      <div class="tc2">
        <button class="tbtn go" onclick="startTimer()">▶ Start</button>
        <button class="tbtn stop" onclick="pauseTimer()">⏸ Pause</button>
        <button class="tbtn rst" onclick="resetTimer()">↺ Reset</button>
        <button class="tbtn log" onclick="logWorkout()">✓ Log It</button>
      </div>
      <div class="ls">
        <div class="lsi"><div class="lsv" id="live-cal">0</div><div class="lsl">Calories</div></div>
        <div class="lsi"><div class="lsv" id="live-min">0</div><div class="lsl">Minutes</div></div>
        <div class="lsi"><div class="lsv" id="live-reps">0</div><div class="lsl">Est. Reps</div></div>
      </div>
    </div>
    <div class="card">
      <div class="sec" style="margin-bottom:13px;">🏆 Personal Records</div>
      <div class="pr-row" id="pr-row"></div>
    </div>
    <div class="card">
      <div class="sec" style="margin-bottom:13px;">➕ Add Custom Exercise</div>
      <div class="cex-form">
        <div class="fg"><label>Name</label><input id="ce-name" placeholder="e.g. Box Jumps"></div>
        <div class="fg"><label>Cal/min</label><input type="number" id="ce-cal" placeholder="8"></div>
        <div class="fg"><label>Reps/min</label><input type="number" id="ce-rpm" placeholder="12"></div>
        <div class="fg"><label>Category</label>
          <select id="ce-cat"><option value="custom">Custom</option><option value="cardio">Cardio</option><option value="strength">Strength</option><option value="core">Core</option><option value="hiit">HIIT</option></select>
        </div>
        <button class="add-btn" onclick="addCustomEx()">+ Add</button>
      </div>
    </div>
  </div>

  <!-- NUTRITION -->
  <div class="view" id="view-food">
    <div class="sec">Today's Nutrition</div>
    <div class="calring">
      <svg width="110" height="110">
        <circle cx="55" cy="55" r="44" fill="none" stroke="#f0f0f0" stroke-width="10"/>
        <circle id="cal-ring" cx="55" cy="55" r="44" fill="none" stroke="#e94560" stroke-width="10" stroke-dasharray="276" stroke-dashoffset="276" stroke-linecap="round" transform="rotate(-90 55 55)" style="transition:stroke-dashoffset .5s"/>
      </svg>
      <div class="ring-info">
        <div class="ring-title">Daily Goal</div>
        <div class="ring-num" id="cal-eaten">0</div>
        <div class="ring-sub">/ <span id="cal-goal-disp">2000</span> kcal</div>
      </div>
      <div>
        <div style="font-size:13px;margin-bottom:6px;"><span style="color:#e94560;font-weight:700" id="cal-remain">2000</span> kcal remaining</div>
        <div style="font-size:12px;color:var(--sub);">Burned: <span style="font-weight:700;color:#0f3460" id="cal-burned-disp">0</span> kcal</div>
        <div style="font-size:12px;color:var(--sub);margin-top:2px;">Net: <span style="font-weight:700;color:#2e7d32" id="cal-net">0</span> kcal</div>
      </div>
    </div>
    <div class="macro-row">
      <div class="macro-card"><div class="mc-val" style="color:#e94560" id="m-cal">0</div><div class="mc-lbl">🔥 Calories</div></div>
      <div class="macro-card"><div class="mc-val" style="color:#2196f3" id="m-pro">0g</div><div class="mc-lbl">💪 Protein</div></div>
      <div class="macro-card"><div class="mc-val" style="color:#ff9800" id="m-carb">0g</div><div class="mc-lbl">🍞 Carbs</div></div>
      <div class="macro-card"><div class="mc-val" style="color:#4caf50" id="m-fat">0g</div><div class="mc-lbl">🥑 Fat</div></div>
    </div>
    <!-- Water tracker -->
    <div class="card">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px;">
        <div class="sec" style="margin:0;">💧 Water Intake</div>
        <div style="font-size:12px;color:var(--sub);" id="water-lbl">0 / 8 glasses</div>
      </div>
      <div class="water-row">
        <div class="water-drops" id="water-drops"></div>
        <button onclick="resetWater()" style="padding:6px 12px;border:1px solid var(--border);border-radius:8px;background:transparent;color:var(--sub);cursor:pointer;font-size:12px;">Reset</button>
      </div>
      <div style="font-size:11px;color:var(--sub);margin-top:8px;">Tap drops to log glasses (goal: 8/day)</div>
    </div>
    <div class="food-wrap">
      <div class="sec" style="margin-bottom:10px;">Add Food</div>
      <div class="food-tabs">
        <button class="meal-tab active" onclick="setMeal('breakfast',this)">🌅 Breakfast</button>
        <button class="meal-tab" onclick="setMeal('lunch',this)">☀️ Lunch</button>
        <button class="meal-tab" onclick="setMeal('dinner',this)">🌙 Dinner</button>
        <button class="meal-tab" onclick="setMeal('snack',this)">🍿 Snack</button>
      </div>
      <div class="food-form">
        <div class="fg"><label>Food</label>
          <select id="food-sel" onchange="fillFood()">
            <option value="">-- Select Food --</option>
            <option value="rice">Rice (1 cup)</option><option value="chicken">Chicken Breast (100g)</option>
            <option value="egg">Egg (1 whole)</option><option value="banana">Banana</option>
            <option value="milk">Milk (1 cup)</option><option value="bread">Bread (1 slice)</option>
            <option value="oats">Oats (50g)</option><option value="apple">Apple</option>
            <option value="daal">Dal (1 bowl)</option><option value="roti">Roti (1 piece)</option>
            <option value="whey">Whey Protein Shake</option><option value="almonds">Almonds (10 pcs)</option>
            <option value="custom">Custom...</option>
          </select>
        </div>
        <div class="fg"><label>Calories</label><input type="number" id="food-cal" placeholder="kcal"></div>
        <div class="fg"><label>Protein (g)</label><input type="number" id="food-pro" placeholder="g"></div>
        <button class="add-btn" onclick="addFood()">+ Add</button>
      </div>
      <div id="custom-food" style="display:none;margin-bottom:13px;">
        <div class="fr">
          <div class="fg"><label>Food Name</label><input id="food-cname" placeholder="e.g. Paratha"></div>
          <div class="fg"><label>Carbs (g)</label><input type="number" id="food-carb" placeholder="g"></div>
        </div>
      </div>
      <div id="food-list"></div>
    </div>
  </div>

  <!-- PROGRESS -->
  <div class="view" id="view-progress">
    <div class="sec">Activity Heatmap (Last 28 Days)</div>
    <div class="card">
      <div class="hmap-labels" id="hmap-days"></div>
      <div class="heatmap" id="heatmap"></div>
      <div style="display:flex;gap:8px;align-items:center;margin-top:8px;font-size:11px;color:var(--sub);">
        <div style="width:12px;height:12px;background:#f0f0f0;border-radius:2px;"></div> None
        <div style="width:12px;height:12px;background:#bbdefb;border-radius:2px;"></div> Light
        <div style="width:12px;height:12px;background:#42a5f5;border-radius:2px;"></div> Moderate
        <div style="width:12px;height:12px;background:#0f3460;border-radius:2px;"></div> Intense
      </div>
    </div>
    <div class="sec">Weight Trend</div>
    <div class="chart-wrap">
      <div class="chart-title">Body Weight (kg)</div>
      <div class="line-chart"><svg class="lc-svg" id="wt-chart"></svg></div>
      <div id="wt-chart-labels" style="display:flex;justify-content:space-between;font-size:9px;color:var(--sub);margin-top:4px;"></div>
    </div>
    <div class="sec">Weekly Training</div>
    <div class="chart-wrap"><div class="chart-title">Calories Burned — Last 7 Days</div><div class="bar-chart" id="cal-chart"></div></div>
    <div class="chart-wrap"><div class="chart-title">Active Minutes — Last 7 Days</div><div class="bar-chart" id="min-chart"></div></div>
    <div class="sec">Daily Goal Rings</div>
    <div class="ring-row">
      <div class="ring-card"><svg width="88" height="88"><circle cx="44" cy="44" r="36" fill="none" stroke="rgba(233,69,96,.15)" stroke-width="8"/><circle id="r1" cx="44" cy="44" r="36" fill="none" stroke="#e94560" stroke-width="8" stroke-dasharray="226" stroke-dashoffset="226" stroke-linecap="round" transform="rotate(-90 44 44)" style="transition:stroke-dashoffset .6s"/></svg><div class="rclbl">Calories</div><div class="rcval" id="r1v">0%</div></div>
      <div class="ring-card"><svg width="88" height="88"><circle cx="44" cy="44" r="36" fill="none" stroke="rgba(15,52,96,.15)" stroke-width="8"/><circle id="r2" cx="44" cy="44" r="36" fill="none" stroke="#0f3460" stroke-width="8" stroke-dasharray="226" stroke-dashoffset="226" stroke-linecap="round" transform="rotate(-90 44 44)" style="transition:stroke-dashoffset .6s"/></svg><div class="rclbl">Active Min</div><div class="rcval" id="r2v">0%</div></div>
      <div class="ring-card"><svg width="88" height="88"><circle cx="44" cy="44" r="36" fill="none" stroke="rgba(76,175,80,.15)" stroke-width="8"/><circle id="r3" cx="44" cy="44" r="36" fill="none" stroke="#4caf50" stroke-width="8" stroke-dasharray="226" stroke-dashoffset="226" stroke-linecap="round" transform="rotate(-90 44 44)" style="transition:stroke-dashoffset .6s"/></svg><div class="rclbl">Nutrition</div><div class="rcval" id="r3v">0%</div></div>
    </div>
    <div class="sec">🏅 Achievements</div>
    <div class="ach-grid" id="ach-grid"></div>
  </div>

  <!-- TARGETS -->
  <div class="view" id="view-targets">
    <div class="tg-form">
      <h3>➕ Set New Target</h3>
      <div class="fi">
        <div class="fg"><label>Type</label>
          <select id="tg-type">
            <option value="calories">🔥 Calories/Day</option>
            <option value="workouts">💪 Workouts/Week</option>
            <option value="minutes">⏱️ Active Min/Day</option>
            <option value="weight">⚖️ Target Weight (kg)</option>
            <option value="protein">💊 Protein/Day (g)</option>
            <option value="water">💧 Water Glasses/Day</option>
          </select>
        </div>
        <div class="fg"><label>Goal</label><input type="number" id="tg-val" placeholder="e.g. 500"></div>
        <div class="fg"><label>Deadline</label><input type="date" id="tg-date"></div>
        <button class="add-btn" onclick="addTarget()">+ Add</button>
      </div>
    </div>
    <div class="sec">Your Targets</div>
    <div class="tlist" id="targets-list"></div>
  </div>

  <!-- PROFILE -->
  <div class="view" id="view-profile">
    <div class="prof-card">
      <div class="ph"><div class="pav" id="prof-av">J</div><div><div class="pnm" id="prof-nm">—</div><div class="pem" id="prof-em">—</div></div></div>
      <div class="pg">
        <div class="pf2"><div class="pfl">Age</div><div class="pfv" id="p-age">—</div></div>
        <div class="pf2"><div class="pfl">Gender</div><div class="pfv" id="p-gen">—</div></div>
        <div class="pf2"><div class="pfl">Weight</div><div class="pfv" id="p-wt">—</div></div>
        <div class="pf2"><div class="pfl">Height</div><div class="pfv" id="p-ht">—</div></div>
        <div class="pf2"><div class="pfl">Goal</div><div class="pfv" id="p-gl">—</div></div>
        <div class="pf2"><div class="pfl">Member Since</div><div class="pfv" id="p-since">—</div></div>
      </div>
      <div class="bmic"><div class="bmiv" id="bmi-v">—</div><div class="bmil">BMI — Body Mass Index</div><div class="bmicat" id="bmi-c">—</div></div>
    </div>
    <div class="prof-card">
      <div class="sec" style="margin-bottom:13px;">✏️ Edit Profile</div>
      <div class="edit-row">
        <div class="fg"><label>Weight (kg)</label><input type="number" id="edit-wt" placeholder="kg"></div>
        <div class="fg"><label>Height (cm)</label><input type="number" id="edit-ht" placeholder="cm"></div>
        <div class="fg"><label>Calorie Goal</label><input type="number" id="edit-calgoal" placeholder="e.g. 2000"></div>
        <div class="fg"><label>Fitness Goal</label>
          <select id="edit-gl"><option>Lose Weight</option><option>Build Muscle</option><option>Improve Endurance</option><option>Stay Fit</option><option>Increase Flexibility</option></select>
        </div>
      </div>
      <button class="save-btn" onclick="saveProfile()">Save Changes</button>
    </div>
    <div class="prof-card">
      <div class="sec" style="margin-bottom:13px;">📊 All-Time Stats</div>
      <div class="sr" style="margin:0;">
        <div class="sc"><div class="si">🔥</div><div class="sv" id="tot-cal">0</div><div class="sl">Cal Burned</div></div>
        <div class="sc"><div class="si">💪</div><div class="sv" id="tot-w">0</div><div class="sl">Workouts</div></div>
        <div class="sc"><div class="si">⏱️</div><div class="sv" id="tot-min">0</div><div class="sl">Minutes</div></div>
        <div class="sc"><div class="si">🔥</div><div class="sv" id="best-str">0</div><div class="sl">Best Streak</div></div>
      </div>
    </div>
    <div class="prof-card">
      <div class="sec" style="margin-bottom:13px;">📅 Weight Log</div>
      <div class="wt-row">
        <div class="fg"><label>Today's Weight (kg)</label><input type="number" id="wt-input" placeholder="e.g. 72.5" step="0.1"></div>
        <button onclick="logWeight()">Log Weight</button>
      </div>
      <div class="wt-list" id="wt-list"></div>
    </div>
  </div>

  <!-- MORE -->
  <div class="view" id="view-more">
    <div class="sec">⏰ Workout Reminders</div>
    <div class="card">
      <div class="rem-row">
        <div class="fg"><label>Time</label><input type="time" id="rem-time" value="07:00"></div>
        <div class="fg"><label>Label</label><input id="rem-label" placeholder="e.g. Morning Run"></div>
        <button class="add-btn" onclick="addReminder()">+ Add</button>
      </div>
      <div class="rem-list" id="rem-list"></div>
      <div style="font-size:11px;color:var(--sub);margin-top:10px;">* Reminders shown as in-app notifications while app is open.</div>
    </div>
    <div class="sec">📋 Weekly Report Card</div>
    <div class="card" id="report-card"></div>
    <div class="sec">🌙 Dark Mode</div>
    <div class="card" style="display:flex;align-items:center;justify-content:space-between;">
      <div><div style="font-weight:700;">Dark Theme</div><div style="font-size:12px;color:var(--sub);">Easy on the eyes at night</div></div>
      <button onclick="toggleDark()" style="padding:10px 20px;background:linear-gradient(135deg,#0f3460,#e94560);color:#fff;border:none;border-radius:10px;cursor:pointer;font-weight:800;">Toggle</button>
    </div>
    <div class="sec">🗑️ Data Management</div>
    <div class="card" style="display:flex;gap:10px;flex-wrap:wrap;">
      <button onclick="clearToday()" style="padding:10px 16px;background:#fff3e0;color:#e65100;border:1px solid #ffcc80;border-radius:10px;cursor:pointer;font-weight:700;font-size:13px;">Clear Today's Data</button>
      <button onclick="clearAll()" style="padding:10px 16px;background:#fff0f0;color:#e94560;border:1px solid #ffcdd2;border-radius:10px;cursor:pointer;font-weight:700;font-size:13px;">Reset All Data</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>
<div class="badge-notif" id="badge-notif">🏅 Achievement Unlocked!<br><span id="badge-name"></span></div>

<script>
// ══════════ QUOTES ══════════
const QUOTES=[
  {q:"The only bad workout is the one that didn't happen.",a:"Unknown"},
  {q:"Take care of your body. It's the only place you have to live.",a:"Jim Rohn"},
  {q:"Strength does not come from the body. It comes from the will of the soul.",a:"Gandhi"},
  {q:"Push yourself because no one else is going to do it for you.",a:"Unknown"},
  {q:"The difference between try and triumph is just a little umph!",a:"Marvin Phillips"},
  {q:"Your body can stand almost anything. It's your mind you have to convince.",a:"Unknown"},
  {q:"Success starts with self-discipline.",a:"Unknown"},
  {q:"Don't wish for it. Work for it.",a:"Unknown"},
];

// ══════════ DATA ══════════
let users=JSON.parse(localStorage.getItem('fl_users')||'[]');
let CU=null,UD={};
let targets=[],wLog=[],fLog=[],wtLog=[],reminders=[],customEx=[];
let curMeal='breakfast';

const BASE_WORKOUTS=[
  {id:'run',icon:'🏃',name:'Running',detail:'Full body cardio',cal:10,tags:['cardio'],rpm:140},
  {id:'pushup',icon:'💪',name:'Push-Ups',detail:'Upper body strength',cal:7,tags:['strength'],rpm:20},
  {id:'squat',icon:'🦵',name:'Squats',detail:'Leg & glute power',cal:8,tags:['strength'],rpm:15},
  {id:'cycling',icon:'🚴',name:'Cycling',detail:'Low impact cardio',cal:9,tags:['cardio'],rpm:80},
  {id:'plank',icon:'🧘',name:'Plank',detail:'Core stability',cal:5,tags:['core'],rpm:1},
  {id:'burpee',icon:'⚡',name:'Burpees',detail:'HIIT full body',cal:14,tags:['hiit'],rpm:10},
  {id:'pullup',icon:'⬆️',name:'Pull-Ups',detail:'Back & bicep',cal:8,tags:['strength'],rpm:8},
  {id:'jumpjack',icon:'🌟',name:'Jumping Jacks',detail:'Warm-up cardio',cal:8,tags:['cardio'],rpm:40},
  {id:'situp',icon:'🔄',name:'Sit-Ups',detail:'Core strength',cal:6,tags:['core'],rpm:20},
];

const FOODS={
  rice:{name:'Rice (1 cup)',cal:206,pro:4,carb:45,fat:0},
  chicken:{name:'Chicken Breast (100g)',cal:165,pro:31,carb:0,fat:3},
  egg:{name:'Egg (1 whole)',cal:78,pro:6,carb:1,fat:5},
  banana:{name:'Banana',cal:105,pro:1,carb:27,fat:0},
  milk:{name:'Milk (1 cup)',cal:149,pro:8,carb:12,fat:8},
  bread:{name:'Bread (1 slice)',cal:79,pro:3,carb:15,fat:1},
  oats:{name:'Oats (50g)',cal:189,pro:7,carb:34,fat:3},
  apple:{name:'Apple',cal:95,pro:0,carb:25,fat:0},
  daal:{name:'Dal (1 bowl)',cal:180,pro:12,carb:30,fat:2},
  roti:{name:'Roti (1 piece)',cal:104,pro:3,carb:20,fat:2},
  whey:{name:'Whey Protein Shake',cal:120,pro:25,carb:3,fat:1},
  almonds:{name:'Almonds (10 pcs)',cal:70,pro:3,carb:2,fat:6},
};

const ACHS=[
  {id:'first',icon:'🎯',name:'First Workout',desc:'Complete first workout',check:()=>UD.totalW>=1},
  {id:'cal100',icon:'🔥',name:'Century Burn',desc:'Burn 100 cal total',check:()=>UD.totalCal>=100},
  {id:'rep100',icon:'💯',name:'Rep Machine',desc:'100+ total reps',check:()=>UD.totalReps>=100},
  {id:'streak3',icon:'🔥',name:'On Fire',desc:'3 day streak',check:()=>(UD.streak||0)>=3},
  {id:'streak7',icon:'🌟',name:'Week Warrior',desc:'7 day streak',check:()=>(UD.streak||0)>=7},
  {id:'food10',icon:'🍎',name:'Mindful Eater',desc:'Log 10 meals',check:()=>(UD.totalMeals||0)>=10},
  {id:'w10',icon:'🏆',name:'Consistent',desc:'10 workouts done',check:()=>UD.totalW>=10},
  {id:'hydrated',icon:'💧',name:'Hydration Hero',desc:'Hit water goal 3 days',check:()=>(UD.waterDays||0)>=3},
  {id:'pr',icon:'🥇',name:'Record Breaker',desc:'Set a personal record',check:()=>Object.keys(UD.PRs||{}).length>=1},
  {id:'allEx',icon:'🎖️',name:'Variety King',desc:'Try all base exercises',check:()=>BASE_WORKOUTS.every(w=>(UD.exDone||[]).includes(w.id))},
];

let selW=null,timerInt=null,timerOn=false,timerSec=0;
let remInt=null;

// ══════════ AUTH ══════════
function switchTab(t){
  document.querySelectorAll('.auth-tab').forEach((el2,i)=>el2.classList.toggle('active',i===(t==='login'?0:1)));
  el('login-form').style.display=t==='login'?'block':'none';
  el('register-form').style.display=t==='register'?'block':'none';
}
function doLogin(){
  const em=v('li-email'),pw=v('li-pass'),err=el('li-err');
  if(!em||!pw){err.textContent='Fill all fields.';return;}
  const u=users.find(x=>x.email===em&&x.password===pw);
  if(!u){err.textContent='Wrong email or password.';return;}
  err.textContent='';loginOK(u);
}
function doRegister(){
  const fn=v('rg-fn'),ln=v('rg-ln'),em=v('rg-em'),pw=v('rg-pw'),
    age=v('rg-age'),gen=v('rg-gen'),wt=v('rg-wt'),ht=v('rg-ht'),gl=v('rg-gl');
  const err=el('rg-err');
  if(!fn||!ln||!em||!pw||!age||!gen||!wt||!ht||!gl){err.textContent='Please fill all fields.';return;}
  if(pw.length<6){err.textContent='Password min 6 chars.';return;}
  if(users.find(x=>x.email===em)){err.textContent='Email already registered.';return;}
  const u={id:Date.now(),fn,ln,email:em,password:pw,age,gender:gen,weight:+wt,height:+ht,goal:gl,calGoal:Math.round(wt*30),joined:new Date().toLocaleDateString()};
  users.push(u);ls('fl_users',users);toast('Welcome '+fn+'! 🎉');loginOK(u);
}
function loginOK(u){
  CU=u;
  UD=lg('fl_data_'+u.id)||{totalCal:0,totalW:0,totalMin:0,totalReps:0,totalMeals:0,streak:0,bestStreak:0,waterDays:0,exDone:[],log:[],flog:[],wtlog:[],targets:[],reminders:[],customEx:[],PRs:{}};
  targets=UD.targets||[];wLog=UD.log||[];fLog=UD.flog||[];
  wtLog=UD.wtlog||[];reminders=UD.reminders||[];customEx=UD.customEx||[];
  el('auth-wrap').style.display='none';el('app').style.display='block';
  if(lg('fl_dark'))document.body.classList.add('dark');
  initApp();
}
function logout(){saveData();clearInterval(remInt);CU=null;resetTimer();el('auth-wrap').style.display='flex';el('app').style.display='none';}
function saveData(){
  if(!CU)return;
  UD.targets=targets;UD.log=wLog;UD.flog=fLog;UD.wtlog=wtLog;
  UD.reminders=reminders;UD.customEx=customEx;
  ls('fl_data_'+CU.id,UD);
  // also update user profile
  const idx=users.findIndex(u=>u.id===CU.id);
  if(idx>=0){users[idx]=CU;ls('fl_users',users);}
}

// ══════════ INIT ══════════
function initApp(){
  const hr=new Date().getHours();
  const grt=hr<12?'Good morning ☀️':hr<17?'Good afternoon 🌤️':'Good evening 🌙';
  el('greeting').textContent=grt+', '+CU.fn+'!';
  el('dash-title').textContent='Hey '+CU.fn+', let\'s go! 💪';
  el('dash-sub').textContent='Goal: '+CU.goal;
  el('user-av').textContent=CU.fn[0].toUpperCase();
  const d=new Date();d.setDate(d.getDate()+30);
  el('tg-date').value=d.toISOString().split('T')[0];
  // Quote
  const q=QUOTES[Math.floor(Math.random()*QUOTES.length)];
  el('quote-box').childNodes[0].textContent='"'+q.q+'"';
  el('quote-auth').textContent='— '+q.a;
  // Pre-fill edit fields
  el('edit-wt').value=CU.weight||'';
  el('edit-ht').value=CU.height||'';
  el('edit-calgoal').value=CU.calGoal||Math.round((CU.weight||70)*30);
  el('edit-gl').value=CU.goal||'Stay Fit';
  buildWorkoutGrid();updateDash();buildTargetsList();updateProfile();buildAch();buildProgress();updateNutrition();buildWater();buildRemList();startReminderCheck();buildWeightLog();buildReport();
}

// ══════════ DARK MODE ══════════
function toggleDark(){
  document.body.classList.toggle('dark');
  ls('fl_dark',document.body.classList.contains('dark')?1:null);
}

// ══════════ DASHBOARD ══════════
function todayWLog(){const t=new Date().toDateString();return wLog.filter(l=>new Date(l.date).toDateString()===t);}
function todayFLog(){const t=new Date().toDateString();return fLog.filter(l=>new Date(l.date).toDateString()===t);}

function updateDash(){
  const tl=todayWLog(),fl2=todayFLog();
  el('d-cal').textContent=Math.round(tl.reduce((s,l)=>s+l.cal,0));
  el('d-food-cal').textContent=Math.round(fl2.reduce((s,l)=>s+(l.cal||0),0));
  el('d-min').textContent=Math.round(tl.reduce((s,l)=>s+l.min,0));
  el('d-streak').textContent=UD.streak||0;
  buildWaterDrops('water-drops-dash',true);
  const dt=el('dash-targets');
  dt.innerHTML=targets.length===0
    ?'<div style="color:var(--sub);font-size:13px;grid-column:span 2;text-align:center;padding:16px;background:var(--card);border-radius:13px;">No targets. Go to 🎯 Targets!</div>'
    :targets.slice(0,4).map(tgCardHTML).join('');
  const al=el('dash-activity');
  al.innerHTML=wLog.length===0
    ?'<div style="color:var(--sub);text-align:center;padding:18px;font-size:13px;">No workouts yet. Start now! 💪</div>'
    :wLog.slice(-6).reverse().map(l=>{
      const w=allWorkouts().find(x=>x.id===l.wid)||{icon:'💪',name:l.wid};
      return`<div class="ai"><div class="aico">${w.icon}</div><div class="ain"><div class="nm">${w.name}</div><div class="dt">${Math.round(l.min)} min · ${l.reps} reps · ${new Date(l.date).toLocaleDateString()}</div></div><div class="acal">🔥 ${Math.round(l.cal)}</div></div>`;
    }).join('');
}

function tgCardHTML(tg){
  const icons={calories:'🔥',workouts:'💪',minutes:'⏱️',weight:'⚖️',protein:'💊',water:'💧'};
  const units={calories:'cal',workouts:'sessions',minutes:'min',weight:'kg',protein:'g',water:'glasses'};
  const cur=getTgCurrent(tg);
  const pct=Math.min(100,Math.round(cur/tg.value*100));
  const col=pct>=100?'#2196f3':pct>=60?'#4caf50':'#ff9800';
  const bclass=pct>=100?'done':pct>=60?'on-track':'behind';
  const btxt=pct>=100?'✓ Done':pct>=60?'On Track':'Behind';
  return`<div class="tc"><div class="th"><div class="tn">${icons[tg.type]||'🎯'} ${tg.type}</div><div class="tbdg ${bclass}">${btxt}</div></div><div class="pb"><div class="pf" style="width:${pct}%;background:${col}"></div></div><div class="pn"><span>${cur} / ${tg.value} ${units[tg.type]||''}</span><span>${pct}%</span></div></div>`;
}

function getTgCurrent(tg){
  const tl=todayWLog(),fl2=todayFLog();
  if(tg.type==='calories') return Math.round(tl.reduce((s,l)=>s+l.cal,0));
  if(tg.type==='minutes') return Math.round(tl.reduce((s,l)=>s+l.min,0));
  if(tg.type==='workouts') return wLog.filter(l=>new Date(l.date)>=wkStart()).length;
  if(tg.type==='weight') return Number(CU.weight)||0;
  if(tg.type==='protein') return Math.round(fl2.reduce((s,l)=>s+(l.pro||0),0));
  if(tg.type==='water') return todayWater();
  return 0;
}
function wkStart(){const d=new Date();d.setDate(d.getDate()-d.getDay());d.setHours(0,0,0,0);return d;}

// ══════════ WORKOUT ══════════
function allWorkouts(){return [...BASE_WORKOUTS,...(customEx||[])];}

function buildWorkoutGrid(){
  el('workout-grid').innerHTML=allWorkouts().map(w=>`<div class="wc" id="wc-${w.id}" onclick="selWorkout('${w.id}')"><div class="wci">${w.icon||'⚡'}</div><div class="wcn">${w.name}</div><div class="wcd">${w.detail||''}</div><div class="wct">${w.tags.map(t=>`<span class="tag ${t}">${t}</span>`).join('')}</div></div>`).join('');
  buildPRRow();
}

function addCustomEx(){
  const nm=v('ce-name'),cal=+v('ce-cal'),rpm=+v('ce-rpm'),cat=v('ce-cat');
  if(!nm||!cal){toast('Enter name and cal/min!');return;}
  const ex={id:'cx'+Date.now(),icon:'⚡',name:nm,detail:'Custom exercise',cal,tags:[cat],rpm:rpm||10};
  if(!customEx)customEx=[];
  customEx.push(ex);UD.customEx=customEx;saveData();buildWorkoutGrid();
  el('ce-name').value='';el('ce-cal').value='';el('ce-rpm').value='';
  toast('Exercise added! 🏋️');
}

function selWorkout(id){
  selW=allWorkouts().find(w=>w.id===id);
  document.querySelectorAll('.wc').forEach(c=>c.classList.remove('sel'));
  el('wc-'+id).classList.add('sel');
  el('sel-name').textContent=selW.name;
  el('sel-icon').textContent=selW.icon||'⚡';
  el('sel-detail').textContent=(selW.detail||'')+' · ~'+selW.cal+' cal/min';
  resetTimer();
}

function startTimer(){
  if(!selW){toast('Select a workout first!');return;}
  if(timerOn)return;timerOn=true;
  timerInt=setInterval(()=>{
    timerSec++;
    const m=Math.floor(timerSec/60),s=timerSec%60;
    el('timer-disp').textContent=(m<10?'0':'')+m+':'+(s<10?'0':'')+s;
    const min=timerSec/60;
    el('live-cal').textContent=Math.round(min*selW.cal);
    el('live-min').textContent=Math.round(min*10)/10;
    el('live-reps').textContent=Math.round(min*selW.rpm);
  },1000);
}
function pauseTimer(){timerOn=false;clearInterval(timerInt);}
function resetTimer(){
  pauseTimer();timerSec=0;
  el('timer-disp').textContent='00:00';
  el('live-cal').textContent='0';el('live-min').textContent='0';el('live-reps').textContent='0';
}

function logWorkout(){
  if(!selW){toast('Pick a workout first!');return;}
  if(timerSec<5){toast('Work out for a bit first! 😄');return;}
  pauseTimer();
  const min=timerSec/60;
  const cal=min*selW.cal,reps=Math.round(min*selW.rpm);
  const entry={wid:selW.id,date:new Date().toISOString(),cal,min,reps};
  wLog.push(entry);
  UD.totalCal=(UD.totalCal||0)+cal;
  UD.totalMin=(UD.totalMin||0)+min;
  UD.totalW=(UD.totalW||0)+1;
  UD.totalReps=(UD.totalReps||0)+reps;
  UD.streak=(UD.streak||0)+1;
  UD.bestStreak=Math.max(UD.bestStreak||0,UD.streak);
  if(!UD.exDone)UD.exDone=[];
  if(!UD.exDone.includes(selW.id))UD.exDone.push(selW.id);
  // PR check
  if(!UD.PRs)UD.PRs={};
  const prKey=selW.id+'_cal';
  if(!UD.PRs[prKey]||cal>UD.PRs[prKey]){UD.PRs[prKey]=cal;toast('🥇 New Personal Record! '+Math.round(cal)+' cal!');}
  else toast('Logged! 🔥 +'+Math.round(cal)+' cal burned!');
  saveData();updateDash();buildProgress();buildPRRow();buildReport();checkAch();resetTimer();
}

function buildPRRow(){
  const prs=UD.PRs||{};
  const rows=BASE_WORKOUTS.slice(0,3).map(w=>{
    const k=w.id+'_cal';const val=prs[k]?Math.round(prs[k]):0;
    return`<div class="pr-card"><div class="pr-val">${val?val+' cal':'—'}</div><div class="pr-lbl">${w.icon} ${w.name}</div><div class="pr-prev">${val?'🏆 Best':'No record yet'}</div></div>`;
  });
  el('pr-row').innerHTML=rows.join('');
}

// ══════════ WATER ══════════
function todayWater(){
  const k='fl_water_'+new Date().toDateString()+'_'+CU.id;
  return parseInt(localStorage.getItem(k)||'0');
}
function setWater(n){
  const k='fl_water_'+new Date().toDateString()+'_'+CU.id;
  localStorage.setItem(k,n);
  if(n>=8&&!UD._wateredToday){UD.waterDays=(UD.waterDays||0)+1;UD._wateredToday=true;saveData();checkAch();}
  buildWater();updateNutrition();updateDash();
}
function resetWater(){const k='fl_water_'+new Date().toDateString()+'_'+CU.id;localStorage.setItem(k,0);UD._wateredToday=false;buildWater();updateNutrition();updateDash();}
function buildWater(){buildWaterDrops('water-drops',false);buildWaterDrops('water-drops-dash',true);}
function buildWaterDrops(containerId,mini){
  const c=el(containerId);if(!c)return;
  const cur=todayWater();
  c.innerHTML='';
  for(let i=1;i<=8;i++){
    const d=document.createElement('span');
    d.className='drop'+(i<=cur?' filled':'');
    d.textContent='💧';d.title=i+' glasses';
    if(mini)d.style.fontSize='18px';
    d.onclick=(()=>{const n=i;return()=>setWater(n===cur?n-1:n);})(i);
    c.appendChild(d);
  }
  if(el('water-lbl'))el('water-lbl').textContent=cur+' / 8 glasses';
  if(el('water-dash-lbl'))el('water-dash-lbl').textContent=cur+' / 8 glasses';
}

// ══════════ NUTRITION ══════════
function setMeal(m,btn){curMeal=m;document.querySelectorAll('.meal-tab').forEach(b=>b.classList.remove('active'));btn.classList.add('active');}
function fillFood(){
  const k=v('food-sel');
  el('custom-food').style.display=k==='custom'?'block':'none';
  if(k&&FOODS[k]){el('food-cal').value=FOODS[k].cal;el('food-pro').value=FOODS[k].pro;}
  else{el('food-cal').value='';el('food-pro').value='';}
}
function addFood(){
  const k=v('food-sel');if(!k){toast('Select a food!');return;}
  let f;
  if(k==='custom'){
    const nm=v('food-cname'),cal=parseInt(v('food-cal')),pro=parseInt(v('food-pro')||0),carb=parseInt(v('food-carb')||0);
    if(!nm||!cal){toast('Enter food name and calories!');return;}
    f={name:nm,cal,pro,carb,fat:0};
  } else {f=FOODS[k];if(!f){toast('Select a valid food!');return;}}
  fLog.push({...f,date:new Date().toISOString(),meal:curMeal});
  UD.totalMeals=(UD.totalMeals||0)+1;
  saveData();updateNutrition();checkAch();
  el('food-sel').value='';el('food-cal').value='';el('food-pro').value='';
  el('custom-food').style.display='none';toast('Added: '+f.name+' 🍽️');
}
function removeFood(i){
  const today=new Date().toDateString();
  const tfl=fLog.filter(l=>new Date(l.date).toDateString()===today);
  const entry=tfl[i];
  const gi=fLog.indexOf(entry);if(gi>=0)fLog.splice(gi,1);
  saveData();updateNutrition();
}
function updateNutrition(){
  const tfl=todayFLog();
  const totalC=Math.round(tfl.reduce((s,l)=>s+(l.cal||0),0));
  const totalP=Math.round(tfl.reduce((s,l)=>s+(l.pro||0),0));
  const totalCb=Math.round(tfl.reduce((s,l)=>s+(l.carb||0),0));
  const totalF=Math.round(tfl.reduce((s,l)=>s+(l.fat||0),0));
  const calGoal=CU.calGoal||Math.round((CU.weight||70)*30);
  const pct=Math.min(1,totalC/calGoal);
  const burned=Math.round(todayWLog().reduce((s,l)=>s+l.cal,0));
  el('cal-eaten').textContent=totalC;
  el('cal-goal-disp').textContent=calGoal;
  el('cal-remain').textContent=Math.max(0,calGoal-totalC);
  el('cal-burned-disp').textContent=burned;
  el('cal-net').textContent=Math.max(0,totalC-burned);
  el('cal-ring').setAttribute('stroke-dashoffset',(276*(1-pct)).toFixed(1));
  el('m-cal').textContent=totalC;el('m-pro').textContent=totalP+'g';el('m-carb').textContent=totalCb+'g';el('m-fat').textContent=totalF+'g';
  const mealIcons={breakfast:'🌅',lunch:'☀️',dinner:'🌙',snack:'🍿'};
  el('food-list').innerHTML=tfl.length===0
    ?'<div style="color:var(--sub);text-align:center;padding:18px;font-size:13px;">No food logged today. Add your meals!</div>'
    :tfl.map((f,i)=>`<div class="food-item"><div class="food-icon">${mealIcons[f.meal]||'🍽️'}</div><div class="food-info"><div class="food-name">${f.name}</div><div class="food-macros">${f.meal||'meal'} · P:${f.pro||0}g C:${f.carb||0}g F:${f.fat||0}g</div></div><div class="food-cal">🔥 ${f.cal}</div><button class="del" onclick="removeFood(${i})">✕</button></div>`).join('');
}

// ══════════ PROGRESS ══════════
function buildProgress(){
  buildHeatmap();buildWeightChart();
  const days=['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
  const calData=[],minData=[],labels=[];
  for(let i=6;i>=0;i--){
    const d=new Date();d.setDate(d.getDate()-i);const ds=d.toDateString();
    labels.push(days[d.getDay()]);
    calData.push(Math.round(wLog.filter(l=>new Date(l.date).toDateString()===ds).reduce((s,l)=>s+l.cal,0)));
    minData.push(Math.round(wLog.filter(l=>new Date(l.date).toDateString()===ds).reduce((s,l)=>s+l.min,0)));
  }
  buildBarChart('cal-chart',calData,labels,'#e94560');
  buildBarChart('min-chart',minData,labels,'#0f3460');
  // Rings
  const tl=todayWLog(),fl2=todayFLog();
  const calGoal=CU.calGoal||Math.round((CU.weight||70)*30);
  setRing('r1',Math.min(1,tl.reduce((s,l)=>s+l.cal,0)/300),'r1v');
  setRing('r2',Math.min(1,tl.reduce((s,l)=>s+l.min,0)/30),'r2v');
  setRing('r3',Math.min(1,fl2.reduce((s,l)=>s+(l.cal||0),0)/calGoal),'r3v');
  el('tot-cal').textContent=Math.round(UD.totalCal||0);
  el('tot-w').textContent=UD.totalW||0;
  el('tot-min').textContent=Math.round(UD.totalMin||0);
  el('best-str').textContent=UD.bestStreak||0;
}

function setRing(id,p,vid){
  el(id).setAttribute('stroke-dashoffset',(226*(1-p)).toFixed(1));
  el(vid).textContent=Math.round(p*100)+'%';
}
function buildBarChart(cid,data,labels,color){
  const max=Math.max(...data,1);
  el(cid).innerHTML=data.map((v2,i)=>`<div class="bar-w"><div class="bar-val">${v2}</div><div class="bar" style="height:${Math.round(v2/max*120)+4}px;background:${color};opacity:${v2>0?0.85:0.2}"></div><div class="bar-lbl">${labels[i]}</div></div>`).join('');
}

function buildHeatmap(){
  const hm=el('heatmap');const lbl=el('hmap-days');
  hm.innerHTML='';
  const days=['S','M','T','W','T','F','S'];
  lbl.innerHTML=days.map(d=>`<span>${d}</span>`).join('');
  for(let i=27;i>=0;i--){
    const d=new Date();d.setDate(d.getDate()-i);const ds=d.toDateString();
    const cals=Math.round(wLog.filter(l=>new Date(l.date).toDateString()===ds).reduce((s,l)=>s+l.cal,0));
    let cls='hday';if(cals>300)cls+=' l3';else if(cals>100)cls+=' l2';else if(cals>0)cls+=' l1';
    const div=document.createElement('div');div.className=cls;div.title=d.toLocaleDateString()+': '+cals+' cal';
    hm.appendChild(div);
  }
}

function buildWeightChart(){
  const svg=el('wt-chart');const lbls=el('wt-chart-labels');
  if(!svg)return;
  const data=wtLog.slice(-12);
  if(data.length<2){svg.innerHTML='<text x="50%" y="50%" text-anchor="middle" fill="#aaa" font-size="12">Log weight in Profile to see trend</text>';lbls.innerHTML='';return;}
  const vals=data.map(d=>d.w);
  const mn=Math.min(...vals)-1,mx=Math.max(...vals)+1;
  const W=svg.clientWidth||300,H=120;
  const pts=data.map((d,i)=>{
    const x=Math.round((i/(data.length-1))*(W-30)+15);
    const y=Math.round(H-((d.w-mn)/(mx-mn||1))*(H-20)-10);
    return{x,y,w:d.w,date:d.date};
  });
  const path=pts.map((p,i)=>i===0?`M${p.x},${p.y}`:`L${p.x},${p.y}`).join(' ');
  svg.innerHTML=`<polyline points="${pts.map(p=>p.x+','+p.y).join(' ')}" fill="none" stroke="#0f3460" stroke-width="2.5" stroke-linejoin="round"/>`
    +pts.map(p=>`<circle cx="${p.x}" cy="${p.y}" r="4" fill="#e94560"><title>${p.w}kg - ${new Date(p.date).toLocaleDateString()}</title></circle>`).join('');
  lbls.innerHTML=data.map(d=>`<span>${new Date(d.date).toLocaleDateString('en',{month:'short',day:'numeric'})}</span>`).join('');
}

// ══════════ WEIGHT LOG ══════════
function logWeight(){
  const w=parseFloat(v('wt-input'));
  if(!w||w<20||w>300){toast('Enter a valid weight!');return;}
  wtLog.push({w,date:new Date().toISOString()});
  CU.weight=w;saveData();buildWeightLog();buildProgress();updateProfile();toast('Weight logged: '+w+' kg ⚖️');
  el('wt-input').value='';
}
function buildWeightLog(){
  const list=el('wt-list');if(!list)return;
  list.innerHTML=wtLog.length===0
    ?'<div style="color:var(--sub);font-size:13px;text-align:center;padding:12px;">No weight entries yet.</div>'
    :wtLog.slice(-7).reverse().map((e,i,arr)=>{
      const prev=arr[i+1];
      const diff=prev?+(e.w-prev.w).toFixed(1):null;
      const diffStr=diff!==null?`<span class="wt-diff ${diff>0?'up':'dn'}">${diff>0?'+':''}${diff}kg</span>`:'';
      return`<div class="wt-item"><div>${new Date(e.date).toLocaleDateString()}</div><div style="display:flex;align-items:center;gap:8px;"><div class="wt-val">${e.w} kg</div>${diffStr}</div></div>`;
    }).join('');
}

// ══════════ TARGETS ══════════
function addTarget(){
  const type=v('tg-type'),val=parseInt(v('tg-val')),date=v('tg-date');
  if(!val||val<=0){toast('Enter a valid goal!');return;}
  if(!date){toast('Set a deadline!');return;}
  targets.push({id:Date.now(),type,value:val,deadline:date});
  saveData();buildTargetsList();updateDash();toast('Target set! 🎯');
}
function delTarget(id){targets=targets.filter(t=>t.id!==id);saveData();buildTargetsList();updateDash();}
function buildTargetsList(){
  const icons={calories:'🔥',workouts:'💪',minutes:'⏱️',weight:'⚖️',protein:'💊',water:'💧'};
  const units={calories:'cal/day',workouts:'sessions/wk',minutes:'min/day',weight:'kg',protein:'g/day',water:'glasses/day'};
  const colors=['#e94560','#0f3460','#ff9800','#9c27b0','#4caf50','#00bcd4'];
  el('targets-list').innerHTML=targets.length===0
    ?'<div style="text-align:center;color:var(--sub);padding:28px;background:var(--card);border-radius:14px;">No targets yet. Add one above!</div>'
    :targets.map((tg,i)=>{
      const cur=getTgCurrent(tg),pct=Math.min(100,Math.round(cur/tg.value*100));
      const col=colors[i%colors.length];
      const dl=Math.round((new Date(tg.deadline)-new Date())/86400000);
      return`<div class="tgc"><div class="tgico">${icons[tg.type]||'🎯'}</div><div class="tgi"><div class="tgn">${tg.type.charAt(0).toUpperCase()+tg.type.slice(1)} Goal</div><div class="tgs">Target: ${tg.value} ${units[tg.type]||''} · ${dl>0?dl+' days left':'Deadline reached'}</div><div class="tgpb"><div class="tgpf" style="width:${pct}%;background:${col}"></div></div></div><div class="tgr"><div class="tgpct">${pct}%</div><div class="tgst">${cur} / ${tg.value}</div><button class="del-btn" onclick="delTarget(${tg.id})">✕</button></div></div>`;
    }).join('');
}

// ══════════ PROFILE ══════════
function updateProfile(){
  el('prof-av').textContent=CU.fn[0].toUpperCase();
  el('prof-nm').textContent=CU.fn+' '+CU.ln;
  el('prof-em').textContent=CU.email;
  el('p-age').textContent=CU.age+' yrs';el('p-gen').textContent=CU.gender;
  el('p-wt').textContent=CU.weight+' kg';el('p-ht').textContent=CU.height+' cm';
  el('p-gl').textContent=CU.goal;el('p-since').textContent=CU.joined||'Today';
  const bmi=CU.weight/((CU.height/100)**2);
  el('bmi-v').textContent=bmi.toFixed(1);
  el('bmi-c').textContent=bmi<18.5?'Underweight':bmi<25?'Normal Weight ✅':bmi<30?'Overweight ⚠️':'Obese ❗';
  el('tot-cal').textContent=Math.round(UD.totalCal||0);
  el('tot-w').textContent=UD.totalW||0;
  el('tot-min').textContent=Math.round(UD.totalMin||0);
  el('best-str').textContent=UD.bestStreak||0;
}
function saveProfile(){
  const wt=parseFloat(v('edit-wt')),ht=parseFloat(v('edit-ht')),cg=parseInt(v('edit-calgoal')),gl=v('edit-gl');
  if(wt)CU.weight=wt;if(ht)CU.height=ht;if(cg)CU.calGoal=cg;if(gl)CU.goal=gl;
  saveData();updateProfile();updateNutrition();toast('Profile updated! ✅');
}

// ══════════ ACHIEVEMENTS ══════════
function buildAch(){el('ach-grid').innerHTML=ACHS.map(a=>`<div class="ach ${a.earned?'earned':''}"><div class="aico2">${a.earned?a.icon:'🔒'}</div><div class="an">${a.name}</div><div class="ad">${a.desc}</div></div>`).join('');}
function checkAch(){ACHS.forEach(a=>{if(!a.earned&&a.check()){a.earned=true;showBadge(a);}});buildAch();}
function showBadge(a){el('badge-name').textContent=a.icon+' '+a.name;const bn=el('badge-notif');bn.classList.add('show');setTimeout(()=>bn.classList.remove('show'),3500);}

// ══════════ REMINDERS ══════════
function addReminder(){
  const t=v('rem-time'),lbl=v('rem-label');
  if(!t){toast('Set a time!');return;}
  reminders.push({id:Date.now(),time:t,label:lbl||'Workout time!'});
  saveData();buildRemList();toast('Reminder set for '+t+' ⏰');
}
function delReminder(id){reminders=reminders.filter(r=>r.id!==id);saveData();buildRemList();}
function buildRemList(){
  el('rem-list').innerHTML=reminders.length===0
    ?'<div style="color:var(--sub);font-size:13px;padding:10px;">No reminders set.</div>'
    :reminders.map(r=>`<div class="rem-item"><div>⏰ <strong>${r.time}</strong> — ${r.label}</div><button onclick="delReminder(${r.id})" style="background:none;border:none;color:#e94560;cursor:pointer;font-size:16px;">✕</button></div>`).join('');
}
function startReminderCheck(){
  clearInterval(remInt);
  remInt=setInterval(()=>{
    const now=new Date();
    const cur=(now.getHours()<10?'0':'')+now.getHours()+':'+(now.getMinutes()<10?'0':'')+now.getMinutes();
    reminders.forEach(r=>{if(r.time===cur&&!r._fired){r._fired=true;toast('⏰ '+r.label);}});
    if(now.getMinutes()===0)reminders.forEach(r=>delete r._fired);
  },15000);
}

// ══════════ REPORT ══════════
function buildReport(){
  const rc=el('report-card');if(!rc)return;
  const days=['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
  let totalCal=0,totalMin=0,totalW2=0,totalFCal=0;
  const rows=[];
  for(let i=6;i>=0;i--){
    const d=new Date();d.setDate(d.getDate()-i);const ds=d.toDateString();
    const wl=wLog.filter(l=>new Date(l.date).toDateString()===ds);
    const fl2=fLog.filter(l=>new Date(l.date).toDateString()===ds);
    const dc=Math.round(wl.reduce((s,l)=>s+l.cal,0));
    const dm=Math.round(wl.reduce((s,l)=>s+l.min,0));
    const dfc=Math.round(fl2.reduce((s,l)=>s+(l.cal||0),0));
    totalCal+=dc;totalMin+=dm;totalW2+=wl.length;totalFCal+=dfc;
    rows.push(`<div style="display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);font-size:13px;"><span>${days[d.getDay()]} ${d.getDate()}</span><span>🔥${dc}cal</span><span>⏱️${dm}min</span><span>🍎${dfc}kcal</span></div>`);
  }
  rc.innerHTML=`<div class="sec" style="margin-bottom:10px;">This Week at a Glance</div>
  <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:12px;">
    <div style="text-align:center;background:#f0f4ff;border-radius:10px;padding:10px;"><div style="font-size:18px;font-weight:900;color:#e94560;">${Math.round(totalCal)}</div><div style="font-size:10px;color:var(--sub);">Cal Burned</div></div>
    <div style="text-align:center;background:#f0f4ff;border-radius:10px;padding:10px;"><div style="font-size:18px;font-weight:900;color:#0f3460;">${totalMin}</div><div style="font-size:10px;color:var(--sub);">Active Min</div></div>
    <div style="text-align:center;background:#f0f4ff;border-radius:10px;padding:10px;"><div style="font-size:18px;font-weight:900;color:#4caf50;">${totalW2}</div><div style="font-size:10px;color:var(--sub);">Workouts</div></div>
    <div style="text-align:center;background:#f0f4ff;border-radius:10px;padding:10px;"><div style="font-size:18px;font-weight:900;color:#ff9800;">${Math.round(totalFCal/7)}</div><div style="font-size:10px;color:var(--sub);">Avg kcal/day</div></div>
  </div>
  ${rows.join('')}`;
}

// ══════════ DATA MGMT ══════════
function clearToday(){
  if(!confirm('Clear today\'s workout and food data?'))return;
  const today=new Date().toDateString();
  wLog=wLog.filter(l=>new Date(l.date).toDateString()!==today);
  fLog=fLog.filter(l=>new Date(l.date).toDateString()!==today);
  saveData();updateDash();updateNutrition();buildProgress();toast('Today\'s data cleared.');
}
function clearAll(){
  if(!confirm('Reset ALL your data? This cannot be undone.'))return;
  UD={totalCal:0,totalW:0,totalMin:0,totalReps:0,totalMeals:0,streak:0,bestStreak:0,waterDays:0,exDone:[],log:[],flog:[],wtlog:[],targets:[],reminders:[],customEx:[],PRs:{}};
  targets=[];wLog=[];fLog=[];wtLog=[];reminders=[];customEx=[];
  saveData();initApp();toast('All data reset.');
}

// ══════════ VIEWS ══════════
function showView(name,btn){
  document.querySelectorAll('.view').forEach(v2=>v2.classList.remove('active'));
  document.querySelectorAll('.nb').forEach(b=>b.classList.remove('active'));
  el('view-'+name).classList.add('active');
  if(btn)btn.classList.add('active');
  if(name==='dashboard')updateDash();
  if(name==='food'){updateNutrition();buildWater();}
  if(name==='progress'){buildProgress();buildAch();}
  if(name==='targets')buildTargetsList();
  if(name==='profile'){updateProfile();buildWeightLog();}
  if(name==='more'){buildRemList();buildReport();}
  if(name==='workout')buildWorkoutGrid();
}

// ══════════ UTILS ══════════
function el(id){return document.getElementById(id);}
function v(id){return el(id)?el(id).value.trim():'';}
function ls(k,d){localStorage.setItem(k,JSON.stringify(d));}
function lg(k){try{return JSON.parse(localStorage.getItem(k));}catch{return null;}}
let toastT;
function toast(msg){const t=el('toast');t.textContent=msg;t.classList.add('show');clearTimeout(toastT);toastT=setTimeout(()=>t.classList.remove('show'),3000);}
</script>
</body>
</html>
