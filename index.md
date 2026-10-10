---
layout: default
title: Home
---

<style>
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&family=DM+Sans:wght@400;500&display=swap");
:root { --ink:#130f26; --panel:rgba(255,255,255,0.05); --line:rgba(255,255,255,0.13); --text:#e9e6f7; --muted:#9a94bd; --rose:#ff7eb6; --ice:#7fd7ff; }
html {
  background:
    radial-gradient(900px 500px at 12% -5%, rgba(255,126,182,0.22), transparent 60%),
    radial-gradient(800px 500px at 95% 10%, rgba(127,215,255,0.16), transparent 60%),
    linear-gradient(rgba(255,255,255,0.035) 1px, transparent 1px) 0 0 / 44px 44px,
    linear-gradient(90deg, rgba(255,255,255,0.035) 1px, transparent 1px) 0 0 / 44px 44px,
    var(--ink) !important;
  background-attachment: fixed !important;
  min-height: 100%;
}
body { background: transparent !important; color: var(--text) !important; font-family: "DM Sans", system-ui, sans-serif; font-size: 17px; line-height: 1.6; }
.site-header, .site-footer { border-color: var(--line) !important; }
.site-title, .site-title:visited, .site-nav .page-link, .site-footer, .site-footer a { color: var(--muted) !important; }
.kb { max-width: 760px; margin: 0 auto; padding: 1.5rem 0 4rem; }
.kb-title {
  font-family: "Space Grotesk", sans-serif;
  font-weight: 700;
  font-size: clamp(2rem, 6vw, 3.3rem);
  letter-spacing: -0.02em;
  line-height: 1.08;
  margin: 0 0 0.4rem;
  border: 0;
  background: linear-gradient(90deg, var(--rose), var(--ice));
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent !important;
  filter: drop-shadow(0 0 18px rgba(255,126,182,0.35));
}
.kb-sub { color: var(--muted); margin: 0 0 2.2rem; }
.kb-folder { margin: 0 0 1.6rem; }
.kb-folder h3 {
  font-family: "Space Grotesk", sans-serif;
  font-weight: 500;
  font-size: 1.2rem;
  color: var(--text) !important;
  margin: 0 0 0.6rem;
  display: flex;
  align-items: center;
  gap: 0.6rem;
}
.kb-folder h3::before { content: ""; width: 9px; height: 9px; border-radius: 50%; background: var(--rose); box-shadow: 0 0 12px var(--rose); }
.kb-count { margin-left: auto; font-family: "DM Sans", sans-serif; font-size: 0.8rem; color: var(--muted); }
.kb-folder ul {
  list-style: none;
  margin: 0;
  padding: 0.3rem 1rem;
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 14px;
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  box-shadow: 0 18px 40px -22px rgba(0,0,0,0.7);
}
.kb-folder li {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
  padding: 0.65rem 0 0.65rem 0.8rem;
  border-left: 2px solid transparent;
  transition: border-color 0.2s, background 0.2s;
}
.kb-folder li + li { border-top: 1px solid var(--line); }
.kb-folder li:hover { border-left-color: var(--rose); background: linear-gradient(90deg, rgba(255,126,182,0.09), transparent); }
.kb-folder li small { color: var(--muted); white-space: nowrap; font-size: 0.82rem; }
.kb a { color: var(--ice) !important; font-weight: 500; text-decoration: none; transition: color 0.2s, text-shadow 0.2s; }
.kb a:hover { color: var(--rose) !important; text-shadow: 0 0 14px rgba(255,126,182,0.55); }
.kb a:focus-visible { outline: 2px solid var(--rose); outline-offset: 3px; border-radius: 4px; }
@media (max-width: 600px) {
  body { font-size: 16px; }
  .kb-folder li { flex-direction: column; gap: 0.1rem; }
}
</style>

<div class="kb">
<h1 class="kb-title">CSE Core Knowledge Base</h1>
<p class="kb-sub">Clear, broken-down notes on core computer science subjects.</p>
{% assign categories = site.posts | map: 'categories' | flatten | uniq | sort %}
{% for category in categories %}
<section class="kb-folder">
<h3>{{ category }}<span class="kb-count">{{ site.categories[category].size }} notes</span></h3>
<ul>
{% for post in site.posts %}
{% if post.categories contains category %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}</a><small>{{ post.date | date: "%b %d, %Y" }}</small></li>
{% endif %}
{% endfor %}
</ul>
</section>
{% endfor %}
</div>
