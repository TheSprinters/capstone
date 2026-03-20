---
toc: false
layout: post
title: DSA Portal Build Summary — TheSprinters
description: A complete summary of the Deputy Sheriffs' Association portal redesign — what we changed from the original dsasd.org, how we built it, the tech stack, and who did what.
permalink: /capstone/dsa-portal-build-summary/
sticky_rank: 8
---

<style>
  .dsa-sum{max-width:960px;margin:0 auto;font-family:'Segoe UI',system-ui,sans-serif;color:#000000 !important;line-height:1.7}
  .dsa-sum h2{color:#0f2847 !important;border-left:4px solid #f59e0b;padding-left:14px;margin-top:2.2rem;font-size:1.4rem}
  .dsa-sum h3{color:#1e3a5f !important;margin-top:1.4rem;font-size:1.1rem}
  .dsa-sum p,.dsa-sum li,.dsa-sum td,.dsa-sum strong,.dsa-sum em,.dsa-sum blockquote{color:#000000 !important}
  .dsa-sum hr{border-color:#e2e8f0}
  .dsa-sum .hero-banner{background:linear-gradient(135deg,#0f2847,#1e3a5f);border-radius:16px;padding:36px 30px;text-align:center;color:#e2e8f0 !important;margin-bottom:28px}
  .dsa-sum .hero-banner h1{font-size:1.8rem;color:#fbbf24 !important;margin-bottom:6px}
  .dsa-sum .hero-banner p{color:#94a3b8 !important;font-size:0.95rem}
  .dsa-sum .hero-banner .team-names{display:flex;justify-content:center;gap:32px;margin-top:16px;flex-wrap:wrap}
  .dsa-sum .hero-banner .team-names span{background:rgba(251,191,36,0.12);border:1px solid rgba(251,191,36,0.3);padding:4px 14px;border-radius:20px;font-size:0.82rem;font-weight:600;color:#fbbf24 !important}
  .dsa-sum .img-row{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin:16px 0}
  .dsa-sum .img-row.three{grid-template-columns:1fr 1fr 1fr}
  .dsa-sum .img-row img{width:100%;border-radius:10px;border:1px solid #e2e8f0;display:block}
  .dsa-sum .img-cap{font-size:0.72rem;color:#64748b !important;text-align:center;margin-top:4px}
  .dsa-sum .compare-card{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin:16px 0}
  .dsa-sum .cc-side{border-radius:12px;padding:18px;font-size:0.85rem}
  .dsa-sum .cc-old{background:#fef2f2;border:1px solid #fecaca}
  .dsa-sum .cc-old h4{color:#dc2626 !important;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px}
  .dsa-sum .cc-new{background:#f0fdf4;border:1px solid #bbf7d0}
  .dsa-sum .cc-new h4{color:#16a34a !important;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px}
  .dsa-sum .cc-side ul{padding-left:16px;margin:0}
  .dsa-sum .cc-side li{margin-bottom:4px;font-size:0.82rem;color:#000000 !important}
  .dsa-sum .cc-side li strong{color:#000000 !important}
  .dsa-sum .feature-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin:16px 0}
  .dsa-sum .feat{background:#f8fafc;border:1px solid #e2e8f0;border-radius:12px;padding:18px}
  .dsa-sum .feat h4{font-size:0.95rem;color:#0f2847 !important;margin-bottom:6px}
  .dsa-sum .feat p{font-size:0.82rem;color:#000000 !important;margin:0}
  .dsa-sum .feat p strong{color:#000000 !important}
  .dsa-sum .feat .f-icon{font-size:1.6rem;margin-bottom:6px}
  .dsa-sum .tech-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin:16px 0}
  .dsa-sum .tech-tag{background:linear-gradient(135deg,#0f2847,#1e3a5f);border-radius:10px;padding:14px;text-align:center}
  .dsa-sum .tech-tag .t-name{font-size:0.82rem;font-weight:700;color:#fbbf24 !important}
  .dsa-sum .tech-tag .t-desc{font-size:0.7rem;color:#94a3b8 !important;margin-top:2px}
  .dsa-sum .work-split{display:grid;grid-template-columns:1fr 1fr 1fr;gap:14px;margin:16px 0}
  .dsa-sum .ws-card{border-radius:12px;padding:18px;text-align:center}
  .dsa-sum .ws-card h4{font-size:1rem;margin-bottom:8px}
  .dsa-sum .ws-card ul{text-align:left;padding-left:16px;margin:0}
  .dsa-sum .ws-card li{font-size:0.8rem;margin-bottom:4px;color:#000000 !important}
  .dsa-sum .ws-akhil{background:#eff6ff;border:1px solid #bfdbfe}
  .dsa-sum .ws-akhil h4{color:#1d4ed8 !important}
  .dsa-sum .ws-neil{background:#fef3c7;border:1px solid #fde68a}
  .dsa-sum .ws-neil h4{color:#b45309 !important}
  .dsa-sum .ws-moiz{background:#ecfdf5;border:1px solid #a7f3d0}
  .dsa-sum .ws-moiz h4{color:#047857 !important}
  .dsa-sum .stat-bar{display:flex;gap:20px;justify-content:center;margin:16px 0;flex-wrap:wrap}
  .dsa-sum .stat-box{background:#0f2847;border-radius:10px;padding:14px 22px;text-align:center}
  .dsa-sum .stat-box .s-num{font-size:1.6rem;font-weight:800;color:#fbbf24 !important}
  .dsa-sum .stat-box .s-lab{font-size:0.68rem;color:#94a3b8 !important;text-transform:uppercase;letter-spacing:0.5px}
  .dsa-sum table{width:100%;border-collapse:collapse;margin:12px 0;font-size:0.82rem}
  .dsa-sum th{background:#0f2847;color:#fbbf24 !important;padding:10px 12px;text-align:left;font-size:0.72rem;text-transform:uppercase;letter-spacing:0.5px}
  .dsa-sum td{padding:8px 12px;border-bottom:1px solid #e2e8f0;color:#000000 !important}
  .dsa-sum td strong{color:#000000 !important}
  .dsa-sum td code{color:#334155 !important}
  .dsa-sum tr:nth-child(even){background:#f8fafc}
  .dsa-sum code{background:#f1f5f9;padding:1px 5px;border-radius:4px;font-size:0.8rem;color:#334155 !important}
  .dsa-sum a{color:#0f6996 !important}
  @media(max-width:700px){
    .dsa-sum .compare-card,.dsa-sum .feature-grid,.dsa-sum .work-split,.dsa-sum .img-row,.dsa-sum .img-row.three,.dsa-sum .tech-grid{grid-template-columns:1fr}
  }
</style>

<div class="dsa-sum">

<div class="hero-banner">
  <img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Logo" style="width:80px;margin-bottom:12px">
  <h1>DSA Portal Build Summary</h1>
  <p>What we changed from dsasd.org, how we built it, and what's next</p>
  <div class="team-names">
    <span>Akhil</span>
    <span>Neil</span>
    <span>Moiz</span>
  </div>
</div>

<div class="stat-bar">
  <div class="stat-box"><div class="s-num">3</div><div class="s-lab">Core Features</div></div>
  <div class="stat-box"><div class="s-num">7</div><div class="s-lab">Sections Built</div></div>
  <div class="stat-box"><div class="s-num">1</div><div class="s-lab">Page (No Redirects)</div></div>
  <div class="stat-box"><div class="s-num">11</div><div class="s-lab">Real DSA Images</div></div>
  <div class="stat-box"><div class="s-num">AI</div><div class="s-lab">Chatbot Live</div></div>
</div>

---

## What We Set Out to Do

Our [original proposal]({{site.baseurl}}/capstone/dsa-redesign/) identified three major problems with the current dsasd.org:

<div class="compare-card">
<div class="cc-side cc-old">
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
<div class="cc-side cc-new">
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

---

## Feature 1: Interactive Member Dashboard

> *"One Dashboard. Every Resource. Zero Clicks Wasted."*

<div class="img-row">
<div>
<img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Dashboard" style="background:#e8ecf0;padding:20px;object-fit:contain;height:200px">
<div class="img-cap">Dashboard with quick-access resource tiles</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/store-interior.jpg" alt="DSA Store">
<div class="img-cap">Store section with real DSA HQ photos</div>
</div>
</div>

### What we built:

<div class="feature-grid">
<div class="feat">
<div class="f-icon">&#128179;</div>
<h4>Quick-Access Resource Tiles</h4>
<p>8 tiles (Benefits, Legal, Wellness, Forms, Events, Store, Newsletters, PAC) that expand <strong>inline detail panels</strong> below them &mdash; no page redirects</p>
</div>
<div class="feat">
<div class="f-icon">&#128270;</div>
<h4>Autocomplete Search Bar</h4>
<p>Type 2+ characters and get instant results that <strong>scroll to the section</strong> and open the relevant detail panel automatically</p>
</div>
<div class="feat">
<div class="f-icon">&#128240;</div>
<h4>Newsletter Preview Cards</h4>
<p>Past Silver Star issues displayed as <strong>clickable cards</strong> with expandable content previews showing article titles inside each issue</p>
</div>
<div class="feat">
<div class="f-icon">&#128197;</div>
<h4>Events with RSVP</h4>
<p>Upcoming events listed with date badges, locations, and <strong>functional RSVP buttons</strong> that update instantly on click</p>
</div>
</div>

### How clicks were minimized:

| Action | dsasd.org (Before) | Our Portal (After) |
|--------|:---:|:---:|
| Find benefits info | Menu &rarr; Benefits &rarr; Open Enrollment page (3 clicks) | Click "Benefits" tile &rarr; inline panel (1 click) |
| Read newsletter | Menu &rarr; Silver Star &rarr; PDF download (3 clicks) | Click "Newsletters" tile &rarr; preview cards (1 click) |
| RSVP for event | Menu &rarr; Events &rarr; Calendar &rarr; Event page (4 clicks) | Scroll to Events &rarr; click RSVP (1 click) |
| Search for info | Find tiny search icon &rarr; new page (2 clicks) | Type in header search &rarr; auto-scroll (0 clicks) |
| Check legal rights | Menu &rarr; Member Resources &rarr; Legal page (3 clicks) | Click "Legal Defense" tile (1 click) |

---

## Feature 2: AI-Powered Smart FAQ Hub

> *"Find Answers Instantly &mdash; Or Chat With Us"*

<div class="feature-grid">
<div class="feat">
<div class="f-icon">&#129302;</div>
<h4>Claude AI Chatbot</h4>
<p>Floating chat widget in the bottom-right corner powered by <strong>Claude API</strong>. Trained on DSA knowledge: membership, benefits, legal defense, events, store, stations, PAC, and more</p>
</div>
<div class="feat">
<div class="f-icon">&#128269;</div>
<h4>Searchable FAQ</h4>
<p>9 pre-written Q&As with <strong>instant search filtering</strong> as you type. <strong>Category tags</strong> (Membership, Benefits, Legal, Events, Store) let you filter by topic</p>
</div>
</div>

### How the chatbot works:

- User types a question in the chat widget
- Frontend sends the message + last 10 messages of history to `POST /api/sheriff/chat`
- Backend builds a Claude API request with a comprehensive **system prompt** containing DSA knowledge
- Claude responds with a helpful, professional answer
- Conversation history is maintained for context

### Chatbot knowledge covers:
- Organization info, headquarters, contact details
- Membership eligibility, dues, enrollment
- Benefits (medical, dental, vision, life insurance)
- Legal defense fund, Weingarten rights, critical incident protocol
- Wellness programs, peer support, CISM team
- All 12 stations + detention facilities
- Events calendar, golf tournament, family picnic
- DSA Store merchandise, PAC endorsements
- Contract/MOU information, grievance procedures

---

## Feature 3: Sheriff-Specific Authentication

<div class="compare-card">
<div class="cc-side cc-old">
<h4>Old dsasd.org Login</h4>
<ul>
<li>Generic WordPress login form</li>
<li>Username + password only</li>
<li>No sheriff-specific fields</li>
<li>Shared user table with all site users</li>
<li>Basic session cookies</li>
</ul>
</div>
<div class="cc-side cc-new">
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

### Signup fields we added (that the original site doesn't have):

| Field | Purpose |
|-------|---------|
| Badge / Sheriff ID | Unique identifier (e.g., SD-1234) |
| Rank | Deputy, Corporal, Sergeant, Lieutenant, Captain |
| Station | Dropdown of all 12 SD County stations |
| Phone | Contact number for the member |

---

## Real DSA Images Integrated

We sourced **11 images** directly from dsasd.org's media library to preserve the organization's visual identity:

<div class="img-row three">
<div>
<img src="{{site.baseurl}}/images/dsa/dsa-logo.png" alt="DSA Logo" style="background:#e8ecf0;padding:10px;object-fit:contain;height:140px">
<div class="img-cap">Official DSA badge + star logo</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/store-relaunch-flyer.png" alt="Store Relaunch">
<div class="img-cap">DSA Store Relaunch flyer</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/golf-tournament-flyer.png" alt="Golf Tournament">
<div class="img-cap">Memorial Golf Tournament flyer</div>
</div>
</div>

<div class="img-row three">
<div>
<img src="{{site.baseurl}}/images/dsa/board-portrait.png" alt="Board Member">
<div class="img-cap">Board & staff portrait</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/memorial-line-of-duty.png" alt="Line of Duty">
<div class="img-cap">Line of Duty memorial</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/silver-star-newsletter.jpg" alt="Silver Star">
<div class="img-cap">Silver Star newsletter</div>
</div>
</div>

<div class="img-row">
<div>
<img src="{{site.baseurl}}/images/dsa/store-interior.jpg" alt="DSA Store">
<div class="img-cap">DSA Store interior at HQ</div>
</div>
<div>
<img src="{{site.baseurl}}/images/dsa/golf-tournament-photo.png" alt="Golf">
<div class="img-cap">Members at the golf tournament</div>
</div>
</div>

---

## Tech Stack

<div class="tech-grid">
<div class="tech-tag"><div class="t-name">Flask + Python</div><div class="t-desc">Backend API server</div></div>
<div class="tech-tag"><div class="t-name">SQLAlchemy</div><div class="t-desc">ORM & database</div></div>
<div class="tech-tag"><div class="t-name">SQLite</div><div class="t-desc">Local dev database</div></div>
<div class="tech-tag"><div class="t-name">JWT Auth</div><div class="t-desc">Token-based sessions</div></div>
<div class="tech-tag"><div class="t-name">Claude API</div><div class="t-desc">AI chatbot (Anthropic)</div></div>
<div class="tech-tag"><div class="t-name">Jekyll</div><div class="t-desc">Static site generator</div></div>
<div class="tech-tag"><div class="t-name">Vanilla JS</div><div class="t-desc">No framework needed</div></div>
<div class="tech-tag"><div class="t-name">CSS Grid</div><div class="t-desc">Responsive layouts</div></div>
</div>

### Backend API endpoints we built:

| Method | Endpoint | Purpose |
|--------|----------|---------|
| `POST` | `/api/sheriff/authenticate` | Login &rarr; returns JWT cookie |
| `DELETE` | `/api/sheriff/authenticate` | Logout &rarr; expires cookie |
| `GET` | `/api/sheriff/id` | Get current user from token |
| `POST` | `/api/sheriff/user` | Create new sheriff (signup) |
| `GET` | `/api/sheriff/user` | List all sheriffs (admin only) |
| `PUT` | `/api/sheriff/user` | Update sheriff profile |
| `DELETE` | `/api/sheriff/user` | Delete sheriff (admin only) |
| `POST` | `/api/sheriff/chat` | AI chatbot &rarr; Claude API |

### Key files:

| File | Purpose |
|------|---------|
| `cap_back/model/sheriff.py` | Sheriff SQLAlchemy model with `sheriff_users` table |
| `cap_back/api/sheriff.py` | Auth + CRUD endpoints with SRP helpers |
| `cap_back/api/sheriff_chat.py` | Claude API integration with SRP functions |
| `cap_front/navigation/sheriff/index.md` | Full single-page portal UI |

---

## Code Quality: SRP Refactoring

We applied the **Single Responsibility Principle** across all three codebases. See our detailed [SRP Refactoring Blog]({{site.baseurl}}/capstone/dsa-srp-refactoring/) for code comparisons.

**Key improvements:**
- **Frontend:** 14 monolithic JS functions &rarr; **30+ focused helpers** (e.g., `apiRequest()`, `showLoggedInUI()`, `sanitizeHTML()`, `getChatInput()`)
- **Backend API:** JWT decode duplicated 4x &rarr; **1 shared `decode_sheriff_token()` function**; cookie logic 2x &rarr; **1 `set_sheriff_cookie()` function**
- **Chatbot API:** 1 monolithic handler &rarr; **5 single-purpose functions** (`validate_chat_request`, `build_message_history`, `call_claude_api`, `parse_claude_response`)

---

## Work Split

<div class="work-split">
<div class="ws-card ws-akhil">
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
<div class="ws-card ws-neil">
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
<div class="ws-card ws-moiz">
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

---

## All Sections Built

| Section | Features | Click Reduction |
|---------|----------|:---:|
| **Hero** | DSA logo, stats (4,229 members / 70+ years / 12 stations / 24/7), CTA buttons | Landing &rarr; immediate context |
| **Resources Dashboard** | 8 tiles with inline expandable detail panels | 3-4 clicks &rarr; 1 click |
| **News** | 3 cards with images, category tags, dates | Static page &rarr; scrollable feed |
| **Events** | 6 events with date badges, RSVP buttons, event images | Calendar page &rarr; inline list |
| **About** | 4 cards: Mission, Stations, Leadership, History with images | About page &rarr; scrollable section |
| **Store** | 8 product cards + real store photos + relaunch flyer | Store page &rarr; inline grid |
| **FAQ** | 9 Q&As, search filter, category tags, AI chatbot | 5 static Q&As &rarr; searchable + AI |
| **Contact** | Staff photos, address/phone/email cards | Contact page &rarr; inline section |
| **Newsletter** | Silver Star preview cards with expandable issue contents | PDF download &rarr; inline preview |
| **Admin Panel** | Member table (admin only), toggled from user dropdown | N/A (new feature) |

---

## What's Next

| Feature | Status | Planned Tech |
|---------|--------|-------------|
| Push notifications for new newsletters | Planned | Service Workers, Web Push API |
| Personalized dashboard per member | Planned | JWT claims + conditional rendering |
| Document center with file downloads | Planned | Flask file serving, S3 storage |
| Integration with dsasd.org WordPress API | Planned | WordPress REST API, data sync |
| Accessibility audit (WCAG 2.1 AA) | Planned | Keyboard nav, ARIA labels, contrast |

</div>
