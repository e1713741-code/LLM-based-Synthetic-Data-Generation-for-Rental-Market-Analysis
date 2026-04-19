# LLM-based-Synthetic-Data-Generation-for-Rental-Market-Analysis
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RA Work Log — 19 April 2026</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Source+Sans+3:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #1a1a2e;
    --ink-light: #3d3d5c;
    --ink-muted: #6b6b8d;
    --bg: #faf9f7;
    --bg-warm: #f3f1ed;
    --accent: #2563eb;
    --accent-light: #dbeafe;
    --accent-dark: #1e40af;
    --green: #059669;
    --green-light: #d1fae5;
    --amber: #d97706;
    --amber-light: #fef3c7;
    --red: #dc2626;
    --red-light: #fee2e2;
    --border: #e5e3df;
    --serif: 'DM Serif Display', Georgia, serif;
    --sans: 'Source Sans 3', -apple-system, sans-serif;
    --mono: 'JetBrains Mono', monospace;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: var(--sans);
    background: var(--bg);
    color: var(--ink);
    line-height: 1.7;
    font-size: 15px;
    -webkit-font-smoothing: antialiased;
  }

  .page {
    max-width: 780px;
    margin: 0 auto;
    padding: 60px 40px 80px;
  }

  /* ── Header ── */
  .header {
    margin-bottom: 48px;
    padding-bottom: 32px;
    border-bottom: 2px solid var(--ink);
  }

  .header-label {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 8px;
  }

  .header-title {
    font-family: var(--serif);
    font-size: 32px;
    line-height: 1.2;
    color: var(--ink);
    margin-bottom: 16px;
  }

  .header-meta {
    display: flex;
    gap: 24px;
    flex-wrap: wrap;
    font-size: 13.5px;
    color: var(--ink-muted);
  }

  .header-meta span {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .header-meta .dot {
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: var(--ink-muted);
    display: inline-block;
  }

  /* ── Sections ── */
  .section {
    margin-bottom: 40px;
  }

  .section-title {
    font-family: var(--serif);
    font-size: 21px;
    color: var(--ink);
    margin-bottom: 16px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
  }

  .section p {
    color: var(--ink-light);
    margin-bottom: 12px;
  }

  /* ── Dataset Overview Cards ── */
  .dataset-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin: 16px 0 20px;
  }

  .stat-card {
    background: white;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 16px;
    text-align: center;
  }

  .stat-card .number {
    font-family: var(--mono);
    font-size: 26px;
    font-weight: 500;
    color: var(--accent-dark);
    line-height: 1.2;
  }

  .stat-card .label {
    font-size: 12px;
    color: var(--ink-muted);
    margin-top: 4px;
    line-height: 1.3;
  }

  .dataset-note {
    background: var(--bg-warm);
    border-left: 3px solid var(--amber);
    padding: 12px 16px;
    border-radius: 0 6px 6px 0;
    font-size: 13.5px;
    color: var(--ink-light);
    margin-top: 12px;
  }

  .dataset-note code {
    font-family: var(--mono);
    font-size: 12.5px;
    background: white;
    padding: 1px 5px;
    border-radius: 3px;
    color: var(--accent-dark);
  }

  /* ── Task Blocks ── */
  .task-block {
    background: white;
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 24px;
    margin-bottom: 20px;
    position: relative;
    overflow: hidden;
  }

  .task-block::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 4px;
    height: 100%;
  }

  .task-block.task1::before { background: var(--accent); }
  .task-block.task2::before { background: var(--red); }
  .task-block.task3::before { background: var(--green); }

  .task-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 12px;
  }

  .task-badge {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 500;
    padding: 3px 8px;
    border-radius: 4px;
    letter-spacing: 0.5px;
  }

  .task1 .task-badge { background: var(--accent-light); color: var(--accent-dark); }
  .task2 .task-badge { background: var(--red-light); color: var(--red); }
  .task3 .task-badge { background: var(--green-light); color: var(--green); }

  .task-name {
    font-weight: 600;
    font-size: 16px;
    color: var(--ink);
  }

  .task-def {
    font-size: 13.5px;
    color: var(--ink-muted);
    margin-bottom: 16px;
    padding: 10px 14px;
    background: var(--bg);
    border-radius: 6px;
    line-height: 1.6;
  }

  .task-result-headline {
    font-family: var(--mono);
    font-size: 28px;
    font-weight: 500;
    margin-bottom: 4px;
  }

  .task1 .task-result-headline { color: var(--accent-dark); }
  .task2 .task-result-headline { color: var(--red); }
  .task3 .task-result-headline { color: var(--green); }

  .task-result-subtitle {
    font-size: 13px;
    color: var(--ink-muted);
    margin-bottom: 16px;
  }

  .task-findings {
    list-style: none;
    padding: 0;
  }

  .task-findings li {
    position: relative;
    padding-left: 18px;
    margin-bottom: 8px;
    font-size: 14px;
    color: var(--ink-light);
    line-height: 1.6;
  }

  .task-findings li::before {
    content: '→';
    position: absolute;
    left: 0;
    color: var(--ink-muted);
    font-weight: 600;
  }

  .task-findings strong {
    color: var(--ink);
    font-weight: 600;
  }

  /* ── Breakdown Bar ── */
  .breakdown {
    margin: 16px 0 12px;
  }

  .breakdown-bar {
    display: flex;
    height: 28px;
    border-radius: 6px;
    overflow: hidden;
    margin-bottom: 10px;
  }

  .breakdown-bar .seg {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 11px;
    font-weight: 600;
    color: white;
    font-family: var(--mono);
  }

  .seg-real { background: var(--green); }
  .seg-interp { background: var(--amber); }
  .seg-nodata { background: #94a3b8; }

  .breakdown-legend {
    display: flex;
    gap: 20px;
    font-size: 12.5px;
    color: var(--ink-muted);
  }

  .breakdown-legend span {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .legend-dot {
    width: 10px;
    height: 10px;
    border-radius: 2px;
    display: inline-block;
  }

  .breakdown-legend strong {
    color: var(--ink);
    font-family: var(--mono);
    font-size: 12px;
  }

  /* ── Deliverables ── */
  .file-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-top: 12px;
  }

  .file-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 14px;
    background: white;
    border: 1px solid var(--border);
    border-radius: 6px;
    font-size: 13px;
  }

  .file-icon {
    font-size: 18px;
    width: 28px;
    text-align: center;
  }

  .file-name {
    font-family: var(--mono);
    font-size: 12.5px;
    color: var(--accent-dark);
  }

  .file-desc {
    font-size: 11.5px;
    color: var(--ink-muted);
  }

  /* ── Technical & Next Steps ── */
  .tech-list {
    list-style: none;
    padding: 0;
  }

  .tech-list li {
    position: relative;
    padding-left: 20px;
    margin-bottom: 10px;
    font-size: 14px;
    color: var(--ink-light);
    line-height: 1.6;
  }

  .tech-list li::before {
    content: '▸';
    position: absolute;
    left: 0;
    color: var(--accent);
    font-weight: 700;
  }

  .next-steps {
    background: var(--accent-light);
    border-radius: 8px;
    padding: 20px 24px;
  }

  .next-steps-title {
    font-weight: 700;
    font-size: 14px;
    color: var(--accent-dark);
    margin-bottom: 8px;
    letter-spacing: 0.5px;
    text-transform: uppercase;
    font-size: 11px;
  }

  .next-steps p {
    font-size: 14px;
    color: var(--ink-light);
    margin-bottom: 6px;
  }

  /* ── Footer ── */
  .footer {
    margin-top: 48px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
    font-size: 12px;
    color: var(--ink-muted);
    text-align: center;
  }
</style>
</head>
<body>
<div class="page">

  <!-- Header -->
  <div class="header">
    <div class="header-label">RA Work Log</div>
    <h1 class="header-title">LLM-Based Synthetic Data Generation<br>for Rental Market Analysis</h1>
    <div class="header-meta">
      <span>📅 19 April 2026</span>
      <span class="dot"></span>
      <span>👤 Supervised by Dr. Jun Hu / Prof. Bingsheng He</span>
      <span class="dot"></span>
      <span>🏛 NUS School of Computing</span>
    </div>
  </div>

  <!-- Background -->
  <div class="section">
    <h2 class="section-title">Task Background</h2>
    <p>Following the project meeting on 9 April, I conducted a data quality audit on the Singapore CCR (Core Central Region) condominium rental price dataset. The objective was to assess the distribution of real versus linearly interpolated data points across the time series, establishing a quantitative baseline for the next phase of data imputation optimization — transitioning from linear interpolation to LLM-based generation.</p>
  </div>

  <!-- Dataset Overview -->
  <div class="section">
    <h2 class="section-title">Dataset Overview</h2>
    <div class="dataset-grid">
      <div class="stat-card">
        <div class="number">961</div>
        <div class="label">Condo Projects</div>
      </div>
      <div class="stat-card">
        <div class="number">315</div>
        <div class="label">Monthly Timesteps</div>
      </div>
      <div class="stat-card">
        <div class="number">346</div>
        <div class="label">Feature Columns</div>
      </div>
    </div>
    <p>Source: URA (Urban Redevelopment Authority) private residential rental data, preprocessed and split into per-timestep CSV files covering November 1999 through January 2026. Each file contains one row per project with geographic coordinates, macroeconomic indicators, amenity features, rental price, and a <code>y_mask</code> validity label.</p>
    <div class="dataset-note">
      <strong>Labeling convention:</strong> <code>y_mask=1</code> → real rental price; <code>y_mask=0</code> with <code>rent&gt;0</code> → linearly interpolated (invalid); <code>y_mask=0</code> with <code>rent=0</code> → no data.
    </div>
  </div>

  <!-- Task 1 -->
  <div class="task-block task1">
    <div class="task-header">
      <span class="task-badge">TASK 1</span>
      <span class="task-name">Projects with Data Emerging After 2021</span>
    </div>
    <div class="task-def">Identify projects that have real data (y_mask=1) from 2021 onward, but either had no real data before 2021, or had a gap of more than 24 months between their last real entry and January 2021.</div>
    <div class="task-result-headline">75 projects</div>
    <div class="task-result-subtitle">met the criteria out of 961 total</div>
    <ul class="task-findings">
      <li><strong>61 projects</strong> had zero real rental records before 2021, with first real data points appearing between 2022 and 2025</li>
      <li><strong>14 projects</strong> had real records before 2021 but with extended gaps exceeding 24 months (ranging from 35 to 216 months)</li>
      <li>Most extreme case: <strong>TANJONG PAGAR CONSERVATION AREA</strong> — last real record in April 2003, a gap of 216 months (18 years), with data not reappearing until May 2024</li>
    </ul>
  </div>

  <!-- Task 2 -->
  <div class="task-block task2">
    <div class="task-header">
      <span class="task-badge">TASK 2</span>
      <span class="task-name">Projects That Disappeared After 2021</span>
    </div>
    <div class="task-def">Identify projects with real rental records before 2021 that experienced 60+ consecutive months (5 years) without any real data after 2021.</div>
    <div class="task-result-headline">69 projects</div>
    <div class="task-result-subtitle">completely vanished from the dataset post-2021</div>
    <ul class="task-findings">
      <li>All <strong>69 projects</strong> had exactly zero real data points after January 2021 — none showed even occasional valid records</li>
      <li>Last real records for these projects ranged from <strong>2006 to 2020</strong></li>
      <li>Representative cases: QUEEN ASTRID PARK (last record Mar 2017), PARK HOUSE (Jan 2019), MONTCLAIR @ WHITLEY (Aug 2020)</li>
    </ul>
  </div>

  <!-- Task 3 -->
  <div class="task-block task3">
    <div class="task-header">
      <span class="task-badge">TASK 3</span>
      <span class="task-name">Data Quality Breakdown — Task 1 Projects</span>
    </div>
    <div class="task-def">For the 75 projects identified in Task 1, count data points with y_mask=1 (real price) vs. rent&gt;0 with y_mask=0 (interpolated price) across all 315 timesteps.</div>
    <div class="task-result-headline">23,625 data points</div>
    <div class="task-result-subtitle">75 projects × 315 timesteps</div>

    <div class="breakdown">
      <div class="breakdown-bar">
        <div class="seg seg-real" style="width:5.2%">5.2%</div>
        <div class="seg seg-interp" style="width:14.2%">14.2%</div>
        <div class="seg seg-nodata" style="width:80.6%">80.7%</div>
      </div>
      <div class="breakdown-legend">
        <span><span class="legend-dot" style="background:var(--green)"></span>Real price <strong>1,225</strong></span>
        <span><span class="legend-dot" style="background:var(--amber)"></span>Interpolated <strong>3,346</strong></span>
        <span><span class="legend-dot" style="background:#94a3b8"></span>No data <strong>19,054</strong></span>
      </div>
    </div>

    <ul class="task-findings">
      <li>These projects are extremely data-sparse: on average only <strong>16.3 real data points</strong> per project (1,225 ÷ 75), covering roughly 5% of timesteps</li>
      <li>Highest interpolation density: <strong>CROWN CENTRE</strong> — 285/315 timesteps interpolated (90.5%), with only 9 real data points</li>
      <li>Interpolated data outnumbers real data by a factor of <strong>2.7×</strong> within this subset</li>
    </ul>
  </div>

  <!-- Deliverables -->
  <div class="section">
    <h2 class="section-title">Deliverables</h2>
    <div class="file-list">
      <div class="file-item">
        <div class="file-icon">🐍</div>
        <div>
          <div class="file-name">analysis_v2.py</div>
          <div class="file-desc">Complete analysis script</div>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">📊</div>
        <div>
          <div class="file-name">task1_results.csv</div>
          <div class="file-desc">75 projects — emerging data</div>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">📊</div>
        <div>
          <div class="file-name">task2_results.csv</div>
          <div class="file-desc">69 projects — disappeared</div>
        </div>
      </div>
      <div class="file-item">
        <div class="file-icon">📊</div>
        <div>
          <div class="file-name">task3_results.csv</div>
          <div class="file-desc">75 projects — quality breakdown</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Technical Approach -->
  <div class="section">
    <h2 class="section-title">Technical Approach</h2>
    <ul class="tech-list">
      <li>Read and restructured 315 timestep CSV files using Python and Pandas, transforming the data from a per-timestep layout into a per-project time series view suitable for longitudinal analysis</li>
      <li>Classified data validity using combined conditions on the <code style="font-family:var(--mono);font-size:12.5px;background:var(--bg-warm);padding:1px 5px;border-radius:3px;">y_mask</code> and <code style="font-family:var(--mono);font-size:12.5px;background:var(--bg-warm);padding:1px 5px;border-radius:3px;">rent_per_sqft</code> fields to distinguish real, interpolated, and missing data</li>
      <li>Implemented a consecutive-gap scanner across each project's time series to detect maximum durations of missing real data, enabling identification of emerging and disappearing projects</li>
    </ul>
  </div>

  <!-- Next Steps -->
  <div class="section">
    <div class="next-steps">
      <div class="next-steps-title">Next Steps</div>
      <p>→ Await feedback from Cici on whether the statistical results and task definitions align with expectations</p>
      <p>→ Use these statistics as a quantitative baseline for the next phase: optimizing data imputation from linear interpolation to LLM-based synthetic generation</p>
    </div>
  </div>

  <div class="footer">
    RA Work Log — NUS School of Computing — LLM-Based Synthetic Data Generation for Rental Market Analysis
  </div>

</div>
</body>
</html>
