---
toc: false
layout: post
title: DSA Portal Build Summary — TheSprinters
description: A complete summary of the Deputy Sheriffs' Association portal redesign — what we changed from the original dsasd.org, how we built it, the tech stack, and who did what.
permalink: /capstone/dsa-portal-build-summary/
sticky_rank: 8
---

<style>
  .bs-wrap {
    max-width: 960px;
    margin: 0 auto;
    font-family: 'Segoe UI', system-ui, sans-serif;
  }

  .bs-card {
    background: #ffffff;
    border: 1px solid #e2e8f0;
    border-radius: 16px;
    padding: 1.5rem 1.6rem;
    margin-bottom: 1.25rem;
    box-shadow: 0 4px 20px rgba(0,0,0,0.06);
  }

  .bs-card h2 {
    color: #0f2847 !important;
    font-size: 1.35rem;
    font-weight: 800;
    border-left: 4px solid #f59e0b;
    padding-left: 14px;
    margin: 0 0 1rem;
  }

  .bs-card h3 {
    color: #1e3a5f !important;
    font-size: 1.05rem;
    font-weight: 700;
    margin: 1.2rem 0 0.5rem;
  }

  .bs-card h4 {
    color: #0f2847 !important;
    font-size: 0.95rem;
    font-weight: 700;
    margin: 0 0 6px;
  }

  .bs-card p {
    color: #1e293b !important;
    line-height: 1.7;
    font-size: 0.92rem;
    margin-bottom: 0.75rem;
  }

  .bs-card strong {
    color: #000000 !important;
  }

  .bs-card ul, .bs-card ol {
    padding-left: 1.2rem;
    margin: 0.5rem 0;
  }

  .bs-card li {
    color: #1e293b !important;
    font-size: 0.88rem;
    line-height: 1.7;
    margin-bottom: 0.4rem;
  }

  .bs-card li strong {
    color: #000000 !important;
  }

  .bs-card code {
    background: none;
    padding: 0;
    border-radius: 0;
    font-size: 0.82rem;
    color: #000000 !important;
  }

  .bs-card blockquote {
    border-left: 3px solid #f59e0b;
    margin: 0.75rem 0;
    padding: 0.5rem 1rem;
    background: #fffbeb;
    border-radius: 0 8px 8px 0;
    color: #1e293b !important;
    font-style: italic;
  }

  /* Hero banner */
  .bs-hero {
    background: linear-gradient(135deg, #0f2847, #1e3a5f);
    border-radius: 16px;
    padding: 2rem 2rem;
    text-align: center;
    margin-bottom: 1.25rem;
    box-shadow: 0 8px 30px rgba(0,0,0,0.15);
  }

  .bs-hero h1 {
    font-size: 1.8rem;
    color: #fbbf24 !important;
    margin-bottom: 6px;
  }

  .bs-hero p {
    color: #94a3b8 !important;
    font-size: 0.95rem;
  }

  .bs-hero .team-names {
    display: flex;
    justify-content: center;
    gap: 24px;
    margin-top: 16px;
    flex-wrap: wrap;
  }

  .bs-hero .team-names span {
    background: rgba(251,191,36,0.12);
    border: 1px solid rgba(251,191,36,0.3);
    padding: 4px 14px;
    border-radius: 20px;
    font-size: 0.82rem;
    font-weight: 600;
    color: #fbbf24 !important;
  }

  /* Stat bar */
  .bs-stat-bar {
    display: flex;
    gap: 16px;
    justify-content: center;
    margin-bottom: 1.25rem;
    flex-wrap: wrap;
  }

  .bs-stat-box {
    background: linear-gradient(135deg, #0f2847, #1e3a5f);
    border-radius: 12px;
    padding: 14px 22px;
    text-align: center;
    box-shadow: 0 4px 16px rgba(0,0,0,0.12);
  }

  .bs-stat-box .s-num {
    font-size: 1.6rem;
    font-weight: 800;
    color: #fbbf24 !important;
  }

  .bs-stat-box .s-lab {
    font-size: 0.68rem;
    color: #94a3b8 !important;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  /* Compare cards */
  .bs-compare {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px;
    margin: 1rem 0;
  }

  .bs-compare-side {
    border-radius: 12px;
    padding: 1.1rem;
    font-size: 0.85rem;
  }

  .bs-compare-old {
    background: #fef2f2;
    border: 1px solid #fecaca;
  }

  .bs-compare-old h4 {
    color: #dc2626 !important;
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 8px;
  }

  .bs-compare-new {
    background: #f0fdf4;
    border: 1px solid #bbf7d0;
  }

  .bs-compare-new h4 {
    color: #16a34a !important;
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 8px;
  }

  .bs-compare-side ul {
    padding-left: 16px;
    margin: 0;
  }

  .bs-compare-side li {
    margin-bottom: 4px;
    font-size: 0.82rem;
    color: #000000 !important;
  }

  /* Feature grid */
  .bs-feat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin: 1rem 0;
  }

  .bs-feat {
    background: #f8fafc;
    border: 1px solid #e2e8f0;
    border-radius: 12px;
    padding: 1.1rem;
  }

  .bs-feat h4 {
    font-size: 0.92rem;
    color: #0f2847 !important;
    margin-bottom: 4px;
  }

  .bs-feat p {
    font-size: 0.82rem;
    color: #000000 !important;
    margin: 0;
  }

  .bs-feat .f-icon {
    font-size: 1.5rem;
    margin-bottom: 4px;
  }

  /* Tech grid */
  .bs-tech-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin: 1rem 0;
  }

  .bs-tech-tag {
    background: linear-gradient(135deg, #0f2847, #1e3a5f);
    border-radius: 10px;
    padding: 14px;
    text-align: center;
  }

  .bs-tech-tag .t-name {
    font-size: 0.82rem;
    font-weight: 700;
    color: #fbbf24 !important;
  }

  .bs-tech-tag .t-desc {
    font-size: 0.7rem;
    color: #94a3b8 !important;
    margin-top: 2px;
  }

  /* Work split */
  .bs-work-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 14px;
    margin: 1rem 0;
  }

  .bs-ws-card {
    border-radius: 12px;
    padding: 1.2rem;
    text-align: center;
  }

  .bs-ws-card h4 {
    font-size: 1rem;
    margin-bottom: 8px;
  }

  .bs-ws-card ul {
    text-align: left;
    padding-left: 16px;
    margin: 0;
  }

  .bs-ws-card li {
    font-size: 0.82rem;
    margin-bottom: 4px;
    color: #000000 !important;
  }

  .bs-ws-akhil { background: #eff6ff; border: 1px solid #bfdbfe; }
  .bs-ws-akhil h4 { color: #1d4ed8 !important; }
  .bs-ws-neil { background: #fef3c7; border: 1px solid #fde68a; }
  .bs-ws-neil h4 { color: #b45309 !important; }
  .bs-ws-moiz { background: #ecfdf5; border: 1px solid #a7f3d0; }
  .bs-ws-moiz h4 { color: #047857 !important; }

  /* Image rows */
  .bs-img-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 14px;
    margin: 1rem 0;
  }

  .bs-img-row.three {
    grid-template-columns: 1fr 1fr 1fr;
  }

  .bs-img-row img {
    width: 100%;
    border-radius: 10px;
    border: 1px solid #e2e8f0;
    display: block;
  }

  .bs-img-cap {
    font-size: 0.72rem;
    color: #64748b !important;
    text-align: center;
    margin-top: 4px;
  }

  /* Tables */
  .bs-table {
    width: 100%;
    border-collapse: collapse;
    margin: 0.75rem 0;
    font-size: 0.82rem;
  }

  .bs-table th {
    background: #0f2847;
    color: #fbbf24 !important;
    padding: 10px 12px;
    text-align: left;
    font-size: 0.72rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .bs-table td {
    padding: 9px 12px;
    border-bottom: 1px solid #e2e8f0;
    color: #000000 !important;
    background: #ffffff;
  }

  .bs-table td strong {
    color: #000000 !important;
  }

  .bs-table td code {
    color: #000000 !important;
    background: none !important;
  }

  .bs-table tr:nth-child(even) td {
    background: #f8fafc;
  }

  /* Global override: kill any theme-level code shading */
  .bs-wrap code,
  .bs-wrap pre,
  .bs-wrap pre code,
  .bs-wrap kbd,
  .bs-wrap samp {
    background: none !important;
    background-color: transparent !important;
    box-shadow: none !important;
    border: none !important;
    color: #000000 !important;
  }

  @media (max-width: 700px) {
    .bs-compare, .bs-feat-grid, .bs-work-grid, .bs-img-row, .bs-img-row.three, .bs-tech-grid { grid-template-columns: 1fr; }
    .bs-card { padding: 1.1rem; }
  }
</style>

<div class="bs-wrap">

<div class="bs-hero">
  <img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Logo" style="width:80px;margin-bottom:12px">
  <h1>DSA Portal Build Summary</h1>
  <p>What we changed from dsasd.org, how we built it, and what's next</p>
  <div class="team-names">
    <span>Akhil</span>
    <span>Neil</span>
    <span>Moiz</span>
  </div>
</div>

<div class="bs-stat-bar">
  <div class="bs-stat-box"><div class="s-num">3</div><div class="s-lab">Core Features</div></div>
  <div class="bs-stat-box"><div class="s-num">7</div><div class="s-lab">Sections Built</div></div>
  <div class="bs-stat-box"><div class="s-num">1</div><div class="s-lab">Page (No Redirects)</div></div>
  <div class="bs-stat-box"><div class="s-num">11</div><div class="s-lab">Real DSA Images</div></div>
  <div class="bs-stat-box"><div class="s-num">AI</div><div class="s-lab">Chatbot Live</div></div>
</div>

<!-- WHAT WE SET OUT TO DO -->
<div class="bs-card">
  <h2>What We Set Out to Do</h2>
  <p>Our <a href="{{site.baseurl}}/capstone/dsa-redesign/" style="color:#0f6996 !important">original proposal</a> identified three major problems with the current dsasd.org:</p>

  <div class="bs-compare">
    <div class="bs-compare-side bs-compare-old">
      <h4>Current dsasd.org Problems</h4>
      <ul>
        <li><strong>9+ menu items</strong> with nested dropdowns</li>
        <li>Members navigate <strong>3-4 pages</strong> to find basic info</li>
        <li>FAQ has only <strong>5 static questions</strong>, no search</li>
        <li>News section shows <strong>2 static cards</strong></li>
        <li>No AI assistance for common questions</li>
        <li>Login page is a <strong>generic WordPress form</strong></li>
        <li>Newsletter only accessible via PDF download</li>
        <li>Mobile nav is <strong>hard to use</strong></li>
      </ul>
    </div>
    <div class="bs-compare-side bs-compare-new">
      <h4>Our Redesigned Portal</h4>
      <ul>
        <li><strong>7 flat nav links</strong> with smooth scroll</li>
        <li>Everything on <strong>1 single page</strong> with inline panels</li>
        <li>FAQ has <strong>9+ questions</strong> with search + category filters</li>
        <li>News section shows <strong>3 image cards</strong> with tags</li>
        <li><strong>AI chatbot</strong> powered by Claude API</li>
        <li>Custom <strong>sheriff-specific login</strong> (badge, rank, station)</li>
        <li>Newsletter <strong>preview cards</strong> with expandable content</li>
        <li><strong>Mobile-responsive</strong> with hamburger menu</li>
      </ul>
    </div>
  </div>
</div>

<!-- FEATURE 1 -->
<div class="bs-card">
  <h2>Feature 1: Interactive Member Dashboard</h2>
  <blockquote>"One Dashboard. Every Resource. Zero Clicks Wasted."</blockquote>

  <div class="bs-img-row">
    <div>
      <img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Dashboard" style="background:#e8ecf0;padding:20px;object-fit:contain;height:200px">
      <div class="bs-img-cap">Dashboard with quick-access resource tiles</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/store-interior.jpg" alt="DSA Store">
      <div class="bs-img-cap">Store section with real DSA HQ photos</div>
    </div>
  </div>

  <h3>What we built:</h3>
  <div class="bs-feat-grid">
    <div class="bs-feat">
      <div class="f-icon">&#128179;</div>
      <h4>Quick-Access Resource Tiles</h4>
      <p>8 tiles (Benefits, Legal, Wellness, Forms, Events, Store, Newsletters, PAC) that expand <strong>inline detail panels</strong> below them &mdash; no page redirects</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128270;</div>
      <h4>Autocomplete Search Bar</h4>
      <p>Type 2+ characters and get instant results that <strong>scroll to the section</strong> and open the relevant detail panel automatically</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128240;</div>
      <h4>Newsletter Preview Cards</h4>
      <p>Past Silver Star issues displayed as <strong>clickable cards</strong> with expandable content previews showing article titles</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128197;</div>
      <h4>Events with RSVP</h4>
      <p>Upcoming events listed with date badges, locations, and <strong>functional RSVP buttons</strong> that update instantly on click</p>
    </div>
  </div>

  <h3>How clicks were minimized:</h3>
  <table class="bs-table">
    <thead>
      <tr><th>Action</th><th>dsasd.org (Before)</th><th>Our Portal (After)</th></tr>
    </thead>
    <tbody>
      <tr><td>Find benefits info</td><td>Menu &rarr; Benefits &rarr; Open Enrollment (3 clicks)</td><td>Click "Benefits" tile &rarr; inline panel (1 click)</td></tr>
      <tr><td>Read newsletter</td><td>Menu &rarr; Silver Star &rarr; PDF download (3 clicks)</td><td>Click "Newsletters" tile &rarr; preview cards (1 click)</td></tr>
      <tr><td>RSVP for event</td><td>Menu &rarr; Events &rarr; Calendar &rarr; Event page (4 clicks)</td><td>Scroll to Events &rarr; click RSVP (1 click)</td></tr>
      <tr><td>Search for info</td><td>Find tiny search icon &rarr; new page (2 clicks)</td><td>Type in header search &rarr; auto-scroll (0 clicks)</td></tr>
      <tr><td>Check legal rights</td><td>Menu &rarr; Member Resources &rarr; Legal page (3 clicks)</td><td>Click "Legal Defense" tile (1 click)</td></tr>
    </tbody>
  </table>
</div>

<!-- FEATURE 2 -->
<div class="bs-card">
  <h2>Feature 2: AI-Powered Smart FAQ Hub</h2>
  <blockquote>"Find Answers Instantly &mdash; Or Chat With Us"</blockquote>

  <div class="bs-feat-grid">
    <div class="bs-feat">
      <div class="f-icon">&#129302;</div>
      <h4>Claude AI Chatbot</h4>
      <p>Floating chat widget powered by <strong>Claude API</strong>. Trained on DSA knowledge: membership, benefits, legal defense, events, store, stations, PAC, and more</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128269;</div>
      <h4>Searchable FAQ</h4>
      <p>9 pre-written Q&As with <strong>instant search filtering</strong> as you type. <strong>Category tags</strong> let you filter by topic</p>
    </div>
  </div>

  <h3>How the chatbot works:</h3>
  <ul>
    <li>User types a question in the chat widget</li>
    <li>Frontend sends the message + last 10 messages to <code>POST /api/sheriff/chat</code></li>
    <li>Backend builds a Claude API request with a comprehensive <strong>system prompt</strong> containing DSA knowledge</li>
    <li>Claude responds with a helpful, professional answer</li>
    <li>Conversation history is maintained for context</li>
  </ul>

  <h3>Chatbot knowledge covers:</h3>
  <ul>
    <li>Organization info, headquarters, contact details</li>
    <li>Membership eligibility, dues, enrollment</li>
    <li>Benefits (medical, dental, vision, life insurance)</li>
    <li>Legal defense fund, Weingarten rights, critical incident protocol</li>
    <li>Wellness programs, peer support, CISM team</li>
    <li>All 12 stations + detention facilities</li>
    <li>Events calendar, golf tournament, family picnic</li>
    <li>DSA Store merchandise, PAC endorsements</li>
    <li>Contract/MOU information, grievance procedures</li>
  </ul>
</div>

<!-- FEATURE 3 -->
<div class="bs-card">
  <h2>Feature 3: Sheriff-Specific Authentication</h2>

  <div class="bs-compare">
    <div class="bs-compare-side bs-compare-old">
      <h4>Old dsasd.org Login</h4>
      <ul>
        <li>Generic WordPress login form</li>
        <li>Username + password only</li>
        <li>No sheriff-specific fields</li>
        <li>Shared user table with all site users</li>
        <li>Basic session cookies</li>
      </ul>
    </div>
    <div class="bs-compare-side bs-compare-new">
      <h4>Our Portal Login</h4>
      <ul>
        <li>Custom modal with <strong>Log In / Sign Up</strong> tabs</li>
        <li>Sheriff-specific fields: <strong>Badge #, Rank, Station</strong></li>
        <li>Separate <code>sheriff_users</code> database table</li>
        <li>Separate <code>jwt_sheriff</code> JWT token cookie</li>
        <li><strong>Admin panel</strong> for viewing all members</li>
        <li>User chip in header shows name + badge on hover</li>
      </ul>
    </div>
  </div>

  <h3>Signup fields we added:</h3>
  <table class="bs-table">
    <thead>
      <tr><th>Field</th><th>Purpose</th></tr>
    </thead>
    <tbody>
      <tr><td>Badge / Sheriff ID</td><td>Unique identifier (e.g., SD-1234)</td></tr>
      <tr><td>Rank</td><td>Deputy, Corporal, Sergeant, Lieutenant, Captain</td></tr>
      <tr><td>Station</td><td>Dropdown of all 12 SD County stations</td></tr>
      <tr><td>Phone</td><td>Contact number for the member</td></tr>
    </tbody>
  </table>
</div>

<!-- IMAGES -->
<div class="bs-card">
  <h2>Real DSA Images Integrated</h2>
  <p>We sourced <strong>11 images</strong> directly from dsasd.org's media library to preserve the organization's visual identity.</p>

  <div class="bs-img-row three">
    <div>
      <img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Logo" style="background:#e8ecf0;padding:10px;object-fit:contain;height:140px">
      <div class="bs-img-cap">Official DSA badge + star logo</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/store-relaunch-flyer.png" alt="Store Relaunch">
      <div class="bs-img-cap">DSA Store Relaunch flyer</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/golf-tournament-flyer.png" alt="Golf Tournament">
      <div class="bs-img-cap">Memorial Golf Tournament flyer</div>
    </div>
  </div>

  <div class="bs-img-row three">
    <div>
      <img src="{{site.baseurl}}/images/dsa/board-portrait.png" alt="Board Member">
      <div class="bs-img-cap">Board & staff portrait</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/memorial-line-of-duty.png" alt="Line of Duty">
      <div class="bs-img-cap">Line of Duty memorial</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/silver-star-newsletter.jpg" alt="Silver Star">
      <div class="bs-img-cap">Silver Star newsletter</div>
    </div>
  </div>

  <div class="bs-img-row">
    <div>
      <img src="{{site.baseurl}}/images/dsa/store-interior.jpg" alt="DSA Store">
      <div class="bs-img-cap">DSA Store interior at HQ</div>
    </div>
    <div>
      <img src="{{site.baseurl}}/images/dsa/golf-tournament-photo.png" alt="Golf">
      <div class="bs-img-cap">Members at the golf tournament</div>
    </div>
  </div>
</div>

<!-- TECH STACK -->
<div class="bs-card">
  <h2>Tech Stack</h2>
  <div class="bs-tech-grid">
    <div class="bs-tech-tag"><div class="t-name">Flask + Python</div><div class="t-desc">Backend API server</div></div>
    <div class="bs-tech-tag"><div class="t-name">SQLAlchemy</div><div class="t-desc">ORM & database</div></div>
    <div class="bs-tech-tag"><div class="t-name">SQLite</div><div class="t-desc">Local dev database</div></div>
    <div class="bs-tech-tag"><div class="t-name">JWT Auth</div><div class="t-desc">Token-based sessions</div></div>
    <div class="bs-tech-tag"><div class="t-name">Claude API</div><div class="t-desc">AI chatbot (Anthropic)</div></div>
    <div class="bs-tech-tag"><div class="t-name">Jekyll</div><div class="t-desc">Static site generator</div></div>
    <div class="bs-tech-tag"><div class="t-name">Vanilla JS</div><div class="t-desc">No framework needed</div></div>
    <div class="bs-tech-tag"><div class="t-name">CSS Grid</div><div class="t-desc">Responsive layouts</div></div>
  </div>

  <h3>Backend API Endpoints:</h3>
  <table class="bs-table">
    <thead>
      <tr><th>Method</th><th>Endpoint</th><th>Purpose</th></tr>
    </thead>
    <tbody>
      <tr><td><code>POST</code></td><td><code>/api/sheriff/authenticate</code></td><td>Login &rarr; returns JWT cookie</td></tr>
      <tr><td><code>DELETE</code></td><td><code>/api/sheriff/authenticate</code></td><td>Logout &rarr; expires cookie</td></tr>
      <tr><td><code>GET</code></td><td><code>/api/sheriff/id</code></td><td>Get current user from token</td></tr>
      <tr><td><code>POST</code></td><td><code>/api/sheriff/user</code></td><td>Create new sheriff (signup)</td></tr>
      <tr><td><code>GET</code></td><td><code>/api/sheriff/user</code></td><td>List all sheriffs (admin only)</td></tr>
      <tr><td><code>PUT</code></td><td><code>/api/sheriff/user</code></td><td>Update sheriff profile</td></tr>
      <tr><td><code>DELETE</code></td><td><code>/api/sheriff/user</code></td><td>Delete sheriff (admin only)</td></tr>
      <tr><td><code>POST</code></td><td><code>/api/sheriff/chat</code></td><td>AI chatbot &rarr; Claude API</td></tr>
    </tbody>
  </table>

  <h3>Key Files:</h3>
  <table class="bs-table">
    <thead>
      <tr><th>File</th><th>Purpose</th></tr>
    </thead>
    <tbody>
      <tr><td><code>cap_back/model/sheriff.py</code></td><td>Sheriff SQLAlchemy model with <code>sheriff_users</code> table</td></tr>
      <tr><td><code>cap_back/api/sheriff.py</code></td><td>Auth + CRUD endpoints with SRP helpers</td></tr>
      <tr><td><code>cap_back/api/sheriff_chat.py</code></td><td>Claude API integration with SRP functions</td></tr>
      <tr><td><code>cap_front/navigation/sheriff/index.md</code></td><td>Full single-page portal UI</td></tr>
    </tbody>
  </table>
</div>

<!-- SRP -->
<div class="bs-card">
  <h2>Code Quality: SRP Refactoring</h2>
  <p>We applied the <strong>Single Responsibility Principle</strong> across all three codebases. See our detailed <a href="{{site.baseurl}}/capstone/dsa-srp-refactoring/" style="color:#0f6996 !important">SRP Refactoring Blog</a> for code comparisons.</p>
  <ul>
    <li><strong>Frontend:</strong> 14 monolithic JS functions &rarr; <strong>30+ focused helpers</strong> (e.g., <code>apiRequest()</code>, <code>showLoggedInUI()</code>, <code>sanitizeHTML()</code>)</li>
    <li><strong>Backend API:</strong> JWT decode duplicated 4x &rarr; <strong>1 shared <code>decode_sheriff_token()</code></strong>; cookie logic 2x &rarr; <strong>1 <code>set_sheriff_cookie()</code></strong></li>
    <li><strong>Chatbot API:</strong> 1 monolithic handler &rarr; <strong>5 single-purpose functions</strong> (<code>validate_chat_request</code>, <code>build_message_history</code>, <code>call_claude_api</code>, <code>parse_claude_response</code>)</li>
  </ul>
</div>

<!-- WORK SPLIT -->
<div class="bs-card">
  <h2>Work Split</h2>
  <div class="bs-work-grid">
    <div class="bs-ws-card bs-ws-akhil">
      <h4>Akhil</h4>
      <ul>
        <li>Backend API architecture</li>
        <li>Sheriff model & database schema</li>
        <li>JWT authentication system</li>
        <li>Claude API chatbot integration</li>
        <li>SRP refactoring (backend)</li>
        <li>API endpoint design</li>
      </ul>
    </div>
    <div class="bs-ws-card bs-ws-neil">
      <h4>Neil</h4>
      <ul>
        <li>UI/UX design & layout</li>
        <li>Single-page architecture</li>
        <li>Search bar with autocomplete</li>
        <li>Login/signup modal design</li>
        <li>Real DSA image integration</li>
        <li>SRP refactoring (frontend JS)</li>
      </ul>
    </div>
    <div class="bs-ws-card bs-ws-moiz">
      <h4>Moiz</h4>
      <ul>
        <li>Events calendar & RSVP</li>
        <li>FAQ search & category filters</li>
        <li>Newsletter preview cards</li>
        <li>Admin panel & member table</li>
        <li>Mobile responsive design</li>
        <li>Blog writeups & documentation</li>
      </ul>
    </div>
  </div>
</div>

<!-- ALL SECTIONS -->
<div class="bs-card">
  <h2>All Sections Built</h2>
  <table class="bs-table">
    <thead>
      <tr><th>Section</th><th>Features</th><th>Click Reduction</th></tr>
    </thead>
    <tbody>
      <tr><td><strong>Hero</strong></td><td>DSA logo, stats (4,229 members / 70+ years / 12 stations / 24/7), CTA buttons</td><td>Landing &rarr; immediate context</td></tr>
      <tr><td><strong>Resources Dashboard</strong></td><td>8 tiles with inline expandable detail panels</td><td>3-4 clicks &rarr; 1 click</td></tr>
      <tr><td><strong>News</strong></td><td>3 cards with images, category tags, dates</td><td>Static page &rarr; scrollable feed</td></tr>
      <tr><td><strong>Events</strong></td><td>6 events with date badges, RSVP buttons, event images</td><td>Calendar page &rarr; inline list</td></tr>
      <tr><td><strong>About</strong></td><td>4 cards: Mission, Stations, Leadership, History with images</td><td>About page &rarr; scrollable section</td></tr>
      <tr><td><strong>Store</strong></td><td>8 product cards + real store photos + relaunch flyer</td><td>Store page &rarr; inline grid</td></tr>
      <tr><td><strong>FAQ</strong></td><td>9 Q&As, search filter, category tags, AI chatbot</td><td>5 static Q&As &rarr; searchable + AI</td></tr>
      <tr><td><strong>Contact</strong></td><td>Staff photos, address/phone/email cards</td><td>Contact page &rarr; inline section</td></tr>
      <tr><td><strong>Newsletter</strong></td><td>Silver Star preview cards with expandable issue contents</td><td>PDF download &rarr; inline preview</td></tr>
      <tr><td><strong>Admin Panel</strong></td><td>Member table (admin only), toggled from user dropdown</td><td>N/A (new feature)</td></tr>
    </tbody>
  </table>
</div>

<!-- WHAT'S NEXT -->
<div class="bs-card">
  <h2>What's Next</h2>
  <table class="bs-table">
    <thead>
      <tr><th>Feature</th><th>Status</th><th>Planned Tech</th></tr>
    </thead>
    <tbody>
      <tr><td>Push notifications for new newsletters</td><td>Planned</td><td>Service Workers, Web Push API</td></tr>
      <tr><td>Personalized dashboard per member</td><td>Planned</td><td>JWT claims + conditional rendering</td></tr>
      <tr><td>Document center with file downloads</td><td>Planned</td><td>Flask file serving, S3 storage</td></tr>
      <tr><td>Integration with dsasd.org WordPress API</td><td>Planned</td><td>WordPress REST API, data sync</td></tr>
      <tr><td>Accessibility audit (WCAG 2.1 AA)</td><td>Planned</td><td>Keyboard nav, ARIA labels, contrast</td></tr>
    </tbody>
  </table>
</div>

<!-- ML PLANS -->
<div class="bs-card">
  <h2>Planned ML Integration</h2>
  <p>We plan to add machine learning features to make the portal smarter and more personalized for DSA members.</p>

  <div class="bs-feat-grid">
    <div class="bs-feat">
      <div class="f-icon">&#129504;</div>
      <h4>Smart Content Recommendations</h4>
      <p>Track which resource tiles, FAQ topics, and newsletter issues each member interacts with, then use <strong>collaborative filtering</strong> to surface the most relevant content on their dashboard</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128200;</div>
      <h4>FAQ Auto-Categorization</h4>
      <p>Use <strong>NLP text classification</strong> (scikit-learn / TF-IDF) to automatically tag and route new member questions to the correct FAQ category or staff contact</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128101;</div>
      <h4>Member Engagement Scoring</h4>
      <p>Build a <strong>logistic regression model</strong> that predicts which members are at risk of disengaging based on login frequency, RSVP history, and resource usage patterns</p>
    </div>
    <div class="bs-feat">
      <div class="f-icon">&#128172;</div>
      <h4>Chatbot Intent Detection</h4>
      <p>Train a lightweight <strong>intent classifier</strong> to detect question categories before sending to Claude API &mdash; enabling faster responses for common queries and reducing API costs</p>
    </div>
  </div>

  <h3>ML Implementation Plan:</h3>
  <table class="bs-table">
    <thead>
      <tr><th>ML Feature</th><th>Model / Approach</th><th>Data Source</th><th>Stack</th></tr>
    </thead>
    <tbody>
      <tr><td>Content recommendations</td><td>Collaborative filtering (item-based)</td><td>User click/interaction logs</td><td>Python, scikit-learn, Flask API</td></tr>
      <tr><td>FAQ auto-categorization</td><td>TF-IDF + Naive Bayes classifier</td><td>Existing FAQ Q&As + chatbot history</td><td>scikit-learn, NLTK</td></tr>
      <tr><td>Engagement scoring</td><td>Logistic regression</td><td>Login timestamps, RSVP data, page views</td><td>pandas, scikit-learn</td></tr>
      <tr><td>Chatbot intent detection</td><td>Text classifier (SVM / logistic)</td><td>Labeled chatbot conversation logs</td><td>scikit-learn, Flask middleware</td></tr>
    </tbody>
  </table>

  <h3>How it connects to the existing portal:</h3>
  <ul>
    <li><strong>Data collection</strong> &mdash; Log user interactions (tile clicks, searches, RSVPs, chat questions) to a new analytics table in the SQLite database</li>
    <li><strong>Model training</strong> &mdash; Run offline training scripts in Python using scikit-learn on the collected interaction data</li>
    <li><strong>Serving predictions</strong> &mdash; Add new Flask API endpoints (e.g., /api/sheriff/recommendations, /api/sheriff/engagement) that return ML predictions</li>
    <li><strong>Frontend integration</strong> &mdash; Dashboard tiles reorder based on recommendation scores; at-risk members get flagged in the admin panel</li>
  </ul>
</div>

</div>
