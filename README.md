<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Alpha Myn — Candidate Assessment</title>
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Share+Tech+Mono&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #0a0a0a;
    --panel: #161b22;
    --border: #2a3040;
    --gold: #f0a500;
    --gold-dim: #c47f00;
    --orange: #e05a00;
    --text: #d4dbe8;
    --muted: #6b7a94;
    --green: #22c55e;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--black); color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 15px; line-height: 1.6; min-height: 100vh; }
  body::before {
    content: ''; position: fixed; inset: 0;
    background-image: linear-gradient(rgba(240,165,0,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(240,165,0,0.03) 1px, transparent 1px);
    background-size: 40px 40px; pointer-events: none; z-index: 0;
  }
  .wrapper { position: relative; z-index: 1; max-width: 760px; margin: 0 auto; padding: 40px 20px 80px; }
  .header { text-align: center; margin-bottom: 48px; padding: 48px 32px; border: 1px solid var(--border); background: linear-gradient(160deg, #161b22 0%, #0e1217 100%); position: relative; overflow: hidden; }
  .header::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; background: linear-gradient(90deg, transparent, var(--gold), var(--orange), var(--gold), transparent); }
  .logo-text { font-family: 'Bebas Neue', sans-serif; font-size: clamp(52px, 10vw, 80px); letter-spacing: 0.12em; color: var(--gold); line-height: 1; text-shadow: 0 0 40px rgba(240,165,0,0.3); }
  .logo-sub { font-family: 'Share Tech Mono', monospace; font-size: 11px; letter-spacing: 0.3em; color: var(--muted); text-transform: uppercase; margin-top: 6px; }
  .header-divider { width: 60px; height: 2px; background: var(--gold); margin: 20px auto; }
  .header h2 { font-family: 'Bebas Neue', sans-serif; font-size: 22px; letter-spacing: 0.15em; color: var(--text); margin-bottom: 10px; }
  .header p { color: var(--muted); font-size: 14px; max-width: 480px; margin: 0 auto; line-height: 1.7; }
  .progress-bar-wrap { margin-bottom: 32px; }
  .progress-meta { display: flex; justify-content: space-between; font-family: 'Share Tech Mono', monospace; font-size: 11px; color: var(--muted); letter-spacing: 0.1em; margin-bottom: 8px; }
  .progress-track { height: 4px; background: var(--border); border-radius: 2px; overflow: hidden; }
  .progress-fill { height: 100%; background: linear-gradient(90deg, var(--gold), var(--orange)); border-radius: 2px; transition: width 0.4s ease; width: 0%; }
  .section { margin-bottom: 32px; }
  .section-label { font-family: 'Share Tech Mono', monospace; font-size: 10px; letter-spacing: 0.35em; text-transform: uppercase; color: var(--gold); margin-bottom: 20px; display: flex; align-items: center; gap: 12px; }
  .section-label::after { content: ''; flex: 1; height: 1px; background: var(--border); }
  .q-card { background: var(--panel); border: 1px solid var(--border); border-radius: 4px; padding: 22px 24px; margin-bottom: 16px; transition: border-color 0.2s; }
  .q-card.error { border-color: rgba(239,68,68,0.5); }
  .q-label { font-size: 14px; font-weight: 500; color: var(--text); margin-bottom: 14px; line-height: 1.5; }
  .q-num { font-family: 'Share Tech Mono', monospace; font-size: 10px; color: var(--gold); letter-spacing: 0.1em; display: block; margin-bottom: 5px; }
  .q-input { width: 100%; background: var(--black); border: 1px solid var(--border); border-radius: 3px; color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 14px; padding: 10px 14px; outline: none; transition: border-color 0.2s; -webkit-appearance: none; appearance: none; }
  .q-input:focus { border-color: var(--gold-dim); }
  textarea.q-input { resize: vertical; min-height: 80px; }
  .options-grid { display: flex; flex-direction: column; gap: 8px; }
  .options-grid.two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  @media (max-width: 480px) { .options-grid.two-col { grid-template-columns: 1fr; } }
  .opt-label { display: flex; align-items: center; gap: 10px; background: var(--black); border: 1px solid var(--border); border-radius: 3px; padding: 10px 14px; cursor: pointer; transition: border-color 0.2s, background 0.2s; font-size: 13.5px; color: var(--text); user-select: none; }
  .opt-label:hover { border-color: var(--gold-dim); background: rgba(240,165,0,0.04); }
  input[type="radio"], input[type="checkbox"] { appearance: none; -webkit-appearance: none; width: 16px; height: 16px; border: 1.5px solid var(--border); border-radius: 50%; flex-shrink: 0; position: relative; transition: border-color 0.2s; cursor: pointer; }
  input[type="checkbox"] { border-radius: 3px; }
  input[type="radio"]:checked, input[type="checkbox"]:checked { border-color: var(--gold); background: var(--gold); }
  input[type="radio"]:checked::after { content: ''; position: absolute; inset: 3px; border-radius: 50%; background: var(--black); }
  input[type="checkbox"]:checked::after { content: '✓'; position: absolute; inset: 0; display: flex; align-items: center; justify-content: center; font-size: 10px; color: var(--black); font-weight: 700; line-height: 1; text-align: center; padding-top: 1px; }
  input[type="radio"]:checked ~ span, input[type="checkbox"]:checked ~ span { color: var(--gold); }
  .pay-wrap { display: flex; align-items: center; gap: 8px; }
  .pay-prefix { font-family: 'Share Tech Mono', monospace; font-size: 16px; color: var(--gold); flex-shrink: 0; }
  .pay-note { font-size: 12px; color: var(--muted); margin-top: 8px; }
  .submit-area { margin-top: 40px; text-align: center; }
  .error-msg { background: rgba(239,68,68,0.1); border: 1px solid rgba(239,68,68,0.3); color: #fca5a5; border-radius: 4px; padding: 12px 16px; font-size: 13px; margin-bottom: 20px; display: none; }
  .error-msg.show { display: block; }
  .submit-btn { background: linear-gradient(135deg, var(--gold), var(--orange)); color: var(--black); border: none; border-radius: 3px; font-family: 'Bebas Neue', sans-serif; font-size: 20px; letter-spacing: 0.15em; padding: 16px 56px; cursor: pointer; transition: opacity 0.2s, transform 0.1s; }
  .submit-btn:hover { opacity: 0.9; transform: translateY(-1px); }
  .submit-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }
  .submit-note { font-size: 12px; color: var(--muted); margin-top: 12px; font-family: 'Share Tech Mono', monospace; }
  #confirmation { display: none; text-align: center; background: var(--panel); border: 1px solid rgba(34,197,94,0.3); border-radius: 4px; padding: 56px 32px; margin-top: 32px; position: relative; }
  #confirmation::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; background: var(--green); }
  .confirm-icon { width: 64px; height: 64px; background: rgba(34,197,94,0.1); border: 1.5px solid rgba(34,197,94,0.4); border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 24px; font-size: 28px; }
  #confirmation h2 { font-family: 'Bebas Neue', sans-serif; font-size: 32px; letter-spacing: 0.15em; color: var(--green); margin-bottom: 12px; }
  #confirmation p { color: var(--muted); font-size: 14px; max-width: 400px; margin: 0 auto; }
  .field-error { font-size: 11px; color: #fca5a5; margin-top: 6px; display: none; font-family: 'Share Tech Mono', monospace; }
  .field-error.show { display: block; }
  .req { color: var(--gold); margin-left: 2px; }
</style>
</head>
<body>
<div class="wrapper">

  <div class="header">
    <div class="logo-text">ALPHA MYN</div>
    <div class="logo-sub">Bitcoin Mining Operations</div>
    <div class="header-divider"></div>
    <h2>CANDIDATE ASSESSMENT</h2>
    <p>Site Operations Technician — Gage, Oklahoma Region<br>Complete all fields honestly. This helps us determine if you're a strong fit for an interview.</p>
  </div>

  <div class="progress-bar-wrap">
    <div class="progress-meta"><span>COMPLETION</span><span id="pct-label">0%</span></div>
    <div class="progress-track"><div class="progress-fill" id="progress-fill"></div></div>
  </div>

  <form id="quiz-form" novalidate>

```
<div class="section">
  <div class="section-label">01 — Contact Information</div>
  <div class="q-card" id="card-name">
    <span class="q-num">Q1</span>
    <div class="q-label">Full Name <span class="req">*</span></div>
    <input type="text" class="q-input" id="q-name" placeholder="First and Last Name">
    <div class="field-error" id="err-name">Please enter your full name.</div>
  </div>
  <div class="q-card" id="card-phone">
    <span class="q-num">Q2</span>
    <div class="q-label">Phone Number <span class="req">*</span></div>
    <input type="tel" class="q-input" id="q-phone" placeholder="(555) 000-0000">
    <div class="field-error" id="err-phone">Please enter your phone number.</div>
  </div>
  <div class="q-card" id="card-email">
    <span class="q-num">Q3</span>
    <div class="q-label">Email Address <span class="req">*</span></div>
    <input type="email" class="q-input" id="q-email" placeholder="you@example.com">
    <div class="field-error" id="err-email">Please enter a valid email address.</div>
  </div>
  <div class="q-card" id="card-city">
    <span class="q-num">Q4</span>
    <div class="q-label">Current City &amp; State <span class="req">*</span></div>
    <input type="text" class="q-input" id="q-city" placeholder="e.g. Woodward, OK">
    <div class="field-error" id="err-city">Please enter your city and state.</div>
  </div>
</div>

<div class="section">
  <div class="section-label">02 — Location &amp; Availability</div>
  <div class="q-card" id="card-distance">
    <span class="q-num">Q5</span>
    <div class="q-label">How far do you currently live from Gage, Oklahoma? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="distance" value="Within 30 minutes"><span>Within 30 minutes</span></label>
      <label class="opt-label"><input type="radio" name="distance" value="30-60 minutes away"><span>30–60 minutes away</span></label>
      <label class="opt-label"><input type="radio" name="distance" value="More than 1 hour away"><span>More than 1 hour away</span></label>
      <label class="opt-label"><input type="radio" name="distance" value="Outside area - willing to relocate"><span>Outside area, but willing to relocate soon</span></label>
    </div>
    <div class="field-error" id="err-distance">Please select an option.</div>
  </div>
  <div class="q-card" id="card-relocate" style="display:none;">
    <span class="q-num">Q5b</span>
    <div class="q-label">If relocating — expected timeline to be near Gage, OK?</div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="relocate_timeline" value="Within 30 days"><span>Within 30 days</span></label>
      <label class="opt-label"><input type="radio" name="relocate_timeline" value="Within 60 days"><span>Within 60 days</span></label>
      <label class="opt-label"><input type="radio" name="relocate_timeline" value="Within 90 days"><span>Within 90 days</span></label>
      <label class="opt-label"><input type="radio" name="relocate_timeline" value="Not sure yet"><span>Not sure yet</span></label>
    </div>
  </div>
  <div class="q-card" id="card-transport">
    <span class="q-num">Q6</span>
    <div class="q-label">Do you have reliable personal transportation? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="transport" value="Yes"><span>Yes</span></label>
      <label class="opt-label"><input type="radio" name="transport" value="No"><span>No</span></label>
    </div>
    <div class="field-error" id="err-transport">Please select an option.</div>
  </div>
  <div class="q-card" id="card-emergency">
    <span class="q-num">Q7</span>
    <div class="q-label">Available for occasional after-hours or emergency call-outs? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="emergency" value="Yes"><span>Yes</span></label>
      <label class="opt-label"><input type="radio" name="emergency" value="Sometimes"><span>Sometimes</span></label>
      <label class="opt-label"><input type="radio" name="emergency" value="No"><span>No</span></label>
    </div>
    <div class="field-error" id="err-emergency">Please select an option.</div>
  </div>
</div>

<div class="section">
  <div class="section-label">03 — Generator &amp; Mechanical Skills</div>
  <div class="q-card" id="card-oilchange">
    <span class="q-num">Q8</span>
    <div class="q-label">Have you performed oil changes on large industrial engines (625 kW generator)? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="oilchange" value="Yes - industrial/generator engines"><span>Yes — on industrial/generator engines specifically</span></label>
      <label class="opt-label"><input type="radio" name="oilchange" value="Yes - vehicles or smaller engines"><span>Yes — on vehicles or smaller engines</span></label>
      <label class="opt-label"><input type="radio" name="oilchange" value="Yes - both"><span>Yes — both industrial and vehicles</span></label>
      <label class="opt-label"><input type="radio" name="oilchange" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-oilchange">Please select an option.</div>
  </div>
  <div class="q-card" id="card-filters">
    <span class="q-num">Q9</span>
    <div class="q-label">Experience changing oil, air, and fuel filters on large engines? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="filters" value="Experienced - comfortable solo"><span>Experienced — comfortable solo</span></label>
      <label class="opt-label"><input type="radio" name="filters" value="Some experience with guidance"><span>Some experience — with guidance</span></label>
      <label class="opt-label"><input type="radio" name="filters" value="Basic - limited hands-on"><span>Basic — limited hands-on</span></label>
      <label class="opt-label"><input type="radio" name="filters" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-filters">Please select an option.</div>
  </div>
  <div class="q-card" id="card-sparkplugs">
    <span class="q-num">Q10</span>
    <div class="q-label">Have you replaced spark plugs on a large natural gas engine? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="sparkplugs" value="Yes - large industrial/gas engines"><span>Yes — on large industrial/gas engines</span></label>
      <label class="opt-label"><input type="radio" name="sparkplugs" value="Yes - automotive only"><span>Yes — automotive engines only</span></label>
      <label class="opt-label"><input type="radio" name="sparkplugs" value="No but willing to learn"><span>No, but confident I can learn quickly</span></label>
      <label class="opt-label"><input type="radio" name="sparkplugs" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-sparkplugs">Please select an option.</div>
  </div>
  <div class="q-card" id="card-genexp">
    <span class="q-num">Q11</span>
    <div class="q-label">Describe any generator maintenance experience. <span class="req">*</span></div>
    <textarea class="q-input" id="q-genexp" placeholder='Brand, size, tasks, duration... (or enter "None")' rows="4"></textarea>
    <div class="field-error" id="err-genexp">Please describe your experience or enter "None".</div>
  </div>
  <div class="q-card" id="card-fluids">
    <span class="q-num">Q12</span>
    <div class="q-label">Which fluids are you comfortable maintaining? <span class="req">*</span> (Select all that apply)</div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="checkbox" name="fluids" value="Engine Oil"><span>Engine Oil</span></label>
      <label class="opt-label"><input type="checkbox" name="fluids" value="Coolant"><span>Coolant</span></label>
      <label class="opt-label"><input type="checkbox" name="fluids" value="Fuel System"><span>Fuel System</span></label>
      <label class="opt-label"><input type="checkbox" name="fluids" value="None"><span>None</span></label>
    </div>
    <div class="field-error" id="err-fluids">Please select at least one option.</div>
  </div>
</div>

<div class="section">
  <div class="section-label">04 — Natural Gas &amp; Field Operations</div>
  <div class="q-card" id="card-natgas">
    <span class="q-num">Q13</span>
    <div class="q-label">Experience with natural gas fuel systems or pressure regulators? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="natgas" value="Yes - extensive"><span>Yes — extensive</span></label>
      <label class="opt-label"><input type="radio" name="natgas" value="Yes - some"><span>Yes — some experience</span></label>
      <label class="opt-label"><input type="radio" name="natgas" value="Safety training only"><span>Safety training only</span></label>
      <label class="opt-label"><input type="radio" name="natgas" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-natgas">Please select an option.</div>
  </div>
  <div class="q-card" id="card-pressure">
    <span class="q-num">Q14</span>
    <div class="q-label">Have you monitored fuel/gas delivery pressures using gauges? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="pressure" value="Yes - regularly"><span>Yes — regularly</span></label>
      <label class="opt-label"><input type="radio" name="pressure" value="Yes - occasionally"><span>Yes — occasionally</span></label>
      <label class="opt-label"><input type="radio" name="pressure" value="Understand the concept"><span>No, but I understand the concept</span></label>
      <label class="opt-label"><input type="radio" name="pressure" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-pressure">Please select an option.</div>
  </div>
  <div class="q-card" id="card-oilfield">
    <span class="q-num">Q15</span>
    <div class="q-label">Do you have oil &amp; gas field operations experience? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="oilfield" value="Yes"><span>Yes</span></label>
      <label class="opt-label"><input type="radio" name="oilfield" value="No"><span>No</span></label>
    </div>
    <div class="field-error" id="err-oilfield">Please select an option.</div>
  </div>
  <div class="q-card" id="card-oilfield-detail" style="display:none;">
    <span class="q-num">Q15b</span>
    <div class="q-label">Describe your oil &amp; gas field experience.</div>
    <textarea class="q-input" id="q-oilfield-detail" placeholder="Role, company, equipment, duration..." rows="3"></textarea>
  </div>
</div>

<div class="section">
  <div class="section-label">05 — Technology &amp; Problem-Solving</div>
  <div class="q-card" id="card-techskill">
    <span class="q-num">Q16</span>
    <div class="q-label">Comfort level with technology (computers, smartphones, monitoring software)? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="techskill" value="Advanced - troubleshoot confidently"><span>Advanced — troubleshoot confidently</span></label>
      <label class="opt-label"><input type="radio" name="techskill" value="Comfortable - learn quickly"><span>Comfortable — learn new tools quickly</span></label>
      <label class="opt-label"><input type="radio" name="techskill" value="Basic"><span>Basic — use standard tools only</span></label>
      <label class="opt-label"><input type="radio" name="techskill" value="Limited"><span>Limited</span></label>
    </div>
    <div class="field-error" id="err-techskill">Please select an option.</div>
  </div>
  <div class="q-card" id="card-network">
    <span class="q-num">Q17</span>
    <div class="q-label">Experience with computer networks or IT equipment? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="network" value="Yes - professional"><span>Yes — professional IT/networking</span></label>
      <label class="opt-label"><input type="radio" name="network" value="Yes - self-taught"><span>Yes — self-taught/hobby level</span></label>
      <label class="opt-label"><input type="radio" name="network" value="Basic - reboot and follow instructions"><span>Basic — can reboot and follow instructions</span></label>
      <label class="opt-label"><input type="radio" name="network" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-network">Please select an option.</div>
  </div>
  <div class="q-card" id="card-datacenter">
    <span class="q-num">Q18</span>
    <div class="q-label">Have you worked with ASIC miners, servers, or industrial compute hardware? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="datacenter" value="Yes - Bitcoin/crypto mining"><span>Yes — Bitcoin/crypto mining hardware</span></label>
      <label class="opt-label"><input type="radio" name="datacenter" value="Yes - data center/servers"><span>Yes — data center/server equipment</span></label>
      <label class="opt-label"><input type="radio" name="datacenter" value="No but fast learner"><span>No, but very interested and fast learner</span></label>
      <label class="opt-label"><input type="radio" name="datacenter" value="No experience"><span>No experience</span></label>
    </div>
    <div class="field-error" id="err-datacenter">Please select an option.</div>
  </div>
  <div class="q-card" id="card-problem">
    <span class="q-num">Q19</span>
    <div class="q-label">Describe a time you identified and solved a mechanical or equipment problem on your own. <span class="req">*</span></div>
    <textarea class="q-input" id="q-problem" placeholder="What broke, how you diagnosed it, what you did..." rows="4"></textarea>
    <div class="field-error" id="err-problem">Please describe a problem-solving example.</div>
  </div>
  <div class="q-card" id="card-reporting">
    <span class="q-num">Q20</span>
    <div class="q-label">Comfortable submitting written inspection reports via phone or computer? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="reporting" value="Yes - no problem"><span>Yes, no problem</span></label>
      <label class="opt-label"><input type="radio" name="reporting" value="Somewhat comfortable"><span>Somewhat</span></label>
      <label class="opt-label"><input type="radio" name="reporting" value="Challenging"><span>Would be challenging</span></label>
    </div>
    <div class="field-error" id="err-reporting">Please select an option.</div>
  </div>
</div>

<div class="section">
  <div class="section-label">06 — Work History &amp; Background</div>
  <div class="q-card" id="card-education">
    <span class="q-num">Q21</span>
    <div class="q-label">Highest level of education or training completed <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="education" value="High school diploma / GED"><span>High school diploma / GED</span></label>
      <label class="opt-label"><input type="radio" name="education" value="Technical / vocational certification"><span>Technical / vocational certification</span></label>
      <label class="opt-label"><input type="radio" name="education" value="Some college"><span>Some college</span></label>
      <label class="opt-label"><input type="radio" name="education" value="Associate's degree"><span>Associate's degree</span></label>
      <label class="opt-label"><input type="radio" name="education" value="Bachelor's degree or higher"><span>Bachelor's degree or higher</span></label>
    </div>
    <div class="field-error" id="err-education">Please select an option.</div>
  </div>
  <div class="q-card" id="card-independent">
    <span class="q-num">Q22</span>
    <div class="q-label">Comfortable working independently at a remote site with minimal supervision? <span class="req">*</span></div>
    <div class="options-grid">
      <label class="opt-label"><input type="radio" name="independent" value="Very comfortable - prefer it"><span>Very comfortable — I prefer it</span></label>
      <label class="opt-label"><input type="radio" name="independent" value="Comfortable - limited check-ins ok"><span>Comfortable — limited check-ins ok</span></label>
      <label class="opt-label"><input type="radio" name="independent" value="Prefer regular guidance"><span>I prefer regular guidance</span></label>
    </div>
    <div class="field-error" id="err-independent">Please select an option.</div>
  </div>
  <div class="q-card" id="card-workhistory">
    <span class="q-num">Q23</span>
    <div class="q-label">Most relevant work experience (last 1–3 positions). <span class="req">*</span></div>
    <textarea class="q-input" id="q-workhistory" placeholder="Job title, company, dates, what you did..." rows="4"></textarea>
    <div class="field-error" id="err-workhistory">Please describe your relevant work history.</div>
  </div>
  <div class="q-card" id="card-growth">
    <span class="q-num">Q24</span>
    <div class="q-label">Alpha Myn is a growing Bitcoin mining operation with significant long-term potential. What interests you most about this opportunity? <span class="req">*</span></div>
    <textarea class="q-input" id="q-growth" placeholder="Tell us what draws you to this role..." rows="3"></textarea>
    <div class="field-error" id="err-growth">Please share what interests you.</div>
  </div>
</div>

<div class="section">
  <div class="section-label">07 — Compensation Expectations</div>
  <div class="q-card" id="card-paytype">
    <span class="q-num">Q25</span>
    <div class="q-label">Preferred pay arrangement? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="paytype" value="Hourly"><span>Hourly</span></label>
      <label class="opt-label"><input type="radio" name="paytype" value="Salary"><span>Salary</span></label>
      <label class="opt-label"><input type="radio" name="paytype" value="1099 / Contract"><span>1099 / Contract</span></label>
      <label class="opt-label"><input type="radio" name="paytype" value="Open to discussion"><span>Open to discussion</span></label>
    </div>
    <div class="field-error" id="err-paytype">Please select an option.</div>
  </div>
  <div class="q-card" id="card-pay">
    <span class="q-num">Q26</span>
    <div class="q-label">Expected pay? <span class="req">*</span><br>
    <small style="color:var(--muted);font-weight:300;">(Hourly rate OR annual salary)</small></div>
    <div class="pay-wrap">
      <span class="pay-prefix">$</span>
      <input type="number" class="q-input" id="q-pay" placeholder="e.g. 22 hourly or 50000 salary" min="1">
    </div>
    <div class="field-error" id="err-pay">Please enter your expected pay.</div>
  </div>
  <div class="q-card">
    <span class="q-num">Q27</span>
    <div class="q-label">Additional compensation notes? <span style="color:var(--muted);font-size:12px;">(Optional)</span></div>
    <textarea class="q-input" id="q-paynotes" placeholder="Bonuses, benefits, flexibility..." rows="2"></textarea>
  </div>
</div>

<div class="section">
  <div class="section-label">08 — Final Questions</div>
  <div class="q-card" id="card-startdate">
    <span class="q-num">Q28</span>
    <div class="q-label">How soon could you start if offered the position? <span class="req">*</span></div>
    <div class="options-grid two-col">
      <label class="opt-label"><input type="radio" name="startdate" value="Immediately"><span>Immediately</span></label>
      <label class="opt-label"><input type="radio" name="startdate" value="2 weeks notice"><span>2 weeks notice</span></label>
      <label class="opt-label"><input type="radio" name="startdate" value="~30 days"><span>~30 days</span></label>
      <label class="opt-label"><input type="radio" name="startdate" value="60+ days"><span>60+ days</span></label>
    </div>
    <div class="field-error" id="err-startdate">Please select an option.</div>
  </div>
  <div class="q-card">
    <span class="q-num">Q29</span>
    <div class="q-label">Anything else you'd like us to know? <span style="color:var(--muted);font-size:12px;">(Optional)</span></div>
    <textarea class="q-input" id="q-anything" placeholder="Anything that sets you apart..." rows="3"></textarea>
  </div>
</div>

<div class="submit-area">
  <div class="error-msg" id="form-error">⚠ Please complete all required fields before submitting.</div>
  <button type="button" id="submit-btn" class="submit-btn">SUBMIT APPLICATION</button>
  <div class="submit-note">Your responses will be reviewed by the Alpha Myn operations team.</div>
</div>
```

  </form>

  <div id="confirmation">
    <div class="confirm-icon">✓</div>
    <h2>SUBMITTED</h2>
    <p>Thank you for completing the Alpha Myn candidate assessment. If your background is a strong fit, our team will reach out to schedule an interview.</p>
  </div>

</div>
<script>
  emailjs.init('mH0Lr5uI4aCtht96l');

var fill = document.getElementById(‘progress-fill’);
var pctLabel = document.getElementById(‘pct-label’);

function updateProgress() {
var answered = new Set();
document.querySelectorAll(‘input[type=“radio”]:checked’).forEach(function(el) { answered.add(el.name); });
if (document.querySelectorAll(‘input[name=“fluids”]:checked’).length) answered.add(‘fluids’);
[‘q-name’,‘q-phone’,‘q-email’,‘q-city’,‘q-genexp’,‘q-problem’,‘q-workhistory’,‘q-growth’,‘q-pay’].forEach(function(id) {
var el = document.getElementById(id);
if (el && el.value.trim()) answered.add(id);
});
var pct = Math.min(100, Math.round((answered.size / 26) * 100));
fill.style.width = pct + ‘%’;
pctLabel.textContent = pct + ‘%’;
}
document.getElementById(‘quiz-form’).addEventListener(‘input’, updateProgress);
document.getElementById(‘quiz-form’).addEventListener(‘change’, updateProgress);

document.querySelectorAll(‘input[name=“distance”]’).forEach(function(el) {
el.addEventListener(‘change’, function() {
document.getElementById(‘card-relocate’).style.display = (el.value === ‘Outside area - willing to relocate’) ? ‘block’ : ‘none’;
});
});
document.querySelectorAll(‘input[name=“oilfield”]’).forEach(function(el) {
el.addEventListener(‘change’, function() {
document.getElementById(‘card-oilfield-detail’).style.display = (el.value === ‘Yes’) ? ‘block’ : ‘none’;
});
});

function v(id) { var el = document.getElementById(id); return el ? el.value.trim() : ‘’; }
function r(name) { var el = document.querySelector(‘input[name=”’ + name + ‘”]:checked’); return el ? el.value : ‘’; }
function cb(name) { var els = document.querySelectorAll(‘input[name=”’ + name + ‘”]:checked’); return els.length ? Array.from(els).map(function(e){return e.value;}).join(’, ’) : ‘’; }
function setError(cardId, errId, isError) {
var card = document.getElementById(cardId);
var err = document.getElementById(errId);
if (card) card.classList.toggle(‘error’, isError);
if (err) err.classList.toggle(‘show’, isError);
return isError;
}

document.getElementById(‘submit-btn’).addEventListener(‘click’, function() {
var bad = false;
bad = setError(‘card-name’,‘err-name’,!v(‘q-name’)) || bad;
bad = setError(‘card-phone’,‘err-phone’,!v(‘q-phone’)) || bad;
bad = setError(‘card-email’,‘err-email’,!v(‘q-email’)||v(‘q-email’).indexOf(’@’)<0) || bad;
bad = setError(‘card-city’,‘err-city’,!v(‘q-city’)) || bad;
bad = setError(‘card-genexp’,‘err-genexp’,!v(‘q-genexp’)) || bad;
bad = setError(‘card-problem’,‘err-problem’,!v(‘q-problem’)) || bad;
bad = setError(‘card-workhistory’,‘err-workhistory’,!v(‘q-workhistory’)) || bad;
bad = setError(‘card-growth’,‘err-growth’,!v(‘q-growth’)) || bad;
bad = setError(‘card-pay’,‘err-pay’,!v(‘q-pay’)||parseFloat(v(‘q-pay’))<=0) || bad;
[[‘distance’,‘err-distance’,‘card-distance’],[‘transport’,‘err-transport’,‘card-transport’],
[‘emergency’,‘err-emergency’,‘card-emergency’],[‘oilchange’,‘err-oilchange’,‘card-oilchange’],
[‘filters’,‘err-filters’,‘card-filters’],[‘sparkplugs’,‘err-sparkplugs’,‘card-sparkplugs’],
[‘natgas’,‘err-natgas’,‘card-natgas’],[‘pressure’,‘err-pressure’,‘card-pressure’],
[‘oilfield’,‘err-oilfield’,‘card-oilfield’],[‘techskill’,‘err-techskill’,‘card-techskill’],
[‘network’,‘err-network’,‘card-network’],[‘datacenter’,‘err-datacenter’,‘card-datacenter’],
[‘reporting’,‘err-reporting’,‘card-reporting’],[‘education’,‘err-education’,‘card-education’],
[‘independent’,‘err-independent’,‘card-independent’],[‘paytype’,‘err-paytype’,‘card-paytype’],
[‘startdate’,‘err-startdate’,‘card-startdate’]
].forEach(function(f){ bad = setError(f[2],f[1],!r(f[0])) || bad; });
bad = setError(‘card-fluids’,‘err-fluids’,!cb(‘fluids’)) || bad;

```
if (bad) {
  document.getElementById('form-error').classList.add('show');
  var firstErr = document.querySelector('.q-card.error');
  if (firstErr) firstErr.scrollIntoView({behavior:'smooth',block:'center'});
  return;
}
document.getElementById('form-error').classList.remove('show');

var btn = document.getElementById('submit-btn');
btn.textContent = 'SENDING...';
btn.disabled = true;

var answers =
  'ALPHA MYN — CANDIDATE APPLICATION\n' +
  '====================================\n\n' +
  'CONTACT INFORMATION\n' +
  '-------------------\n' +
  'Full Name: ' + v('q-name') + '\n' +
  'Phone: ' + v('q-phone') + '\n' +
  'Email: ' + v('q-email') + '\n' +
  'City / State: ' + v('q-city') + '\n\n' +
  'LOCATION & AVAILABILITY\n' +
  '-----------------------\n' +
  'Distance from Gage OK: ' + r('distance') + '\n' +
  'Relocation Timeline: ' + (r('relocate_timeline') || 'N/A') + '\n' +
  'Reliable Transportation: ' + r('transport') + '\n' +
  'Emergency Availability: ' + r('emergency') + '\n\n' +
  'GENERATOR & MECHANICAL SKILLS\n' +
  '------------------------------\n' +
  'Oil Change Experience: ' + r('oilchange') + '\n' +
  'Filter Change Experience: ' + r('filters') + '\n' +
  'Spark Plug Experience: ' + r('sparkplugs') + '\n' +
  'Generator Experience Detail:\n' + v('q-genexp') + '\n' +
  'Fluids Comfortable With: ' + cb('fluids') + '\n\n' +
  'NATURAL GAS & FIELD OPERATIONS\n' +
  '-------------------------------\n' +
  'Natural Gas Experience: ' + r('natgas') + '\n' +
  'Pressure Monitoring: ' + r('pressure') + '\n' +
  'Oil & Gas Field Experience: ' + r('oilfield') + '\n' +
  'Oil Field Detail:\n' + (v('q-oilfield-detail') || 'N/A') + '\n\n' +
  'TECHNOLOGY & PROBLEM-SOLVING\n' +
  '-----------------------------\n' +
  'Tech Skill Level: ' + r('techskill') + '\n' +
  'Network/IT Experience: ' + r('network') + '\n' +
  'Mining Hardware Experience: ' + r('datacenter') + '\n' +
  'Problem Solving Example:\n' + v('q-problem') + '\n' +
  'Comfortable with Reporting: ' + r('reporting') + '\n\n' +
  'WORK HISTORY & BACKGROUND\n' +
  '--------------------------\n' +
  'Education: ' + r('education') + '\n' +
  'Works Independently: ' + r('independent') + '\n' +
  'Work History:\n' + v('q-workhistory') + '\n' +
  'Interest in Role:\n' + v('q-growth') + '\n\n' +
  'COMPENSATION\n' +
  '-------------\n' +
  'Pay Type: ' + r('paytype') + '\n' +
  'Expected Pay: $' + v('q-pay') + '\n' +
  'Compensation Notes: ' + (v('q-paynotes') || 'None') + '\n\n' +
  'FINAL\n' +
  '------\n' +
  'Available Start Date: ' + r('startdate') + '\n' +
  'Additional Info: ' + (v('q-anything') || 'None');

emailjs.send('service_m7l6bko', 'template_6rd9t4h', {
  name: v('q-name'),
  email: v('q-email'),
  message: answers
})
.then(function() {
  document.getElementById('quiz-form').style.display = 'none';
  var conf = document.getElementById('confirmation');
  conf.style.display = 'block';
  conf.scrollIntoView({behavior:'smooth'});
  fill.style.width = '100%';
  pctLabel.textContent = '100%';
})
.catch(function(err) {
  btn.textContent = 'SUBMIT APPLICATION';
  btn.disabled = false;
  var errBox = document.getElementById('form-error');
  var detail = '';
  if (err && err.text) detail = err.text;
  else if (err && err.status) detail = 'Status: ' + err.status;
  else detail = JSON.stringify(err);
  errBox.textContent = 'Error: ' + detail;
  errBox.classList.add('show');
});
```

});
</script>

</body>
</html>
