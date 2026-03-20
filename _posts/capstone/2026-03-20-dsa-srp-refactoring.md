---
toc: false
layout: post
title: SRP Refactoring - DSA Portal Codebase
description: Applying the Single Responsibility Principle across three key files in the DSA portal — frontend JavaScript, backend API, and AI chatbot — with side-by-side code comparisons.
permalink: /capstone/dsa-srp-refactoring/
sticky_rank: 8
---

<style>
  .srp-blog { max-width: 900px; margin: 0 auto; font-family: 'Segoe UI', system-ui, sans-serif; color: #1e293b; line-height: 1.7; }
  .srp-blog h2 { color: #0f2847; border-bottom: 2px solid #f59e0b; padding-bottom: 6px; margin-top: 2rem; }
  .srp-blog h3 { color: #1e3a5f; margin-top: 1.5rem; }
  .srp-blog .file-path { background: #f1f5f9; border-left: 3px solid #f59e0b; padding: 6px 12px; font-family: monospace; font-size: 0.85rem; color: #334155; margin: 12px 0 8px; border-radius: 0 6px 6px 0; }
  .srp-blog .code-compare { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin: 12px 0; }
  .srp-blog .code-compare pre { margin: 0; font-size: 0.78rem; border-radius: 8px; padding: 14px; overflow-x: auto; }
  .srp-blog .old-code { background: #fef2f2; border: 1px solid #fecaca; }
  .srp-blog .old-code code { color: #991b1b; }
  .srp-blog .new-code { background: #f0fdf4; border: 1px solid #bbf7d0; }
  .srp-blog .new-code code { color: #166534; }
  .srp-blog .label { font-size: 0.72rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 4px; }
  .srp-blog .label-old { color: #dc2626; }
  .srp-blog .label-new { color: #16a34a; }
  .srp-blog .summary-card { background: linear-gradient(135deg, #0f2847, #1e3a5f); color: #e2e8f0; padding: 20px 24px; border-radius: 12px; margin: 20px 0; }
  .srp-blog .summary-card h3 { color: #fbbf24; margin-top: 0; }
  .srp-blog .summary-card ul { padding-left: 18px; }
  .srp-blog .summary-card li { margin-bottom: 4px; color: #cbd5e1; }
  .srp-blog table { width: 100%; border-collapse: collapse; margin: 12px 0; font-size: 0.85rem; }
  .srp-blog th { background: #0f2847; color: #fbbf24; padding: 10px 14px; text-align: left; }
  .srp-blog td { padding: 8px 14px; border-bottom: 1px solid #e2e8f0; }
  .srp-blog tr:nth-child(even) { background: #f8fafc; }
  @media (max-width: 700px) { .srp-blog .code-compare { grid-template-columns: 1fr; } }
</style>

<div class="srp-blog">

## What is the Single Responsibility Principle?

The **Single Responsibility Principle (SRP)** states that every function, class, or module should have **one reason to change** — meaning it should do exactly one thing. When a function handles validation, API calls, DOM updates, and error handling all at once, it becomes hard to read, test, and maintain. SRP refactoring splits these concerns so each piece has a clear, isolated purpose.

We applied SRP across **three files** in the DSA portal codebase without changing any functionality or UI:

| File | Type | Changes |
|------|------|---------|
| `navigation/sheriff/index.md` | Frontend JS | 14 monolithic functions &rarr; 30+ focused functions |
| `api/sheriff.py` | Backend API | 4x duplicated auth logic &rarr; 4 shared helpers |
| `api/sheriff_chat.py` | AI Chatbot | 1 monolithic handler &rarr; 5 single-purpose functions |

---

## File 1: Frontend JavaScript (DSA Portal UI)

<div class="file-path">cap_front/navigation/sheriff/index.md &mdash; &lt;script&gt; section</div>

### Problem: `updateUI()` did everything

The old `updateUI()` function handled both the logged-in and logged-out states in a single dense block with no separation:

<div class="code-compare">
<div>
<div class="label label-old">BEFORE</div>
<pre class="old-code"><code>function updateUI() {
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
<div class="label label-new">AFTER</div>
<pre class="new-code"><code>function showLoggedInUI() {
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

**Why this is better:** Each UI state is now its own function. `showLoggedInUI()` only populates the logged-in header. `showLoggedOutUI()` only resets to anonymous state. `updateUI()` is a one-line router.

---

### Problem: `sendChat()` handled input, API, DOM, and state

<div class="code-compare">
<div>
<div class="label label-old">BEFORE</div>
<pre class="old-code"><code>function sendChat(){
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
<div class="label label-new">AFTER</div>
<pre class="new-code"><code>function getChatInput() { ... }
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

**Why this is better:** Each sub-task is its own function: reading input, rendering messages, managing the typing indicator, and toggling the send button. `sendChat()` now only orchestrates the flow.

---

### Problem: Duplicated fetch + error handling across `doLogin`, `doSignup`, `logout`

<div class="code-compare">
<div>
<div class="label label-old">BEFORE (repeated in every auth function)</div>
<pre class="old-code"><code>fetch(`${API}/api/sheriff/authenticate`,{
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
<div class="label label-new">AFTER (one shared helper)</div>
<pre class="new-code"><code>function apiRequest(path, method, body) {
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

### Other frontend SRP extractions

| Old | New | Responsibility |
|-----|-----|---------------|
| inline `document.getElementById` everywhere | `el(id)` helper | DOM element lookup |
| inline string escaping in `addMsg` | `sanitizeHTML(text)` | XSS-safe text encoding |
| `closeModal()` hiding errors inline | `showError()` / `hideError()` | Error display toggling |
| FAQ filter + tag logic mixed | `setActiveFaqTag()`, `filterFaqByCategory()`, `filterFaqBySearch()` | Each filter type isolated |
| Inline search matching + rendering | `findSearchMatches()`, `renderSearchDropdown()`, `handleSearchItemClick()` | Search pipeline stages |
| Scroll spy inline in event listener | `getActiveSection()`, `highlightActiveNavLink()` | Section detection vs DOM update |

---

## File 2: Backend Sheriff API

<div class="file-path">cap_back/api/sheriff.py</div>

### Problem: JWT decode + Sheriff lookup duplicated 4 times

The exact same token-decoding block appeared in `_ID.get()`, `_CRUD.get()`, `_CRUD.put()`, and `_CRUD.delete()`:

<div class="code-compare">
<div>
<div class="label label-old">BEFORE (copy-pasted 4x)</div>
<pre class="old-code"><code>token = request.cookies.get("jwt_sheriff")
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
<div class="label label-new">AFTER (one helper, used 4x)</div>
<pre class="new-code"><code>def decode_sheriff_token():
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

### Problem: Cookie-setting logic duplicated in login and logout

<div class="code-compare">
<div>
<div class="label label-old">BEFORE (in both post and delete)</div>
<pre class="old-code"><code>is_production = os.environ.get(
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
<div class="label label-new">AFTER (one function)</div>
<pre class="new-code"><code>def set_sheriff_cookie(response, token, max_age):
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

### All helpers extracted in `sheriff.py`

| Helper | Responsibility | Replaces |
|--------|---------------|----------|
| `decode_sheriff_token()` | Read cookie &rarr; decode JWT &rarr; return Sheriff | 4 copy-pasted blocks |
| `require_admin()` | Decode + verify admin role | 2 inline admin checks |
| `set_sheriff_cookie()` | Set cookie with prod/dev settings | 2 duplicated cookie blocks |
| `validate_signup_data()` | Validate name/uid/badge/password | Inline validation in `post()` |
| `AuthError` exception class | Carry error responses from helpers | Return tuples from nested code |

---

## File 3: AI Chatbot API

<div class="file-path">cap_back/api/sheriff_chat.py</div>

### Problem: One function did 5 things

The original `sheriff_chat()` validated input, checked the API key, built message history, called Claude, and parsed the response:

<div class="code-compare">
<div>
<div class="label label-old">BEFORE (1 monolithic function)</div>
<pre class="old-code"><code>@sheriff_chat_api.route('/sheriff/chat',
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
<div class="label label-new">AFTER (5 focused functions)</div>
<pre class="new-code"><code>def validate_chat_request(body):
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

---

<div class="summary-card">
<h3>Key Takeaways</h3>
<ul>
<li><strong>Zero behavior changes</strong> &mdash; every endpoint, every button, every error message works identically</li>
<li><strong>Eliminated duplication</strong> &mdash; JWT decoding went from 4 copies to 1 function; cookie logic from 2 copies to 1; fetch boilerplate from 3 copies to 1</li>
<li><strong>Functions went from ~5 responsibilities to 1</strong> &mdash; <code>sendChat()</code> dropped from handling 6 concerns to being a clean orchestrator</li>
<li><strong>Readability improved</strong> &mdash; function names now describe what they do: <code>showLoggedInUI()</code>, <code>decode_sheriff_token()</code>, <code>validate_chat_request()</code></li>
<li><strong>Testability improved</strong> &mdash; each helper can be unit tested in isolation (e.g., test <code>build_message_history()</code> without an HTTP server)</li>
</ul>
</div>

### Files Changed

| File Path | Lines Before | Lines After | Functions Added |
|-----------|:---:|:---:|:---:|
| `cap_front/navigation/sheriff/index.md` (JS) | ~135 | ~265 | +18 new helpers |
| `cap_back/api/sheriff.py` | 226 | 227 | +5 helpers (AuthError + 4 functions) |
| `cap_back/api/sheriff_chat.py` | 174 | 227 | +4 focused functions |

</div>
