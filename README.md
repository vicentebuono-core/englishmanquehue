# englishmanquehue
English apps for practicing content
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Reported Speech — ESL Interactive App</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
/* ===== RESET & BASE ===== */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0f0e17;--bg2:#1a1830;--bg3:#231f3a;--bg4:#2e2950;
  --accent:#7c5cbf;--accent2:#e94560;--accent3:#00d4aa;--accent4:#f7b731;
  --text:#fffffe;--text2:#b8b5d4;--text3:#7c7a9a;
  --green:#22c55e;--red:#ef4444;--blue:#3b82f6;--orange:#f97316;
  --card:#1e1c35;--border:#3a3660;
  --r-sm:8px;--r-md:12px;--r-lg:16px;--r-xl:24px;
  --shadow:0 4px 24px rgba(0,0,0,.4);
  --font-size-base:16px;
}
.large-text{--font-size-base:22px}
.large-text *:not(.ws-cell):not(.ws-cell *){font-size:calc(var(--font-size-base) * var(--fs-mult, 1)) !important}
.large-text .ws-cell{font-size:11px!important}

.high-contrast{
  --bg:#000!important;--bg2:#000!important;--bg3:#111!important;--bg4:#111!important;
  --text:#fff!important;--text2:#fff!important;--text3:#ffff00!important;
  --card:#111!important;--border:#fff!important;--accent:#ffff00!important;
  --accent2:#ff4444!important;--accent3:#00ffaa!important;--accent4:#ffff00!important;
}
.high-contrast .tab-btn{border:2px solid #fff!important;color:#fff!important}
.high-contrast .tab-btn.active{background:#ffff00!important;color:#000!important}
.high-contrast .opt-btn{border:2px solid #fff!important;color:#fff!important;background:#111!important}
.high-contrast .opt-btn:hover{background:#333!important}
.high-contrast .opt-btn.correct{background:#004400!important;color:#00ff00!important;border-color:#00ff00!important}
.high-contrast .opt-btn.wrong{background:#440000!important;color:#ff4444!important;border-color:#ff4444!important}

html,body{min-height:100vh;background:var(--bg);color:var(--text);font-family:'Nunito',sans-serif;font-size:var(--font-size-base);line-height:1.6;overflow-x:hidden}

/* ===== SCROLLBAR ===== */
::-webkit-scrollbar{width:6px}
::-webkit-scrollbar-track{background:var(--bg2)}
::-webkit-scrollbar-thumb{background:var(--accent);border-radius:3px}

/* ===== ANIMATIONS ===== */
@keyframes fadeIn{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
@keyframes popIn{0%{transform:scale(.5);opacity:0}70%{transform:scale(1.08)}100%{transform:scale(1);opacity:1}}
@keyframes shake{0%,100%{transform:translateX(0)}20%,60%{transform:translateX(-8px)}40%,80%{transform:translateX(8px)}}
@keyframes pulse{0%,100%{transform:scale(1)}50%{transform:scale(1.05)}}
@keyframes glow{0%,100%{box-shadow:0 0 8px var(--accent)}50%{box-shadow:0 0 24px var(--accent),0 0 40px var(--accent)}}
@keyframes slideLeft{from{opacity:0;transform:translateX(30px)}to{opacity:1;transform:translateX(0)}}
@keyframes countdownPulse{0%,100%{transform:scale(1)}50%{transform:scale(1.2)}}
@keyframes confettiFall{0%{transform:translateY(-20px) rotate(0deg);opacity:1}100%{transform:translateY(120px) rotate(720deg);opacity:0}}
@keyframes streakFlash{0%{background:var(--accent4)}50%{background:var(--accent3)}100%{background:var(--accent4)}}
@keyframes timerWarning{0%,100%{background:var(--accent2)}50%{background:#ff6b6b}}
@keyframes levelUp{0%{transform:scale(1) rotate(0deg)}25%{transform:scale(1.3) rotate(-5deg)}50%{transform:scale(1.3) rotate(5deg)}75%{transform:scale(1.1) rotate(-2deg)}100%{transform:scale(1) rotate(0deg)}}

/* ===== LAYOUT ===== */
.app-wrap{max-width:900px;margin:0 auto;padding:0 16px 60px}

/* ===== HEADER ===== */
.app-header{padding:20px 0 10px;text-align:center;position:relative}
.app-title{font-size:2rem;font-weight:900;background:linear-gradient(135deg,#c084fc,#818cf8,#38bdf8);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;letter-spacing:-1px}
.app-subtitle{font-size:.9rem;color:var(--text2);margin-top:4px}

/* ===== ACCESSIBILITY BAR ===== */
.access-bar{display:flex;gap:8px;flex-wrap:wrap;justify-content:center;padding:12px;background:var(--bg2);border-radius:var(--r-lg);margin:10px 0;border:1px solid var(--border)}
.access-btn{padding:6px 14px;border-radius:20px;border:1.5px solid var(--border);background:var(--bg3);color:var(--text2);font-size:.8rem;font-weight:700;cursor:pointer;transition:all .2s;font-family:'Nunito',sans-serif}
.access-btn:hover{border-color:var(--accent);color:var(--text)}
.access-btn.on{background:var(--accent);border-color:var(--accent);color:#fff}
.access-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}

/* ===== TABS ===== */
.tabs-wrap{display:flex;gap:4px;flex-wrap:wrap;background:var(--bg2);border-radius:var(--r-lg);padding:6px;margin:10px 0;border:1px solid var(--border)}
.tab-btn{flex:1;min-width:100px;padding:10px 8px;border-radius:var(--r-md);border:none;background:transparent;color:var(--text2);font-size:.82rem;font-weight:700;cursor:pointer;transition:all .25s;font-family:'Nunito',sans-serif;display:flex;align-items:center;justify-content:center;gap:5px;white-space:nowrap}
.tab-btn:hover{background:var(--bg3);color:var(--text)}
.tab-btn.active{background:linear-gradient(135deg,var(--accent),#6048a8);color:#fff;box-shadow:0 2px 12px rgba(124,92,191,.4)}
.tab-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}

/* ===== LEVEL BADGE ===== */
.level-badge{display:inline-flex;align-items:center;gap:6px;padding:6px 14px;border-radius:20px;font-size:.82rem;font-weight:800;border:2px solid transparent;transition:all .3s}
.level-1{background:rgba(34,197,94,.15);border-color:var(--green);color:var(--green)}
.level-2{background:rgba(59,130,246,.15);border-color:var(--blue);color:var(--blue)}
.level-3{background:rgba(239,68,68,.15);border-color:var(--red);color:var(--red)}
.level-badge.animating{animation:levelUp .6s ease}

/* ===== PROGRESS ===== */
.progress-row{display:flex;align-items:center;gap:10px;margin:10px 0}
.progress-track{flex:1;height:8px;background:var(--bg3);border-radius:4px;overflow:hidden;border:1px solid var(--border)}
.progress-fill{height:100%;border-radius:4px;transition:width .5s cubic-bezier(.4,0,.2,1);background:linear-gradient(90deg,var(--accent),var(--accent3))}
.progress-label{font-size:.78rem;color:var(--text3);min-width:40px;text-align:right;font-weight:700}

/* ===== SCORE BAR ===== */
.score-row{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin:10px 0}
.score-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r-md);padding:10px;text-align:center}
.score-card .val{font-size:1.5rem;font-weight:900;color:var(--accent3)}
.score-card .lbl{font-size:.72rem;color:var(--text3);font-weight:700;text-transform:uppercase;letter-spacing:.5px;margin-top:2px}

/* ===== CARDS ===== */
.q-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r-xl);padding:20px;margin:12px 0;animation:fadeIn .35s ease;box-shadow:var(--shadow)}
.q-label{font-size:.72rem;font-weight:800;text-transform:uppercase;letter-spacing:1px;color:var(--accent);margin-bottom:8px;display:flex;align-items:center;gap:6px}
.q-text{font-size:1rem;font-weight:700;color:var(--text);line-height:1.6;margin-bottom:14px;background:var(--bg3);border-radius:var(--r-md);padding:12px 14px;border-left:4px solid var(--accent)}
.q-ctx{font-size:.9rem;color:var(--accent3);font-weight:700;margin-bottom:12px;padding:8px 12px;background:rgba(0,212,170,.08);border-radius:var(--r-sm);border:1px solid rgba(0,212,170,.2)}

/* ===== OPTIONS ===== */
.opts-grid{display:grid;gap:8px}
.opt-btn{width:100%;background:var(--bg3);border:2px solid var(--border);border-radius:var(--r-md);padding:12px 16px;font-size:.92rem;font-weight:700;color:var(--text);text-align:left;cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:10px;font-family:'Nunito',sans-serif}
.opt-btn:hover:not(:disabled){background:var(--bg4);border-color:var(--accent);transform:translateX(4px)}
.opt-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}
.opt-btn .opt-letter{width:28px;height:28px;border-radius:6px;background:var(--bg4);color:var(--text2);font-size:.78rem;font-weight:800;display:flex;align-items:center;justify-content:center;flex-shrink:0;border:1px solid var(--border)}
.opt-btn.correct{background:rgba(34,197,94,.15)!important;border-color:var(--green)!important;color:var(--green)!important;animation:popIn .3s ease}
.opt-btn.correct .opt-letter{background:var(--green);color:#fff;border-color:var(--green)}
.opt-btn.wrong{background:rgba(239,68,68,.15)!important;border-color:var(--red)!important;color:var(--red)!important;animation:shake .35s ease}
.opt-btn.wrong .opt-letter{background:var(--red);color:#fff;border-color:var(--red)}
.opt-btn:disabled{cursor:default;opacity:.7}

/* ===== FEEDBACK ===== */
.fb-box{padding:12px 16px;border-radius:var(--r-md);font-size:.88rem;font-weight:700;display:none;line-height:1.6;margin-top:8px;animation:popIn .25s ease}
.fb-box.show{display:block}
.fb-box.ok{background:rgba(34,197,94,.12);color:#4ade80;border:1.5px solid var(--green)}
.fb-box.bad{background:rgba(239,68,68,.12);color:#f87171;border:1.5px solid var(--red)}

/* ===== ACTION BTN ===== */
.action-btn{display:none;margin-top:12px;background:linear-gradient(135deg,var(--accent),#6048a8);color:#fff;border:none;border-radius:var(--r-md);padding:11px 24px;font-size:.92rem;font-weight:800;cursor:pointer;transition:all .2s;font-family:'Nunito',sans-serif;box-shadow:0 2px 12px rgba(124,92,191,.3)}
.action-btn:hover{transform:scale(1.03);box-shadow:0 4px 20px rgba(124,92,191,.5)}
.action-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}
.action-btn.show{display:inline-flex;align-items:center;gap:6px;animation:popIn .25s ease}

/* ===== FILL INPUT ===== */
.fill-sentence{font-size:.95rem;color:var(--text);line-height:2.6;background:var(--bg3);border-radius:var(--r-md);padding:14px 16px;border:1.5px solid var(--border);margin:8px 0}
.fill-input{border:2px solid var(--accent);border-radius:6px;padding:4px 10px;font-size:.9rem;font-weight:700;background:var(--bg);color:var(--text);min-width:150px;vertical-align:middle;margin:0 4px;font-family:'Nunito',sans-serif}
.fill-input:focus{outline:none;box-shadow:0 0 0 3px rgba(124,92,191,.3);border-color:var(--accent3)}
.fill-input.ok{border-color:var(--green);background:rgba(34,197,94,.1);color:#4ade80}
.fill-input.bad{border-color:var(--red);background:rgba(239,68,68,.1);color:#f87171}
.check-btn{background:linear-gradient(135deg,var(--accent3),#00a882);color:#000;border:none;border-radius:var(--r-md);padding:9px 18px;font-size:.88rem;font-weight:800;cursor:pointer;margin-top:8px;font-family:'Nunito',sans-serif;transition:all .2s}
.check-btn:hover{transform:scale(1.03)}
.check-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}

/* ===== WORDSEARCH ===== */
.ws-container{overflow-x:auto;margin:10px 0}
.ws-grid-wrap{display:inline-grid;border:2px solid var(--border);border-radius:var(--r-md);overflow:hidden;user-select:none;min-width:300px;width:100%}
.ws-cell{display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:800;color:var(--text2);cursor:pointer;border-right:1px solid rgba(58,54,96,.5);border-bottom:1px solid rgba(58,54,96,.5);aspect-ratio:1;transition:background .1s;font-family:'Space Mono',monospace;min-width:0}
.ws-cell:hover{background:var(--bg4)}
.ws-cell.selecting{background:rgba(124,92,191,.35);color:var(--text)}
.ws-cell.found{background:rgba(0,212,170,.25)!important;color:var(--accent3)!important;font-weight:900}
.ws-cell.found-flash{background:var(--accent3)!important;color:#000!important;animation:popIn .3s ease}
.ws-words-chips{display:flex;flex-wrap:wrap;gap:6px;margin:8px 0}
.ws-chip{padding:4px 10px;border-radius:20px;font-size:.75rem;font-weight:700;background:var(--bg3);color:var(--text2);border:1.5px solid var(--border);transition:all .2s}
.ws-chip.found{background:rgba(0,212,170,.2);color:var(--accent3);border-color:var(--accent3);text-decoration:line-through}

/* ===== VOCAB CARDS ===== */
.vocab-grid{display:grid;gap:10px;margin:8px 0}
.vocab-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r-lg);padding:14px 16px;cursor:pointer;transition:all .2s}
.vocab-card:hover{border-color:var(--accent);transform:translateY(-2px);box-shadow:0 4px 20px rgba(124,92,191,.2)}
.vocab-card .vc-phrase{font-size:.95rem;font-weight:900;color:var(--accent3);margin-bottom:6px;display:flex;align-items:center;gap:8px}
.vocab-card .vc-def{font-size:.82rem;color:var(--text2);margin-bottom:8px;line-height:1.5}
.vocab-card .vc-direct{font-size:.83rem;background:var(--bg3);border-radius:var(--r-sm);padding:8px 10px;color:var(--text2);border-left:3px solid var(--accent);margin-bottom:6px;line-height:1.5}
.vocab-card .vc-reported{font-size:.83rem;background:rgba(0,212,170,.08);border-radius:var(--r-sm);padding:8px 10px;color:var(--accent3);border-left:3px solid var(--accent3);line-height:1.5}

/* ===== MATCHING ===== */
.match-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin:8px 0}
.match-col{display:flex;flex-direction:column;gap:6px}
.match-card{background:var(--bg3);border:2px solid var(--border);border-radius:var(--r-md);padding:10px 12px;font-size:.82rem;font-weight:700;color:var(--text);cursor:pointer;transition:all .2s;text-align:left;line-height:1.4;min-height:50px}
.match-card:hover:not(.matched):not(.disabled){border-color:var(--accent);background:var(--bg4)}
.match-card:focus{outline:3px solid var(--accent3);outline-offset:2px}
.match-card.selected{border-color:var(--accent3);background:rgba(0,212,170,.1);animation:glow 1.5s infinite}
.match-card.matched{border-color:var(--green);background:rgba(34,197,94,.12);color:#4ade80;cursor:default;animation:popIn .35s ease}
.match-card.wrong-flash{border-color:var(--red);background:rgba(239,68,68,.1);animation:shake .35s ease}
.match-card.disabled{cursor:default;opacity:.5}

/* ===== GAME MODE ===== */
.game-arena{background:var(--card);border:1px solid var(--border);border-radius:var(--r-xl);padding:20px;margin:10px 0;box-shadow:var(--shadow)}
.game-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;flex-wrap:wrap;gap:8px}
.lives-row{display:flex;gap:4px}
.life-icon{font-size:1.2rem;transition:all .3s}
.life-icon.lost{filter:grayscale(1);opacity:.3;transform:scale(.8)}
.streak-badge{padding:4px 12px;border-radius:20px;font-size:.78rem;font-weight:800;background:rgba(247,183,49,.15);color:var(--accent4);border:1.5px solid var(--accent4);display:flex;align-items:center;gap:4px;transition:all .3s}
.streak-badge.on-fire{animation:streakFlash .8s infinite;border-color:var(--accent3);color:#000}
.timer-wrap{margin:10px 0}
.timer-track{height:10px;background:var(--bg3);border-radius:5px;overflow:hidden;border:1px solid var(--border)}
.timer-fill{height:100%;border-radius:5px;transition:width .1s linear;background:linear-gradient(90deg,var(--accent3),var(--accent))}
.timer-fill.urgent{background:linear-gradient(90deg,var(--red),var(--accent2));animation:timerWarning .5s infinite}
.timer-num{font-size:1.8rem;font-weight:900;text-align:center;color:var(--accent3);font-family:'Space Mono',monospace;margin:4px 0}
.timer-num.urgent{color:var(--red)}
.game-bubble{background:var(--bg3);border:2px solid var(--accent);border-radius:16px 16px 16px 4px;padding:12px 16px;font-size:1rem;font-weight:700;color:var(--text);margin:10px 0;line-height:1.5;position:relative}
.game-question{font-size:1.05rem;font-weight:800;color:var(--text);margin:8px 0 14px;text-align:center}
.points-popup{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);font-size:3rem;font-weight:900;color:var(--accent4);pointer-events:none;z-index:9999;animation:popIn .2s ease, confettiFall .8s .2s ease forwards;text-shadow:0 0 20px rgba(247,183,49,.5)}
.game-result{text-align:center;padding:20px;animation:fadeIn .5s ease}
.result-score{font-size:4rem;font-weight:900;color:var(--accent3);line-height:1;text-shadow:0 0 30px rgba(0,212,170,.4)}
.result-grade{font-size:1.3rem;font-weight:800;margin:8px 0}
.result-msg{font-size:.9rem;color:var(--text2);margin:6px 0 16px;line-height:1.6}
.leaderboard{background:var(--bg3);border-radius:var(--r-lg);padding:14px;margin:12px 0;border:1px solid var(--border)}
.leaderboard-title{font-size:.85rem;font-weight:800;color:var(--accent);margin-bottom:10px;display:flex;align-items:center;gap:6px;text-transform:uppercase;letter-spacing:.5px}
.lb-row{display:flex;align-items:center;gap:10px;padding:8px 10px;border-radius:var(--r-sm);margin-bottom:4px;background:var(--card);border:1px solid var(--border)}
.lb-rank{font-size:.85rem;font-weight:900;color:var(--accent4);min-width:24px;text-align:center}
.lb-name{font-size:.85rem;font-weight:700;color:var(--text);flex:1}
.lb-score{font-size:.88rem;font-weight:900;color:var(--accent3)}

/* ===== PERFORMANCE REPORT ===== */
.report-wrap{animation:fadeIn .5s ease}
.report-header{text-align:center;padding:20px;background:var(--card);border-radius:var(--r-xl);margin-bottom:14px;border:1px solid var(--border)}
.report-score-big{font-size:3.5rem;font-weight:900;color:var(--accent3)}
.report-grade{font-size:1.2rem;font-weight:800;margin:6px 0}
.report-sections{display:grid;gap:10px}
.report-section{background:var(--card);border-radius:var(--r-lg);padding:14px 16px;border:1px solid var(--border)}
.report-section h3{font-size:.88rem;font-weight:800;text-transform:uppercase;letter-spacing:.5px;margin-bottom:10px;display:flex;align-items:center;gap:6px}
.mistake-item{padding:12px;border-radius:var(--r-md);background:var(--bg3);margin-bottom:8px;border:1px solid var(--border)}
.mistake-item:last-child{margin-bottom:0}
.mi-q{font-size:.83rem;font-weight:700;color:var(--text);margin-bottom:6px}
.mi-yours{display:inline-block;background:rgba(239,68,68,.15);color:#f87171;border-radius:4px;padding:2px 8px;font-size:.8rem;font-weight:700;margin:2px 0}
.mi-correct{display:inline-block;background:rgba(34,197,94,.15);color:#4ade80;border-radius:4px;padding:2px 8px;font-size:.8rem;font-weight:700;margin:2px 0}
.mi-rule{font-size:.8rem;color:var(--blue);margin-top:4px;font-style:italic;line-height:1.5}
.mi-tip{font-size:.8rem;color:var(--accent4);margin-top:4px;line-height:1.5}
.strength-tag{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:20px;font-size:.78rem;font-weight:700;background:rgba(34,197,94,.12);color:#4ade80;border:1px solid rgba(34,197,94,.3);margin:3px}
.weak-tag{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;border-radius:20px;font-size:.78rem;font-weight:700;background:rgba(239,68,68,.12);color:#f87171;border:1px solid rgba(239,68,68,.3);margin:3px}

/* ===== SECTION HEADER ===== */
.section-header{display:flex;align-items:center;justify-content:space-between;margin:12px 0 6px;flex-wrap:wrap;gap:8px}
.section-title{font-size:1rem;font-weight:800;color:var(--text)}
.conf-overlay{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:9998;overflow:hidden}
.conf-piece{position:absolute;top:-20px;width:10px;height:10px;animation:confettiFall 1s ease forwards}

/* ===== REPLAY BTN ===== */
.replay-btn{background:linear-gradient(135deg,var(--accent3),#00a882);color:#000;border:none;border-radius:var(--r-md);padding:12px 28px;font-size:.95rem;font-weight:800;cursor:pointer;margin-top:12px;font-family:'Nunito',sans-serif;transition:all .2s;display:inline-flex;align-items:center;gap:6px}
.replay-btn:hover{transform:scale(1.04)}
.replay-btn:focus{outline:3px solid var(--accent3);outline-offset:2px}
.save-score-btn{background:linear-gradient(135deg,var(--accent),#6048a8);color:#fff;border:none;border-radius:var(--r-md);padding:10px 22px;font-size:.88rem;font-weight:800;cursor:pointer;margin:6px;font-family:'Nunito',sans-serif;transition:all .2s}
.save-score-btn:hover{transform:scale(1.03)}

/* ===== CLOZE SPECIFIC ===== */
.cloze-opts{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:8px;margin-top:10px}

/* ===== RESPONSIVE ===== */
@media(max-width:600px){
  .match-grid{grid-template-columns:1fr}
  .score-row{grid-template-columns:repeat(3,1fr)}
  .tab-btn{font-size:.7rem;padding:8px 4px;min-width:60px}
  .app-title{font-size:1.5rem}
  .ws-cell{font-size:10px}
}
</style>
</head>
<body>
<div id="confetti-overlay" class="conf-overlay"></div>
<div class="app-wrap">

<!-- HEADER -->
<div class="app-header">
  <div class="app-title">✨ Reported Speech Lab</div>
  <div class="app-subtitle">10th Grade ESL · Interactive Practice · All Levels</div>
</div>

<!-- ACCESSIBILITY -->
<div class="access-bar" role="toolbar" aria-label="Accessibility options">
  <span style="font-size:.8rem;color:var(--text3);font-weight:700">⚙️ Accessibility:</span>
  <button class="access-btn" id="btn-tts" onclick="toggleTTS()" aria-pressed="false">🔊 Read Aloud</button>
  <button class="access-btn" id="btn-large" onclick="toggleLarge()" aria-pressed="false">🔤 Larger Text</button>
  <button class="access-btn" id="btn-hc" onclick="toggleHC()" aria-pressed="false">🌗 High Contrast</button>
  <button class="access-btn" onclick="stopSpeech()">⏹ Stop Audio</button>
</div>

<!-- TABS -->
<div class="tabs-wrap" role="tablist">
  <button class="tab-btn active" id="tab-vocab" onclick="switchTab('vocab')" role="tab">📚 Vocabulary</button>
  <button class="tab-btn" id="tab-cloze" onclick="switchTab('cloze')" role="tab">✏️ Cloze</button>
  <button class="tab-btn" id="tab-mcq" onclick="switchTab('mcq')" role="tab">✅ Grammar</button>
  <button class="tab-btn" id="tab-fill" onclick="switchTab('fill')" role="tab">📝 Fill In</button>
  <button class="tab-btn" id="tab-ws" onclick="switchTab('ws')" role="tab">🔍 Wordsearch</button>
  <button class="tab-btn" id="tab-game" onclick="switchTab('game')" role="tab">🎮 Game Mode</button>
  <button class="tab-btn" id="tab-report" onclick="switchTab('report')" role="tab">📊 My Report</button>
</div>

<!-- PANES -->
<div id="pane-vocab" class="pane"></div>
<div id="pane-cloze" class="pane" style="display:none"></div>
<div id="pane-mcq" class="pane" style="display:none"></div>
<div id="pane-fill" class="pane" style="display:none"></div>
<div id="pane-ws" class="pane" style="display:none"></div>
<div id="pane-game" class="pane" style="display:none"></div>
<div id="pane-report" class="pane" style="display:none"></div>

</div><!-- end app-wrap -->

<script>
/* ============================================================
   GLOBAL STATE
============================================================ */
var synth = window.speechSynthesis;
var ttsOn = false, largeOn = false, hcOn = false;
var TRACKER = { attempts:0, correct:0, mistakes:[] };
function TRACKER_record(isCorrect, mistakeObj) {
  TRACKER.attempts++;
  if (isCorrect) { TRACKER.correct++; }
  else { TRACKER.mistakes.push(mistakeObj); }
}
function TRACKER_reset() { TRACKER.attempts=0; TRACKER.correct=0; TRACKER.mistakes=[]; }
var leaderboard = [];

function speak(t) {
  if (!ttsOn || !synth) return;
  synth.cancel();
  var u = new SpeechSynthesisUtterance(t);
  u.rate = 0.88; u.lang = 'en-US';
  synth.speak(u);
}
function stopSpeech() { if (synth) synth.cancel(); }
function toggleTTS() {
  ttsOn = !ttsOn;
  var b = document.getElementById('btn-tts');
  b.classList.toggle('on', ttsOn);
  b.setAttribute('aria-pressed', ttsOn);
  if (ttsOn) speak('Read aloud is now on.');
}
function toggleLarge() {
  largeOn = !largeOn;
  document.body.classList.toggle('large-text', largeOn);
  var b = document.getElementById('btn-large');
  b.classList.toggle('on', largeOn);
  b.setAttribute('aria-pressed', largeOn);
}
function toggleHC() {
  hcOn = !hcOn;
  document.body.classList.toggle('high-contrast', hcOn);
  var b = document.getElementById('btn-hc');
  b.classList.toggle('on', hcOn);
  b.setAttribute('aria-pressed', hcOn);
}

function switchTab(name) {
  var panes = ['vocab','cloze','mcq','fill','ws','game','report'];
  panes.forEach(function(p) {
    document.getElementById('pane-'+p).style.display = p===name ? 'block' : 'none';
    document.getElementById('tab-'+p).classList.toggle('active', p===name);
  });
  if (name === 'report') renderReport();
}

/* ============================================================
   VOCABULARY DATA
============================================================ */
var VOCAB = [
  {
    phrase:'agree',
    emoji:'🤝',
    def:'To say you share the same opinion or accept something.',
    direct:'"Yes, the homework was too difficult," said Ana.',
    reported:'Ana agreed that the homework was too difficult.'
  },
  {
    phrase:'deny',
    emoji:'🙅',
    def:'To say that something is NOT true; to refuse to accept a fact.',
    direct:'"I did NOT break the window," said Marco.',
    reported:'Marco denied breaking the window.'
  },
  {
    phrase:'refuse',
    emoji:'🚫',
    def:'To say that you will NOT do something.',
    direct:'"I won\'t clean the classroom," said the student.',
    reported:'The student refused to clean the classroom.'
  },
  {
    phrase:'report',
    emoji:'📋',
    def:'To tell someone officially or publicly about something.',
    direct:'"There is a fire in the building!" said the guard.',
    reported:'The guard reported that there was a fire in the building.'
  },
  {
    phrase:'inform',
    emoji:'ℹ️',
    def:'To give someone facts or information about something.',
    direct:'"The bus will be late today," said the driver.',
    reported:'The driver informed them that the bus would be late that day.'
  },
  {
    phrase:'confirm',
    emoji:'✅',
    def:'To say that something is definitely true or will happen.',
    direct:'"Yes, the exam is on Friday," said the teacher.',
    reported:'The teacher confirmed that the exam was on Friday.'
  },
  {
    phrase:'admit',
    emoji:'🤦',
    def:'To confess that something is true, especially something bad.',
    direct:'"I forgot to do my homework," said Diego.',
    reported:'Diego admitted that he had forgotten to do his homework.'
  },
  {
    phrase:'argue',
    emoji:'💬',
    def:'To express a strong opinion and give reasons for it.',
    direct:'"The rule is completely unfair," said the students.',
    reported:'The students argued that the rule was completely unfair.'
  },
  {
    phrase:'insist',
    emoji:'👊',
    def:'To say something very firmly and repeatedly.',
    direct:'"You MUST wear a helmet," said the coach.',
    reported:'The coach insisted that they had to wear a helmet.'
  },
  {
    phrase:'claim',
    emoji:'🗣️',
    def:'To say something is true, sometimes without strong proof.',
    direct:'"I finished the exam first," said Roberto.',
    reported:'Roberto claimed that he had finished the exam first.'
  },
  {
    phrase:'point out',
    emoji:'☝️',
    def:'To mention or draw attention to a fact or detail.',
    direct:'"There is a mistake on page 5," said the student.',
    reported:'The student pointed out that there was a mistake on page 5.'
  },
  {
    phrase:'shout at the top of one\'s voice',
    emoji:'📢',
    def:'To yell as loudly as possible, usually in panic or excitement.',
    direct:'"WATCH OUT FOR THE CAR!" screamed the woman.',
    reported:'The woman shouted at the top of her voice that they should watch out for the car.'
  },
  {
    phrase:'gossip',
    emoji:'🤫',
    def:'To talk informally about other people\'s private lives.',
    direct:'"Did you hear that Sofia got a new boyfriend?" she whispered.',
    reported:'She gossiped that Sofia had got a new boyfriend.'
  },
  {
    phrase:'cry out in surprise',
    emoji:'😱',
    def:'To suddenly exclaim because you are shocked or astonished.',
    direct:'"Oh no! I left my phone at home!" said Lucas.',
    reported:'Lucas cried out in surprise that he had left his phone at home.'
  },
  {
    phrase:'mutter under one\'s breath',
    emoji:'😤',
    def:'To speak quietly to yourself, usually when annoyed.',
    direct:'"This is so boring," said the boy quietly under his breath.',
    reported:'The boy muttered under his breath that it was so boring.'
  },
  {
    phrase:'boast proudly',
    emoji:'😎',
    def:'To talk very proudly about your own achievements.',
    direct:'"I scored the winning goal in the final!" said Carlos.',
    reported:'Carlos boasted proudly that he had scored the winning goal in the final.'
  },
  {
    phrase:'cheer excitedly',
    emoji:'🎉',
    def:'To shout with joy and excitement about something positive.',
    direct:'"WE WON THE CHAMPIONSHIP!" shouted the team.',
    reported:'The team cheered excitedly that they had won the championship.'
  },
  {
    phrase:'complain bitterly',
    emoji:'😠',
    def:'To express strong dissatisfaction or unhappiness about something.',
    direct:'"This food is absolutely terrible!" said the customer.',
    reported:'The customer complained bitterly that the food was absolutely terrible.'
  },
  {
    phrase:'quarrel fiercely',
    emoji:'⚡',
    def:'To argue very aggressively and angrily with someone.',
    direct:'"You NEVER listen to me!" she shouted at him.',
    reported:'She quarrelled fiercely with him, saying he never listened to her.'
  },
  {
    phrase:'whisper softly',
    emoji:'🌙',
    def:'To speak in a very quiet, gentle voice, close to someone.',
    direct:'"I love you," he said quietly to her.',
    reported:'He whispered softly that he loved her.'
  }
];

/* ============================================================
   QUESTION BANKS — 3 LEVELS EACH
============================================================ */

// ---- CLOZE QUESTIONS ----
var CLOZE_BANK = {
  1: [
    {
      sentence: '"Yes, this book is really interesting," said Mia.',
      context: 'Mia ___ that the book was really interesting.',
      options: ['agreed','denied','refused','shouted'],
      answer: 'agreed',
      rule: '"Agreed" is used when someone says they think something is true or good.'
    },
    {
      sentence: '"I did NOT steal the money!" said Pedro.',
      context: 'Pedro ___ stealing the money.',
      options: ['denied','admitted','confirmed','argued'],
      answer: 'denied',
      rule: '"Denied" is followed by a gerund (-ing). It means saying something is NOT true.'
    },
    {
      sentence: '"I won\'t do the dishes," said Tim.',
      context: 'Tim ___ to do the dishes.',
      options: ['refused','agreed','insisted','informed'],
      answer: 'refused',
      rule: '"Refused" is followed by "to + infinitive". It expresses a firm "no".'
    },
    {
      sentence: '"The meeting starts at 9 am," the secretary said.',
      context: 'The secretary ___ them that the meeting started at 9 am.',
      options: ['informed','gossiped','denied','argued'],
      answer: 'informed',
      rule: '"Informed" means giving someone official or important facts.'
    },
    {
      sentence: '"Yes, your application was successful," said the manager.',
      context: 'The manager ___ that our application had been successful.',
      options: ['confirmed','denied','quarrelled','muttered'],
      answer: 'confirmed',
      rule: '"Confirmed" means saying something is definitely true or official.'
    }
  ],
  2: [
    {
      sentence: '"I forgot to bring my homework today," said Luis, looking embarrassed.',
      context: 'Luis ___ that he had forgotten to bring his homework that day.',
      options: ['admitted','boasted proudly','cheered excitedly','denied'],
      answer: 'admitted',
      rule: '"Admitted" is used when someone confesses to something they did wrong, especially reluctantly.'
    },
    {
      sentence: '"This rule is unfair and should be changed," said the class representative.',
      context: 'The class representative ___ that the rule was unfair and should be changed.',
      options: ['argued','whispered softly','gossiped','cheered excitedly'],
      answer: 'argued',
      rule: '"Argued" is used when someone gives strong reasons for their position or opinion.'
    },
    {
      sentence: '"You MUST wear your seatbelt at ALL times," said the driving instructor firmly.',
      context: 'The driving instructor ___ that they had to wear their seatbelts at all times.',
      options: ['insisted','whispered softly','gossiped','admitted'],
      answer: 'insisted',
      rule: '"Insisted" means saying something firmly and refusing to change your position.'
    },
    {
      sentence: '"I scored 100% on every single test this year," said Valentina.',
      context: 'Valentina ___ that she had scored 100% on every test that year.',
      options: ['boasted proudly','muttered under her breath','denied','refused'],
      answer: 'boasted proudly',
      rule: '"Boasted proudly" shows the speaker is talking about their achievements with pride and self-satisfaction.'
    },
    {
      sentence: '"Did you know that Sofia has a new boyfriend?" she told everyone at lunch.',
      context: 'She ___ that Sofia had a new boyfriend.',
      options: ['gossiped','confirmed','pointed out','reported'],
      answer: 'gossiped',
      rule: '"Gossiped" means sharing informal, personal information about others — often private news.'
    }
  ],
  3: [
    {
      sentence: '"HELP! THERE\'S A FIRE UPSTAIRS!" screamed the boy.',
      context: 'The boy ___ that there was a fire upstairs.',
      options: ['shouted at the top of his voice','whispered softly','gossiped','muttered under his breath'],
      answer: 'shouted at the top of his voice',
      rule: '"Shouted at the top of one\'s voice" indicates extreme urgency or panic — the loudest possible shout.'
    },
    {
      sentence: '"Oh my goodness! I can\'t believe I won first prize!" exclaimed Clara.',
      context: 'Clara ___ that she couldn\'t believe she had won first prize.',
      options: ['cried out in surprise','whispered softly','muttered under her breath','complained bitterly'],
      answer: 'cried out in surprise',
      rule: '"Cried out in surprise" is used for sudden, involuntary exclamations of shock or amazement.'
    },
    {
      sentence: '"This is completely ridiculous," the student said very quietly, clearly annoyed.',
      context: 'The student ___ that it was completely ridiculous.',
      options: ['muttered under their breath','shouted at the top of their voice','cheered excitedly','confirmed'],
      answer: 'muttered under their breath',
      rule: '"Muttered under one\'s breath" shows the speaker is annoyed but speaking so quietly others can barely hear.'
    },
    {
      sentence: '"YOU NEVER HELP ME WITH ANYTHING!" she screamed at her brother.',
      context: 'She ___ with her brother, saying he never helped her with anything.',
      options: ['quarrelled fiercely','whispered softly','cheered excitedly','agreed'],
      answer: 'quarrelled fiercely',
      rule: '"Quarrelled fiercely" shows an intense, angry argument — "fiercely" emphasizes how aggressive it was.'
    },
    {
      sentence: '"Look, on page 3 there is a typo in the title," the editor told the publisher.',
      context: 'The editor ___ that there was a typo in the title on page 3.',
      options: ['pointed out','muttered under their breath','boasted proudly','cheered excitedly'],
      answer: 'pointed out',
      rule: '"Pointed out" means drawing someone\'s attention to a specific fact or detail — neutral and informative.'
    }
  ]
};

// ---- MCQ GRAMMAR QUESTIONS ----
var MCQ_BANK = {
  1: [
    {
      direct: '"I am happy," said Tom.',
      context: 'Tom said that he ___',
      options: ['is happy.', 'was happy.', 'were happy.', 'has been happy.'],
      answer: 1,
      tip: 'Present simple "am" → past simple "was" (tense backshift). "I" → "he" (pronoun change).',
      rule: 'Tense backshift: present simple → past simple.'
    },
    {
      direct: '"She studies every day," said the teacher.',
      context: 'The teacher said that she ___',
      options: ['studies every day.', 'studied every day.', 'study every day.', 'is studying every day.'],
      answer: 1,
      tip: 'Present simple "studies" → past simple "studied".',
      rule: 'Tense backshift: present simple → past simple.'
    },
    {
      direct: '"I will help you," said Maria.',
      context: 'Maria said that she ___',
      options: ['will help me.', 'would help me.', 'can help me.', 'could help me.'],
      answer: 1,
      tip: '"will" → "would" in reported speech. "I" → "she", "you" → "me".',
      rule: 'Modal backshift: will → would.'
    },
    {
      direct: '"We are playing football," they said.',
      context: 'They said that they ___',
      options: ['are playing football.', 'were playing football.', 'played football.', 'have played football.'],
      answer: 1,
      tip: 'Present continuous "are playing" → past continuous "were playing".',
      rule: 'Tense backshift: present continuous → past continuous.'
    },
    {
      direct: '"I can swim," said the child.',
      context: 'The child said that she ___',
      options: ['can swim.', 'could swim.', 'will swim.', 'would swim.'],
      answer: 1,
      tip: '"can" → "could" in reported speech.',
      rule: 'Modal backshift: can → could.'
    }
  ],
  2: [
    {
      direct: '"I have finished my homework," said Ana.',
      context: 'Ana said that she ___',
      options: ['has finished her homework.', 'had finished her homework.', 'finished her homework.', 'have finished her homework.'],
      answer: 1,
      tip: 'Present perfect "have finished" → past perfect "had finished". "my" → "her".',
      rule: 'Tense backshift: present perfect → past perfect. Pronoun: my → her.'
    },
    {
      direct: '"I am going to the cinema tomorrow," said Luis.',
      context: 'Luis said that he ___',
      options: ['is going to the cinema tomorrow.', 'was going to the cinema the next day.', 'went to the cinema tomorrow.', 'will go to the cinema the next day.'],
      answer: 1,
      tip: '"tomorrow" → "the next day". "am going" → "was going". "I" → "he".',
      rule: 'Time expression: tomorrow → the next day. Tense backshift + pronoun change.'
    },
    {
      direct: '"Do you understand the lesson?" the teacher asked.',
      context: 'The teacher asked if I ___',
      options: ['understood the lesson.', 'understand the lesson.', 'did understand the lesson.', 'understood that lesson.'],
      answer: 0,
      tip: 'Yes/no questions use "if" + statement word order. "understand" → "understood".',
      rule: 'Reported question: "if" + statement word order. Tense backshift.'
    },
    {
      direct: '"I saw the film last night," said Sofia.',
      context: 'Sofia said she ___',
      options: ['saw the film last night.', 'had seen the film the night before.', 'has seen the film last night.', 'saw the film the night before.'],
      answer: 1,
      tip: 'Past simple "saw" → past perfect "had seen". "last night" → "the night before".',
      rule: 'Tense backshift: past simple → past perfect. Time expression: last night → the night before.'
    },
    {
      direct: '"My parents are coming today," said Marco.',
      context: 'Marco said that his parents ___',
      options: ['are coming today.', 'were coming that day.', 'were coming today.', 'came that day.'],
      answer: 1,
      tip: '"are coming" → "were coming". "today" → "that day". "my" → "his".',
      rule: 'Backshift + time change: today → that day. Pronoun: my → his.'
    }
  ],
  3: [
    {
      direct: '"I have been waiting here for two hours!" complained Elena.',
      context: 'Elena complained that she ___',
      options: ['has been waiting there for two hours.', 'had been waiting there for two hours.', 'was waiting there for two hours.', 'waited there for two hours.'],
      answer: 1,
      tip: 'Present perfect continuous "have been waiting" → past perfect continuous "had been waiting". "here" → "there".',
      rule: 'Tense backshift: present perfect continuous → past perfect continuous. Place: here → there.'
    },
    {
      direct: '"Where did you find my keys?" she asked him.',
      context: 'She asked him where ___',
      options: ['did he find her keys.', 'he had found her keys.', 'he found her keys.', 'he has found her keys.'],
      answer: 1,
      tip: 'Wh- questions: use question word + statement word order. Past simple "found" → past perfect "had found".',
      rule: 'Reported wh-question: question word + statement order. Tense backshift to past perfect.'
    },
    {
      direct: '"I can\'t come to the party because I must study," said Roberto.',
      context: 'Roberto said he ___',
      options: ["can't come because he must study.", "couldn't come because he had to study.", "couldn't come because he must study.", "can't come because he had to study."],
      answer: 1,
      tip: '"can\'t" → "couldn\'t"; "must" → "had to" (both modal backshift). "I" → "he".',
      rule: 'Double modal backshift: can\'t → couldn\'t, must → had to.'
    },
    {
      direct: '"We were studying when the electricity went off," said the students.',
      context: 'The students said they ___',
      options: ['were studying when the electricity had gone off.', 'had been studying when the electricity had gone off.', 'studied when the electricity went off.', 'had been studying when the electricity went off.'],
      answer: 1,
      tip: 'Past continuous "were studying" → past perfect continuous "had been studying". The completed action "went off" → "had gone off".',
      rule: 'Complex backshift: past continuous → past perfect continuous; past simple → past perfect.'
    },
    {
      direct: '"I will have finished this project by next Friday," the engineer told her boss.',
      context: 'The engineer told her boss that she ___',
      options: ['will have finished the project by next Friday.', 'would have finished the project by the following Friday.', 'would finish the project by the following Friday.', 'had finished the project by the following Friday.'],
      answer: 1,
      tip: '"will have finished" → "would have finished" (future perfect → conditional perfect). "next Friday" → "the following Friday".',
      rule: 'Future perfect backshift: will have + past participle → would have + past participle.'
    }
  ]
};

// ---- FILL IN QUESTIONS ----
var FILL_BANK = {
  1: [
    {
      direct: '"I am tired," said Carlos.',
      before: 'Carlos said that he ',
      blank: 'was tired',
      after: '.',
      hint: 'am tired → ?',
      rule: '"am" (present simple) → "was" (past simple). "I" → "he".'
    },
    {
      direct: '"She loves chocolate," said the boy.',
      before: 'The boy said that she ',
      blank: 'loved chocolate',
      after: '.',
      hint: 'loves → ?',
      rule: 'Present simple "loves" → past simple "loved". No pronoun change here.'
    },
    {
      direct: '"I can help you," said María.',
      before: 'María said she ',
      blank: 'could help',
      after: ' me.',
      hint: 'can help → ?',
      rule: '"can" → "could". "I" → "she", "you" → "me".'
    },
    {
      direct: '"We are watching TV," they said.',
      before: 'They said they ',
      blank: 'were watching',
      after: ' TV.',
      hint: 'are watching → ?',
      rule: 'Present continuous "are watching" → past continuous "were watching".'
    },
    {
      direct: '"I will call you tomorrow," said Lucas.',
      before: 'Lucas said he ',
      blank: 'would call',
      after: ' me the next day.',
      hint: 'will call → ?',
      rule: '"will call" → "would call". "tomorrow" → "the next day".'
    }
  ],
  2: [
    {
      direct: '"I have already eaten lunch," said Camila.',
      before: 'Camila said she ',
      blank: 'had already eaten',
      after: ' lunch.',
      hint: 'have eaten → ?',
      rule: 'Present perfect "have eaten" → past perfect "had eaten". "I" → "she".'
    },
    {
      direct: '"My sister is coming today," said Pedro.',
      before: 'Pedro said his sister ',
      blank: 'was coming',
      after: ' that day.',
      hint: 'is coming → ? (and today → ?)',
      rule: '"is coming" → "was coming". "today" → "that day". "my" → "his".'
    },
    {
      direct: '"I saw Diego yesterday," said Elena.',
      before: 'Elena said she ',
      blank: 'had seen',
      after: ' Diego the day before.',
      hint: 'saw → ? (past simple → past perfect)',
      rule: 'Past simple "saw" → past perfect "had seen". "yesterday" → "the day before".'
    },
    {
      direct: '"I can\'t find my keys," said Roberto.',
      before: 'Roberto said he ',
      blank: "couldn't find",
      after: ' his keys.',
      hint: "can't find → ?",
      rule: '"can\'t" → "couldn\'t". "my" → "his".'
    },
    {
      direct: '"We have been studying for three hours," said the students.',
      before: 'The students said they ',
      blank: 'had been studying',
      after: ' for three hours.',
      hint: 'have been studying → ?',
      rule: 'Present perfect continuous "have been studying" → past perfect continuous "had been studying".'
    }
  ],
  3: [
    {
      direct: '"I have been working on this project since Monday," said the teacher.',
      before: 'The teacher said she ',
      blank: 'had been working',
      after: ' on that project since Monday.',
      hint: 'have been working → ? (and this → ?)',
      rule: 'Present perfect continuous → past perfect continuous. "this" → "that".'
    },
    {
      direct: '"I will have completed the assignment by next week," said Ana.',
      before: 'Ana said she ',
      blank: 'would have completed',
      after: ' the assignment by the following week.',
      hint: 'will have completed → ? (future perfect → ?)',
      rule: 'Future perfect "will have completed" → conditional perfect "would have completed".'
    },
    {
      direct: '"I must leave now," said the visitor.',
      before: 'The visitor said he ',
      blank: 'had to leave',
      after: ' then.',
      hint: 'must leave → ? (now → ?)',
      rule: '"must" → "had to". "now" → "then".'
    },
    {
      direct: '"Where can I find the library?" the student asked.',
      before: 'The student asked where ',
      blank: 'they could find',
      after: ' the library.',
      hint: 'can I find → ? (question word + statement order)',
      rule: 'Wh-question becomes a statement. "can" → "could". "I" → "they". No inversion.'
    },
    {
      direct: '"I was reading when the alarm went off," said Mr. García.',
      before: 'Mr. García said he ',
      blank: 'had been reading',
      after: ' when the alarm had gone off.',
      hint: 'was reading → ? (past continuous → ?)',
      rule: 'Past continuous "was reading" → past perfect continuous "had been reading".'
    }
  ]
};

// ---- GAME MODE QUESTIONS (all levels, randomised) ----
var GAME_QUESTIONS = [
  {level:1, direct:'"I am cold," said Julia.', q:'Julia said that she ___',opts:['is cold.','was cold.','were cold.'],ans:1,rule:'am → was (tense backshift)'},
  {level:1, direct:'"I will help," said Tom.', q:'Tom said he ___',opts:['will help.','would help.','could help.'],ans:1,rule:'will → would (modal backshift)'},
  {level:1, direct:'"We can swim," they said.', q:'They said they ___',opts:['can swim.','could swim.','were swimming.'],ans:1,rule:'can → could (modal backshift)'},
  {level:1, direct:'"I love music," said Mia.', q:'Mia said she ___',opts:['loves music.','loved music.','has loved music.'],ans:1,rule:'present simple → past simple'},
  {level:1, direct:'"She is reading," said Dan.', q:'Dan said she ___',opts:['is reading.','was reading.','had read.'],ans:1,rule:'present continuous → past continuous'},
  {level:2, direct:'"I have finished," said Rosa.', q:'Rosa said she ___',opts:['has finished.','had finished.','was finishing.'],ans:1,rule:'present perfect → past perfect'},
  {level:2, direct:'"I saw him yesterday," said Pedro.', q:'Pedro said he ___',opts:['saw him yesterday.','had seen him the day before.','saw him the day before.'],ans:1,rule:'past simple → past perfect; yesterday → the day before'},
  {level:2, direct:'"My sister is here today," said Luis.', q:'Luis said his sister ___',opts:['is here today.','was there that day.','was here today.'],ans:1,rule:'time expression today → that day; here → there'},
  {level:2, direct:'"I must go now," said Ana.', q:'Ana said she ___',opts:['must go then.','had to go then.','would go now.'],ans:1,rule:'must → had to; now → then'},
  {level:2, direct:'"Where do you live?" she asked.', q:'She asked where ___',opts:['do I live.','I lived.','did I live.'],ans:1,rule:'wh-question → statement word order + backshift'},
  {level:3, direct:'"I have been waiting for hours," she complained.', q:'She complained that she ___',opts:['has been waiting for hours.','had been waiting for hours.','was waiting for hours.'],ans:1,rule:'present perfect continuous → past perfect continuous'},
  {level:3, direct:'"I can\'t come because I must study," said Marco.', q:'Marco said he ___',opts:["can't come because he must study.","couldn't come because he had to study.","couldn't come because he must study."],ans:1,rule:"can't → couldn't; must → had to (double modal backshift)"},
  {level:3, direct:'"We were eating when the bell rang," they said.', q:'They said they ___',opts:['were eating when the bell rang.','had been eating when the bell had rung.','ate when the bell rang.'],ans:1,rule:'past continuous → past perfect continuous; past simple → past perfect'},
  {level:3, direct:'"I will have finished by Friday," said the student.', q:'The student said he ___',opts:['will have finished by Friday.','would have finished by the following Friday.','had finished by Friday.'],ans:1,rule:'future perfect → conditional perfect; Friday → the following Friday'},
  {level:3, direct:'"Did you see what happened?" she asked.', q:'She asked whether ___',opts:['did I see what had happened.','I had seen what had happened.','I saw what happened.'],ans:1,rule:'yes/no question → "whether" + statement order + past perfect'}
];

/* ============================================================
   ADAPTIVE DIFFICULTY ENGINE
============================================================ */
var diffState = {
  level: 1,
  streak: 0,
  wrongStreak: 0
};

function updateDifficulty(correct) {
  if (correct) {
    diffState.wrongStreak = 0;
    diffState.streak++;
    if (diffState.streak >= 2 && diffState.level < 3) {
      diffState.level++;
      diffState.streak = 0;
      showLevelChange(true);
    }
  } else {
    diffState.streak = 0;
    diffState.wrongStreak++;
    if (diffState.wrongStreak >= 2 && diffState.level > 1) {
      diffState.level--;
      diffState.wrongStreak = 0;
      showLevelChange(false);
    }
  }
}

function getLevelBadge(level, animate) {
  var data = {
    1: {cls:'level-1', icon:'🟢', label:'Level 1 — Basic'},
    2: {cls:'level-2', icon:'🔵', label:'Level 2 — Intermediate'},
    3: {cls:'level-3', icon:'🔴', label:'Level 3 — Advanced'}
  };
  var d = data[level];
  return '<span class="level-badge '+d.cls+(animate?' animating':'')+'">'+d.icon+' '+d.label+'</span>';
}

function showLevelChange(up) {
  var msg = up ? '🎉 Level Up! Moving to a harder level!' : '💪 Let\'s review! Moving to an easier level.';
  var div = document.createElement('div');
  div.style.cssText = 'position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);background:var(--card);border:2px solid var(--accent3);border-radius:var(--r-xl);padding:20px 30px;font-size:1.1rem;font-weight:800;color:var(--text);z-index:9999;text-align:center;animation:popIn .4s ease;box-shadow:0 4px 40px rgba(0,0,0,.6)';
  div.innerHTML = msg;
  document.body.appendChild(div);
  setTimeout(function(){div.remove();}, 2000);
}

/* ============================================================
   ACTIVITY 1: VOCABULARY CARDS
============================================================ */
function renderVocab() {
  var h = '<div class="section-header"><div class="section-title">📚 Vocabulary in Context</div></div>';
  h += '<p style="font-size:.85rem;color:var(--text2);margin-bottom:10px">Click any card to hear it read aloud. Study each phrase with its direct and reported speech examples.</p>';
  h += '<div class="vocab-grid">';
  VOCAB.forEach(function(v, i) {
    h += '<div class="vocab-card" onclick="speakVocab('+i+')" tabindex="0" onkeydown="if(event.key===\'Enter\')speakVocab('+i+')" aria-label="'+v.phrase+'">';
    h += '<div class="vc-phrase">'+v.emoji+' <span style="font-family:\'Space Mono\',monospace">'+v.phrase+'</span></div>';
    h += '<div class="vc-def">'+v.def+'</div>';
    h += '<div class="vc-direct"><strong>💬 Direct:</strong> '+v.direct+'</div>';
    h += '<div class="vc-reported"><strong>📋 Reported:</strong> '+v.reported+'</div>';
    h += '</div>';
  });
  h += '</div>';
  document.getElementById('pane-vocab').innerHTML = h;
}

function speakVocab(i) {
  var v = VOCAB[i];
  speak(v.phrase + '. ' + v.def + '. Example: ' + v.direct + '. Reported: ' + v.reported);
}

/* ============================================================
   ACTIVITY 2: CLOZE (Vocabulary in context)
============================================================ */
var clozeState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue:[] };

function buildClozeQueue() {
  var level = diffState.level;
  var pool = CLOZE_BANK[level].slice();
  // shuffle
  for (var i = pool.length-1; i > 0; i--) {
    var j = Math.floor(Math.random()*(i+1));
    var tmp = pool[i]; pool[i] = pool[j]; pool[j] = tmp;
  }
  return pool.slice(0, 5);
}

function initCloze() {
  diffState.level = 1; diffState.streak = 0; diffState.wrongStreak = 0;
  clozeState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue: buildClozeQueue() };
  renderCloze();
}

function renderCloze() {
  if (clozeState.cur >= clozeState.queue.length) { showClozeDone(); return; }
  var q = clozeState.queue[clozeState.cur];
  clozeState.answered = false;
  var pct = Math.round(clozeState.cur / clozeState.queue.length * 100);

  var h = '<div class="section-header">';
  h += getLevelBadge(diffState.level, false);
  h += '<div style="font-size:.82rem;color:var(--text3)">Question '+(clozeState.cur+1)+' / '+clozeState.queue.length+'</div>';
  h += '</div>';
  h += '<div class="progress-row"><div class="progress-track"><div class="progress-fill" style="width:'+pct+'%"></div></div><div class="progress-label">'+pct+'%</div></div>';
  h += '<div class="score-row"><div class="score-card"><div class="val">'+clozeState.score+'</div><div class="lbl">Score</div></div><div class="score-card"><div class="val">'+clozeState.total+'</div><div class="lbl">Done</div></div><div class="score-card"><div class="val">'+(clozeState.total > 0 ? Math.round(clozeState.score/clozeState.total*100) : 0)+'%</div><div class="lbl">Accuracy</div></div></div>';

  h += '<div class="q-card">';
  h += '<div class="q-label">✏️ Choose the correct reporting phrase</div>';
  h += '<div class="q-text">'+q.sentence+' <button style="background:none;border:none;cursor:pointer;font-size:.9rem" onclick="speak(\''+q.sentence.replace(/'/g,"\\'")+'\')" title="Listen">🔊</button></div>';
  h += '<div class="q-ctx">📝 '+q.context.replace('___','<strong style="color:var(--accent4)">[ ? ]</strong>')+'</div>';
  h += '<div class="cloze-opts">';
  // shuffle options
  var opts = q.options.slice();
  for (var i = opts.length-1; i > 0; i--) { var j = Math.floor(Math.random()*(i+1)); var t=opts[i];opts[i]=opts[j];opts[j]=t; }
  opts.forEach(function(opt, idx) {
    h += '<button class="opt-btn" id="cloze-opt-'+idx+'" onclick="checkCloze(\''+opt+'\')" style="justify-content:center;text-align:center">';
    h += '<span>'+opt+'</span></button>';
  });
  h += '</div>';
  h += '<div class="fb-box" id="cloze-fb"></div>';
  h += '<button class="action-btn" id="cloze-next" onclick="nextCloze()">'+(clozeState.cur < clozeState.queue.length-1 ? 'Next Question ➡️' : 'See Results 🏆')+'</button>';
  h += '</div>';

  document.getElementById('pane-cloze').innerHTML = h;
  speak(q.sentence);
}

function checkCloze(chosen) {
  if (clozeState.answered) return;
  clozeState.answered = true;
  var q = clozeState.queue[clozeState.cur];
  var correct = chosen.toLowerCase() === q.answer.toLowerCase();
  clozeState.total++;

  document.querySelectorAll('#pane-cloze .opt-btn').forEach(function(b) {
    b.disabled = true;
    var bText = b.querySelector('span').textContent;
    if (bText.toLowerCase() === q.answer.toLowerCase()) b.classList.add('correct');
    else if (bText.toLowerCase() === chosen.toLowerCase()) b.classList.add('wrong');
  });

  var fb = document.getElementById('cloze-fb');
  fb.classList.add('show');
  if (correct) {
    clozeState.score++;
    fb.className = 'fb-box show ok';
    fb.innerHTML = '✅ Correct! <strong>'+q.answer+'</strong> is right. '+q.rule;
    speak('Correct! ' + q.rule);
  } else {
    clozeState.mistakes.push({ type:'cloze', q:q.sentence+' '+q.context, yours:chosen, correct:q.answer, rule:q.rule, tip:'Remember: "'+q.answer+'" — '+q.rule });
    fb.className = 'fb-box show bad';
    fb.innerHTML = '❌ Not quite! The answer is <strong>'+q.answer+'</strong>. '+q.rule;
    speak('Not quite. The answer is ' + q.answer + '. ' + q.rule);
  }
  var mistakeObj = correct ? null : { activity:'Cloze', q:q.sentence+'\n'+q.context, yours:chosen, correct:q.answer, rule:q.rule, tip:'The correct reporting verb here is "'+q.answer+'". '+q.rule };
  TRACKER_record(correct, mistakeObj);
  updateDifficulty(correct);
  document.getElementById('cloze-next').classList.add('show');
}

function nextCloze() {
  clozeState.cur++;
  if (clozeState.cur >= clozeState.queue.length) {
    clozeState.queue = clozeState.queue.concat(buildClozeQueue());
  }
  renderCloze();
}

function showClozeDone() {
  renderDoneScreen('pane-cloze', clozeState.score, clozeState.total, 'initCloze');
}

/* ============================================================
   ACTIVITY 3: MCQ GRAMMAR
============================================================ */
var mcqState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue:[] };

function buildMCQQueue() {
  var level = diffState.level;
  var pool = MCQ_BANK[level].slice();
  for (var i = pool.length-1; i > 0; i--) { var j=Math.floor(Math.random()*(i+1)); var t=pool[i];pool[i]=pool[j];pool[j]=t; }
  return pool.slice(0, 5);
}

function initMCQ() {
  diffState.level = 1; diffState.streak = 0; diffState.wrongStreak = 0;
  mcqState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue: buildMCQQueue() };
  renderMCQ();
}

function renderMCQ() {
  if (mcqState.cur >= mcqState.queue.length) { showMCQDone(); return; }
  var q = mcqState.queue[mcqState.cur];
  mcqState.answered = false;
  var pct = Math.round(mcqState.cur / mcqState.queue.length * 100);

  var h = '<div class="section-header">';
  h += getLevelBadge(diffState.level, false);
  h += '<div style="font-size:.82rem;color:var(--text3)">Question '+(mcqState.cur+1)+' / '+mcqState.queue.length+'</div>';
  h += '</div>';
  h += '<div class="progress-row"><div class="progress-track"><div class="progress-fill" style="width:'+pct+'%"></div></div><div class="progress-label">'+pct+'%</div></div>';
  h += '<div class="score-row"><div class="score-card"><div class="val">'+mcqState.score+'</div><div class="lbl">Score</div></div><div class="score-card"><div class="val">'+mcqState.total+'</div><div class="lbl">Done</div></div><div class="score-card"><div class="val">'+(mcqState.total>0?Math.round(mcqState.score/mcqState.total*100):0)+'%</div><div class="lbl">Accuracy</div></div></div>';

  var letters = ['A','B','C','D'];
  h += '<div class="q-card">';
  h += '<div class="q-label">✅ Choose the correct reported speech form</div>';
  h += '<div class="q-text">'+q.direct+' <button style="background:none;border:none;cursor:pointer;font-size:.9rem" onclick="speak(\''+q.direct.replace(/'/g,"\\'")+'\')" title="Listen">🔊</button></div>';
  h += '<div class="q-ctx">📝 '+q.context.replace('___','<strong style="color:var(--accent4)">[ ? ]</strong>')+'</div>';
  h += '<div class="opts-grid">';
  q.options.forEach(function(opt, idx) {
    h += '<button class="opt-btn" id="mcq-opt-'+idx+'" onclick="checkMCQ('+idx+')">';
    h += '<span class="opt-letter">'+letters[idx]+'</span><span>'+opt+'</span></button>';
  });
  h += '</div>';
  h += '<div class="fb-box" id="mcq-fb"></div>';
  h += '<button class="action-btn" id="mcq-next" onclick="nextMCQ()">'+(mcqState.cur < mcqState.queue.length-1 ? 'Next Question ➡️' : 'See Results 🏆')+'</button>';
  h += '</div>';

  document.getElementById('pane-mcq').innerHTML = h;
  speak(q.direct);
}

function checkMCQ(idx) {
  if (mcqState.answered) return;
  mcqState.answered = true;
  var q = mcqState.queue[mcqState.cur];
  var correct = idx === q.answer;
  mcqState.total++;

  for (var k = 0; k < q.options.length; k++) {
    var btn = document.getElementById('mcq-opt-'+k);
    if (btn) btn.disabled = true;
    if (k === q.answer && btn) btn.classList.add('correct');
    else if (k === idx && !correct && btn) btn.classList.add('wrong');
  }

  var fb = document.getElementById('mcq-fb');
  fb.classList.add('show');
  if (correct) {
    mcqState.score++;
    fb.className = 'fb-box show ok';
    fb.innerHTML = '✅ Correct! ' + q.tip;
    speak('Correct! ' + q.tip);
  } else {
    mcqState.mistakes.push({ type:'mcq', q:q.direct+' '+q.context, yours:q.options[idx], correct:q.options[q.answer], rule:q.rule, tip:q.tip });
    fb.className = 'fb-box show bad';
    fb.innerHTML = '❌ Not quite! '+q.tip;
    speak('Not quite. ' + q.tip);
  }
  var mistakeObj = correct ? null : { activity:'Grammar MCQ', q:q.direct+'\n'+q.context, yours:q.options[idx], correct:q.options[q.answer], rule:q.rule, tip:q.tip };
  TRACKER_record(correct, mistakeObj);
  updateDifficulty(correct);
  document.getElementById('mcq-next').classList.add('show');
}

function nextMCQ() {
  mcqState.cur++;
  if (mcqState.cur >= mcqState.queue.length) {
    mcqState.queue = mcqState.queue.concat(buildMCQQueue());
  }
  renderMCQ();
}

function showMCQDone() {
  renderDoneScreen('pane-mcq', mcqState.score, mcqState.total, 'initMCQ');
}

/* ============================================================
   ACTIVITY 4: FILL IN THE BLANKS
============================================================ */
var fillState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue:[] };

function buildFillQueue() {
  var level = diffState.level;
  var pool = FILL_BANK[level].slice();
  for (var i = pool.length-1; i > 0; i--) { var j=Math.floor(Math.random()*(i+1)); var t=pool[i];pool[i]=pool[j];pool[j]=t; }
  return pool.slice(0, 5);
}

function initFill() {
  diffState.level = 1; diffState.streak = 0; diffState.wrongStreak = 0;
  fillState = { cur:0, answered:false, mistakes:[], score:0, total:0, queue: buildFillQueue() };
  renderFill();
}

function renderFill() {
  if (fillState.cur >= fillState.queue.length) { showFillDone(); return; }
  var q = fillState.queue[fillState.cur];
  fillState.answered = false;
  var pct = Math.round(fillState.cur / fillState.queue.length * 100);

  var h = '<div class="section-header">';
  h += getLevelBadge(diffState.level, false);
  h += '<div style="font-size:.82rem;color:var(--text3)">Question '+(fillState.cur+1)+' / '+fillState.queue.length+'</div>';
  h += '</div>';
  h += '<div class="progress-row"><div class="progress-track"><div class="progress-fill" style="width:'+pct+'%"></div></div><div class="progress-label">'+pct+'%</div></div>';
  h += '<div class="score-row"><div class="score-card"><div class="val">'+fillState.score+'</div><div class="lbl">Score</div></div><div class="score-card"><div class="val">'+fillState.total+'</div><div class="lbl">Done</div></div><div class="score-card"><div class="val">'+(fillState.total>0?Math.round(fillState.score/fillState.total*100):0)+'%</div><div class="lbl">Accuracy</div></div></div>';

  h += '<div class="q-card">';
  h += '<div class="q-label">📝 Fill in the blank with the correct reported form</div>';
  h += '<div class="q-text">'+q.direct+' <button style="background:none;border:none;cursor:pointer;font-size:.9rem" onclick="speak(\''+q.direct.replace(/'/g,"\\'")+'\')" title="Listen">🔊</button></div>';
  h += '<div class="fill-sentence">'+q.before+'<input class="fill-input" id="fill-inp" placeholder="'+q.hint+'" aria-label="Fill in the blank" />'+q.after+'</div>';
  h += '<button class="check-btn" onclick="checkFill()">✔ Check Answer</button>';
  h += '<div class="fb-box" id="fill-fb"></div>';
  h += '<button class="action-btn" id="fill-next" onclick="nextFill()">'+(fillState.cur < fillState.queue.length-1 ? 'Next Question ➡️' : 'See Results 🏆')+'</button>';
  h += '</div>';

  document.getElementById('pane-fill').innerHTML = h;
  var inp = document.getElementById('fill-inp');
  if (inp) inp.addEventListener('keydown', function(e){ if(e.key==='Enter') checkFill(); });
  speak(q.direct);
}

function checkFill() {
  if (fillState.answered) return;
  var inp = document.getElementById('fill-inp');
  if (!inp) return;
  var val = inp.value.trim().toLowerCase();
  if (!val) { inp.focus(); return; }
  fillState.answered = true;
  inp.disabled = true;
  document.querySelector('#pane-fill .check-btn').disabled = true;

  var q = fillState.queue[fillState.cur];
  var accepted = q.blank.toLowerCase();
  var correct = val === accepted || val.replace(/\s+/g,' ') === accepted;
  fillState.total++;

  var fb = document.getElementById('fill-fb');
  fb.classList.add('show');
  if (correct) {
    inp.classList.add('ok');
    fillState.score++;
    fb.className = 'fb-box show ok';
    fb.innerHTML = '✅ Correct! ' + q.rule;
    speak('Correct! ' + q.rule);
  } else {
    inp.classList.add('bad');
    fillState.mistakes.push({ type:'fill', q:q.direct, yours:val, correct:q.blank, rule:q.rule, tip:'The answer is: "'+q.blank+'". '+q.rule });
    fb.className = 'fb-box show bad';
    fb.innerHTML = '❌ The answer is: <strong>'+q.blank+'</strong>. '+q.rule;
    speak('Not quite. The answer is: ' + q.blank + '. ' + q.rule);
  }
  var mistakeObj = correct ? null : { activity:'Fill In', q:q.direct, yours:val, correct:q.blank, rule:q.rule, tip:'The answer is "'+q.blank+'". '+q.rule };
  TRACKER_record(correct, mistakeObj);
  updateDifficulty(correct);
  document.getElementById('fill-next').classList.add('show');
}

function nextFill() {
  fillState.cur++;
  if (fillState.cur >= fillState.queue.length) {
    fillState.queue = fillState.queue.concat(buildFillQueue());
  }
  renderFill();
}

function showFillDone() {
  renderDoneScreen('pane-fill', fillState.score, fillState.total, 'initFill');
}

/* ============================================================
   GENERIC DONE SCREEN
============================================================ */
function renderDoneScreen(paneId, score, total, resetFn) {
  var pct = total > 0 ? Math.round(score/total*100) : 0;
  var grade = pct>=90?'🏆 Outstanding!':pct>=75?'⭐ Well done!':pct>=60?'👍 Good effort!':pct>=40?'💪 Keep practicing!':'📖 Review the rules!';
  var h = '<div style="text-align:center;padding:20px;background:var(--card);border-radius:var(--r-xl);border:1px solid var(--border);margin:10px 0;animation:popIn .4s ease">';
  h += '<div style="font-size:3rem;font-weight:900;color:var(--accent3)">'+score+'/'+total+'</div>';
  h += '<div style="font-size:1.1rem;font-weight:800;margin:6px 0">'+grade+'</div>';
  h += '<div style="font-size:.88rem;color:var(--text2)">Accuracy: '+pct+'%</div>';
  h += '<br><button class="replay-btn" onclick="'+resetFn+'()">🔄 Try Again</button>';
  h += '&nbsp;<button class="replay-btn" style="background:linear-gradient(135deg,var(--accent),#6048a8)" onclick="switchTab(\'report\')">📊 View Full Report</button>';
  h += '</div>';
  document.getElementById(paneId).innerHTML = h;
  if (pct >= 80) spawnConfetti();
  speak(grade);
}

/* ============================================================
   ACTIVITY 5: WORDSEARCH
============================================================ */
// Words for grid — compound phrases join without spaces
var WS_WORDS_RAW = [
  {display:'agree', grid:'AGREE'},
  {display:'deny', grid:'DENY'},
  {display:'refuse', grid:'REFUSE'},
  {display:'report', grid:'REPORT'},
  {display:'inform', grid:'INFORM'},
  {display:'confirm', grid:'CONFIRM'},
  {display:'admit', grid:'ADMIT'},
  {display:'argue', grid:'ARGUE'},
  {display:'insist', grid:'INSIST'},
  {display:'claim', grid:'CLAIM'},
  {display:'pointout', grid:'POINTOUT'},
  {display:'gossip', grid:'GOSSIP'},
  {display:'mutter', grid:'MUTTER'},
  {display:'boast', grid:'BOAST'},
  {display:'cheer', grid:'CHEER'},
  {display:'complain', grid:'COMPLAIN'},
  {display:'quarrel', grid:'QUARREL'},
  {display:'whisper', grid:'WHISPER'}
];

var WS_GRID_SIZE = 18;
var wsGrid = [], wsPlaced = [], wsFound = [], wsSelStart = null, wsSelCells = [], wsIsSelecting = false;

function buildWSGrid() {
  wsGrid = [];
  wsPlaced = [];
  wsFound = [];
  wsSelStart = null;
  wsSelCells = [];
  wsIsSelecting = false;

  for (var r = 0; r < WS_GRID_SIZE; r++) {
    wsGrid.push([]);
    for (var c = 0; c < WS_GRID_SIZE; c++) wsGrid[r].push('');
  }

  // directions: horizontal right, vertical down
  var dirs = [[0,1],[1,0]];
  var words = WS_WORDS_RAW.slice().sort(function(){ return Math.random()-.5; });

  words.forEach(function(wObj) {
    var word = wObj.grid;
    var placed = false;
    var tries = 0;
    while (!placed && tries < 300) {
      tries++;
      var dir = dirs[Math.floor(Math.random()*dirs.length)];
      var maxR = WS_GRID_SIZE - (dir[0] * word.length);
      var maxC = WS_GRID_SIZE - (dir[1] * word.length);
      if (maxR <= 0 || maxC <= 0) continue;
      var r = Math.floor(Math.random()*maxR);
      var c = Math.floor(Math.random()*maxC);
      var cells = [], valid = true;
      for (var i = 0; i < word.length; i++) {
        var nr = r + dir[0]*i, nc = c + dir[1]*i;
        if (wsGrid[nr][nc] !== '' && wsGrid[nr][nc] !== word[i]) { valid=false; break; }
        cells.push([nr, nc]);
      }
      if (valid) {
        cells.forEach(function(cell, i){ wsGrid[cell[0]][cell[1]] = word[i]; });
        wsPlaced.push({ word: word, display: wObj.display, cells: cells });
        placed = true;
      }
    }
  });

  var alpha = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  for (var r = 0; r < WS_GRID_SIZE; r++)
    for (var c = 0; c < WS_GRID_SIZE; c++)
      if (wsGrid[r][c] === '') wsGrid[r][c] = alpha[Math.floor(Math.random()*26)];
}

function renderWS() {
  buildWSGrid();
  drawWS();
}

function drawWS() {
  var foundSet = {};
  wsFound.forEach(function(w){ foundSet[w]=true; });

  var h = '<div class="section-header"><div class="section-title">🔍 Word Search</div>';
  h += '<div style="font-size:.82rem;color:var(--text3)">Found: '+wsFound.length+'/'+WS_WORDS_RAW.length+'</div></div>';
  h += '<div class="progress-row"><div class="progress-track"><div class="progress-fill" style="width:'+Math.round(wsFound.length/WS_WORDS_RAW.length*100)+'%"></div></div><div class="progress-label">'+Math.round(wsFound.length/WS_WORDS_RAW.length*100)+'%</div></div>';
  h += '<p style="font-size:.8rem;color:var(--text3);margin-bottom:8px">Click and drag to select words (left→right or top→bottom). Words may overlap!</p>';

  // Chips
  h += '<div class="ws-words-chips">';
  WS_WORDS_RAW.forEach(function(w){
    h += '<span class="ws-chip'+(foundSet[w.grid]?' found':'')+'" id="wchip-'+w.grid+'">'+w.display+'</span>';
  });
  h += '</div>';

  // Grid
  h += '<div class="ws-container"><div class="ws-grid-wrap" id="ws-grid" style="grid-template-columns:repeat('+WS_GRID_SIZE+',1fr)">';
  for (var r = 0; r < WS_GRID_SIZE; r++) {
    for (var c = 0; c < WS_GRID_SIZE; c++) {
      var isFound = wsPlaced.some(function(p){
        return foundSet[p.word] && p.cells.some(function(cell){ return cell[0]===r && cell[1]===c; });
      });
      h += '<div class="ws-cell'+(isFound?' found':'')+'" id="wsc-'+r+'-'+c+'" data-r="'+r+'" data-c="'+c+'">'+wsGrid[r][c]+'</div>';
    }
  }
  h += '</div></div>';

  if (wsFound.length === WS_WORDS_RAW.length) {
    h += '<div style="text-align:center;padding:16px;background:rgba(0,212,170,.1);border-radius:var(--r-lg);margin-top:10px;border:1px solid var(--accent3)"><div style="font-size:1.5rem;font-weight:900;color:var(--accent3)">🎉 All words found!</div><button class="replay-btn" onclick="renderWS()" style="margin-top:8px">🔄 New Grid</button></div>';
  }

  document.getElementById('pane-ws').innerHTML = h;
  attachWSEvents();
}

function attachWSEvents() {
  var cells = document.querySelectorAll('.ws-cell');
  cells.forEach(function(cell) {
    cell.addEventListener('mousedown', function(e){ e.preventDefault(); wsIsSelecting=true; wsSelCells=[[+cell.dataset.r,+cell.dataset.c]]; highlightWSCells(); });
    cell.addEventListener('mouseover', function(){ if(!wsIsSelecting)return; extendWSSelection(+cell.dataset.r,+cell.dataset.c); highlightWSCells(); });
    cell.addEventListener('mouseup', function(){ if(!wsIsSelecting)return; wsIsSelecting=false; checkWSWord(); });
    cell.addEventListener('touchstart',function(e){ e.preventDefault(); wsIsSelecting=true; wsSelCells=[[+cell.dataset.r,+cell.dataset.c]]; highlightWSCells(); },{passive:false});
    cell.addEventListener('touchmove',function(e){ e.preventDefault(); var t=e.touches[0]; var el=document.elementFromPoint(t.clientX,t.clientY); if(el&&el.dataset&&el.dataset.r!=null){ extendWSSelection(+el.dataset.r,+el.dataset.c); highlightWSCells(); } },{passive:false});
    cell.addEventListener('touchend',function(){ wsIsSelecting=false; checkWSWord(); });
  });
  document.addEventListener('mouseup', function(){ wsIsSelecting=false; });
}

function extendWSSelection(r, c) {
  if (!wsSelCells.length) { wsSelCells=[[r,c]]; return; }
  var fr=wsSelCells[0][0], fc=wsSelCells[0][1];
  var dr=r-fr, dc=c-fc;
  var newSel=[[fr,fc]];
  if (dr===0 && dc!==0) {
    var step=dc>0?1:-1;
    for (var i=1;i<=Math.abs(dc);i++) newSel.push([fr, fc+step*i]);
  } else if (dc===0 && dr!==0) {
    var step2=dr>0?1:-1;
    for (var i=1;i<=Math.abs(dr);i++) newSel.push([fr+step2*i, fc]);
  } else {
    newSel=[[fr,fc],[r,c]];
  }
  wsSelCells=newSel;
}

function highlightWSCells() {
  var foundSet={};
  wsFound.forEach(function(w){foundSet[w]=true;});
  document.querySelectorAll('.ws-cell').forEach(function(el){
    if (!foundSet[/* need to check */el.id]) el.classList.remove('selecting');
  });
  wsSelCells.forEach(function(pos){
    var el=document.getElementById('wsc-'+pos[0]+'-'+pos[1]);
    if (el && !el.classList.contains('found')) el.classList.add('selecting');
  });
}

function checkWSWord() {
  document.querySelectorAll('.ws-cell.selecting').forEach(function(el){ el.classList.remove('selecting'); });
  if (!wsSelCells.length) return;
  var word = wsSelCells.map(function(pos){ return wsGrid[pos[0]][pos[1]]; }).join('');
  var match = wsPlaced.find(function(p){ return p.word === word && wsFound.indexOf(p.word) === -1; });
  if (match) {
    wsFound.push(match.word);
    speak('Found: ' + match.display);
    // flash cells
    wsSelCells.forEach(function(pos){
      var el=document.getElementById('wsc-'+pos[0]+'-'+pos[1]);
      if(el){ el.classList.add('found-flash'); setTimeout(function(){ el.classList.add('found'); el.classList.remove('found-flash'); },300); }
    });
    var chip=document.getElementById('wchip-'+match.word);
    if(chip) chip.classList.add('found');
    var prog=document.querySelector('#pane-ws .progress-fill');
    if(prog) prog.style.width=Math.round(wsFound.length/WS_WORDS_RAW.length*100)+'%';
    if(wsFound.length===WS_WORDS_RAW.length){ setTimeout(function(){ drawWS(); spawnConfetti(); },500); }
  }
  wsSelCells=[];
}

/* ============================================================
   GAME MODE (KAHOOT STYLE)
============================================================ */
var gameState = {
  cur: 0, score: 0, streak: 0, lives: 3, answered: false,
  timerInterval: null, timeLeft: 12, totalCorrect: 0, totalQ: 0,
  mistakes: [], queue: [], startTime: 0
};

function initGame() {
  clearInterval(gameState.timerInterval);
  var pool = GAME_QUESTIONS.slice().sort(function(){ return Math.random()-.5; });
  gameState = { cur:0, score:0, streak:0, lives:3, answered:false, timerInterval:null, timeLeft:12, totalCorrect:0, totalQ:0, mistakes:[], queue:pool.slice(0,12), startTime:0 };
  renderGame();
}

function renderGame() {
  if (gameState.cur >= gameState.queue.length || gameState.lives <= 0) { endGame(); return; }
  var q = gameState.queue[gameState.cur];
  gameState.answered = false;
  gameState.timeLeft = 12;
  gameState.startTime = Date.now();

  var levelColors = {1:'#22c55e',2:'#3b82f6',3:'#ef4444'};
  var lc = levelColors[q.level] || '#22c55e';

  var h = '<div class="game-arena">';
  // Header
  h += '<div class="game-header">';
  h += '<div class="lives-row" id="g-lives">';
  for (var i=0;i<3;i++) h += '<span class="life-icon'+(i>=gameState.lives?' lost':'')+'">❤️</span>';
  h += '</div>';
  h += '<div class="streak-badge'+(gameState.streak>=3?' on-fire':'')+'">'+( gameState.streak>=3?'🔥 On Fire! +streak':'⚡ Streak: '+gameState.streak )+'</div>';
  h += '<div style="font-size:.8rem;background:rgba('+lc.replace('#','')+'22);color:'+lc+';padding:4px 10px;border-radius:20px;font-weight:700;border:1px solid '+lc+'">Lvl '+q.level+'</div>';
  h += '</div>';
  // Score
  h += '<div class="score-row"><div class="score-card"><div class="val" id="g-score">'+gameState.score+'</div><div class="lbl">Score</div></div><div class="score-card"><div class="val" id="g-correct">'+gameState.totalCorrect+'</div><div class="lbl">Correct</div></div><div class="score-card"><div class="val">'+(gameState.cur+1)+'/'+gameState.queue.length+'</div><div class="lbl">Round</div></div></div>';
  // Timer
  h += '<div class="timer-wrap"><div class="timer-num" id="g-timer-num">'+gameState.timeLeft+'</div><div class="timer-track"><div class="timer-fill" id="g-timer" style="width:100%"></div></div></div>';
  // Question bubble
  h += '<div class="game-bubble">'+q.direct+' <button style="background:none;border:none;cursor:pointer;font-size:.9rem" onclick="speak(\''+q.direct.replace(/'/g,"\\'")+'\')" title="Listen">🔊</button></div>';
  h += '<div class="game-question">'+q.q+'</div>';
  // Options
  var letters=['A','B','C'];
  h += '<div class="opts-grid">';
  q.opts.forEach(function(opt,idx){
    h += '<button class="opt-btn" id="gopt-'+idx+'" onclick="checkGame('+idx+')">';
    h += '<span class="opt-letter">'+letters[idx]+'</span><span>'+opt+'</span></button>';
  });
  h += '</div>';
  h += '<div class="fb-box" id="g-fb"></div>';
  h += '</div>';

  document.getElementById('pane-game').innerHTML = h;
  startGameTimer();
  speak(q.direct + '. ' + q.q);
}

function startGameTimer() {
  clearInterval(gameState.timerInterval);
  gameState.timerInterval = setInterval(function(){
    gameState.timeLeft--;
    var tn=document.getElementById('g-timer-num');
    var tf=document.getElementById('g-timer');
    if(tn) { tn.textContent=gameState.timeLeft; if(gameState.timeLeft<=4){ tn.classList.add('urgent'); } }
    if(tf) { tf.style.width=Math.round(gameState.timeLeft/12*100)+'%'; if(gameState.timeLeft<=4) tf.classList.add('urgent'); }
    if(gameState.timeLeft<=0){ clearInterval(gameState.timerInterval); timeExpiredGame(); }
  }, 1000);
}

function checkGame(idx) {
  if (gameState.answered) return;
  clearInterval(gameState.timerInterval);
  gameState.answered = true;
  var q = gameState.queue[gameState.cur];
  var correct = idx === q.ans;
  var elapsed = (Date.now() - gameState.startTime) / 1000;
  gameState.totalQ++;

  document.querySelectorAll('[id^="gopt-"]').forEach(function(b){ b.disabled=true; });
  document.getElementById('gopt-'+q.ans).classList.add('correct');
  if (!correct) document.getElementById('gopt-'+idx).classList.add('wrong');

  var fb = document.getElementById('g-fb');
  fb.classList.add('show');

  if (correct) {
    gameState.streak++;
    gameState.totalCorrect++;
    var pts = elapsed < 4 ? 1000 : elapsed < 8 ? 700 : 400;
    if (gameState.streak >= 3) pts += 300;
    gameState.score += pts;
    var gs=document.getElementById('g-score'); if(gs) gs.textContent=gameState.score;
    var gc=document.getElementById('g-correct'); if(gc) gc.textContent=gameState.totalCorrect;
    fb.className = 'fb-box show ok';
    fb.innerHTML = '✅ Correct! +'+pts+' pts'+(gameState.streak>=3?' 🔥 Streak bonus!':'');
    showPointsPopup('+'+pts);
    speak('Correct! ' + pts + ' points!');
  } else {
    gameState.streak = 0;
    gameState.lives--;
    gameState.mistakes.push({ q:q.direct+' '+q.q, yours:q.opts[idx], correct:q.opts[q.ans], rule:q.rule, tip:'Remember: '+q.rule });
    fb.className = 'fb-box show bad';
    fb.innerHTML = '❌ Wrong! '+q.rule;
    speak('Wrong. ' + q.rule);
    if (gameState.lives <= 0) { setTimeout(function(){ endGame(); }, 1500); return; }
  }
  var mistakeObj = correct ? null : { activity:'Game Mode', q:q.direct+'\n'+q.q, yours:q.opts[idx], correct:q.opts[q.ans], rule:q.rule, tip:'Remember: '+q.rule };
  TRACKER_record(correct, mistakeObj);
  if (correct) {
    setTimeout(function(){ gameState.cur++; renderGame(); }, 1600);
  } else {
    if (gameState.lives <= 0) { setTimeout(function(){ endGame(); }, 1500); return; }
    setTimeout(function(){ gameState.cur++; renderGame(); }, 1600);
  }
}

function timeExpiredGame() {
  if (gameState.answered) return;
  gameState.answered = true;
  var q = gameState.queue[gameState.cur];
  gameState.streak = 0;
  gameState.lives--;
  gameState.totalQ++;
  gameState.mistakes.push({ q:q.direct, yours:'(time expired)', correct:q.opts[q.ans], rule:q.rule, tip:q.rule });

  TRACKER_record(false, { activity:'Game Mode', q:q.direct, yours:'(time expired)', correct:q.opts[q.ans], rule:q.rule, tip:q.rule });
  document.querySelectorAll('[id^="gopt-"]').forEach(function(b){ b.disabled=true; });
  var cb=document.getElementById('gopt-'+q.ans); if(cb) cb.classList.add('correct');
  var fb=document.getElementById('g-fb');
  if(fb){ fb.className='fb-box show bad'; fb.innerHTML='⏱️ Time\'s up! Answer: <strong>'+q.opts[q.ans]+'</strong>'; }
  speak('Time is up!');
  if (gameState.lives <= 0) { setTimeout(function(){ endGame(); }, 1500); return; }
  setTimeout(function(){ gameState.cur++; renderGame(); }, 1800);
}

function showPointsPopup(txt) {
  var d=document.createElement('div');
  d.className='points-popup';
  d.textContent=txt;
  document.body.appendChild(d);
  setTimeout(function(){ d.remove(); }, 1000);
}

function endGame() {
  clearInterval(gameState.timerInterval);
  var pct = gameState.totalQ > 0 ? Math.round(gameState.totalCorrect/gameState.totalQ*100) : 0;
  var grade = pct>=90?'🏆 Excellent control of reported speech!':pct>=75?'⭐ Strong performance! Keep it up!':pct>=60?'👍 Good effort! Work on tense backshift.':pct>=40?'💪 Keep practicing the grammar rules!':'📖 Review reported speech rules carefully.';

  var h = '<div class="game-result">';
  h += '<div style="font-size:1rem;font-weight:800;color:var(--text2);margin-bottom:4px">FINAL SCORE</div>';
  h += '<div class="result-score">'+gameState.score+'</div>';
  h += '<div class="result-grade">'+grade+'</div>';
  h += '<div class="result-msg">Correct: '+gameState.totalCorrect+' / '+gameState.totalQ+' &nbsp;·&nbsp; Accuracy: '+pct+'% &nbsp;·&nbsp; Best streak: '+gameState.streak+'🔥</div>';

  // Leaderboard save
  h += '<div style="display:flex;gap:8px;flex-wrap:wrap;justify-content:center;margin-top:8px">';
  h += '<input id="lb-name-inp" placeholder="Enter your name..." style="padding:8px 12px;border-radius:var(--r-md);border:2px solid var(--border);background:var(--bg3);color:var(--text);font-size:.88rem;font-family:\'Nunito\',sans-serif;min-width:150px">';
  h += '<button class="save-score-btn" onclick="saveToLB()">💾 Save Score</button>';
  h += '</div>';

  // Leaderboard display
  h += renderLeaderboard();

  h += '<button class="replay-btn" onclick="initGame()" style="margin:6px">🔄 Play Again</button>';
  h += '<button class="replay-btn" onclick="switchTab(\'report\')" style="margin:6px;background:linear-gradient(135deg,var(--accent),#6048a8)">📊 Full Report</button>';
  h += '</div>';

  document.getElementById('pane-game').innerHTML = h;
  if (pct >= 75) spawnConfetti();
  speak(grade);
}

function saveToLB() {
  var inp = document.getElementById('lb-name-inp');
  if (!inp || !inp.value.trim()) return;
  var pct = gameState.totalQ > 0 ? Math.round(gameState.totalCorrect/gameState.totalQ*100) : 0;
  leaderboard.push({ name: inp.value.trim(), score: gameState.score, correct: gameState.totalCorrect, total: gameState.totalQ, pct: pct });
  leaderboard.sort(function(a,b){ return b.score-a.score; });
  leaderboard = leaderboard.slice(0, 10);
  var lb = document.querySelector('#pane-game .leaderboard');
  if (lb) lb.outerHTML = renderLeaderboard();
}

function renderLeaderboard() {
  if (!leaderboard.length) return '<div style="text-align:center;color:var(--text3);font-size:.82rem;margin:8px">Complete the game and save your score to see the leaderboard.</div>';
  var h = '<div class="leaderboard"><div class="leaderboard-title">🏅 Leaderboard</div>';
  var medals = ['🥇','🥈','🥉'];
  leaderboard.slice(0,10).forEach(function(entry, i){
    h += '<div class="lb-row"><div class="lb-rank">'+(medals[i]||'#'+(i+1))+'</div><div class="lb-name">'+entry.name+'</div><div style="font-size:.78rem;color:var(--text3)">'+entry.pct+'%</div><div class="lb-score">'+entry.score+'</div></div>';
  });
  h += '</div>';
  return h;
}

/* ============================================================
   PERFORMANCE REPORT
============================================================ */
function renderReport() {
  var attempts  = TRACKER.attempts;
  var correct   = TRACKER.correct;
  var mistakes  = TRACKER.mistakes;
  var pct = attempts > 0 ? Math.round(correct / attempts * 100) : 0;
  var h = '<div class="report-wrap">';
  if (attempts === 0) {
    h += '<div style="text-align:center;padding:40px 20px;background:var(--card);border-radius:var(--r-xl);border:1px solid var(--border);margin:10px 0">';
    h += '<div style="font-size:3rem;margin-bottom:12px">\u{1F4CA}</div>';
    h += '<div style="font-size:1.1rem;font-weight:800;color:var(--text);margin-bottom:8px">No data yet</div>';
    h += '<div style="font-size:.9rem;color:var(--text2);line-height:1.6;max-width:340px;margin:0 auto">Answer at least one question in any activity. Your report appears here after your very first answer \u2014 no need to finish the whole activity.</div>';
    h += '<br><button class="replay-btn" onclick="switchTab(\'cloze\')">\u270F\uFE0F Start practicing</button>';
    h += '</div></div>';
    document.getElementById('pane-report').innerHTML = h;
    return;
  }
  var grade = pct>=90?'\u{1F3C6} Outstanding \u2014 Excellent mastery of reported speech!'
             :pct>=75?'\u2B50 Well done \u2014 Strong understanding overall!'
             :pct>=60?'\u{1F44D} Good effort \u2014 A few areas to improve.'
             :pct>=40?'\u{1F4AA} Keep practicing \u2014 Review the key rules below.'
                     :'\u{1F4D6} Needs review \u2014 Study reported speech rules carefully.';
  var topics = [
    { key:'Tense backshift',    tokens:['tense backshift','past simple','past perfect','past continuous','future perfect','conditional perfect','present perfect'] },
    { key:'Pronoun changes',    tokens:['pronoun','he"','she"','they"','her"','his"','their"'] },
    { key:'Time expressions',   tokens:['time expression','today','tomorrow','yesterday','the next day','that day','the night before','the following','now →','here →'] },
    { key:'Modal verbs',        tokens:['modal','will → would','can → could','must → had to','may → might','shall → should'] },
    { key:'Reported questions', tokens:['reported question','if/whether','statement word order','wh-question','no inversion'] }
  ];
  var weakMap = {};
  mistakes.forEach(function(m) {
    var hay = ((m.rule||'') + ' ' + (m.tip||'')).toLowerCase();
    topics.forEach(function(t) {
      if (t.tokens.some(function(tok){ return hay.indexOf(tok.toLowerCase()) !== -1; }))
        weakMap[t.key] = (weakMap[t.key]||0) + 1;
    });
  });
  var weaknesses = topics.filter(function(t){ return weakMap[t.key]; }).map(function(t){ return t.key; });
  var strengths  = topics.filter(function(t){ return !weakMap[t.key]; }).map(function(t){ return t.key; });
  h += '<div class="report-header">';
  h += '<div style="font-size:.78rem;font-weight:800;text-transform:uppercase;letter-spacing:.8px;color:var(--text3);margin-bottom:6px">\u{1F4CA} Performance Report</div>';
  h += '<div class="report-score-big">'+pct+'%</div>';
  h += '<div class="report-grade">'+grade+'</div>';
  h += '<div style="font-size:.78rem;color:var(--text3);margin-top:4px">Based on '+attempts+' question'+(attempts===1?'':'s')+' answered \u00b7 updates live after every answer</div>';
  h += '<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:12px">';
  h += '<div class="score-card"><div class="val">'+correct+'</div><div class="lbl">Correct</div></div>';
  h += '<div class="score-card"><div class="val">'+(attempts-correct)+'</div><div class="lbl">Wrong</div></div>';
  h += '<div class="score-card"><div class="val">'+mistakes.length+'</div><div class="lbl">Mistakes</div></div>';
  h += '</div></div>';
  h += '<div class="report-sections">';
  if (strengths.length > 0) {
    h += '<div class="report-section"><h3 style="color:var(--green)">\u{1F4AA} Strengths</h3>';
    strengths.forEach(function(s){ h += '<span class="strength-tag">\u2705 '+s+'</span>'; });
    h += '</div>';
  }
  if (weaknesses.length > 0) {
    h += '<div class="report-section"><h3 style="color:var(--red)">\u26A0\uFE0F Areas to improve</h3>';
    weaknesses.forEach(function(w){ h += '<span class="weak-tag">\u{1F4CC} '+w+' ('+weakMap[w]+' error'+(weakMap[w]>1?'s':'')+')</span>'; });
    h += '</div>';
  }
  h += '<div class="report-section">';
  if (mistakes.length > 0) {
    h += '<h3 style="color:var(--accent4)">\u{1F4DD} Mistake review \u2014 '+mistakes.length+' error'+(mistakes.length===1?'':'s')+'</h3>';
    mistakes.forEach(function(m, i){
      h += '<div class="mistake-item">';
      h += '<div class="mi-q" style="margin-bottom:6px"><span style="background:var(--bg4);border-radius:4px;padding:1px 7px;font-size:.72rem;font-weight:800;color:var(--text3);margin-right:6px">'+m.activity+'</span>'+(i+1)+'. '+m.q.replace(/\n/g,' \u2014 ')+'</div>';
      h += '<div style="margin:3px 0">\u274C You answered: <span class="mi-yours">'+m.yours+'</span></div>';
      h += '<div style="margin:3px 0">\u2705 Correct answer: <span class="mi-correct">'+m.correct+'</span></div>';
      if (m.rule) h += '<div class="mi-rule">\u{1F4DA} <strong>Rule:</strong> '+m.rule+'</div>';
      if (m.tip && m.tip !== m.rule) h += '<div class="mi-tip">\u{1F4A1} <strong>Tip:</strong> '+m.tip+'</div>';
      h += '</div>';
    });
  } else {
    h += '<h3 style="color:var(--green)">\u{1F389} No mistakes yet!</h3>';
    h += '<p style="font-size:.83rem;color:var(--text2);margin-top:6px">Every error you make will appear here with a full explanation and grammar tip.</p>';
  }
  h += '</div>';
  if (weaknesses.length > 0) {
    var tipMap = {
      'Tense backshift':    '\u{1F3AF} <strong>Tense Backshift:</strong> Present simple \u2192 past simple \u00b7 Present continuous \u2192 past continuous \u00b7 Will \u2192 would \u00b7 Can \u2192 could \u00b7 Present perfect \u2192 past perfect \u00b7 Past simple \u2192 past perfect \u00b7 Past continuous \u2192 past perfect continuous.',
      'Pronoun changes':    '\u{1F3AF} <strong>Pronoun Changes:</strong> "I" \u2192 he/she/they &nbsp;|&nbsp; "my" \u2192 his/her/their &nbsp;|&nbsp; "we" \u2192 they &nbsp;|&nbsp; "you" \u2192 I/he/she (depends on context). Re-read the sentence to choose the right pronoun.',
      'Time expressions':   '\u{1F3AF} <strong>Time Expressions:</strong> today \u2192 that day &nbsp;|&nbsp; now \u2192 then &nbsp;|&nbsp; tomorrow \u2192 the next day &nbsp;|&nbsp; yesterday \u2192 the day before &nbsp;|&nbsp; next week \u2192 the following week &nbsp;|&nbsp; here \u2192 there &nbsp;|&nbsp; this \u2192 that.',
      'Modal verbs':        '\u{1F3AF} <strong>Modal Verbs:</strong> will \u2192 would &nbsp;|&nbsp; can \u2192 could &nbsp;|&nbsp; may \u2192 might &nbsp;|&nbsp; must \u2192 had to &nbsp;|&nbsp; shall \u2192 should. Note: would, could, might, should do NOT change further.',
      'Reported questions': '\u{1F3AF} <strong>Reported Questions:</strong> Yes/no \u2192 "asked if/whether" + statement word order. Wh- questions \u2192 question word + subject + verb (no inversion). Always apply tense backshift.'
    };
    h += '<div class="report-section"><h3 style="color:var(--blue)">\u{1F4D6} Personalised study tips</h3>';
    weaknesses.forEach(function(w){ if(tipMap[w]) h += '<div class="mistake-item"><div class="mi-rule">'+tipMap[w]+'</div></div>'; });
    h += '</div>';
  }
  h += '</div>';
  h += '<div style="text-align:center;margin-top:14px;display:flex;flex-wrap:wrap;gap:8px;justify-content:center">';
  h += '<button class="replay-btn" onclick="switchTab(\'cloze\')">\u270F\uFE0F Keep Practicing</button>';
  h += '<button class="replay-btn" onclick="TRACKER_reset();switchTab(\'cloze\')" style="background:linear-gradient(135deg,var(--accent2),#c23)">\u{1F504} Reset Progress</button>';
  h += '</div></div>';
  document.getElementById('pane-report').innerHTML = h;
}


/* ============================================================
   CONFETTI
============================================================ */
function spawnConfetti() {
  var overlay = document.getElementById('confetti-overlay');
  if (!overlay) return;
  var colors = ['#7c5cbf','#e94560','#00d4aa','#f7b731','#3b82f6','#22c55e','#f97316'];
  for (var i = 0; i < 40; i++) {
    (function(delay){
      setTimeout(function(){
        var d=document.createElement('div');
        d.className='conf-piece';
        d.style.cssText='left:'+Math.random()*100+'%;background:'+colors[Math.floor(Math.random()*colors.length)]+';animation-delay:0s;border-radius:'+(Math.random()>.5?'50%':'3px')+';width:'+(8+Math.random()*8)+'px;height:'+(8+Math.random()*8)+'px';
        overlay.appendChild(d);
        setTimeout(function(){ d.remove(); }, 1000);
      }, delay);
    })(i*40);
  }
}

/* ============================================================
   INIT
============================================================ */
window.addEventListener('DOMContentLoaded', function() {
  renderVocab();
  initCloze();
  initMCQ();
  initFill();
  renderWS();
  initGame();
});
</script>
</body>
</html>
