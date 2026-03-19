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
    /* ===== RESET & BASE ===== */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      background: #0a1628;
      color: #e2e8f0;
      line-height: 1.6;
      overflow-x: hidden;
    }
    a { color: #60a5fa; text-decoration: none; transition: color 0.2s; }
    a:hover { color: #93c5fd; }

    /* ===== TOP BAR ===== */
    .top-bar {
      background: #1a2744;
      padding: 6px 20px;
      font-size: 0.8rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #2a3a5c;
    }
    .top-bar-left span { margin-right: 20px; color: #94a3b8; }
    .top-bar-right a { margin-left: 15px; color: #94a3b8; }
    .top-bar-right a:hover { color: #fbbf24; }

    /* ===== HEADER / MEGA NAV ===== */
    .main-header {
      background: linear-gradient(135deg, #1e3a5f 0%, #0f2847 100%);
      position: sticky;
      top: 0;
      z-index: 1000;
      box-shadow: 0 2px 20px rgba(0,0,0,0.3);
    }
    .header-inner {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 20px;
      height: 70px;
    }
    .logo {
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .logo-badge {
      width: 45px;
      height: 45px;
      background: linear-gradient(135deg, #fbbf24, #f59e0b);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.4rem;
      font-weight: 800;
      color: #1e3a5f;
    }
    .logo-text h1 { font-size: 1.1rem; color: #fff; font-weight: 700; letter-spacing: 0.5px; }
    .logo-text span { font-size: 0.7rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 1px; }

    /* Nav menu */
    .nav-menu { display: flex; gap: 0; height: 100%; align-items: stretch; }
    .nav-item {
      position: relative;
      padding: 0 18px;
      display: flex;
      align-items: center;
      cursor: pointer;
      color: #cbd5e1;
      font-size: 0.9rem;
      font-weight: 500;
      transition: all 0.2s;
      height: 100%;
    }
    .nav-item:hover { color: #fbbf24; background: rgba(251,191,36,0.08); }
    .nav-item .arrow { font-size: 0.6rem; margin-left: 5px; transition: transform 0.2s; }
    .nav-item:hover .arrow { transform: rotate(180deg); }

    /* Mega dropdown */
    .mega-dropdown {
      display: none;
      position: absolute;
      top: 100%;
      left: 50%;
      transform: translateX(-50%);
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 0 0 12px 12px;
      padding: 20px;
      min-width: 300px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.4);
      z-index: 999;
    }
    .nav-item:hover .mega-dropdown { display: block; }
    .mega-link {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 12px;
      border-radius: 8px;
      transition: background 0.2s;
      color: #cbd5e1;
    }
    .mega-link:hover { background: rgba(96,165,250,0.1); color: #60a5fa; }
    .mega-icon { font-size: 1.2rem; width: 30px; text-align: center; }
    .mega-label { font-size: 0.85rem; }
    .mega-desc { font-size: 0.72rem; color: #64748b; }

    /* Search bar */
    .search-container {
      position: relative;
      width: 220px;
    }
    .search-input {
      width: 100%;
      padding: 8px 36px 8px 14px;
      background: rgba(255,255,255,0.08);
      border: 1px solid #2a3a5c;
      border-radius: 25px;
      color: #e2e8f0;
      font-size: 0.85rem;
      outline: none;
      transition: all 0.3s;
    }
    .search-input::placeholder { color: #64748b; }
    .search-input:focus { border-color: #60a5fa; background: rgba(255,255,255,0.12); box-shadow: 0 0 0 3px rgba(96,165,250,0.15); }
    .search-icon {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      color: #64748b;
      font-size: 0.9rem;
      pointer-events: none;
    }
    .search-results {
      display: none;
      position: absolute;
      top: calc(100% + 6px);
      left: 0;
      right: 0;
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 10px 30px rgba(0,0,0,0.4);
      z-index: 1001;
    }
    .search-results.active { display: block; }
    .search-result-item {
      padding: 10px 14px;
      cursor: pointer;
      font-size: 0.85rem;
      color: #cbd5e1;
      border-bottom: 1px solid #2a3a5c;
      transition: background 0.15s;
    }
    .search-result-item:hover { background: rgba(96,165,250,0.1); }
    .search-result-item:last-child { border-bottom: none; }

    /* Auth buttons */
    .auth-buttons { display: flex; gap: 10px; align-items: center; }
    .btn-login, .btn-signup {
      padding: 8px 18px;
      border-radius: 8px;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      border: none;
      transition: all 0.2s;
    }
    .btn-login { background: transparent; color: #fbbf24; border: 1px solid #fbbf24; }
    .btn-login:hover { background: rgba(251,191,36,0.1); }
    .btn-signup { background: linear-gradient(135deg, #f59e0b, #d97706); color: #1e3a5f; }
    .btn-signup:hover { transform: translateY(-1px); box-shadow: 0 4px 12px rgba(245,158,11,0.3); }

    /* User dropdown (shown when logged in) */
    .user-dropdown { position: relative; display: none; }
    .user-dropdown.active { display: block; }
    .user-btn {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 6px 14px;
      background: rgba(251,191,36,0.1);
      border: 1px solid #fbbf24;
      border-radius: 8px;
      color: #fbbf24;
      cursor: pointer;
      font-size: 0.85rem;
      font-weight: 600;
    }
    .user-menu {
      display: none;
      position: absolute;
      top: calc(100% + 8px);
      right: 0;
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 10px;
      min-width: 200px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.4);
      z-index: 1001;
      overflow: hidden;
    }
    .user-menu.active { display: block; }
    .user-menu-item {
      padding: 12px 16px;
      cursor: pointer;
      color: #cbd5e1;
      font-size: 0.85rem;
      border-bottom: 1px solid #2a3a5c;
      transition: background 0.15s;
    }
    .user-menu-item:hover { background: rgba(96,165,250,0.1); }
    .user-menu-item:last-child { border-bottom: none; }
    .user-menu-header {
      padding: 14px 16px;
      background: rgba(251,191,36,0.05);
      border-bottom: 1px solid #2a3a5c;
    }
    .user-menu-header .name { font-weight: 700; color: #fbbf24; font-size: 0.95rem; }
    .user-menu-header .badge { font-size: 0.75rem; color: #94a3b8; }

    /* Mobile menu */
    .mobile-toggle {
      display: none;
      font-size: 1.5rem;
      background: none;
      border: none;
      color: #fff;
      cursor: pointer;
    }

    /* ===== HERO ===== */
    .hero {
      background: linear-gradient(135deg, #0f2847 0%, #1e3a5f 50%, #0a1628 100%);
      padding: 80px 20px;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .hero::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: radial-gradient(circle at 30% 50%, rgba(251,191,36,0.04) 0%, transparent 50%),
                  radial-gradient(circle at 70% 50%, rgba(96,165,250,0.04) 0%, transparent 50%);
      animation: heroFloat 20s ease-in-out infinite;
    }
    @keyframes heroFloat { 0%, 100% { transform: translate(0, 0); } 50% { transform: translate(-20px, 10px); } }
    .hero-content { position: relative; z-index: 1; max-width: 800px; margin: 0 auto; }
    .hero h2 { font-size: 2.8rem; font-weight: 800; margin-bottom: 16px; background: linear-gradient(135deg, #fbbf24, #f59e0b); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    .hero p { font-size: 1.15rem; color: #94a3b8; margin-bottom: 30px; line-height: 1.7; }
    .hero-stats { display: flex; justify-content: center; gap: 50px; margin-top: 40px; }
    .hero-stat { text-align: center; }
    .hero-stat .number { font-size: 2.2rem; font-weight: 800; color: #fbbf24; }
    .hero-stat .label { font-size: 0.8rem; color: #64748b; text-transform: uppercase; letter-spacing: 1px; }

    /* ===== DASHBOARD TILES ===== */
    .section-title { text-align: center; margin: 60px 0 30px; font-size: 1.8rem; font-weight: 700; color: #fff; }
    .section-subtitle { text-align: center; color: #64748b; margin-top: -20px; margin-bottom: 30px; font-size: 0.95rem; }

    .dashboard { max-width: 1200px; margin: 0 auto; padding: 0 20px 40px; }
    .tiles { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
    .tile {
      background: linear-gradient(145deg, #1a2744, #15203a);
      border: 1px solid #2a3a5c;
      border-radius: 14px;
      padding: 24px;
      cursor: pointer;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
    }
    .tile::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(90deg, #fbbf24, #f59e0b);
      opacity: 0;
      transition: opacity 0.3s;
    }
    .tile:hover { transform: translateY(-4px); border-color: #fbbf24; box-shadow: 0 8px 30px rgba(251,191,36,0.1); }
    .tile:hover::after { opacity: 1; }
    .tile-icon { font-size: 2rem; margin-bottom: 12px; }
    .tile-title { font-weight: 700; font-size: 1.05rem; margin-bottom: 6px; color: #fff; }
    .tile-desc { font-size: 0.82rem; color: #64748b; }

    /* ===== NEWS FEED ===== */
    .news-section { max-width: 1200px; margin: 0 auto; padding: 0 20px 60px; }
    .news-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 20px; }
    .news-card {
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 14px;
      padding: 24px;
      transition: all 0.3s;
    }
    .news-card:hover { border-color: #3b82f6; }
    .news-tag {
      display: inline-block;
      padding: 3px 10px;
      border-radius: 20px;
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 10px;
    }
    .tag-announcement { background: rgba(251,191,36,0.15); color: #fbbf24; }
    .tag-event { background: rgba(96,165,250,0.15); color: #60a5fa; }
    .tag-benefit { background: rgba(52,211,153,0.15); color: #34d399; }
    .news-card h3 { font-size: 1.1rem; margin-bottom: 8px; color: #fff; }
    .news-card p { font-size: 0.85rem; color: #94a3b8; }
    .news-date { font-size: 0.75rem; color: #475569; margin-top: 10px; }

    /* ===== EVENTS CALENDAR ===== */
    .events-section { max-width: 1200px; margin: 0 auto; padding: 0 20px 60px; }
    .events-list { display: flex; flex-direction: column; gap: 12px; }
    .event-item {
      display: flex;
      align-items: center;
      gap: 16px;
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 12px;
      padding: 16px 20px;
      transition: border-color 0.2s;
    }
    .event-item:hover { border-color: #60a5fa; }
    .event-date-box {
      min-width: 55px;
      text-align: center;
      background: rgba(96,165,250,0.1);
      border-radius: 8px;
      padding: 8px;
    }
    .event-date-box .month { font-size: 0.65rem; text-transform: uppercase; color: #60a5fa; letter-spacing: 1px; }
    .event-date-box .day { font-size: 1.4rem; font-weight: 800; color: #fff; }
    .event-info h4 { font-size: 0.95rem; color: #fff; margin-bottom: 3px; }
    .event-info p { font-size: 0.8rem; color: #64748b; }
    .event-rsvp {
      margin-left: auto;
      padding: 6px 16px;
      background: rgba(96,165,250,0.15);
      border: 1px solid #3b82f6;
      border-radius: 6px;
      color: #60a5fa;
      font-size: 0.8rem;
      cursor: pointer;
      transition: all 0.2s;
    }
    .event-rsvp:hover { background: #3b82f6; color: #fff; }

    /* ===== FAQ SECTION ===== */
    .faq-section {
      max-width: 900px;
      margin: 0 auto;
      padding: 0 20px 60px;
    }
    .faq-search {
      width: 100%;
      padding: 14px 20px;
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 12px;
      color: #e2e8f0;
      font-size: 1rem;
      margin-bottom: 20px;
      outline: none;
      transition: border-color 0.3s;
    }
    .faq-search:focus { border-color: #60a5fa; }
    .faq-categories { display: flex; gap: 8px; margin-bottom: 20px; flex-wrap: wrap; }
    .faq-cat {
      padding: 6px 14px;
      border-radius: 20px;
      font-size: 0.8rem;
      background: rgba(255,255,255,0.05);
      border: 1px solid #2a3a5c;
      color: #94a3b8;
      cursor: pointer;
      transition: all 0.2s;
    }
    .faq-cat.active, .faq-cat:hover { background: rgba(251,191,36,0.15); border-color: #fbbf24; color: #fbbf24; }
    .faq-item {
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 10px;
      margin-bottom: 10px;
      overflow: hidden;
      transition: border-color 0.2s;
    }
    .faq-item:hover { border-color: #3b82f6; }
    .faq-question {
      padding: 16px 20px;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: 600;
      color: #e2e8f0;
      font-size: 0.95rem;
    }
    .faq-question .toggle { font-size: 1.2rem; transition: transform 0.3s; color: #fbbf24; }
    .faq-question.open .toggle { transform: rotate(45deg); }
    .faq-answer {
      display: none;
      padding: 0 20px 16px;
      font-size: 0.88rem;
      color: #94a3b8;
      line-height: 1.7;
    }
    .faq-answer.open { display: block; }

    /* ===== CHATBOT ===== */
    .chatbot-trigger {
      position: fixed;
      bottom: 24px;
      right: 24px;
      width: 60px;
      height: 60px;
      background: linear-gradient(135deg, #f59e0b, #d97706);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: 0 6px 25px rgba(245,158,11,0.4);
      z-index: 1100;
      transition: all 0.3s;
      border: none;
      font-size: 1.5rem;
    }
    .chatbot-trigger:hover { transform: scale(1.1); }
    .chatbot-window {
      display: none;
      position: fixed;
      bottom: 100px;
      right: 24px;
      width: 380px;
      max-height: 500px;
      background: #1a2744;
      border: 1px solid #2a3a5c;
      border-radius: 16px;
      z-index: 1100;
      box-shadow: 0 20px 60px rgba(0,0,0,0.5);
      flex-direction: column;
      overflow: hidden;
    }
    .chatbot-window.open { display: flex; }
    .chatbot-header {
      background: linear-gradient(135deg, #1e3a5f, #0f2847);
      padding: 16px 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #2a3a5c;
    }
    .chatbot-header h3 { color: #fbbf24; font-size: 1rem; }
    .chatbot-close { background: none; border: none; color: #94a3b8; font-size: 1.3rem; cursor: pointer; }
    .chatbot-messages {
      flex: 1;
      overflow-y: auto;
      padding: 16px;
      max-height: 340px;
    }
    .chat-msg {
      margin-bottom: 12px;
      display: flex;
    }
    .chat-msg.bot { justify-content: flex-start; }
    .chat-msg.user { justify-content: flex-end; }
    .chat-bubble {
      max-width: 80%;
      padding: 10px 14px;
      border-radius: 12px;
      font-size: 0.85rem;
      line-height: 1.5;
    }
    .chat-msg.bot .chat-bubble { background: #15203a; color: #cbd5e1; border-bottom-left-radius: 4px; }
    .chat-msg.user .chat-bubble { background: #3b82f6; color: #fff; border-bottom-right-radius: 4px; }
    .chatbot-input-area {
      display: flex;
      gap: 8px;
      padding: 12px 16px;
      border-top: 1px solid #2a3a5c;
      background: #15203a;
    }
    .chatbot-input {
      flex: 1;
      padding: 10px 14px;
      background: rgba(255,255,255,0.05);
      border: 1px solid #2a3a5c;
      border-radius: 8px;
      color: #e2e8f0;
      font-size: 0.85rem;
      outline: none;
    }
    .chatbot-send {
      padding: 10px 16px;
      background: #f59e0b;
      border: none;
      border-radius: 8px;
      color: #1e3a5f;
      font-weight: 700;
      cursor: pointer;
      transition: background 0.2s;
    }
    .chatbot-send:hover { background: #fbbf24; }

    /* ===== LOGIN MODAL ===== */
    .modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.7);
      z-index: 2000;
      align-items: center;
      justify-content: center;
    }
    .modal-overlay.active { display: flex; }
    .modal {
      background: linear-gradient(145deg, #1a2744, #15203a);
      border: 1px solid #2a3a5c;
      border-radius: 20px;
      padding: 40px;
      width: 100%;
      max-width: 440px;
      position: relative;
      box-shadow: 0 25px 60px rgba(0,0,0,0.5);
    }
    .modal-close {
      position: absolute;
      top: 16px;
      right: 20px;
      background: none;
      border: none;
      color: #64748b;
      font-size: 1.5rem;
      cursor: pointer;
    }
    .modal h2 { font-size: 1.6rem; color: #fbbf24; margin-bottom: 6px; }
    .modal .modal-subtitle { color: #64748b; font-size: 0.9rem; margin-bottom: 24px; }
    .modal-form .form-group { margin-bottom: 16px; }
    .modal-form label { display: block; font-size: 0.8rem; color: #94a3b8; margin-bottom: 5px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; }
    .modal-form input, .modal-form select {
      width: 100%;
      padding: 12px 14px;
      background: rgba(255,255,255,0.05);
      border: 1px solid #2a3a5c;
      border-radius: 10px;
      color: #e2e8f0;
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.3s;
    }
    .modal-form input:focus, .modal-form select:focus { border-color: #fbbf24; }
    .modal-form select option { background: #1a2744; color: #e2e8f0; }
    .modal-submit {
      width: 100%;
      padding: 14px;
      background: linear-gradient(135deg, #f59e0b, #d97706);
      border: none;
      border-radius: 10px;
      color: #1e3a5f;
      font-size: 1rem;
      font-weight: 700;
      cursor: pointer;
      margin-top: 8px;
      transition: all 0.2s;
    }
    .modal-submit:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(245,158,11,0.3); }
    .modal-error { color: #ef4444; font-size: 0.85rem; margin-top: 10px; display: none; }
    .modal-tabs { display: flex; gap: 0; margin-bottom: 24px; }
    .modal-tab {
      flex: 1;
      padding: 10px;
      text-align: center;
      cursor: pointer;
      font-weight: 600;
      font-size: 0.9rem;
      color: #64748b;
      border-bottom: 2px solid transparent;
      transition: all 0.2s;
    }
    .modal-tab.active { color: #fbbf24; border-bottom-color: #fbbf24; }

    /* ===== FOOTER ===== */
    .site-footer {
      background: #0d1b2a;
      border-top: 1px solid #1a2744;
      padding: 40px 20px;
      margin-top: 40px;
    }
    .footer-inner { max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 30px; }
    .footer-col h4 { color: #fbbf24; font-size: 0.9rem; margin-bottom: 14px; text-transform: uppercase; letter-spacing: 1px; }
    .footer-col p, .footer-col a { font-size: 0.85rem; color: #64748b; display: block; margin-bottom: 8px; }
    .footer-col a:hover { color: #fbbf24; }
    .footer-bottom { text-align: center; margin-top: 30px; padding-top: 20px; border-top: 1px solid #1a2744; color: #475569; font-size: 0.8rem; }

    /* ===== BACK BUTTON ===== */
    .back-to-main {
      position: fixed;
      top: 80px;
      left: 16px;
      padding: 8px 14px;
      background: rgba(96,165,250,0.15);
      border: 1px solid #3b82f6;
      border-radius: 8px;
      color: #60a5fa;
      font-size: 0.8rem;
      cursor: pointer;
      z-index: 999;
      transition: all 0.2s;
      text-decoration: none;
    }
    .back-to-main:hover { background: #3b82f6; color: #fff; }

    /* ===== ADMIN PANEL ===== */
    .admin-panel {
      display: none;
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 20px 60px;
    }
    .admin-panel.active { display: block; }
    .admin-table { width: 100%; border-collapse: collapse; background: #1a2744; border-radius: 12px; overflow: hidden; }
    .admin-table th { background: #15203a; padding: 14px 16px; text-align: left; font-size: 0.8rem; color: #fbbf24; text-transform: uppercase; letter-spacing: 0.5px; }
    .admin-table td { padding: 12px 16px; border-bottom: 1px solid #2a3a5c; font-size: 0.85rem; color: #cbd5e1; }
    .admin-table tr:hover td { background: rgba(96,165,250,0.05); }
    .status-badge { padding: 3px 10px; border-radius: 12px; font-size: 0.72rem; font-weight: 600; }
    .status-active { background: rgba(52,211,153,0.15); color: #34d399; }
    .status-retired { background: rgba(148,163,184,0.15); color: #94a3b8; }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 768px) {
      .top-bar { display: none; }
      .nav-menu { display: none; }
      .mobile-toggle { display: block; }
      .hero h2 { font-size: 1.8rem; }
      .hero-stats { flex-direction: column; gap: 20px; }
      .search-container { width: 160px; }
      .header-inner { height: 60px; }
      .chatbot-window { width: calc(100% - 48px); right: 24px; }
    }
  </style>
</head>
<body>

  <!-- Back to main site -->
  <a href="{{ site.baseurl }}/" class="back-to-main">&#8592; Back to Main Site</a>

  <!-- Top Bar -->
  <div class="top-bar">
    <div class="top-bar-left">
      <span>13881 Danielson St, Poway, CA 92064</span>
      <span>(858) 486-9009</span>
      <span>info@dsasd.org</span>
    </div>
    <div class="top-bar-right">
      <a href="#">Member Resources</a>
      <a href="#">Contact</a>
    </div>
  </div>

  <!-- Header with Mega Menu -->
  <header class="main-header">
    <div class="header-inner">
      <div class="logo">
        <div class="logo-badge">DSA</div>
        <div class="logo-text">
          <h1>Deputy Sheriffs' Association</h1>
          <span>San Diego County</span>
        </div>
      </div>

      <nav class="nav-menu">
        <div class="nav-item">
          About <span class="arrow">&#9660;</span>
          <div class="mega-dropdown">
            <a class="mega-link" href="#"><div class="mega-icon">&#9733;</div><div><div class="mega-label">Our Mission</div><div class="mega-desc">70 years of service</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128101;</div><div><div class="mega-label">Leadership</div><div class="mega-desc">Board of Directors</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128240;</div><div><div class="mega-label">History</div><div class="mega-desc">Since 1955</div></div></a>
          </div>
        </div>
        <div class="nav-item">
          Members <span class="arrow">&#9660;</span>
          <div class="mega-dropdown">
            <a class="mega-link" href="#"><div class="mega-icon">&#128179;</div><div><div class="mega-label">Benefits</div><div class="mega-desc">Insurance, legal, wellness</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128197;</div><div><div class="mega-label">Events</div><div class="mega-desc">Upcoming activities</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128196;</div><div><div class="mega-label">Documents</div><div class="mega-desc">Forms & resources</div></div></a>
          </div>
        </div>
        <div class="nav-item">
          News <span class="arrow">&#9660;</span>
          <div class="mega-dropdown">
            <a class="mega-link" href="#"><div class="mega-icon">&#128227;</div><div><div class="mega-label">Announcements</div><div class="mega-desc">Latest updates</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128220;</div><div><div class="mega-label">Newsletters</div><div class="mega-desc">Monthly publications</div></div></a>
            <a class="mega-link" href="#"><div class="mega-icon">&#128221;</div><div><div class="mega-label">Meeting Minutes</div><div class="mega-desc">Board meetings</div></div></a>
          </div>
        </div>
        <div class="nav-item">Store</div>
        <div class="nav-item" onclick="scrollToFAQ()">FAQ</div>
      </nav>

      <div class="search-container">
        <input type="text" class="search-input" placeholder="Search DSA..." id="siteSearch" autocomplete="off">
        <span class="search-icon">&#128269;</span>
        <div class="search-results" id="searchResults"></div>
      </div>

      <div class="auth-buttons" id="authButtons">
        <button class="btn-login" onclick="openModal('login')">Log In</button>
        <button class="btn-signup" onclick="openModal('signup')">Sign Up</button>
      </div>

      <div class="user-dropdown" id="userDropdown">
        <div class="user-btn" onclick="toggleUserMenu()">
          <span>&#9733;</span>
          <span id="userName">Deputy</span>
          <span class="arrow">&#9660;</span>
        </div>
        <div class="user-menu" id="userMenu">
          <div class="user-menu-header">
            <div class="name" id="menuUserName">-</div>
            <div class="badge" id="menuBadge">Badge: -</div>
          </div>
          <div class="user-menu-item" id="menuRank">Rank: -</div>
          <div class="user-menu-item" id="menuStation">Station: -</div>
          <div class="user-menu-item" id="adminPanelBtn" style="display:none;" onclick="toggleAdminPanel()">&#128100; View All Members</div>
          <div class="user-menu-item" onclick="logoutSheriff()" style="color:#ef4444;">&#128682; Log Out</div>
        </div>
      </div>

      <button class="mobile-toggle" onclick="toggleMobileNav()">&#9776;</button>
    </div>
  </header>

  <!-- Hero -->
  <section class="hero">
    <div class="hero-content">
      <h2>Protecting Those Who Protect Us</h2>
      <p>The Deputy Sheriffs' Association of San Diego County is the labor union representing the dedicated officers of the San Diego County Sheriff's Department. For over 70 years, we've been providing essential benefits, organizing events, and advocating for deputies of all ranks.</p>
      <div class="hero-stats">
        <div class="hero-stat"><div class="number">4,229</div><div class="label">Active Members</div></div>
        <div class="hero-stat"><div class="number">70+</div><div class="label">Years of Service</div></div>
        <div class="hero-stat"><div class="number">12</div><div class="label">Stations Covered</div></div>
        <div class="hero-stat"><div class="number">24/7</div><div class="label">Member Support</div></div>
      </div>
    </div>
  </section>

  <!-- Dashboard Tiles -->
  <h2 class="section-title">Member Dashboard</h2>
  <p class="section-subtitle">Quick access to everything you need</p>
  <div class="dashboard">
    <div class="tiles">
      <div class="tile"><div class="tile-icon">&#128179;</div><div class="tile-title">Benefits & Insurance</div><div class="tile-desc">Health, dental, vision, and life insurance plans for you and your family.</div></div>
      <div class="tile"><div class="tile-icon">&#128196;</div><div class="tile-title">Forms & Documents</div><div class="tile-desc">Downloadable forms, contracts, and important legal documents.</div></div>
      <div class="tile"><div class="tile-icon">&#128197;</div><div class="tile-title">Events Calendar</div><div class="tile-desc">Upcoming meetings, social events, and training sessions.</div></div>
      <div class="tile"><div class="tile-icon">&#128176;</div><div class="tile-title">DSA Store</div><div class="tile-desc">Official DSA merchandise and apparel for members.</div></div>
      <div class="tile"><div class="tile-icon">&#128272;</div><div class="tile-title">Legal Defense</div><div class="tile-desc">Access to legal representation and defense fund resources.</div></div>
      <div class="tile"><div class="tile-icon">&#127891;</div><div class="tile-title">Wellness Programs</div><div class="tile-desc">Mental health, fitness, and peer support programs.</div></div>
      <div class="tile"><div class="tile-icon">&#128240;</div><div class="tile-title">Newsletters</div><div class="tile-desc">Monthly DSA newsletters and board meeting minutes.</div></div>
      <div class="tile"><div class="tile-icon">&#127937;</div><div class="tile-title">Political Action</div><div class="tile-desc">DSA PAC updates and candidate endorsements.</div></div>
    </div>
  </div>

  <!-- Latest News -->
  <h2 class="section-title">Latest News</h2>
  <div class="news-section">
    <div class="news-grid">
      <div class="news-card">
        <span class="news-tag tag-announcement">Announcement</span>
        <h3>2026 Contract Negotiations Update</h3>
        <p>The DSA bargaining team has reached a tentative agreement with the county on wages, benefits, and working conditions for the next three years.</p>
        <div class="news-date">March 15, 2026</div>
      </div>
      <div class="news-card">
        <span class="news-tag tag-event">Event</span>
        <h3>Annual DSA Family Picnic</h3>
        <p>Join us at Poway Community Park on April 12th for our annual family picnic. Food, games, and fellowship for all DSA members and their families.</p>
        <div class="news-date">March 10, 2026</div>
      </div>
      <div class="news-card">
        <span class="news-tag tag-benefit">Benefit</span>
        <h3>New Dental Plan Options Available</h3>
        <p>We've partnered with Delta Dental to offer expanded coverage options. Open enrollment begins April 1st.</p>
        <div class="news-date">March 5, 2026</div>
      </div>
    </div>
  </div>

  <!-- Upcoming Events -->
  <h2 class="section-title">Upcoming Events</h2>
  <div class="events-section">
    <div class="events-list">
      <div class="event-item">
        <div class="event-date-box"><div class="month">APR</div><div class="day">02</div></div>
        <div class="event-info"><h4>Board of Directors Meeting</h4><p>DSA Headquarters, Poway - 6:00 PM</p></div>
        <button class="event-rsvp">RSVP</button>
      </div>
      <div class="event-item">
        <div class="event-date-box"><div class="month">APR</div><div class="day">12</div></div>
        <div class="event-info"><h4>Annual Family Picnic</h4><p>Poway Community Park - 11:00 AM</p></div>
        <button class="event-rsvp">RSVP</button>
      </div>
      <div class="event-item">
        <div class="event-date-box"><div class="month">APR</div><div class="day">18</div></div>
        <div class="event-info"><h4>Wellness Workshop: Stress Management</h4><p>Virtual Event - 2:00 PM</p></div>
        <button class="event-rsvp">RSVP</button>
      </div>
      <div class="event-item">
        <div class="event-date-box"><div class="month">MAY</div><div class="day">01</div></div>
        <div class="event-info"><h4>Deputy of the Year Awards</h4><p>Hilton San Diego - 7:00 PM</p></div>
        <button class="event-rsvp">RSVP</button>
      </div>
    </div>
  </div>

  <!-- FAQ Section -->
  <h2 class="section-title" id="faqSection">Frequently Asked Questions</h2>
  <p class="section-subtitle">Find answers instantly or chat with us</p>
  <div class="faq-section">
    <input type="text" class="faq-search" placeholder="Search FAQs..." id="faqSearch">
    <div class="faq-categories">
      <div class="faq-cat active" data-cat="all">All</div>
      <div class="faq-cat" data-cat="membership">Membership</div>
      <div class="faq-cat" data-cat="benefits">Benefits</div>
      <div class="faq-cat" data-cat="events">Events</div>
      <div class="faq-cat" data-cat="legal">Legal</div>
      <div class="faq-cat" data-cat="store">Store</div>
    </div>
    <div id="faqList">
      <div class="faq-item" data-cat="membership">
        <div class="faq-question" onclick="toggleFaq(this)"><span>How do I become a DSA member?</span><span class="toggle">+</span></div>
        <div class="faq-answer">All sworn personnel of the San Diego County Sheriff's Department are eligible for DSA membership. Contact the DSA office at (858) 486-9009 or visit our headquarters at 13881 Danielson Street, Poway to complete your enrollment. Membership dues are automatically deducted from your paycheck.</div>
      </div>
      <div class="faq-item" data-cat="membership">
        <div class="faq-question" onclick="toggleFaq(this)"><span>What are the membership dues?</span><span class="toggle">+</span></div>
        <div class="faq-answer">DSA membership dues are set by the Board of Directors and are competitive with similar law enforcement unions. Dues cover legal defense, political representation, member benefits, and organizational operations. Contact the office for current rates.</div>
      </div>
      <div class="faq-item" data-cat="benefits">
        <div class="faq-question" onclick="toggleFaq(this)"><span>What insurance benefits are available?</span><span class="toggle">+</span></div>
        <div class="faq-answer">DSA members have access to group health insurance (medical, dental, vision), life insurance, disability insurance, and supplemental coverage options. We negotiate competitive rates with major providers to ensure comprehensive coverage for members and their families.</div>
      </div>
      <div class="faq-item" data-cat="benefits">
        <div class="faq-question" onclick="toggleFaq(this)"><span>How does the wellness program work?</span><span class="toggle">+</span></div>
        <div class="faq-answer">Our wellness program includes peer support counseling, mental health resources, fitness facility access, and stress management workshops. All services are confidential. Contact the Wellness Coordinator through the member portal or call the DSA office.</div>
      </div>
      <div class="faq-item" data-cat="legal">
        <div class="faq-question" onclick="toggleFaq(this)"><span>What legal defense does DSA provide?</span><span class="toggle">+</span></div>
        <div class="faq-answer">The DSA Legal Defense Fund provides legal representation for members facing administrative investigations, critical incidents, and civil litigation arising from the performance of their duties. Contact the DSA office immediately if you need legal assistance.</div>
      </div>
      <div class="faq-item" data-cat="events">
        <div class="faq-question" onclick="toggleFaq(this)"><span>How do I RSVP for events?</span><span class="toggle">+</span></div>
        <div class="faq-answer">You can RSVP for DSA events through the member portal, by calling the office, or by clicking the RSVP button next to any event on this page. Most events are open to members and their immediate families.</div>
      </div>
      <div class="faq-item" data-cat="store">
        <div class="faq-question" onclick="toggleFaq(this)"><span>How do I purchase DSA merchandise?</span><span class="toggle">+</span></div>
        <div class="faq-answer">Visit the DSA Store section on our website or stop by the DSA office in Poway. We carry official DSA apparel, accessories, and memorabilia. Online orders ship within 5-7 business days. Member discounts apply automatically.</div>
      </div>
    </div>
  </div>

  <!-- Admin Panel (hidden by default) -->
  <h2 class="section-title admin-panel" id="adminTitle">All Registered Members</h2>
  <div class="admin-panel" id="adminPanel">
    <table class="admin-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Username</th>
          <th>Sheriff ID</th>
          <th>Rank</th>
          <th>Station</th>
          <th>Email</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody id="adminTableBody">
      </tbody>
    </table>
  </div>

  <!-- Footer -->
  <footer class="site-footer">
    <div class="footer-inner">
      <div class="footer-col">
        <h4>DSA San Diego</h4>
        <p>13881 Danielson Street</p>
        <p>Poway, CA 92064</p>
        <p>(858) 486-9009</p>
        <p>info@dsasd.org</p>
      </div>
      <div class="footer-col">
        <h4>Quick Links</h4>
        <a href="#">Benefits</a>
        <a href="#">Events</a>
        <a href="#">Store</a>
        <a href="#">Contact</a>
      </div>
      <div class="footer-col">
        <h4>Resources</h4>
        <a href="#">Legal Defense</a>
        <a href="#">Wellness</a>
        <a href="#">Newsletters</a>
        <a href="#">Meeting Minutes</a>
      </div>
      <div class="footer-col">
        <h4>Connect</h4>
        <a href="#">Facebook</a>
        <a href="#">Twitter</a>
        <a href="#">Instagram</a>
        <a href="#">YouTube</a>
      </div>
    </div>
    <div class="footer-bottom">
      &copy; 2026 Deputy Sheriffs' Association of San Diego County. All rights reserved.
    </div>
  </footer>

  <!-- Chatbot -->
  <button class="chatbot-trigger" id="chatbotTrigger" onclick="toggleChatbot()">&#128172;</button>
  <div class="chatbot-window" id="chatbotWindow">
    <div class="chatbot-header">
      <h3>DSA FAQ Assistant</h3>
      <button class="chatbot-close" onclick="toggleChatbot()">&times;</button>
    </div>
    <div class="chatbot-messages" id="chatMessages">
      <div class="chat-msg bot"><div class="chat-bubble">Hi! I'm the DSA FAQ Assistant. Ask me anything about membership, benefits, events, legal defense, or the DSA store. How can I help you today?</div></div>
    </div>
    <div class="chatbot-input-area">
      <input type="text" class="chatbot-input" id="chatInput" placeholder="Type your question..." onkeydown="if(event.key==='Enter')sendChat()">
      <button class="chatbot-send" onclick="sendChat()">Send</button>
    </div>
  </div>

  <!-- Login/Signup Modal -->
  <div class="modal-overlay" id="modalOverlay">
    <div class="modal">
      <button class="modal-close" onclick="closeModal()">&times;</button>
      <h2 id="modalTitle">Member Login</h2>
      <p class="modal-subtitle" id="modalSubtitle">Access your DSA member portal</p>

      <div class="modal-tabs">
        <div class="modal-tab active" id="tabLogin" onclick="switchTab('login')">Log In</div>
        <div class="modal-tab" id="tabSignup" onclick="switchTab('signup')">Sign Up</div>
      </div>

      <!-- Login Form -->
      <form class="modal-form" id="loginForm" onsubmit="sheriffLogin(event)">
        <div class="form-group">
          <label>Username</label>
          <input type="text" id="loginUid" placeholder="Enter your username" required>
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="loginPassword" placeholder="Enter your password" required>
        </div>
        <button type="submit" class="modal-submit">Log In</button>
        <p class="modal-error" id="loginError"></p>
      </form>

      <!-- Signup Form -->
      <form class="modal-form" id="signupFormSheriff" onsubmit="sheriffSignup(event)" style="display:none;">
        <div class="form-group">
          <label>Full Name</label>
          <input type="text" id="signupName" placeholder="e.g., John Smith" required>
        </div>
        <div class="form-group">
          <label>Username</label>
          <input type="text" id="signupUidSheriff" placeholder="Choose a username" required>
        </div>
        <div class="form-group">
          <label>Sheriff ID / Badge Number</label>
          <input type="text" id="signupSheriffId" placeholder="e.g., SD-1234" required>
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="signupEmailSheriff" placeholder="your@email.com">
        </div>
        <div class="form-group">
          <label>Rank</label>
          <select id="signupRank">
            <option value="Deputy">Deputy</option>
            <option value="Corporal">Corporal</option>
            <option value="Sergeant">Sergeant</option>
            <option value="Lieutenant">Lieutenant</option>
            <option value="Captain">Captain</option>
          </select>
        </div>
        <div class="form-group">
          <label>Station / Location</label>
          <select id="signupStation">
            <option value="San Diego Central">San Diego Central</option>
            <option value="Vista Station">Vista Station</option>
            <option value="Encinitas Station">Encinitas Station</option>
            <option value="Fallbrook Station">Fallbrook Station</option>
            <option value="Imperial Beach Station">Imperial Beach Station</option>
            <option value="Lemon Grove Station">Lemon Grove Station</option>
            <option value="Pine Valley Station">Pine Valley Station</option>
            <option value="Rancho San Diego Station">Rancho San Diego Station</option>
            <option value="San Marcos Station">San Marcos Station</option>
            <option value="Santee Station">Santee Station</option>
            <option value="4S Ranch Station">4S Ranch Station</option>
            <option value="DSA Headquarters - Poway">DSA Headquarters - Poway</option>
          </select>
        </div>
        <div class="form-group">
          <label>Phone Number</label>
          <input type="tel" id="signupPhone" placeholder="(xxx) xxx-xxxx">
        </div>
        <div class="form-group">
          <label>Password (min 8 characters)</label>
          <input type="password" id="signupPasswordSheriff" placeholder="Create a password" required minlength="8">
        </div>
        <button type="submit" class="modal-submit">Create Account</button>
        <p class="modal-error" id="signupError"></p>
      </form>
    </div>
  </div>

  <script>
    // ===== CONFIG =====
    const API_BASE = (location.hostname === 'localhost' || location.hostname === '127.0.0.1')
      ? 'http://localhost:8587'
      : 'https://flask.opencodingsociety.com';

    let currentUser = null;

    // ===== MODAL =====
    function openModal(tab) {
      document.getElementById('modalOverlay').classList.add('active');
      switchTab(tab || 'login');
    }
    function closeModal() {
      document.getElementById('modalOverlay').classList.remove('active');
      document.getElementById('loginError').style.display = 'none';
      document.getElementById('signupError').style.display = 'none';
    }
    function switchTab(tab) {
      document.getElementById('tabLogin').classList.toggle('active', tab === 'login');
      document.getElementById('tabSignup').classList.toggle('active', tab === 'signup');
      document.getElementById('loginForm').style.display = tab === 'login' ? 'block' : 'none';
      document.getElementById('signupFormSheriff').style.display = tab === 'signup' ? 'block' : 'none';
      document.getElementById('modalTitle').textContent = tab === 'login' ? 'Member Login' : 'Create Account';
      document.getElementById('modalSubtitle').textContent = tab === 'login' ? 'Access your DSA member portal' : 'Register as a DSA member';
    }

    // ===== LOGIN =====
    function sheriffLogin(e) {
      e.preventDefault();
      const uid = document.getElementById('loginUid').value;
      const password = document.getElementById('loginPassword').value;

      fetch(`${API_BASE}/api/sheriff/authenticate`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        credentials: 'include',
        body: JSON.stringify({ uid, password })
      })
      .then(r => {
        if (!r.ok) return r.json().then(d => { throw new Error(d.message || 'Login failed'); });
        return r.json();
      })
      .then(data => {
        currentUser = data.user;
        closeModal();
        updateUIForUser();
      })
      .catch(err => {
        const el = document.getElementById('loginError');
        el.textContent = err.message;
        el.style.display = 'block';
      });
    }

    // ===== SIGNUP =====
    function sheriffSignup(e) {
      e.preventDefault();
      const body = {
        name: document.getElementById('signupName').value,
        uid: document.getElementById('signupUidSheriff').value,
        sheriff_id: document.getElementById('signupSheriffId').value,
        email: document.getElementById('signupEmailSheriff').value,
        rank: document.getElementById('signupRank').value,
        station: document.getElementById('signupStation').value,
        phone: document.getElementById('signupPhone').value,
        password: document.getElementById('signupPasswordSheriff').value,
      };

      fetch(`${API_BASE}/api/sheriff/user`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        credentials: 'include',
        body: JSON.stringify(body)
      })
      .then(r => {
        if (!r.ok) return r.json().then(d => { throw new Error(d.message || 'Signup failed'); });
        return r.json();
      })
      .then(() => {
        switchTab('login');
        document.getElementById('loginUid').value = body.uid;
        alert('Account created! Please log in.');
      })
      .catch(err => {
        const el = document.getElementById('signupError');
        el.textContent = err.message;
        el.style.display = 'block';
      });
    }

    // ===== LOGOUT =====
    function logoutSheriff() {
      fetch(`${API_BASE}/api/sheriff/authenticate`, {
        method: 'DELETE',
        credentials: 'include'
      }).finally(() => {
        currentUser = null;
        updateUIForUser();
        document.getElementById('userMenu').classList.remove('active');
      });
    }

    // ===== UI UPDATE =====
    function updateUIForUser() {
      const authBtns = document.getElementById('authButtons');
      const userDrop = document.getElementById('userDropdown');
      if (currentUser) {
        authBtns.style.display = 'none';
        userDrop.classList.add('active');
        document.getElementById('userName').textContent = currentUser.name.split(' ')[0];
        document.getElementById('menuUserName').textContent = currentUser.name;
        document.getElementById('menuBadge').textContent = 'Badge: ' + currentUser.sheriff_id;
        document.getElementById('menuRank').textContent = 'Rank: ' + currentUser.rank;
        document.getElementById('menuStation').textContent = 'Station: ' + currentUser.station;
        if (currentUser.role === 'Admin') {
          document.getElementById('adminPanelBtn').style.display = 'block';
        }
      } else {
        authBtns.style.display = 'flex';
        userDrop.classList.remove('active');
        document.getElementById('adminPanel').classList.remove('active');
        document.getElementById('adminTitle').classList.remove('active');
        document.getElementById('adminPanelBtn').style.display = 'none';
      }
    }

    function toggleUserMenu() {
      document.getElementById('userMenu').classList.toggle('active');
    }

    // ===== ADMIN PANEL =====
    function toggleAdminPanel() {
      const panel = document.getElementById('adminPanel');
      const title = document.getElementById('adminTitle');
      panel.classList.toggle('active');
      title.classList.toggle('active');
      if (panel.classList.contains('active')) loadAdminData();
      document.getElementById('userMenu').classList.remove('active');
    }

    function loadAdminData() {
      fetch(`${API_BASE}/api/sheriff/user`, {
        credentials: 'include'
      })
      .then(r => r.json())
      .then(users => {
        const tbody = document.getElementById('adminTableBody');
        tbody.innerHTML = '';
        users.forEach(u => {
          const statusClass = u.status === 'Active' ? 'status-active' : 'status-retired';
          tbody.innerHTML += `<tr>
            <td>${u.name}</td>
            <td>${u.uid}</td>
            <td>${u.sheriff_id}</td>
            <td>${u.rank}</td>
            <td>${u.station}</td>
            <td>${u.email}</td>
            <td><span class="status-badge ${statusClass}">${u.status}</span></td>
          </tr>`;
        });
      })
      .catch(err => console.error('Admin data error:', err));
    }

    // ===== SEARCH =====
    const searchData = [
      'Benefits & Insurance', 'Legal Defense Fund', 'Wellness Programs',
      'Events Calendar', 'DSA Store', 'Board Meeting Minutes',
      'Newsletters', 'Political Action Committee', 'Membership Enrollment',
      'Contract Information', 'Dental Plan', 'FAQ', 'Contact Us'
    ];

    document.getElementById('siteSearch').addEventListener('input', function() {
      const q = this.value.toLowerCase().trim();
      const results = document.getElementById('searchResults');
      if (q.length < 2) { results.classList.remove('active'); return; }
      const matches = searchData.filter(item => item.toLowerCase().includes(q));
      if (matches.length === 0) { results.classList.remove('active'); return; }
      results.innerHTML = matches.map(m => `<div class="search-result-item">${m}</div>`).join('');
      results.classList.add('active');
    });

    document.addEventListener('click', function(e) {
      if (!e.target.closest('.search-container')) document.getElementById('searchResults').classList.remove('active');
      if (!e.target.closest('.user-dropdown')) document.getElementById('userMenu').classList.remove('active');
    });

    // ===== FAQ =====
    function toggleFaq(el) {
      el.classList.toggle('open');
      el.nextElementSibling.classList.toggle('open');
    }

    document.querySelectorAll('.faq-cat').forEach(cat => {
      cat.addEventListener('click', function() {
        document.querySelectorAll('.faq-cat').forEach(c => c.classList.remove('active'));
        this.classList.add('active');
        const category = this.dataset.cat;
        document.querySelectorAll('.faq-item').forEach(item => {
          item.style.display = (category === 'all' || item.dataset.cat === category) ? 'block' : 'none';
        });
      });
    });

    document.getElementById('faqSearch').addEventListener('input', function() {
      const q = this.value.toLowerCase();
      document.querySelectorAll('.faq-item').forEach(item => {
        const text = item.textContent.toLowerCase();
        item.style.display = text.includes(q) ? 'block' : 'none';
      });
    });

    function scrollToFAQ() {
      document.getElementById('faqSection').scrollIntoView({ behavior: 'smooth' });
    }

    // ===== CHATBOT =====
    const faqData = [
      { q: ['member', 'join', 'become', 'enroll', 'sign up'], a: 'All sworn personnel of the San Diego County Sheriff\'s Department are eligible. Contact the DSA office at (858) 486-9009 or visit our headquarters at 13881 Danielson Street, Poway.' },
      { q: ['dues', 'cost', 'fee', 'price'], a: 'DSA membership dues are set by the Board of Directors and are automatically deducted from your paycheck. Contact the office at (858) 486-9009 for current rates.' },
      { q: ['insurance', 'health', 'dental', 'vision', 'medical'], a: 'DSA members have access to group health insurance (medical, dental, vision), life insurance, disability insurance, and supplemental coverage. We negotiate competitive rates with major providers.' },
      { q: ['legal', 'defense', 'lawyer', 'attorney'], a: 'The DSA Legal Defense Fund provides representation for administrative investigations, critical incidents, and civil litigation arising from your duties. Contact the DSA office immediately if you need help.' },
      { q: ['wellness', 'mental health', 'stress', 'counseling', 'fitness'], a: 'Our wellness program includes peer support counseling, mental health resources, fitness facility access, and stress management workshops. All services are confidential.' },
      { q: ['event', 'picnic', 'meeting', 'rsvp'], a: 'You can RSVP through the member portal, by calling the office, or via the RSVP buttons on this page. Check the Events section for upcoming activities.' },
      { q: ['store', 'merchandise', 'apparel', 'buy', 'shop'], a: 'Visit the DSA Store section or stop by the office in Poway. We carry official apparel, accessories, and memorabilia. Member discounts apply automatically.' },
      { q: ['contact', 'phone', 'email', 'address', 'location'], a: 'DSA Headquarters: 13881 Danielson Street, Poway, CA 92064. Phone: (858) 486-9009. Email: info@dsasd.org.' },
      { q: ['contract', 'negotiation', 'bargaining', 'wage', 'salary'], a: 'The DSA bargaining team negotiates contracts covering wages, benefits, and working conditions. Check the News section for the latest updates on negotiations.' },
      { q: ['newsletter', 'minutes', 'publication'], a: 'Monthly newsletters and board meeting minutes are available in the Newsletters section of the member portal. Back issues are archived for reference.' },
    ];

    function toggleChatbot() {
      document.getElementById('chatbotWindow').classList.toggle('open');
    }

    function sendChat() {
      const input = document.getElementById('chatInput');
      const msg = input.value.trim();
      if (!msg) return;
      input.value = '';

      addChatMessage(msg, 'user');

      const q = msg.toLowerCase();
      let answer = null;
      for (const faq of faqData) {
        if (faq.q.some(keyword => q.includes(keyword))) {
          answer = faq.a;
          break;
        }
      }

      setTimeout(() => {
        addChatMessage(answer || "I'm not sure about that. You can call the DSA office at (858) 486-9009 or email info@dsasd.org for help. You can also scroll down to the FAQ section for more topics.", 'bot');
      }, 500);
    }

    function addChatMessage(text, sender) {
      const container = document.getElementById('chatMessages');
      const div = document.createElement('div');
      div.className = 'chat-msg ' + sender;
      div.innerHTML = '<div class="chat-bubble">' + text + '</div>';
      container.appendChild(div);
      container.scrollTop = container.scrollHeight;
    }

    // ===== CHECK AUTH ON LOAD =====
    (function checkAuth() {
      fetch(`${API_BASE}/api/sheriff/id`, { credentials: 'include' })
        .then(r => { if (!r.ok) throw new Error(); return r.json(); })
        .then(data => { currentUser = data; updateUIForUser(); })
        .catch(() => {});
    })();
  </script>

</body>
</html>
