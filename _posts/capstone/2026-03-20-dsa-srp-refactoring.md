---
toc: false
layout: post
title: SRP Refactoring - DSA Portal Codebase
description: Applying the Single Responsibility Principle across three key files in the DSA portal — frontend JavaScript, backend API, and AI chatbot — with side-by-side code comparisons.
permalink: /capstone/dsa-srp-refactoring/
sticky_rank: 8
---

<style>
  .srp-wrap {
    max-width: 920px;
    margin: 0 auto;
    font-family: 'Segoe UI', system-ui, sans-serif;
  }

  .srp-card {
    background: #ffffff;
    border: 1px solid #e2e8f0;
    border-radius: 16px;
    padding: 1.5rem 1.6rem;
    margin-bottom: 1.25rem;
    box-shadow: 0 4px 20px rgba(0,0,0,0.06);
  }

  .srp-card h2 {
    color: #0f2847 !important;
    font-size: 1.35rem;
    font-weight: 800;
    border-bottom: 2px solid #f59e0b;
    padding-bottom: 8px;
    margin: 0 0 1rem;
  }

  .srp-card h3 {
    color: #1e3a5f !important;
    font-size: 1.05rem;
    font-weight: 700;
    margin: 1.2rem 0 0.5rem;
  }

  .srp-card p {
    color: #1e293b !important;
    line-height: 1.7;
    font-size: 0.92rem;
    margin-bottom: 0.75rem;
  }

  .srp-card strong {
    color: #000000 !important;
  }

  .srp-card ul, .srp-card ol {
    padding-left: 1.2rem;
    margin: 0.5rem 0;
  }

  .srp-card li {
    color: #1e293b !important;
    font-size: 0.9rem;
    line-height: 1.7;
    margin-bottom: 0.4rem;
  }

  .srp-card code {
    background: #f1f5f9;
    padding: 1px 6px;
    border-radius: 4px;
    font-size: 0.82rem;
    color: #334155 !important;
  }

  .srp-file-path {
    background: #f1f5f9;
    border-left: 3px solid #f59e0b;
    padding: 8px 14px;
    font-family: monospace;
    font-size: 0.85rem;
    color: #334155 !important;
    margin: 0.75rem 0;
    border-radius: 0 8px 8px 0;
  }

  .srp-compare {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin: 1rem 0;
  }

  .srp-compare pre {
    margin: 0;
    font-size: 0.78rem;
    border-radius: 10px;
    padding: 14px;
    overflow-x: auto;
    line-height: 1.5;
  }

  .srp-old {
    background: #fef2f2;
    border: 1px solid #fecaca;
  }

  .srp-old code {
    color: #991b1b !important;
    background: transparent !important;
    padding: 0 !important;
  }

  .srp-new {
    background: #f0fdf4;
    border: 1px solid #bbf7d0;
  }

  .srp-new code {
    color: #166534 !important;
    background: transparent !important;
    padding: 0 !important;
  }

  .srp-label {
    font-size: 0.72rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 4px;
  }

  .srp-label-old { color: #dc2626 !important; }
  .srp-label-new { color: #16a34a !important; }

  .srp-hero {
    background: linear-gradient(135deg, #0f2847, #1e3a5f);
    border-radius: 16px;
    padding: 2rem 1.8rem;
    margin-bottom: 1.25rem;
    box-shadow: 0 8px 30px rgba(0,0,0,0.15);
  }

  .srp-hero h2 {
    color: #fbbf24 !important;
    font-size: 1.5rem;
    font-weight: 800;
    margin: 0 0 0.5rem;
    border: none;
    padding: 0;
  }

  .srp-hero p {
    color: #cbd5e1 !important;
    font-size: 0.95rem;
    line-height: 1.7;
    margin-bottom: 0;
  }

  .srp-takeaway {
    background: linear-gradient(135deg, #0f2847, #1e3a5f);
    border-radius: 16px;
    padding: 1.5rem 1.6rem;
    margin-bottom: 1.25rem;
    box-shadow: 0 8px 30px rgba(0,0,0,0.15);
  }

  .srp-takeaway h3 {
    color: #fbbf24 !important;
    font-size: 1.1rem;
    margin: 0 0 0.75rem;
  }

  .srp-takeaway li {
    color: #cbd5e1 !important;
    font-size: 0.9rem;
    line-height: 1.7;
    margin-bottom: 0.5rem;
  }

  .srp-takeaway strong {
    color: #ffffff !important;
  }

  .srp-takeaway code {
    color: #fbbf24 !important;
    background: rgba(255,255,255,0.1) !important;
    padding: 1px 5px;
    border-radius: 4px;
    font-size: 0.82rem;
  }

  .srp-table {
    width: 100%;
    border-collapse: collapse;
    margin: 0.75rem 0;
    font-size: 0.85rem;
  }

  .srp-table th {
    background: #0f2847;
    color: #fbbf24 !important;
    padding: 10px 14px;
    text-align: left;
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .srp-table td {
    padding: 9px 14px;
    border-bottom: 1px solid #e2e8f0;
    color: #000000 !important;
    background: #ffffff;
  }

  .srp-table td code {
    color: #334155 !important;
  }

  .srp-table tr:nth-child(even) td {
    background: #f8fafc;
  }

  @media (max-width: 700px) {
    .srp-compare { grid-template-columns: 1fr; }
    .srp-card { padding: 1.1rem; }
  }
</style>

<div class="srp-wrap">

<div class="srp-hero">
  <h2>Single Responsibility Principle (SRP) Refactoring</h2>
  <p>Every function, class, or module should have <strong style="color:#fbbf24 !important">one reason to change</strong>. We applied SRP across three key files in the DSA portal without changing any functionality or UI.</p>
</div>

<div class="srp-card">
  <h2>Overview: What Changed</h2>
  <table class="srp-table">
    <thead>
      <tr><th>File</th><th>Type</th><th>Changes</th></tr>
    </thead>
    <tbody>
      <tr><td><code>navigation/sheriff/index.md</code></td><td>Frontend JS</td><td>14 monolithic functions &rarr; 30+ focused functions</td></tr>
      <tr><td><code>api/sheriff.py</code></td><td>Backend API</td><td>4x duplicated auth logic &rarr; 4 shared helpers</td></tr>
      <tr><td><code>api/sheriff_chat.py</code></td><td>AI Chatbot</td><td>1 monolithic handler &rarr; 5 single-purpose functions</td></tr>
    </tbody>
  </table>
</div>

<!-- FILE 1 -->
<div class="srp-card">
  <h2>File 1: Frontend JavaScript (DSA Portal UI)</h2>
  <div class="srp-file-path">cap_front/navigation/sheriff/index.md &mdash; &lt;script&gt; section</div>

  <h3>Problem: <code>updateUI()</code> did everything</h3>
  <p>The old function handled both logged-in and logged-out states in a single dense block with no separation.</p>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE</div>
      <pre class="srp-old"><code>function updateUI() {
  document.getElementById('authBtns').style.display = user?'none':'flex';
  const ua = document.getElementById('userArea');
  if(user){ua.classList.add('active');
    document.getElementById('uName').textContent=user.name.split(' ')[0];
    document.getElementById('upName').textContent=user.name;
    document.getElementById('upBadge').textContent='Badge: '+user.sheriff_id;
    document.getElementById('upRank').textContent='Rank: '+user.rank;
    document.getElementById('upStation').textContent='Station: '+user.station;
    document.getElementById('adminBtn').style.display=
      user.role==='Admin'?'block':'none';}
  else{ua.classList.remove('active');
    document.getElementById('adminSection').classList.remove('open');}
}</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER</div>
      <pre class="srp-new"><code>function showLoggedInUI() {
  el('authBtns').style.display = 'none';
  el('userArea').classList.add('active');
  el('uName').textContent = user.name.split(' ')[0];
  el('upName').textContent = user.name;
  el('upBadge').textContent = 'Badge: ' + user.sheriff_id;
  el('upRank').textContent = 'Rank: ' + user.rank;
  el('upStation').textContent = 'Station: ' + user.station;
  el('adminBtn').style.display =
    user.role === 'Admin' ? 'block' : 'none';
}

function showLoggedOutUI() {
  el('authBtns').style.display = 'flex';
  el('userArea').classList.remove('active');
  el('adminSection').classList.remove('open');
}

function updateUI() {
  user ? showLoggedInUI() : showLoggedOutUI();
}</code></pre>
    </div>
  </div>

  <p><strong>Why this is better:</strong> Each UI state is its own function. <code>updateUI()</code> becomes a one-line router.</p>
</div>

<div class="srp-card">
  <h3>Problem: <code>sendChat()</code> handled input, API, DOM, and state</h3>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE</div>
      <pre class="srp-old"><code>function sendChat(){
  const inp=document.getElementById('cbIn'),
    msg=inp.value.trim();
  if(!msg)return;inp.value='';
  addMsg(msg,'user');
  chatHist.push({role:'user',content:msg});
  const tid=showTyping(),
    btn=document.getElementById('cbSend');
  btn.disabled=true;btn.textContent='...';
  fetch(`${API}/api/sheriff/chat`,{...})
  .then(r=>{...})
  .then(d=>{rmTyping(tid);addMsg(d.reply,'bot');
    chatHist.push({role:'assistant',content:d.reply});})
  .catch(()=>{rmTyping(tid);addMsg("Sorry...");})
  .finally(()=>{btn.disabled=false;
    btn.textContent='Send';});
}</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER (6 helpers + orchestrator)</div>
      <pre class="srp-new"><code>function getChatInput() { ... }
function addChatMessage(text, sender) { ... }
function showTypingIndicator() { ... }
function removeTypingIndicator(id) { ... }
function disableChatSend() { ... }
function enableChatSend() { ... }

function sendChat() {
  const msg = getChatInput();
  if (!msg) return;
  addChatMessage(msg, 'user');
  chatHist.push({ role: 'user', content: msg });
  const typingId = showTypingIndicator();
  disableChatSend();
  apiRequest('/api/sheriff/chat', 'POST',
    { message: msg, history: chatHist.slice(-10) })
    .then(d => {
      removeTypingIndicator(typingId);
      addChatMessage(d.reply, 'bot');
      chatHist.push({role:'assistant',content:d.reply});
    })
    .catch(() => { ... })
    .finally(enableChatSend);
}</code></pre>
    </div>
  </div>

  <p><strong>Why this is better:</strong> Each sub-task is its own function. <code>sendChat()</code> now only orchestrates the flow.</p>
</div>

<div class="srp-card">
  <h3>Problem: Duplicated fetch + error handling</h3>
  <p>The same fetch boilerplate was repeated in <code>doLogin</code>, <code>doSignup</code>, and <code>logout</code>.</p>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE (repeated 3x)</div>
      <pre class="srp-old"><code>fetch(`${API}/api/sheriff/authenticate`,{
  method:'POST',
  headers:{'Content-Type':'application/json'},
  credentials:'include',
  body:JSON.stringify({...})
})
.then(r=>{
  if(!r.ok) return r.json().then(d=>{
    throw new Error(d.message||'Login failed')
  });
  return r.json()
})</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER (one shared helper)</div>
      <pre class="srp-new"><code>function apiRequest(path, method, body) {
  const opts = {
    method, credentials: 'include',
    headers: {'Content-Type':'application/json'}
  };
  if (body) opts.body = JSON.stringify(body);
  return fetch(`${API}${path}`, opts).then(r => {
    if (!r.ok) return r.json().then(d => {
      throw new Error(
        d.message || d.error || 'Request failed'
      );
    });
    return r.json();
  });
}

// Usage — one clean line:
apiRequest('/api/sheriff/authenticate','POST',
  getLoginCredentials())
  .then(d => { user = d.user; ... })</code></pre>
    </div>
  </div>
</div>

<div class="srp-card">
  <h3>All Frontend SRP Extractions</h3>
  <table class="srp-table">
    <thead>
      <tr><th>Old Pattern</th><th>New Function</th><th>Responsibility</th></tr>
    </thead>
    <tbody>
      <tr><td>Inline <code>document.getElementById</code></td><td><code>el(id)</code></td><td>DOM element lookup</td></tr>
      <tr><td>Inline string escaping</td><td><code>sanitizeHTML(text)</code></td><td>XSS-safe text encoding</td></tr>
      <tr><td>Inline error display/hide</td><td><code>showError()</code> / <code>hideError()</code></td><td>Error display toggling</td></tr>
      <tr><td>Mixed FAQ filter + tag logic</td><td><code>setActiveFaqTag()</code>, <code>filterFaqByCategory()</code>, <code>filterFaqBySearch()</code></td><td>Each filter type isolated</td></tr>
      <tr><td>Inline search matching</td><td><code>findSearchMatches()</code>, <code>renderSearchDropdown()</code>, <code>handleSearchItemClick()</code></td><td>Search pipeline stages</td></tr>
      <tr><td>Scroll spy in event listener</td><td><code>getActiveSection()</code>, <code>highlightActiveNavLink()</code></td><td>Section detection vs DOM update</td></tr>
    </tbody>
  </table>
</div>

<!-- FILE 2 -->
<div class="srp-card">
  <h2>File 2: Backend Sheriff API</h2>
  <div class="srp-file-path">cap_back/api/sheriff.py</div>

  <h3>Problem: JWT decode + Sheriff lookup duplicated 4 times</h3>
  <p>The exact same token-decoding block appeared in <code>_ID.get()</code>, <code>_CRUD.get()</code>, <code>_CRUD.put()</code>, and <code>_CRUD.delete()</code>.</p>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE (copy-pasted 4x)</div>
      <pre class="srp-old"><code>token = request.cookies.get("jwt_sheriff")
if not token:
    return {'message': 'Not authenticated'}, 401
try:
    data = jwt.decode(token,
        current_app.config["SECRET_KEY"],
        algorithms=["HS256"])
    sheriff = Sheriff.query.filter_by(
        _uid=data["_uid"]).first()
    if not sheriff:
        return {'message': 'Sheriff not found'}, 404
except jwt.ExpiredSignatureError:
    return {'message': 'Token expired'}, 401
except jwt.InvalidTokenError:
    return {'message': 'Invalid token'}, 401</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER (one helper, used 4x)</div>
      <pre class="srp-new"><code>def decode_sheriff_token():
    """Read cookie, decode JWT, return Sheriff."""
    token = request.cookies.get("jwt_sheriff")
    if not token:
        raise AuthError(
            {'message': 'Not authenticated'}, 401)
    try:
        data = jwt.decode(token,
            current_app.config["SECRET_KEY"],
            algorithms=["HS256"])
    except jwt.ExpiredSignatureError:
        raise AuthError(
            {'message': 'Token expired'}, 401)
    except jwt.InvalidTokenError:
        raise AuthError(
            {'message': 'Invalid token'}, 401)
    sheriff = Sheriff.query.filter_by(
        _uid=data["_uid"]).first()
    if not sheriff:
        raise AuthError(
            {'message': 'Sheriff not found'}, 404)
    return sheriff

# Usage in any endpoint:
def get(self):
    try:
        sheriff = decode_sheriff_token()
        return jsonify(sheriff.read())
    except AuthError as e:
        return e.body, e.status_code</code></pre>
    </div>
  </div>
</div>

<div class="srp-card">
  <h3>Problem: Cookie-setting logic duplicated in login and logout</h3>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE (in both post and delete)</div>
      <pre class="srp-old"><code>is_production = os.environ.get(
    'IS_PRODUCTION', 'false').lower() == 'true'
cookie_name = "jwt_sheriff"
if is_production:
    resp.set_cookie(cookie_name, token,
        max_age=43200, secure=True,
        httponly=True, path='/',
        samesite='None',
        domain='.opencodingsociety.com')
else:
    resp.set_cookie(cookie_name, token,
        max_age=43200, secure=False,
        httponly=False, path='/',
        samesite='Lax')</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER (one function)</div>
      <pre class="srp-new"><code>def set_sheriff_cookie(response, token, max_age):
    """Set jwt_sheriff cookie for prod or dev."""
    is_prod = os.environ.get(
        'IS_PRODUCTION','false').lower() == 'true'
    name = "jwt_sheriff"
    if is_prod:
        response.set_cookie(name, token,
            max_age=max_age, secure=True,
            httponly=True, path='/',
            samesite='None',
            domain='.opencodingsociety.com')
    else:
        response.set_cookie(name, token,
            max_age=max_age, secure=False,
            httponly=False, path='/',
            samesite='Lax')
    return response

# Login:  set_sheriff_cookie(resp, token, 43200)
# Logout: set_sheriff_cookie(resp, '', 0)</code></pre>
    </div>
  </div>
</div>

<div class="srp-card">
  <h3>All Helpers Extracted in <code>sheriff.py</code></h3>
  <table class="srp-table">
    <thead>
      <tr><th>Helper</th><th>Responsibility</th><th>Replaces</th></tr>
    </thead>
    <tbody>
      <tr><td><code>decode_sheriff_token()</code></td><td>Read cookie &rarr; decode JWT &rarr; return Sheriff</td><td>4 copy-pasted blocks</td></tr>
      <tr><td><code>require_admin()</code></td><td>Decode + verify admin role</td><td>2 inline admin checks</td></tr>
      <tr><td><code>set_sheriff_cookie()</code></td><td>Set cookie with prod/dev settings</td><td>2 duplicated cookie blocks</td></tr>
      <tr><td><code>validate_signup_data()</code></td><td>Validate name/uid/badge/password</td><td>Inline validation in <code>post()</code></td></tr>
      <tr><td><code>AuthError</code> exception class</td><td>Carry error responses from helpers</td><td>Return tuples from nested code</td></tr>
    </tbody>
  </table>
</div>

<!-- FILE 3 -->
<div class="srp-card">
  <h2>File 3: AI Chatbot API</h2>
  <div class="srp-file-path">cap_back/api/sheriff_chat.py</div>

  <h3>Problem: One function did 5 things</h3>
  <p>The original <code>sheriff_chat()</code> validated input, checked the API key, built message history, called Claude, and parsed the response.</p>

  <div class="srp-compare">
    <div>
      <div class="srp-label srp-label-old">BEFORE (1 monolithic function)</div>
      <pre class="srp-old"><code>@sheriff_chat_api.route('/sheriff/chat',
    methods=['POST'])
def sheriff_chat():
    body = request.get_json()
    if not body or not body.get('message'):
        return jsonify({'error': '...'}), 400

    api_key = app.config.get('CLAUDE_API_KEY')
    if not api_key:
        return jsonify({'error': '...'}), 500

    user_message = body['message']
    history = body.get('history', [])

    messages = []
    for msg in history[-10:]:
        messages.append({
            "role": msg.get("role", "user"),
            "content": msg.get("content", "")
        })
    messages.append({"role":"user",
        "content": user_message})

    try:
        response = requests.post(CLAUDE_API_URL,
            headers={...}, json={...}, timeout=30)
        if response.status_code != 200: ...
        data = response.json()
        reply = data["content"][0]["text"]
        return jsonify({'reply': reply})
    except requests.Timeout: ...
    except Exception as e: ...</code></pre>
    </div>
    <div>
      <div class="srp-label srp-label-new">AFTER (5 focused functions)</div>
      <pre class="srp-new"><code>def validate_chat_request(body):
    """Extract and validate message + history."""
    if not body or not body.get('message'):
        raise ValueError('Message is required')
    return body['message'], body.get('history', [])

def build_message_history(history, user_message):
    """Build Claude API messages array."""
    messages = []
    for msg in history[-10:]:
        messages.append({...})
    messages.append(
      {"role":"user","content": user_message})
    return messages

def call_claude_api(api_key, messages):
    """Make the HTTP call to Claude."""
    return requests.post(CLAUDE_API_URL, ...)

def parse_claude_response(response):
    """Extract reply text from Claude response."""
    return response.json()["content"][0]["text"]

@sheriff_chat_api.route('/sheriff/chat',
    methods=['POST'])
def sheriff_chat():
    """Orchestrate: validate, build, call, parse."""
    body = request.get_json()
    try:
        msg, history = validate_chat_request(body)
    except ValueError as e:
        return jsonify({'error': str(e)}), 400
    ...
    messages = build_message_history(history, msg)
    response = call_claude_api(api_key, messages)
    reply = parse_claude_response(response)
    return jsonify({'reply': reply})</code></pre>
    </div>
  </div>
</div>

<!-- TAKEAWAYS -->
<div class="srp-takeaway">
  <h3>Key Takeaways</h3>
  <ul>
    <li><strong>Zero behavior changes</strong> &mdash; every endpoint, every button, every error message works identically</li>
    <li><strong>Eliminated duplication</strong> &mdash; JWT decoding: 4 copies &rarr; 1 function; cookie logic: 2 copies &rarr; 1; fetch boilerplate: 3 copies &rarr; 1</li>
    <li><strong>Functions went from ~5 responsibilities to 1</strong> &mdash; <code>sendChat()</code> dropped from 6 concerns to a clean orchestrator</li>
    <li><strong>Readability improved</strong> &mdash; function names describe what they do: <code>showLoggedInUI()</code>, <code>decode_sheriff_token()</code>, <code>validate_chat_request()</code></li>
    <li><strong>Testability improved</strong> &mdash; each helper can be unit tested in isolation</li>
  </ul>
</div>

<!-- FINAL STATS -->
<div class="srp-card">
  <h2>Files Changed Summary</h2>
  <table class="srp-table">
    <thead>
      <tr><th>File Path</th><th>Lines Before</th><th>Lines After</th><th>Functions Added</th></tr>
    </thead>
    <tbody>
      <tr><td><code>cap_front/navigation/sheriff/index.md</code> (JS)</td><td>~135</td><td>~265</td><td>+18 new helpers</td></tr>
      <tr><td><code>cap_back/api/sheriff.py</code></td><td>226</td><td>227</td><td>+5 helpers (AuthError + 4 functions)</td></tr>
      <tr><td><code>cap_back/api/sheriff_chat.py</code></td><td>174</td><td>227</td><td>+4 focused functions</td></tr>
    </tbody>
  </table>
</div>

</div>
