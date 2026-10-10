---
layout: default
title: Home
---

<style>
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@500;600;700&family=Fredoka:wght@400;600&display=swap");

:root { 
  --bg-pink: #fff0f5; 
  --card-bg: rgba(255, 255, 255, 0.85); 
  --pastel-pink: #ffb7c5; 
  --deep-pink: #ff69b4; 
  --strawberry-red: #ff4757;
  --text-main: #594a4e; 
  --text-muted: #9c848b; 
  --border-pink: #ffd1dc; 
}

html {
  background: 
    radial-gradient(circle at 10% 20%, rgba(255, 183, 197, 0.4) 0%, transparent 40%),
    radial-gradient(circle at 90% 80%, rgba(255, 223, 186, 0.4) 0%, transparent 40%),
    radial-gradient(circle at 50% 50%, rgba(255, 240, 245, 1) 0%, #ffe4e9 100%) !important;
  background-attachment: fixed !important;
  min-height: 100%;
}

body { 
  background: transparent !important; 
  color: var(--text-main) !important; 
  font-family: "Quicksand", system-ui, sans-serif; 
  font-weight: 500; 
  font-size: 18px; 
  line-height: 1.6; 
}

/* Fluffy cloud background decorations */
body::before {
  content: "☁️ 🌸 🍓 ☁️  🐰 🍓 ☁️  🐱 🌸 ☁️";
  position: fixed; 
  top: 10px; 
  left: 0; 
  right: 0;
  text-align: center;
  font-size: 1.2rem;
  opacity: 0.4;
  z-index: -1;
  pointer-events: none;
  letter-spacing: 1.5rem;
}

.site-header, .site-footer { 
  border-color: var(--border-pink) !important; 
  background-color: rgba(255, 255, 255, 0.6) !important;
  backdrop-filter: blur(5px);
}

.site-title, .site-title:visited, .site-nav .page-link, .site-footer, .site-footer a { 
  color: var(--text-muted) !important; 
  font-family: "Fredoka", sans-serif;
}

.kb { 
  max-width: 780px; 
  margin: 0 auto; 
  padding: 2rem 1rem 5rem; 
}

.kb-title {
  position: relative;
  font-family: "Fredoka", cursive, sans-serif;
  font-weight: 600;
  font-size: clamp(2rem, 5vw, 2.8rem);
  text-align: center;
  color: var(--deep-pink) !important;
  margin: 0 0 0.5rem;
  border: 0;
  text-shadow: 2px 2px 0px #fff, 4px 4px 0px var(--border-pink);
}

.kb-title::before {
  content: "🍓 ";
}

.kb-title::after {
  content: " 🐰";
}

.kb-sub { 
  font-family: "Quicksand", sans-serif; 
  text-align: center;
  font-size: 1rem; 
  color: var(--text-muted); 
  margin: 0 0 2.5rem; 
  background: var(--card-bg);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  display: inline-block;
  left: 50%;
  position: relative;
  transform: translateX(-50%);
  border: 2px dashed var(--pastel-pink);
  box-shadow: 0 4px 15px rgba(255, 183, 197, 0.3);
}

.kb-sub b { 
  color: var(--strawberry-red); 
  font-weight: 700; 
}

.kb-folder { 
  margin: 0 0 2rem; 
}

.kb-folder h3 {
  font-family: "Fredoka", sans-serif;
  font-weight: 600;
  font-size: 1.2rem;
  color: var(--deep-pink) !important;
  margin: 0 0 0.8rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

/* Cute cat/rabbit icons for folders */
.kb-folder h3::before { 
  content: "🐾"; 
  font-size: 1rem;
}

.kb-count { 
  margin-left: auto; 
  font-family: "Quicksand", sans-serif; 
  font-weight: 600; 
  font-size: 0.8rem; 
  background: var(--pastel-pink);
  color: #fff;
  padding: 2px 10px;
  border-radius: 12px;
  box-shadow: 0 2px 5px rgba(255, 105, 180, 0.2);
}

.kb-folder ul {
  list-style: none;
  margin: 0;
  padding: 0.5rem 1.2rem;
  background: var(--card-bg);
  border: 2px solid var(--border-pink);
  border-radius: 24px;
  backdrop-filter: blur(8px);
  box-shadow: 0 8px 25px rgba(255, 183, 197, 0.25);
}

.kb-folder li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 0.8rem 0.5rem;
  border-radius: 12px;
  transition: all 0.2s ease;
}

.kb-folder li + li { 
  border-top: 1px dashed var(--border-pink); 
}

.kb-folder li:hover { 
  background: rgba(255, 183, 197, 0.18); 
  transform: translateX(4px);
}

/* Cute little strawberry bullet on hover */
.kb-folder li:hover::before {
  content: "🍓";
  font-size: 0.8rem;
  margin-right: -0.5rem;
}

.kb-folder li small { 
  font-family: "Quicksand", sans-serif; 
  color: var(--text-muted); 
  white-space: nowrap; 
  font-size: 0.8rem; 
  background: #fff;
  padding: 2px 8px;
  border-radius: 8px;
  border: 1px solid var(--border-pink);
}

.kb a { 
  color: var(--deep-pink) !important; 
  font-weight: 600; 
  text-decoration: none; 
  transition: all 0.2s ease; 
}

.kb a:hover { 
  color: var(--strawberry-red) !important; 
  text-shadow: 0 0 8px rgba(255, 71, 87, 0.3);
}

.kb a:focus-visible { 
  outline: 2px solid var(--deep-pink); 
  outline-offset: 3px; 
}

@media (max-width: 600px) {
  body { font-size: 16px; }
  .kb-folder li { flex-direction: column; align-items: flex-start; gap: 0.3rem; }
  .kb-folder li small { align-self: flex-end; }
}
</style>

<div class="kb">
<h1 class="kb-title">CSE Core Knowledge Base</h1>
<p class="kb-sub"><b>humaira@cute-cloud</b>:~$ spreading joy & notes 💕</p>
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
