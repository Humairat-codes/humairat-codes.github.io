
---
layout: default
title: "Humaira's Labs"
---

<div class="lab-shell">

  <header class="lab-header">
    <div class="lab-eyebrow">
      <span class="lab-status-dot"></span>
      PERSONAL RESEARCH ARCHIVE / 2026
    </div>

    <h1 class="lab-title">OMNIX<span>'S</span> LABS</h1>

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
    <span class="lab-about-signature">OMNIX / END OF TRANSMISSION</span>
  </section>

  <footer class="lab-footer">
    <span>OMNIX'S LABS</span>
    <span>BUILT THROUGH CURIOSITY · {{ site.time | date: "%Y" }}</span>
  </footer>

</div>

<style>
/* OMNIX'S LABS — BLUE HOUR ARCHIVE */

.lab-shell {
  --bg: #080d19;
  --panel: rgba(20, 31, 50, .76);
  --silver: #c5d0df;
  --muted: #8d9eb6;
  --ice: #a9d8ff;
  --blue: #347dff;
  --line: rgba(174, 199, 231, .19);

  position: relative;
  isolation: isolate;
  max-width: 1120px;
  margin: 0 auto;
  padding: clamp(20px, 5vw, 64px);
  color: #e5edf9;
  background:
    radial-gradient(ellipse at 12% 0%, #234a8045, transparent 38%),
    radial-gradient(ellipse at 90% 28%, #444b9130, transparent 36%),
    linear-gradient(155deg, #080d19, #0c1424 60%, #080d19);
  border: 1px solid var(--line);
  border-radius: 20px;
  overflow: hidden;
  font-family: Inter, "Segoe UI", sans-serif;
  line-height: 1.7;
}

.lab-shell *,
.lab-shell *::before,
.lab-shell *::after {
  box-sizing: border-box;
}

.lab-shell a {
  color: var(--ice);
  text-decoration: none;
}

.lab-shell a:hover {
  color: #fff;
}

.lab-header {
  position: relative;
  padding: 10px 0 54px;
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
.lab-footer {
  font-family: "SFMono-Regular", Consolas, monospace;
  font-size: .72rem;
  letter-spacing: .09em;
}

.lab-eyebrow {
  display: flex;
  align-items: center;
  gap: 10px;
  color: var(--silver);
}

.lab-status-dot,
.lab-note-marker {
  width: 7px;
  height: 7px;
  flex: 0 0 7px;
  border-radius: 50%;
  background: #83c9ff;
  box-shadow: 0 0 12px #347dff;
}

.lab-title {
  margin: 28px 0 8px !important;
  padding: 0 !important;
  border: 0 !important;
  color: #f1f6ff !important;
  font-size: clamp(2.6rem, 8vw, 5.4rem) !important;
  line-height: 1.05 !important;
  font-weight: 800 !important;
  letter-spacing: -.075em !important;
  text-shadow: 0 0 36px #347dff2a;
}

.lab-title span {
  color: #a9d8ff;
}

.lab-subtitle {
  margin: 18px 0 10px;
  color: var(--silver);
  font-size: clamp(1.05rem, 2.5vw, 1.4rem);
}

.lab-intro {
  max-width: 580px;
  color: var(--muted);
  font-size: .96rem;
}

.lab-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
  margin-top: 32px;
  padding-top: 20px;
  border-top: 1px solid var(--line);
}

.lab-nav a {
  font-family: Consolas, monospace;
  font-size: .75rem;
  letter-spacing: .1em;
}

.lab-section {
  margin-top: 54px;
}

.lab-section-heading {
  display: flex;
  justify-content: space-between;
  align-items: end;
  gap: 16px;
  margin-bottom: 22px;
}

.lab-kicker {
  color: #8cbaff;
}

.lab-section-heading h2,
.lab-about h2 {
  margin: 8px 0 0 !important;
  padding: 0 !important;
  border: 0 !important;
  color: #eef4ff !important;
  font-size: clamp(1.55rem, 4vw, 2.1rem) !important;
  letter-spacing: -.045em;
}

.lab-counter {
  color: var(--muted);
  white-space: nowrap;
}

.lab-archive-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 14px;
}

.lab-category-card {
  position: relative;
  min-width: 0;
  padding: 22px;
  background:
    linear-gradient(140deg, #ffffff06, transparent 60%),
    var(--panel);
  border: 1px solid var(--line);
  border-radius: 13px;
  transition: border-color .2s, background .2s, transform .2s;
}

.lab-category-card:hover {
  transform: translateY(-3px);
  border-color: #83bfff80;
  background-color: #172641;
}

.lab-card-top,
.lab-card-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.lab-card-symbol {
  color: var(--ice);
  font-size: 1.25rem;
  text-shadow: 0 0 15px #347dff70;
}

.lab-card-index {
  color: #7186a5;
}

.lab-category-card h3 {
  margin: 22px 0 8px;
  color: #e8f1ff;
  font-size: 1.08rem;
  letter-spacing: -.02em;
}

.lab-card-description {
  min-height: 48px;
  margin: 0 0 22px;
  color: var(--muted);
  font-size: .86rem;
}

.lab-card-bottom {
  padding-top: 14px;
  border-top: 1px solid var(--line);
  color: var(--muted);
}

.lab-card-bottom a {
  color: var(--ice);
}

.lab-note-list {
  border-top: 1px solid var(--line);
}

.lab-note {
  display: grid;
  grid-template-columns: 8px minmax(0, 1fr) auto 14px;
  align-items: center;
  gap: 17px;
  padding: 22px 8px;
  border-bottom: 1px solid var(--line);
  transition: background .2s;
}

.lab-note:hover {
  background: #a9d8ff08;
}

.lab-note-content {
  min-width: 0;
}

.lab-note-category {
  color: #88b9f6;
  text-transform: uppercase;
  overflow-wrap: anywhere;
}

.lab-note-content h3 {
  margin: 5px 0 !important;
  padding: 0 !important;
  border: 0 !important;
  color: #e5edf9 !important;
  font-size: 1rem !important;
  letter-spacing: -.015em;
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

.lab-note-arrow {
  color: #8dbfff;
}

.lab-discipline {
  margin-top: 18px;
  padding: 20px;
  background: #101a2a99;
  border: 1px solid var(--line);
  border-radius: 12px;
  scroll-margin-top: 24px;
}

.lab-discipline-heading {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.lab-discipline-heading h3 {
  margin: 0;
  color: #e6effe;
  font-size: 1.05rem;
  text-transform: capitalize;
}

.lab-discipline-heading > span {
  color: var(--muted);
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
  border-top: 1px solid #ffffff0c;
}

.lab-discipline li a {
  min-width: 0;
  overflow-wrap: anywhere;
}

.lab-about {
  margin-top: 58px;
  padding: clamp(22px, 4vw, 38px);
  background:
    radial-gradient(ellipse at 0% 0%, #347dff20, transparent 65%),
    #101a2a99;
  border: 1px solid #9fcaff32;
  border-radius: 15px;
}

.lab-about h2 {
  margin-top: 15px !important;
}

.lab-about > p {
  max-width: 680px;
  color: var(--muted);
}

.lab-about-signature {
  display: block;
  margin-top: 28px;
  color: #8cbaff;
}

.lab-footer {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 42px;
  padding-top: 20px;
  border-top: 1px solid var(--line);
  color: #7186a5;
}

@media (max-width: 640px) {
  .lab-shell {
    padding: 22px 16px;
    border-radius: 12px;
  }

  .lab-archive-grid {
    grid-template-columns: 1fr;
  }

  .lab-section-heading {
    align-items: start;
  }

  .lab-note {
    grid-template-columns: 7px minmax(0, 1fr) 12px;
    gap: 11px;
  }

  .lab-note-date {
    grid-column: 2;
    grid-row: 2;
    font-size: .68rem;
  }

  .lab-note-arrow {
    grid-column: 3;
    grid-row: 1;
  }

  .lab-discipline li {
    flex-direction: column;
    gap: 3px;
  }

  .lab-footer {
    flex-direction: column;
  }
}

@media (prefers-reduced-motion: reduce) {
  .lab-shell *,
  .lab-shell *::before,
  .lab-shell *::after {
    transition: none !important;
    scroll-behavior: auto !important;
  }
}
</style>
