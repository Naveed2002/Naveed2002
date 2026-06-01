<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Naveed Nawaz — GitHub Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;500;600;700;800&display=swap" rel="stylesheet"/>
<link href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css" rel="stylesheet"/>
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --accent:#00F5A0;--accent2:#00D4FF;--accent3:#FF6B35;
    --bg:#090E1A;--bg2:#0D1528;--bg3:#111B35;
    --border:#1E2D50;--text:#E2E8F8;--muted:#5A6A8A;--dim:#8A9ABE;
  }
  body{background:var(--bg);color:var(--text);font-family:'Syne',sans-serif;max-width:420px;margin:0 auto;overflow-x:hidden}
  .mono{font-family:'Space Mono',monospace}

  /* HEADER */
  .header{background:var(--bg2);border-bottom:1px solid var(--border);padding:16px;display:flex;align-items:center;gap:12px;position:relative}
  .header::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--accent),var(--accent2),var(--accent3))}
  .avatar{width:48px;height:48px;border-radius:12px;background:linear-gradient(135deg,#00F5A0,#00D4FF);display:flex;align-items:center;justify-content:center;font-weight:800;font-size:15px;color:#090E1A;flex-shrink:0;font-family:'Syne',sans-serif}
  .name{font-size:17px;font-weight:800;color:var(--text);letter-spacing:-0.3px}
  .handle{font-size:11px;color:var(--accent);font-family:'Space Mono',monospace;margin-top:3px}
  .role{font-size:10px;color:var(--dim);margin-top:2px}
  .badge{margin-left:auto;background:rgba(0,245,160,0.1);border:1px solid rgba(0,245,160,0.3);border-radius:6px;padding:4px 10px;font-size:10px;font-family:'Space Mono',monospace;color:var(--accent);display:flex;align-items:center;gap:5px;white-space:nowrap}
  .dot{width:6px;height:6px;border-radius:50%;background:var(--accent);animation:pulse 2s infinite}
  @keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.4;transform:scale(0.75)}}

  /* STATS */
  .stats-row{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--border)}
  .stat{background:var(--bg2);padding:14px 8px;text-align:center}
  .stat-num{font-size:22px;font-weight:800;font-family:'Space Mono',monospace;background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
  .stat-label{font-size:9px;color:var(--muted);margin-top:4px;text-transform:uppercase;letter-spacing:.9px}

  /* SECTIONS */
  .section{padding:16px}
  .sec-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
  .sec-title{font-size:10px;font-weight:600;text-transform:uppercase;letter-spacing:1.4px;color:var(--dim);font-family:'Space Mono',monospace}
  .sec-tag{font-size:10px;font-family:'Space Mono',monospace;color:var(--accent2);background:rgba(0,212,255,0.08);border:1px solid rgba(0,212,255,0.2);padding:2px 8px;border-radius:4px}
  .divider{height:1px;background:var(--border)}

  /* CONTRIBUTION GRID */
  .contrib-grid{display:grid;grid-template-columns:repeat(26,1fr);gap:2px;margin-bottom:8px}
  .cell{aspect-ratio:1;border-radius:2px;background:var(--bg3)}
  .c1{background:rgba(0,245,160,0.15)}.c2{background:rgba(0,245,160,0.35)}.c3{background:rgba(0,245,160,0.6)}.c4{background:rgba(0,245,160,0.9)}
  .contrib-footer{display:flex;align-items:center;justify-content:space-between}
  .contrib-total{font-size:11px;color:var(--dim);font-family:'Space Mono',monospace}
  .legend{display:flex;align-items:center;gap:3px}
  .legend span{font-size:9px;color:var(--muted)}
  .lg{width:9px;height:9px;border-radius:2px}

  /* REPOS */
  .repo-list{display:flex;flex-direction:column;gap:8px}
  .repo{background:var(--bg2);border:1px solid var(--border);border-radius:10px;padding:13px 14px;transition:border-color .2s,transform .15s}
  .repo:hover{border-color:rgba(0,245,160,0.35);transform:translateY(-1px)}
  .repo-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:6px}
  .repo-name{font-size:13px;font-weight:700;color:var(--accent2);font-family:'Space Mono',monospace}
  .repo-lang{font-size:10px;padding:2px 8px;border-radius:4px;font-family:'Space Mono',monospace;border:1px solid;white-space:nowrap}
  .lang-dart{color:#54C5F8;border-color:rgba(84,197,248,.3);background:rgba(84,197,248,.08)}
  .lang-js{color:#F7DF1E;border-color:rgba(247,223,30,.3);background:rgba(247,223,30,.08)}
  .lang-kt{color:#A97BFF;border-color:rgba(169,123,255,.3);background:rgba(169,123,255,.08)}
  .repo-desc{font-size:12px;color:var(--muted);line-height:1.5;margin-bottom:8px}
  .repo-meta{display:flex;align-items:center;gap:12px}
  .meta-item{display:flex;align-items:center;gap:4px;font-size:11px;color:var(--dim);font-family:'Space Mono',monospace}
  .star-icon{color:#FFB800}.fork-icon{color:var(--accent2)}
  .updated{font-size:10px;color:var(--muted);margin-left:auto}

  /* LANGUAGE BARS */
  .lang-bars{display:flex;flex-direction:column;gap:10px}
  .lang-row{display:flex;align-items:center;gap:10px}
  .lang-name{font-size:11px;font-family:'Space Mono',monospace;color:var(--dim);width:54px;flex-shrink:0}
  .lang-bar-wrap{flex:1;height:6px;background:var(--bg3);border-radius:3px;overflow:hidden}
  .lang-bar{height:100%;border-radius:3px}
  .lb-dart{background:linear-gradient(90deg,#54C5F8,#00D4FF)}
  .lb-kt{background:linear-gradient(90deg,#A97BFF,#7B53D4)}
  .lb-js{background:linear-gradient(90deg,#F7DF1E,#FFB800)}
  .lb-py{background:linear-gradient(90deg,#00F5A0,#0BD08A)}
  .lang-pct{font-size:10px;font-family:'Space Mono',monospace;color:var(--muted);width:32px;text-align:right}

  /* PULL REQUESTS */
  .pr-list{display:flex;flex-direction:column;gap:6px}
  .pr{display:flex;align-items:center;gap:10px;padding:10px 12px;background:var(--bg2);border:1px solid var(--border);border-radius:8px}
  .pr-status{width:8px;height:8px;border-radius:50%;flex-shrink:0}
  .ps-open{background:var(--accent)}.ps-review{background:var(--accent2)}.ps-merged{background:#A97BFF}
  .pr-info{flex:1}
  .pr-title{font-size:12px;color:var(--text);font-weight:500;line-height:1.3}
  .pr-sub{font-size:10px;color:var(--muted);font-family:'Space Mono',monospace;margin-top:2px}
  .pr-badge{font-size:9px;padding:2px 7px;border-radius:4px;font-family:'Space Mono',monospace;border:1px solid;flex-shrink:0}
  .pb-open{color:var(--accent);border-color:rgba(0,245,160,.3);background:rgba(0,245,160,.08)}
  .pb-review{color:var(--accent2);border-color:rgba(0,212,255,.3);background:rgba(0,212,255,.08)}
  .pb-merged{color:#A97BFF;border-color:rgba(169,123,255,.3);background:rgba(169,123,255,.08)}

  /* ACTIVITY */
  .activity-list{display:flex;flex-direction:column}
  .act-item{display:flex;align-items:flex-start;gap:10px;padding:10px 0;border-bottom:1px solid rgba(30,45,80,.7)}
  .act-item:last-child{border-bottom:none}
  .act-icon{width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:14px}
  .ai-push{background:rgba(0,245,160,0.1);border:1px solid rgba(0,245,160,0.2);color:var(--accent)}
  .ai-pr{background:rgba(0,212,255,0.1);border:1px solid rgba(0,212,255,0.2);color:var(--accent2)}
  .ai-star{background:rgba(255,184,0,0.1);border:1px solid rgba(255,184,0,0.2);color:#FFB800}
  .ai-fork{background:rgba(255,107,53,0.1);border:1px solid rgba(255,107,53,0.2);color:var(--accent3)}
  .act-info{flex:1}
  .act-title{font-size:12px;color:var(--text);line-height:1.5}
  .act-title strong{color:var(--accent2)}
  .act-time{font-size:10px;color:var(--muted);font-family:'Space Mono',monospace;margin-top:2px}

  /* FOOTER */
  .footer{padding:14px 16px;display:flex;align-items:center;justify-content:space-between;border-top:1px solid var(--border);background:var(--bg2)}
  .footer-stat{text-align:center}
  .footer-num{font-size:16px;font-weight:700;font-family:'Space Mono',monospace}
  .fn-green{color:var(--accent)}.fn-blue{color:var(--accent2)}.fn-orange{color:var(--accent3)}
  .footer-label{font-size:9px;color:var(--muted);text-transform:uppercase;letter-spacing:.7px;margin-top:2px}
</style>
</head>
<body>

<!-- HEADER -->
<div class="header">
  <div class="avatar">NN</div>
  <div>
    <div class="name">Naveed Nawaz</div>
    <div class="handle">@naveed-nawaz</div>
    <div class="role">Flutter Mobile App Developer</div>
  </div>
  <div class="badge"><span class="dot"></span>Active</div>
</div>

<!-- STATS -->
<div class="stats-row">
  <div class="stat"><div class="stat-num">47</div><div class="stat-label">Repos</div></div>
  <div class="stat"><div class="stat-num">1.2k</div><div class="stat-label">Followers</div></div>
  <div class="stat"><div class="stat-num">2.8k</div><div class="stat-label">Stars</div></div>
</div>

<!-- CONTRIBUTIONS -->
<div class="section">
  <div class="sec-header">
    <span class="sec-title">Contributions</span>
    <span class="sec-tag">1,847 this year</span>
  </div>
  <div class="contrib-grid" id="cgrid"></div>
  <div class="contrib-footer">
    <span class="contrib-total mono">Mar — Jun 2026</span>
    <div class="legend">
      <span>Less</span>
      <div class="lg" style="background:var(--bg3)"></div>
      <div class="lg c1"></div><div class="lg c2"></div><div class="lg c3"></div><div class="lg c4"></div>
      <span>More</span>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- TOP REPOS -->
<div class="section">
  <div class="sec-header">
    <span class="sec-title">Top Repositories</span>
    <span class="sec-tag">Pinned</span>
  </div>
  <div class="repo-list">
    <div class="repo">
      <div class="repo-top">
        <span class="repo-name">flutter_ui_kit</span>
        <span class="repo-lang lang-dart">Dart</span>
      </div>
      <div class="repo-desc">Futuristic component library for Flutter with glassmorphism, neon effects & adaptive theming.</div>
      <div class="repo-meta">
        <span class="meta-item"><span class="star-icon">★</span> 847</span>
        <span class="meta-item"><span class="fork-icon">⑂</span> 124</span>
        <span class="updated">2 days ago</span>
      </div>
    </div>
    <div class="repo">
      <div class="repo-top">
        <span class="repo-name">nav_animations</span>
        <span class="repo-lang lang-dart">Dart</span>
      </div>
      <div class="repo-desc">Custom route transitions & page animations package for Flutter apps.</div>
      <div class="repo-meta">
        <span class="meta-item"><span class="star-icon">★</span> 392</span>
        <span class="meta-item"><span class="fork-icon">⑂</span> 67</span>
        <span class="updated">5 days ago</span>
      </div>
    </div>
    <div class="repo">
      <div class="repo-top">
        <span class="repo-name">shop_app_flutter</span>
        <span class="repo-lang lang-kt">Kotlin</span>
      </div>
      <div class="repo-desc">Full-stack e-commerce app with Riverpod state management & Firebase backend.</div>
      <div class="repo-meta">
        <span class="meta-item"><span class="star-icon">★</span> 218</span>
        <span class="meta-item"><span class="fork-icon">⑂</span> 43</span>
        <span class="updated">1 week ago</span>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- LANGUAGE BARS -->
<div class="section">
  <div class="sec-header">
    <span class="sec-title">Language Breakdown</span>
  </div>
  <div class="lang-bars">
    <div class="lang-row">
      <span class="lang-name">Dart</span>
      <div class="lang-bar-wrap"><div class="lang-bar lb-dart" style="width:72%"></div></div>
      <span class="lang-pct">72%</span>
    </div>
    <div class="lang-row">
      <span class="lang-name">Kotlin</span>
      <div class="lang-bar-wrap"><div class="lang-bar lb-kt" style="width:14%"></div></div>
      <span class="lang-pct">14%</span>
    </div>
    <div class="lang-row">
      <span class="lang-name">JS</span>
      <div class="lang-bar-wrap"><div class="lang-bar lb-js" style="width:8%"></div></div>
      <span class="lang-pct">8%</span>
    </div>
    <div class="lang-row">
      <span class="lang-name">Python</span>
      <div class="lang-bar-wrap"><div class="lang-bar lb-py" style="width:6%"></div></div>
      <span class="lang-pct">6%</span>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- PULL REQUESTS -->
<div class="section">
  <div class="sec-header">
    <span class="sec-title">Pull Requests</span>
    <span class="sec-tag">3 active</span>
  </div>
  <div class="pr-list">
    <div class="pr">
      <div class="pr-status ps-open"></div>
      <div class="pr-info">
        <div class="pr-title">Add dark mode tokens to ui_kit</div>
        <div class="pr-sub">flutter_ui_kit · #83 · opened 3h ago</div>
      </div>
      <span class="pr-badge pb-open">Open</span>
    </div>
    <div class="pr">
      <div class="pr-status ps-review"></div>
      <div class="pr-info">
        <div class="pr-title">Refactor navigation state logic</div>
        <div class="pr-sub">nav_animations · #21 · 2 reviews</div>
      </div>
      <span class="pr-badge pb-review">Review</span>
    </div>
    <div class="pr">
      <div class="pr-status ps-merged"></div>
      <div class="pr-info">
        <div class="pr-title">Fix iOS safe area insets</div>
        <div class="pr-sub">shop_app_flutter · #67 · merged yesterday</div>
      </div>
      <span class="pr-badge pb-merged">Merged</span>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ACTIVITY FEED -->
<div class="section">
  <div class="sec-header">
    <span class="sec-title">Recent Activity</span>
  </div>
  <div class="activity-list">
    <div class="act-item">
      <div class="act-icon ai-push">↑</div>
      <div class="act-info">
        <div class="act-title">Pushed 3 commits to <strong>flutter_ui_kit</strong> — glassmorphism widget update</div>
        <div class="act-time">2 hours ago</div>
      </div>
    </div>
    <div class="act-item">
      <div class="act-icon ai-pr">⊕</div>
      <div class="act-info">
        <div class="act-title">Opened PR <strong>#83</strong> in flutter_ui_kit</div>
        <div class="act-time">3 hours ago</div>
      </div>
    </div>
    <div class="act-item">
      <div class="act-icon ai-star">★</div>
      <div class="act-info">
        <div class="act-title">Starred <strong>flutter/flutter</strong> repository</div>
        <div class="act-time">Yesterday</div>
      </div>
    </div>
    <div class="act-item">
      <div class="act-icon ai-fork">⑂</div>
      <div class="act-info">
        <div class="act-title">Forked <strong>riverpod_examples</strong> by rrousselGit</div>
        <div class="act-time">2 days ago</div>
      </div>
    </div>
  </div>
</div>

<!-- FOOTER -->
<div class="footer">
  <div class="footer-stat"><div class="footer-num fn-green">24</div><div class="footer-label">Issues Open</div></div>
  <div class="footer-stat"><div class="footer-num fn-blue">156</div><div class="footer-label">Commits/mo</div></div>
  <div class="footer-stat"><div class="footer-num fn-orange">8</div><div class="footer-label">Following</div></div>
</div>

<script>
  // Generate contribution heatmap
  const grid = document.getElementById('cgrid');
  const pattern = [0,0,1,1,2,2,3,4,3,2,1,0,1,2,3,4,4,3,2,1,2,3,4,3,2,1];
  pattern.forEach(w => {
    const d = document.createElement('div');
    d.className = 'cell' + (w ? ` c${w}` : '');
    grid.appendChild(d);
  });
</script>
</body>
</html>
