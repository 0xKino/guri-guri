<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>guri-guri</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@200;300;400;500;600&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap');

:root {
  --bg: #0C0B0F;
  --bg2: #111015;
  --fg: #E8E4DF;
  --fg-dim: #7A756D;
  --fg-faint: #3A3732;
  --accent: #E8713A;
  --warm: #F5C882;
  --rose: #D4727A;
  --sage: #8BAA7A;
  --font: 'Outfit', sans-serif;
  --mono: 'Space Mono', monospace;
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }

body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--fg);
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}

body::after {
  content: '';
  position: fixed;
  inset: 0;
  background: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.7' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 10000;
}

::selection { background: var(--accent); color: var(--bg); }
a { color: inherit; text-decoration: none; }

/* laser dot cursor */
#laserDot {
  position: fixed;
  width: 8px; height: 8px;
  background: #ff2020;
  border-radius: 50%;
  pointer-events: none;
  z-index: 9998;
  box-shadow: 0 0 12px 4px rgba(255,32,32,0.5), 0 0 30px 8px rgba(255,32,32,0.15);
  mix-blend-mode: screen;
  transition: opacity 0.2s;
  opacity: 0;
}

body:hover #laserDot { opacity: 1; }

/* ===== NAV ===== */
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 28px 48px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  mix-blend-mode: difference;
}

.nav-name { font-family: var(--mono); font-size: 0.75rem; letter-spacing: 0.08em; }
.nav-right { display: flex; gap: 32px; }
.nav-right a { font-size: 0.75rem; letter-spacing: 0.06em; color: var(--fg-dim); transition: color 0.3s; }
.nav-right a:hover { color: var(--fg); }

/* ===== HERO ===== */
.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 0 48px 80px;
  position: relative;
}

.orb {
  position: absolute; border-radius: 50%; filter: blur(120px); pointer-events: none;
  animation: drift 20s ease-in-out infinite alternate;
}
.orb-1 { width: 500px; height: 500px; background: var(--accent); opacity: 0.06; top: 10%; right: 10%; }
.orb-2 { width: 400px; height: 400px; background: var(--warm); opacity: 0.04; bottom: 20%; left: 5%; animation-delay: -7s; }
.orb-3 { width: 300px; height: 300px; background: var(--rose); opacity: 0.035; top: 40%; left: 50%; animation-delay: -14s; }

@keyframes drift {
  0% { transform: translate(0, 0) scale(1); }
  100% { transform: translate(40px, -30px) scale(1.1); }
}

.hero-title {
  font-weight: 200;
  font-size: clamp(4rem, 12vw, 10rem);
  line-height: 0.9;
  letter-spacing: -0.04em;
  position: relative; z-index: 1;
  opacity: 0;
  animation: fadeUp 1s 0.2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
.hero-title em { font-style: italic; font-weight: 300; color: var(--accent); }

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(40px); }
  to { opacity: 1; transform: translateY(0); }
}

.scroll-hint {
  position: absolute; bottom: 32px; left: 48px;
  display: flex; align-items: center; gap: 12px; z-index: 1;
}
.scroll-line {
  width: 1px; height: 48px; background: var(--fg-faint);
  position: relative; overflow: hidden;
}
.scroll-line::after {
  content: ''; position: absolute; top: -100%; width: 100%; height: 50%;
  background: var(--accent); animation: scrollPulse 2s ease-in-out infinite;
}
@keyframes scrollPulse { 0% { top: -50%; } 100% { top: 150%; } }
.scroll-text {
  font-family: var(--mono); font-size: 0.6rem; letter-spacing: 0.12em;
  color: var(--fg-faint); text-transform: uppercase; writing-mode: vertical-lr;
}

/* ===== SECTIONS ===== */
.s { padding: 160px 48px; position: relative; }
.s-label {
  font-family: var(--mono); font-size: 0.65rem; letter-spacing: 0.14em;
  text-transform: uppercase; color: var(--fg-faint); margin-bottom: 48px;
  display: flex; align-items: center; gap: 16px;
}
.s-label::before { content: ''; width: 24px; height: 1px; background: var(--fg-faint); }

.about { display: grid; grid-template-columns: 1fr 1fr; gap: 120px; max-width: 1100px; }
.about-left h2 { font-weight: 300; font-size: clamp(1.8rem, 3.5vw, 2.8rem); line-height: 1.25; letter-spacing: -0.02em; }
.about-left h2 span { color: var(--accent); }
.about-right { padding-top: 8px; }
.about-right p { font-size: 0.92rem; line-height: 1.85; color: var(--fg-dim); margin-bottom: 24px; }

/* ===== BRANDS ===== */
.brands-list { display: flex; flex-direction: column; }
.brand-row {
  display: grid; grid-template-columns: 200px 1fr 200px 48px;
  align-items: center; padding: 40px 0; border-bottom: 1px solid var(--fg-faint);
  position: relative; transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.brand-row:first-child { border-top: 1px solid var(--fg-faint); }
.brand-row:hover { padding-left: 24px; }
.brand-row:hover .brand-name { color: var(--accent); }
.brand-row:hover .brand-arrow { opacity: 1; transform: translateX(0); }
.brand-name { font-weight: 500; font-size: 1.4rem; letter-spacing: -0.01em; transition: color 0.4s; }
.brand-desc { font-size: 0.82rem; color: var(--fg-dim); line-height: 1.6; padding-right: 48px; }
.brand-tag { font-family: var(--mono); font-size: 0.6rem; letter-spacing: 0.08em; color: var(--fg-faint); text-transform: uppercase; }
.brand-arrow { font-size: 1.2rem; color: var(--accent); opacity: 0; transform: translateX(-8px); transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1); }

/* ===== MARQUEE ===== */
.marquee-wrap { overflow: hidden; padding: 80px 0; border-top: 1px solid var(--fg-faint); border-bottom: 1px solid var(--fg-faint); }
.marquee-inner { display: flex; gap: 80px; animation: slide 40s linear infinite; width: max-content; }
.marquee-inner span { font-weight: 200; font-size: clamp(3rem, 6vw, 5rem); letter-spacing: -0.03em; color: var(--fg-faint); white-space: nowrap; }
.marquee-inner span:nth-child(odd) { font-style: italic; }
.marquee-inner span .paw { display: inline-block; font-size: 0.6em; margin: 0 24px; opacity: 0.4; }
@keyframes slide { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

/* ===== TERMINAL ===== */
.term-wrap { max-width: 700px; }
.term { background: var(--bg2); border: 1px solid var(--fg-faint); border-radius: 12px; overflow: hidden; }
.term-bar { padding: 12px 16px; display: flex; gap: 6px; align-items: center; border-bottom: 1px solid var(--fg-faint); }
.term-dot { width: 8px; height: 8px; border-radius: 50%; }
.term-dot:nth-child(1) { background: #E8713A; opacity: 0.7; }
.term-dot:nth-child(2) { background: #F5C882; opacity: 0.5; }
.term-dot:nth-child(3) { background: #7A756D; opacity: 0.3; }
.term-bar span { font-family: var(--mono); font-size: 0.6rem; color: var(--fg-faint); margin-left: 8px; }
.term-body { padding: 24px; font-family: var(--mono); font-size: 0.72rem; line-height: 2.2; color: var(--fg-dim); }
.term-body .p { color: var(--accent); }
.term-body .g { color: #8BAA7A; }
.term-body .d { color: var(--fg-faint); }
.term-body .w { color: var(--warm); }

/* ===== GALLERY ===== */
.gallery { display: grid; grid-template-columns: repeat(5, 1fr); gap: 3px; max-width: 1200px; }
.gallery-cell {
  aspect-ratio: 1; background: var(--bg2); border: 1px solid var(--fg-faint); border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  position: relative; overflow: hidden;
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.gallery-cell:hover { border-color: var(--accent); transform: scale(1.04); z-index: 2; }
.gallery-cell:hover svg { transform: scale(1.08); }
.gallery-cell:hover .gallery-label { opacity: 1; transform: translateY(0); }
.gallery-cell svg { width: 70%; height: 70%; transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1); }
.gallery-label {
  position: absolute; bottom: 10px; left: 10px;
  font-family: var(--mono); font-size: 0.5rem; color: var(--fg-dim);
  letter-spacing: 0.06em; opacity: 0; transform: translateY(6px); transition: all 0.3s;
}

/* ===== CTA ===== */
.cta { text-align: center; padding: 200px 48px; }
.cta h2 { font-weight: 200; font-size: clamp(2.5rem, 6vw, 5rem); line-height: 1; letter-spacing: -0.04em; margin-bottom: 32px; }
.cta h2 em { font-style: italic; font-weight: 300; color: var(--accent); }
.cta p { color: var(--fg-dim); font-size: 0.9rem; max-width: 400px; margin: 0 auto 48px; line-height: 1.7; }
.cta-btn { display: inline-block; font-family: var(--mono); font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--bg); background: var(--accent); padding: 14px 40px; border-radius: 100px; transition: all 0.3s; }
.cta-btn:hover { transform: translateY(-2px); box-shadow: 0 12px 40px rgba(232,113,58,0.2); }

/* ===== FOOTER ===== */
.foot { padding: 48px; border-top: 1px solid var(--fg-faint); display: flex; justify-content: space-between; align-items: center; }
.foot-left { font-family: var(--mono); font-size: 0.6rem; color: var(--fg-faint); letter-spacing: 0.06em; }
.foot-right { display: flex; gap: 24px; }
.foot-right a { font-size: 0.7rem; color: var(--fg-faint); transition: color 0.3s; }
.foot-right a:hover { color: var(--accent); }

/* ===== WALKING CATS LAYER ===== */
#catWorld {
  position: fixed; inset: 0;
  pointer-events: none;
  z-index: 50;
  overflow: hidden;
}

.wanderCat {
  position: absolute;
  bottom: 0;
  transition: none;
  will-change: transform;
  image-rendering: auto;
}

/* ===== VIGNETTES ===== */
.vig {
  position: absolute; pointer-events: none;
  opacity: 0; transition: opacity 1.5s;
}
.vig.vis { opacity: 1; }

/* ===== REVEALS ===== */
.r { opacity: 0; transform: translateY(24px); transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1); }
.r.v { opacity: 1; transform: translateY(0); }

/* ===== RESPONSIVE ===== */
@media (max-width: 800px) {
  .nav { padding: 20px 24px; }
  .hero { padding: 0 24px 60px; }
  .s { padding: 100px 24px; }
  .about { grid-template-columns: 1fr; gap: 48px; }
  .brand-row { grid-template-columns: 1fr; gap: 8px; padding: 28px 0; }
  .brand-arrow, .brand-tag { display: none; }
  .gallery { grid-template-columns: repeat(2, 1fr); }
  .cta { padding: 120px 24px; }
  .foot { flex-direction: column; gap: 16px; text-align: center; }
  .scroll-hint { display: none; }
  .vig { display: none; }
  #laserDot { display: none; }
}
</style>
</head>
<body>

<div id="laserDot"></div>
<div id="catWorld"></div>

<nav class="nav">
  <span class="nav-name">guri-guri</span>
  <div class="nav-right">
    <a href="#brands">brands</a>
    <a href="#agents">agents</a>
    <a href="#world">world</a>
  </div>
</nav>

<section class="hero">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>
  <h1 class="hero-title">build<br><em>beautifully</em></h1>
  <div class="scroll-hint"><div class="scroll-line"></div><span class="scroll-text">scroll</span></div>

  <!-- Hero vignette: big cat with coffee -->
  <div class="vig vis" style="right: 6%; top: 15%;">
    <svg width="130" height="150" viewBox="0 0 130 150" fill="none" opacity="0.06">
      <ellipse cx="65" cy="100" rx="30" ry="24" fill="#E8713A"/>
      <circle cx="65" cy="60" r="24" fill="#E8713A"/>
      <path d="M46 48 L40 20 L56 44" fill="#E8713A"/>
      <path d="M84 48 L90 20 L74 44" fill="#E8713A"/>
      <ellipse cx="56" cy="57" rx="5" ry="6" fill="white"/>
      <ellipse cx="74" cy="57" rx="5" ry="6" fill="white"/>
      <circle cx="56" cy="58" r="3" fill="#0C0B0F"/>
      <circle cx="74" cy="58" r="3" fill="#0C0B0F"/>
      <path d="M95 95 Q115 72 110 45" stroke="#E8713A" stroke-width="7" fill="none" stroke-linecap="round"/>
      <rect x="80" y="108" width="18" height="16" rx="3" fill="white" opacity="0.25"/>
      <path d="M98 112 Q105 112 105 120 Q105 125 98 125" stroke="white" stroke-width="1.5" fill="none" opacity="0.2"/>
      <path d="M85 108 Q87 103 89 108" stroke="white" stroke-width="0.8" fill="none" opacity="0.15"/>
      <path d="M87 106 Q88 102 90 106" stroke="white" stroke-width="0.6" fill="none" opacity="0.1"/>
    </svg>
  </div>
</section>

<section class="s" id="about">
  <div class="s-label r">001 — about</div>
  <div class="about">
    <div class="about-left r">
      <h2>A small constellation of <span>service companies</span> for Latin American businesses entering Miami.</h2>
    </div>
    <div class="about-right r" style="transition-delay: 0.15s;">
      <p>Guri-Guri is a holding structure — not a brand you'll see on a billboard. We own and operate specialized companies, each focused on one thing done exceptionally well.</p>
      <p>Video. Immigration. Digital presence. Three discrete product suites, unified by shared infrastructure, agentic AI tooling, and an obsessive focus on the LatAm → US corridor.</p>
      <p style="color: var(--fg-faint); font-family: var(--mono); font-size: 0.7rem;">Based in Doral, FL · Wyoming holding structure · AI-native from day one</p>
    </div>
  </div>
  <!-- Vignette: cat at whiteboard with glasses -->
  <div class="vig" style="right: 3%; top: 18%;">
    <svg width="170" height="140" viewBox="0 0 170 140" fill="none" opacity="0.04">
      <rect x="40" y="8" width="85" height="58" rx="3" stroke="white" stroke-width="1.2" fill="none"/>
      <line x1="55" y1="24" x2="100" y2="24" stroke="white" stroke-width="0.8" opacity="0.5"/>
      <line x1="55" y1="34" x2="82" y2="34" stroke="white" stroke-width="0.8" opacity="0.5"/>
      <polyline points="55,52 68,46 78,50 90,30 102,26" stroke="#E8713A" stroke-width="1.5" fill="none"/>
      <ellipse cx="138" cy="90" rx="17" ry="14" fill="#888"/>
      <circle cx="138" cy="66" r="13" fill="#999"/>
      <path d="M128 58 L124 42 L134 55" fill="#999"/>
      <path d="M148 58 L152 42 L142 55" fill="#888"/>
      <ellipse cx="133" cy="65" rx="3" ry="3.5" fill="white"/>
      <ellipse cx="143" cy="65" rx="3" ry="3.5" fill="white"/>
      <circle cx="133" cy="66" r="1.8" fill="#0C0B0F"/>
      <circle cx="143" cy="66" r="1.8" fill="#0C0B0F"/>
      <circle cx="133" cy="65" r="4.5" stroke="white" stroke-width="0.8" fill="none" opacity="0.25"/>
      <circle cx="143" cy="65" r="4.5" stroke="white" stroke-width="0.8" fill="none" opacity="0.25"/>
      <line x1="125" y1="82" x2="102" y2="50" stroke="#F5C882" stroke-width="1.8" stroke-linecap="round" opacity="0.5"/>
    </svg>
  </div>
</section>

<section class="s" id="brands">
  <div class="s-label r">002 — brands</div>
  <div class="brands-list r">
    <div class="brand-row">
      <div class="brand-name">Michi Media</div>
      <div class="brand-desc">Video production, post-production, AI dubbing, and social content — from brand films to TikTok cuts.</div>
      <div class="brand-tag">video · content</div>
      <div class="brand-arrow">→</div>
    </div>
    <div class="brand-row">
      <div class="brand-name">Cruce Consulting</div>
      <div class="brand-desc">Immigration strategy, visa pathways, entity setup advisory, and relocation concierge for entrepreneurs.</div>
      <div class="brand-tag">immigration · legal</div>
      <div class="brand-arrow">→</div>
    </div>
    <div class="brand-row">
      <div class="brand-name">Nodo Studio</div>
      <div class="brand-desc">Bilingual websites, search optimization, and social media management — digital presence from zero to scale.</div>
      <div class="brand-tag">web · seo · social</div>
      <div class="brand-arrow">→</div>
    </div>
  </div>
  <!-- Vignette: tuxedo cat doing taxes -->
  <div class="vig" style="left: 2%; bottom: 4%;">
    <svg width="150" height="120" viewBox="0 0 150 120" fill="none" opacity="0.035">
      <rect x="10" y="82" width="130" height="5" rx="2" fill="white"/>
      <rect x="15" y="60" width="28" height="22" rx="1" fill="white" opacity="0.2"/>
      <rect x="17" y="57" width="28" height="22" rx="1" fill="white" opacity="0.15"/>
      <rect x="95" y="68" width="18" height="14" rx="2" fill="white" opacity="0.2"/>
      <ellipse cx="72" cy="56" rx="20" ry="15" fill="#1A1A1A" opacity="0.7"/>
      <ellipse cx="72" cy="60" rx="12" ry="8" fill="white" opacity="0.1"/>
      <circle cx="72" cy="35" r="14" fill="#1A1A1A" opacity="0.7"/>
      <path d="M62 27 L57 10 L67 24" fill="#1A1A1A" opacity="0.7"/>
      <path d="M82 27 L87 10 L77 24" fill="#1A1A1A" opacity="0.7"/>
      <ellipse cx="67" cy="34" rx="3" ry="3.5" fill="#8BAA7A" opacity="0.8"/>
      <ellipse cx="77" cy="34" rx="3" ry="3.5" fill="#8BAA7A" opacity="0.8"/>
      <circle cx="67" cy="34" r="5" stroke="white" stroke-width="0.7" fill="none" opacity="0.2"/>
      <circle cx="77" cy="34" r="5" stroke="white" stroke-width="0.7" fill="none" opacity="0.2"/>
      <line x1="56" y1="68" x2="44" y2="75" stroke="#F5C882" stroke-width="1.5" stroke-linecap="round" opacity="0.3"/>
    </svg>
  </div>
</section>

<div class="marquee-wrap">
  <div class="marquee-inner">
    <span>video<span class="paw">🐾</span></span><span>immigration<span class="paw">🐾</span></span>
    <span>digital<span class="paw">🐾</span></span><span>agents<span class="paw">🐾</span></span>
    <span>miami<span class="paw">🐾</span></span><span>latam<span class="paw">🐾</span></span>
    <span>video<span class="paw">🐾</span></span><span>immigration<span class="paw">🐾</span></span>
    <span>digital<span class="paw">🐾</span></span><span>agents<span class="paw">🐾</span></span>
    <span>miami<span class="paw">🐾</span></span><span>latam<span class="paw">🐾</span></span>
  </div>
</div>

<section class="s" id="agents">
  <div class="s-label r">003 — agents</div>
  <div class="about r">
    <div class="about-left"><h2>Every brand runs on <span>autonomous workflows</span> — not chatbots.</h2></div>
    <div class="about-right"><p>Our agent pipelines handle the repetitive: script generation, document checklists, SEO audits, social scheduling. Humans handle the nuanced: strategy, taste, relationships.</p></div>
  </div>
  <div style="height: 64px;"></div>
  <div class="term-wrap r">
    <div class="term">
      <div class="term-bar"><div class="term-dot"></div><div class="term-dot"></div><div class="term-dot"></div><span>guri-guri/agent</span></div>
      <div class="term-body" id="term"></div>
    </div>
  </div>
  <!-- Vignette: cat on video call -->
  <div class="vig" style="right: 2%; top: 12%;">
    <svg width="160" height="130" viewBox="0 0 160 130" fill="none" opacity="0.04">
      <rect x="30" y="10" width="70" height="48" rx="3" stroke="white" stroke-width="1" fill="none"/>
      <rect x="35" y="15" width="28" height="18" rx="1" fill="white" opacity="0.06"/>
      <rect x="67" y="15" width="28" height="18" rx="1" fill="white" opacity="0.06"/>
      <rect x="35" y="36" width="28" height="18" rx="1" fill="white" opacity="0.06"/>
      <rect x="67" y="36" width="28" height="18" rx="1" fill="white" opacity="0.06"/>
      <circle cx="49" cy="23" r="3.5" fill="#E8713A" opacity="0.35"/>
      <circle cx="81" cy="23" r="3.5" fill="#D4727A" opacity="0.35"/>
      <circle cx="49" cy="44" r="3.5" fill="#F5C882" opacity="0.35"/>
      <circle cx="81" cy="44" r="3.5" fill="#888" opacity="0.35"/>
      <ellipse cx="65" cy="90" rx="22" ry="17" fill="#E8713A" opacity="0.6"/>
      <circle cx="65" cy="70" r="15" fill="#E8713A" opacity="0.6"/>
      <path d="M54 62 L49 44 L60 58" fill="#E8713A" opacity="0.6"/>
      <path d="M76 62 L81 44 L70 58" fill="#E8713A" opacity="0.6"/>
      <path d="M48 66 Q48 55 65 55 Q82 55 82 66" stroke="white" stroke-width="1.5" fill="none" opacity="0.15"/>
      <rect x="44" y="62" width="6" height="10" rx="3" fill="white" opacity="0.12"/>
      <rect x="80" y="62" width="6" height="10" rx="3" fill="white" opacity="0.12"/>
    </svg>
  </div>
</section>

<section class="s" id="world">
  <div class="s-label r">004 — world</div>
  <div style="max-width: 500px; margin-bottom: 64px;" class="r">
    <h2 style="font-weight: 300; font-size: 1.6rem; line-height: 1.35;">Meet the team.</h2>
    <p style="color: var(--fg-dim); font-size: 0.85rem; line-height: 1.7; margin-top: 12px;">They're cats. They're very good at their jobs.</p>
  </div>

  <div class="gallery r">
    <!-- 1: DEV CAT typing -->
    <div class="gallery-cell">
      <svg viewBox="0 0 100 100" fill="none">
        <rect x="20" y="70" width="60" height="5" rx="2" fill="#3A3732"/>
        <rect x="28" y="55" width="36" height="15" rx="3" fill="#222" stroke="#E8713A" stroke-width="0.5" opacity="0.6"/>
        <text x="33" y="64" font-family="monospace" font-size="4" fill="#E8713A" opacity="0.4">$ deploy</text>
        <ellipse cx="50" cy="42" rx="16" ry="13" fill="#E8713A" opacity="0.85"/>
        <circle cx="50" cy="30" r="11" fill="#E8713A"/>
        <path d="M42 24 L39 12 L46 22" fill="#E8713A"/><path d="M58 24 L61 12 L54 22" fill="#E8713A"/>
        <ellipse cx="46" cy="29" rx="2.5" ry="3" fill="#0C0B0F"/><ellipse cx="54" cy="29" rx="2.5" ry="3" fill="#0C0B0F"/>
        <circle cx="47" cy="28" r="0.8" fill="white" opacity="0.6"/><circle cx="55" cy="28" r="0.8" fill="white" opacity="0.6"/>
        <path d="M49 33 L50 34.5 L51 33" fill="#C4593A"/>
        <ellipse cx="40" cy="58" rx="5" ry="3" fill="#F5C882" opacity="0.5"><animate attributeName="ry" values="3;2;3" dur="0.5s" repeatCount="indefinite"/></ellipse>
        <ellipse cx="60" cy="58" rx="5" ry="3" fill="#F5C882" opacity="0.5"><animate attributeName="ry" values="2;3;2" dur="0.5s" repeatCount="indefinite"/></ellipse>
        <path d="M66 38 Q78 28 75 16" stroke="#E8713A" stroke-width="3.5" fill="none" stroke-linecap="round"><animate attributeName="d" values="M66 38 Q78 28 75 16;M66 38 Q80 25 77 13;M66 38 Q78 28 75 16" dur="3s" repeatCount="indefinite"/></path>
      </svg>
      <span class="gallery-label">dev cat</span>
    </div>
    <!-- 2: LEGAL CAT tuxedo suit -->
    <div class="gallery-cell">
      <svg viewBox="0 0 100 100" fill="none">
        <circle cx="50" cy="28" r="14" fill="#1A1A1A"/><ellipse cx="50" cy="30" rx="8" ry="5" fill="#E8E4DF" opacity="0.12"/>
        <path d="M40 20 L36 6 L45 17" fill="#1A1A1A"/><path d="M60 20 L64 6 L55 17" fill="#1A1A1A"/>
        <ellipse cx="45" cy="27" rx="3" ry="3.5" fill="#8BAA7A"/><ellipse cx="55" cy="27" rx="3" ry="3.5" fill="#8BAA7A"/>
        <circle cx="45" cy="27" r="1.5" fill="#0C0B0F"/><circle cx="55" cy="27" r="1.5" fill="#0C0B0F"/>
        <path d="M49 32 L50 33.5 L51 32" fill="#D4727A"/>
        <path d="M36 46 L50 42 L64 46 L64 82 L36 82Z" fill="#1A1A1A" opacity="0.8"/>
        <path d="M36 46 L50 42 L64 46" fill="#3A3732"/>
        <line x1="50" y1="42" x2="50" y2="66" stroke="#E8713A" stroke-width="1.5"/>
        <path d="M48 44 L50 42 L52 44 L50 48Z" fill="#E8713A"/>
        <rect x="68" y="58" width="14" height="10" rx="2" fill="#3A3732" stroke="#E8713A" stroke-width="0.5" opacity="0.6"/>
        <path d="M72 58 L72 54 L78 54 L78 58" stroke="#E8713A" stroke-width="0.5" fill="none" opacity="0.6"/>
      </svg>
      <span class="gallery-label">legal cat</span>
    </div>
    <!-- 3: CEO CAT yacht sunglasses -->
    <div class="gallery-cell">
      <svg viewBox="0 0 100 100" fill="none">
        <circle cx="82" cy="16" r="8" fill="#F5C882" opacity="0.12"/>
        <path d="M0 72 Q25 66 50 72 Q75 78 100 72 L100 100 L0 100Z" fill="#1A2A3A" opacity="0.3"><animate attributeName="d" values="M0 72 Q25 66 50 72 Q75 78 100 72 L100 100 L0 100Z;M0 74 Q25 70 50 74 Q75 78 100 74 L100 100 L0 100Z;M0 72 Q25 66 50 72 Q75 78 100 72 L100 100 L0 100Z" dur="3s" repeatCount="indefinite"/></path>
        <path d="M20 70 L30 78 L70 78 L80 70Z" fill="#3A3732"/>
        <rect x="32" y="66" width="36" height="4" rx="1" fill="#3A3732" opacity="0.8"/>
        <ellipse cx="50" cy="55" rx="12" ry="9" fill="#E8713A" opacity="0.85"/>
        <circle cx="50" cy="44" r="9" fill="#E8713A"/>
        <path d="M44 38 L41 28 L47 36" fill="#E8713A"/><path d="M56 38 L59 28 L53 36" fill="#E8713A"/>
        <rect x="43" y="42" width="6" height="3.5" rx="1.5" fill="#0C0B0F" opacity="0.85"/>
        <rect x="51" y="42" width="6" height="3.5" rx="1.5" fill="#0C0B0F" opacity="0.85"/>
        <line x1="49" y1="43.5" x2="51" y2="43.5" stroke="#0C0B0F" stroke-width="0.5"/>
        <path d="M49 47.5 L50 48.5 L51 47.5" fill="#C4593A"/>
        <line x1="72" y1="50" x2="72" y2="62" stroke="#E8E4DF" stroke-width="0.5" opacity="0.35"/>
        <path d="M67 50 L72 42 L77 50Z" fill="none" stroke="#E8E4DF" stroke-width="0.5" opacity="0.35"/>
      </svg>
      <span class="gallery-label">ceo cat</span>
    </div>
    <!-- 4: SIAMESE cat with headphones -->
    <div class="gallery-cell">
      <svg viewBox="0 0 100 100" fill="none">
        <ellipse cx="50" cy="60" rx="18" ry="15" fill="#F0E6D6" opacity="0.7"/>
        <circle cx="50" cy="38" r="14" fill="#F0E6D6" opacity="0.7"/>
        <!-- siamese dark points -->
        <ellipse cx="50" cy="42" rx="8" ry="6" fill="#5C4033" opacity="0.15"/>
        <path d="M40 28 L37 14 L45 26" fill="#5C4033" opacity="0.4"/>
        <path d="M60 28 L63 14 L55 26" fill="#5C4033" opacity="0.4"/>
        <ellipse cx="45" cy="37" rx="3" ry="3.5" fill="#4A90D9"/>
        <ellipse cx="55" cy="37" rx="3" ry="3.5" fill="#4A90D9"/>
        <circle cx="45" cy="37" r="1.5" fill="#0C0B0F"/><circle cx="55" cy="37" r="1.5" fill="#0C0B0F"/>
        <path d="M49 42 L50 43.5 L51 42" fill="#5C4033"/>
        <path d="M34 34 Q34 18 50 18 Q66 18 66 34" stroke="#3A3732" stroke-width="2.5" fill="none"/>
        <rect x="30" y="30" width="6" height="10" rx="3" fill="#3A3732"/><rect x="64" y="30" width="6" height="10" rx="3" fill="#3A3732"/>
        <path d="M70 40 L78 48" stroke="#3A3732" stroke-width="1.5" stroke-linecap="round"/><circle cx="80" cy="50" r="3" fill="#3A3732" opacity="0.6"/>
        <path d="M68 58 Q80 45 76 32" stroke="#5C4033" stroke-width="3" fill="none" stroke-linecap="round" opacity="0.4"/>
      </svg>
      <span class="gallery-label">content cat</span>
    </div>
    <!-- 5: GRAY cat napping on server rack -->
    <div class="gallery-cell">
      <svg viewBox="0 0 100 100" fill="none">
        <!-- server rack -->
        <rect x="15" y="50" width="70" height="40" rx="3" fill="#222" stroke="#3A3732" stroke-width="0.8"/>
        <rect x="20" y="55" width="60" height="8" rx="1" fill="#1A1A1A"/><circle cx="72" cy="59" r="2" fill="#8BAA7A" opacity="0.6"><animate attributeName="opacity" values="0.6;0.2;0.6" dur="2s" repeatCount="indefinite"/></circle>
        <rect x="20" y="66" width="60" height="8" rx="1" fill="#1A1A1A"/><circle cx="72" cy="70" r="2" fill="#E8713A" opacity="0.4"><animate attributeName="opacity" values="0.4;0.1;0.4" dur="3s" repeatCount="indefinite"/></circle>
        <rect x="20" y="77" width="60" height="8" rx="1" fill="#1A1A1A"/><circle cx="72" cy="81" r="2" fill="#4A90D9" opacity="0.3"/>
        <!-- sleeping gray cat on top -->
        <ellipse cx="52" cy="42" rx="22" ry="10" fill="#888" opacity="0.75"/>
        <circle cx="36" cy="38" r="9" fill="#999" opacity="0.75"/>
        <path d="M29 33 L27 22 L33 31" fill="#999" opacity="0.75"/><path d="M43 33 L45 22 L39 31" fill="#888" opacity="0.75"/>
        <!-- closed eyes (sleeping) -->
        <path d="M32 37 Q34 39 36 37" stroke="#555" stroke-width="1" fill="none"/>
        <path d="M38 37 Q40 39 42 37" stroke="#555" stroke-width="1" fill="none"/>
        <!-- zzz -->
        <text x="55" y="28" font-family="var(--mono)" font-size="7" fill="#7A756D" opacity="0.4">z</text>
        <text x="62" y="22" font-family="var(--mono)" font-size="9" fill="#7A756D" opacity="0.3">z</text>
        <text x="70" y="15" font-family="var(--mono)" font-size="11" fill="#7A756D" opacity="0.2">z</text>
        <!-- tail draping -->
        <path d="M74 42 Q82 38 78 50" stroke="#888" stroke-width="4" fill="none" stroke-linecap="round" opacity="0.6"/>
      </svg>
      <span class="gallery-label">ops cat</span>
    </div>
  </div>
</section>

<section class="cta">
  <div class="r">
    <h2>ready to <em>cross?</em></h2>
    <p>Whether you need one brand or all three, we'll assemble the right stack for your US entry.</p>
    <a href="#" class="cta-btn">get in touch</a>
  </div>
</section>

<footer class="foot">
  <span class="foot-left">© 2026 guri-guri holdings llc · doral, fl</span>
  <div class="foot-right"><a href="#">michi media</a><a href="#">cruce consulting</a><a href="#">nodo studio</a></div>
</footer>

<script>
// ===== LASER DOT (cursor) =====
const laser = document.getElementById('laserDot');
let mx = -100, my = -100;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
function updateLaser() {
  laser.style.left = (mx - 4) + 'px';
  laser.style.top = (my - 4) + 'px';
  requestAnimationFrame(updateLaser);
}
updateLaser();

// ===== AUTONOMOUS WALKING CATS =====
const catWorld = document.getElementById('catWorld');

const CAT_BREEDS = [
  { name: 'orange',   body: '#E8713A', head: '#F0884A', ears: '#E8713A', inner: '#F5C882', belly: '#F5C882', eyes: '#0C0B0F', nose: '#C4593A', pupil: null },
  { name: 'tuxedo',   body: '#1A1A1A', head: '#222',    ears: '#1A1A1A', inner: '#444',    belly: '#E8E4DF', eyes: '#8BAA7A', nose: '#D4727A', pupil: '#0C0B0F' },
  { name: 'calico',   body: '#F0E6D6', head: '#F0E6D6', ears: '#E8713A', inner: '#F5C882', belly: '#F0E6D6', eyes: '#0C0B0F', nose: '#D4727A', pupil: null, patches: ['#E8713A', '#333'] },
  { name: 'gray',     body: '#888',    head: '#999',    ears: '#888',    inner: '#AAA',    belly: '#AAA',    eyes: '#F5C882', nose: '#D4727A', pupil: '#0C0B0F' },
  { name: 'siamese',  body: '#F0E6D6', head: '#F0E6D6', ears: '#5C4033', inner: '#5C4033', belly: '#F0E6D6', eyes: '#4A90D9', nose: '#5C4033', pupil: '#0C0B0F' },
  { name: 'ginger',   body: '#D4883A', head: '#E09848', ears: '#D4883A', inner: '#F5C882', belly: '#F5C882', eyes: '#0C0B0F', nose: '#AA6030', pupil: null },
  { name: 'void',     body: '#111',    head: '#181818', ears: '#111',    inner: '#333',    belly: '#222',    eyes: '#F5C882', nose: '#555',    pupil: '#0C0B0F' },
  { name: 'cream',    body: '#F5E8D0', head: '#F8EDD8', ears: '#F0DFC0', inner: '#FFF5E8', belly: '#FFF5E8', eyes: '#8BAA7A', nose: '#D4A080', pupil: '#0C0B0F' },
];

function buildCatSVG(breed, frame) {
  const b = breed;
  const legOffset = frame % 2 === 0 ? 1 : -1;
  const tailWag = Math.sin(frame * 0.3) * 8;
  const earTwitch = frame % 20 === 0 ? -3 : 0;
  const isBlinking = frame % 40 >= 38;

  let patches = '';
  if (b.patches) {
    patches = `<ellipse cx="14" cy="14" rx="5" ry="4" fill="${b.patches[0]}" opacity="0.35"/>
    <ellipse cx="26" cy="16" rx="4" ry="3.5" fill="${b.patches[1]}" opacity="0.25"/>`;
  }

  const eyeFill = b.pupil ? b.eyes : b.eyes;
  const eyeInner = b.pupil || 'none';

  return `<svg width="44" height="32" viewBox="0 0 44 32" fill="none" xmlns="http://www.w3.org/2000/svg">
    <!-- body -->
    <ellipse cx="20" cy="18" rx="12" ry="8" fill="${b.body}"/>
    ${patches}
    <!-- belly -->
    <ellipse cx="20" cy="20" rx="7" ry="4" fill="${b.belly}" opacity="0.15"/>
    <!-- legs (animated) -->
    <ellipse cx="11" cy="26" rx="3.5" ry="${2 + legOffset * 0.4}" fill="${b.body}"/>
    <ellipse cx="18" cy="26" rx="3.5" ry="${2 - legOffset * 0.4}" fill="${b.body}"/>
    <ellipse cx="22" cy="26" rx="3.5" ry="${2 - legOffset * 0.4}" fill="${b.body}"/>
    <ellipse cx="29" cy="26" rx="3.5" ry="${2 + legOffset * 0.4}" fill="${b.body}"/>
    <!-- head -->
    <circle cx="20" cy="10" r="8" fill="${b.head}"/>
    <!-- ears -->
    <path d="M13 6 L${11 + earTwitch} -2 L17 4" fill="${b.ears}"/>
    <path d="M14 5 L${12 + earTwitch} 0 L16.5 4" fill="${b.inner}" opacity="0.3"/>
    <path d="M27 6 L29 -2 L23 4" fill="${b.ears}"/>
    <path d="M26 5 L28 0 L23.5 4" fill="${b.inner}" opacity="0.3"/>
    <!-- eyes -->
    ${isBlinking
      ? `<line x1="16" y1="9" x2="19" y2="9" stroke="${eyeFill}" stroke-width="1" stroke-linecap="round"/>
         <line x1="21" y1="9" x2="24" y2="9" stroke="${eyeFill}" stroke-width="1" stroke-linecap="round"/>`
      : `<ellipse cx="17" cy="9" rx="2" ry="2.5" fill="${eyeFill}"/>
         ${eyeInner !== 'none' ? `<circle cx="17" cy="9" r="1" fill="${eyeInner}"/>` : ''}
         <circle cx="17.8" cy="8.2" r="0.6" fill="white" opacity="0.5"/>
         <ellipse cx="23" cy="9" rx="2" ry="2.5" fill="${eyeFill}"/>
         ${eyeInner !== 'none' ? `<circle cx="23" cy="9" r="1" fill="${eyeInner}"/>` : ''}
         <circle cx="23.8" cy="8.2" r="0.6" fill="white" opacity="0.5"/>`
    }
    <!-- nose -->
    <path d="M19 12 L20 13.2 L21 12Z" fill="${b.nose}"/>
    <!-- whiskers -->
    <line x1="8" y1="11" x2="14" y2="11.5" stroke="${b.belly}" stroke-width="0.3" opacity="0.3"/>
    <line x1="8" y1="13" x2="14" y2="12.5" stroke="${b.belly}" stroke-width="0.3" opacity="0.3"/>
    <line x1="32" y1="11" x2="26" y2="11.5" stroke="${b.belly}" stroke-width="0.3" opacity="0.3"/>
    <line x1="32" y1="13" x2="26" y2="12.5" stroke="${b.belly}" stroke-width="0.3" opacity="0.3"/>
    <!-- tail -->
    <path d="M32 16 Q${38 + tailWag} ${8 + Math.abs(tailWag)*0.3} ${36 + tailWag * 0.5} 4" stroke="${b.body}" stroke-width="3" fill="none" stroke-linecap="round"/>
  </svg>`;
}

function buildSittingCatSVG(breed, frame) {
  const b = breed;
  const tailWag = Math.sin(frame * 0.15) * 6;
  const isBlinking = frame % 50 >= 48;
  const earTwitch = frame % 30 === 0 ? -2 : 0;

  const eyeFill = b.eyes;
  const eyeInner = b.pupil || 'none';

  return `<svg width="36" height="38" viewBox="0 0 36 38" fill="none">
    <ellipse cx="18" cy="26" rx="11" ry="9" fill="${b.body}"/>
    <ellipse cx="18" cy="29" rx="7" ry="5" fill="${b.belly}" opacity="0.12"/>
    <circle cx="18" cy="12" r="9" fill="${b.head}"/>
    <path d="M11 6 L${9 + earTwitch} -2 L15 4" fill="${b.ears}"/>
    <path d="M12 5 L${10 + earTwitch} 0 L14.5 4" fill="${b.inner}" opacity="0.3"/>
    <path d="M25 6 L27 -2 L21 4" fill="${b.ears}"/>
    <path d="M24 5 L26 0 L21.5 4" fill="${b.inner}" opacity="0.3"/>
    ${isBlinking
      ? `<line x1="14" y1="11" x2="17" y2="11" stroke="${eyeFill}" stroke-width="1" stroke-linecap="round"/>
         <line x1="19" y1="11" x2="22" y2="11" stroke="${eyeFill}" stroke-width="1" stroke-linecap="round"/>`
      : `<ellipse cx="15" cy="11" rx="2" ry="2.5" fill="${eyeFill}"/>
         ${eyeInner !== 'none' ? `<circle cx="15" cy="11" r="1" fill="${eyeInner}"/>` : ''}
         <circle cx="15.7" cy="10.3" r="0.5" fill="white" opacity="0.5"/>
         <ellipse cx="21" cy="11" rx="2" ry="2.5" fill="${eyeFill}"/>
         ${eyeInner !== 'none' ? `<circle cx="21" cy="11" r="1" fill="${eyeInner}"/>` : ''}
         <circle cx="21.7" cy="10.3" r="0.5" fill="white" opacity="0.5"/>`
    }
    <path d="M17 14 L18 15.2 L19 14Z" fill="${b.nose}"/>
    <ellipse cx="11" cy="33" rx="4" ry="2.5" fill="${b.body}"/>
    <ellipse cx="25" cy="33" rx="4" ry="2.5" fill="${b.body}"/>
    <path d="M29 24 Q${34 + tailWag} ${16} ${32 + tailWag * 0.5} 8" stroke="${b.body}" stroke-width="3" fill="none" stroke-linecap="round"/>
  </svg>`;
}

// Cat behavior states
const STATES = { WALK: 0, SIT: 1, GROOM: 2, NAP: 3, CHASE_LASER: 4 };

class WanderCat {
  constructor(breed, startX) {
    this.breed = breed;
    this.x = startX;
    this.dir = Math.random() > 0.5 ? 1 : -1;
    this.speed = 0.5 + Math.random() * 0.8;
    this.state = STATES.WALK;
    this.stateTimer = 200 + Math.random() * 400;
    this.frame = Math.floor(Math.random() * 100);
    this.el = document.createElement('div');
    this.el.className = 'wanderCat';
    this.el.style.opacity = '0.35';
    this.el.style.bottom = '2px';
    catWorld.appendChild(this.el);
    this.laserInterest = 0;
  }

  update() {
    this.frame++;
    this.stateTimer--;

    // chance to notice laser
    const distToLaser = Math.abs(this.x - mx);
    if (distToLaser < 250 && Math.random() < 0.005 && this.state !== STATES.CHASE_LASER) {
      this.state = STATES.CHASE_LASER;
      this.stateTimer = 120 + Math.random() * 200;
    }

    if (this.stateTimer <= 0) {
      const r = Math.random();
      if (r < 0.45) { this.state = STATES.WALK; this.stateTimer = 200 + Math.random() * 500; this.dir = Math.random() > 0.5 ? 1 : -1; }
      else if (r < 0.7) { this.state = STATES.SIT; this.stateTimer = 150 + Math.random() * 300; }
      else if (r < 0.85) { this.state = STATES.GROOM; this.stateTimer = 100 + Math.random() * 150; }
      else { this.state = STATES.NAP; this.stateTimer = 300 + Math.random() * 400; }
    }

    if (this.state === STATES.WALK) {
      this.x += this.speed * this.dir;
      if (this.x > window.innerWidth + 50) this.dir = -1;
      if (this.x < -50) this.dir = 1;
      this.el.innerHTML = buildCatSVG(this.breed, this.frame);
      this.el.style.transform = `translateX(${this.x}px) scaleX(${this.dir > 0 ? 1 : -1})`;
    } else if (this.state === STATES.CHASE_LASER) {
      const dx = mx - this.x;
      this.dir = dx > 0 ? 1 : -1;
      this.x += Math.sign(dx) * Math.min(Math.abs(dx) * 0.04, 2.5);
      this.el.innerHTML = buildCatSVG(this.breed, this.frame);
      this.el.style.transform = `translateX(${this.x}px) scaleX(${this.dir > 0 ? 1 : -1})`;
    } else {
      // sitting/grooming/napping
      this.el.innerHTML = buildSittingCatSVG(this.breed, this.frame);
      this.el.style.transform = `translateX(${this.x}px) scaleX(${this.dir > 0 ? 1 : -1})`;
    }
  }
}

// Spawn cats
const cats = [];
const numCats = 7;
for (let i = 0; i < numCats; i++) {
  const breed = CAT_BREEDS[i % CAT_BREEDS.length];
  const startX = (window.innerWidth / (numCats + 1)) * (i + 1) + (Math.random() - 0.5) * 100;
  cats.push(new WanderCat(breed, startX));
}

function updateCats() {
  cats.forEach(c => c.update());
  requestAnimationFrame(updateCats);
}
updateCats();

// ===== FLOATING PAWS CANVAS =====
const pawCanvas = document.createElement('canvas');
pawCanvas.style.cssText = 'position:fixed;inset:0;pointer-events:none;z-index:1;opacity:0.035;';
document.body.appendChild(pawCanvas);
const ctx = pawCanvas.getContext('2d');
let paws = [];

function resizeCanvas() { pawCanvas.width = window.innerWidth; pawCanvas.height = window.innerHeight; }
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

for (let i = 0; i < 15; i++) {
  paws.push({
    x: Math.random() * window.innerWidth, y: Math.random() * window.innerHeight,
    size: 6 + Math.random() * 10, speedX: (Math.random() - 0.5) * 0.25, speedY: -0.15 - Math.random() * 0.25,
    opacity: 0.3 + Math.random() * 0.7, rotation: Math.random() * Math.PI * 2, rotSpeed: (Math.random() - 0.5) * 0.004,
  });
}

function drawPaw(x, y, size, rotation, opacity) {
  ctx.save(); ctx.translate(x, y); ctx.rotate(rotation); ctx.globalAlpha = opacity;
  ctx.fillStyle = '#E8713A';
  ctx.beginPath(); ctx.ellipse(0, 2, size * 0.4, size * 0.5, 0, 0, Math.PI * 2); ctx.fill();
  const r = size * 0.17;
  ctx.beginPath(); ctx.arc(-size * 0.28, -size * 0.35, r, 0, Math.PI * 2); ctx.fill();
  ctx.beginPath(); ctx.arc(0, -size * 0.45, r, 0, Math.PI * 2); ctx.fill();
  ctx.beginPath(); ctx.arc(size * 0.28, -size * 0.35, r, 0, Math.PI * 2); ctx.fill();
  ctx.restore();
}

function animatePaws() {
  ctx.clearRect(0, 0, pawCanvas.width, pawCanvas.height);
  paws.forEach(p => {
    p.x += p.speedX; p.y += p.speedY; p.rotation += p.rotSpeed;
    if (p.y < -30) { p.y = pawCanvas.height + 30; p.x = Math.random() * pawCanvas.width; }
    if (p.x < -30) p.x = pawCanvas.width + 30;
    if (p.x > pawCanvas.width + 30) p.x = -30;
    drawPaw(p.x, p.y, p.size, p.rotation, p.opacity);
  });
  requestAnimationFrame(animatePaws);
}
animatePaws();

// ===== SCROLL REVEAL =====
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('v'); });
}, { threshold: 0.08, rootMargin: '0px 0px -40px 0px' });
document.querySelectorAll('.r').forEach(el => obs.observe(el));

const vigObs = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('vis'); });
}, { threshold: 0.1 });
document.querySelectorAll('.vig:not(.vis)').forEach(el => vigObs.observe(el));

// ===== TERMINAL =====
const lines = [
  ['p','~ ','michi-agent deploy --client acme-co'],['d','  scanning 47 brand assets...'],
  ['g','  ✓ 3 video scripts generated (es → en)'],['g','  ✓ 4 social cuts exported'],['',''],
  ['p','~ ','cruce-agent status --visa E2'],['d','  docs: 14/16 complete'],
  ['w','  ⧖ next: financial projections (3d)'],['g','  ✓ auto-drafted, queued for review'],['',''],
  ['p','~ ','nodo-agent audit acme-co.com'],['d','  pagespeed: 34 → 91'],
  ['g','  ✓ 12 fixes deployed · sitemap rebuilt'],
];

let termReady = false;
const termObs = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting && !termReady) { termReady = true; typeTerm(); } });
}, { threshold: 0.3 });
termObs.observe(document.getElementById('term'));

function typeTerm() {
  const el = document.getElementById('term'); el.innerHTML = '';
  lines.forEach((l, i) => {
    setTimeout(() => {
      const div = document.createElement('div');
      if (l[0]==='p') div.innerHTML=`<span class="p">${l[1]}</span>${l[2]}`;
      else if (l[0]==='') div.innerHTML='&nbsp;';
      else div.innerHTML=`<span class="${l[0]}">${l[1]}</span>`;
      div.style.opacity='0'; div.style.transform='translateY(4px)'; div.style.transition='all 0.3s';
      el.appendChild(div);
      requestAnimationFrame(()=>{ div.style.opacity='1'; div.style.transform='translateY(0)'; });
    }, i * 300);
  });
}
</script>
</body>
</html>
