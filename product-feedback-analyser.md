<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Product Feedback Analyser — Personal Project</title>
<meta name="description" content="A repeatable workflow for turning raw customer feedback into prioritised product opportunities, using Qualtrics, Excel and Microsoft Copilot.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="style.css">
</head>
<body>

<header class="site-header">
  <div class="container">
    <a href="/" class="logo">Product Feedback Analyser</a>
    <nav>
      <a href="#problem">Problem</a>
      <a href="#workflow">Workflow</a>
      <a href="#framework">Framework</a>
      <a href="#outcome">Outcome</a>
      <a href="full-design.html">Full design doc →</a>
    </nav>
  </div>
</header>

<main>

<section class="hero">
  <div class="container">
    <span class="eyebrow">Personal project · Product Feedback Analyser</span>
    <h1>Turning customer noise into prioritised product opportunities.</h1>
    <p class="lede">I designed a repeatable workflow that takes customer feedback from multiple channels, pulls out what actually matters, and turns it into a prioritised list of opportunities the team can act on. Built using Qualtrics, Excel and Microsoft Copilot.</p>
    <div class="meta-grid">
      <div><span class="meta-label">Role</span><span class="meta-value">Product Manager</span></div>
      <div><span class="meta-label">Tools</span><span class="meta-value">Qualtrics · Excel · Copilot</span></div>
      <div><span class="meta-label">Output</span><span class="meta-value">Workflow + scoring framework</span></div>
      <div><span class="meta-label">Type</span><span class="meta-value">Internal process design</span></div>
    </div>
  </div>
</section>

<section id="problem" class="section">
  <div class="container narrow">
    <span class="section-tag">01 · The problem</span>
    <h2>Feedback was everywhere. Insight was nowhere.</h2>
    <p>Customer feedback was coming in from surveys, support tickets, sales conversations and app reviews. All of it was sitting in different tools, owned by different people. Nobody had a clear picture of what customers were actually struggling with the most.</p>
    <p>The team was making roadmap decisions based on gut feel or whoever spoke loudest in the last meeting. Not because they didn't care about customer feedback, but because there was no practical way to pull it all together and make sense of it at scale.</p>
    <div class="callout">
      <strong>The problem wasn't a lack of feedback.</strong> It was that there was no repeatable way to synthesise it, prioritise it, and turn it into decisions.
    </div>
  </div>
</section>

<section id="workflow" class="section section-alt">
  <div class="container">
    <span class="section-tag">02 · The workflow</span>
    <h2>From raw comment to roadmap input, in ten steps.</h2>
    <p class="section-intro">I designed an end to end pipeline that any PM on the team could pick up and run. Each step has a clear owner, a clear output, and a clear handoff to the next.</p>

    <div class="workflow-grid">
      <div class="workflow-step"><span class="step-num">01</span><h3>Collect</h3><p>Gather feedback from Qualtrics surveys, support exports, app store reviews and interview notes.</p></div>
      <div class="workflow-step"><span class="step-num">02</span><h3>Consolidate</h3><p>Bring everything into one Excel workbook. One row per piece of feedback.</p></div>
      <div class="workflow-step"><span class="step-num">03</span><h3>Clean</h3><p>Remove duplicates, standardise dates, filter out anything off topic.</p></div>
      <div class="workflow-step"><span class="step-num">04</span><h3>Categorise</h3><p>Tag each row with the product area, customer segment and feedback type. Copilot drafts, I review.</p></div>
      <div class="workflow-step"><span class="step-num">05</span><h3>Detect themes</h3><p>Copilot clusters similar comments together. I then review and decide whether to confirm, split or merge them.</p></div>
      <div class="workflow-step"><span class="step-num">06</span><h3>Identify pain points</h3><p>Turn the themes into named pain points with severity and frequency counts.</p></div>
      <div class="workflow-step"><span class="step-num">07</span><h3>Generate opportunities</h3><p>Translate each pain point into a customer outcome led opportunity statement.</p></div>
      <div class="workflow-step"><span class="step-num">08</span><h3>Prioritise</h3><p>Score each opportunity against six criteria weighted for strategic alignment.</p></div>
      <div class="workflow-step"><span class="step-num">09</span><h3>Report</h3><p>Produce a stakeholder summary and a working PM summary for the monthly review.</p></div>
      <div class="workflow-step"><span class="step-num">10</span><h3>Feed roadmap</h3><p>Top opportunities go into backlog grooming and quarterly planning with the full evidence trail attached.</p></div>
    </div>
  </div>
</section>

<section id="framework" class="section">
  <div class="container narrow">
    <span class="section-tag">03 · The prioritisation framework</span>
    <h2>A scoring model that starts conversations, not ends them.</h2>
    <p>Every opportunity gets scored 1 to 5 against six criteria. Strategic alignment is weighted higher because it is the one that most often gets quietly ignored. Effort is weighted lower because it is the easiest to get wrong early on.</p>

    <table class="framework-table">
      <thead><tr><th>Criterion</th><th>What it measures</th><th>Weight</th></tr></thead>
      <tbody>
        <tr><td><strong>Frequency</strong></td><td>How often this came up across feedback</td><td>1.0</td></tr>
        <tr><td><strong>Severity</strong></td><td>How painful it is for the customer when it happens</td><td>1.0</td></tr>
        <tr><td><strong>Customer impact</strong></td><td>How broadly it affects different segments and areas</td><td>1.0</td></tr>
        <tr><td><strong>Strategic alignment</strong></td><td>How well it fits with where the product is heading</td><td>1.5</td></tr>
        <tr><td><strong>Confidence in evidence</strong></td><td>How strong and consistent the supporting feedback is</td><td>1.0</td></tr>
        <tr><td><strong>Implementation effort</strong></td><td>Inverse scoring. Lower effort scores higher</td><td>0.5</td></tr>
      </tbody>
    </table>

    <div class="formula-box">
      <span class="formula-label">Score formula</span>
      <code>(Freq × 1.0) + (Sev × 1.0) + (Impact × 1.0) + (Strategic × 1.5) + (Confidence × 1.0) + (Effort × 0.5)</code>
      <span class="formula-meta">Maximum possible: 30. The score is a starting point for the conversation, not the final answer.</span>
    </div>
  </div>
</section>

<section id="outcome" class="section section-alt">
  <div class="container narrow">
    <span class="section-tag">04 · The outcome</span>
    <h2>What changed.</h2>
    <p>The team went from making prioritisation decisions based on assumptions to having a clear, evidence backed process. Every opportunity in the backlog could be traced right back to the original customer comments that produced it. Instead of debating what customers might want, the conversation became about what to do with what they actually told us.</p>

    <div class="outcome-grid">
      <div class="outcome-card"><h3>Single source of truth</h3><p>All feedback in one place with a consistent way of tagging and organising it.</p></div>
      <div class="outcome-card"><h3>Repeatable rhythm</h3><p>Weekly hygiene, monthly synthesis, quarterly roadmap input. Any PM can run it.</p></div>
      <div class="outcome-card"><h3>Evidence trail</h3><p>Every opportunity links back to the actual customer voices that justify it.</p></div>
      <div class="outcome-card"><h3>Better conversations</h3><p>Less time arguing about what to build. More time deciding how to act on what customers said.</p></div>
    </div>
  </div>
</section>

<section class="section">
  <div class="container narrow">
    <span class="section-tag">05 · Reflection</span>
    <h2>What I would do differently.</h2>
    <p>Copilot is great as a fast first draft analyst but it is not a replacement for PM judgement. Early on I trusted its clustering more than I should have and a few themes ended up too broad to actually act on. The fix was adding a proper review step after every Copilot output and keeping the tag glossary tight. If I was starting again I would build that review gate in from day one instead of retrofitting it later.</p>
    <p>I would also start tracking how long each step takes sooner. Knowing which themes keep recurring month after month and which opportunities actually get acted on versus shelved is where the real learning lives.</p>
  </div>
</section>

<section class="section section-cta">
  <div class="container narrow">
    <h2>Want the full design document?</h2>
    <p>The complete workflow specification including the Excel workbook structure, Copilot prompts, a worked example with sample data, the operating model, and risks and limitations.</p>
    <a href="full-design.html" class="btn">Read the full design document →</a>
  </div>
</section>

</main>

<footer class="site-footer">
  <div class="container">
    <p>Designed and written by [Your Name] · <a href="https://github.com/[your-username]">GitHub</a> · <a href="mailto:[your-email]">Get in touch</a></p>
  </div>
</footer>

</body>
</html>
