---
layout: none
title: DSA Portal
permalink: /sheriff/
search_exclude: true
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Deputy Sheriffs' Association of San Diego County</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; scroll-padding-top: 80px; }
    body { font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; background: #0b1a2e; color: #e2e8f0; line-height: 1.6; }
    a { color: #60a5fa; text-decoration: none; }

    /* ===== HEADER ===== */
    .header {
      position: sticky; top: 0; z-index: 1000;
      background: rgba(15,40,71,0.95); backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255,255,255,0.06);
    }
    .header-inner {
      max-width: 1200px; margin: 0 auto; height: 64px;
      display: flex; align-items: center; justify-content: space-between; padding: 0 24px; gap: 16px;
    }
    .logo { display: flex; align-items: center; gap: 10px; flex-shrink: 0; cursor: pointer; }
    .logo-badge { width: 38px; height: 38px; background: linear-gradient(135deg,#fbbf24,#d97706); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: 900; font-size: 0.8rem; color: #1e3a5f; }
    .logo-text { font-size: 0.95rem; font-weight: 700; color: #fff; }
    .logo-sub { font-size: 0.62rem; color: #64748b; text-transform: uppercase; letter-spacing: 1.5px; }

    nav { display: flex; gap: 2px; align-items: center; }
    .nav-link {
      padding: 8px 14px; border-radius: 8px; font-size: 0.82rem; font-weight: 500; color: #94a3b8;
      cursor: pointer; transition: all 0.15s; white-space: nowrap;
    }
    .nav-link:hover, .nav-link.active { color: #fbbf24; background: rgba(251,191,36,0.08); }

    .header-right { display: flex; align-items: center; gap: 10px; flex-shrink: 0; }

    .search-box { position: relative; }
    .search-box input {
      width: 180px; padding: 7px 32px 7px 12px; background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.08);
      border-radius: 20px; color: #e2e8f0; font-size: 0.8rem; outline: none; transition: all 0.25s;
    }
    .search-box input::placeholder { color: #475569; }
    .search-box input:focus { border-color: #fbbf24; width: 240px; background: rgba(255,255,255,0.1); }
    .search-box .icon { position: absolute; right: 10px; top: 50%; transform: translateY(-50%); color: #475569; font-size: 0.8rem; pointer-events: none; }
    .search-dropdown {
      display: none; position: absolute; top: calc(100% + 6px); left: 0; right: 0;
      background: #162a46; border: 1px solid #2a3a5c; border-radius: 10px; overflow: hidden;
      box-shadow: 0 12px 40px rgba(0,0,0,0.5); z-index: 1001;
    }
    .search-dropdown.open { display: block; }
    .search-item { padding: 10px 14px; font-size: 0.82rem; color: #cbd5e1; cursor: pointer; border-bottom: 1px solid #1e3352; }
    .search-item:hover { background: rgba(251,191,36,0.08); color: #fbbf24; }
    .search-item:last-child { border-bottom: none; }

    .btn { padding: 7px 16px; border-radius: 8px; font-size: 0.8rem; font-weight: 600; cursor: pointer; border: none; transition: all 0.2s; }
    .btn-outline { background: transparent; color: #fbbf24; border: 1px solid rgba(251,191,36,0.4); }
    .btn-outline:hover { background: rgba(251,191,36,0.1); }
    .btn-gold { background: linear-gradient(135deg,#f59e0b,#d97706); color: #1e3a5f; }
    .btn-gold:hover { box-shadow: 0 4px 14px rgba(245,158,11,0.3); }

    .user-area { position: relative; display: none; }
    .user-area.active { display: flex; align-items: center; }
    .user-chip {
      display: flex; align-items: center; gap: 6px; padding: 5px 12px;
      background: rgba(251,191,36,0.08); border: 1px solid rgba(251,191,36,0.3); border-radius: 8px;
      color: #fbbf24; font-size: 0.8rem; font-weight: 600; cursor: pointer;
    }
    .user-panel {
      display: none; position: absolute; top: calc(100% + 8px); right: 0;
      background: #162a46; border: 1px solid #2a3a5c; border-radius: 12px;
      min-width: 220px; box-shadow: 0 12px 40px rgba(0,0,0,0.5); overflow: hidden; z-index: 1001;
    }
    .user-panel.open { display: block; }
    .up-header { padding: 14px 16px; background: rgba(251,191,36,0.04); border-bottom: 1px solid #1e3352; }
    .up-name { font-weight: 700; color: #fbbf24; }
    .up-badge { font-size: 0.72rem; color: #64748b; }
    .up-item { padding: 10px 16px; font-size: 0.82rem; color: #94a3b8; cursor: pointer; border-bottom: 1px solid #1e3352; }
    .up-item:hover { background: rgba(96,165,250,0.06); color: #fff; }

    .back-link {
      position: fixed; bottom: 20px; left: 20px; padding: 6px 14px;
      background: rgba(96,165,250,0.12); border: 1px solid rgba(96,165,250,0.3); border-radius: 8px;
      color: #60a5fa; font-size: 0.75rem; z-index: 999; transition: all 0.2s;
    }
    .back-link:hover { background: #3b82f6; color: #fff; }

    /* ===== HERO ===== */
    .hero {
      padding: 100px 24px 80px; text-align: center;
      background: linear-gradient(170deg, rgba(15,40,71,0.92) 0%, rgba(22,42,70,0.94) 40%, rgba(11,26,46,0.96) 100%);
      position: relative; overflow: hidden;
    }
    .hero::before {
      content: ''; position: absolute; inset: 0;
      background: url('{{ site.baseurl }}/images/dsa/store-uniforms.jpg') center/cover no-repeat;
      opacity: 0.12; z-index: 0;
    }
    .hero::after {
      content: ''; position: absolute; top: 50%; left: 50%; width: 600px; height: 600px;
      background: radial-gradient(circle, rgba(251,191,36,0.06) 0%, transparent 70%);
      transform: translate(-50%,-50%); pointer-events: none; z-index: 0;
    }
    .hero-inner { position: relative; z-index: 1; max-width: 720px; margin: 0 auto; }
    .hero-logo { width: 110px; height: auto; margin-bottom: 20px; filter: drop-shadow(0 4px 16px rgba(0,0,0,0.5)); }
    .hero h2 { font-size: 2.6rem; font-weight: 800; background: linear-gradient(135deg,#fbbf24,#f59e0b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 14px; }
    .hero p { font-size: 1.05rem; color: #7f8ea3; margin-bottom: 28px; }

    /* Image cards */
    .img-card { border-radius: 12px; overflow: hidden; }
    .img-card img { width: 100%; height: 180px; object-fit: cover; display: block; }
    .news-card .img-card img { height: 160px; }
    .about-card .img-card { margin-bottom: 14px; }
    .about-card .img-card img { height: 170px; }
    .store-hero { border-radius: 14px; overflow: hidden; margin-bottom: 24px; }
    .store-hero img { width: 100%; height: 240px; object-fit: cover; display: block; }
    .hero-cta { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
    .hero-cta .btn { padding: 12px 28px; font-size: 0.9rem; border-radius: 10px; }
    .stats { display: flex; justify-content: center; gap: 48px; margin-top: 50px; flex-wrap: wrap; }
    .stat-num { font-size: 2rem; font-weight: 800; color: #fbbf24; }
    .stat-label { font-size: 0.7rem; color: #475569; text-transform: uppercase; letter-spacing: 1px; }

    /* ===== SECTIONS ===== */
    .section { max-width: 1100px; margin: 0 auto; padding: 60px 24px; }
    .sec-head { text-align: center; margin-bottom: 36px; }
    .sec-head h2 { font-size: 1.7rem; font-weight: 700; color: #fff; margin-bottom: 6px; }
    .sec-head p { color: #475569; font-size: 0.9rem; }

    /* Tiles */
    .tiles { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
    .tile {
      background: rgba(22,42,70,0.6); border: 1px solid rgba(255,255,255,0.06); border-radius: 12px;
      padding: 20px; cursor: pointer; transition: all 0.25s; position: relative;
    }
    .tile:hover { border-color: #fbbf24; transform: translateY(-3px); box-shadow: 0 8px 24px rgba(0,0,0,0.3); }
    .tile-icon { font-size: 1.6rem; margin-bottom: 8px; }
    .tile-title { font-size: 0.9rem; font-weight: 700; color: #fff; margin-bottom: 4px; }
    .tile-desc { font-size: 0.76rem; color: #64748b; line-height: 1.5; }

    /* Expandable detail panel (opens inline, no page redirect) */
    .detail-panel {
      display: none; max-width: 1100px; margin: -20px auto 0; padding: 0 24px 40px;
      animation: panelIn 0.3s ease;
    }
    .detail-panel.open { display: block; }
    @keyframes panelIn { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: none; } }
    .dp-card {
      background: #162a46; border: 1px solid #1e3352; border-radius: 14px; padding: 32px;
      position: relative;
    }
    .dp-close { position: absolute; top: 14px; right: 18px; background: none; border: none; color: #475569; font-size: 1.4rem; cursor: pointer; }
    .dp-close:hover { color: #ef4444; }
    .dp-card h3 { font-size: 1.3rem; color: #fbbf24; margin-bottom: 16px; }
    .dp-card p, .dp-card li { font-size: 0.88rem; color: #94a3b8; line-height: 1.7; }
    .dp-card ul { padding-left: 20px; margin-top: 10px; }
    .dp-card li { margin-bottom: 6px; }
    .dp-card .dp-contact { margin-top: 16px; padding: 14px; background: rgba(251,191,36,0.05); border-radius: 8px; font-size: 0.82rem; color: #cbd5e1; }

    /* News */
    .news-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
    .news-card { background: #162a46; border: 1px solid #1e3352; border-radius: 12px; padding: 22px; transition: border-color 0.2s; }
    .news-card:hover { border-color: #3b82f6; }
    .news-tag { display: inline-block; padding: 2px 8px; border-radius: 12px; font-size: 0.65rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 8px; }
    .t-ann { background: rgba(251,191,36,0.12); color: #fbbf24; }
    .t-evt { background: rgba(96,165,250,0.12); color: #60a5fa; }
    .t-ben { background: rgba(52,211,153,0.12); color: #34d399; }
    .news-card h3 { font-size: 1rem; color: #fff; margin-bottom: 6px; }
    .news-card p { font-size: 0.8rem; color: #7f8ea3; }
    .news-date { font-size: 0.7rem; color: #3b4d6b; margin-top: 8px; }

    /* Events */
    .ev-list { display: flex; flex-direction: column; gap: 10px; }
    .ev {
      display: flex; align-items: center; gap: 16px;
      background: #162a46; border: 1px solid #1e3352; border-radius: 10px; padding: 14px 18px; transition: border-color 0.2s;
    }
    .ev:hover { border-color: #60a5fa; }
    .ev-date { min-width: 50px; text-align: center; background: rgba(96,165,250,0.08); border-radius: 8px; padding: 6px; }
    .ev-date .m { font-size: 0.6rem; text-transform: uppercase; color: #60a5fa; letter-spacing: 1px; }
    .ev-date .d { font-size: 1.3rem; font-weight: 800; color: #fff; }
    .ev-info h4 { font-size: 0.88rem; color: #fff; }
    .ev-info p { font-size: 0.75rem; color: #475569; }
    .ev-rsvp {
      margin-left: auto; padding: 6px 14px; background: rgba(96,165,250,0.1); border: 1px solid rgba(96,165,250,0.3);
      border-radius: 6px; color: #60a5fa; font-size: 0.75rem; font-weight: 600; cursor: pointer; transition: all 0.2s;
    }
    .ev-rsvp:hover { background: #3b82f6; color: #fff; border-color: #3b82f6; }
    .ev-rsvp.done { background: rgba(52,211,153,0.1); border-color: #34d399; color: #34d399; pointer-events: none; }

    /* About */
    .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
    .about-card { background: #162a46; border: 1px solid #1e3352; border-radius: 12px; padding: 24px; }
    .about-card h3 { font-size: 1.05rem; color: #fbbf24; margin-bottom: 10px; }
    .about-card p { font-size: 0.84rem; color: #7f8ea3; }
    .about-card ul { padding-left: 18px; margin-top: 8px; }
    .about-card li { font-size: 0.82rem; color: #94a3b8; margin-bottom: 4px; }

    /* FAQ */
    .faq-wrap { max-width: 800px; margin: 0 auto; }
    .faq-bar { display: flex; gap: 8px; margin-bottom: 16px; flex-wrap: wrap; align-items: center; }
    .faq-bar input { flex: 1; min-width: 200px; padding: 10px 16px; background: #162a46; border: 1px solid #1e3352; border-radius: 10px; color: #e2e8f0; font-size: 0.88rem; outline: none; }
    .faq-bar input:focus { border-color: #fbbf24; }
    .faq-tag { padding: 5px 12px; border-radius: 16px; font-size: 0.72rem; font-weight: 600; background: rgba(255,255,255,0.04); border: 1px solid #1e3352; color: #64748b; cursor: pointer; transition: all 0.15s; }
    .faq-tag.on, .faq-tag:hover { background: rgba(251,191,36,0.1); border-color: #fbbf24; color: #fbbf24; }
    .fq { background: #162a46; border: 1px solid #1e3352; border-radius: 10px; margin-bottom: 8px; overflow: hidden; }
    .fq-q { padding: 14px 18px; cursor: pointer; display: flex; justify-content: space-between; align-items: center; font-weight: 600; font-size: 0.9rem; color: #e2e8f0; }
    .fq-q .t { color: #fbbf24; transition: transform 0.25s; font-size: 1.1rem; }
    .fq-q.open .t { transform: rotate(45deg); }
    .fq-a { display: none; padding: 0 18px 14px; font-size: 0.84rem; color: #7f8ea3; line-height: 1.7; }
    .fq-a.open { display: block; }

    /* Store */
    .store-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; }
    .store-item {
      background: #162a46; border: 1px solid #1e3352; border-radius: 12px; padding: 20px; text-align: center; transition: all 0.2s;
    }
    .store-item:hover { border-color: #fbbf24; transform: translateY(-2px); }
    .store-item .si-icon { font-size: 2rem; margin-bottom: 8px; }
    .store-item h4 { font-size: 0.88rem; color: #fff; margin-bottom: 4px; }
    .store-item p { font-size: 0.72rem; color: #475569; }
    .store-item .price { font-size: 0.9rem; font-weight: 700; color: #fbbf24; margin-top: 8px; }

    /* Contact */
    .contact-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
    .c-card { background: #162a46; border: 1px solid #1e3352; border-radius: 12px; padding: 24px; text-align: center; }
    .c-card .c-icon { font-size: 1.6rem; margin-bottom: 8px; }
    .c-card h4 { font-size: 0.9rem; color: #fff; margin-bottom: 4px; }
    .c-card p { font-size: 0.82rem; color: #7f8ea3; }
    .c-card a { color: #fbbf24; }

    /* Admin */
    .admin-section { display: none; }
    .admin-section.open { display: block; }
    .a-table { width: 100%; border-collapse: collapse; background: #162a46; border-radius: 12px; overflow: hidden; }
    .a-table th { background: #0f2040; padding: 12px 16px; text-align: left; font-size: 0.72rem; color: #fbbf24; text-transform: uppercase; letter-spacing: 0.5px; }
    .a-table td { padding: 10px 16px; border-bottom: 1px solid #1e3352; font-size: 0.82rem; color: #cbd5e1; }
    .a-table tr:hover td { background: rgba(96,165,250,0.04); }
    .badge-s { padding: 2px 8px; border-radius: 10px; font-size: 0.68rem; font-weight: 600; }
    .badge-active { background: rgba(52,211,153,0.12); color: #34d399; }

    /* Footer */
    footer { background: #091425; border-top: 1px solid #1e3352; padding: 36px 24px; margin-top: 40px; }
    .ft-inner { max-width: 1100px; margin: 0 auto; display: grid; grid-template-columns: 2fr 1fr 1fr; gap: 32px; }
    .ft-col h4 { color: #fbbf24; font-size: 0.8rem; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 12px; }
    .ft-col p, .ft-col a { font-size: 0.8rem; color: #3b4d6b; display: block; margin-bottom: 6px; }
    .ft-col a:hover { color: #fbbf24; }
    .ft-copy { text-align: center; margin-top: 24px; font-size: 0.72rem; color: #1e3352; }

    /* Chatbot */
    .cb-trigger {
      position: fixed; bottom: 22px; right: 22px; width: 56px; height: 56px;
      background: linear-gradient(135deg,#f59e0b,#d97706); border-radius: 50%; border: none;
      display: flex; align-items: center; justify-content: center; font-size: 1.4rem;
      cursor: pointer; box-shadow: 0 6px 24px rgba(245,158,11,0.35); z-index: 1100; transition: transform 0.2s;
    }
    .cb-trigger:hover { transform: scale(1.08); }
    .cb-win {
      display: none; position: fixed; bottom: 90px; right: 22px; width: 370px; max-height: 480px;
      background: #162a46; border: 1px solid #2a3a5c; border-radius: 14px;
      z-index: 1100; box-shadow: 0 16px 50px rgba(0,0,0,0.5); flex-direction: column; overflow: hidden;
    }
    .cb-win.open { display: flex; }
    .cb-head { background: #0f2040; padding: 14px 18px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #1e3352; }
    .cb-head h3 { color: #fbbf24; font-size: 0.92rem; }
    .cb-x { background: none; border: none; color: #475569; font-size: 1.3rem; cursor: pointer; }
    .cb-msgs { flex: 1; overflow-y: auto; padding: 14px; max-height: 320px; }
    .cm { margin-bottom: 10px; display: flex; }
    .cm.bot { justify-content: flex-start; }
    .cm.user { justify-content: flex-end; }
    .cb { max-width: 82%; padding: 9px 13px; border-radius: 10px; font-size: 0.82rem; line-height: 1.5; }
    .cm.bot .cb { background: #0f2040; color: #cbd5e1; border-bottom-left-radius: 3px; }
    .cm.user .cb { background: #3b82f6; color: #fff; border-bottom-right-radius: 3px; }
    .cb-input { display: flex; gap: 8px; padding: 10px 14px; border-top: 1px solid #1e3352; background: #0f2040; }
    .cb-input input { flex: 1; padding: 9px 12px; background: rgba(255,255,255,0.04); border: 1px solid #1e3352; border-radius: 8px; color: #e2e8f0; font-size: 0.82rem; outline: none; }
    .cb-input button { padding: 9px 14px; background: #f59e0b; border: none; border-radius: 8px; color: #1e3a5f; font-weight: 700; font-size: 0.82rem; cursor: pointer; }
    .cb-input button:disabled { opacity: 0.4; cursor: not-allowed; }
    .typing-dots { display: flex; gap: 4px; padding: 10px 14px !important; align-items: center; }
    .typing-dots span { width: 7px; height: 7px; background: #475569; border-radius: 50%; animation: tdot 1.4s infinite ease-in-out both; }
    .typing-dots span:nth-child(2) { animation-delay: 0.2s; }
    .typing-dots span:nth-child(3) { animation-delay: 0.4s; }
    @keyframes tdot { 0%,80%,100% { transform: scale(0.5); opacity: 0.3; } 40% { transform: scale(1); opacity: 1; } }

    /* Modal */
    .modal-bg { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.65); z-index: 2000; align-items: center; justify-content: center; }
    .modal-bg.open { display: flex; }
    .modal { background: #162a46; border: 1px solid #2a3a5c; border-radius: 16px; padding: 36px; width: 100%; max-width: 420px; position: relative; }
    .modal-x { position: absolute; top: 14px; right: 16px; background: none; border: none; color: #475569; font-size: 1.4rem; cursor: pointer; }
    .modal h2 { font-size: 1.4rem; color: #fbbf24; margin-bottom: 4px; }
    .modal .sub { color: #475569; font-size: 0.82rem; margin-bottom: 20px; }
    .mtabs { display: flex; margin-bottom: 20px; }
    .mtab { flex: 1; padding: 8px; text-align: center; font-weight: 600; font-size: 0.85rem; color: #475569; border-bottom: 2px solid transparent; cursor: pointer; }
    .mtab.on { color: #fbbf24; border-bottom-color: #fbbf24; }
    .fg { margin-bottom: 14px; }
    .fg label { display: block; font-size: 0.72rem; color: #64748b; margin-bottom: 4px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; }
    .fg input, .fg select {
      width: 100%; padding: 10px 12px; background: rgba(255,255,255,0.04); border: 1px solid #1e3352;
      border-radius: 8px; color: #e2e8f0; font-size: 0.85rem; outline: none;
    }
    .fg input:focus, .fg select:focus { border-color: #fbbf24; }
    .fg select option { background: #162a46; }
    .modal-submit { width: 100%; padding: 12px; background: linear-gradient(135deg,#f59e0b,#d97706); border: none; border-radius: 10px; color: #1e3a5f; font-size: 0.95rem; font-weight: 700; cursor: pointer; margin-top: 6px; }
    .modal-err { color: #ef4444; font-size: 0.8rem; margin-top: 8px; display: none; }

    /* Mobile */
    .mob-toggle { display: none; background: none; border: none; color: #fff; font-size: 1.4rem; cursor: pointer; }
    @media (max-width: 900px) {
      nav { display: none; }
      .mob-toggle { display: block; }
      .tiles { grid-template-columns: repeat(2, 1fr); }
      .news-grid { grid-template-columns: 1fr; }
      .about-grid { grid-template-columns: 1fr; }
      .store-grid { grid-template-columns: repeat(2, 1fr); }
      .contact-row { grid-template-columns: 1fr; }
      .ft-inner { grid-template-columns: 1fr; }
      .hero h2 { font-size: 1.8rem; }
      .stats { gap: 20px; }
      .search-box input { width: 140px; }
      .cb-win { width: calc(100% - 40px); right: 20px; }
    }
    @media (max-width: 500px) {
      .tiles { grid-template-columns: 1fr; }
      .store-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<a href="{{ site.baseurl }}/" class="back-link">&#8592; Main Site</a>

<!-- HEADER -->
<header class="header">
  <div class="header-inner">
    <div class="logo" onclick="scrollTo('#top')">
      <img src="{{ site.baseurl }}/images/dsa/dsa-logo.png" alt="DSA Logo" style="width:42px;height:auto;">
      <div><div class="logo-text">Deputy Sheriffs' Assoc.</div><div class="logo-sub">San Diego County</div></div>
    </div>
    <nav>
      <div class="nav-link" onclick="scrollTo('#dashboard')">Resources</div>
      <div class="nav-link" onclick="scrollTo('#news')">News</div>
      <div class="nav-link" onclick="scrollTo('#events')">Events</div>
      <div class="nav-link" onclick="scrollTo('#about')">About</div>
      <div class="nav-link" onclick="scrollTo('#store')">Store</div>
      <div class="nav-link" onclick="scrollTo('#faq')">FAQ</div>
      <div class="nav-link" onclick="scrollTo('#contact')">Contact</div>
    </nav>
    <div class="header-right">
      <div class="search-box">
        <input type="text" placeholder="Search..." id="searchInput" autocomplete="off">
        <span class="icon">&#128269;</span>
        <div class="search-dropdown" id="searchDrop"></div>
      </div>
      <div id="authBtns">
        <button class="btn btn-outline" onclick="openModal('login')">Log In</button>
        <button class="btn btn-gold" onclick="openModal('signup')">Join</button>
      </div>
      <div class="user-area" id="userArea">
        <div class="user-chip" onclick="document.getElementById('userPanel').classList.toggle('open')">
          &#9733; <span id="uName">Deputy</span> &#9662;
        </div>
        <div class="user-panel" id="userPanel">
          <div class="up-header"><div class="up-name" id="upName">-</div><div class="up-badge" id="upBadge">-</div></div>
          <div class="up-item" id="upRank">-</div>
          <div class="up-item" id="upStation">-</div>
          <div class="up-item" id="adminBtn" style="display:none" onclick="toggleAdmin()">&#128100; View All Members</div>
          <div class="up-item" onclick="logout()" style="color:#ef4444">&#128682; Log Out</div>
        </div>
      </div>
      <button class="mob-toggle" onclick="this.nextElementSibling?.classList.toggle('open')">&#9776;</button>
    </div>
  </div>
</header>

<!-- HERO -->
<section class="hero" id="top">
  <div class="hero-inner">
    <img src="{{ site.baseurl }}/images/dsa/dsa-logo.png" alt="DSA Badge" class="hero-logo">
    <h2>The Strength Behind the Badge</h2>
    <p>Representing the dedicated officers of the San Diego County Sheriff's Department since 1955. Benefits, legal defense, events, and advocacy &mdash; all in one place.</p>
    <div class="hero-cta">
      <button class="btn btn-gold" onclick="scrollTo('#dashboard')">Explore Resources</button>
      <button class="btn btn-outline" onclick="scrollTo('#about')">Learn About DSA</button>
    </div>
    <div class="stats">
      <div><div class="stat-num">4,229</div><div class="stat-label">Active Members</div></div>
      <div><div class="stat-num">70+</div><div class="stat-label">Years of Service</div></div>
      <div><div class="stat-num">12</div><div class="stat-label">Stations</div></div>
      <div><div class="stat-num">24/7</div><div class="stat-label">Support</div></div>
    </div>
  </div>
</section>

<!-- DASHBOARD -->
<div class="section" id="dashboard">
  <div class="sec-head"><h2>Member Resources</h2><p>Click any tile to see details instantly &mdash; no extra pages</p></div>
  <div class="tiles">
    <div class="tile" onclick="openDetail('benefits')"><div class="tile-icon">&#128179;</div><div class="tile-title">Benefits</div><div class="tile-desc">Health, dental, vision & life insurance</div></div>
    <div class="tile" onclick="openDetail('legal')"><div class="tile-icon">&#128272;</div><div class="tile-title">Legal Defense</div><div class="tile-desc">Representation & defense fund</div></div>
    <div class="tile" onclick="openDetail('wellness')"><div class="tile-icon">&#127891;</div><div class="tile-title">Wellness</div><div class="tile-desc">Peer support & mental health</div></div>
    <div class="tile" onclick="openDetail('forms')"><div class="tile-icon">&#128196;</div><div class="tile-title">Forms & Docs</div><div class="tile-desc">Contracts, forms & downloads</div></div>
    <div class="tile" onclick="scrollTo('#events')"><div class="tile-icon">&#128197;</div><div class="tile-title">Events</div><div class="tile-desc">Upcoming meetings & social events</div></div>
    <div class="tile" onclick="scrollTo('#store')"><div class="tile-icon">&#128176;</div><div class="tile-title">DSA Store</div><div class="tile-desc">Official merch & apparel</div></div>
    <div class="tile" onclick="openDetail('newsletters')"><div class="tile-icon">&#128240;</div><div class="tile-title">Newsletters</div><div class="tile-desc">Monthly publications & minutes</div></div>
    <div class="tile" onclick="openDetail('pac')"><div class="tile-icon">&#127937;</div><div class="tile-title">Political Action</div><div class="tile-desc">PAC updates & endorsements</div></div>
  </div>
</div>

<!-- Detail panels (expand inline below tiles — zero clicks to a new page) -->
<div class="detail-panel" id="dp-benefits"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('benefits')">&times;</button>
  <h3>Benefits & Insurance</h3>
  <p>DSA members and their families have access to comprehensive coverage negotiated at competitive group rates:</p>
  <ul>
    <li><strong>Medical:</strong> Multiple plan options through leading providers with low copays and broad network access across San Diego County.</li>
    <li><strong>Dental:</strong> Delta Dental PPO and Premier plans. Preventive care covered at 100%; major services at 50-80%.</li>
    <li><strong>Vision:</strong> VSP coverage for annual exams, frames, lenses, and contacts with low out-of-pocket costs.</li>
    <li><strong>Life & Disability:</strong> Group term life insurance and short/long-term disability coverage included with membership.</li>
    <li><strong>Supplemental:</strong> Optional additional life insurance, accident insurance, and critical illness policies available.</li>
  </ul>
  <p>Open enrollment is announced annually. Coverage changes can also be made during qualifying life events.</p>
  <div class="dp-contact">Questions? Call (858) 486-9009 or email benefits@dsasd.org</div>
</div></div>

<div class="detail-panel" id="dp-legal"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('legal')">&times;</button>
  <h3>Legal Defense Fund</h3>
  <p>The DSA Legal Defense Fund provides critical support when you need it most:</p>
  <ul>
    <li><strong>Administrative Investigations:</strong> Full representation during IA interviews and Skelly hearings.</li>
    <li><strong>Critical Incidents:</strong> Immediate attorney response 24/7 for officer-involved shootings, use-of-force incidents, and in-custody deaths.</li>
    <li><strong>Civil Litigation:</strong> Defense against lawsuits arising from the performance of your duties.</li>
    <li><strong>Weingarten Rights:</strong> Your right to union representation at any investigatory interview that could lead to discipline.</li>
    <li><strong>Coverage:</strong> Attorney fees, expert witnesses, court costs, and related expenses.</li>
  </ul>
  <div class="dp-contact">24/7 Legal Hotline: (858) 486-9009 &mdash; Call immediately if involved in a critical incident</div>
</div></div>

<div class="detail-panel" id="dp-wellness"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('wellness')">&times;</button>
  <h3>Wellness & Peer Support</h3>
  <p>Your well-being matters. All services are <strong>completely confidential</strong>:</p>
  <ul>
    <li><strong>Peer Support Team:</strong> Trained deputy counselors available for confidential conversations.</li>
    <li><strong>CISM Team:</strong> Critical Incident Stress Management debriefings after traumatic events.</li>
    <li><strong>Mental Health Referrals:</strong> Licensed therapists experienced with law enforcement issues.</li>
    <li><strong>Fitness Partnerships:</strong> Gym discounts and fitness facility access across San Diego County.</li>
    <li><strong>Wellness Workshops:</strong> Regular stress management, sleep health, and resilience seminars.</li>
    <li><strong>Family Support:</strong> Resources for spouses and families of law enforcement personnel.</li>
    <li><strong>Substance Abuse:</strong> Confidential counseling and treatment referrals.</li>
  </ul>
  <div class="dp-contact">Wellness Coordinator: (858) 486-9009 ext. 3 &mdash; All inquiries are 100% confidential</div>
</div></div>

<div class="detail-panel" id="dp-forms"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('forms')">&times;</button>
  <h3>Forms & Documents</h3>
  <p>Access important DSA documents and forms:</p>
  <ul>
    <li><strong>Membership Enrollment Form</strong> &mdash; New member registration and payroll deduction authorization</li>
    <li><strong>Beneficiary Designation Form</strong> &mdash; Life insurance beneficiary updates</li>
    <li><strong>Grievance Filing Form</strong> &mdash; Formal grievance submission per the MOU</li>
    <li><strong>Current MOU (Memorandum of Understanding)</strong> &mdash; Full contract with the County of San Diego</li>
    <li><strong>Board Meeting Minutes</strong> &mdash; Monthly meeting records and motions</li>
    <li><strong>Insurance Plan Summaries</strong> &mdash; Coverage details for medical, dental, and vision</li>
    <li><strong>Retirement Planning Guide</strong> &mdash; SDCERA pension information for deputies</li>
  </ul>
  <div class="dp-contact">Request forms: info@dsasd.org or visit DSA HQ at 13881 Danielson St, Poway</div>
</div></div>

<div class="detail-panel" id="dp-newsletters"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('newsletters')">&times;</button>
  <h3>Newsletters & Publications</h3>
  <div style="margin-bottom:16px;border-radius:10px;overflow:hidden"><img src="{{ site.baseurl }}/images/dsa/silver-star-newsletter.jpg" alt="Silver Star Newsletter" style="width:100%;max-height:180px;object-fit:cover;display:block"></div>
  <p>Stay informed with DSA communications:</p>
  <ul>
    <li><strong>Monthly Newsletter:</strong> DSA updates, member spotlights, benefit reminders, and legislative news.</li>
    <li><strong>Board Meeting Minutes:</strong> Official records from monthly Board of Directors meetings.</li>
    <li><strong>Annual Report:</strong> Year-in-review of DSA activities, financials, and accomplishments.</li>
    <li><strong>Legislative Updates:</strong> Alerts on bills and policies affecting law enforcement in California.</li>
  </ul>
  <div class="dp-contact">Subscribe to email updates: info@dsasd.org</div>
</div></div>

<div class="detail-panel" id="dp-pac"><div class="dp-card">
  <button class="dp-close" onclick="closeDetail('pac')">&times;</button>
  <h3>Political Action Committee</h3>
  <p>The DSA PAC advocates for the interests of San Diego County deputies:</p>
  <ul>
    <li><strong>Candidate Endorsements:</strong> Research-based endorsements for local, state, and federal elections that support law enforcement.</li>
    <li><strong>Legislative Advocacy:</strong> Lobbying on bills affecting deputy working conditions, retirement, and safety.</li>
    <li><strong>Voter Guides:</strong> Published before each election with DSA-endorsed candidates and ballot measures.</li>
    <li><strong>PAC Contributions:</strong> Voluntary member contributions support political activities.</li>
  </ul>
  <div class="dp-contact">PAC inquiries: pac@dsasd.org</div>
</div></div>

<!-- NEWS -->
<div class="section" id="news">
  <div class="sec-head"><h2>Latest News</h2></div>
  <div class="news-grid">
    <div class="news-card"><div class="img-card"><img src="{{ site.baseurl }}/images/dsa/board-portrait.png" alt="DSA Board Member"></div><span class="news-tag t-ann">Announcement</span><h3>2026 Contract Negotiations Update</h3><p>The DSA bargaining team has reached a tentative agreement with the county on wages, benefits, and working conditions for the next three years.</p><div class="news-date">March 15, 2026</div></div>
    <div class="news-card"><div class="img-card"><img src="{{ site.baseurl }}/images/dsa/golf-tournament-photo.png" alt="DSA Golf Tournament"></div><span class="news-tag t-evt">Event</span><h3>Annual DSA Family Picnic</h3><p>Join us at Poway Community Park on April 12th. Food, games, and fellowship for all DSA members and families.</p><div class="news-date">March 10, 2026</div></div>
    <div class="news-card"><div class="img-card"><img src="{{ site.baseurl }}/images/dsa/silver-star-newsletter.jpg" alt="Silver Star Newsletter"></div><span class="news-tag t-ben">Benefit</span><h3>New Dental Plan Options</h3><p>Expanded Delta Dental coverage now available. Open enrollment begins April 1st with improved major services rates.</p><div class="news-date">March 5, 2026</div></div>
  </div>
</div>

<!-- EVENTS -->
<div class="section" id="events">
  <div class="sec-head"><h2>Upcoming Events</h2></div>
  <div class="ev-list">
    <div class="ev"><div class="ev-date"><div class="m">APR</div><div class="d">02</div></div><div class="ev-info"><h4>Board of Directors Meeting</h4><p>DSA Headquarters, Poway &mdash; 6:00 PM</p></div><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
    <div class="ev"><div class="ev-date"><div class="m">APR</div><div class="d">12</div></div><div class="ev-info"><h4>Annual Family Picnic</h4><p>Poway Community Park &mdash; 11:00 AM</p></div><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
    <div class="ev"><div class="ev-date"><div class="m">APR</div><div class="d">18</div></div><div class="ev-info"><h4>Wellness Workshop: Stress Management</h4><p>Virtual Event &mdash; 2:00 PM</p></div><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
    <div class="ev"><div class="ev-date"><div class="m">MAY</div><div class="d">01</div></div><div class="ev-info"><h4>Deputy of the Year Awards</h4><p>Hilton San Diego &mdash; 7:00 PM</p></div><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
    <div class="ev"><div class="ev-date"><div class="m">MAY</div><div class="d">15</div></div><div class="ev-info"><h4>Charity Golf Tournament</h4><p>Morgan Run Club & Resort &mdash; 8:00 AM</p></div><img src="{{ site.baseurl }}/images/dsa/golf-tournament-flyer.png" alt="Golf Tournament" style="width:48px;height:48px;border-radius:8px;object-fit:cover;margin-left:auto;margin-right:8px;flex-shrink:0"><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
    <div class="ev"><div class="ev-date"><div class="m">MAY</div><div class="d">22</div></div><div class="ev-info"><h4>Law Enforcement Memorial</h4><p>County Admin Center &mdash; 10:00 AM</p></div><img src="{{ site.baseurl }}/images/dsa/memorial-line-of-duty.png" alt="Line of Duty Memorial" style="width:48px;height:48px;border-radius:8px;object-fit:cover;margin-left:auto;margin-right:8px;flex-shrink:0"><button class="ev-rsvp" onclick="rsvp(this)">RSVP</button></div>
  </div>
</div>

<!-- ABOUT -->
<div class="section" id="about">
  <div class="sec-head"><h2>About the DSA</h2></div>
  <div class="about-grid">
    <div class="about-card">
      <div class="img-card"><img src="{{ site.baseurl }}/images/dsa/dsa-logo.png" alt="DSA Logo" style="height:170px;object-fit:contain;background:#e8ecf0;padding:20px"></div>
      <h3>Our Mission</h3>
      <p>The Deputy Sheriffs' Association of San Diego County is the labor union representing all sworn personnel of the San Diego County Sheriff's Department. Founded in 1955, we negotiate contracts, provide legal defense, support political action, and deliver member benefits and wellness programs for over 4,229 members.</p>
      <p style="margin-top:10px">As the exclusive collective bargaining unit, the DSA negotiates Memoranda of Understanding (MOUs) covering wages, benefits, working conditions, overtime, and retirement with the County of San Diego.</p>
    </div>
    <div class="about-card">
      <h3>Stations We Cover</h3>
      <ul>
        <li>San Diego Central</li><li>Vista</li><li>Encinitas</li><li>Fallbrook</li>
        <li>Imperial Beach</li><li>Lemon Grove</li><li>Pine Valley</li><li>Rancho San Diego</li>
        <li>San Marcos</li><li>Santee</li><li>4S Ranch</li><li>Court Services</li>
        <li>Detention Facilities (Vista, Central, East Mesa, George Bailey, Las Colinas)</li>
      </ul>
    </div>
    <div class="about-card">
      <div class="img-card"><img src="{{ site.baseurl }}/images/dsa/board-portrait.png" alt="DSA Board Member"></div>
      <h3>Leadership</h3>
      <p>The DSA is governed by a Board of Directors elected by the membership. The Board meets monthly at DSA Headquarters in Poway to review operations, approve expenditures, and set policy direction.</p>
      <p style="margin-top:8px">Shop stewards are assigned to each station and facility to provide frontline union representation and ensure contract compliance.</p>
    </div>
    <div class="about-card">
      <div class="img-card"><img src="{{ site.baseurl }}/images/dsa/memorial-line-of-duty.png" alt="Line of Duty Memorial"></div>
      <h3>History</h3>
      <p>Since 1955, the DSA has grown from a small association of deputies to one of the largest law enforcement labor organizations in California. Key milestones include establishing the Legal Defense Fund, negotiating landmark contracts, and expanding wellness and peer support services.</p>
    </div>
  </div>
</div>

<!-- STORE -->
<div class="section" id="store">
  <div class="sec-head"><h2>DSA Store</h2><p>Official merchandise &mdash; member discounts applied automatically</p></div>
  <div class="store-hero"><img src="{{ site.baseurl }}/images/dsa/store-interior.jpg" alt="DSA Store Interior"></div>
  <div class="store-grid">
    <div class="store-item"><div class="si-icon">&#128085;</div><h4>Polo Shirt</h4><p>Embroidered DSA logo</p><div class="price">$35</div></div>
    <div class="store-item"><div class="si-icon">&#129506;</div><h4>Baseball Cap</h4><p>Adjustable, navy blue</p><div class="price">$22</div></div>
    <div class="store-item"><div class="si-icon">&#129689;</div><h4>Challenge Coin</h4><p>Collector's edition</p><div class="price">$15</div></div>
    <div class="store-item"><div class="si-icon">&#128188;</div><h4>Duffel Bag</h4><p>DSA branded, heavy duty</p><div class="price">$45</div></div>
    <div class="store-item"><div class="si-icon">&#9749;</div><h4>Travel Mug</h4><p>Stainless, 16oz</p><div class="price">$18</div></div>
    <div class="store-item"><div class="si-icon">&#128737;</div><h4>Lapel Pin</h4><p>Gold DSA shield</p><div class="price">$12</div></div>
    <div class="store-item"><div class="si-icon">&#127939;</div><h4>Workout Tee</h4><p>Moisture-wicking</p><div class="price">$28</div></div>
    <div class="store-item"><div class="si-icon">&#128218;</div><h4>Patch Set</h4><p>Velcro-backed, set of 3</p><div class="price">$20</div></div>
  </div>
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:20px">
    <div style="border-radius:10px;overflow:hidden"><img src="{{ site.baseurl }}/images/dsa/store-relaunch-flyer.png" alt="DSA Store Relaunch" style="width:100%;height:180px;object-fit:cover;display:block"></div>
    <div style="border-radius:10px;overflow:hidden"><img src="{{ site.baseurl }}/images/dsa/store-uniforms.jpg" alt="DSA Uniforms" style="width:100%;height:180px;object-fit:cover;display:block"></div>
  </div>
  <p style="text-align:center;margin-top:16px;color:#475569;font-size:0.8rem">Also available at DSA HQ, 13881 Danielson St, Poway &mdash; Online orders ship within 5-7 business days</p>
</div>

<!-- FAQ -->
<div class="section" id="faq">
  <div class="sec-head"><h2>Frequently Asked Questions</h2><p>Search below or ask the AI chatbot (bottom right)</p></div>
  <div class="faq-wrap">
    <div class="faq-bar">
      <input type="text" placeholder="Search FAQs..." id="faqSearch">
      <div class="faq-tag on" data-c="all">All</div>
      <div class="faq-tag" data-c="membership">Membership</div>
      <div class="faq-tag" data-c="benefits">Benefits</div>
      <div class="faq-tag" data-c="legal">Legal</div>
      <div class="faq-tag" data-c="events">Events</div>
      <div class="faq-tag" data-c="store">Store</div>
    </div>
    <div id="faqList">
      <div class="fq" data-c="membership"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>How do I become a DSA member?</span><span class="t">+</span></div><div class="fq-a">All sworn personnel of the San Diego County Sheriff's Department are eligible. Contact the DSA office at (858) 486-9009 or visit headquarters at 13881 Danielson Street, Poway. Dues are automatically deducted from your paycheck and benefits begin immediately.</div></div>
      <div class="fq" data-c="membership"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>What do membership dues cover?</span><span class="t">+</span></div><div class="fq-a">Dues cover legal defense, political representation, member benefits, organizational operations, and access to all DSA programs. Rates are set by the Board of Directors. Contact the office for current rates.</div></div>
      <div class="fq" data-c="membership"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>What are Weingarten Rights?</span><span class="t">+</span></div><div class="fq-a">You have the right to request union representation at any investigatory interview that could lead to discipline. If management denies your request, the interview must stop. Contact a shop steward or the DSA office immediately.</div></div>
      <div class="fq" data-c="benefits"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>What insurance benefits are available?</span><span class="t">+</span></div><div class="fq-a">Members have access to group health insurance (medical, dental, vision), life insurance, disability insurance, and supplemental coverage. We negotiate competitive rates with major providers. Coverage extends to you and your family.</div></div>
      <div class="fq" data-c="benefits"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>When is open enrollment?</span><span class="t">+</span></div><div class="fq-a">Open enrollment is announced annually, typically in the fall. You can also make changes during qualifying life events such as marriage, birth of a child, or change in spouse's coverage.</div></div>
      <div class="fq" data-c="legal"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>What legal defense does DSA provide?</span><span class="t">+</span></div><div class="fq-a">The Legal Defense Fund covers administrative investigations, IA interviews, Skelly hearings, critical incidents (24/7 response), and civil litigation from on-duty actions. Attorney fees, expert witnesses, and court costs are covered.</div></div>
      <div class="fq" data-c="legal"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>What should I do after a critical incident?</span><span class="t">+</span></div><div class="fq-a">Call the DSA 24/7 legal hotline at (858) 486-9009 immediately. Do not give a detailed statement until your attorney arrives. You have the right to representation. The CISM team is also available for post-incident support.</div></div>
      <div class="fq" data-c="events"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>How do I RSVP for events?</span><span class="t">+</span></div><div class="fq-a">Click the RSVP button next to any event on this page, call the office, or email info@dsasd.org. Most events are open to members and their immediate families.</div></div>
      <div class="fq" data-c="store"><div class="fq-q" onclick="toggleFaqAnswer(this)"><span>How do I buy DSA merchandise?</span><span class="t">+</span></div><div class="fq-a">Browse the Store section above or visit DSA HQ in Poway. Online orders ship within 5-7 business days. Member discounts are applied automatically at checkout.</div></div>
    </div>
  </div>
</div>

<!-- CONTACT -->
<div class="section" id="contact">
  <div class="sec-head"><h2>Contact Us</h2></div>
  <div style="display:flex;gap:16px;justify-content:center;margin-bottom:24px;flex-wrap:wrap">
    <div style="text-align:center"><img src="{{ site.baseurl }}/images/dsa/staff-photo-1.png" alt="DSA Staff" style="width:80px;height:80px;border-radius:50%;object-fit:cover;border:2px solid #fbbf24"><p style="font-size:0.72rem;color:#94a3b8;margin-top:4px">DSA Staff</p></div>
    <div style="text-align:center"><img src="{{ site.baseurl }}/images/dsa/staff-photo-2.png" alt="DSA Staff" style="width:80px;height:80px;border-radius:50%;object-fit:cover;border:2px solid #fbbf24"><p style="font-size:0.72rem;color:#94a3b8;margin-top:4px">DSA Staff</p></div>
    <div style="text-align:center"><img src="{{ site.baseurl }}/images/dsa/board-portrait.png" alt="Board Member" style="width:80px;height:80px;border-radius:50%;object-fit:cover;border:2px solid #fbbf24"><p style="font-size:0.72rem;color:#94a3b8;margin-top:4px">Board Member</p></div>
  </div>
  <div class="contact-row">
    <div class="c-card"><div class="c-icon">&#128205;</div><h4>Visit Us</h4><p>13881 Danielson Street<br>Poway, CA 92064</p><p style="margin-top:6px;font-size:0.75rem;color:#475569">Mon-Fri 8:00 AM - 5:00 PM</p></div>
    <div class="c-card"><div class="c-icon">&#128222;</div><h4>Call Us</h4><p><a href="tel:+18584869009">(858) 486-9009</a></p><p style="margin-top:4px;font-size:0.75rem;color:#475569">24/7 Legal Hotline available</p></div>
    <div class="c-card"><div class="c-icon">&#128231;</div><h4>Email Us</h4><p><a href="mailto:info@dsasd.org">info@dsasd.org</a></p><p style="margin-top:4px"><a href="mailto:benefits@dsasd.org" style="font-size:0.78rem">benefits@dsasd.org</a></p></div>
  </div>
</div>

<!-- ADMIN -->
<div class="section admin-section" id="adminSection">
  <div class="sec-head"><h2>All Registered Members</h2></div>
  <table class="a-table"><thead><tr><th>Name</th><th>Username</th><th>Badge</th><th>Rank</th><th>Station</th><th>Email</th><th>Status</th></tr></thead><tbody id="adminBody"></tbody></table>
</div>

<!-- FOOTER -->
<footer>
  <div class="ft-inner">
    <div class="ft-col"><div style="display:flex;align-items:center;gap:12px;margin-bottom:10px"><img src="{{ site.baseurl }}/images/dsa/dsa-logo.png" alt="DSA" style="width:50px;height:auto;opacity:0.8"><h4 style="margin:0">Deputy Sheriffs' Association</h4></div><p>13881 Danielson Street, Poway, CA 92064</p><p>(858) 486-9009 &middot; info@dsasd.org</p><p style="margin-top:8px;color:#1e3352">&copy; 2026 DSA San Diego County</p></div>
    <div class="ft-col"><h4>Navigate</h4><a href="#dashboard">Resources</a><a href="#news">News</a><a href="#events">Events</a><a href="#store">Store</a><a href="#faq">FAQ</a></div>
    <div class="ft-col"><h4>Support</h4><a href="#contact">Contact</a><a href="javascript:void(0)" onclick="openDetail('legal')">Legal Defense</a><a href="javascript:void(0)" onclick="openDetail('wellness')">Wellness</a><a href="javascript:void(0)" onclick="openDetail('forms')">Forms</a></div>
  </div>
</footer>

<!-- CHATBOT -->
<button class="cb-trigger" onclick="document.getElementById('cbWin').classList.toggle('open')">&#128172;</button>
<div class="cb-win" id="cbWin">
  <div class="cb-head"><h3>DSA Assistant (AI)</h3><button class="cb-x" onclick="document.getElementById('cbWin').classList.remove('open')">&times;</button></div>
  <div class="cb-msgs" id="cbMsgs"><div class="cm bot"><div class="cb">Hi! I'm the DSA FAQ Assistant powered by AI. Ask me anything about membership, benefits, legal defense, events, or the store.</div></div></div>
  <div class="cb-input"><input id="cbIn" placeholder="Ask a question..." onkeydown="if(event.key==='Enter')sendChat()"><button id="cbSend" onclick="sendChat()">Send</button></div>
</div>

<!-- LOGIN MODAL -->
<div class="modal-bg" id="modalBg">
  <div class="modal">
    <button class="modal-x" onclick="closeModal()">&times;</button>
    <h2 id="mTitle">Member Login</h2>
    <p class="sub" id="mSub">Access your DSA portal</p>
    <div class="mtabs"><div class="mtab on" id="tLog" onclick="mTab('login')">Log In</div><div class="mtab" id="tSign" onclick="mTab('signup')">Sign Up</div></div>
    <form id="fLogin" onsubmit="doLogin(event)">
      <div class="fg"><label>Username</label><input id="lUid" placeholder="Enter username" required></div>
      <div class="fg"><label>Password</label><input type="password" id="lPw" placeholder="Enter password" required></div>
      <button type="submit" class="modal-submit">Log In</button>
      <p class="modal-err" id="lErr"></p>
    </form>
    <form id="fSign" onsubmit="doSignup(event)" style="display:none">
      <div class="fg"><label>Full Name</label><input id="sName" placeholder="John Smith" required></div>
      <div class="fg"><label>Username</label><input id="sUid" placeholder="Choose a username" required></div>
      <div class="fg"><label>Badge / Sheriff ID</label><input id="sSid" placeholder="SD-1234" required></div>
      <div class="fg"><label>Email</label><input type="email" id="sEmail" placeholder="your@email.com"></div>
      <div class="fg"><label>Rank</label><select id="sRank"><option>Deputy</option><option>Corporal</option><option>Sergeant</option><option>Lieutenant</option><option>Captain</option></select></div>
      <div class="fg"><label>Station</label><select id="sStation"><option>San Diego Central</option><option>Vista Station</option><option>Encinitas Station</option><option>Fallbrook Station</option><option>Imperial Beach Station</option><option>Lemon Grove Station</option><option>Pine Valley Station</option><option>Rancho San Diego Station</option><option>San Marcos Station</option><option>Santee Station</option><option>4S Ranch Station</option><option>DSA Headquarters - Poway</option></select></div>
      <div class="fg"><label>Phone</label><input type="tel" id="sPhone" placeholder="(xxx) xxx-xxxx"></div>
      <div class="fg"><label>Password (min 8 chars)</label><input type="password" id="sPw" placeholder="Create password" required minlength="8"></div>
      <button type="submit" class="modal-submit">Create Account</button>
      <p class="modal-err" id="sErr"></p>
    </form>
  </div>
</div>

<script>
/* ================================================================
   CONFIG — single source for API base URL
   ================================================================ */
const API = (location.hostname === 'localhost' || location.hostname === '127.0.0.1')
  ? 'http://localhost:8587'
  : 'https://flask.opencodingsociety.com';

let user = null;

/* ================================================================
   DOM HELPERS — each does exactly one thing
   ================================================================ */

/** Scroll the viewport to the element matching `sel`. */
function scrollTo(sel) {
  document.querySelector(sel)?.scrollIntoView({ behavior: 'smooth' });
}

/** Return a DOM element by id (shorthand). */
function el(id) { return document.getElementById(id); }

/** Show an error message inside a `.modal-err` element. */
function showError(elementId, message) {
  const err = el(elementId);
  err.textContent = message;
  err.style.display = 'block';
}

/** Hide an error message element. */
function hideError(elementId) {
  el(elementId).style.display = 'none';
}

/** Sanitize a string for safe HTML insertion. */
function sanitizeHTML(text) {
  return text
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/\n/g, '<br>');
}

/** Make a JSON POST/PUT/DELETE request to the API. */
function apiRequest(path, method, body) {
  const opts = { method, credentials: 'include', headers: { 'Content-Type': 'application/json' } };
  if (body) opts.body = JSON.stringify(body);
  return fetch(`${API}${path}`, opts).then(r => {
    if (!r.ok) return r.json().then(d => { throw new Error(d.message || d.error || 'Request failed'); });
    return r.json();
  });
}

/* ================================================================
   DETAIL PANELS — open / close inline resource panels
   ================================================================ */

function closeAllDetailPanels() {
  document.querySelectorAll('.detail-panel').forEach(p => p.classList.remove('open'));
}

function openDetail(id) {
  closeAllDetailPanels();
  const panel = el('dp-' + id);
  if (panel) {
    panel.classList.add('open');
    panel.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
  }
}

function closeDetail(id) {
  el('dp-' + id)?.classList.remove('open');
}

/* ================================================================
   RSVP — mark an event button as RSVP'd
   ================================================================ */

function rsvp(btn) {
  btn.textContent = '\u2713 RSVP\'d';
  btn.classList.add('done');
}

/* ================================================================
   FAQ — toggle answers and filter by category / search
   ================================================================ */

function toggleFaqAnswer(questionEl) {
  questionEl.classList.toggle('open');
  questionEl.nextElementSibling.classList.toggle('open');
}

function filterFaqByCategory(category) {
  document.querySelectorAll('.fq').forEach(f => {
    f.style.display = (category === 'all' || f.dataset.c === category) ? '' : 'none';
  });
}

function filterFaqBySearch(query) {
  const q = query.toLowerCase();
  document.querySelectorAll('.fq').forEach(f => {
    f.style.display = f.textContent.toLowerCase().includes(q) ? '' : 'none';
  });
}

function setActiveFaqTag(activeTag) {
  document.querySelectorAll('.faq-tag').forEach(x => x.classList.remove('on'));
  activeTag.classList.add('on');
}

document.querySelectorAll('.faq-tag').forEach(t => t.addEventListener('click', function() {
  setActiveFaqTag(this);
  filterFaqByCategory(this.dataset.c);
}));

el('faqSearch').addEventListener('input', function() {
  filterFaqBySearch(this.value);
});

/* ================================================================
   SEARCH — autocomplete dropdown that scrolls to sections
   ================================================================ */

const searchMap = [
  { label: 'Benefits & Insurance', target: '#dashboard', detail: 'benefits' },
  { label: 'Legal Defense',        target: '#dashboard', detail: 'legal' },
  { label: 'Wellness Programs',    target: '#dashboard', detail: 'wellness' },
  { label: 'Forms & Documents',    target: '#dashboard', detail: 'forms' },
  { label: 'Newsletters',          target: '#dashboard', detail: 'newsletters' },
  { label: 'Political Action',     target: '#dashboard', detail: 'pac' },
  { label: 'Events Calendar',      target: '#events' },
  { label: 'DSA Store',            target: '#store' },
  { label: 'FAQ',                  target: '#faq' },
  { label: 'Contact Us',           target: '#contact' },
  { label: 'About DSA',            target: '#about' },
  { label: 'Latest News',          target: '#news' },
  { label: 'Membership',           target: '#faq' },
];

function findSearchMatches(query) {
  return searchMap.filter(s => s.label.toLowerCase().includes(query.toLowerCase()));
}

function renderSearchDropdown(hits, dropdown) {
  dropdown.innerHTML = hits.map(h =>
    `<div class="search-item" data-target="${h.target}" data-detail="${h.detail || ''}">${h.label}</div>`
  ).join('');
}

function handleSearchItemClick(item, dropdown) {
  scrollTo(item.dataset.target);
  if (item.dataset.detail) setTimeout(() => openDetail(item.dataset.detail), 400);
  dropdown.classList.remove('open');
  el('searchInput').value = '';
}

el('searchInput').addEventListener('input', function() {
  const q = this.value.trim(), drop = el('searchDrop');
  if (q.length < 2) { drop.classList.remove('open'); return; }
  const hits = findSearchMatches(q);
  if (!hits.length) { drop.classList.remove('open'); return; }
  renderSearchDropdown(hits, drop);
  drop.classList.add('open');
  drop.querySelectorAll('.search-item').forEach(it =>
    it.addEventListener('click', function() { handleSearchItemClick(this, drop); })
  );
});

/* ================================================================
   CLICK-AWAY — close dropdowns when clicking outside
   ================================================================ */

function closeDropdownsOnClickAway(e) {
  if (!e.target.closest('.search-box')) el('searchDrop').classList.remove('open');
  if (!e.target.closest('.user-area')) el('userPanel')?.classList.remove('open');
}

document.addEventListener('click', closeDropdownsOnClickAway);

/* ================================================================
   NAV HIGHLIGHT — highlight the active nav link on scroll
   ================================================================ */

const sectionIds = ['dashboard', 'news', 'events', 'about', 'store', 'faq', 'contact'];

function getActiveSection() {
  const y = window.scrollY + 120;
  let active = '';
  sectionIds.forEach(s => {
    const section = el(s);
    if (section && section.offsetTop <= y) active = s;
  });
  return active;
}

function highlightActiveNavLink() {
  const active = getActiveSection();
  document.querySelectorAll('.nav-link').forEach(l => {
    l.classList.toggle('active', l.getAttribute('onclick')?.includes(active));
  });
}

window.addEventListener('scroll', highlightActiveNavLink);

/* ================================================================
   MODAL — open / close / tab switching for login/signup
   ================================================================ */

function openModal(tab) {
  el('modalBg').classList.add('open');
  switchModalTab(tab || 'login');
}

function closeModal() {
  el('modalBg').classList.remove('open');
  hideError('lErr');
  hideError('sErr');
}

function switchModalTab(t) {
  const isLogin = (t === 'login');
  el('tLog').classList.toggle('on', isLogin);
  el('tSign').classList.toggle('on', !isLogin);
  el('fLogin').style.display = isLogin ? 'block' : 'none';
  el('fSign').style.display = isLogin ? 'none' : 'block';
  el('mTitle').textContent = isLogin ? 'Member Login' : 'Create Account';
  el('mSub').textContent = isLogin ? 'Access your DSA portal' : 'Register as a DSA member';
}

// kept as global alias so onclick="mTab(...)" in HTML still works
function mTab(t) { switchModalTab(t); }

/* ================================================================
   AUTH — login, signup, logout, session check
   ================================================================ */

function getLoginCredentials() {
  return { uid: el('lUid').value, password: el('lPw').value };
}

function getSignupData() {
  return {
    name: el('sName').value, uid: el('sUid').value,
    sheriff_id: el('sSid').value, email: el('sEmail').value,
    rank: el('sRank').value, station: el('sStation').value,
    phone: el('sPhone').value, password: el('sPw').value,
  };
}

function doLogin(e) {
  e.preventDefault();
  apiRequest('/api/sheriff/authenticate', 'POST', getLoginCredentials())
    .then(d => { user = d.user; closeModal(); updateUI(); })
    .catch(err => showError('lErr', err.message));
}

function doSignup(e) {
  e.preventDefault();
  const body = getSignupData();
  apiRequest('/api/sheriff/user', 'POST', body)
    .then(() => { switchModalTab('login'); el('lUid').value = body.uid; alert('Account created! Please log in.'); })
    .catch(err => showError('sErr', err.message));
}

function logout() {
  apiRequest('/api/sheriff/authenticate', 'DELETE')
    .finally(() => { user = null; updateUI(); el('userPanel').classList.remove('open'); });
}

/* ================================================================
   UI STATE — update header to reflect logged-in / logged-out
   ================================================================ */

function showLoggedInUI() {
  el('authBtns').style.display = 'none';
  el('userArea').classList.add('active');
  el('uName').textContent = user.name.split(' ')[0];
  el('upName').textContent = user.name;
  el('upBadge').textContent = 'Badge: ' + user.sheriff_id;
  el('upRank').textContent = 'Rank: ' + user.rank;
  el('upStation').textContent = 'Station: ' + user.station;
  el('adminBtn').style.display = user.role === 'Admin' ? 'block' : 'none';
}

function showLoggedOutUI() {
  el('authBtns').style.display = 'flex';
  el('userArea').classList.remove('active');
  el('adminSection').classList.remove('open');
}

function updateUI() {
  user ? showLoggedInUI() : showLoggedOutUI();
}

/* ================================================================
   ADMIN PANEL — toggle and load member table
   ================================================================ */

function toggleAdmin() {
  const s = el('adminSection');
  s.classList.toggle('open');
  if (s.classList.contains('open')) loadAdmin();
  el('userPanel').classList.remove('open');
  if (s.classList.contains('open')) setTimeout(() => s.scrollIntoView({ behavior: 'smooth' }), 100);
}

function renderAdminRow(u) {
  return `<tr><td>${u.name}</td><td>${u.uid}</td><td>${u.sheriff_id}</td><td>${u.rank}</td><td>${u.station}</td><td>${u.email}</td><td><span class="badge-s badge-active">${u.status}</span></td></tr>`;
}

function loadAdmin() {
  fetch(`${API}/api/sheriff/user`, { credentials: 'include' })
    .then(r => r.json())
    .then(users => { el('adminBody').innerHTML = users.map(renderAdminRow).join(''); })
    .catch(e => console.error(e));
}

/* ================================================================
   CHATBOT — AI-powered DSA FAQ assistant
   ================================================================ */

let chatHist = [];

function getChatInput() {
  const inp = el('cbIn');
  const msg = inp.value.trim();
  inp.value = '';
  return msg;
}

function addChatMessage(text, sender) {
  const container = el('cbMsgs');
  const div = document.createElement('div');
  div.className = 'cm ' + sender;
  div.innerHTML = '<div class="cb">' + sanitizeHTML(text) + '</div>';
  container.appendChild(div);
  container.scrollTop = container.scrollHeight;
}

function showTypingIndicator() {
  const container = el('cbMsgs');
  const div = document.createElement('div');
  const id = 't' + Date.now();
  div.id = id;
  div.className = 'cm bot';
  div.innerHTML = '<div class="cb typing-dots"><span></span><span></span><span></span></div>';
  container.appendChild(div);
  container.scrollTop = container.scrollHeight;
  return id;
}

function removeTypingIndicator(id) {
  el(id)?.remove();
}

function disableChatSend() {
  const btn = el('cbSend');
  btn.disabled = true;
  btn.textContent = '...';
}

function enableChatSend() {
  const btn = el('cbSend');
  btn.disabled = false;
  btn.textContent = 'Send';
}

function sendChat() {
  const msg = getChatInput();
  if (!msg) return;

  addChatMessage(msg, 'user');
  chatHist.push({ role: 'user', content: msg });

  const typingId = showTypingIndicator();
  disableChatSend();

  apiRequest('/api/sheriff/chat', 'POST', { message: msg, history: chatHist.slice(-10) })
    .then(d => {
      removeTypingIndicator(typingId);
      addChatMessage(d.reply, 'bot');
      chatHist.push({ role: 'assistant', content: d.reply });
    })
    .catch(() => {
      removeTypingIndicator(typingId);
      addChatMessage("Sorry, I can't connect right now. Call (858) 486-9009 or email info@dsasd.org.", 'bot');
    })
    .finally(enableChatSend);
}

/* ================================================================
   INIT — check auth session on page load
   ================================================================ */

function checkExistingSession() {
  fetch(`${API}/api/sheriff/id`, { credentials: 'include' })
    .then(r => { if (!r.ok) throw 0; return r.json(); })
    .then(d => { user = d; updateUI(); })
    .catch(() => {});
}

checkExistingSession();
</script>
</body>
</html>
