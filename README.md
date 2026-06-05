<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Carlos Alexandre</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #0a0a0f;
      --surface: #0f0f1a;
      --surface2: #141425;
      --border: #1e1e3a;
      --accent: #00ff88;
      --accent2: #0088ff;
      --accent3: #7c3aed;
      --text: #e2e8f0;
      --muted: #64748b;
      --glow: 0 0 20px rgba(0, 255, 136, 0.3);
      --glow2: 0 0 20px rgba(0, 136, 255, 0.3);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'JetBrains Mono', monospace;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 40px 20px 60px;
      position: relative;
      overflow-x: hidden;
    }

    /* Grid background */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,255,136,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,255,136,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    /* Radial glow center */
    body::after {
      content: '';
      position: fixed;
      top: -20%;
      left: 50%;
      transform: translateX(-50%);
      width: 600px;
      height: 600px;
      background: radial-gradient(circle, rgba(0,136,255,0.08) 0%, transparent 70%);
      pointer-events: none;
      z-index: 0;
    }

    .container {
      width: 100%;
      max-width: 420px;
      position: relative;
      z-index: 1;
    }

    /* ── TERMINAL BAR ── */
    .terminal-bar {
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 10px 10px 0 0;
      padding: 10px 16px;
      display: flex;
      align-items: center;
      gap: 8px;
      margin-bottom: -1px;
    }

    .dot { width: 10px; height: 10px; border-radius: 50%; }
    .dot-r { background: #ff5f57; }
    .dot-y { background: #ffbd2e; }
    .dot-g { background: #28c840; }

    .terminal-title {
      font-size: 11px;
      color: var(--muted);
      margin-left: 8px;
      letter-spacing: 0.05em;
    }

    /* ── PROFILE CARD ── */
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 0 0 16px 16px;
      padding: 32px 24px 28px;
      margin-bottom: 12px;
    }

    .profile-section {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 16px;
      margin-bottom: 28px;
    }

    .avatar-wrapper {
      position: relative;
      width: 90px;
      height: 90px;
    }

    .avatar-ring {
      position: absolute;
      inset: -3px;
      border-radius: 50%;
      background: conic-gradient(var(--accent), var(--accent2), var(--accent3), var(--accent));
      animation: spin 4s linear infinite;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }

    .avatar-inner {
      position: absolute;
      inset: 2px;
      border-radius: 50%;
      background: var(--bg);
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .avatar-placeholder {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      background: linear-gradient(135deg, var(--surface2), var(--border));
      font-size: 28px;
      color: var(--accent);
      font-weight: 700;
      letter-spacing: -1px;
    }

    .profile-info { text-align: center; }

    .name {
      font-family: 'Space Mono', monospace;
      font-size: 20px;
      font-weight: 700;
      color: #fff;
      letter-spacing: -0.5px;
      margin-bottom: 4px;
    }

    .handle {
      font-size: 12px;
      color: var(--accent);
      letter-spacing: 0.1em;
      margin-bottom: 10px;
    }

    .handle::before { content: '> '; opacity: 0.5; }

    .tags {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
      justify-content: center;
    }

    .tag {
      font-size: 10px;
      padding: 3px 10px;
      border-radius: 4px;
      font-weight: 500;
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .tag-green { background: rgba(0,255,136,0.1); color: var(--accent); border: 1px solid rgba(0,255,136,0.2); }
    .tag-blue  { background: rgba(0,136,255,0.1); color: var(--accent2); border: 1px solid rgba(0,136,255,0.2); }
    .tag-purple{ background: rgba(124,58,237,0.1); color: #a78bfa; border: 1px solid rgba(124,58,237,0.2); }

    /* ── STATS BAR ── */
    .stats {
      display: flex;
      justify-content: space-around;
      padding: 16px 0;
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      margin-bottom: 24px;
    }

    .stat { text-align: center; }

    .stat-value {
      font-family: 'Space Mono', monospace;
      font-size: 18px;
      font-weight: 700;
      color: var(--accent);
    }

    .stat-label {
      font-size: 9px;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
      margin-top: 2px;
    }

    /* ── SECTION LABEL ── */
    .section-label {
      font-size: 9px;
      color: var(--muted);
      letter-spacing: 0.15em;
      text-transform: uppercase;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .section-label::before { content: '//'; color: var(--accent3); }
    .section-label::after { content: ''; flex: 1; height: 1px; background: var(--border); }

    /* ── LINK BUTTONS ── */
    .links { display: flex; flex-direction: column; gap: 8px; }

    .link-btn {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 14px 16px;
      background: var(--surface2);
      border: 1px solid var(--border);
      border-radius: 10px;
      text-decoration: none;
      color: var(--text);
      transition: all 0.2s ease;
      position: relative;
      overflow: hidden;
      cursor: pointer;
    }

    .link-btn::before {
      content: '';
      position: absolute;
      left: 0; top: 0; bottom: 0;
      width: 3px;
      border-radius: 10px 0 0 10px;
    }

    .link-btn.instagram::before { background: linear-gradient(to bottom, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); }
    .link-btn.linkedin::before  { background: var(--accent2); box-shadow: var(--glow2); }
    .link-btn.whatsapp::before  { background: #25d366; box-shadow: 0 0 10px rgba(37,211,102,0.4); }
    .link-btn.github::before    { background: #c9d1d9; }

    .link-btn:hover {
      background: var(--border);
      transform: translateX(4px);
      border-color: rgba(255,255,255,0.1);
    }

    .link-btn:hover .link-arrow { opacity: 1; transform: translateX(0); }

    .link-icon {
      width: 38px; height: 38px;
      border-radius: 8px;
      display: flex; align-items: center; justify-content: center;
      font-size: 18px;
      flex-shrink: 0;
    }

    .link-btn.instagram .link-icon { background: linear-gradient(135deg, #f09433, #dc2743, #bc1888); }
    .link-btn.linkedin  .link-icon { background: rgba(0,136,255,0.15); border: 1px solid rgba(0,136,255,0.2); }
    .link-btn.whatsapp  .link-icon { background: rgba(37,211,102,0.15); border: 1px solid rgba(37,211,102,0.2); }
    .link-btn.github    .link-icon { background: rgba(201,209,217,0.1); border: 1px solid rgba(201,209,217,0.1); }

    .link-text { flex: 1; }

    .link-title {
      font-size: 13px;
      font-weight: 700;
      color: #fff;
      margin-bottom: 2px;
    }

    .link-sub {
      font-size: 10px;
      color: var(--muted);
    }

    .link-arrow {
      font-size: 12px;
      color: var(--muted);
      opacity: 0;
      transform: translateX(-4px);
      transition: all 0.2s;
    }

    /* ── FOOTER ── */
    .footer {
      margin-top: 28px;
      text-align: center;
      font-size: 10px;
      color: var(--muted);
      letter-spacing: 0.1em;
    }

    .footer span { color: var(--accent); }

    /* ── CURSOR BLINK ── */
    .cursor {
      display: inline-block;
      width: 8px;
      height: 14px;
      background: var(--accent);
      margin-left: 2px;
      vertical-align: middle;
      animation: blink 1s step-end infinite;
    }

    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0; }
    }

    /* ── ENTRY ANIMATIONS ── */
    .container { animation: fadeUp 0.6s ease both; }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .link-btn:nth-child(1) { animation: slideIn 0.4s 0.1s ease both; }
    .link-btn:nth-child(2) { animation: slideIn 0.4s 0.2s ease both; }
    .link-btn:nth-child(3) { animation: slideIn 0.4s 0.3s ease both; }

    @keyframes slideIn {
      from { opacity: 0; transform: translateX(-12px); }
      to   { opacity: 1; transform: translateX(0); }
    }

    /* Scanline effect */
    .scanline {
      position: fixed;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, rgba(0,255,136,0.4), transparent);
      animation: scan 3s linear infinite;
      pointer-events: none;
      z-index: 999;
    }

    @keyframes scan {
      from { top: -2px; }
      to   { top: 100vh; }
    }
  </style>
</head>
<body>

<div class="scanline"></div>

<div class="container">

  <!-- Terminal chrome -->
  <div class="terminal-bar">
    <div class="dot dot-r"></div>
    <div class="dot dot-y"></div>
    <div class="dot dot-g"></div>
    <span class="terminal-title">carlos.alexandre ~ links.sh</span>
  </div>

  <!-- Main card -->
  <div class="card">

    <div class="profile-section">
      <div class="avatar-wrapper">
        <div class="avatar-ring"></div>
        <div class="avatar-inner">
          <div class="avatar-placeholder">CA</div>
        </div>
      </div>

      <div class="profile-info">
        <div class="name">Carlos Alexandre<span class="cursor"></span></div>
        <div class="handle">carlos.sreis_</div>
        <div class="tags">
          <span class="tag tag-green">Dev</span>
          <span class="tag tag-blue">Tech</span>
          <span class="tag tag-purple">Builder</span>
        </div>
      </div>
    </div>

    <div class="stats">
      <div class="stat">
        <div class="stat-value">31</div>
        <div class="stat-label">posts</div>
      </div>
      <div class="stat">
        <div class="stat-value">5.6k</div>
        <div class="stat-label">followers</div>
      </div>
      <div class="stat">
        <div class="stat-value">999</div>
        <div class="stat-label">following</div>
      </div>
    </div>

    <div class="section-label">conecte-se</div>

    <div class="links">

      <a class="link-btn instagram"
         href="https://www.instagram.com/carlos.sreis_" target="_blank">
        <div class="link-icon">📸</div>
        <div class="link-text">
          <div class="link-title">Instagram</div>
          <div class="link-sub">@carlos.sreis_</div>
        </div>
        <span class="link-arrow">→</span>
      </a>

      <a class="link-btn linkedin"
         href="https://www.linkedin.com/in/carlos-alexandre-0392a0361" target="_blank">
        <div class="link-icon">💼</div>
        <div class="link-text">
          <div class="link-title">LinkedIn</div>
          <div class="link-sub">carlos-alexandre</div>
        </div>
        <span class="link-arrow">→</span>
      </a>

      <a class="link-btn whatsapp"
         href="https://wa.me/" target="_blank">
        <div class="link-icon">💬</div>
        <div class="link-text">
          <div class="link-title">WhatsApp</div>
          <div class="link-sub">manda um oi</div>
        </div>
        <span class="link-arrow">→</span>
      </a>

    </div>
  </div>

  <div class="footer">
    feito com <span>{"</span> código <span>"}</span> por carlos
  </div>

</div>
</body>
</html>
