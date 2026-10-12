---
layout: page
title: projects
permalink: /projects/
---

<p class="jump"><a href="#work">work</a><span class="sep">/</span><a href="#cv">computer vision</a></p>

<div class="grid">
  <a class="card feature" href="https://clearoapp.com/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/clearo.png" alt="clearo" loading="lazy"/></div>
    <div class="meta">
      <span class="tag">new</span>
      <span class="title">clearo</span>
      <span class="desc">agentic marketplace through imessage</span>
    </div>
  </a>
</div>

<h3 id="work">work</h3>

<div class="grid">
  <a class="card" href="https://tyeoh9.github.io/llm-validation-framework/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/validate-llm.png" alt="validate-llm" loading="lazy"/></div>
    <div class="meta">
      <span class="title">validate-llm</span>
      <span class="desc">python package for catching unwanted llm outputs</span>
    </div>
  </a>
  <a class="card" href="https://github.com/tyeoh9/repometrics">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/repometrics.png" alt="repometrics" loading="lazy"/></div>
    <div class="meta">
      <span class="title">repometrics</span>
      <span class="desc">cli tool to check repo health</span>
    </div>
  </a>
  <a class="card" href="https://inky-254095790852.us-central1.run.app/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/inky.gif" alt="inky" loading="lazy"/></div>
    <div class="meta">
      <span class="title">inky</span>
      <span class="desc">an ai writing companion that thinks alongside you</span>
    </div>
  </a>
  <a class="card" href="https://github.com/tyeoh9/GPT4oVisionTrafficMonitor">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/part2_ui.png" alt="gpt traffic monitor assistant" loading="lazy"/></div>
    <div class="meta">
      <span class="title">gpt traffic monitor assistant</span>
    </div>
  </a>
  <a class="card" href="https://github.com/tyeoh9/NPRRenderer">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/link.gif" alt="non-photorealistic shader" loading="lazy"/></div>
    <div class="meta">
      <span class="title">non-photorealistic shader</span>
    </div>
  </a>
  <a class="card" href="https://github.com/tyeoh9/BYOW">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/gameplay.gif" alt="build your own world" loading="lazy"/></div>
    <div class="meta">
      <span class="title">build your own world</span>
      <span class="desc">an engine for generating explorable worlds</span>
    </div>
  </a>
</div>

<h3 id="cv">computer vision</h3>

<div class="grid centered">
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project6/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project6/part2/final_render/final.gif" alt="neural radiance fields" loading="lazy"/></div>
    <div class="meta">
      <span class="title">neural radiance fields</span>
    </div>
  </a>
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project5/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project5/part_a/part7_2/test_inpaint3.png" alt="the power of diffusion models" loading="lazy"/></div>
    <div class="meta">
      <span class="title">the power of diffusion models</span>
    </div>
  </a>
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project4/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project4/heyns/blended_mosaic.jpg" alt="image warping and mosaicing" loading="lazy"/></div>
    <div class="meta">
      <span class="title">image warping and mosaicing</span>
    </div>
  </a>
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project3/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project3/part3_results/morphed_kanye_thomas-ezgif.com-loop-count.gif" alt="face morphing" loading="lazy"/></div>
    <div class="meta">
      <span class="title">face morphing</span>
    </div>
  </a>
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project2/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project2/results/blending/oraple.jpg" alt="convolutions, filters, and frequencies" loading="lazy"/></div>
    <div class="meta">
      <span class="title">convolutions, filters, and frequencies</span>
    </div>
  </a>
  <a class="card" href="{{ site.baseurl }}/projects/cs180/project1/">
    <div class="thumb"><img src="{{ site.baseurl }}/projects/cs180/project1/results/harvesters/after_harvesters.jpg" alt="colorizing the prokudin-gorskii collection" loading="lazy"/></div>
    <div class="meta">
      <span class="title">colorizing the prokudin-gorskii collection</span>
    </div>
  </a>
</div>

<style>
  .w { max-width: 880px; }
  .jump { margin-top: -0.5rem; }
  .sep { color: #aaa; margin: 0 0.6rem; }
  h3 { margin: 3.5rem 0 1.25rem; padding-bottom: 0.4rem; border-bottom: 1px solid #ddd; }
  .grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem; }
  .card { display: flex; flex-direction: column; border: 1px solid #ddd; text-decoration: none; transition: border-color 0.15s; }
  .card:hover { border-color: #888; }
  .thumb { aspect-ratio: 16 / 10; overflow: hidden; border-bottom: 1px solid #ddd; }
  .thumb img { width: 100%; height: 100%; object-fit: cover; object-position: left top; display: block; }
  @supports not (aspect-ratio: 1 / 1) {
    .thumb { position: relative; height: 0; padding-top: 62.5%; }
    .thumb img { position: absolute; top: 0; left: 0; }
  }
  .meta { padding: 0.8rem 1rem 1rem; display: flex; flex-direction: column; gap: 0.3rem; }
  .title { font-weight: bold; text-decoration: underline; }
  .desc { color: #666; font-size: 0.9em; line-height: 1.4; }
  .centered .thumb img { object-position: center; }
  .feature { grid-column: 1 / -1; flex-direction: row; }
  .feature .thumb { flex: 3; border-bottom: 0; border-right: 1px solid #ddd; }
  .feature .meta { flex: 2; justify-content: center; padding: 1.5rem; }
  .feature .title { font-size: 1.4em; }
  /* theme inverts the page in dark mode: #0000ee renders as the yellow link color */
  .tag { align-self: flex-start; font-size: 0.8em; font-weight: bold; background: #0000ee; color: #fff; padding: 0.1rem 0.5rem; letter-spacing: 0.05em; }
  @media (max-width: 860px) {
    .grid { grid-template-columns: repeat(2, 1fr); }
  }
  @media (max-width: 640px) {
    .grid { grid-template-columns: 1fr; }
    .feature { flex-direction: column; }
    .feature .thumb { border-right: 0; border-bottom: 1px solid #ddd; }
    .feature .meta { padding: 0.8rem 1rem 1rem; }
  }
</style>
