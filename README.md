<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Multi-Course Programming &amp; Tech LMS</title>
<style>
  :root { --primary:#004aad; --primary-dark:#003175; --accent:#fca311; --dark:#14213d; --bg:#f4f7fb; --card:#fff; --text:#1e293b; --muted:#64748b; --success:#15803d; --danger:#b91c1c; --border:#e2e8f0; }
  * { box-sizing:border-box; margin:0; padding:0; font-family:"Segoe UI",system-ui,-apple-system,sans-serif; }
  body { background:var(--bg); color:var(--text); line-height:1.55; }
  nav { background:var(--dark); color:#fff; padding:.9rem 1.75rem; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:.75rem; }
  nav .brand { font-size:1.15rem; font-weight:700; cursor:pointer; }
  nav .nav-actions { display:flex; gap:.5rem; flex-wrap:wrap; align-items:center; }
  button,select,input,textarea { font-family:inherit; font-size:.92rem; }
  button { border:none; border-radius:6px; padding:.5rem .95rem; font-weight:600; cursor:pointer; }
  button:hover { opacity:.92; } button:disabled { opacity:.55; cursor:not-allowed; }
  .btn-primary{background:var(--primary);color:#fff}.btn-accent{background:var(--accent);color:var(--dark)}
  .btn-success{background:var(--success);color:#fff}.btn-danger{background:var(--danger);color:#fff}
  .btn-ghost{background:rgba(255,255,255,.12);color:#fff}
  .container { max-width:1200px; margin:1.75rem auto; padding:0 1rem; }
  .hidden { display:none !important; }
  .card { background:var(--card); border:1px solid var(--border); border-radius:10px; padding:1.4rem; box-shadow:0 2px 8px rgba(15,23,42,.04); margin-bottom:1.25rem; }
  .grid-2 { display:grid; grid-template-columns:repeat(auto-fit,minmax(320px,1fr)); gap:1.25rem; }
  .grid-3 { display:grid; grid-template-columns:repeat(auto-fit,minmax(290px,1fr)); gap:1.25rem; }
  .form-row { margin-bottom:.85rem; } .form-row label { display:block; font-weight:600; margin-bottom:.3rem; font-size:.88rem; }
  .form-row input,.form-row select,.form-row textarea { width:100%; padding:.55rem .7rem; border:1px solid #cbd5e1; border-radius:6px; background:#fff; }
  .tag { display:inline-block; background:#e0ecff; color:var(--primary-dark); font-size:.76rem; font-weight:700; padding:.2rem .55rem; border-radius:999px; margin-bottom:.5rem; }
  .price-strip { display:flex; justify-content:space-between; background:#f8fafc; border:1px solid var(--border); border-radius:8px; padding:.65rem .8rem; margin:.75rem 0; font-size:.86rem; }
  .banner { padding:.8rem 1rem; border-radius:8px; margin-bottom:1rem; font-weight:600; font-size:.9rem; }
  .banner-info{background:#e0ecff;color:var(--primary-dark)}.banner-ok{background:#dcfce7;color:var(--success)}.banner-err{background:#fee2e2;color:var(--danger)}
  .stat-box { background:#f8fafc; border:1px solid var(--border); border-radius:8px; padding:1rem; text-align:center; }
  .stat-num { font-size:1.5rem; font-weight:800; color:var(--primary); } .stat-label { font-size:.82rem; color:var(--muted); }
  .module-item { background:#f8fafc; border:1px solid var(--border); border-radius:8px; padding:.75rem .9rem; margin-top:.5rem; }
  pre { background:#0f172a; color:#e2e8f0; padding:.65rem; border-radius:6px; font-size:.8rem; overflow-x:auto; margin-top:.4rem; }
  table { width:100%; border-collapse:collapse; margin-top:.75rem; font-size:.88rem; }
  th,td { border:1px solid var(--border); padding:.55rem .7rem; text-align:left; } th { background:#f8fafc; }
</style>
</head>
<body>
<nav>
  <div class="brand" data-nav="catalog">CodeForge Multi-Course LMS</div>
  <div class="nav-actions">
    <button class="btn-ghost" data-nav="catalog">Catalog</button>
    <button class="btn-ghost" data-nav="my-courses">My Courses</button>
    <button class="btn-ghost" data-nav="auth">Login / Register</button>
    <button class="btn-accent" id="admin-btn">Admin</button>
    <button id="logout-btn" class="btn-danger hidden">Logout</button>
  </div>
</nav>

<div class="container">
  <div id="status-banner" class="banner banner-info">Loading LMS...</div>

  <section id="section-catalog">
    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:.75rem;margin-bottom:1rem;">
        <div><h2>Course Catalog</h2><p style="color:var(--muted);font-size:.9rem;">Browse courses in any language · Pay via Telebirr, CBE Birr (ETB) or PayPal (USD)</p></div>
        <div style="display:flex;gap:.5rem;flex-wrap:wrap;">
          <input id="lang-filter" type="text" placeholder="Filter by language or title..." style="padding:.45rem .7rem;border:1px solid #cbd5e1;border-radius:6px;min-width:220px;" />
          <button class="btn-primary" id="refresh-catalog">Refresh</button>
        </div>
      </div>
      <div id="catalog-grid" class="grid-3"></div>
    </div>
  </section>

  <section id="section-auth" class="hidden">
    <div class="grid-2">
      <div class="card">
        <h3>Student Login</h3>
        <form id="login-form">
          <div class="form-row"><label>Email</label><input id="login-email" type="email" required /></div>
          <div class="form-row"><label>Password</label><input id="login-password" type="password" required /></div>
          <button type="submit" class="btn-primary">Sign In</button>
        </form>
      </div>
      <div class="card">
        <h3>Create Student Account</h3>
        <form id="register-form">
          <div class="form-row"><label>Full Name</label><input id="reg-name" type="text" required /></div>
          <div class="form-row"><label>Email</label><input id="reg-email" type="email" required /></div>
          <div class="form-row"><label>Password (min 8 chars)</label><input id="reg-password" type="password" minlength="8" required /></div>
          <button type="submit" class="btn-success">Register</button>
        </form>
      </div>
    </div>
  </section>

  <section id="section-my-courses" class="hidden">
    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:.5rem;margin-bottom:1rem;">
        <h2>My Enrolled Courses &amp; Certificates</h2>
        <button class="btn-primary" id="reload-my">Reload</button>
      </div>
      <div id="my-courses-list"></div>
    </div>
  </section>

  <section id="section-admin" class="hidden">
    <div class="card">
      <h2>Admin Control Panel</h2>
      <div style="display:flex;gap:.6rem;align-items:center;flex-wrap:wrap;margin:.75rem 0 1.25rem;">
        <input id="admin-code-input" type="password" placeholder="Enter admin code" style="padding:.5rem .7rem;border:1px solid #cbd5e1;border-radius:6px;width:220px;" />
        <button class="btn-primary" id="load-analytics">Load Analytics</button>
      </div>
      <div class="grid-3" style="margin-bottom:1.25rem;">
        <div class="stat-box"><div class="stat-num" id="stat-students">0</div><div class="stat-label">Total Students</div></div>
        <div class="stat-box"><div class="stat-num" id="stat-courses">0</div><div class="stat-label">Total Courses</div></div>
        <div class="stat-box"><div class="stat-num" id="stat-enrollments">0</div><div class="stat-label">Paid Enrollments</div></div>
        <div class="stat-box"><div class="stat-num" id="stat-etb">0.00 ETB</div><div class="stat-label">Revenue (ETB)</div></div>
        <div class="stat-box"><div class="stat-num" id="stat-usd">$0.00</div><div class="stat-label">Revenue (USD)</div></div>
      </div>
      <div class="card"><h3>Per-Course Breakdown</h3><div id="admin-course-stats-table"><p style="color:var(--muted);font-size:.88rem;">Load analytics to inspect per-course counts.</p></div></div>
      <div class="grid-2">
        <div class="card" style="margin:0;">
          <h3>Create New Course</h3>
          <form id="create-course-form">
            <div class="form-row"><label>Course Title</label><input id="c-title" type="text" required /></div>
            <div class="form-row"><label>Programming Language(s)</label><input id="c-lang" type="text" value="Any / Python, JS, Rust, Go, C++" required /></div>
            <div class="form-row"><label>Description</label><textarea id="c-desc" rows="2" required></textarea></div>
            <div class="grid-2" style="gap:.6rem;">
              <div class="form-row"><label>Price (ETB)</label><input id="c-price-etb" type="number" step="0.01" min="0" value="500" required /></div>
              <div class="form-row"><label>Price (USD)</label><input id="c-price-usd" type="number" step="0.01" min="0" value="10" required /></div>
              <div class="form-row"><label>Cert Fee (ETB)</label><input id="c-cert-etb" type="number" step="0.01" min="0" value="150" required /></div>
              <div class="form-row"><label>Cert Fee (USD)</label><input id="c-cert-usd" type="number" step="0.01" min="0" value="3" required /></div>
            </div>
            <button type="submit" class="btn-success">Publish Course</button>
          </form>
        </div>
        <div>
          <div class="card">
            <h3>Add Lesson / Module</h3>
            <form id="add-module-form">
              <div class="form-row"><label>Target Course</label><select id="m-course-select" required></select></div>
              <div class="form-row"><label>Module Title</label><input id="m-title" type="text" required /></div>
              <div class="form-row"><label>Content URL</label><input id="m-url" type="url" required /></div>
              <div class="grid-2" style="gap:.6rem;">
                <div class="form-row"><label>Language</label><input id="m-lang" type="text" placeholder="Any" /></div>
                <div class="form-row"><label>Content Type</label>
                  <select id="m-type">
                    <option value="CODE_REPO">CODE_REPO</option>
                    <option value="VIDEO">VIDEO</option>
                    <option value="SANDBOX">SANDBOX</option>
                    <option value="ARTICLE">ARTICLE</option>
                  </select>
                </div>
              </div>
              <div class="form-row"><label>Starter Code (optional)</label><textarea id="m-code" rows="2"></textarea></div>
              <button type="submit" class="btn-primary">Add Module</button>
            </form>
          </div>
          <div class="card" style="margin:0;">
            <h3>Update / Delete Course</h3>
            <form id="update-course-form">
              <div class="form-row"><label>Course</label><select id="u-course-select" required></select></div>
              <div class="grid-2" style="gap:.6rem;">
                <div class="form-row"><label>Price (ETB)</label><input id="u-price-etb" type="number" step="0.01" min="0" required /></div>
                <div class="form-row"><label>Price (USD)</label><input id="u-price-usd" type="number" step="0.01" min="0" required /></div>
                <div class="form-row"><label>Cert Fee (ETB)</label><input id="u-cert-etb" type="number" step="0.01" min="0" required /></div>
                <div class="form-row"><label>Cert Fee (USD)</label><input id="u-cert-usd" type="number" step="0.01" min="0" required /></div>
              </div>
              <div style="display:flex;gap:.5rem;flex-wrap:wrap;">
                <button type="submit" class="btn-accent">Update Pricing</button>
                <button type="button" class="btn-danger" id="delete-course-btn">Delete Course</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</div>

<script>
  const API = location.origin + '/api';
  const state = {
    courses: [],
    enrolledIds: new Set(),
    token: localStorage.getItem('lms_token') || '',
    user: JSON.parse(localStorage.getItem('lms_user') || 'null'),
  };

  // ---- helpers ----
  const $ = id => document.getElementById(id);
  const esc = s => String(s ?? '').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');
  const safeId = s => String(s ?? '').replace(/[^a-zA-Z0-9_-]/g, '');
  const safeUrl = u => /^https?:\/\//i.test(String(u ?? '').trim()) ? esc(u) : '#';
  const setBanner = (msg, type = 'info') => {
    const el = $('status-banner');
    el.className = 'banner banner-' + type;
    el.textContent = msg + ' | ' + (state.user ? state.user.name + ' (' + state.user.email + ')' : 'Guest');
  };
  const authHeaders = (extra = {}) => state.token ? { ...extra, Authorization: 'Bearer ' + state.token } : extra;
  const adminHeaders = (extra = {}) => ({ ...extra, 'x-admin-code': $('admin-code-input').value.trim() });

  function updateSessionUI() {
    $('logout-btn').classList.toggle('hidden', !(state.user && state.token));
    setBanner(state.user ? 'Signed in' : 'Browse courses or sign in');
  }

  function show(section) {
    ['catalog','auth','my-courses','admin'].forEach(s => $('section-' + s).classList.toggle('hidden', s !== section));
    if (section === 'catalog') fetchCatalog();
    if (section === 'my-courses') fetchMyCourses();
    if (section === 'admin') populateAdminSelects();
  }

  // ---- API ----
  async function api(path, opts = {}) {
    const r = await fetch(API + path, opts);
    const ct = r.headers.get('content-type') || '';
    if (!r.ok) {
      const body = ct.includes('json') ? await r.json().catch(() => ({})) : {};
      throw new Error(body.error || `Request failed (${r.status})`);
    }
    return ct.includes('json') ? r.json() : r;
  }

  async function fetchCatalog() {
    try {
      const { courses } = await api('/courses');
      state.courses = courses || [];
      populateAdminSelects();
      renderCatalog();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  function renderCatalog() {
    const q = ($('lang-filter').value || '').trim().toLowerCase();
    const list = state.courses.filter(c =>
      !q || (c.programmingLanguage || '').toLowerCase().includes(q) || (c.title || '').toLowerCase().includes(q)
    );
    const grid = $('catalog-grid');
    if (!list.length) { grid.innerHTML = '<p style="color:var(--muted)">No courses found. Admins can add courses in the Admin panel.</p>'; return; }
    grid.innerHTML = list.map((c, i) => {
      const done = state.enrolledIds.has(c.id);
      return `
        <div class="card" style="margin:0;display:flex;flex-direction:column;justify-content:space-between">
          <div>
            <span class="tag">${esc(c.programmingLanguage || 'Any Language')}</span>
            <h3>${esc(c.title)}</h3>
            <p style="color:var(--muted);font-size:.88rem;margin:.4rem 0">${esc(c.description)}</p>
            <p style="font-size:.82rem;color:var(--muted)">Lessons: ${(c.modules || []).length}</p>
            <div class="price-strip">
              <div><strong>ETB:</strong> ${esc(c.priceETB)}<br/><span style="color:var(--muted);font-size:.78rem">Cert: ${esc(c.certFeeETB)} ETB</span></div>
              <div style="text-align:right"><strong>USD:</strong> $${esc(c.priceUSD)}<br/><span style="color:var(--muted);font-size:.78rem">Cert: $${esc(c.certFeeUSD)}</span></div>
            </div>
          </div>
          <div>
            <div class="form-row" style="margin-bottom:.5rem">
              <select id="pay-opt-${i}" ${done ? 'disabled' : ''}>
                <option value="ETB|TELEBIRR">Telebirr (ETB)</option>
                <option value="ETB|CBE_BIRR">CBE Birr (ETB)</option>
                <option value="USD|PAYPAL">PayPal (USD)</option>
              </select>
            </div>
            <button class="${done ? 'btn-success' : 'btn-primary'}" style="width:100%" ${done ? 'disabled' : ''}
              data-action="enroll" data-course-id="${safeId(c.id)}" data-pay-index="${i}">
              ${done ? 'Enrolled' : 'Enroll Now'}
            </button>
          </div>
        </div>`;
    }).join('');
  }

  async function fetchMyCourses() {
    if (!state.token) { $('my-courses-list').innerHTML = '<p style="color:var(--muted)">Please sign in to view enrolled courses.</p>'; return; }
    try {
      const { enrollments } = await api('/my-courses', { headers: authHeaders() });
      state.enrolledIds = new Set(enrollments.map(e => e.courseId));
      renderCatalog();
      const el = $('my-courses-list');
      if (!enrollments.length) { el.innerHTML = '<p style="color:var(--muted)">No enrollments yet.</p>'; return; }
      el.innerHTML = enrollments.map((enr, idx) => {
        const c = enr.course;
        const issued = enr.certificateStatus === 'ISSUED';
        const mods = (c.modules || []).map(m => `
          <div class="module-item">
            <strong>${esc(m.title)}</strong>
            <span class="tag">${esc(m.language || c.programmingLanguage || 'Any')} • ${esc(m.contentType)}</span><br/>
            <a href="${safeUrl(m.contentUrl)}" target="_blank" rel="noopener noreferrer">${esc(m.contentUrl)}</a>
            ${m.starterCode ? `<pre>${esc(m.starterCode)}</pre>` : ''}
          </div>`).join('');
        const certBtns = issued
          ? `<button class="btn-success" data-action="download-cert" data-course-id="${safeId(c.id)}">Download PDF Certificate</button>`
          : `<select id="cert-opt-${idx}" style="padding:.4rem .6rem;border:1px solid #cbd5e1;border-radius:6px">
              <option value="ETB|TELEBIRR">Telebirr (ETB)</option>
              <option value="ETB|CBE_BIRR">CBE Birr (ETB)</option>
              <option value="USD|PAYPAL">PayPal (USD)</option>
             </select>
             <button class="btn-success" data-action="pay-cert" data-course-id="${safeId(c.id)}" data-cert-index="${idx}">Pay &amp; Download PDF</button>`;
        return `
          <div class="card">
            <div style="display:flex;justify-content:space-between;align-items:flex-start;flex-wrap:wrap;gap:.5rem">
              <div>
                <span class="tag">${esc(c.programmingLanguage || 'Any Language')}</span>
                <h3>${esc(c.title)}</h3>
                <p style="font-size:.88rem;color:var(--muted)">Certificate: <strong>${esc(enr.certificateStatus)}</strong></p>
              </div>
              <div style="display:flex;gap:.45rem;flex-wrap:wrap">${certBtns}</div>
            </div>
            ${mods}
          </div>`;
      }).join('');
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function saveBlob(res, fallbackName) {
    const blob = await res.blob();
    const disp = res.headers.get('Content-Disposition') || '';
    const m = disp.match(/filename="?([^";]+)"?/i);
    const name = m ? m[1] : fallbackName;
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url; a.download = name;
    document.body.appendChild(a); a.click(); a.remove();
    setTimeout(() => URL.revokeObjectURL(url), 1000);
  }

  // ---- Event handlers ----
  async function handleLogin(e) {
    e.preventDefault();
    try {
      const d = await api('/auth/login', {
        method: 'POST', headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ email: $('login-email').value.trim(), password: $('login-password').value }),
      });
      state.token = d.token; state.user = d.user;
      localStorage.setItem('lms_token', d.token);
      localStorage.setItem('lms_user', JSON.stringify(d.user));
      updateSessionUI(); await fetchMyCourses(); show('my-courses');
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleRegister(e) {
    e.preventDefault();
    try {
      const d = await api('/auth/register', {
        method: 'POST', headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          name: $('reg-name').value.trim(),
          email: $('reg-email').value.trim(),
          password: $('reg-password').value,
        }),
      });
      state.token = d.token; state.user = d.user;
      localStorage.setItem('lms_token', d.token);
      localStorage.setItem('lms_user', JSON.stringify(d.user));
      updateSessionUI(); show('catalog');
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleEnroll(courseId, payIndex) {
    if (!state.token) { setBanner('Please sign in first.', 'err'); show('auth'); return; }
    const [currency, paymentMethod] = ($('pay-opt-' + payIndex).value || '').split('|');
    try {
      const d = await api('/enroll', {
        method: 'POST', headers: authHeaders({ 'Content-Type': 'application/json' }),
        body: JSON.stringify({ courseId, currency, paymentMethod }),
      });
      state.enrolledIds.add(courseId); renderCatalog();
      setBanner('Enrolled! Ref: ' + d.transaction.providerRef, 'ok');
      show('my-courses');
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handlePayCert(courseId, certIndex) {
    const [currency, paymentMethod] = ($('cert-opt-' + certIndex).value || '').split('|');
    try {
      const r = await fetch(`${API}/certificate/${encodeURIComponent(courseId)}`, {
        method: 'POST', headers: authHeaders({ 'Content-Type': 'application/json' }),
        body: JSON.stringify({ currency, paymentMethod }),
      });
      if (!r.ok) {
        const d = await r.json().catch(() => ({}));
        throw new Error(d.error || 'Certificate payment failed');
      }
      await saveBlob(r, 'Certificate.pdf');
      setBanner('Certificate issued and downloaded!', 'ok');
      fetchMyCourses();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleDownloadCert(courseId) {
    try {
      const r = await fetch(`${API}/certificate/${encodeURIComponent(courseId)}/download`, { headers: authHeaders() });
      if (!r.ok) {
        const d = await r.json().catch(() => ({}));
        throw new Error(d.error || 'Download failed');
      }
      await saveBlob(r, 'Certificate.pdf');
      setBanner('Certificate downloaded!', 'ok');
    } catch (e) { setBanner(e.message, 'err'); }
  }

  function populateAdminSelects() {
    const html = state.courses.map(c => `<option value="${esc(c.id)}">${esc(c.title)} (${esc(c.programmingLanguage || 'Any')})</option>`).join('');
    const m = $('m-course-select'), u = $('u-course-select');
    if (m) m.innerHTML = html || '<option value="">No courses</option>';
    if (u) { u.innerHTML = html || '<option value="">No courses</option>'; prefillUpdateCourse(); }
  }

  function prefillUpdateCourse() {
    const sel = $('u-course-select');
    const c = state.courses.find(x => x.id === sel.value);
    if (!c) return;
    $('u-price-etb').value = c.priceETB;
    $('u-price-usd').value = c.priceUSD;
    $('u-cert-etb').value = c.certFeeETB;
    $('u-cert-usd').value = c.certFeeUSD;
  }

  async function fetchAdminAnalytics() {
    try {
      const d = await api('/admin/analytics', { headers: adminHeaders() });
      $('stat-students').textContent = d.totalStudents ?? 0;
      $('stat-courses').textContent = d.totalCourses ?? 0;
      $('stat-enrollments').textContent = d.totalEnrollments ?? 0;
      $('stat-etb').textContent = Number(d.revenue?.ETB || 0).toFixed(2) + ' ETB';
      $('stat-usd').textContent = '$' + Number(d.revenue?.USD || 0).toFixed(2);
      const stats = d.courseStats || [];
      $('admin-course-stats-table').innerHTML = !stats.length
        ? '<p style="color:var(--muted);font-size:.88rem">No courses yet.</p>'
        : `<table><thead><tr><th>Course</th><th>Language</th><th>Enrollments</th><th>Modules</th></tr></thead><tbody>${
            stats.map(s => `<tr><td>${esc(s.title)}</td><td>${esc(s.programmingLanguage || 'Any')}</td><td>${s._count?.enrollments ?? 0}</td><td>${s._count?.modules ?? 0}</td></tr>`).join('')
          }</tbody></table>`;
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleCreateCourse(e) {
    e.preventDefault();
    try {
      const d = await api('/admin/courses', {
        method: 'POST', headers: adminHeaders({ 'Content-Type': 'application/json' }),
        body: JSON.stringify({
          title: $('c-title').value.trim(),
          programmingLanguage: $('c-lang').value.trim(),
          description: $('c-desc').value.trim(),
          priceETB: Number($('c-price-etb').value),
          priceUSD: Number($('c-price-usd').value),
          certFeeETB: Number($('c-cert-etb').value),
          certFeeUSD: Number($('c-cert-usd').value),
        }),
      });
      e.target.reset();
      $('c-lang').value = 'Any / Python, JS, Rust, Go, C++';
      setBanner('Created: ' + d.course.title, 'ok');
      await fetchCatalog(); await fetchAdminAnalytics();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleAddModule(e) {
    e.preventDefault();
    const courseId = $('m-course-select').value;
    if (!courseId) return;
    try {
      const d = await api(`/admin/courses/${encodeURIComponent(courseId)}/modules`, {
        method: 'POST', headers: adminHeaders({ 'Content-Type': 'application/json' }),
        body: JSON.stringify({
          title: $('m-title').value.trim(),
          contentUrl: $('m-url').value.trim(),
          language: $('m-lang').value.trim() || undefined,
          contentType: $('m-type').value,
          starterCode: $('m-code').value || undefined,
        }),
      });
      e.target.reset();
      setBanner('Added module: ' + d.module.title, 'ok');
      await fetchCatalog(); await fetchAdminAnalytics();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleUpdateCourse(e) {
    e.preventDefault();
    const courseId = $('u-course-select').value;
    if (!courseId) return;
    try {
      const d = await api(`/admin/courses/${encodeURIComponent(courseId)}`, {
        method: 'PUT', headers: adminHeaders({ 'Content-Type': 'application/json' }),
        body: JSON.stringify({
          priceETB: Number($('u-price-etb').value),
          priceUSD: Number($('u-price-usd').value),
          certFeeETB: Number($('u-cert-etb').value),
          certFeeUSD: Number($('u-cert-usd').value),
        }),
      });
      setBanner('Updated: ' + d.course.title, 'ok');
      await fetchCatalog();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  async function handleDeleteCourse() {
    const courseId = $('u-course-select').value;
    if (!courseId || !confirm('Delete this course and all its modules/enrollments?')) return;
    try {
      await api(`/admin/courses/${encodeURIComponent(courseId)}`, { method: 'DELETE', headers: adminHeaders() });
      setBanner('Course deleted.', 'ok');
      await fetchCatalog(); await fetchAdminAnalytics();
    } catch (e) { setBanner(e.message, 'err'); }
  }

  // ---- Wire up ----
  document.querySelectorAll('[data-nav]').forEach(el => el.addEventListener('click', () => show(el.dataset.nav)));
  $('admin-btn').addEventListener('click', () => {
    const code = prompt('Enter Admin Code:');
    if (!code) return;
    $('admin-code-input').value = code;
    show('admin');
    fetchAdminAnalytics();
  });
  $('logout-btn').addEventListener('click', () => {
    state.token = ''; state.user = null; state.enrolledIds.clear();
    localStorage.removeItem('lms_token'); localStorage.removeItem('lms_user');
    updateSessionUI(); renderCatalog(); show('catalog');
  });
  $('refresh-catalog').addEventListener('click', fetchCatalog);
  $('lang-filter').addEventListener('input', renderCatalog);
  $('reload-my').addEventListener('click', fetchMyCourses);
  $('load-analytics').addEventListener('click', fetchAdminAnalytics);
  $('login-form').addEventListener('submit', handleLogin);
  $('register-form').addEventListener('submit', handleRegister);
  $('create-course-form').addEventListener('submit', handleCreateCourse);
  $('add-module-form').addEventListener('submit', handleAddModule);
  $('update-course-form').addEventListener('submit', handleUpdateCourse);
  $('delete-course-btn').addEventListener('click', handleDeleteCourse);
  $('u-course-select').addEventListener('change', prefillUpdateCourse);

  // Delegated clicks (XSS-safe: IDs are sanitized to [a-zA-Z0-9_-])
  document.addEventListener('click', (e) => {
    const btn = e.target.closest('[data-action]');
    if (!btn) return;
    const id = btn.dataset.courseId;
    if (!id || !/^[a-zA-Z0-9_-]+$/.test(id)) return;
    if (btn.dataset.action === 'enroll') handleEnroll(id, btn.dataset.payIndex);
    if (btn.dataset.action === 'pay-cert') handlePayCert(id, btn.dataset.certIndex);
    if (btn.dataset.action === 'download-cert') handleDownloadCert(id);
  });

  // ---- Boot ----
  updateSessionUI();
  fetchCatalog();
  if (state.token) fetchMyCourses();
</script>
</body>
</html>
