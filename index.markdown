---
layout: home
title: thomas yeoh
---

<p class="tagline">master’s student at uc irvine and berkeley eecs alum, with experience in software engineering, backend systems, and machine learning. my work spans startups, research labs, and big tech — designing APIs, building pipelines, and plenty of debugging.</p>

<p class="prev"><span class="label">previously:</span> apple, zoofi ai, keysight</p>

<p class="nav">
  <a href="/tyeoh/projects/">projects</a><span class="sep">/</span><a href="/tyeoh/resume/">resume</a><span class="sep">/</span><a href="https://www.linkedin.com/in/yeoh">linkedin</a><span class="sep">/</span><a href="https://github.com/tyeoh9">github</a><span class="sep">/</span><span class="email">tyeoh@berkeley.edu</span>
</p>

### latest work

<dl class="work">
  <dt><a href="https://clearoapp.com/">clearo</a> <span class="tag">new</span></dt>
  <dd>agentic marketplace through imessage</dd>
  <dt><a href="https://tyeoh9.github.io/llm-validation-framework/">validate-llm</a></dt>
  <dd>python package for catching unwanted llm outputs</dd>
  <dt><a href="https://github.com/tyeoh9/repometrics">repometrics</a></dt>
  <dd>cli tool to check repo health</dd>
  <dt><a href="https://inky-254095790852.us-central1.run.app/">inky</a></dt>
  <dd>an ai writing companion that thinks alongside you</dd>
</dl>

<style>
  header h1 { margin-bottom: 0.25rem; }
  .tagline { margin: 0.5rem 0 1rem; color: #444; line-height: 1.6; }
  .prev { margin: 0 0 1rem; }
  .label { color: #666; }
  .nav { margin: 0.4rem 0; }
  .nav a { white-space: nowrap; }
  .sep { color: #aaa; margin: 0 0.6rem; }
  h3 { margin-top: 2.5rem; }
  .work { display: grid; grid-template-columns: max-content 1fr; gap: 0.5rem 1.5rem; margin: 0; }
  .work dt, .work dd { margin: 0; }
  .work dd { color: #666; }
  .email { white-space: nowrap; }
  .tag { font-size: 0.75em; font-weight: bold; background: #0000ee; color: #fff; padding: 0 0.4rem; margin-left: 0.3rem; }
  @media (max-width: 520px) {
    .work { grid-template-columns: 1fr; gap: 0.1rem; }
    .work dd { margin-bottom: 0.7rem; }
  }
</style>

<style>
  .cursor { display: inline-block; width: 0.6em; height: 1em; margin-left: 0.15em; background: currentColor; vertical-align: -0.1em; animation: blink 1s steps(1) infinite; }
  @keyframes blink { 50% { opacity: 0; } }
  @media (prefers-reduced-motion: reduce) { .cursor { animation: none; } }
</style>

<script>
// Name resolves from random characters once on load, then a block cursor blinks after it.
(function () {
  var h1 = document.querySelector('header h1');
  if (!h1) return;
  var name = h1.textContent;
  var text = document.createElement('span');
  var cursor = document.createElement('span');
  text.textContent = name;
  text.setAttribute('aria-hidden', 'true');
  cursor.className = 'cursor';
  cursor.setAttribute('aria-hidden', 'true');
  h1.setAttribute('aria-label', name);
  h1.textContent = '';
  h1.appendChild(text);
  h1.appendChild(cursor);

  var reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if (reduce) return;

  var chars = 'abcdefghijklmnopqrstuvwxyz0123456789/<>_-=+*#';
  var frame = 0, total = 14;
  (function step() {
    var out = '';
    for (var i = 0; i < name.length; i++) {
      var c = name.charAt(i);
      out += (c === ' ' || i < (frame / total) * name.length) ? c : chars.charAt(Math.floor(Math.random() * chars.length));
    }
    text.textContent = out;
    if (++frame <= total) setTimeout(step, 45);
    else text.textContent = name;
  })();
})();
</script>
