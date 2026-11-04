---
layout: default
title: Home
---

<section class="hero">
  <div>
    <div class="status"><span class="dot"></span>Open to roles in professional baseball</div>
    <h1>Jake Kleiman<br><span class="grad">Baseball Analytics</span></h1>
    <p class="lead">I'm a baseball analyst who graduated from Syracuse University in May 2026 with a B.S. in Sport Analytics and a minor in Sport Management. Most recently, I worked in Baseball Operations at the MLB Commissioner's Office, building reports on playing rules, game pace and on-field trends.</p>
    <div class="btn-row">
      <a class="btn btn-primary" href="{{ '/projects/' | relative_url }}">See my work →</a>
      <a class="btn" href="{{ '/resume/' | relative_url }}">Resume</a>
      <a class="btn" href="{{ site.linkedin }}" target="_blank" rel="noopener">LinkedIn ↗</a>
    </div>
  </div>

  <div class="stat-card">
    <div class="head"><span>Scouting report</span><span>2026</span></div>
    <div class="row"><span class="k">School</span><span class="v">Syracuse University</span></div>
    <div class="row"><span class="k">Degree</span><span class="v">B.S. Sport Analytics</span></div>
    <div class="row"><span class="k">Minor</span><span class="v">Sport Management</span></div>
    <div class="row"><span class="k">Last stop</span><span class="v">MLB Commissioner's Office</span></div>
    <div class="row"><span class="k">Tools</span><span class="v">R · Python · SQL · Tableau</span></div>
    <div class="row"><span class="k">Home</span><span class="v">Ridgewood, NJ</span></div>
  </div>
</section>

<section class="section">
  <div class="section-title">What I'm looking for</div>
  <div class="chips">
    <span class="chip">Baseball Operations</span>
    <span class="chip">Analytics</span>
    <span class="chip">Player Development</span>
    <span class="chip">Scouting</span>
    <span class="chip">Baseball Strategy</span>
  </div>
</section>

<section class="section">
  <div class="section-title">Experience highlights</div>
  <div class="grid-3">
    <div class="card">
      <div class="icon">⚾</div>
      <h3>MLB Commissioner's Office</h3>
      <p>Baseball Operations intern on the On-Field Strategy team. Built SQL, R and Excel reports on playing rules, game pace and competitive balance.</p>
    </div>
    <div class="card">
      <div class="icon">📈</div>
      <h3>Westhampton Aviators</h3>
      <p>Pitching analyst in the Hamptons Collegiate Baseball League. Used TrackMan data for pitcher evaluation and opponent scouting reports.</p>
    </div>
    <div class="card">
      <div class="icon">🧢</div>
      <h3>Syracuse Club Baseball</h3>
      <p>President of a 30+ player program. Ran baseball operations and landed a multi-year deal to open each season at NBT Bank Stadium.</p>
    </div>
  </div>
</section>

<section class="section">
  <div class="section-title">Featured project</div>
  <div class="project">
    <a class="project-img" href="{{ '/lineup-lab/' | relative_url }}"><img src="{{ '/04-season-chart.png' | relative_url }}" alt="Lineup Lab season rankings chart"></a>
    <div class="project-body">
      <div class="meta">R Shiny · 2026 season</div>
      <h2><a href="{{ '/lineup-lab/' | relative_url }}">Lineup Lab: Grading How MLB Teams Order Their Lineups</a></h2>
      <p>An app that takes any 2026 MLB lineup and estimates how many runs a different batting order would add, then grades all 30 teams on how well they ordered their nine.</p>
      <div class="btn-row" style="margin-top:0">
        <a class="btn btn-primary" href="{{ '/lineup-lab/' | relative_url }}">Read the article</a>
        <a class="btn" href="{{ site.app_url }}" target="_blank" rel="noopener">Try the app ↗</a>
      </div>
    </div>
  </div>
</section>

<section class="contact">
  <div>
    <h2>Let's talk baseball.</h2>
    <p>The best way to reach me is email or LinkedIn.</p>
  </div>
  <div class="btn-row" style="margin-top:0">
    <a class="btn btn-primary" href="mailto:{{ site.email }}">{{ site.email }}</a>
    <a class="btn" href="{{ site.linkedin }}" target="_blank" rel="noopener">LinkedIn ↗</a>
  </div>
</section>
