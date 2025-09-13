---
title: Schedule
nav: Schedule
---
# Workshop Schedule

<script>
(function () {
  const timeEls = Array.from(document.querySelectorAll('time.event-time'));
  if (!timeEls.length) return;

  const tzSelect = document.getElementById('tz-select');
  const tzResetBtn = document.getElementById('tz-reset');
  const userTZ = Intl.DateTimeFormat().resolvedOptions().timeZone;

  // Populate timezone list (modern browsers)
  function getAllTimeZones() {
    if (Intl.supportedValuesOf && Intl.supportedValuesOf('timeZone')) {
      return Intl.supportedValuesOf('timeZone');
    }
    // Fallback (tiny curated list)
    return [
      'UTC','America/New_York','America/Chicago','America/Denver','America/Los_Angeles',
      'Europe/London','Europe/Paris','Europe/Berlin','Europe/Madrid',
      'Asia/Dubai','Asia/Kolkata','Asia/Singapore','Asia/Tokyo','Australia/Sydney'
    ];
  }

  function formatOptions(style) {
    // Two presets: "long" (weekday/date) and "short"
    if (style === 'short') {
      return { hour: 'numeric', minute: '2-digit', timeZoneName: 'short' };
    }
    return {
      weekday: 'short', year: 'numeric', month: 'short', day: 'numeric',
      hour: 'numeric', minute: '2-digit', timeZoneName: 'short'
    };
  }

  function renderTimes(tz) {
    for (const el of timeEls) {
      const iso = el.getAttribute('data-iso');
      const style = el.getAttribute('data-format') || 'long';
      if (!iso) continue;

      // Parse ISO with offset/UTC: safe with built-in Date
      const d = new Date(iso);
      if (isNaN(d)) continue;

      const fmt = new Intl.DateTimeFormat(undefined, { ...formatOptions(style), timeZone: tz });
      const text = fmt.format(d);

      // Update text content and machine-readable datetime attribute
      el.textContent = text;
      try {
        // For machine readability, store the localized version in title as a hint
        el.setAttribute('title', text + ' (' + tz + ')');
        el.setAttribute('data-shown-tz', tz);
        // Keep datetime attribute in UTC for semantics
        el.setAttribute('datetime', d.toISOString());
      } catch(e) {}
    }
  }

  // Populate the selector
  const tzs = getAllTimeZones();
  const frag = document.createDocumentFragment();
  tzs.forEach(z => {
    const opt = document.createElement('option');
    opt.value = z; opt.textContent = z;
    frag.appendChild(opt);
  });
  tzSelect.appendChild(frag);

  // Load preference from localStorage or use user tz
  const saved = localStorage.getItem('preferredTZ') || userTZ || 'UTC';
  if (tzs.includes(saved)) tzSelect.value = saved;

  // Initial render
  renderTimes(tzSelect.value);

  // Handlers
  tzSelect.addEventListener('change', () => {
    const tz = tzSelect.value;
    localStorage.setItem('preferredTZ', tz);
    renderTimes(tz);
  });

  tzResetBtn.addEventListener('click', () => {
    tzSelect.value = userTZ || 'UTC';
    localStorage.setItem('preferredTZ', tzSelect.value);
    renderTimes(tzSelect.value);
  });
})();
</script>

Zoom Link: https://tinyurl.com/4p3kc89a

**Central U.S. Time, September 15, 2025**

<table class="table table-striped table-bordered">
  <thead>
    <tr>
      <th style="width: 30%;">Time</th>
      <th>Session</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><time data-iso="2025-09-15T09:09:00-06:00" date-format="long">9:00 am - 9:20 am</time></td>
      <td>Opening Remarks and Technical Setup</td>
    </tr>
    <tr>
      <td>9:20 am - 9:40 am</td>
      <td><strong>Paper:</strong> <em>Coming Back Differently: A Case Study of Near Death Experiences of Webpages</em> by <a href="https://lesleyodu.github.io/">Lesley Frew</a>, <a href="https://www.cs.odu.edu/~mln/">Michael Nelson</a>, and <a href="https://weiglemc.github.io/">Michele Weigle</a></td>
    </tr>
    <tr>
      <td>9:40 am - 10:00 am</td>
      <td><strong>Paper:</strong> <em>Toward Robust URL Extraction for Open Science: A Study of arXiv File Formats and Temporal Trends</em> by <a href="https://rochanaro.github.io/">Rochana R. Obadage</a>, <a href="https://liyalamia.github.io/Portfolio/">Lamia Salsabil</a>, <a href="https://x.com/ibnesayeed">Sawood Alam</a>, <a href="https://waingram.github.io/">William A. Ingram</a>, <a href="https://bipasha-banerjee.github.io/">Bipasha Banarjee</a>, <a href="https://fox.cs.vt.edu/">Edward A. Fox</a>, and <a href="https://fanchyna.wixsite.com/jianwu">Jian Wu</a></td>
    </tr>
    <tr>
      <td>10:00 am - 10:20 am</td>
      <td><strong>Paper:</strong> <em>Medieval Citation Networks as Digital Hyperlinks: Transformer-Based Authorship Attribution in Historical Text Collections</em> by <a href="https://u.cs.biu.ac.il/~schlerj">Jonathan Schler</a>, <a href="https://www.linkedin.com/in/natibg/">Nati Ben-Gigi</a>, Binyamin Katzoff, and <a href="https://is.biu.ac.il/maayanz">Maayan Geffet-Tamir</a></td>
    </tr>
    <tr>
      <td>10:20 am - 10:30 am</td>
      <td>Transition Buffer</td>
    </tr>
    <tr>
      <td>10:30 am - 11:00 am</td>
      <td>Coffee Break <em>(Hosted by ACM Hypertext)</em></td>
    </tr>
    <tr>
      <td>11:00 am - 11:05 am</td>
      <td>Session Restart &amp; Quick Welcome Back</td>
    </tr>
    <tr>
      <td>11:05 am - 11:25 am</td>
      <td><strong>Paper:</strong> <em>Lost, but Preserved - A Web Archiving Perspective on the Ephemeral Web</em> by <a href="https://x.com/ibnesayeed">Sawood Alam</a> and <a href="https://x.com/markgraham">Mark Graham</a></td>
    </tr>
    <tr>
      <td>11:25 am - 11:45 am</td>
      <td><strong>Invited Talk:</strong> <em>Detecting and Diagnosing Errors in Replaying Archived Web Pages</em> by <a href="https://jingyzhu.github.io/">Jingyuan Zhu</a> and <a href="https://www.harsha.usc.edu/">Harsha V. Madhyastha</a></td>
    </tr>
    <tr>
      <td>11:45 am - 11:55 am (flexible)</td>
      <td>Open Lightning Talks <em>(Drop-in, short-format contributions)</em></td>
    </tr>
    <tr>
      <td>11:55 am - 12:10 pm (flexible)</td>
      <td>Community Discussion: <em>The Future of WADL</em></td>
    </tr>
    <tr>
      <td>12:10 pm - 12:30 pm (flexible)</td>
      <td>Workshop Wrap-Up &amp; Closing Reflections</td>
    </tr>
    <tr>
      <td>12:30 pm onward</td>
      <td>Lunch <em>(Hosted by ACM Hypertext)</em></td>
    </tr>
  </tbody>
</table>
