---
layout: default
title: Home
---

<style>
@import url("https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Rajdhani:wght@500;600&family=JetBrains+Mono:wght@400;500&display=swap");
:root { --bg:#07060f; --cyan:#00e5ff; --mag:#ff2bd6; --blue:#3d5bff; --text:#d7e3ff; --muted:#7f8bb3; --line:rgba(0,229,255,0.28); }
html {
  background:
    radial-gradient(900px 520px at 8% -8%, rgba(61,91,255,0.38), transparent 62%),
    radial-gradient(800px 480px at 100% 0%, rgba(0,229,255,0.16), transparent 60%),
    radial-gradient(70% 38% at 50% 100%, rgba(255,43,214,0.30), transparent 70%),
    var(--bg) !important;
  background-attachment: fixed !important;
  min-height: 100%;
}
body { background: transparent !important; color: var(--text) !important; font-family: "Rajdhani", system-ui, sans-serif; font-weight: 500; font-size: 19px; line-height: 1.5; }
body::before {
  content: "";
  position: fixed; left: -50%; right: -50%; bottom: 0; height: 60vh;
  z-index: -1; pointer-events: none;
  background:
    linear-gradient(rgba(255,43,214,0.42) 1px, transparent 1px) 0 0 / 100% 42px,
    linear-gradient(90deg, rgba(255,43,214,0.42) 1px, transparent 1px) 0 0 / 64px 100%;
  transform: perspective(260px) rotateX(58deg);
  transform-origin: 50% 100%;
  -webkit-mask-image: linear-gradient(to top, #000, transparent 85%);
  mask-image: linear-gradient(to top, #000, transparent 85%);
}
body::after {
  content: "";
  position: fixed; inset: 0; z-index: 50; pointer-events: none;
  background: repeating-linear-gradient(0deg, rgba(255,255,255,0.028) 0 1px, transparent 1px 3px);
}
.site-header, .site-footer { border-color: var(--line) !important; }
.site-title, .site-title:visited, .site-nav .page-link, .site-footer, .site-footer a { color: var(--muted) !important; }
.kb { max-width: 780px; margin: 0 auto; padding: 1.5rem 0 5rem; }
.kb-title {
  position: relative;
  font-family: "Orbitron", sans-serif;
  font-weight: 800;
  font-size: clamp(1.7rem, 5.6vw, 2.9rem);
  letter-spacing: 0.04em;
  line-height: 1.15;
  text-transform: uppercase;
  margin: 0 0 0.6rem;
  border: 0;
  color: #fff !important;
  text-shadow: 0 0 8px rgba(0,229,255,0.9), 0 0 28px rgba(0,229,255,0.55), 0 0 60px rgba(61,91,255,0.5);
}
.kb-title::before, .kb-title::after {
  content: attr(data-text);
  position: absolute; left: 0; top: 0; width: 100%;
  opacity: 0; pointer-events: none;
}
.kb-title::before { color: var(--mag); text-shadow: none; animation: glitchA 1.1s steps(1) 0.3s 1; }
.kb-title::after { color: var(--cyan); text-shadow: none; animation: glitchB 1.1s steps(1) 0.3s 1; }
@keyframes glitchA {
  0%, 100% { opacity: 0; }
  10% { opacity: 0.9; transform: translate(-4px, 1px); clip-path: inset(10% 0 60% 0); }
  30% { opacity: 0.9; transform: translate(5px, -1px); clip-path: inset(55% 0 15% 0); }
  55% { opacity: 0.9; transform: translate(-3px, 0); clip-path: inset(30% 0 40% 0); }
  75% { opacity: 0; }
}
@keyframes glitchB {
  0%, 100% { opacity: 0; }
  15% { opacity: 0.9; transform: translate(4px, -1px); clip-path: inset(60% 0 10% 0); }
  40% { opacity: 0.9; transform: translate(-5px, 1px); clip-path: inset(5% 0 70% 0); }
  65% { opacity: 0.9; transform: translate(3px, 0); clip-path: inset(40% 0 30% 0); }
  80% { opacity: 0; }
}
.kb-sub { font-family: "JetBrains Mono", monospace; font-size: 0.85rem; color: var(--muted); margin: 0 0 2.4rem; }
.kb-sub b { color: var(--mag); font-weight: 500; }
.kb-sub::after { content: "\2588"; color: var(--cyan); margin-left: 0.3rem; animation: blink 1.1s steps(2) infinite; }
@keyframes blink { 50% { opacity: 0; } }
.kb-folder { margin: 0 0 1.8rem; }
.kb-folder h3 {
  font-family: "Orbitron", sans-serif;
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: 0.06em;
  color: var(--text) !important;
  margin: 0 0 0.6rem;
  display: flex;
  align-items: baseline;
  gap: 0.6rem;
}
.kb-folder h3::before { content: "//"; font-family: "JetBrains Mono", monospace; color: var(--mag); text-shadow: 0 0 10px var(--mag); }
.kb-count { margin-left: auto; font-family: "JetBrains Mono", monospace; font-weight: 400; font-size: 0.74rem; letter-spacing: 0; color: var(--muted); }
.kb-folder ul {
  list-style: none;
  margin: 0;
  padding: 0.25rem 1rem;
  background: linear-gradient(180deg, rgba(14,12,34,0.82), rgba(8,7,20,0.82));
  border: 1px solid var(--line);
  border-radius: 4px;
  -webkit-backdrop-filter: blur(8px);
  backdrop-filter: blur(8px);
  box-shadow: 0 0 22px rgba(0,229,255,0.09), inset 0 0 30px rgba(61,91,255,0.07);
}
.kb-folder li {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
  padding: 0.6rem 0 0.6rem 0.8rem;
  border-left: 2px solid transparent;
  transition: border-color 0.18s, background 0.18s;
}
.kb-folder li + li { border-top: 1px solid rgba(0,229,255,0.12); }
.kb-folder li:hover { border-left-color: var(--mag); background: linear-gradient(90deg, rgba(255,43,214,0.14), transparent); }
.kb-folder li small { font-family: "JetBrains Mono", monospace; color: var(--muted); white-space: nowrap; font-size: 0.74rem; }
.kb a { color: var(--cyan) !important; font-weight: 600; text-decoration: none; transition: color 0.18s, text-shadow 0.18s; }
.kb a:hover { color: #fff !important; text-shadow: 0 0 10px var(--mag), 0 0 22px var(--mag); }
.kb a:focus-visible { outline: 2px solid var(--mag); outline-offset: 3px; }
@media (max-width: 600px) {
  body { font-size: 17px; }
  .kb-folder li { flex-direction: column; gap: 0.1rem; }
}
@media (prefers-reduced-motion: reduce) {
  .kb-title::before, .kb-title::after, .kb-sub::after { animation: none; }
}
</style>

<div class="kb">
<h1 class="kb-title" data-text="CSE Core Knowledge Base">CSE Core Knowledge Base</h1>
<p class="kb-sub"><b>humaira@cse</b>:~$ ls ./notes</p>
{% assign categories = site.posts | map: 'categories' | flatten | uniq | sort %}
{% for category in categories %}
<section class="kb-folder">
<h3>{{ category }}<span class="kb-count">{{ site.categories[category].size }} notes</span></h3>
<ul>
{% for post in site.posts %}
{% if post.categories contains category %}
<li><a href="{{ post.url | relative_url }}">{{ post.title }}</a><small>{{ post.date | date: "%Y-%m-%d" }}</small></li>
{% endif %}
{% endfor %}
</ul>
</section>
{% endfor %}
</div>
