---
layout: default
title: "Humaira's Labs"
---

<div class="lab-shell">

  <header class="lab-header">
    <svg class="lab-wires" viewBox="0 0 360 420" aria-hidden="true" focusable="false">
      <defs>
        <linearGradient id="lw" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0" stop-color="#ff3d9a"/>
          <stop offset="0.6" stop-color="#8a5cff"/>
          <stop offset="1" stop-color="#2fd8ff"/>
        </linearGradient>
      </defs>
      <g fill="none" stroke="url(#lw)" stroke-linecap="round">
        <path stroke-width="2.4" d="M40 0 C 30 80, 70 120, 55 200 S 40 320, 60 380"/>
        <path stroke-width="1.6" d="M90 0 C 100 90, 60 150, 85 230 S 110 330, 95 400"/>
        <path stroke-width="2.2" d="M140 0 C 130 60, 170 130, 150 210 S 130 300, 150 360"/>
        <path stroke-width="1.4" d="M190 0 C 200 100, 160 170, 185 250 S 215 340, 200 410"/>
        <path stroke-width="2.4" d="M240 0 C 235 70, 275 140, 255 220 S 235 310, 258 390"/>
        <path stroke-width="1.6" d="M290 0 C 300 60, 270 120, 290 190 S 310 280, 295 340"/>
        <path stroke-width="2" d="M335 0 C 325 90, 345 150, 332 230"/>
      </g>
      <g fill="#ffffff">
        <circle cx="60" cy="380" r="4"/>
        <circle cx="95" cy="400" r="3"/>
        <circle cx="150" cy="360" r="4"/>
        <circle cx="200" cy="410" r="3"/>
        <circle cx="258" cy="390" r="4"/>
        <circle cx="295" cy="340" r="3"/>
        <circle cx="332" cy="230" r="4"/>
      </g>
    </svg>

    <div class="lab-eyebrow">
      <span class="lab-status-dot"></span>
      PERSONAL RESEARCH ARCHIVE / 2026
      <span class="lab-jp">ヒューマイラ研究所</span>
    </div>

    <h1 class="lab-title">HUMAIRA<span>'S</span> LABS</h1>

    <p class="lab-subtitle">
      Explore the unknown. Document the process.
    </p>

    <p class="lab-intro">
      A living archive of computer science, algorithms,
      systems, mathematics, and ideas worth investigating.
    </p>

    <nav class="lab-nav" aria-label="Main navigation">
      <a href="#archive">ARCHIVE</a>
      <a href="#recent-notes">FIELD NOTES</a>
      <a href="#about">ABOUT</a>
    </nav>
  </header>

  <section class="lab-section" id="archive">
    <div class="lab-section-heading">
      <div>
        <span class="lab-kicker">01 / KNOWLEDGE SYSTEMS</span>
        <h2>Research Archive</h2>
      </div>
      <span class="lab-counter">
        {{ site.posts | size }} RECORDS
      </span>
    </div>

    {% assign categories = site.posts
      | map: "categories"
      | join: ","
      | split: ","
      | uniq
      | sort %}

    <div class="lab-archive-grid">
      {% for category in categories %}
        {% assign category_posts = site.posts
          | where_exp: "post", "post.categories contains category" %}

        {% if category != "" %}
          <article class="lab-category-card">
            <div class="lab-card-top">
              <span class="lab-card-symbol">✳</span>
              <span class="lab-card-index">
                {{ forloop.index | prepend: "00" | slice: -2, 2 }}
              </span>
            </div>

            <h3>{{ category | replace: "-", " " }}</h3>

            <p class="lab-card-description">
              Explore notes, concepts, and technical discoveries.
            </p>

            <div class="lab-card-bottom">
              <span>{{ category_posts.size }} NOTES</span>
              <a
                href="#category-{{ category | slugify }}"
                aria-label="Explore {{ category }} notes"
              >EXPLORE ↗</a>
            </div>
          </article>
        {% endif %}
      {% endfor %}
    </div>
  </section>

  <section class="lab-section" id="recent-notes">
    <div class="lab-section-heading">
      <div>
        <span class="lab-kicker">02 / LATEST DISCOVERIES</span>
        <h2>Recent Field Notes</h2>
      </div>
      <span class="lab-counter">LIVE ARCHIVE</span>
    </div>

    <div class="lab-note-list">
      {% for post in site.posts limit:10 %}
        <a class="lab-note" href="{{ post.url | relative_url }}">
          <div class="lab-note-marker"></div>

          <div class="lab-note-content">
            <span class="lab-note-category">
              {{ post.categories | join: " / " | default: "GENERAL" }}
            </span>

            <h3>{{ post.title | escape }}</h3>

            {% if post.excerpt %}
              <p>{{ post.excerpt | strip_html | strip_newlines | truncate: 120 }}</p>
            {% endif %}
          </div>

          <time class="lab-note-date"
            datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%d %b %Y" }}
          </time>

          <span class="lab-note-arrow">↗</span>
        </a>
      {% endfor %}
    </div>
  </section>

  <section class="lab-section lab-category-index">
    <div class="lab-section-heading">
      <div>
        <span class="lab-kicker">03 / SUBJECT INDEX</span>
        <h2>Explore by Discipline</h2>
      </div>
    </div>

    {% for category in categories %}
      {% assign category_posts = site.posts
        | where_exp: "post", "post.categories contains category" %}

      {% if category != "" %}
        <div class="lab-discipline" id="category-{{ category | slugify }}">
          <div class="lab-discipline-heading">
            <h3>{{ category | replace: "-", " " }}</h3>
            <span>{{ category_posts.size }} NOTES</span>
          </div>

          <ul>
            {% for post in category_posts %}
              <li>
                <a href="{{ post.url | relative_url }}">
                  {{ post.title | escape }}
                </a>
                <time datetime="{{ post.date | date_to_xmlschema }}">
                  {{ post.date | date: "%d %b %Y" }}
                </time>
              </li>
            {% endfor %}
          </ul>
        </div>
      {% endif %}
    {% endfor %}
  </section>

  <section class="lab-about" id="about">
    <span class="lab-kicker">04 / THE RESEARCHER</span>
    <h2>Curiosity is the starting point.</h2>
    <p>
      This is my personal laboratory for understanding how things work:
      from the foundations of computation to the systems we build on top.
      Every note is a step toward deeper understanding.
    </p>
    <span class="lab-about-signature">HUMAIRA / END OF TRANSMISSION</span>
  </section>

  <footer class="lab-footer">
    <span>HUMAIRA'S LABS</span>
    <span>BUILT THROUGH CURIOSITY · {{ site.time | date: "%Y" }}</span>
  </footer>

</div>

<style>
/* HUMAIRA'S LABS — NEON MANGA CYBER ARCHIVE */
@import url("https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@500;700&family=IBM+Plex+Mono:wght@400;500&family=Inter:wght@400;500&family=Noto+Sans+JP:wght@500&display=swap");

html {
  background:
    radial-gradient(900px 560px at 100% 0%, rgba(255, 61, 154, .26), transparent 62%),
    radial-gradient(900px 600px at 0% 12%, rgba(75, 70, 255, .30), transparent 62%),
    radial-gradient(800px 500px at 20% 100%, rgba(47, 216, 255, .13), transparent 62%),
    #06050f !important;
  background-attachment: fixed !important;
  min-height: 100%;
}

body {
  background: transparent !important;
  color: #ece8fb !important;
}

.site-header, .site-footer { border-color: rgba(255, 255, 255, .12) !important; }
.site-title, .site-title:visited, .site-nav .page-link, .site-footer, .site-footer a { color: #9a95bd !important; }

.lab-shell {
  --panel: rgba(16, 12, 32, .88);
  --text: #ece8fb;
  --muted: #9a95bd;
  --line: rgba(255, 255, 255, .14);
  --mag: #ff3d9a;
  --vio: #7b61ff;
  --teal: #2fd8ff;

  position: relative;
  isolation: isolate;
  max-width: 1120px;
  margin: 0 auto;
  padding: clamp(20px, 5vw, 64px);
  color: var(--text);
  font-family: Inter, "Segoe UI", sans-serif;
  line-height: 1.65;
}

.lab-shell *,
.lab-shell *::before,
.lab-shell *::after { box-sizing: border-box; }

.lab-shell a {
  color: var(--teal);
  text-decoration: none;
  transition: color .15s;
}
.lab-shell a:hover { color: #fff; }
.lab-shell a:focus-visible { outline: 2px solid var(--mag); outline-offset: 3px; }

/* ---------- header ---------- */
.lab-header { position: relative; padding: 10px 0 54px; }

.lab-wires {
  position: absolute;
  top: -40px;
  right: -8px;
  width: min(44%, 380px);
  height: auto;
  z-index: -1;
  pointer-events: none;
  filter: drop-shadow(0 0 7px rgba(255, 61, 154, .6));
}

.lab-header::before {
  content: "";
  position: absolute;
  left: -50px;
  top: -50px;
  width: 280px;
  height: 280px;
  z-index: -1;
  pointer-events: none;
  background: radial-gradient(var(--mag) 1.2px, transparent 1.8px) 0 0 / 7px 7px;
  -webkit-mask-image: radial-gradient(circle at 0 0, #000, transparent 68%);
  mask-image: radial-gradient(circle at 0 0, #000, transparent 68%);
  opacity: .5;
}

.lab-eyebrow,
.lab-kicker,
.lab-counter,
.lab-card-index,
.lab-card-bottom,
.lab-note-category,
.lab-note-date,
.lab-discipline-heading > span,
.lab-discipline time,
.lab-about-signature,
.lab-footer,
.lab-nav a {
  font-family: "IBM Plex Mono", Consolas, monospace;
  font-size: .72rem;
  letter-spacing: .09em;
}

.lab-eyebrow {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 8px 12px;
  color: #cfc9ee;
}

.lab-jp {
  font-family: "Noto Sans JP", sans-serif;
  color: var(--mag);
  letter-spacing: .12em;
  padding-left: 12px;
  border-left: 1px solid var(--line);
}

.lab-status-dot,
.lab-note-marker {
  width: 8px;
  height: 8px;
  flex: 0 0 8px;
  border-radius: 50%;
  background: var(--mag);
  box-shadow: 0 0 12px var(--mag);
}

.lab-title {
  margin: 26px 0 8px !important;
  padding: 0 !important;
  border: 0 !important;
  color: #fff !important;
  font-family: "Chakra Petch", Inter, sans-serif !important;
  font-size: clamp(2.5rem, 8.4vw, 5.6rem) !important;
  line-height: 1.02 !important;
  font-weight: 700 !important;
  letter-spacing: -.02em !important;
  /* print-misregistration look, like a risograph poster */
  text-shadow: 3px 0 0 rgba(255, 61, 154, .9), -3px 0 0 rgba(47, 216, 255, .85);
}
.lab-title span { color: var(--mag); text-shadow: 3px 0 0 rgba(47, 216, 255, .85), -3px 0 0 rgba(123, 97, 255, .8); }

.lab-subtitle {
  margin: 18px 0 10px;
  color: #e4defa;
  font-size: clamp(1.05rem, 2.5vw, 1.4rem);
}

.lab-intro {
  max-width: 560px;
  color: var(--muted);
  font-size: .96rem;
}

.lab-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 32px;
}

.lab-nav a {
  padding: 8px 16px;
  color: var(--text);
  border: 1px solid var(--line);
  border-radius: 3px;
  background: rgba(255, 255, 255, .03);
  transition: background .15s, border-color .15s, color .15s;
}
.lab-nav a:hover {
  background: var(--mag);
  border-color: var(--mag);
  color: #07050f;
}

/* ---------- sections ---------- */
.lab-section { margin-top: 58px; }

.lab-section-heading {
  display: flex;
  justify-content: space-between;
  align-items: end;
  gap: 16px;
  margin-bottom: 24px;
}

.lab-kicker { color: var(--mag); }

.lab-section-heading h2,
.lab-about h2 {
  margin: 8px 0 0 !important;
  padding: 0 !important;
  border: 0 !important;
  color: #fff !important;
  font-family: "Chakra Petch", Inter, sans-serif !important;
  font-weight: 700 !important;
  font-size: clamp(1.6rem, 4vw, 2.2rem) !important;
  letter-spacing: -.01em;
}

.lab-counter {
  padding: 4px 11px;
  color: var(--muted);
  white-space: nowrap;
  border: 1px solid var(--line);
  border-radius: 999px;
}

/* ---------- archive cards: manga panels ---------- */
.lab-archive-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 22px;
}

.lab-category-card {
  --accent: var(--mag);
  position: relative;
  min-width: 0;
  padding: 22px;
  overflow: hidden;
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 4px;
  box-shadow: 5px 5px 0 var(--accent);
  transition: transform .15s, box-shadow .15s;
}
.lab-category-card:nth-child(3n+2) { --accent: var(--vio); }
.lab-category-card:nth-child(3n) { --accent: var(--teal); }

/* screentone corner */
.lab-category-card::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  width: 130px;
  height: 130px;
  pointer-events: none;
  background: radial-gradient(var(--accent) 1.1px, transparent 1.7px) 0 0 / 6px 6px;
  -webkit-mask-image: radial-gradient(circle at 100% 0, #000, transparent 70%);
  mask-image: radial-gradient(circle at 100% 0, #000, transparent 70%);
  opacity: .45;
}

.lab-category-card:hover {
  transform: translate(-3px, -3px);
  box-shadow: 8px 8px 0 var(--accent);
}

.lab-card-top,
.lab-card-bottom {
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.lab-card-symbol {
  color: var(--accent);
  font-size: 1.3rem;
  text-shadow: 0 0 14px var(--accent);
}

.lab-card-index { color: #8c86b3; }

.lab-category-card h3 {
  position: relative;
  z-index: 1;
  margin: 22px 0 8px;
  color: #fff;
  font-family: "Chakra Petch", Inter, sans-serif;
  font-size: 1.2rem;
  text-transform: capitalize;
}

.lab-card-description {
  position: relative;
  z-index: 1;
  min-height: 48px;
  margin: 0 0 22px;
  color: var(--muted);
  font-size: .86rem;
}

.lab-card-bottom {
  padding-top: 14px;
  border-top: 1px dashed var(--line);
  color: var(--muted);
}
.lab-card-bottom a { color: var(--accent); }

/* ---------- recent notes ---------- */
.lab-note-list { border-top: 1px solid var(--line); }

.lab-note {
  --accent: var(--mag);
  display: grid;
  grid-template-columns: 8px minmax(0, 1fr) auto 14px;
  align-items: center;
  gap: 17px;
  padding: 22px 10px;
  border-bottom: 1px solid var(--line);
  border-left: 2px solid transparent;
  transition: background .18s, border-color .18s;
}
.lab-note:nth-child(3n+2) { --accent: var(--vio); }
.lab-note:nth-child(3n) { --accent: var(--teal); }
.lab-note .lab-note-marker { background: var(--accent); box-shadow: 0 0 12px var(--accent); }

.lab-note:hover {
  border-left-color: var(--accent);
  background: linear-gradient(90deg, rgba(255, 255, 255, .06), transparent 70%);
}

.lab-note-content { min-width: 0; }

.lab-note-category {
  color: var(--accent);
  text-transform: uppercase;
  overflow-wrap: anywhere;
}

.lab-note-content h3 {
  margin: 5px 0 !important;
  padding: 0 !important;
  border: 0 !important;
  color: #f4f1ff !important;
  font-family: "Chakra Petch", Inter, sans-serif !important;
  font-size: 1.08rem !important;
}

.lab-note-content p {
  margin: 5px 0 0;
  color: var(--muted);
  font-size: .84rem;
}

.lab-note-date,
.lab-discipline time {
  color: var(--muted);
  white-space: nowrap;
  letter-spacing: 0;
}

.lab-note-arrow { color: var(--accent); }

/* ---------- discipline index ---------- */
.lab-discipline {
  --accent: var(--mag);
  margin-top: 18px;
  padding: 20px 22px;
  background: var(--panel);
  border: 1px solid var(--line);
  border-left: 4px solid var(--accent);
  border-radius: 4px;
  scroll-margin-top: 24px;
}
.lab-discipline:nth-of-type(3n) { --accent: var(--vio); }
.lab-discipline:nth-of-type(3n+1) { --accent: var(--teal); }

.lab-discipline-heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.lab-discipline-heading h3 {
  margin: 0;
  color: #fff;
  font-family: "Chakra Petch", Inter, sans-serif;
  font-size: 1.12rem;
  text-transform: capitalize;
}

.lab-discipline-heading > span {
  color: var(--accent);
  white-space: nowrap;
}

.lab-discipline ul {
  margin: 14px 0 0;
  padding: 0;
  list-style: none;
}

.lab-discipline li {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 16px;
  padding: 12px 0;
  border-top: 1px solid rgba(255, 255, 255, .08);
}

.lab-discipline li a { min-width: 0; overflow-wrap: anywhere; color: var(--text); }
.lab-discipline li a:hover { color: var(--accent); }

/* ---------- about ---------- */
.lab-about {
  position: relative;
  margin-top: 62px;
  padding: clamp(24px, 4vw, 42px);
  overflow: hidden;
  background:
    linear-gradient(135deg, rgba(255, 61, 154, .16), rgba(123, 97, 255, .12) 55%, rgba(47, 216, 255, .08)),
    var(--panel);
  border: 1px solid rgba(255, 255, 255, .2);
  border-radius: 4px;
  box-shadow: 6px 6px 0 var(--vio);
}

.lab-about h2 { margin-top: 15px !important; }

.lab-about > p {
  max-width: 660px;
  color: #bdb7dc;
}

.lab-about-signature {
  display: block;
  margin-top: 28px;
  color: var(--mag);
}

.lab-footer {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 46px;
  padding-top: 20px;
  border-top: 1px solid var(--line);
  color: #8c86b3;
}

/* ---------- mobile ---------- */
@media (max-width: 640px) {
  .lab-shell { padding: 22px 16px; }

  .lab-wires { width: 72%; opacity: .32; }

  .lab-section-heading { align-items: start; }

  .lab-note {
    grid-template-columns: 8px minmax(0, 1fr) 12px;
    gap: 11px;
  }

  .lab-note-date {
    grid-column: 2;
    grid-row: 2;
    font-size: .68rem;
  }

  .lab-note-arrow { grid-column: 3; grid-row: 1; }

  .lab-discipline li { flex-direction: column; gap: 3px; }

  .lab-footer { flex-direction: column; }
}

@media (prefers-reduced-motion: reduce) {
  .lab-shell *,
  .lab-shell *::before,
  .lab-shell *::after {
    transition: none !important;
    scroll-behavior: auto !important;
  }
  .lab-category-card:hover { transform: none; }
}
</style>
