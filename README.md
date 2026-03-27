<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ahad Naveed — Senior Flutter Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --bg2: #080d1a;
    --accent: #00e5ff;
    --accent2: #7b2fff;
    --accent3: #ff3d6e;
    --text: #e8eaf6;
    --muted: #5c6bc0;
    --card: rgba(255,255,255,0.04);
    --card-border: rgba(0,229,255,0.12);
    --glow: 0 0 40px rgba(0,229,255,0.15);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; overflow-x: hidden; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  #cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    top: 0; left: 0;
    pointer-events: none;
    z-index: 9999;
    mix-blend-mode: difference;
    transition: transform 0.1s ease;
  }
  #cursor-trail {
    width: 36px; height: 36px;
    border: 1px solid rgba(0,229,255,0.4);
    border-radius: 50%;
    position: fixed;
    top: 0; left: 0;
    pointer-events: none;
    z-index: 9998;
    transition: all 0.18s ease;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.5;
  }

  /* ─── NAVBAR ─── */
  nav {
    position: fixed;
    top: 0; width: 100%;
    z-index: 500;
    padding: 20px 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    backdrop-filter: blur(20px);
    background: rgba(5,8,16,0.6);
    border-bottom: 1px solid rgba(0,229,255,0.06);
    transition: all 0.3s;
  }
  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 3px;
    color: var(--accent);
    text-decoration: none;
  }
  .nav-logo span { color: var(--text); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    color: var(--muted);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--accent);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { width: 100%; }
  .nav-hire {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 10px 24px;
    border: 1px solid var(--accent);
    color: var(--accent);
    background: transparent;
    cursor: none;
    transition: all 0.3s;
    text-decoration: none;
  }
  .nav-hire:hover {
    background: var(--accent);
    color: var(--bg);
    box-shadow: 0 0 30px rgba(0,229,255,0.4);
  }

  /* ─── HERO ─── */
  #hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    position: relative;
    overflow: hidden;
    padding: 100px 60px 60px;
  }

  /* 3D grid floor */
  #hero-canvas {
    position: absolute;
    inset: 0;
    z-index: 0;
  }

  .hero-content {
    position: relative;
    z-index: 2;
    max-width: 900px;
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.3s forwards;
  }

  .hero-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(72px, 12vw, 160px);
    line-height: 0.9;
    letter-spacing: -2px;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.8s 0.5s forwards;
  }
  .hero-name .line2 {
    -webkit-text-stroke: 1px rgba(0,229,255,0.6);
    color: transparent;
    display: block;
  }

  .hero-role {
    font-family: 'Space Mono', monospace;
    font-size: 14px;
    letter-spacing: 3px;
    color: var(--muted);
    margin-bottom: 40px;
    opacity: 0;
    animation: fadeUp 0.8s 0.7s forwards;
  }
  .hero-role span { color: var(--accent2); }

  .hero-desc {
    font-size: 18px;
    font-weight: 300;
    line-height: 1.7;
    color: rgba(232,234,246,0.7);
    max-width: 560px;
    margin-bottom: 56px;
    opacity: 0;
    animation: fadeUp 0.8s 0.9s forwards;
  }

  .hero-btns {
    display: flex; gap: 20px; flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s 1.1s forwards;
  }
  .btn-primary {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 16px 36px;
    background: var(--accent);
    color: var(--bg);
    text-decoration: none;
    font-weight: 700;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .btn-primary::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent2);
    transform: translateX(-100%);
    transition: transform 0.3s;
  }
  .btn-primary:hover::before { transform: translateX(0); }
  .btn-primary span { position: relative; z-index: 1; }
  .btn-secondary {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 16px 36px;
    border: 1px solid rgba(0,229,255,0.3);
    color: var(--text);
    text-decoration: none;
    transition: all 0.3s;
  }
  .btn-secondary:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: var(--glow);
  }

  .hero-stats {
    position: absolute;
    right: 60px;
    bottom: 80px;
    display: flex;
    flex-direction: column;
    gap: 32px;
    z-index: 2;
    opacity: 0;
    animation: fadeIn 1s 1.5s forwards;
  }
  .stat-item { text-align: right; }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px;
    color: var(--accent);
    line-height: 1;
    display: block;
  }
  .stat-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--muted);
    text-transform: uppercase;
  }

  .scroll-hint {
    position: absolute;
    bottom: 40px;
    left: 60px;
    display: flex;
    align-items: center;
    gap: 12px;
    opacity: 0;
    animation: fadeIn 1s 2s forwards;
    z-index: 2;
  }
  .scroll-hint-line {
    width: 40px;
    height: 1px;
    background: var(--muted);
    position: relative;
    overflow: hidden;
  }
  .scroll-hint-line::after {
    content: '';
    position: absolute;
    height: 100%;
    width: 100%;
    background: var(--accent);
    animation: slideLine 2s infinite;
  }
  @keyframes slideLine {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(100%); }
  }
  .scroll-hint span {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--muted);
    text-transform: uppercase;
  }

  /* ─── SECTION COMMON ─── */
  section {
    padding: 120px 60px;
    position: relative;
  }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 16px;
  }
  .section-label::before {
    content: '';
    display: block;
    width: 32px;
    height: 1px;
    background: var(--accent);
  }

  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(48px, 7vw, 96px);
    letter-spacing: -1px;
    line-height: 0.95;
    margin-bottom: 60px;
  }

  /* ─── ABOUT ─── */
  #about { background: var(--bg2); }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }
  .about-text p {
    font-size: 17px;
    line-height: 1.8;
    color: rgba(232,234,246,0.75);
    margin-bottom: 24px;
  }
  .about-highlight {
    color: var(--accent) !important;
    font-weight: 500;
  }
  .about-card-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .about-card {
    background: var(--card);
    border: 1px solid var(--card-border);
    padding: 28px;
    transition: all 0.4s;
    position: relative;
    overflow: hidden;
  }
  .about-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }
  .about-card:hover { transform: translateY(-4px); box-shadow: var(--glow); border-color: rgba(0,229,255,0.3); }
  .about-card:hover::before { transform: scaleX(1); }
  .about-card-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 8px;
  }
  .about-card-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--muted);
    text-transform: uppercase;
  }

  /* ─── SKILLS ─── */
  #skills { background: var(--bg); }
  .skills-container { display: flex; flex-direction: column; gap: 48px; }
  .skill-category-title {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    color: var(--accent2);
    text-transform: uppercase;
    margin-bottom: 20px;
  }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 12px; }
  .skill-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    padding: 10px 20px;
    border: 1px solid rgba(0,229,255,0.15);
    color: rgba(232,234,246,0.7);
    transition: all 0.3s;
    cursor: default;
    position: relative;
    overflow: hidden;
  }
  .skill-tag::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,229,255,0.08), rgba(123,47,255,0.08));
    transform: translateY(100%);
    transition: transform 0.3s;
  }
  .skill-tag:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 0 20px rgba(0,229,255,0.12);
  }
  .skill-tag:hover::before { transform: translateY(0); }
  .skill-tag span { position: relative; }

  .skills-visual {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
    margin-top: 60px;
  }
  .skill-bar-item {
    background: var(--card);
    border: 1px solid var(--card-border);
    padding: 24px;
    transition: all 0.3s;
  }
  .skill-bar-item:hover { border-color: rgba(0,229,255,0.3); }
  .skill-bar-name {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    color: var(--text);
    margin-bottom: 12px;
    display: flex;
    justify-content: space-between;
  }
  .skill-bar-name span { color: var(--accent); }
  .skill-bar-track {
    height: 3px;
    background: rgba(255,255,255,0.06);
    position: relative;
    overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    width: 0;
    transition: width 1.2s cubic-bezier(0.16, 1, 0.3, 1);
  }

  /* ─── SERVICES ─── */
  #services { background: var(--bg2); }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    background: rgba(0,229,255,0.06);
  }
  .service-card {
    background: var(--bg2);
    padding: 48px 36px;
    position: relative;
    overflow: hidden;
    transition: all 0.4s;
    cursor: default;
  }
  .service-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,229,255,0.06), rgba(123,47,255,0.06));
    opacity: 0;
    transition: opacity 0.4s;
  }
  .service-card:hover::after { opacity: 1; }
  .service-card:hover { transform: translateY(-2px); }
  .service-icon {
    font-size: 36px;
    margin-bottom: 24px;
    display: block;
    transition: transform 0.3s;
  }
  .service-card:hover .service-icon { transform: scale(1.15) rotate(-5deg); }
  .service-num {
    position: absolute;
    top: 24px; right: 28px;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 72px;
    color: rgba(0,229,255,0.04);
    line-height: 1;
    transition: color 0.4s;
  }
  .service-card:hover .service-num { color: rgba(0,229,255,0.08); }
  .service-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 28px;
    letter-spacing: 1px;
    margin-bottom: 16px;
    transition: color 0.3s;
  }
  .service-card:hover .service-title { color: var(--accent); }
  .service-desc {
    font-size: 14px;
    line-height: 1.7;
    color: rgba(232,234,246,0.55);
  }

  /* ─── PROJECTS ─── */
  #projects { background: var(--bg); }
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--card-border);
    padding: 40px;
    position: relative;
    overflow: hidden;
    transition: all 0.4s;
    group: true;
  }
  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,229,255,0.04), transparent);
    transition: left 0.6s;
  }
  .project-card:hover::before { left: 100%; }
  .project-card:hover {
    border-color: rgba(0,229,255,0.3);
    transform: translateY(-6px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.4), var(--glow);
  }
  .project-tag {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 16px;
    display: block;
  }
  .project-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 32px;
    letter-spacing: 1px;
    margin-bottom: 16px;
  }
  .project-desc {
    font-size: 14px;
    line-height: 1.7;
    color: rgba(232,234,246,0.6);
    margin-bottom: 28px;
  }
  .project-tech { display: flex; flex-wrap: wrap; gap: 8px; }
  .tech-pill {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 1px;
    padding: 6px 14px;
    background: rgba(123,47,255,0.15);
    border: 1px solid rgba(123,47,255,0.3);
    color: rgba(232,234,246,0.7);
  }
  .project-arrow {
    position: absolute;
    top: 40px; right: 40px;
    font-size: 24px;
    color: rgba(0,229,255,0.3);
    transition: all 0.3s;
  }
  .project-card:hover .project-arrow {
    color: var(--accent);
    transform: translate(4px, -4px);
  }

  /* ─── EXPERIENCE ─── */
  #experience { background: var(--bg2); }
  .timeline {
    position: relative;
    padding-left: 60px;
  }
  .timeline::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(180deg, var(--accent), var(--accent2), transparent);
  }
  .timeline-item {
    position: relative;
    margin-bottom: 64px;
    opacity: 0;
    transform: translateX(-20px);
    transition: all 0.6s;
  }
  .timeline-item.visible { opacity: 1; transform: translateX(0); }
  .timeline-dot {
    position: absolute;
    left: -68px;
    top: 8px;
    width: 16px; height: 16px;
    background: var(--bg2);
    border: 2px solid var(--accent);
    border-radius: 50%;
    transition: all 0.3s;
  }
  .timeline-item:hover .timeline-dot {
    background: var(--accent);
    box-shadow: 0 0 20px rgba(0,229,255,0.5);
  }
  .timeline-date {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 12px;
  }
  .timeline-company {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 36px;
    letter-spacing: 1px;
    margin-bottom: 4px;
  }
  .timeline-role {
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    letter-spacing: 1px;
    color: var(--muted);
    margin-bottom: 20px;
  }
  .timeline-points { list-style: none; }
  .timeline-points li {
    font-size: 14px;
    line-height: 1.7;
    color: rgba(232,234,246,0.65);
    padding: 8px 0;
    padding-left: 20px;
    position: relative;
    border-bottom: 1px solid rgba(255,255,255,0.04);
  }
  .timeline-points li::before {
    content: '▸';
    position: absolute;
    left: 0;
    color: var(--accent);
    font-size: 12px;
  }

  /* ─── HIRE ME ─── */
  #hirme {
    background: var(--bg);
    text-align: center;
    padding: 160px 60px;
    position: relative;
    overflow: hidden;
  }
  #hirme::before {
    content: 'HIRE ME';
    position: absolute;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 40vw;
    color: rgba(0,229,255,0.02);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    white-space: nowrap;
    pointer-events: none;
    user-select: none;
  }
  #hirme .section-label { justify-content: center; }
  #hirme .section-title { text-align: center; }
  .hire-subtitle {
    font-size: 18px;
    color: rgba(232,234,246,0.6);
    max-width: 560px;
    margin: 0 auto 60px;
    line-height: 1.7;
  }
  .hire-btns {
    display: flex;
    gap: 20px;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 80px;
  }
  .hire-btn {
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 18px 48px;
    text-decoration: none;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .hire-btn-whatsapp {
    background: #25D366;
    color: #fff;
    font-weight: 700;
  }
  .hire-btn-whatsapp:hover {
    background: #128C7E;
    transform: translateY(-3px);
    box-shadow: 0 20px 40px rgba(37,211,102,0.3);
  }
  .hire-btn-linkedin {
    border: 1px solid rgba(0,229,255,0.3);
    color: var(--text);
  }
  .hire-btn-linkedin:hover {
    border-color: var(--accent);
    color: var(--accent);
    transform: translateY(-3px);
    box-shadow: var(--glow);
  }
  .hire-btn-email {
    background: var(--accent2);
    color: #fff;
  }
  .hire-btn-email:hover {
    background: #5b1fff;
    transform: translateY(-3px);
    box-shadow: 0 20px 40px rgba(123,47,255,0.3);
  }
  .contact-info {
    display: flex;
    gap: 48px;
    justify-content: center;
    flex-wrap: wrap;
  }
  .contact-item {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    color: var(--muted);
  }
  .contact-item a {
    color: var(--muted);
    text-decoration: none;
    transition: color 0.3s;
  }
  .contact-item a:hover { color: var(--accent); }

  /* ─── FOOTER ─── */
  footer {
    background: var(--bg2);
    padding: 40px 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top: 1px solid rgba(0,229,255,0.06);
  }
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 24px;
    letter-spacing: 3px;
    color: var(--accent);
  }
  .footer-copy {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 1px;
    color: var(--muted);
  }

  /* ─── SCROLL REVEAL ─── */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ─── FLOATING PARTICLES ─── */
  .particle {
    position: fixed;
    width: 2px; height: 2px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    opacity: 0;
    z-index: 1;
  }

  /* ─── KEYFRAMES ─── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-12px); }
  }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 1024px) {
    nav { padding: 16px 32px; }
    .nav-links { display: none; }
    section { padding: 80px 32px; }
    .hero-content { padding: 0; }
    .hero-stats { right: 32px; bottom: 60px; }
    #hero { padding: 100px 32px 60px; }
    .about-grid, .skills-visual, .services-grid { grid-template-columns: 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 16px; text-align: center; }
  }

  /* Glitch effect on hero name hover */
  .hero-name:hover {
    animation: glitch 0.3s;
  }
  @keyframes glitch {
    0% { text-shadow: none; }
    20% { text-shadow: 3px 0 var(--accent3), -3px 0 var(--accent); }
    40% { text-shadow: -3px 0 var(--accent3), 3px 0 var(--accent2); }
    60% { text-shadow: 2px 0 var(--accent), -2px 0 var(--accent3); }
    80% { text-shadow: -2px 0 var(--accent2), 2px 0 var(--accent); }
    100% { text-shadow: none; }
  }

  /* Active nav */
  .nav-links a.active { color: var(--accent); }
  .nav-links a.active::after { width: 100%; }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div id="cursor"></div>
<div id="cursor-trail"></div>

<!-- NAVBAR -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">AN<span>.</span></a>
  <ul class="nav-links">
    <li><a href="#about" class="nav-link">About</a></li>
    <li><a href="#skills" class="nav-link">Skills</a></li>
    <li><a href="#services" class="nav-link">Services</a></li>
    <li><a href="#projects" class="nav-link">Projects</a></li>
    <li><a href="#experience" class="nav-link">Experience</a></li>
  </ul>
  <a href="https://wa.me/923049184381" target="_blank" class="nav-hire">Hire Me</a>
</nav>

<!-- HERO -->
<section id="hero">
  <canvas id="hero-canvas"></canvas>
  <div class="hero-content">
    <p class="hero-tag">// Senior Flutter Developer</p>
    <h1 class="hero-name">
      AHAD<br>
      <span class="line2">NAVEED</span>
    </h1>
    <p class="hero-role">Flutter · Dart · <span>300+ Apps Delivered</span></p>
    <p class="hero-desc">
      Results-driven developer crafting high-performance mobile experiences. 
      4+ years architecting Flutter frontends across fintech, healthcare, logistics & beyond.
    </p>
    <div class="hero-btns">
      <a href="https://wa.me/923049184381" target="_blank" class="btn-primary"><span>💬 WhatsApp Me</span></a>
      <a href="https://linkedin.com/in/ahadnaveed" target="_blank" class="btn-secondary">LinkedIn →</a>
    </div>
  </div>
  <div class="hero-stats">
    <div class="stat-item">
      <span class="stat-num">300+</span>
      <span class="stat-label">Apps Delivered</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">4+</span>
      <span class="stat-label">Years Experience</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">5+</span>
      <span class="stat-label">Companies</span>
    </div>
  </div>
  <div class="scroll-hint">
    <div class="scroll-hint-line"></div>
    <span>Scroll to explore</span>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-label">01 &nbsp; About Me</div>
  <div class="about-grid">
    <div class="about-text reveal">
      <h2 class="section-title">BUILDING<br>THE FUTURE<br>ON MOBILE</h2>
      <p>I'm a Senior Flutter Developer based in <span class="about-highlight">Sahiwal, Pakistan</span>, with 4+ years of experience delivering scalable mobile solutions across e-commerce, healthcare, fintech, and logistics.</p>
      <p>At <span class="about-highlight">Duseca Software</span>, I architected the frontend for over 300 mobile applications — managing client lifecycles from discovery calls to delivery. A foreign client even traveled to Pakistan to personally recognize my work.</p>
      <p>I bridge the gap between design and engineering — guiding UI/UX teams, conducting requirement sessions, and translating complex business problems into elegant Flutter solutions.</p>
    </div>
    <div class="about-card-grid reveal">
      <div class="about-card">
        <div class="about-card-num">300+</div>
        <div class="about-card-label">Apps Shipped</div>
      </div>
      <div class="about-card">
        <div class="about-card-num">4+</div>
        <div class="about-card-label">Years Flutter</div>
      </div>
      <div class="about-card">
        <div class="about-card-num">5+</div>
        <div class="about-card-label">Platforms</div>
      </div>
      <div class="about-card">
        <div class="about-card-num">⭐</div>
        <div class="about-card-label">Fiverr & Upwork</div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-label">02 &nbsp; Technical Skills</div>
  <h2 class="section-title reveal">MY<br>ARSENAL</h2>
  <div class="skills-container">
    <div class="reveal">
      <p class="skill-category-title">// Frontend — Primary Expertise</p>
      <div class="skill-tags">
        <div class="skill-tag"><span>Flutter</span></div>
        <div class="skill-tag"><span>Dart</span></div>
        <div class="skill-tag"><span>Custom Widgets</span></div>
        <div class="skill-tag"><span>Animations</span></div>
        <div class="skill-tag"><span>Responsive Layouts</span></div>
        <div class="skill-tag"><span>Material Design</span></div>
        <div class="skill-tag"><span>Cupertino</span></div>
        <div class="skill-tag"><span>Provider</span></div>
        <div class="skill-tag"><span>GetX</span></div>
        <div class="skill-tag"><span>Clean Architecture</span></div>
        <div class="skill-tag"><span>MVVM</span></div>
        <div class="skill-tag"><span>MVC</span></div>
        <div class="skill-tag"><span>Android</span></div>
        <div class="skill-tag"><span>iOS</span></div>
        <div class="skill-tag"><span>Flutter Web</span></div>
        <div class="skill-tag"><span>Figma</span></div>
        <div class="skill-tag"><span>Adobe XD</span></div>
      </div>
    </div>
    <div class="reveal">
      <p class="skill-category-title">// Backend — Firebase & APIs</p>
      <div class="skill-tags">
        <div class="skill-tag"><span>Firebase Auth</span></div>
        <div class="skill-tag"><span>Firestore</span></div>
        <div class="skill-tag"><span>Realtime Database</span></div>
        <div class="skill-tag"><span>Cloud Storage</span></div>
        <div class="skill-tag"><span>FCM Push Notifications</span></div>
        <div class="skill-tag"><span>REST APIs</span></div>
        <div class="skill-tag"><span>JSON Parsing</span></div>
        <div class="skill-tag"><span>Payment Gateways</span></div>
        <div class="skill-tag"><span>Hive</span></div>
        <div class="skill-tag"><span>SharedPreferences</span></div>
        <div class="skill-tag"><span>SQLite</span></div>
      </div>
    </div>
  </div>

  <div class="skills-visual">
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">Flutter / Dart <span>98%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="98"></div></div>
    </div>
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">State Management <span>95%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="95"></div></div>
    </div>
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">Firebase BaaS <span>90%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="90"></div></div>
    </div>
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">App Architecture <span>93%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="93"></div></div>
    </div>
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">UI/UX Integration <span>96%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="96"></div></div>
    </div>
    <div class="skill-bar-item reveal">
      <div class="skill-bar-name">Client Communication <span>92%</span></div>
      <div class="skill-bar-track"><div class="skill-bar-fill" data-width="92"></div></div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services">
  <div class="section-label">03 &nbsp; Services</div>
  <h2 class="section-title reveal">WHAT I<br>DELIVER</h2>
  <div class="services-grid reveal">
    <div class="service-card">
      <span class="service-num">01</span>
      <span class="service-icon">📱</span>
      <h3 class="service-title">Flutter App Development</h3>
      <p class="service-desc">End-to-end cross-platform mobile apps for Android & iOS from a single codebase. Pixel-perfect UI, smooth animations, and native performance.</p>
    </div>
    <div class="service-card">
      <span class="service-num">02</span>
      <span class="service-icon">🎨</span>
      <h3 class="service-title">UI/UX Implementation</h3>
      <p class="service-desc">Translating Figma & Adobe XD designs into polished Flutter interfaces. I guide design teams on implementation feasibility and best practices.</p>
    </div>
    <div class="service-card">
      <span class="service-num">03</span>
      <span class="service-icon">🔥</span>
      <h3 class="service-title">Firebase Integration</h3>
      <p class="service-desc">Full Firebase BaaS setup: Auth, Firestore, Realtime DB, Cloud Storage, and FCM push notifications for real-time, offline-first apps.</p>
    </div>
    <div class="service-card">
      <span class="service-num">04</span>
      <span class="service-icon">🏗️</span>
      <h3 class="service-title">App Architecture</h3>
      <p class="service-desc">Scalable, maintainable codebases using Clean Architecture, MVVM, and MVC patterns with Provider & GetX state management.</p>
    </div>
    <div class="service-card">
      <span class="service-num">05</span>
      <span class="service-icon">🔌</span>
      <h3 class="service-title">API & SDK Integration</h3>
      <p class="service-desc">REST API integration, JSON parsing, third-party SDKs, and payment gateway implementation — Stripe, PayPal, and local gateways.</p>
    </div>
    <div class="service-card">
      <span class="service-num">06</span>
      <span class="service-icon">🌐</span>
      <h3 class="service-title">Flutter Web</h3>
      <p class="service-desc">Extend your Flutter app to the web. Responsive layouts, cross-device compatibility, and consistent design from a single codebase.</p>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label">04 &nbsp; Notable Projects</div>
  <h2 class="section-title reveal">FEATURED<br>WORK</h2>
  <div class="projects-grid">
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">E-Commerce & Retail</span>
      <h3 class="project-title">Retail Commerce Platforms</h3>
      <p class="project-desc">Responsive product listings, cart flows, checkout funnels, order tracking, and payment gateway integration across multiple retail clients.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">GetX</span>
        <span class="tech-pill">REST API</span>
        <span class="tech-pill">Payment Gateway</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">Healthcare</span>
      <h3 class="project-title">Telemedicine Apps</h3>
      <p class="project-desc">Patient and doctor-facing UIs: appointment booking, consultation flows, prescription management, and health record screens.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">Firebase</span>
        <span class="tech-pill">FCM</span>
        <span class="tech-pill">Firestore</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">Fintech</span>
      <h3 class="project-title">Wallet & Banking Apps</h3>
      <p class="project-desc">Secure transaction flows, digital wallet dashboards, balance screens, and fund transfer interfaces following mobile security best practices.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">Provider</span>
        <span class="tech-pill">Clean Architecture</span>
        <span class="tech-pill">Encryption</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">Logistics</span>
      <h3 class="project-title">Fleet Tracking System</h3>
      <p class="project-desc">Real-time delivery tracking, driver dashboards, dispatch management, and live map route visualization for logistics clients.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">Google Maps</span>
        <span class="tech-pill">Realtime DB</span>
        <span class="tech-pill">GetX</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">Hospitality</span>
      <h3 class="project-title">Booking & Scheduling Apps</h3>
      <p class="project-desc">Calendar-based booking flows, service availability management, provider profiles, and automated reminders for service sectors.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">Firebase</span>
        <span class="tech-pill">Notifications</span>
        <span class="tech-pill">MVVM</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-arrow">↗</span>
      <span class="project-tag">Enterprise</span>
      <h3 class="project-title">ERP & Analytics Dashboards</h3>
      <p class="project-desc">Supplier management, inventory tracking, HR modules, and multi-role analytics dashboards for SME clients across manufacturing.</p>
      <div class="project-tech">
        <span class="tech-pill">Flutter</span>
        <span class="tech-pill">REST API</span>
        <span class="tech-pill">Charts</span>
        <span class="tech-pill">MVC</span>
      </div>
    </div>
  </div>
</section>

<!-- EXPERIENCE -->
<section id="experience">
  <div class="section-label">05 &nbsp; Experience</div>
  <h2 class="section-title reveal">CAREER<br>JOURNEY</h2>
  <div class="timeline">
    <div class="timeline-item reveal">
      <div class="timeline-dot"></div>
      <div class="timeline-date">Jan 2021 — Present</div>
      <h3 class="timeline-company">Duseca Software</h3>
      <p class="timeline-role">Senior Flutter Developer</p>
      <ul class="timeline-points">
        <li>Architected and delivered frontend for 300+ mobile apps across e-commerce, healthcare, logistics, fintech & hospitality</li>
        <li>Primary client contact for international clients — managed communication, requirement meetings & technical scoping</li>
        <li>Foreign client traveled to Pakistan specifically to acknowledge the quality of delivered work</li>
        <li>Pixel-perfect Flutter UIs with cross-device performance optimization</li>
        <li>Guided UI/UX designers on feasibility, improving handoff quality and reducing rework cycles</li>
      </ul>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot"></div>
      <div class="timeline-date">Dec 2020 — Jan 2022</div>
      <h3 class="timeline-company">Terasharp</h3>
      <p class="timeline-role">Flutter Developer</p>
      <ul class="timeline-points">
        <li>Developed cross-platform mobile apps for diverse client verticals using Flutter & Dart</li>
        <li>Built and maintained a reusable component library accelerating frontend development</li>
        <li>Integrated REST APIs and Firebase backend services for seamless real-time functionality</li>
        <li>Contributed to scalable frontend architecture patterns adopted team-wide</li>
      </ul>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot"></div>
      <div class="timeline-date">Contract</div>
      <h3 class="timeline-company">MasterMind Tech</h3>
      <p class="timeline-role">Flutter Developer</p>
      <ul class="timeline-points">
        <li>Delivered specialized mobile frontend solutions as part of high-impact project engagements</li>
        <li>Worked closely with product teams to translate domain requirements into intuitive mobile interfaces</li>
      </ul>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot"></div>
      <div class="timeline-date">2021 — 2024</div>
      <h3 class="timeline-company">Fiverr & Upwork</h3>
      <p class="timeline-role">Freelance Flutter Developer</p>
      <ul class="timeline-points">
        <li>Built and ranked profiles on both platforms through consistent quality and strong client reviews</li>
        <li>Independently managed full client lifecycle: qualification, discovery calls, proposals, development & support</li>
        <li>Maintained strong repeat-business track record across international clientele</li>
      </ul>
    </div>
  </div>
</section>

<!-- HIRE ME -->
<section id="hirme">
  <div class="section-label">06 &nbsp; Let's Work Together</div>
  <h2 class="section-title">HAVE A<br>PROJECT?</h2>
  <p class="hire-subtitle">Ready to build your next mobile app? Let's talk. I'm available for freelance projects, full-time roles, and long-term collaborations.</p>
  <div class="hire-btns">
    <a href="https://wa.me/923049184381" target="_blank" class="hire-btn hire-btn-whatsapp">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      WhatsApp
    </a>
    <a href="https://linkedin.com/in/ahadnaveed" target="_blank" class="hire-btn hire-btn-linkedin">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      LinkedIn
    </a>
    <a href="mailto:babaa336@gmail.com" class="hire-btn hire-btn-email">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      Email Me
    </a>
  </div>
  <div class="contact-info">
    <div class="contact-item">📍 Sahiwal, Punjab, Pakistan</div>
    <div class="contact-item"><a href="tel:+923049184381">📞 +92-304-9184381</a></div>
    <div class="contact-item"><a href="https://github.com/Ahad2222" target="_blank">⌨ github.com/Ahad2222</a></div>
    <div class="contact-item"><a href="mailto:babaa336@gmail.com">✉ babaa336@gmail.com</a></div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">AN.</div>
  <div class="footer-copy">© 2025 Ahad Naveed — Senior Flutter Developer</div>
  <div class="footer-copy" style="font-size:10px; color: var(--muted);">Sahiwal · Pakistan</div>
</footer>

<!-- THREE.JS CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<script>
/* ─── CURSOR ─── */
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursor-trail');
let mx = 0, my = 0, tx = 0, ty = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx - 6 + 'px';
  cursor.style.top = my - 6 + 'px';
});

function animCursor() {
  tx += (mx - tx) * 0.12;
  ty += (my - ty) * 0.12;
  trail.style.left = tx - 18 + 'px';
  trail.style.top = ty - 18 + 'px';
  requestAnimationFrame(animCursor);
}
animCursor();

document.querySelectorAll('a, button, .service-card, .project-card, .about-card').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform = 'scale(2.5)';
    trail.style.transform = 'scale(1.5)';
    trail.style.borderColor = 'rgba(0,229,255,0.7)';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.transform = 'scale(1)';
    trail.style.transform = 'scale(1)';
    trail.style.borderColor = 'rgba(0,229,255,0.4)';
  });
});

/* ─── THREE.JS 3D GRID HERO ─── */
const canvas = document.getElementById('hero-canvas');
const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
renderer.setSize(window.innerWidth, window.innerHeight);

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.set(0, 8, 20);
camera.lookAt(0, 0, 0);

// Grid lines
const gridMat = new THREE.LineBasicMaterial({ color: 0x00e5ff, transparent: true, opacity: 0.08 });
const gridGroup = new THREE.Group();

for (let i = -20; i <= 20; i++) {
  const hGeo = new THREE.BufferGeometry().setFromPoints([
    new THREE.Vector3(-20, 0, i), new THREE.Vector3(20, 0, i)
  ]);
  const vGeo = new THREE.BufferGeometry().setFromPoints([
    new THREE.Vector3(i, 0, -20), new THREE.Vector3(i, 0, 20)
  ]);
  gridGroup.add(new THREE.Line(hGeo, gridMat));
  gridGroup.add(new THREE.Line(vGeo, gridMat));
}
gridGroup.position.y = -4;
scene.add(gridGroup);

// Floating particles
const particleGeo = new THREE.BufferGeometry();
const count = 120;
const positions = new Float32Array(count * 3);
for (let i = 0; i < count; i++) {
  positions[i * 3]     = (Math.random() - 0.5) * 60;
  positions[i * 3 + 1] = Math.random() * 20 - 5;
  positions[i * 3 + 2] = (Math.random() - 0.5) * 40;
}
particleGeo.setAttribute('position', new THREE.BufferAttribute(positions, 3));
const particleMat = new THREE.PointsMaterial({ color: 0x00e5ff, size: 0.08, transparent: true, opacity: 0.6 });
const particles = new THREE.Points(particleGeo, particleMat);
scene.add(particles);

// Vertical accent lines
const vLineMat = new THREE.LineBasicMaterial({ color: 0x7b2fff, transparent: true, opacity: 0.15 });
for (let i = 0; i < 8; i++) {
  const x = (Math.random() - 0.5) * 30;
  const z = (Math.random() - 0.5) * 20;
  const h = Math.random() * 6 + 2;
  const vGeo = new THREE.BufferGeometry().setFromPoints([
    new THREE.Vector3(x, -4, z), new THREE.Vector3(x, -4 + h, z)
  ]);
  scene.add(new THREE.Line(vGeo, vLineMat));
}

// Ambient light
const ambientLight = new THREE.AmbientLight(0x00e5ff, 0.1);
scene.add(ambientLight);

let scrollY = 0;
window.addEventListener('scroll', () => { scrollY = window.scrollY; });

function animate3D(t) {
  requestAnimationFrame(animate3D);
  const time = t * 0.001;
  gridGroup.position.z = (time * 2) % 2;
  particles.rotation.y = time * 0.04;
  camera.position.y = 8 - scrollY * 0.005;
  renderer.render(scene, camera);
}
animate3D(0);

window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});

/* ─── SCROLL REVEAL ─── */
const revealEls = document.querySelectorAll('.reveal');
const timelineItems = document.querySelectorAll('.timeline-item');

const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      // Trigger skill bars
      const bars = entry.target.querySelectorAll('.skill-bar-fill');
      bars.forEach(bar => {
        setTimeout(() => { bar.style.width = bar.dataset.width + '%'; }, 200);
      });
    }
  });
}, { threshold: 0.15 });

revealEls.forEach(el => observer.observe(el));
timelineItems.forEach(el => observer.observe(el));

// Also trigger skill bars that are already visible
document.querySelectorAll('.skill-bar-fill').forEach(bar => {
  const parentObserver = new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) {
      setTimeout(() => { bar.style.width = bar.dataset.width + '%'; }, 300);
      parentObserver.disconnect();
    }
  }, { threshold: 0.3 });
  parentObserver.observe(bar.closest('.skill-bar-item'));
});

/* ─── ACTIVE NAV ─── */
const sections = document.querySelectorAll('section[id]');
const navLinks = document.querySelectorAll('.nav-link');

window.addEventListener('scroll', () => {
  let current = '';
  sections.forEach(s => {
    if (window.scrollY >= s.offsetTop - 200) current = s.id;
  });
  navLinks.forEach(a => {
    a.classList.remove('active');
    if (a.getAttribute('href') === '#' + current) a.classList.add('active');
  });
});

/* ─── PARALLAX on HERO ─── */
window.addEventListener('scroll', () => {
  const y = window.scrollY;
  const heroContent = document.querySelector('.hero-content');
  if (heroContent) heroContent.style.transform = `translateY(${y * 0.25}px)`;
  const heroStats = document.querySelector('.hero-stats');
  if (heroStats) heroStats.style.transform = `translateY(${y * 0.15}px)`;
});
</script>
</body>
</html>
