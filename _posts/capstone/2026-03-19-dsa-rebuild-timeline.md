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
    --dsa-ink: #102033;
    --dsa-muted: #5b6b7f;
    --dsa-line: rgba(12, 49, 84, 0.14);
    --dsa-panel: linear-gradient(180deg, #ffffff 0%, #f5f8fc 100%);
    --dsa-accent: #0d5c8f;
    --dsa-accent-2: #18a0a8;
    --dsa-soft: #e8f4fb;
    --dsa-gold: #f4b544;
    --dsa-shadow: 0 18px 45px rgba(16, 32, 51, 0.10);
    color: var(--dsa-ink);
  }

  .dsa-timeline-page h2,
  .dsa-timeline-page h3,
  .dsa-timeline-page h4 {
    color: var(--dsa-ink);
  }

  .dsa-hero {
    background:
      radial-gradient(circle at top right, rgba(24, 160, 168, 0.22), transparent 32%),
      linear-gradient(135deg, #0b2742 0%, #114b74 55%, #16758d 100%);
    color: #fff;
    border-radius: 28px;
    padding: 2.5rem 2rem;
    box-shadow: var(--dsa-shadow);
    margin: 1.5rem 0 2rem;
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
    background: rgba(255, 255, 255, 0.14);
    margin-bottom: 1rem;
  }

  .dsa-hero h2 {
    color: #fff;
    font-size: clamp(2rem, 4vw, 3rem);
    line-height: 1.05;
    margin-bottom: 0.75rem;
  }

  .dsa-hero p {
    color: rgba(255, 255, 255, 0.88);
    font-size: 1.02rem;
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
  .dsa-milestone {
    background: var(--dsa-panel);
    border: 1px solid rgba(13, 92, 143, 0.10);
    border-radius: 22px;
    box-shadow: var(--dsa-shadow);
  }

  .dsa-stat {
    padding: 1.1rem 1rem;
    background: rgba(255, 255, 255, 0.12);
    border-color: rgba(255, 255, 255, 0.16);
    box-shadow: none;
  }

  .dsa-stat-label {
    display: block;
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: rgba(255, 255, 255, 0.72);
    margin-bottom: 0.35rem;
  }

  .dsa-stat strong {
    font-size: 1.15rem;
    color: #fff;
  }

  .dsa-section-title {
    margin: 2.5rem 0 1rem;
    font-size: 1.6rem;
  }

  .dsa-summary-card {
    padding: 1.35rem 1.4rem;
    margin-bottom: 2rem;
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
    opacity: 0.9;
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
    color: var(--dsa-accent);
    font-size: 0.8rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    padding: 0.4rem 0.7rem;
    border-radius: 999px;
    margin-bottom: 0.55rem;
  }

  .dsa-week-date {
    color: var(--dsa-muted);
    font-weight: 600;
    white-space: nowrap;
  }

  .dsa-week-card h3 {
    margin: 0 0 0.4rem;
    font-size: 1.35rem;
  }

  .dsa-focus {
    color: var(--dsa-accent);
    font-weight: 700;
    margin-bottom: 0.65rem;
  }

  .dsa-week-card ul {
    margin: 0.75rem 0 0;
    padding-left: 1.1rem;
  }

  .dsa-week-card li {
    margin-bottom: 0.45rem;
    color: #1c3147;
  }

  .dsa-team-card {
    padding: 1.3rem;
  }

  .dsa-team-card h4 {
    margin-bottom: 0.45rem;
  }

  .dsa-role-tag {
    display: inline-block;
    font-size: 0.76rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--dsa-accent);
    background: var(--dsa-soft);
    border-radius: 999px;
    padding: 0.35rem 0.65rem;
    margin-bottom: 0.8rem;
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
  }

  .dsa-ownership-table th {
    background: #103a5d;
    color: #fff;
    font-weight: 700;
  }

  .dsa-ownership-table td {
    background: #fff;
    color: #173047;
  }

  .dsa-milestone {
    padding: 1.5rem;
    margin-top: 2rem;
    border-left: 8px solid var(--dsa-gold);
  }

  .dsa-milestone p:last-child {
    margin-bottom: 0;
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
      This is our ideal 5-week roadmap for rebuilding the Deputy Sheriffs' Association website. The plan keeps the same core milestones, but adds clearer deliverables for what we will design, build, test, and present each week.
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
      The rebuild moves from early prototypes into a working full-stack website, then into polish and final presentation. Across the five weeks, we will cover homepage redesign, navigation improvements, member portal UX, FAQ structure, contact flow, API and authentication work, responsive frontend implementation, accessibility checks, QA, and stakeholder-facing delivery materials.
    </p>
  </section>

  <h2 class="dsa-section-title">Rebuild Timeline</h2>

  <div class="dsa-timeline">
    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 1</span>
          <h3>Prototype and Scope Lock</h3>
        </div>
        <div class="dsa-week-date">March 23-27, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Rapid prototypes of key features</div>
      <p>
        We begin by shaping the core user experience and confirming what the rebuild needs to include before development gets too deep.
      </p>
      <ul>
        <li>Clickable UI prototypes for the homepage, member portal dashboard, FAQ hub, and contact flow.</li>
        <li>Feature list locked and scope confirmed so the team knows exactly what the final build must deliver.</li>
        <li>Early navigation, content hierarchy, and page-to-page user flow decisions mapped out.</li>
        <li>Initial technical planning for backend routes, data needs, and integration points.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 2</span>
          <h3>Design System and Frontend Foundation</h3>
        </div>
        <div class="dsa-week-date">March 30-April 3, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Design system + frontend foundation</div>
      <p>
        After the concept is approved, we translate prototypes into a reusable visual and technical system that the whole site can build on.
      </p>
      <ul>
        <li>Final UI kit established with colors, typography, spacing, card patterns, buttons, and layout rules.</li>
        <li>Responsive page skeletons created and wired to mock data to test layout behavior across desktop and mobile.</li>
        <li>Navigation shell, reusable components, and content sections prepared for later API integration.</li>
        <li>Content inventory and QA review used to catch missing assets or unclear copy early.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 3</span>
          <h3>Core Build and Integrations</h3>
        </div>
        <div class="dsa-week-date">April 6-10, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Core build: backend + integrations</div>
      <p>
        This is the production-heavy week where the rebuild shifts from mockups into a working system.
      </p>
      <ul>
        <li>Authentication, member data endpoints, and content management hooks implemented.</li>
        <li>Frontend components connected to live APIs so the portal and dynamic site areas reflect real data.</li>
        <li>Error handling, edge cases, and integration logic reviewed while the main flows are still being built.</li>
        <li>Core functionality validated against the original scope to keep the final sprint focused on polish instead of rework.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 4</span>
          <h3>Polish, QA, and Accessibility</h3>
        </div>
        <div class="dsa-week-date">April 13-17, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Polish + QA</div>
      <p>
        With the main functionality in place, the team shifts to quality, consistency, and readiness for external review.
      </p>
      <ul>
        <li>Accessibility pass completed for readability, structure, contrast, navigation clarity, and usability.</li>
        <li>Performance tuning, bug fixing, and load checks reduce friction across devices and browsers.</li>
        <li>Cross-device testing verifies mobile responsiveness and overall visual consistency.</li>
        <li>Content review ensures the site feels complete, accurate, and aligned with stakeholder expectations.</li>
      </ul>
    </article>

    <article class="dsa-week-card">
      <div class="dsa-week-top">
        <div>
          <span class="dsa-week-chip">Week 5</span>
          <h3>Final Package and Stakeholder Outreach</h3>
        </div>
        <div class="dsa-week-date">April 20-24, 2026</div>
      </div>
      <div class="dsa-focus">Focus: Final package + stakeholder outreach</div>
      <p>
        The last week is about packaging the work professionally and preparing for presentation to the Deputy Sheriffs' Association.
      </p>
      <ul>
        <li>Final build packaged and deployment-ready with a clean handoff plan.</li>
        <li>Demo script, talking points, and presentation deck prepared to communicate the redesign clearly.</li>
        <li>Final design tweaks applied so the experience feels polished and intentional.</li>
        <li>Outreach to the Deputy Sheriffs' Association scheduled with a presentation-ready deliverable set.</li>
      </ul>
    </article>
  </div>

  <h2 class="dsa-section-title">Work Split (3 Members)</h2>

  <div class="dsa-team-grid">
    <section class="dsa-team-card">
      <span class="dsa-role-tag">Moiz · Backend</span>
      <h4>System and Data Ownership</h4>
      <p>
        API design, authentication, data models, integration with member data, and deployment readiness.
      </p>
    </section>

    <section class="dsa-team-card">
      <span class="dsa-role-tag">Neil · UI</span>
      <h4>Interface and Experience</h4>
      <p>
        Visual system, UI prototypes, responsive layouts, and final frontend polish.
      </p>
    </section>

    <section class="dsa-team-card">
      <span class="dsa-role-tag">Akhil · All-rounder</span>
      <h4>Support, QA, and Delivery</h4>
      <p>
        Full-stack support wherever needed, QA and testing, and stakeholder presentation materials.
      </p>
    </section>
  </div>

  <h2 class="dsa-section-title">Weekly Ownership Snapshot</h2>

  <table class="dsa-ownership-table">
    <thead>
      <tr>
        <th>Week (Dates)</th>
        <th>Moiz</th>
        <th>Neil</th>
        <th>Akhil</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Week 1</strong><br>March 23-27, 2026</td>
        <td>Prototype backend routes + data model sketch</td>
        <td>Clickable UI prototypes</td>
        <td>UX flow review + feedback synthesis</td>
      </tr>
      <tr>
        <td><strong>Week 2</strong><br>March 30-April 3, 2026</td>
        <td>API scaffolding + auth plan</td>
        <td>Design system + page skeletons</td>
        <td>QA on prototypes + content inventory</td>
      </tr>
      <tr>
        <td><strong>Week 3</strong><br>April 6-10, 2026</td>
        <td>Implement auth + member endpoints</td>
        <td>Integrate UI with APIs</td>
        <td>Fixes, edge cases, and test coverage</td>
      </tr>
      <tr>
        <td><strong>Week 4</strong><br>April 13-17, 2026</td>
        <td>Load/perf checks + logging</td>
        <td>Final UI polish + accessibility</td>
        <td>Cross-device QA + content review</td>
      </tr>
      <tr>
        <td><strong>Week 5</strong><br>April 20-24, 2026</td>
        <td>Deployment checklist + handoff</td>
        <td>Final design tweaks</td>
        <td>Demo script + stakeholder outreach</td>
      </tr>
    </tbody>
  </table>

  <section class="dsa-milestone">
    <h2>Final Milestone</h2>
    <p>
      By <strong>April 24, 2026</strong>, we will have a complete, polished rebuild ready for presentation and formal outreach to the Deputy Sheriffs' Association.
    </p>
    <p>
      The final result is not just a coded website, but a full capstone package: working product, tested experience, clear design system, and a presentation-ready story of the rebuild.
    </p>
  </section>
</div>
