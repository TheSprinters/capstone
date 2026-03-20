---
toc: false
layout: post
title: DSA Website Rebuild Timeline - TheSprinters
description: A 5-week plan to prototype features, build the final site, and present the Deputy Sheriffs' Association website rebuild.
permalink: /dsa-rebuild-timeline/
sticky_rank: 8
---

<style>
  .dsa-timeline-page {
    --dsa-bg: linear-gradient(180deg, #0f2031 0%, #162c43 100%);
    --dsa-ink: #152b3f;
    --dsa-muted: #314b61;
    --dsa-line: rgba(16, 55, 92, 0.12);
    --dsa-panel: #ffffff;
    --dsa-accent: #0f6996;
    --dsa-accent-2: #29a0a8;
    --dsa-soft: #e8f4fb;
    --dsa-gold: #e6a93f;
    --dsa-shadow: 0 22px 48px rgba(4, 14, 24, 0.28);
    color: #ffffff;
    background: var(--dsa-bg);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 30px;
    padding: 1.5rem;
  }

  .dsa-timeline-page h2,
  .dsa-timeline-page h3,
  .dsa-timeline-page h4 {
    color: #ffffff;
  }

  .dsa-hero {
    background:
      radial-gradient(circle at top right, rgba(255, 255, 255, 0.18), transparent 32%),
      linear-gradient(135deg, #12314d 0%, #15557a 58%, #21848d 100%);
    color: #fff;
    border-radius: 28px;
    padding: 2.5rem 2rem;
    box-shadow: var(--dsa-shadow);
    margin: 0.35rem 0 2rem;
    overflow: hidden;
    position: relative;
  }

  .dsa-hero::after {
    content: "";
    position: absolute;
    inset: auto -60px -80px auto;
    width: 220px;
    height: 220px;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.08);
  }

  .dsa-kicker {
    display: inline-block;
    font-size: 0.78rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    font-weight: 700;
    padding: 0.45rem 0.75rem;
    border-radius: 999px;
    background: rgba(255, 255, 255, 0.22);
    color: #ffffff;
    border: 1px solid rgba(255, 255, 255, 0.18);
    margin-bottom: 1rem;
  }

  .dsa-hero h2 {
    color: #fff;
    font-size: clamp(2rem, 4vw, 3rem);
    line-height: 1.05;
    margin-bottom: 0.75rem;
    font-weight: 800;
  }

  .dsa-hero p {
    color: #ffffff;
    font-size: 1.05rem;
    font-weight: 500;
    line-height: 1.7;
    max-width: 760px;
    margin-bottom: 1.5rem;
  }

  .dsa-stat-grid,
  .dsa-team-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
  }

  .dsa-stat,
  .dsa-team-card,
  .dsa-summary-card,
  .dsa-week-card,
  .dsa-milestone,
  .dsa-outreach-card {
    background: var(--dsa-panel);
    border: 1px solid rgba(13, 92, 143, 0.10);
    border-radius: 22px;
    box-shadow: var(--dsa-shadow);
  }

  .dsa-stat {
    padding: 1.1rem 1rem;
    background: rgba(9, 23, 36, 0.38);
    border-color: rgba(255, 255, 255, 0.18);
    box-shadow: none;
  }

  .dsa-stat-label {
    display: block;
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: rgba(255, 255, 255, 0.92);
    font-weight: 700;
    margin-bottom: 0.35rem;
  }

  .dsa-stat strong {
    font-size: 1.18rem;
    font-weight: 800;
    color: #fff;
  }

  .dsa-section-title {
    margin: 2.5rem 0 1rem;
    font-size: 1.6rem;
    color: #ffffff;
    font-weight: 800;
  }

  .dsa-summary-card {
    padding: 1.35rem 1.4rem;
    margin-bottom: 2rem;
  }

  /* Cards use dark text on white background */
  .dsa-summary-card,
  .dsa-team-card,
  .dsa-week-card,
  .dsa-milestone,
  .dsa-outreach-card {
    background: #ffffff;
    color: var(--dsa-ink);
  }

  .dsa-summary-card h3,
  .dsa-team-card h4,
  .dsa-week-card h3,
  .dsa-milestone h2,
  .dsa-outreach-card h3 {
    color: var(--dsa-ink) !important;
  }

  .dsa-summary-card p,
  .dsa-team-card p,
  .dsa-week-card p,
  .dsa-milestone p,
  .dsa-outreach-card p {
    color: var(--dsa-muted) !important;
    font-weight: 600;
    line-height: 1.7;
  }

  .dsa-summary-card li,
  .dsa-team-card li,
  .dsa-week-card li,
  .dsa-milestone li,
  .dsa-outreach-card li {
    color: #20384d !important;
    font-weight: 600;
    line-height: 1.65;
  }

  .dsa-summary-card p:last-child {
    margin-bottom: 0;
  }

  .dsa-timeline {
    position: relative;
    margin: 2rem 0;
    padding-left: 1.25rem;
  }

  .dsa-timeline::before {
    content: "";
    position: absolute;
    top: 0.5rem;
    bottom: 0.5rem;
    left: 0.25rem;
    width: 3px;
    border-radius: 999px;
    background: linear-gradient(180deg, var(--dsa-accent), var(--dsa-accent-2));
    opacity: 1;
  }

  .dsa-week-card {
    position: relative;
    margin: 0 0 1.35rem 1.5rem;
    padding: 1.4rem 1.4rem 1.2rem;
  }

  .dsa-week-card::before {
    content: "";
    position: absolute;
    left: -1.92rem;
    top: 1.55rem;
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--dsa-gold), #ffd36a);
    border: 3px solid #fff;
    box-shadow: 0 0 0 5px rgba(244, 181, 68, 0.18);
  }

  .dsa-week-top {
    display: flex;
    justify-content: space-between;
    gap: 1rem;
    align-items: flex-start;
    margin-bottom: 0.9rem;
  }

  .dsa-week-chip {
    display: inline-block;
    background: var(--dsa-soft);
    color: var(--dsa-accent) !important;
    font-size: 0.8rem;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    padding: 0.4rem 0.7rem;
    border-radius: 999px;
    margin-bottom: 0.55rem;
    border: 1px solid rgba(15, 105, 150, 0.12);
  }

  .dsa-week-date {
    color: #27465e !important;
    font-weight: 700;
    white-space: nowrap;
  }

  .dsa-week-card h3 {
    margin: 0 0 0.4rem;
    font-size: 1.35rem;
    font-weight: 800;
  }

  .dsa-focus {
    color: var(--dsa-accent) !important;
    font-weight: 800;
    margin-bottom: 0.65rem;
  }

  .dsa-week-card ul {
    margin: 0.75rem 0 0;
    padding-left: 1.1rem;
  }

  .dsa-week-card li {
    margin-bottom: 0.45rem;
    color: #20384d !important;
    font-weight: 600;
    line-height: 1.65;
  }

  .dsa-team-card {
    padding: 1.3rem;
  }

  .dsa-team-card h4 {
    margin-bottom: 0.45rem;
    font-weight: 800;
  }

  .dsa-role-tag {
    display: inline-block;
    font-size: 0.76rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--dsa-accent) !important;
    background: var(--dsa-soft);
    border-radius: 999px;
    padding: 0.35rem 0.65rem;
    margin-bottom: 0.8rem;
    border: 1px solid rgba(14, 90, 134, 0.12);
  }

  .dsa-ownership-table {
    width: 100%;
    border-collapse: collapse;
    overflow: hidden;
    border-radius: 20px;
    margin-top: 1rem;
    box-shadow: var(--dsa-shadow);
  }

  .dsa-ownership-table th,
  .dsa-ownership-table td {
    padding: 1rem;
    text-align: left;
    vertical-align: top;
    border: 1px solid var(--dsa-line);
    line-height: 1.6;
  }

  .dsa-ownership-table th {
    background: linear-gradient(135deg, #12314d 0%, #175d84 100%);
    color: #fff;
    font-weight: 800;
  }

  .dsa-ownership-table td {
    background: #ffffff;
    color: #173047 !important;
    font-weight: 500;
  }

  .dsa-milestone {
    padding: 1.5rem;
    margin-top: 2rem;
    border-left: 8px solid var(--dsa-gold);
  }

  .dsa-milestone h2 {
    font-weight: 800;
  }

  .dsa-milestone p:last-child {
    margin-bottom: 0;
  }

  .dsa-outreach-card {
    padding: 1.5rem;
    margin-top: 1.5rem;
    border-left: 8px solid var(--dsa-accent-2);
  }

  .dsa-outreach-card h3 {
    font-weight: 800;
    margin-bottom: 0.5rem;
  }

  .dsa-outreach-card ul {
    margin: 0.75rem 0 0;
    padding-left: 1.1rem;
  }

  .dsa-outreach-step {
    display: flex;
    align-items: flex-start;
    gap: 1rem;
    margin-bottom: 1rem;
    padding: 1rem;
    background: var(--dsa-soft);
    border-radius: 14px;
    border: 1px solid rgba(15, 105, 150, 0.10);
  }

  .dsa-outreach-step-num {
    flex-shrink: 0;
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--dsa-accent), var(--dsa-accent-2));
    color: #fff;
    font-weight: 800;
    font-size: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .dsa-outreach-step-text {
    flex: 1;
  }

  .dsa-outreach-step-text strong {
    color: var(--dsa-ink) !important;
    display: block;
    margin-bottom: 0.25rem;
  }

  .dsa-outreach-step-text span {
    color: var(--dsa-muted) !important;
    font-weight: 600;
    font-size: 0.95rem;
    line-height: 1.6;
  }

  @media (max-width: 900px) {
    .dsa-stat-grid,
    .dsa-team-grid {
      grid-template-columns: 1fr;
    }

    .dsa-week-top {
      flex-direction: column;
    }

    .dsa-week-date {
      white-space: normal;
    }
  }

  @media (max-width: 700px) {
    .dsa-hero {
      padding: 2rem 1.25rem;
      border-radius: 22px;
    }

    .dsa-timeline-page {
      padding: 0.9rem;
      border-radius: 22px;
    }

    .dsa-timeline {
      padding-left: 0.95rem;
    }

    .dsa-week-card {
      margin-left: 1.15rem;
      padding: 1.15rem;
    }

    .dsa-week-card::before {
      left: -1.55rem;
    }

    .dsa-ownership-table {
      display: block;
      overflow-x: auto;
      white-space: nowrap;
    }
  }
</style>

<div class="dsa-timeline-page">
  <section class="dsa-hero">
    <span class="dsa-kicker">TheSprinters Project Plan</span>
    <h2>DSA Website Rebuild Timeline</h2>
    <p>
      Our 5-week roadmap for rebuilding the Deputy Sheriffs' Association website — from a polished single-page portal with working authentication and AI-powered features, through QA and final delivery to the DSA organization.
    </p>
    <div class="dsa-stat-grid">
      <div class="dsa-stat">
        <span class="dsa-stat-label">Start Date</span>
        <strong>March 19, 2026</strong>
      </div>
      <div class="dsa-stat">
        <span class="dsa-stat-label">Project Length</span>
        <strong>5 Weeks</strong>
      </div>
      <div class="dsa-stat">
        <span class="dsa-stat-label">Final Target</span>
        <strong>April 24, 2026</strong>
      </div>
    </div>
  </section>

  <section class="dsa-summary-card">
    <h3>What This Timeline Covers</h3>
    <p>
      The rebuild transforms the existing dsasd.org WordPress site into a modern, single-page portal with functional authentication, an AI chatbot, interactive FAQ, searchable content, and a streamlined member dashboard. Across five weeks we move from UI prototyping and backend API work, through integration and polish, to a presentation-ready package for the DSA organization.
    </p>
  </section>

  <h2 class="dsa-section-title">Rebuild Timeline</h2>

  <div class="dsa-timeline">
    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 1</span>
          <h3>Portal UI and Backend Foundation</h3>
        </div>
        <div class="dsa-week-date">March 23-27, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Polished UI + backend APIs</div>
      <p>
        Build the single-page portal layout and wire up the Flask backend with sheriff authentication and data models.
      </p>
      <ul>
        <li>Single-page portal UI with hero, about, services, FAQ, newsletter, board, events, contact, and footer sections.</li>
        <li>Flask backend with Sheriff model, JWT authentication (login/signup), and CRUD endpoints.</li>
        <li>Smooth-scroll navigation with active link highlighting and working search bar.</li>
        <li>Real DSA images (logo, store photos, board portraits, memorial, golf tournament) integrated from dsasd.org.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 2</span>
          <h3>Interactive Features and AI Chatbot</h3>
        </div>
        <div class="dsa-week-date">March 30-April 3, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Making every button functional</div>
      <p>
        Connect all interactive elements to the backend and add the AI-powered chatbot for member support.
      </p>
      <ul>
        <li>AI chatbot powered by Claude API with conversation history and DSA-specific system prompt.</li>
        <li>FAQ section with category tag filtering, keyword search, and expandable answers.</li>
        <li>Login/signup modals wired to sheriff auth endpoints with cookie-based sessions.</li>
        <li>Admin panel for managing sheriff users (view all, update roles, delete accounts).</li>
        <li>Newsletter section with interactive Silver Star preview cards and expandable content.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 3</span>
          <h3>Code Quality and SRP Refactoring</h3>
        </div>
        <div class="dsa-week-date">April 6-10, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Clean code + Single Responsibility Principle</div>
      <p>
        Refactor frontend and backend code to follow SRP, improving maintainability without changing functionality.
      </p>
      <ul>
        <li>Frontend JS refactored into 30+ focused helper functions (DOM helpers, auth, chatbot, search, FAQ, admin, UI state).</li>
        <li>Backend sheriff.py refactored — extracted AuthError, decode_sheriff_token, require_admin, set_sheriff_cookie, validate_signup_data.</li>
        <li>Backend sheriff_chat.py refactored — split monolithic handler into validate, build, call, and parse functions.</li>
        <li>Shared apiRequest() wrapper on frontend to eliminate duplicate fetch logic across all endpoints.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 4</span>
          <h3>Polish, Testing, and Responsiveness</h3>
        </div>
        <div class="dsa-week-date">April 13-17, 2026</div>
      </div>
      <div class="dsa-focus">Focus: QA + cross-device polish</div>
      <p>
        With all features working, focus shifts to visual polish, accessibility, and testing across devices.
      </p>
      <ul>
        <li>Responsive layout testing on mobile, tablet, and desktop breakpoints.</li>
        <li>Accessibility pass — contrast ratios, keyboard navigation, screen reader labels.</li>
        <li>Bug fixes for edge cases in auth flow, chatbot error handling, and search behavior.</li>
        <li>Performance tuning — image optimization, lazy loading, and smooth animations.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 5</span>
          <h3>Presentation and DSA Outreach</h3>
        </div>
        <div class="dsa-week-date">April 20-24, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Final package + DSA organization outreach</div>
      <p>
        Package the complete rebuild and present it to the Deputy Sheriffs' Association for feedback and adoption.
      </p>
      <ul>
        <li>Final build packaged with deployment-ready configuration and clean handoff documentation.</li>
        <li>Demo walkthrough prepared showing before/after comparison with dsasd.org.</li>
        <li>Presentation deck highlighting reduced clicks, AI features, modern UI, and mobile responsiveness.</li>
        <li>Formal outreach email and meeting with DSA leadership to present the redesign proposal.</li>
      </ul>
    </article>
  </div>

  <h2 class="dsa-section-title">DSA Organization Communication Plan</h2>

  <section class="dsa-outreach-card">
    <h3>How We Plan to Engage the DSA</h3>
    <p>
      Our outreach strategy ensures the DSA organization is informed and involved at the right moments — not just at the end.
    </p>

    <div class="dsa-outreach-step">
      <div class="dsa-outreach-step-num">1</div>
      <div class="dsa-outreach-step-text">
        <strong>Week 2 — Initial Contact (March 30)</strong>
        <span>Send an introductory email to DSA leadership explaining the project, sharing early screenshots of the polished portal, and asking for any priorities or feedback on direction.</span>
      </div>
    </div>

    <div class="dsa-outreach-step">
      <div class="dsa-outreach-step-num">2</div>
      <div class="dsa-outreach-step-text">
        <strong>Week 4 — Progress Update (April 13)</strong>
        <span>Share a live demo link or video walkthrough of the working portal with authentication, chatbot, and all interactive features. Collect feedback on any adjustments before final polish.</span>
      </div>
    </div>

    <div class="dsa-outreach-step">
      <div class="dsa-outreach-step-num">3</div>
      <div class="dsa-outreach-step-text">
        <strong>Week 5 — Formal Presentation (April 20-24)</strong>
        <span>Schedule an in-person or virtual meeting with DSA leadership to present the final rebuild, walk through the before/after comparison, and discuss next steps for adoption or integration with dsasd.org.</span>
      </div>
    </div>
  </section>

  <h2 class="dsa-section-title">Work Split (3 Members)</h2>

  <div class="dsa-team-grid">
    <section class="dsa-team-card">
      <span class="dsa-role-tag">Akhil · Backend & API</span>
      <h4>System Architecture</h4>
      <p>
        Flask API design, Sheriff model and database, JWT authentication, Claude AI chatbot endpoint, SRP refactoring of backend files.
      </p>
    </section>

    <section class="dsa-team-card">
      <span class="dsa-role-tag">Neil · UI/UX & Frontend</span>
      <h4>Interface and Experience</h4>
      <p>
        Single-page portal layout, responsive design, real DSA image integration, search and FAQ interactivity, frontend SRP refactoring.
      </p>
    </section>

    <section class="dsa-team-card">
      <span class="dsa-role-tag">Moiz · Calendar & Info Architecture</span>
      <h4>Content and Delivery</h4>
      <p>
        Information architecture, events and newsletter content, QA and cross-device testing, DSA outreach coordination and presentation materials.
      </p>
    </section>
  </div>

  <h2 class="dsa-section-title">Weekly Ownership Snapshot</h2>

  <table class="dsa-ownership-table">
    <thead>
      <tr>
        <th>Week (Dates)</th>
        <th>Akhil</th>
        <th>Neil</th>
        <th>Moiz</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Week 1</strong><br>March 23-27</td>
        <td>Sheriff model, JWT auth, CRUD API endpoints</td>
        <td>Single-page portal UI, smooth scroll, real DSA images</td>
        <td>Content inventory, navigation structure, UX flow</td>
      </tr>
      <tr>
        <td><strong>Week 2</strong><br>March 30-April 3</td>
        <td>Claude chatbot API, admin endpoints</td>
        <td>Login/signup modals, FAQ interactivity, search bar</td>
        <td>Newsletter cards, events section, initial DSA email</td>
      </tr>
      <tr>
        <td><strong>Week 3</strong><br>April 6-10</td>
        <td>SRP refactor: sheriff.py, sheriff_chat.py</td>
        <td>SRP refactor: frontend JS (30+ helpers)</td>
        <td>SRP blog writeup, integration testing</td>
      </tr>
      <tr>
        <td><strong>Week 4</strong><br>April 13-17</td>
        <td>API error handling, performance checks</td>
        <td>Responsive polish, accessibility pass</td>
        <td>Cross-device QA, DSA progress update email</td>
      </tr>
      <tr>
        <td><strong>Week 5</strong><br>April 20-24</td>
        <td>Deployment config, handoff docs</td>
        <td>Final UI tweaks, before/after visuals</td>
        <td>Demo script, presentation deck, DSA meeting</td>
      </tr>
    </tbody>
  </table>

  <section class="dsa-milestone">
    <h2>Final Milestone</h2>
    <p>
      By <strong>April 24, 2026</strong>, we will deliver a complete, polished DSA portal rebuild with working authentication, AI chatbot, interactive FAQ, and a modern responsive design — ready for formal presentation to the Deputy Sheriffs' Association.
    </p>
    <p>
      The final deliverable includes the working portal, clean refactored codebase, deployment documentation, and a presentation package comparing our rebuild against the current dsasd.org site.
    </p>
  </section>
</div>
