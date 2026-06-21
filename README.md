<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#0a0a0f">
<title>MindSprint Pro — Focus & Reaction Training</title>
<link rel="manifest" href="data:application/json,{}">
<style>
  :root {
    --bg: #0a0a0f;
    --bg2: #12121a;
    --bg3: #1a1a28;
    --bg4: #22223a;
    --accent: #7c3aed;
    --accent2: #a855f7;
    --accent3: #06d6a0;
    --gold: #f59e0b;
    --danger: #ef4444;
    --text: #f1f0ff;
    --text2: #a09bbf;
    --text3: #6b6685;
    --border: rgba(255,255,255,0.08);
    --border2: rgba(255,255,255,0.15);
    --glass: rgba(255,255,255,0.04);
    --glass2: rgba(255,255,255,0.07);
    --radius: 12px;
    --radius2: 20px;
    --shadow: 0 8px 32px rgba(0,0,0,0.4);
    --glow: 0 0 20px rgba(124,58,237,0.3);
    --glow2: 0 0 40px rgba(168,85,247,0.2);
    --transition: 0.2s cubic-bezier(0.4,0,0.2,1);
  }
  .theme-cyber { --accent:#00f5ff;--accent2:#ff00ff;--accent3:#00ff88;--bg:#050510;--bg2:#0a0520;--bg3:#0f0828;--gold:#ffdd00; }
  .theme-gold { --accent:#f59e0b;--accent2:#fbbf24;--accent3:#10b981;--bg:#0c0a00;--bg2:#1a1400;--bg3:#241e00;--glow:0 0 20px rgba(245,158,11,0.3); }
  .theme-space { --accent:#3b82f6;--accent2:#60a5fa;--accent3:#06d6a0;--bg:#010408;--bg2:#020810;--bg3:#030d1a; }
  .theme-amoled { --bg:#000000;--bg2:#0a0a0a;--bg3:#111;--bg4:#1a1a1a; }
  .theme-light { --bg:#f8f7ff;--bg2:#fff;--bg3:#f0eeff;--bg4:#e8e5ff;--text:#1a1a2e;--text2:#444466;--text3:#888;--border:rgba(0,0,0,0.1);--border2:rgba(0,0,0,0.2);--glass:rgba(0,0,0,0.02);--glass2:rgba(0,0,0,0.05);--shadow:0 8px 32px rgba(0,0,0,0.1); }

  * { margin:0; padding:0; box-sizing:border-box; }
  body { font-family:'Inter',system-ui,sans-serif; background:var(--bg); color:var(--text); min-height:100vh; overflow-x:hidden; }
  
  #particles-canvas { position:fixed; top:0; left:0; width:100%; height:100%; pointer-events:none; z-index:0; opacity:0.4; }
  
  .app { position:relative; z-index:1; display:flex; min-height:100vh; }
  
  /* Sidebar */
  .sidebar { width:240px; background:var(--bg2); border-right:1px solid var(--border); display:flex; flex-direction:column; padding:20px 0; flex-shrink:0; transition:var(--transition); }
  .sidebar-logo { padding:0 20px 24px; display:flex; align-items:center; gap:10px; }
  .logo-icon { width:36px; height:36px; background:linear-gradient(135deg,var(--accent),var(--accent2)); border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:18px; box-shadow:var(--glow); }
  .logo-text { font-size:16px; font-weight:700; letter-spacing:-0.3px; }
  .logo-sub { font-size:10px; color:var(--text3); letter-spacing:1px; text-transform:uppercase; }
  .nav-section { padding:8px 12px 4px; font-size:10px; color:var(--text3); text-transform:uppercase; letter-spacing:1px; font-weight:600; }
  .nav-item { display:flex; align-items:center; gap:10px; padding:10px 20px; cursor:pointer; color:var(--text2); font-size:13px; font-weight:500; border-radius:0; transition:var(--transition); position:relative; }
  .nav-item:hover { background:var(--glass2); color:var(--text); }
  .nav-item.active { background:linear-gradient(90deg,rgba(124,58,237,0.15),transparent); color:var(--accent2); }
  .nav-item.active::before { content:''; position:absolute; left:0; top:0; bottom:0; width:3px; background:var(--accent); border-radius:0 3px 3px 0; }
  .nav-icon { font-size:16px; width:20px; text-align:center; }
  .nav-badge { margin-left:auto; background:var(--accent); color:#fff; font-size:10px; padding:1px 6px; border-radius:10px; font-weight:600; }
  .sidebar-footer { margin-top:auto; padding:16px 20px; border-top:1px solid var(--border); }
  .xp-bar-wrap { margin-top:8px; }
  .xp-bar-label { display:flex; justify-content:space-between; font-size:11px; color:var(--text3); margin-bottom:4px; }
  .xp-bar { height:4px; background:var(--border2); border-radius:2px; overflow:hidden; }
  .xp-bar-fill { height:100%; background:linear-gradient(90deg,var(--accent),var(--accent2)); border-radius:2px; transition:width 0.5s ease; }
  .user-info { display:flex; align-items:center; gap:10px; }
  .user-avatar { width:34px; height:34px; border-radius:50%; background:linear-gradient(135deg,var(--accent),var(--accent2)); display:flex; align-items:center; justify-content:center; font-size:13px; font-weight:700; }
  .user-name { font-size:13px; font-weight:600; }
  .user-rank { font-size:11px; color:var(--gold); font-weight:500; }

  /* Main */
  .main { flex:1; display:flex; flex-direction:column; overflow:hidden; }
  .topbar { background:var(--bg2); border-bottom:1px solid var(--border); padding:12px 24px; display:flex; align-items:center; gap:16px; }
  .topbar-title { font-size:18px; font-weight:700; flex:1; }
  .topbar-stat { display:flex; align-items:center; gap:6px; padding:6px 12px; background:var(--glass); border:1px solid var(--border); border-radius:8px; font-size:12px; }
  .topbar-stat span:last-child { color:var(--accent2); font-weight:600; }
  .btn { display:inline-flex; align-items:center; gap:6px; padding:8px 16px; border-radius:8px; border:none; cursor:pointer; font-size:13px; font-weight:600; transition:var(--transition); font-family:inherit; }
  .btn-primary { background:linear-gradient(135deg,var(--accent),var(--accent2)); color:#fff; box-shadow:var(--glow); }
  .btn-primary:hover { opacity:0.9; transform:translateY(-1px); box-shadow:var(--glow2); }
  .btn-ghost { background:var(--glass); border:1px solid var(--border); color:var(--text2); }
  .btn-ghost:hover { background:var(--glass2); color:var(--text); }
  .btn-sm { padding:5px 10px; font-size:11px; }
  .btn-danger { background:rgba(239,68,68,0.15); border:1px solid rgba(239,68,68,0.3); color:#ef4444; }
  .btn-danger:hover { background:rgba(239,68,68,0.25); }

  .content { flex:1; overflow-y:auto; padding:24px; }
  .content::-webkit-scrollbar { width:6px; }
  .content::-webkit-scrollbar-track { background:transparent; }
  .content::-webkit-scrollbar-thumb { background:var(--border2); border-radius:3px; }

  /* Views */
  .view { display:none; }
  .view.active { display:block; }

  /* Dashboard */
  .dash-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:16px; margin-bottom:24px; }
  .stat-card { background:var(--bg2); border:1px solid var(--border); border-radius:var(--radius); padding:18px; position:relative; overflow:hidden; }
  .stat-card::before { content:''; position:absolute; top:0; right:0; width:80px; height:80px; border-radius:50%; background:var(--accent); opacity:0.05; transform:translate(25px,-25px); }
  .stat-label { font-size:11px; color:var(--text3); text-transform:uppercase; letter-spacing:0.8px; font-weight:600; margin-bottom:8px; }
  .stat-value { font-size:28px; font-weight:800; letter-spacing:-1px; line-height:1; }
  .stat-value.accent { color:var(--accent2); }
  .stat-value.gold { color:var(--gold); }
  .stat-value.green { color:var(--accent3); }
  .stat-sub { font-size:11px; color:var(--text3); margin-top:4px; }
  .stat-trend { font-size:11px; color:var(--accent3); font-weight:600; }

  .grid-2 { display:grid; grid-template-columns:1fr 1fr; gap:16px; margin-bottom:24px; }
  .grid-3 { display:grid; grid-template-columns:1fr 1fr 1fr; gap:16px; margin-bottom:24px; }
  .card { background:var(--bg2); border:1px solid var(--border); border-radius:var(--radius2); padding:20px; }
  .card-title { font-size:14px; font-weight:700; margin-bottom:16px; display:flex; align-items:center; gap:8px; }
  .card-title-icon { font-size:16px; }

  /* Chart containers */
  .chart-wrap { position:relative; height:200px; }

  /* Game modes grid */
  .modes-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:16px; }
  .mode-card { background:var(--bg2); border:1px solid var(--border); border-radius:var(--radius2); padding:20px; cursor:pointer; transition:var(--transition); position:relative; overflow:hidden; }
  .mode-card::after { content:''; position:absolute; inset:0; background:linear-gradient(135deg,var(--accent),var(--accent2)); opacity:0; transition:var(--transition); }
  .mode-card:hover { border-color:var(--accent); transform:translateY(-2px); box-shadow:var(--glow); }
  .mode-card:hover::after { opacity:0.05; }
  .mode-icon { font-size:32px; margin-bottom:12px; }
  .mode-name { font-size:16px; font-weight:700; margin-bottom:6px; }
  .mode-desc { font-size:12px; color:var(--text2); line-height:1.5; }
  .mode-stats { display:flex; gap:12px; margin-top:12px; }
  .mode-stat { font-size:11px; color:var(--text3); }
  .mode-stat strong { color:var(--accent2); }
  .diff-badge { display:inline-block; padding:2px 8px; border-radius:4px; font-size:10px; font-weight:700; text-transform:uppercase; margin-top:8px; }
  .diff-easy { background:rgba(6,214,160,0.15); color:var(--accent3); }
  .diff-med { background:rgba(245,158,11,0.15); color:var(--gold); }
  .diff-hard { background:rgba(239,68,68,0.15); color:var(--danger); }

  /* Game Arena */
  .game-arena { background:var(--bg2); border:1px solid var(--border); border-radius:var(--radius2); padding:24px; min-height:500px; display:flex; flex-direction:column; }
  .game-header { display:flex; align-items:center; gap:16px; margin-bottom:20px; }
  .game-title { font-size:20px; font-weight:800; flex:1; }
  .game-timer { font-size:24px; font-weight:800; font-variant-numeric:tabular-nums; color:var(--accent2); }
  .game-score-bar { display:flex; gap:16px; padding:12px 16px; background:var(--bg3); border-radius:var(--radius); margin-bottom:20px; }
  .game-metric { flex:1; text-align:center; }
  .game-metric-label { font-size:10px; color:var(--text3); text-transform:uppercase; letter-spacing:0.5px; }
  .game-metric-val { font-size:20px; font-weight:800; color:var(--text); }
  .game-metric-val.fast { color:var(--accent3); }
  .game-metric-val.slow { color:var(--danger); }
  .game-field { flex:1; background:var(--bg3); border-radius:var(--radius); position:relative; overflow:hidden; min-height:320px; display:flex; align-items:center; justify-content:center; user-select:none; }
  .game-overlay { position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:12px; background:var(--bg3); z-index:10; }
  .game-overlay h2 { font-size:28px; font-weight:800; }
  .game-overlay p { color:var(--text2); font-size:14px; }

  /* Reaction targets */
  .reaction-target { width:80px; height:80px; border-radius:50%; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:24px; position:absolute; transform:translate(-50%,-50%); transition:transform 0.1s; animation:popIn 0.15s ease; box-shadow:0 0 20px currentColor; }
  @keyframes popIn { from{transform:translate(-50%,-50%) scale(0)}to{transform:translate(-50%,-50%) scale(1)} }
  .reaction-target:hover { transform:translate(-50%,-50%) scale(1.1); }
  .target-pulse { animation:pulse 1s infinite; }
  @keyframes pulse { 0%,100%{box-shadow:0 0 20px currentColor}50%{box-shadow:0 0 40px currentColor,0 0 80px currentColor} }

  /* Memory cards */
  .memory-grid { display:grid; gap:8px; padding:16px; }
  .mem-cell { aspect-ratio:1; border-radius:8px; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:22px; transition:var(--transition); border:2px solid transparent; }
  .mem-cell.highlight { border-color:var(--accent2); box-shadow:0 0 15px var(--accent); animation:memFlash 0.3s ease; }
  @keyframes memFlash { 0%,100%{opacity:1}50%{opacity:0.5} }
  .mem-cell:hover { transform:scale(1.05); }
  .mem-cell.correct { border-color:var(--accent3); }
  .mem-cell.wrong { border-color:var(--danger); animation:shake 0.3s ease; }
  @keyframes shake { 0%,100%{transform:translateX(0)}25%{transform:translateX(-5px)}75%{transform:translateX(5px)} }

  /* Focus grid */
  .focus-grid { display:grid; gap:6px; padding:16px; max-width:400px; margin:0 auto; }
  .focus-cell { aspect-ratio:1; border-radius:8px; background:var(--bg2); border:1px solid var(--border); cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:18px; font-weight:700; color:var(--text2); transition:var(--transition); }
  .focus-cell:hover { background:var(--bg4); color:var(--text); border-color:var(--accent); }
  .focus-cell.target { color:var(--accent2); border-color:var(--accent2); }
  .focus-cell.wrong-click { background:rgba(239,68,68,0.2); border-color:var(--danger); animation:shake 0.3s ease; }

  /* Color focus */
  .color-grid { display:grid; gap:10px; padding:16px; }
  .color-swatch { border-radius:10px; cursor:pointer; aspect-ratio:1; transition:var(--transition); position:relative; border:3px solid transparent; }
  .color-swatch:hover { transform:scale(1.05); }
  .color-swatch.selected { border-color:#fff; }

  /* Aim trainer */
  .aim-target { width:60px; height:60px; border-radius:50%; position:absolute; cursor:crosshair; transform:translate(-50%,-50%); display:flex; align-items:center; justify-content:center; animation:popIn 0.15s ease; box-shadow:0 0 20px currentColor; }
  .aim-inner { width:20px; height:20px; border-radius:50%; background:#fff; }

  /* Distraction mode */
  .fake-notif { position:absolute; background:var(--bg2); border:1px solid var(--border); border-radius:10px; padding:12px 16px; width:240px; box-shadow:var(--shadow); cursor:pointer; animation:slideIn 0.3s ease; z-index:5; }
  @keyframes slideIn { from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:translateX(0)} }
  .fake-notif-app { font-size:10px; color:var(--text3); margin-bottom:4px; font-weight:600; }
  .fake-notif-text { font-size:12px; color:var(--text); line-height:1.4; }
  .focus-target { width:60px; height:60px; border:3px solid var(--accent3); border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:24px; cursor:pointer; animation:breathe 2s infinite; }
  @keyframes breathe { 0%,100%{transform:scale(1);box-shadow:0 0 0 0 rgba(6,214,160,0.4)}50%{transform:scale(1.05);box-shadow:0 0 0 20px rgba(6,214,160,0)} }

  /* Analytics */
  .analytics-row { display:grid; grid-template-columns:1fr 1fr; gap:16px; margin-bottom:16px; }
  .streak-flame { font-size:32px; animation:flicker 1.5s infinite; }
  @keyframes flicker { 0%,100%{opacity:1;transform:scaleY(1)}50%{opacity:0.8;transform:scaleY(0.97)} }
  .progress-ring { position:relative; width:80px; height:80px; margin:0 auto 8px; }
  .progress-ring svg { transform:rotate(-90deg); }
  .ring-text { position:absolute; inset:0; display:flex; align-items:center; justify-content:center; font-size:16px; font-weight:800; color:var(--accent2); }

  /* Achievements */
  .achievement-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(180px,1fr)); gap:12px; }
  .ach-card { background:var(--bg3); border:1px solid var(--border); border-radius:var(--radius); padding:16px; text-align:center; transition:var(--transition); }
  .ach-card.unlocked { border-color:var(--gold); background:rgba(245,158,11,0.05); }
  .ach-card.locked { opacity:0.4; }
  .ach-icon { font-size:28px; margin-bottom:8px; }
  .ach-name { font-size:12px; font-weight:700; margin-bottom:4px; }
  .ach-desc { font-size:10px; color:var(--text3); }
  .ach-xp { font-size:10px; color:var(--gold); font-weight:700; margin-top:6px; }

  /* Settings */
  .settings-section { margin-bottom:24px; }
  .settings-title { font-size:14px; font-weight:700; margin-bottom:12px; color:var(--text2); text-transform:uppercase; letter-spacing:0.5px; }
  .setting-row { display:flex; align-items:center; justify-content:space-between; padding:12px 0; border-bottom:1px solid var(--border); }
  .setting-label { font-size:14px; font-weight:500; }
  .setting-sub { font-size:12px; color:var(--text3); margin-top:2px; }
  .toggle { width:44px; height:24px; border-radius:12px; background:var(--border2); border:none; cursor:pointer; position:relative; transition:var(--transition); flex-shrink:0; }
  .toggle.on { background:var(--accent); }
  .toggle::after { content:''; width:18px; height:18px; border-radius:50%; background:#fff; position:absolute; top:3px; left:3px; transition:var(--transition); }
  .toggle.on::after { left:23px; }
  .theme-grid { display:grid; grid-template-columns:repeat(5,1fr); gap:8px; margin-top:12px; }
  .theme-btn { padding:8px; border-radius:8px; border:2px solid var(--border); cursor:pointer; text-align:center; font-size:11px; font-weight:600; transition:var(--transition); }
  .theme-btn.active { border-color:var(--accent); }
  .theme-preview { width:30px; height:20px; border-radius:4px; margin:0 auto 4px; }

  /* AI Coach */
  .coach-panel { display:flex; gap:16px; margin-bottom:16px; }
  .coach-avatar { width:60px; height:60px; border-radius:50%; background:linear-gradient(135deg,var(--accent),var(--accent3)); display:flex; align-items:center; justify-content:center; font-size:28px; flex-shrink:0; box-shadow:var(--glow); }
  .coach-bubble { background:var(--bg3); border:1px solid var(--border); border-radius:16px 16px 16px 4px; padding:14px 18px; font-size:13px; line-height:1.6; color:var(--text); flex:1; }
  .training-plan { display:grid; gap:8px; }
  .plan-item { display:flex; align-items:center; gap:12px; padding:12px; background:var(--bg3); border-radius:var(--radius); }
  .plan-icon { font-size:20px; width:36px; height:36px; border-radius:8px; background:rgba(124,58,237,0.15); display:flex; align-items:center; justify-content:center; flex-shrink:0; }
  .plan-name { font-size:13px; font-weight:600; }
  .plan-desc { font-size:11px; color:var(--text3); }
  .plan-duration { margin-left:auto; font-size:12px; color:var(--accent2); font-weight:600; }

  /* Leaderboard */
  .lb-row { display:flex; align-items:center; gap:12px; padding:12px; border-radius:var(--radius); margin-bottom:6px; background:var(--bg3); transition:var(--transition); }
  .lb-row:hover { background:var(--bg4); }
  .lb-row.you { border:1px solid var(--accent); background:rgba(124,58,237,0.08); }
  .lb-rank { font-size:14px; font-weight:800; width:28px; text-align:center; color:var(--text3); }
  .lb-rank.gold { color:#ffd700; }
  .lb-rank.silver { color:#c0c0c0; }
  .lb-rank.bronze { color:#cd7f32; }
  .lb-avatar { width:34px; height:34px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:14px; font-weight:700; flex-shrink:0; }
  .lb-name { font-size:13px; font-weight:600; flex:1; }
  .lb-score { font-size:15px; font-weight:800; color:var(--accent2); }
  .lb-level { font-size:11px; color:var(--text3); }

  /* Toast */
  #toast { position:fixed; top:20px; right:20px; z-index:1000; pointer-events:none; }
  .toast-item { background:var(--bg2); border:1px solid var(--border); border-radius:10px; padding:12px 18px; margin-bottom:8px; font-size:13px; box-shadow:var(--shadow); animation:toastIn 0.3s ease; display:flex; align-items:center; gap:8px; }
  @keyframes toastIn { from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:translateX(0)} }
  .toast-success { border-color:var(--accent3); }
  .toast-warning { border-color:var(--gold); }

  /* Sound controls */
  .sound-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; }
  .sound-btn { padding:12px; background:var(--bg3); border:1px solid var(--border); border-radius:var(--radius); cursor:pointer; text-align:center; font-size:12px; font-weight:600; transition:var(--transition); }
  .sound-btn.active { border-color:var(--accent); color:var(--accent2); background:rgba(124,58,237,0.08); }
  .sound-btn:hover { background:var(--bg4); }
  .volume-row { display:flex; align-items:center; gap:12px; margin-top:12px; }
  .volume-row input[type=range] { flex:1; accent-color:var(--accent); }

  /* Modal */
  .modal-bg { position:fixed; inset:0; background:rgba(0,0,0,0.7); display:flex; align-items:center; justify-content:center; z-index:200; backdrop-filter:blur(8px); display:none; }
  .modal-bg.open { display:flex; }
  .modal { background:var(--bg2); border:1px solid var(--border); border-radius:var(--radius2); padding:28px; max-width:440px; width:90%; animation:modalIn 0.3s ease; }
  @keyframes modalIn { from{opacity:0;transform:scale(0.95)}to{opacity:1;transform:scale(1)} }
  .modal h2 { font-size:22px; font-weight:800; margin-bottom:8px; }
  .modal p { color:var(--text2); font-size:14px; line-height:1.6; margin-bottom:20px; }
  .result-stats { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom:20px; }
  .result-stat { background:var(--bg3); border-radius:var(--radius); padding:12px; text-align:center; }
  .result-stat-val { font-size:24px; font-weight:800; color:var(--accent2); }
  .result-stat-label { font-size:11px; color:var(--text3); text-transform:uppercase; letter-spacing:0.5px; }
  .star-row { display:flex; justify-content:center; gap:4px; font-size:28px; margin-bottom:8px; }
  .xp-gain { text-align:center; font-size:16px; color:var(--gold); font-weight:700; margin-bottom:16px; }

  /* Responsive */
  @media(max-width:768px) {
    .sidebar { display:none; }
    .grid-2,.grid-3,.analytics-row { grid-template-columns:1fr; }
    .dash-grid { grid-template-columns:1fr 1fr; }
    .modes-grid { grid-template-columns:1fr; }
    .theme-grid { grid-template-columns:repeat(3,1fr); }
  }

  /* Animations */
  .fade-in { animation:fadeIn 0.3s ease; }
  @keyframes fadeIn { from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)} }
  .spin { animation:spin 1s linear infinite; }
  @keyframes spin { to{transform:rotate(360deg)} }
</style>
</head>
<body>

<canvas id="particles-canvas"></canvas>

<div id="toast"></div>

<div class="modal-bg" id="result-modal">
  <div class="modal">
    <div class="star-row" id="modal-stars">⭐⭐⭐</div>
    <h2 id="modal-title">Session Complete!</h2>
    <div class="xp-gain" id="modal-xp">+320 XP Earned</div>
    <div class="result-stats" id="modal-stats"></div>
    <div style="display:flex;gap:10px">
      <button class="btn btn-primary" style="flex:1" onclick="closeModal();startGame(currentGame)">▶ Play Again</button>
      <button class="btn btn-ghost" style="flex:1" onclick="closeModal();showView('games')">← Back</button>
    </div>
  </div>
</div>

<div class="app">
  <!-- Sidebar -->
  <aside class="sidebar">
    <div class="sidebar-logo">
      <div class="logo-icon">⚡</div>
      <div>
        <div class="logo-text">MindSprint</div>
        <div class="logo-sub">Pro</div>
      </div>
    </div>

    <div class="nav-section">Main</div>
    <div class="nav-item active" onclick="showView('dashboard')"><span class="nav-icon">🏠</span> Dashboard</div>
    <div class="nav-item" onclick="showView('games')"><span class="nav-icon">🎮</span> Games <span class="nav-badge">6</span></div>
    <div class="nav-item" onclick="showView('analytics')"><span class="nav-icon">📊</span> Analytics</div>
    <div class="nav-item" onclick="showView('leaderboard')"><span class="nav-icon">🏆</span> Leaderboard</div>

    <div class="nav-section">Training</div>
    <div class="nav-item" onclick="showView('coach')"><span class="nav-icon">🤖</span> AI Coach</div>
    <div class="nav-item" onclick="showView('achievements')"><span class="nav-icon">🎖️</span> Achievements</div>
    <div class="nav-item" onclick="showView('challenges')"><span class="nav-icon">🔥</span> Daily Challenges</div>

    <div class="nav-section">Settings</div>
    <div class="nav-item" onclick="showView('settings')"><span class="nav-icon">⚙️</span> Settings</div>

    <div class="sidebar-footer">
      <div class="user-info">
        <div class="user-avatar" id="sb-avatar">🎯</div>
        <div>
          <div class="user-name" id="sb-name">Sprinter</div>
          <div class="user-rank" id="sb-rank">⚡ Level 7 — Elite</div>
        </div>
      </div>
      <div class="xp-bar-wrap">
        <div class="xp-bar-label"><span>XP Progress</span><span id="sb-xp">2840 / 3000</span></div>
        <div class="xp-bar"><div class="xp-bar-fill" id="sb-xp-bar" style="width:94%"></div></div>
      </div>
    </div>
  </aside>

  <!-- Main -->
  <main class="main">
    <div class="topbar">
      <div class="topbar-title" id="topbar-title">Dashboard</div>
      <div class="topbar-stat">🔥 Streak <span id="tb-streak">7</span></div>
      <div class="topbar-stat">⚡ Level <span id="tb-level">7</span></div>
      <div class="topbar-stat">🏅 Rank <span id="tb-rank">#42</span></div>
      <button class="btn btn-primary btn-sm" onclick="showView('games')">▶ Play Now</button>
    </div>

    <div class="content">

      <!-- Dashboard -->
      <div class="view active" id="view-dashboard">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">Welcome back, Sprinter! 👋</h1>
          <p style="color:var(--text2);font-size:14px">Your focus score improved by <span style="color:var(--accent3);font-weight:700">+12%</span> this week. Keep it up!</p>
        </div>
        <div class="dash-grid">
          <div class="stat-card">
            <div class="stat-label">Today's Focus Score</div>
            <div class="stat-value accent" id="dash-focus">847</div>
            <div class="stat-trend">↑ +23 from yesterday</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Avg Reaction Time</div>
            <div class="stat-value green" id="dash-reaction">241ms</div>
            <div class="stat-trend">↑ 15ms faster this week</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Accuracy</div>
            <div class="stat-value accent" id="dash-accuracy">94.2%</div>
            <div class="stat-trend">↑ +1.4% from last week</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Daily Streak</div>
            <div class="stat-value gold" id="dash-streak">🔥 7</div>
            <div class="stat-sub">Personal best: 14 days</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Total Sessions</div>
            <div class="stat-value" id="dash-sessions">142</div>
            <div class="stat-sub">48 min today</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Best Score</div>
            <div class="stat-value gold">1,240</div>
            <div class="stat-sub">Reaction Tap · 2 days ago</div>
          </div>
        </div>
        <div class="grid-2">
          <div class="card">
            <div class="card-title">📈 Weekly Progress</div>
            <div class="chart-wrap"><canvas id="weekly-chart" aria-label="Weekly progress chart"></canvas></div>
          </div>
          <div class="card">
            <div class="card-title">🎮 Game Performance</div>
            <div class="chart-wrap"><canvas id="radar-chart" aria-label="Radar chart of game performance"></canvas></div>
          </div>
        </div>
        <div class="card" style="margin-bottom:16px">
          <div class="card-title">🔥 Daily Challenges</div>
          <div style="display:grid;gap:8px" id="daily-challenges-list"></div>
        </div>
        <div class="card">
          <div class="card-title">⚡ Quick Play</div>
          <div style="display:flex;gap:10px;flex-wrap:wrap" id="quick-play-btns"></div>
        </div>
      </div>

      <!-- Games -->
      <div class="view" id="view-games">
        <div style="margin-bottom:20px;display:flex;align-items:center;justify-content:space-between">
          <div>
            <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">Game Modes</h1>
            <p style="color:var(--text2);font-size:14px">Choose your training challenge</p>
          </div>
          <div style="display:flex;gap:8px" id="timer-btns">
            <button class="btn btn-ghost btn-sm" onclick="setTimer(30)">30s</button>
            <button class="btn btn-ghost btn-sm" onclick="setTimer(60)">1m</button>
            <button class="btn btn-primary btn-sm" onclick="setTimer(180)">3m</button>
            <button class="btn btn-ghost btn-sm" onclick="setTimer(300)">5m</button>
          </div>
        </div>
        <div class="modes-grid" id="modes-container"></div>
      </div>

      <!-- Game Arena -->
      <div class="view" id="view-arena">
        <div style="margin-bottom:16px;display:flex;align-items:center;gap:10px">
          <button class="btn btn-ghost btn-sm" onclick="exitGame()">← Back</button>
          <h1 style="font-size:18px;font-weight:800" id="arena-title">Game</h1>
          <div style="margin-left:auto;display:flex;gap:8px">
            <button class="btn btn-ghost btn-sm" id="pause-btn" onclick="togglePause()">⏸ Pause</button>
          </div>
        </div>
        <div class="game-arena">
          <div class="game-score-bar">
            <div class="game-metric"><div class="game-metric-label">Score</div><div class="game-metric-val" id="g-score">0</div></div>
            <div class="game-metric"><div class="game-metric-label">Time</div><div class="game-metric-val" id="g-time">3:00</div></div>
            <div class="game-metric"><div class="game-metric-label">Hits</div><div class="game-metric-val" id="g-hits">0</div></div>
            <div class="game-metric"><div class="game-metric-label">Accuracy</div><div class="game-metric-val" id="g-acc">—</div></div>
            <div class="game-metric"><div class="game-metric-label">Best RT</div><div class="game-metric-val" id="g-rt">—</div></div>
          </div>
          <div class="game-field" id="game-field">
            <div class="game-overlay" id="game-overlay">
              <div style="font-size:48px">🎯</div>
              <h2 id="overlay-title">Ready?</h2>
              <p id="overlay-desc">Press Start to begin</p>
              <button class="btn btn-primary" onclick="beginGame()">▶ Start Game</button>
            </div>
          </div>
        </div>
      </div>

      <!-- Analytics -->
      <div class="view" id="view-analytics">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">Analytics</h1>
          <p style="color:var(--text2);font-size:14px">Detailed performance insights</p>
        </div>
        <div class="dash-grid" style="margin-bottom:16px">
          <div class="stat-card">
            <div class="stat-label">Consistency Score</div>
            <div class="stat-value accent">87%</div>
            <div class="stat-trend">↑ Very consistent</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Improvement Rate</div>
            <div class="stat-value green">+12%</div>
            <div class="stat-sub">vs last week</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Total XP</div>
            <div class="stat-value gold">28,400</div>
            <div class="stat-sub">Level 7 — 160 to next</div>
          </div>
          <div class="stat-card">
            <div class="stat-label">Training Time</div>
            <div class="stat-value">24.5h</div>
            <div class="stat-sub">This month</div>
          </div>
        </div>
        <div class="analytics-row">
          <div class="card">
            <div class="card-title">📅 Monthly Progress</div>
            <div class="chart-wrap"><canvas id="monthly-chart" aria-label="Monthly progress line chart"></canvas></div>
          </div>
          <div class="card">
            <div class="card-title">⚡ Reaction Distribution</div>
            <div class="chart-wrap"><canvas id="reaction-dist-chart" aria-label="Reaction time distribution bar chart"></canvas></div>
          </div>
        </div>
        <div class="grid-3">
          <div class="card" style="text-align:center">
            <div class="card-title" style="justify-content:center">🎯 Accuracy</div>
            <div class="progress-ring">
              <svg width="80" height="80" viewBox="0 0 80 80">
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--border2)" stroke-width="8"/>
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--accent)" stroke-width="8" stroke-dasharray="213.6" stroke-dashoffset="12" stroke-linecap="round"/>
              </svg>
              <div class="ring-text">94%</div>
            </div>
            <div style="font-size:12px;color:var(--text3)">Average accuracy</div>
          </div>
          <div class="card" style="text-align:center">
            <div class="card-title" style="justify-content:center">🔥 Focus</div>
            <div class="progress-ring">
              <svg width="80" height="80" viewBox="0 0 80 80">
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--border2)" stroke-width="8"/>
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--accent3)" stroke-width="8" stroke-dasharray="213.6" stroke-dashoffset="26" stroke-linecap="round"/>
              </svg>
              <div class="ring-text" style="color:var(--accent3)">87%</div>
            </div>
            <div style="font-size:12px;color:var(--text3)">Focus retention</div>
          </div>
          <div class="card" style="text-align:center">
            <div class="card-title" style="justify-content:center">🏃 Speed</div>
            <div class="progress-ring">
              <svg width="80" height="80" viewBox="0 0 80 80">
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--border2)" stroke-width="8"/>
                <circle cx="40" cy="40" r="34" fill="none" stroke="var(--gold)" stroke-width="8" stroke-dasharray="213.6" stroke-dashoffset="43" stroke-linecap="round"/>
              </svg>
              <div class="ring-text" style="color:var(--gold)">80%</div>
            </div>
            <div style="font-size:12px;color:var(--text3)">Speed percentile</div>
          </div>
        </div>
        <div style="display:flex;gap:10px;margin-top:8px">
          <button class="btn btn-primary" onclick="exportPDF()">📄 Export PDF Report</button>
          <button class="btn btn-ghost">Share Progress</button>
        </div>
      </div>

      <!-- Leaderboard -->
      <div class="view" id="view-leaderboard">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">🏆 Leaderboard</h1>
          <p style="color:var(--text2);font-size:14px">Global rankings — updated daily</p>
        </div>
        <div style="display:flex;gap:8px;margin-bottom:16px" id="lb-tabs">
          <button class="btn btn-primary btn-sm">Global</button>
          <button class="btn btn-ghost btn-sm">Friends</button>
          <button class="btn btn-ghost btn-sm">Weekly</button>
        </div>
        <div class="card" id="lb-list"></div>
      </div>

      <!-- AI Coach -->
      <div class="view" id="view-coach">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">🤖 AI Coach</h1>
          <p style="color:var(--text2);font-size:14px">Personalized training recommendations</p>
        </div>
        <div class="coach-panel">
          <div class="coach-avatar">🤖</div>
          <div class="coach-bubble" id="coach-message">Analyzing your performance data... Based on your last 7 sessions, your reaction time has improved by 15ms. However, I've noticed your accuracy drops in the final minute of longer sessions — this suggests attention fatigue. I recommend focusing on Distraction Resistance Mode to build mental stamina, followed by short Focus Grid sessions to reset your concentration span.</div>
        </div>
        <div class="card" style="margin-bottom:16px">
          <div class="card-title">📅 Today's Training Plan</div>
          <div class="training-plan" id="training-plan"></div>
        </div>
        <div class="grid-2">
          <div class="card">
            <div class="card-title">📊 Performance Prediction</div>
            <div class="chart-wrap"><canvas id="predict-chart" aria-label="Performance prediction chart"></canvas></div>
          </div>
          <div class="card">
            <div class="card-title">💡 Today's Tips</div>
            <div id="tips-list" style="display:grid;gap:8px"></div>
          </div>
        </div>
      </div>

      <!-- Achievements -->
      <div class="view" id="view-achievements">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">🎖️ Achievements</h1>
          <p style="color:var(--text2);font-size:14px">Unlock badges by hitting milestones</p>
        </div>
        <div class="achievement-grid" id="achievements-grid"></div>
      </div>

      <!-- Daily Challenges -->
      <div class="view" id="view-challenges">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">🔥 Daily Challenges</h1>
          <p style="color:var(--text2);font-size:14px">Complete for bonus XP and badges</p>
        </div>
        <div class="grid-2">
          <div id="daily-ch-list" style="display:grid;gap:10px"></div>
          <div>
            <div class="card" style="margin-bottom:12px">
              <div class="card-title">📅 Weekly Missions</div>
              <div id="weekly-missions" style="display:grid;gap:8px"></div>
            </div>
            <div class="card">
              <div class="card-title">🏅 Reward Preview</div>
              <div style="text-align:center;padding:16px">
                <div style="font-size:48px;margin-bottom:8px">🏆</div>
                <div style="font-weight:700;margin-bottom:4px">Week Champion</div>
                <div style="color:var(--text3);font-size:12px">Complete all 7 daily challenges this week</div>
                <div style="color:var(--gold);font-weight:700;margin-top:8px">+1,000 XP + Exclusive Badge</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Settings -->
      <div class="view" id="view-settings">
        <div style="margin-bottom:20px">
          <h1 style="font-size:22px;font-weight:800;margin-bottom:4px">⚙️ Settings</h1>
        </div>
        <div class="card" style="margin-bottom:16px">
          <div class="settings-section">
            <div class="settings-title">Theme</div>
            <div class="theme-grid">
              <div class="theme-btn active" onclick="setTheme('')">
                <div class="theme-preview" style="background:linear-gradient(135deg,#0a0a0f,#7c3aed)"></div>
                Cyber Dark
              </div>
              <div class="theme-btn" onclick="setTheme('cyber')">
                <div class="theme-preview" style="background:linear-gradient(135deg,#050510,#00f5ff)"></div>
                Cyber Neon
              </div>
              <div class="theme-btn" onclick="setTheme('gold')">
                <div class="theme-preview" style="background:linear-gradient(135deg,#0c0a00,#f59e0b)"></div>
                Dark Gold
              </div>
              <div class="theme-btn" onclick="setTheme('space')">
                <div class="theme-preview" style="background:linear-gradient(135deg,#010408,#3b82f6)"></div>
                Space Blue
              </div>
              <div class="theme-btn" onclick="setTheme('amoled')">
                <div class="theme-preview" style="background:#000;border:1px solid #333"></div>
                AMOLED
              </div>
              <div class="theme-btn" onclick="setTheme('light')">
                <div class="theme-preview" style="background:linear-gradient(135deg,#f8f7ff,#a855f7)"></div>
                Light Minimal
              </div>
            </div>
          </div>
          <div class="settings-section">
            <div class="settings-title">Audio</div>
            <div class="setting-row">
              <div><div class="setting-label">Sound Effects</div><div class="setting-sub">Clicks, hits, and feedback sounds</div></div>
              <button class="toggle on" id="sfx-toggle" onclick="this.classList.toggle('on')"></button>
            </div>
            <div class="setting-row">
              <div><div class="setting-label">Focus Music</div><div class="setting-sub">Ambient background music while playing</div></div>
              <button class="toggle" id="music-toggle" onclick="this.classList.toggle('on');toggleMusic()"></button>
            </div>
            <div class="volume-row">
              <span style="font-size:12px;color:var(--text3)">Volume</span>
              <input type="range" min="0" max="100" value="60" id="volume-slider" oninput="setVolume(this.value)">
              <span style="font-size:12px;color:var(--text2);min-width:30px" id="vol-label">60%</span>
            </div>
            <div class="sound-grid" style="margin-top:12px">
              <div class="sound-btn" onclick="playSound('focus');this.classList.toggle('active')">🎵 Focus Beats</div>
              <div class="sound-btn" onclick="playSound('nature');this.classList.toggle('active')">🌿 Nature Sounds</div>
              <div class="sound-btn" onclick="playSound('rain');this.classList.toggle('active')">🌧️ Rain</div>
              <div class="sound-btn" onclick="playSound('space');this.classList.toggle('active')">🌌 Space Ambience</div>
            </div>
          </div>
          <div class="settings-section">
            <div class="settings-title">Gameplay</div>
            <div class="setting-row">
              <div><div class="setting-label">Haptic Feedback</div><div class="setting-sub">Vibrate on mobile devices</div></div>
              <button class="toggle on" onclick="this.classList.toggle('on')"></button>
            </div>
            <div class="setting-row">
              <div><div class="setting-label">Show Milliseconds</div><div class="setting-sub">Display precise reaction times</div></div>
              <button class="toggle on" onclick="this.classList.toggle('on')"></button>
            </div>
            <div class="setting-row">
              <div><div class="setting-label">Difficulty Auto-Scale</div><div class="setting-sub">Increase difficulty based on performance</div></div>
              <button class="toggle on" onclick="this.classList.toggle('on')"></button>
            </div>
            <div class="setting-row">
              <div><div class="setting-label">Reduced Motion</div><div class="setting-sub">Minimize animations for accessibility</div></div>
              <button class="toggle" onclick="this.classList.toggle('on')"></button>
            </div>
          </div>
          <div class="settings-section">
            <div class="settings-title">Account</div>
            <div class="setting-row">
              <div><div class="setting-label">Username</div></div>
              <input type="text" value="Sprinter" style="background:var(--bg3);border:1px solid var(--border);border-radius:6px;padding:6px 10px;color:var(--text);font-size:13px;width:140px">
            </div>
            <div style="margin-top:12px;display:flex;gap:10px">
              <button class="btn btn-primary" onclick="toast('Settings saved!','success')">Save Changes</button>
              <button class="btn btn-ghost">Reset Stats</button>
              <button class="btn btn-danger">Delete Account</button>
            </div>
          </div>
        </div>
      </div>

    </div><!-- end content -->
  </main>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script>
// ─── State ───────────────────────────────────────────────────────────────────
const state = {
  xp: 2840, level: 7, streak: 7, sessions: 142,
  focusScore: 847, bestReaction: 241, accuracy: 94.2,
  totalXP: 28400, rank: 42,
  sessionDuration: 180,
  achievements: []
};

let currentGame = null, gameInterval = null, gameRunning = false, gamePaused = false;
let gameTime = 180, gameScore = 0, gameHits = 0, gameMisses = 0, gameRT = [], lastTargetTime = 0;
let memSequence = [], memPlayer = [], memStep = 0, memPhase = 'show';
let focusNumbers = [], focusNext = 1, focusGridSize = 5;
let aimInterval = null, distractionInterval = null;
let colorLevel = 1, colorTarget = null;
let audioCtx = null, musicNode = null;
let volume = 0.6;

// ─── Particles ───────────────────────────────────────────────────────────────
(function() {
  const c = document.getElementById('particles-canvas');
  const ctx = c.getContext('2d');
  let W,H,particles = [];
  function resize() { W = c.width = window.innerWidth; H = c.height = window.innerHeight; }
  window.addEventListener('resize', resize); resize();
  for(let i=0;i<60;i++) particles.push({x:Math.random()*2000,y:Math.random()*2000,r:Math.random()*1.5+0.5,vx:(Math.random()-0.5)*0.3,vy:(Math.random()-0.5)*0.3,o:Math.random()*0.5+0.1});
  function draw() {
    ctx.clearRect(0,0,W,H);
    particles.forEach(p => {
      p.x+=p.vx; p.y+=p.vy;
      if(p.x<0)p.x=W; if(p.x>W)p.x=0; if(p.y<0)p.y=H; if(p.y>H)p.y=0;
      ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
      ctx.fillStyle=`rgba(168,85,247,${p.o})`; ctx.fill();
    });
    requestAnimationFrame(draw);
  }
  draw();
})();

// ─── Navigation ──────────────────────────────────────────────────────────────
function showView(id) {
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  document.getElementById('view-'+id)?.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n=>{ if(n.textContent.trim().toLowerCase().includes(id.split('-')[0].toLowerCase())) n.classList.add('active'); });
  const titles = {dashboard:'Dashboard',games:'Game Modes',arena:'Game Arena',analytics:'Analytics',leaderboard:'Leaderboard',coach:'AI Coach',achievements:'Achievements',challenges:'Daily Challenges',settings:'Settings'};
  document.getElementById('topbar-title').textContent = titles[id]||id;
  stopGame();
  if(id==='leaderboard') renderLeaderboard();
  if(id==='dashboard') setTimeout(initDashCharts,100);
  if(id==='analytics') setTimeout(initAnalyticsCharts,100);
  if(id==='coach') setTimeout(initCoachCharts,100);
}

// ─── Toast ───────────────────────────────────────────────────────────────────
function toast(msg, type='success') {
  const el = document.createElement('div');
  el.className = `toast-item toast-${type}`;
  el.innerHTML = `${type==='success'?'✅':type==='warning'?'⚠️':'ℹ️'} ${msg}`;
  document.getElementById('toast').appendChild(el);
  setTimeout(()=>el.remove(),3000);
}

// ─── Theme ───────────────────────────────────────────────────────────────────
function setTheme(t) {
  document.body.className = t ? 'theme-'+t : '';
  document.querySelectorAll('.theme-btn').forEach((b,i)=>b.classList.remove('active'));
  event.target.closest('.theme-btn').classList.add('active');
  toast('Theme applied!','success');
}

// ─── Timer ───────────────────────────────────────────────────────────────────
function setTimer(secs) {
  state.sessionDuration = secs;
  document.querySelectorAll('#timer-btns .btn').forEach(b=>{ b.className='btn btn-ghost btn-sm'; });
  event.target.className = 'btn btn-primary btn-sm';
  toast(`Session: ${secs<60?secs+'s':secs/60+'m'}`,'success');
}

// ─── Game Modes ──────────────────────────────────────────────────────────────
const GAMES = [
  {id:'reaction',name:'Reaction Tap',icon:'⚡',desc:'Tap targets the moment they appear. Measures pure reaction speed in milliseconds.',diff:'hard',color:'#7c3aed',bestRT:'241ms',plays:47},
  {id:'color',name:'Color Focus',icon:'🎨',desc:'Find the target color among distractors. Difficulty increases automatically.',diff:'med',color:'#06d6a0',bestRT:'—',plays:23},
  {id:'memory',name:'Memory Flash',icon:'🧠',desc:'Watch the sequence flash, then repeat it perfectly. Trains working memory.',diff:'med',color:'#f59e0b',bestRT:'—',plays:31},
  {id:'focus',name:'Focus Grid',icon:'🔢',desc:'Click numbers in correct order as fast as possible. Sharpens concentration.',diff:'easy',color:'#3b82f6',bestRT:'—',plays:55},
  {id:'aim',name:'Aim Trainer',icon:'🎯',desc:'Hit moving targets with precision. Speed escalates over time.',diff:'hard',color:'#ef4444',bestRT:'—',plays:38},
  {id:'distraction',name:'Distraction Resistance',icon:'🧘',desc:'Fake notifications appear — resist clicking them. Only hit the real target.',diff:'med',color:'#a855f7',bestRT:'—',plays:19},
];

function renderModes() {
  const c = document.getElementById('modes-container');
  c.innerHTML = GAMES.map(g=>`
    <div class="mode-card" onclick="startGame('${g.id}')">
      <div class="mode-icon">${g.icon}</div>
      <div class="mode-name">${g.name}</div>
      <div class="mode-desc">${g.desc}</div>
      <div class="mode-stats">
        <span class="mode-stat">🎮 <strong>${g.plays}</strong> plays</span>
        ${g.bestRT!=='—'?`<span class="mode-stat">⚡ Best <strong>${g.bestRT}</strong></span>`:''}
      </div>
      <span class="diff-badge diff-${g.diff}">${g.diff}</span>
    </div>
  `).join('');
}

// ─── Start Game ──────────────────────────────────────────────────────────────
function startGame(id) {
  currentGame = id;
  showView('arena');
  const g = GAMES.find(x=>x.id===id);
  document.getElementById('arena-title').textContent = g.name + ' ' + g.icon;
  document.getElementById('g-score').textContent = '0';
  document.getElementById('g-hits').textContent = '0';
  document.getElementById('g-acc').textContent = '—';
  document.getElementById('g-rt').textContent = '—';
  gameTime = state.sessionDuration;
  updateTimerDisplay();
  resetGameState();
  const overlay = document.getElementById('game-overlay');
  overlay.style.display = 'flex';
  document.getElementById('overlay-title').textContent = g.name;
  document.getElementById('overlay-desc').textContent = g.desc;
}

function beginGame() {
  document.getElementById('game-overlay').style.display = 'none';
  gameRunning = true; gamePaused = false;
  gameScore=0; gameHits=0; gameMisses=0; gameRT=[];
  gameTime = state.sessionDuration;
  const field = document.getElementById('game-field');
  field.innerHTML = '';
  switch(currentGame) {
    case 'reaction': runReactionGame(); break;
    case 'color': runColorGame(); break;
    case 'memory': runMemoryGame(); break;
    case 'focus': runFocusGame(); break;
    case 'aim': runAimGame(); break;
    case 'distraction': runDistractionGame(); break;
  }
  gameInterval = setInterval(tickTimer,1000);
}

function tickTimer() {
  if(gamePaused) return;
  gameTime--;
  updateTimerDisplay();
  if(gameTime<=0) endGame();
}

function updateTimerDisplay() {
  const m = Math.floor(gameTime/60), s = gameTime%60;
  document.getElementById('g-time').textContent = `${m}:${s.toString().padStart(2,'0')}`;
  document.getElementById('g-time').className = 'game-metric-val' + (gameTime<=10?' slow':'');
}

function resetGameState() {
  clearInterval(gameInterval); clearInterval(aimInterval); clearInterval(distractionInterval);
  if(aimInterval) clearInterval(aimInterval);
  memSequence=[]; memPlayer=[]; memStep=0; colorLevel=1; focusNext=1;
  aimInterval=null; distractionInterval=null;
}

function togglePause() {
  gamePaused = !gamePaused;
  document.getElementById('pause-btn').textContent = gamePaused ? '▶ Resume' : '⏸ Pause';
  if(gamePaused) {
    const o = document.getElementById('game-overlay');
    o.style.display='flex';
    document.getElementById('overlay-title').textContent = '⏸ Paused';
    document.getElementById('overlay-desc').textContent = '';
    document.querySelector('#game-overlay button').textContent = '▶ Resume';
    document.querySelector('#game-overlay button').onclick = ()=>{ gamePaused=false; o.style.display='none'; document.getElementById('pause-btn').textContent='⏸ Pause'; };
  }
}

function exitGame() { stopGame(); showView('games'); }
function stopGame() {
  gameRunning=false;
  clearInterval(gameInterval);
  clearInterval(aimInterval);
  clearInterval(distractionInterval);
  document.getElementById('game-field').innerHTML='';
}

function updateScoreBar() {
  document.getElementById('g-score').textContent = gameScore;
  document.getElementById('g-hits').textContent = gameHits;
  const total = gameHits+gameMisses;
  if(total>0) document.getElementById('g-acc').textContent = Math.round(gameHits/total*100)+'%';
  if(gameRT.length>0) document.getElementById('g-rt').textContent = Math.min(...gameRT)+'ms';
}

function endGame() {
  stopGame();
  const xpGain = Math.round(gameScore/10 * (1+state.streak*0.05));
  state.xp += xpGain; state.sessions++;
  if(state.xp>=3000) { state.level++; state.xp-=3000; toast('🎉 Level Up! You reached Level '+state.level,'success'); }
  updateSidebar();
  showResultModal(xpGain);
}

function showResultModal(xp) {
  const stars = gameScore>500?'⭐⭐⭐':gameScore>200?'⭐⭐':'⭐';
  document.getElementById('modal-stars').textContent = stars;
  document.getElementById('modal-title').textContent = gameScore>500?'Outstanding! 🔥':gameScore>200?'Great Session! 💪':'Keep Going! 🎯';
  document.getElementById('modal-xp').textContent = `+${xp} XP Earned`;
  const total = gameHits+gameMisses;
  const acc = total>0?Math.round(gameHits/total*100):0;
  const bestRT = gameRT.length>0?Math.min(...gameRT)+' ms':'—';
  document.getElementById('modal-stats').innerHTML = `
    <div class="result-stat"><div class="result-stat-val">${gameScore}</div><div class="result-stat-label">Score</div></div>
    <div class="result-stat"><div class="result-stat-val">${gameHits}</div><div class="result-stat-label">Hits</div></div>
    <div class="result-stat"><div class="result-stat-val">${acc}%</div><div class="result-stat-label">Accuracy</div></div>
    <div class="result-stat"><div class="result-stat-val">${bestRT}</div><div class="result-stat-label">Best RT</div></div>
  `;
  document.getElementById('result-modal').classList.add('open');
}

function closeModal() { document.getElementById('result-modal').classList.remove('open'); }

// ─── Reaction Game ────────────────────────────────────────────────────────────
function runReactionGame() {
  const field = document.getElementById('game-field');
  field.style.cursor = 'crosshair';
  field.onclick = () => { gameMisses++; updateScoreBar(); };
  spawnTarget();
}

function spawnTarget() {
  if(!gameRunning||gamePaused) return;
  const field = document.getElementById('game-field');
  const colors = ['#7c3aed','#06d6a0','#f59e0b','#ef4444','#3b82f6','#a855f7'];
  const emojis = ['🎯','⚡','💥','🔴','⭐','🎪'];
  const color = colors[Math.floor(Math.random()*colors.length)];
  const t = document.createElement('div');
  t.className = 'reaction-target target-pulse';
  t.style.cssText = `left:${15+Math.random()*70}%;top:${15+Math.random()*70}%;color:${color};background:${color}22;`;
  t.textContent = emojis[Math.floor(Math.random()*emojis.length)];
  lastTargetTime = Date.now();
  const delay = 800+Math.random()*2000;
  t.onclick = (e) => {
    e.stopPropagation();
    const rt = Date.now()-lastTargetTime;
    gameRT.push(rt); gameHits++;
    const pts = Math.max(10,Math.round(1000/rt*50));
    gameScore+=pts; t.remove();
    playBeep(800,0.1);
    if(gameRunning) setTimeout(spawnTarget,300+Math.random()*600);
    updateScoreBar();
  };
  field.querySelectorAll('.reaction-target').forEach(el=>el.remove());
  field.appendChild(t);
  setTimeout(()=>{ if(t.parentNode){ t.remove(); gameMisses++; updateScoreBar(); if(gameRunning)setTimeout(spawnTarget,200); } }, delay+2500);
}

// ─── Color Focus ──────────────────────────────────────────────────────────────
function runColorGame() {
  const field = document.getElementById('game-field');
  field.innerHTML='<div id="color-area" style="width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;padding:20px"></div>';
  renderColorRound();
}

function renderColorRound() {
  if(!gameRunning) return;
  const area = document.getElementById('color-area');
  const n = Math.min(4+colorLevel*2, 16);
  const cols = Math.min(4,Math.ceil(Math.sqrt(n)));
  const hue = Math.floor(Math.random()*360);
  colorTarget = hue;
  const swatches = [hue];
  while(swatches.length<n) { let h=(hue+(Math.random()*80-40+360))%360; if(Math.abs(h-hue)>10)swatches.push(h); }
  for(let i=swatches.length-1;i>0;i--){let j=Math.floor(Math.random()*(i+1));[swatches[i],swatches[j]]=[swatches[j],swatches[i]];}
  area.innerHTML = `
    <div style="font-size:13px;color:var(--text2);margin-bottom:8px">Find the <strong style="color:hsl(${hue},80%,60%)">target color</strong> — Level ${colorLevel}</div>
    <div style="display:grid;grid-template-columns:repeat(${cols},1fr);gap:8px;width:min(320px,100%)">
      ${swatches.map(h=>`<div class="color-swatch" style="background:hsl(${h},75%,55%)" onclick="colorClick(${h},${hue})"></div>`).join('')}
    </div>
    <div style="display:flex;align-items:center;gap:8px;margin-top:8px">
      <div style="width:24px;height:24px;border-radius:4px;background:hsl(${hue},80%,60%)"></div>
      <span style="font-size:12px;color:var(--text3)">Match this shade</span>
    </div>`;
}

function colorClick(picked, target) {
  if(Math.abs(picked-target)<15||(picked>345&&target<15)||(target>345&&picked<15)) {
    gameHits++; gameScore+=10+colorLevel*5; colorLevel++; playBeep(600,0.1);
  } else { gameMisses++; gameScore=Math.max(0,gameScore-5); playBeep(200,0.1); }
  updateScoreBar(); setTimeout(renderColorRound,400);
}

// ─── Memory Game ──────────────────────────────────────────────────────────────
function runMemoryGame() {
  const field = document.getElementById('game-field');
  field.innerHTML = '<div id="mem-area" style="width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;padding:16px"><div id="mem-info" style="font-size:13px;color:var(--text2)">Watch the sequence...</div><div id="mem-grid" class="memory-grid" style="grid-template-columns:repeat(4,1fr);width:min(280px,90%)"></div></div>';
  const emojis = ['🔴','🟡','🟢','🔵','🟣','🟠','⭐','💎'];
  memSequence = []; memPlayer = []; memStep = 1;
  const grid = document.getElementById('mem-grid');
  grid.innerHTML = emojis.map((e,i)=>`<div class="mem-cell" style="background:var(--bg4);font-size:22px" id="mc${i}" onclick="memClick(${i})">${e}</div>`).join('');
  newMemRound();
}

function newMemRound() {
  memPhase = 'show'; memPlayer = [];
  memSequence.push(Math.floor(Math.random()*8));
  document.getElementById('mem-info').textContent = `Sequence length: ${memSequence.length} — Watch carefully...`;
  let i=0;
  const showNext = ()=>{
    if(i>0) document.getElementById('mc'+memSequence[i-1]).classList.remove('highlight');
    if(i<memSequence.length) {
      document.getElementById('mc'+memSequence[i]).classList.add('highlight');
      playBeep(300+memSequence[i]*50,0.08);
      i++; setTimeout(showNext,600);
    } else { memPhase='input'; document.getElementById('mem-info').textContent='Now repeat the sequence!'; }
  };
  setTimeout(showNext,600);
}

function memClick(idx) {
  if(memPhase!=='input'||!gameRunning) return;
  memPlayer.push(idx);
  const k=memPlayer.length-1;
  if(memSequence[k]===idx) {
    document.getElementById('mc'+idx).classList.add('correct');
    setTimeout(()=>document.getElementById('mc'+idx).classList.remove('correct'),300);
    if(memPlayer.length===memSequence.length) {
      gameHits++; gameScore+=memSequence.length*20; updateScoreBar(); playBeep(800,0.1);
      document.getElementById('mem-info').textContent='✅ Correct! Next round...';
      setTimeout(newMemRound,800);
    }
  } else {
    document.getElementById('mc'+idx).classList.add('wrong');
    setTimeout(()=>document.getElementById('mc'+idx).classList.remove('wrong'),400);
    gameMisses++; gameScore=Math.max(0,gameScore-10); updateScoreBar(); playBeep(150,0.1);
    document.getElementById('mem-info').textContent='❌ Wrong! Starting over...';
    memSequence=[]; setTimeout(()=>{ memSequence=[]; newMemRound(); },900);
  }
}

// ─── Focus Grid ───────────────────────────────────────────────────────────────
function runFocusGame() {
  focusNext=1;
  const field = document.getElementById('game-field');
  field.innerHTML='<div id="fg-area" style="width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:8px;padding:12px"><div id="fg-info" style="font-size:13px;color:var(--text2)">Click numbers 1→25 in order</div><div id="fg-grid" class="focus-grid" style="grid-template-columns:repeat(5,1fr);width:min(320px,90%)"></div></div>';
  renderFocusGrid();
}

function renderFocusGrid() {
  const nums = Array.from({length:25},(_,i)=>i+1).sort(()=>Math.random()-0.5);
  const grid = document.getElementById('fg-grid');
  grid.innerHTML = nums.map(n=>`<div class="focus-cell ${n===focusNext?'target':''}" id="fn${n}" onclick="focusClick(${n})">${n}</div>`).join('');
}

function focusClick(n) {
  if(!gameRunning||gamePaused) return;
  if(n===focusNext) {
    document.getElementById('fn'+n).style.cssText='background:rgba(124,58,237,0.3);color:var(--accent);pointer-events:none;opacity:0.5';
    gameHits++; gameScore+=10+(focusNext>12?5:0); focusNext++;
    if(focusNext<=25) {
      const next = document.getElementById('fn'+focusNext);
      if(next) next.classList.add('target');
    }
    if(focusNext>25) { gameScore+=200; toast('🎉 Grid Complete! +200 bonus','success'); setTimeout(runFocusGame,400); focusNext=1; }
    updateScoreBar(); playBeep(500+n*10,0.08);
  } else {
    const el = document.getElementById('fn'+n);
    el.classList.add('wrong-click');
    setTimeout(()=>el.classList.remove('wrong-click'),300);
    gameMisses++; gameScore=Math.max(0,gameScore-5); updateScoreBar(); playBeep(200,0.08);
  }
}

// ─── Aim Trainer ──────────────────────────────────────────────────────────────
function runAimGame() {
  const field = document.getElementById('game-field');
  field.style.cursor='crosshair';
  field.onclick=()=>{gameMisses++;updateScoreBar();};
  spawnAimTarget();
  let speed=1;
  aimInterval = setInterval(()=>{ speed+=0.05; }, 3000);
}

function spawnAimTarget() {
  if(!gameRunning) return;
  const field = document.getElementById('game-field');
  field.querySelectorAll('.aim-target').forEach(e=>e.remove());
  const colors = ['#ef4444','#f59e0b','#06d6a0','#7c3aed','#3b82f6'];
  const col = colors[Math.floor(Math.random()*colors.length)];
  const size = Math.max(30, 70-gameHits*2);
  const t = document.createElement('div');
  t.className='aim-target';
  t.style.cssText=`left:${10+Math.random()*80}%;top:${10+Math.random()*80}%;width:${size}px;height:${size}px;background:${col}33;color:${col};border:2px solid ${col};`;
  t.innerHTML='<div class="aim-inner"></div>';
  lastTargetTime = Date.now();
  t.onclick=(e)=>{
    e.stopPropagation();
    const rt=Date.now()-lastTargetTime; gameRT.push(rt);
    gameHits++; gameScore+=Math.max(10,Math.round(500/rt*30)); playBeep(700,0.1);
    t.remove(); updateScoreBar(); if(gameRunning)setTimeout(spawnAimTarget,200);
  };
  field.appendChild(t);
  const timeout = Math.max(800,2500-gameHits*30);
  setTimeout(()=>{ if(t.parentNode){t.remove();gameMisses++;updateScoreBar();if(gameRunning)spawnAimTarget();} },timeout);
}

// ─── Distraction Resistance ────────────────────────────────────────────────────
const fakeNotifs = [
  {app:'Messages',text:'Hey! Are you free tonight?'},
  {app:'Twitter',text:'🔥 Trending: New AI breaks records'},
  {app:'Email',text:'You\'ve won a $500 Amazon gift card!'},
  {app:'YouTube',text:'New video: 10 things you didn\'t know...'},
  {app:'Instagram',text:'@user just posted a photo'},
  {app:'News',text:'BREAKING: Major development in...'},
];

function runDistractionGame() {
  const field = document.getElementById('game-field');
  field.innerHTML = `
    <div id="dist-area" style="width:100%;height:100%;position:relative;display:flex;align-items:center;justify-content:center">
      <div id="dist-target" class="focus-target" onclick="distHit()">🎯</div>
    </div>`;
  let notifCount=0;
  distractionInterval = setInterval(()=>{
    if(!gameRunning||gamePaused) return;
    const area = document.getElementById('dist-area');
    if(!area) return;
    const n = fakeNotifs[notifCount%fakeNotifs.length]; notifCount++;
    const el = document.createElement('div');
    el.className='fake-notif';
    el.style.cssText=`top:${10+Math.random()*70}%;right:10px;`;
    el.innerHTML=`<div class="fake-notif-app">${n.app}</div><div class="fake-notif-text">${n.text}</div>`;
    el.onclick=()=>{ gameMisses++; gameScore=Math.max(0,gameScore-30); updateScoreBar(); el.remove(); playBeep(200,0.1); toast('❌ Distracted! -30 pts','warning'); };
    area.appendChild(el);
    setTimeout(()=>el.remove(),3000);
  },2000);
}

function distHit() {
  if(!gameRunning||gamePaused) return;
  gameHits++; gameScore+=50; updateScoreBar(); playBeep(700,0.1);
  const t=document.getElementById('dist-target');
  if(t){t.style.left=10+Math.random()*70+'%';t.style.top=10+Math.random()*70+'%';}
}

// ─── Audio ────────────────────────────────────────────────────────────────────
function getAudioCtx() { if(!audioCtx) audioCtx=new(window.AudioContext||window.webkitAudioContext)(); return audioCtx; }
function playBeep(freq,vol=0.2) {
  if(!document.getElementById('sfx-toggle').classList.contains('on')) return;
  try {
    const ctx=getAudioCtx();
    const o=ctx.createOscillator(); const g=ctx.createGain();
    o.connect(g); g.connect(ctx.destination);
    o.frequency.value=freq; o.type='sine';
    g.gain.setValueAtTime(vol*volume,ctx.currentTime);
    g.gain.exponentialRampToValueAtTime(0.001,ctx.currentTime+0.15);
    o.start(); o.stop(ctx.currentTime+0.15);
  } catch(e){}
}
function setVolume(v) { volume=v/100; document.getElementById('vol-label').textContent=v+'%'; }
function toggleMusic() { toast('Focus music '+(document.getElementById('music-toggle').classList.contains('on')?'started':'stopped'),'success'); }
function playSound(t) { toast(`🎵 ${t} sound selected`,'success'); }

// ─── Charts ───────────────────────────────────────────────────────────────────
let chartsInitialized = {};
function initDashCharts() {
  if(chartsInitialized.dash) return; chartsInitialized.dash=true;
  new Chart(document.getElementById('weekly-chart'),{
    type:'bar',
    data:{labels:['Mon','Tue','Wed','Thu','Fri','Sat','Sun'],datasets:[{label:'Focus Score',data:[720,780,810,760,847,830,870],backgroundColor:'rgba(124,58,237,0.6)',borderColor:'#7c3aed',borderWidth:2,borderRadius:6},{label:'Accuracy %',data:[88,90,92,91,94,93,95],backgroundColor:'rgba(6,214,160,0.4)',borderColor:'#06d6a0',borderWidth:2,borderRadius:6}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{beginAtZero:false,min:700,grid:{color:'rgba(255,255,255,0.05)'},ticks:{color:'#6b6685'}},x:{grid:{display:false},ticks:{color:'#6b6685'}}}}
  });
  new Chart(document.getElementById('radar-chart'),{
    type:'radar',
    data:{labels:['Reaction','Memory','Focus','Accuracy','Speed','Consistency'],datasets:[{label:'Your Stats',data:[85,72,87,94,80,88],backgroundColor:'rgba(124,58,237,0.2)',borderColor:'#7c3aed',borderWidth:2,pointBackgroundColor:'#a855f7',pointRadius:4},{label:'Avg Player',data:[65,60,70,75,65,70],backgroundColor:'rgba(168,85,247,0.05)',borderColor:'rgba(168,85,247,0.3)',borderWidth:1,borderDash:[4,4],pointRadius:3}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{r:{beginAtZero:true,max:100,grid:{color:'rgba(255,255,255,0.08)'},pointLabels:{color:'#a09bbf',font:{size:11}},ticks:{display:false}}}}
  });
}

function initAnalyticsCharts() {
  if(chartsInitialized.analytics) return; chartsInitialized.analytics=true;
  new Chart(document.getElementById('monthly-chart'),{
    type:'line',
    data:{labels:['W1','W2','W3','W4'],datasets:[{label:'Focus',data:[720,760,810,847],borderColor:'#7c3aed',backgroundColor:'rgba(124,58,237,0.1)',fill:true,tension:0.4,borderWidth:2,pointRadius:4,pointBackgroundColor:'#7c3aed'},{label:'Accuracy',data:[88,90,92,94],borderColor:'#06d6a0',backgroundColor:'rgba(6,214,160,0.05)',fill:true,tension:0.4,borderWidth:2,pointRadius:4,pointBackgroundColor:'#06d6a0'}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:'rgba(255,255,255,0.05)'},ticks:{color:'#6b6685'}},x:{grid:{display:false},ticks:{color:'#6b6685'}}}}
  });
  new Chart(document.getElementById('reaction-dist-chart'),{
    type:'bar',
    data:{labels:['<200ms','200-250ms','250-300ms','300-350ms','350ms+'],datasets:[{label:'Frequency',data:[12,35,28,15,8],backgroundColor:['#06d6a0','#7c3aed','#f59e0b','#ef4444','#6b7280'],borderRadius:6}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:'rgba(255,255,255,0.05)'},ticks:{color:'#6b6685'}},x:{grid:{display:false},ticks:{color:'#6b6685'}}}}
  });
}

function initCoachCharts() {
  if(chartsInitialized.coach) return; chartsInitialized.coach=true;
  new Chart(document.getElementById('predict-chart'),{
    type:'line',
    data:{labels:['Now','1 week','2 weeks','1 month','3 months'],datasets:[{label:'Projected RT (ms)',data:[241,228,215,190,160],borderColor:'#06d6a0',backgroundColor:'rgba(6,214,160,0.1)',fill:true,tension:0.4,borderWidth:2,borderDash:[6,3],pointRadius:4,pointBackgroundColor:'#06d6a0'},{label:'Focus Score',data:[847,890,930,980,1100],borderColor:'#7c3aed',backgroundColor:'rgba(124,58,237,0.05)',fill:true,tension:0.4,borderWidth:2,pointRadius:4,pointBackgroundColor:'#7c3aed'}]},
    options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{grid:{color:'rgba(255,255,255,0.05)'},ticks:{color:'#6b6685'}},x:{grid:{display:false},ticks:{color:'#6b6685'}}}}
  });
}

// ─── Leaderboard ──────────────────────────────────────────────────────────────
const LB_DATA = [
  {name:'NovaMind',score:2841,level:15,avatar:'🧠',color:'#7c3aed'},
  {name:'ReflexKing',score:2650,level:14,avatar:'⚡',color:'#f59e0b'},
  {name:'FocusPro',score:2480,level:13,avatar:'🎯',color:'#06d6a0'},
  {name:'ZenFlow',score:2310,level:12,avatar:'🧘',color:'#3b82f6'},
  {name:'SwiftAim',score:2180,level:11,avatar:'🏹',color:'#ef4444'},
  {name:'MindWave',score:2050,level:10,avatar:'🌊',color:'#a855f7'},
  {name:'SpeedDemon',score:1980,level:9,avatar:'👻',color:'#f59e0b'},
  {name:'Sprinter',score:1840,level:7,avatar:'🎯',color:'#7c3aed',you:true},
  {name:'CalmChaos',score:1720,level:8,avatar:'🌀',color:'#06d6a0'},
  {name:'NeonBurst',score:1650,level:7,avatar:'💥',color:'#ef4444'},
];

function renderLeaderboard() {
  const medals = ['gold','silver','bronze'];
  document.getElementById('lb-list').innerHTML = LB_DATA.map((p,i)=>`
    <div class="lb-row ${p.you?'you':''}">
      <div class="lb-rank ${medals[i]||''}">${i<3?['🥇','🥈','🥉'][i]:i+1}</div>
      <div class="lb-avatar" style="background:${p.color}22;color:${p.color}">${p.avatar}</div>
      <div><div class="lb-name">${p.name}${p.you?' (You)':''}</div><div class="lb-level">Level ${p.level}</div></div>
      <div class="lb-score">${p.score.toLocaleString()}</div>
    </div>`).join('');
}

// ─── Achievements ─────────────────────────────────────────────────────────────
const ACHIEVEMENTS = [
  {icon:'⚡',name:'Speed Demon',desc:'Get under 200ms reaction',xp:'+200 XP',unlocked:true},
  {icon:'🎯',name:'Dead Eye',desc:'100% accuracy in Aim Trainer',xp:'+300 XP',unlocked:true},
  {icon:'🧠',name:'Memory Master',desc:'Repeat a 10-item sequence',xp:'+250 XP',unlocked:true},
  {icon:'🔥',name:'On Fire',desc:'7-day streak',xp:'+500 XP',unlocked:true},
  {icon:'🏆',name:'Top 50',desc:'Reach global rank #50',xp:'+400 XP',unlocked:true},
  {icon:'🧘',name:'Unshakeable',desc:'Resist 50 distractions',xp:'+350 XP',unlocked:false},
  {icon:'💯',name:'Perfect Session',desc:'100% accuracy, full session',xp:'+600 XP',unlocked:false},
  {icon:'🌟',name:'Level 10',desc:'Reach level 10',xp:'+1000 XP',unlocked:false},
  {icon:'📅',name:'Month Strong',desc:'30-day streak',xp:'+2000 XP',unlocked:false},
  {icon:'🚀',name:'Rocket Speed',desc:'Sub 150ms reaction time',xp:'+800 XP',unlocked:false},
  {icon:'🔢',name:'Grid Master',desc:'Complete 10 focus grids',xp:'+400 XP',unlocked:false},
  {icon:'👑',name:'Champion',desc:'Reach rank #1',xp:'+5000 XP',unlocked:false},
];

function renderAchievements() {
  document.getElementById('achievements-grid').innerHTML = ACHIEVEMENTS.map(a=>`
    <div class="ach-card ${a.unlocked?'unlocked':'locked'}">
      <div class="ach-icon">${a.icon}</div>
      <div class="ach-name">${a.name}</div>
      <div class="ach-desc">${a.desc}</div>
      <div class="ach-xp">${a.xp}</div>
    </div>`).join('');
}

// ─── Daily Challenges ─────────────────────────────────────────────────────────
const CHALLENGES = [
  {icon:'⚡',name:'Speed Runner',desc:'Get avg reaction under 250ms',progress:80,goal:100,xp:150,done:false},
  {icon:'🎯',name:'Sharpshooter',desc:'Score 500+ in Aim Trainer',progress:100,goal:100,xp:200,done:true},
  {icon:'🧠',name:'Memory Test',desc:'Complete a 8-step sequence',progress:60,goal:100,xp:175,done:false},
  {icon:'🔥',name:'Daily Grind',desc:'Complete 3 game sessions',progress:67,goal:100,xp:100,done:false},
];

const WEEKLY = [
  {name:'Weekend Warrior',desc:'Play 15 sessions this week',progress:9,goal:15,xp:500},
  {name:'Master of All',desc:'Try every game mode',progress:5,goal:6,xp:400},
  {name:'Score Hunter',desc:'Earn 5,000 total points',progress:3200,goal:5000,xp:600},
];

function renderChallenges() {
  document.getElementById('daily-ch-list').innerHTML = CHALLENGES.map(c=>`
    <div class="plan-item">
      <div class="plan-icon">${c.icon}</div>
      <div style="flex:1">
        <div class="plan-name">${c.name} ${c.done?'✅':''}</div>
        <div class="plan-desc">${c.desc}</div>
        <div style="margin-top:6px;height:4px;background:var(--border2);border-radius:2px">
          <div style="height:100%;background:${c.done?'var(--accent3)':'var(--accent)'};border-radius:2px;width:${c.progress}%"></div>
        </div>
      </div>
      <div class="plan-duration">${c.xp} XP</div>
    </div>`).join('');

  document.getElementById('weekly-missions').innerHTML = WEEKLY.map(w=>`
    <div style="padding:10px;background:var(--bg3);border-radius:var(--radius)">
      <div style="display:flex;justify-content:space-between;margin-bottom:4px">
        <span style="font-size:12px;font-weight:600">${w.name}</span>
        <span style="font-size:11px;color:var(--gold)">${w.xp} XP</span>
      </div>
      <div style="font-size:11px;color:var(--text3);margin-bottom:6px">${w.desc}</div>
      <div style="display:flex;align-items:center;gap:6px">
        <div style="flex:1;height:4px;background:var(--border2);border-radius:2px">
          <div style="height:100%;background:var(--accent2);border-radius:2px;width:${Math.round(w.progress/w.goal*100)}%"></div>
        </div>
        <span style="font-size:10px;color:var(--text3)">${w.progress}/${w.goal}</span>
      </div>
    </div>`).join('');
}

// ─── Training Plan ────────────────────────────────────────────────────────────
const PLAN = [
  {icon:'⚡',name:'Reaction Tap Warm-up',desc:'3 min session, easy difficulty',dur:'3 min'},
  {icon:'🧘',name:'Distraction Resistance',desc:'Build mental stamina',dur:'5 min'},
  {icon:'🔢',name:'Focus Grid Sprint',desc:'2 min burst, medium difficulty',dur:'2 min'},
  {icon:'🎯',name:'Aim Trainer Cool-down',desc:'Precision practice',dur:'3 min'},
];

const TIPS = [
  {icon:'💡',text:'Take a 2-min break between sessions to prevent fatigue buildup.'},
  {icon:'🌬️',text:'Deep breathing before a session improves reaction time by up to 8%.'},
  {icon:'💧',text:'Staying hydrated is directly linked to faster cognitive processing.'},
  {icon:'🎧',text:'Binaural beats at 40Hz can enhance focus during training.'},
];

function renderCoachPlan() {
  document.getElementById('training-plan').innerHTML = PLAN.map(p=>`
    <div class="plan-item">
      <div class="plan-icon">${p.icon}</div>
      <div style="flex:1"><div class="plan-name">${p.name}</div><div class="plan-desc">${p.desc}</div></div>
      <div class="plan-duration">${p.dur}</div>
      <button class="btn btn-ghost btn-sm" onclick="startGame('${['reaction','distraction','focus','aim'][PLAN.indexOf(p)]}')">▶</button>
    </div>`).join('');
  document.getElementById('tips-list').innerHTML = TIPS.map(t=>`
    <div style="display:flex;gap:8px;padding:8px;background:var(--bg3);border-radius:8px">
      <span style="font-size:16px">${t.icon}</span>
      <span style="font-size:12px;color:var(--text2);line-height:1.5">${t.text}</span>
    </div>`).join('');
}

// ─── Dashboard extras ─────────────────────────────────────────────────────────
function renderDailyDash() {
  document.getElementById('daily-challenges-list').innerHTML = CHALLENGES.slice(0,3).map(c=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px;background:var(--bg3);border-radius:8px">
      <span>${c.icon}</span>
      <div style="flex:1">
        <div style="font-size:12px;font-weight:600">${c.name}</div>
        <div style="height:4px;background:var(--border2);border-radius:2px;margin-top:4px">
          <div style="height:100%;background:${c.done?'var(--accent3)':'var(--accent)'};border-radius:2px;width:${c.progress}%"></div>
        </div>
      </div>
      <span style="font-size:11px;color:var(--gold)">${c.xp} XP</span>
    </div>`).join('');

  document.getElementById('quick-play-btns').innerHTML = GAMES.map(g=>`
    <button class="btn btn-ghost" onclick="startGame('${g.id}')">${g.icon} ${g.name}</button>`).join('');
}

// ─── Sidebar update ───────────────────────────────────────────────────────────
function updateSidebar() {
  const xpPct = Math.round(state.xp/3000*100);
  document.getElementById('sb-xp').textContent = state.xp+' / 3000';
  document.getElementById('sb-xp-bar').style.width = xpPct+'%';
  document.getElementById('sb-rank').textContent = `⚡ Level ${state.level} — ${state.level<5?'Rookie':state.level<10?'Elite':'Pro'}`;
  document.getElementById('tb-level').textContent = state.level;
  document.getElementById('tb-streak').textContent = state.streak;
  document.getElementById('tb-rank').textContent = '#'+state.rank;
}

// ─── Export PDF ───────────────────────────────────────────────────────────────
function exportPDF() {
  toast('📄 Generating your performance report...','success');
  setTimeout(()=>{
    const data = `MINDSPRINT PRO — PERFORMANCE REPORT
Generated: ${new Date().toLocaleDateString()}

PLAYER: Sprinter | Level ${state.level} | Rank #${state.rank}

SUMMARY
  Focus Score: ${state.focusScore}
  Avg Reaction: ${state.bestReaction}ms
  Accuracy: ${state.accuracy}%
  Streak: ${state.streak} days
  Total Sessions: ${state.sessions}

ACHIEVEMENTS: 5 unlocked

Report generated by MindSprint Pro`;
    const blob = new Blob([data],{type:'text/plain'});
    const a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = 'mindsprint-report.txt';
    a.click();
    toast('✅ Report downloaded!','success');
  },1500);
}

// ─── Init ─────────────────────────────────────────────────────────────────────
renderModes();
renderAchievements();
renderChallenges();
renderDailyDash();
renderCoachPlan();
renderLeaderboard();
updateSidebar();
setTimeout(initDashCharts, 200);

// PWA manifest
const manifest = {name:'MindSprint Pro',short_name:'MindSprint',display:'standalone',theme_color:'#0a0a0f',background_color:'#0a0a0f',icons:[{src:'data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>⚡</text></svg>',sizes:'any',type:'image/svg+xml'}]};
const blob = new Blob([JSON.stringify(manifest)],{type:'application/json'});
document.querySelector('[rel=manifest]').href = URL.createObjectURL(blob);
</script>
</body>
</html>
