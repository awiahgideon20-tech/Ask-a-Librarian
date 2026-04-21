<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>WIUC Library Portal – Kumasi Campus</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --blue: #0a3d7a; --blue-dark: #072d5c; --blue-mid: #1a5296;
    --blue-light: #d6e6f7; --gold: #c9a227; --gold-light: #f5e4a0; --gold-dark: #9c7b18;
    --bg: #f5f5f5; --bg2: #ffffff; --text: #1a1a1a; --text2: #555; --border: rgba(0,0,0,0.12);
  }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; background: var(--bg); color: var(--text); }
  .page { max-width: 860px; margin: 0 auto; }
  .header { background: var(--blue); color: #fff; padding: 1.25rem 2rem; display: flex; align-items: center; gap: 1rem; border-bottom: 3px solid var(--gold); }
  .logo-circle { width: 56px; height: 56px; border-radius: 50%; overflow: hidden; background: #fff; flex-shrink: 0; display: flex; align-items: center; justify-content: center; border: 2px solid var(--gold); }
  .logo-circle img { width: 52px; height: 52px; object-fit: contain; }
  .header h1 { font-size: 16px; font-weight: 500; line-height: 1.4; }
  .header p { font-size: 12px; opacity: 0.7; margin-top: 2px; }
  .nav { background: var(--blue-dark); display: flex; border-bottom: 1px solid #051f42; }
  .nav button { background: none; border: none; color: rgba(255,255,255,0.6); font-size: 13px; padding: 10px 18px; cursor: pointer; font-family: inherit; transition: all 0.15s; border-bottom: 2px solid transparent; }
  .nav button:hover { background: rgba(255,255,255,0.07); color: #fff; }
  .nav button.active { color: var(--gold); border-bottom: 2px solid var(--gold); background: rgba(255,255,255,0.04); }
 
  /* Login */
  .login-wrap { background: var(--bg); min-height: 420px; display: flex; align-items: center; justify-content: center; padding: 2rem; }
  .login-card { background: var(--bg2); border: 1px solid var(--border); border-radius: 12px; padding: 2rem 2rem 1.75rem; width: 100%; max-width: 400px; box-shadow: 0 2px 16px rgba(0,0,0,0.08); }
  .login-card .top { text-align: center; margin-bottom: 1.5rem; }
  .login-logo { width: 80px; height: 80px; border-radius: 50%; overflow: hidden; background: #fff; border: 2px solid var(--gold); display: flex; align-items: center; justify-content: center; margin: 0 auto 12px; }
  .login-logo img { width: 74px; height: 74px; object-fit: contain; }
  .login-card h2 { font-size: 17px; font-weight: 500; color: var(--text); }
  .login-card .sub { font-size: 13px; color: var(--text2); margin-top: 4px; }
  .gold-bar { height: 3px; background: linear-gradient(90deg, var(--gold), var(--gold-light), var(--gold)); border-radius: 2px; margin: 1.25rem 0; }
  .field { margin-bottom: 14px; }
  .field label { display: block; font-size: 11px; font-weight: 600; color: var(--text2); margin-bottom: 5px; text-transform: uppercase; letter-spacing: 0.06em; }
  .field input { width: 100%; padding: 9px 12px; font-size: 14px; border: 1px solid var(--border); border-radius: 8px; font-family: inherit; background: #fff; color: var(--text); }
  .field input:focus { outline: none; border-color: var(--blue); box-shadow: 0 0 0 3px rgba(10,61,122,0.12); }
  .field .hint { font-size: 11px; color: var(--text2); margin-top: 4px; }
  .login-btn { width: 100%; background: var(--blue); color: #fff; border: none; border-radius: 8px; padding: 10px; font-size: 14px; font-weight: 500; cursor: pointer; font-family: inherit; transition: background 0.15s; margin-top: 6px; }
  .login-btn:hover { background: var(--blue-dark); }
  .login-footer { text-align: center; margin-top: 14px; font-size: 12px; color: var(--text2); }
  .login-footer a { color: var(--blue-mid); cursor: pointer; text-decoration: none; }
  .err-msg { background: #fde8e8; color: #8b1a1a; font-size: 12px; padding: 7px 10px; border-radius: 8px; margin-bottom: 12px; display: none; border: 1px solid #f5b8b8; }
  .err-msg.show { display: block; }
 
  /* App */
  .app { display: none; }
  .welcome-bar { background: var(--blue-light); border-bottom: 1px solid #b8d1ed; padding: 8px 1.5rem; font-size: 13px; color: var(--blue); display: flex; justify-content: space-between; align-items: center; }
  .welcome-bar button { background: none; border: 1px solid var(--blue); color: var(--blue); border-radius: 6px; padding: 3px 10px; font-size: 12px; cursor: pointer; font-family: inherit; }
  .welcome-bar button:hover { background: var(--blue); color: #fff; }
 
  /* Chat */
  .chat-area { padding: 1.25rem 1.25rem 0; min-height: 300px; max-height: 380px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; background: #f0f4f9; }
  .msg { display: flex; gap: 9px; align-items: flex-start; }
  .msg.user { flex-direction: row-reverse; }
  .avatar { width: 32px; height: 32px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 10px; font-weight: 600; flex-shrink: 0; }
  .avatar.bot { background: var(--blue); color: var(--gold); }
  .avatar.user { background: var(--gold); color: var(--blue-dark); }
  .bubble { max-width: 76%; padding: 9px 13px; border-radius: 12px; font-size: 13.5px; line-height: 1.65; }
  .bubble.bot { background: #fff; border: 1px solid var(--border); color: var(--text); border-radius: 4px 12px 12px 12px; }
  .bubble.user { background: var(--blue); color: #fff; border-radius: 12px 4px 12px 12px; }
  .typing { display: flex; gap: 4px; align-items: center; padding: 10px 13px; }
  .typing span { width: 6px; height: 6px; background: #aaa; border-radius: 50%; animation: bounce 1.2s infinite; }
  .typing span:nth-child(2) { animation-delay: 0.2s; }
  .typing span:nth-child(3) { animation-delay: 0.4s; }
  @keyframes bounce { 0%,80%,100%{transform:translateY(0)} 40%{transform:translateY(-6px)} }
  .quick-chips { display: flex; flex-wrap: wrap; gap: 7px; padding: 0.75rem 1.25rem 0.5rem; background: #f0f4f9; }
  .chip { background: #fff; border: 1px solid var(--border); border-radius: 20px; padding: 4px 13px; font-size: 12px; cursor: pointer; color: var(--text2); font-family: inherit; transition: all 0.15s; }
  .chip:hover { border-color: var(--blue); color: var(--blue); background: var(--blue-light); }
  .input-row { display: flex; gap: 9px; padding: 0.75rem 1.25rem 1.25rem; background: #f0f4f9; border-top: 1px solid var(--border); }
  .input-row input { flex: 1; font-size: 13.5px; padding: 8px 12px; border: 1px solid var(--border); border-radius: 8px; font-family: inherit; background: #fff; color: var(--text); }
  .input-row input:focus { outline: none; border-color: var(--blue); box-shadow: 0 0 0 2px rgba(10,61,122,0.1); }
  .send-btn { background: var(--blue); color: #fff; border: none; border-radius: 8px; padding: 8px 18px; font-size: 13px; cursor: pointer; font-family: inherit; }
  .send-btn:hover { background: var(--blue-dark); }
 
  /* Hours */
  .info-panel { padding: 1.25rem; background: var(--bg); display: none; flex-direction: column; gap: 1rem; }
  .info-panel.visible { display: flex; }
  .info-card { background: #fff; border: 1px solid var(--border); border-radius: 10px; padding: 1rem 1.25rem; }
  .info-card h3 { font-size: 14px; font-weight: 600; margin-bottom: 10px; color: var(--blue); }
  .badge { display: inline-block; font-size: 11px; padding: 2px 8px; border-radius: 10px; background: var(--gold-light); color: var(--gold-dark); font-weight: 600; margin-left: 6px; }
  .hours-row { display: flex; justify-content: space-between; font-size: 13px; padding: 6px 0; border-bottom: 1px solid var(--border); color: var(--text2); }
  .hours-row:last-child { border: none; }
  .hours-row strong { color: var(--text); font-weight: 500; }
  .info-card p, .info-card li { font-size: 13px; color: var(--text2); line-height: 1.7; }
  .info-card ul { padding-left: 1.1rem; }
 
  /* Citation */
  .citation-panel { padding: 1.25rem; background: var(--bg); display: none; flex-direction: column; gap: 1rem; }
  .citation-panel.visible { display: flex; }
  .cite-select { display: flex; gap: 7px; flex-wrap: wrap; margin-bottom: 0.75rem; }
  .cite-btn { background: #fff; border: 1px solid var(--border); border-radius: 8px; padding: 5px 13px; font-size: 13px; cursor: pointer; font-family: inherit; color: var(--text2); transition: all 0.15s; }
  .cite-btn.active { background: var(--blue); color: #fff; border-color: var(--blue); }
  .cite-form { display: flex; flex-direction: column; gap: 8px; }
  .cite-form input { font-size: 13px; padding: 7px 11px; border: 1px solid var(--border); border-radius: 8px; font-family: inherit; background: #fff; color: var(--text); }
  .cite-form input:focus { outline: none; border-color: var(--blue); }
  .cite-form .row2 { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .gen-btn { background: var(--blue); color: #fff; border: none; border-radius: 8px; padding: 8px 18px; font-size: 13px; cursor: pointer; font-family: inherit; align-self: flex-start; margin-top: 4px; }
  .gen-btn:hover { background: var(--blue-dark); }
  .cite-output { background: #f5f5f5; border: 1px solid var(--border); border-radius: 8px; padding: 1rem; font-size: 13px; color: var(--text2); line-height: 1.8; font-family: monospace; }
</style>
</head>
<body>
<div class="page">
  <div class="header">
    <div class="logo-circle">
      <img src="OIP.webp" alt="WIUC Logo" onerror="this.style.display='none';this.parentNode.innerHTML='<span style=\'color:var(--gold);font-weight:700;font-size:13px;\'>WIUC</span>'" />
    </div>
    <div>
      <h1>Wisconsin International University College</h1>
      <p>Kumasi Campus &middot; Library Portal</p>
    </div>
  </div>
 
  <!-- LOGIN -->
  <div id="loginPage">
    <div class="login-wrap">
      <div class="login-card">
        <div class="top">
          <div class="login-logo">
            <img src="OIP.webp" alt="WIUC Logo" onerror="this.style.display='none';this.parentNode.innerHTML='<span style=\'color:var(--gold);font-weight:700;font-size:18px;\'>WIUC</span>'" />
          </div>
          <div class="gold-bar"></div>
          <h2>Student Library Login</h2>
          <p class="sub">Sign in with your WIUC student credentials</p>
        </div>
        <div class="err-msg" id="errMsg">Invalid index number or password. Please try again.</div>
        <div class="field">
          <label>Index Number</label>
          <input type="text" id="studentId" placeholder="e.g. WIUC/KS/24/0001" onkeydown="if(event.key==='Enter') doLogin()" />
          <div class="hint">Enter your index number as it appears on your student ID card</div>
        </div>
        <div class="field">
          <label>Password</label>
          <input type="password" id="password" placeholder="Enter your password" onkeydown="if(event.key==='Enter') doLogin()" />
        </div>
        <button class="login-btn" onclick="doLogin()">Sign in to Library Portal</button>
        <div class="login-footer">
          <a onclick="forgotPw()">Forgot password?</a> &nbsp;&middot;&nbsp; <a onclick="helpMsg()">Need help?</a>
        </div>
      </div>
    </div>
  </div>
 
  <!-- MAIN APP -->
  <div class="app" id="mainApp">
    <div class="welcome-bar">
      <span id="welcomeText">Welcome back</span>
      <button onclick="doLogout()">Sign out</button>
    </div>
    <div class="nav">
      <button class="active" onclick="switchTab('chat')">Ask the assistant</button>
      <button onclick="switchTab('hours')">Library hours</button>
      <button onclick="switchTab('citation')">Citation generator</button>
    </div>
 
    <div id="tab-chat">
      <div class="chat-area" id="chatArea"></div>
      <div class="quick-chips">
        <button class="chip" onclick="sendChip('How do I access journal articles off-campus?')">Off-campus access</button>
        <button class="chip" onclick="sendChip('What research databases are available?')">Research databases</button>
        <button class="chip" onclick="sendChip('How do I renew my borrowed books?')">Renew books</button>
        <button class="chip" onclick="sendChip('Is the library open on weekends?')">Weekend hours</button>
        <button class="chip" onclick="sendChip('How do I request an interlibrary loan?')">Interlibrary loan</button>
      </div>
      <div class="input-row">
        <input type="text" id="userInput" placeholder="Ask about research, resources, hours, citations…" onkeydown="if(event.key==='Enter') sendMessage()" />
        <button class="send-btn" onclick="sendMessage()">Send</button>
      </div>
    </div>
 
    <div id="tab-hours" class="info-panel">
      <div class="info-card">
        <h3>Main Library Hours <span class="badge">Kumasi Campus</span></h3>
        <div class="hours-row"><span>Monday &ndash; Friday</span><strong>8:30 am &ndash; 5:00 pm</strong></div>
        <div class="hours-row"><span>Saturday</span><strong>9:00 am &ndash; 3:00 pm</strong></div>
        <div class="hours-row"><span>Sunday</span><strong>9:00 am &ndash; 3:00 pm</strong></div>
      </div>
      <div class="info-card">
        <h3>Public Holidays</h3>
        <p>The library is closed on all Ghanaian public holidays. Check the university notice board or portal for special opening announcements during exam periods.</p>
      </div>
      <div class="info-card">
        <h3>Contact &amp; Location</h3>
        <p>Wisconsin International University College, Kumasi Campus<br>Tel: +233 32 000 0000 &middot; library.kumasi@wiuc.edu.gh</p>
      </div>
    </div>
 
    <div id="tab-citation" class="citation-panel">
      <div class="info-card">
        <h3>Generate a citation</h3>
        <div class="cite-select">
          <button class="cite-btn active" onclick="setCiteStyle('APA')">APA 7th</button>
          <button class="cite-btn" onclick="setCiteStyle('MLA')">MLA 9th</button>
          <button class="cite-btn" onclick="setCiteStyle('Chicago')">Chicago 17th</button>
          <button class="cite-btn" onclick="setCiteStyle('Harvard')">Harvard</button>
        </div>
        <div class="cite-form">
          <input type="text" id="citeAuthor" placeholder="Author(s) e.g. Mensah, K. A." />
          <input type="text" id="citeTitle" placeholder="Title of work" />
          <div class="row2">
            <input type="text" id="citeYear" placeholder="Year e.g. 2023" />
            <input type="text" id="citePublisher" placeholder="Publisher / Journal" />
          </div>
          <input type="text" id="citeDoi" placeholder="DOI or URL (optional)" />
          <button class="gen-btn" onclick="generateCite()">Generate citation</button>
        </div>
      </div>
      <div class="info-card" id="citeResult" style="display:none;">
        <h3>Your citation <span class="badge" id="citeStyleLabel">APA</span></h3>
        <div class="cite-output" id="citeOutput"></div>
      </div>
    </div>
  </div>
</div>
 
<script>
let citeStyle = 'APA';
const knowledge = {
  hours: "The WIUC Kumasi Campus Library is open Monday to Friday from 8:30 am to 5:00 pm, and on Saturdays and Sundays from 9:00 am to 3:00 pm. The library is closed on public holidays.",
  databases: "The library provides access to databases including JSTOR, EBSCOhost, PubMed, IEEE Xplore, Scopus, Web of Science, and ProQuest. Log in with your WIUC credentials on the library portal.",
  offcampus: "You can access all e-resources off-campus using the university's VPN or the EZproxy link on the library website. Sign in with your index number and password.",
  interlibrary: "Interlibrary loans (ILL) can be requested at the circulation desk or via the library portal under 'Request a Document'. Allow 3–7 working days. Students get up to 10 free requests per semester.",
  renew: "Books can be renewed online via My Library Account on the portal, in person at the circulation desk, or by calling the library. You may renew up to 3 times unless another student has placed a hold.",
  research: "Our research librarians offer one-on-one consultations. Book a session via the library portal or email library.kumasi@wiuc.edu.gh. We can help with literature searches, database training, and referencing.",
  print: "Printing and scanning are available in the library. Use your student card to access the service — top up your print balance at the circulation desk or on the portal.",
  citation: "WIUC supports APA, MLA, Chicago, and Harvard referencing styles. Use the Citation Generator tab above, or attend a referencing workshop — check the university notice board for dates.",
  default: "I can help with research support, library hours, accessing resources, citations, and general library questions. Could you give me a bit more detail about what you need?"
};
function getReply(text) {
  const t = text.toLowerCase();
  if (/hour|open|clos|time|weekend|holiday|vacation/.test(t)) return knowledge.hours;
  if (/database|journal|article|access|ebsco|jstor|pubmed|scopus/.test(t)) return knowledge.databases;
  if (/off.?campus|remote|home|vpn|ezproxy/.test(t)) return knowledge.offcampus;
  if (/interlibrary|ill|loan|borrow from another/.test(t)) return knowledge.interlibrary;
  if (/renew|renewal|extend|overdue/.test(t)) return knowledge.renew;
  if (/research|librarian|consult|help.*find|find.*source|literature/.test(t)) return knowledge.research;
  if (/print|scan|copy|photocopy/.test(t)) return knowledge.print;
  if (/cit[ae]|referenc|apa|mla|chicago|harvard/.test(t)) return knowledge.citation;
  return knowledge.default;
}
function doLogin() {
  const id = document.getElementById('studentId').value.trim();
  const pw = document.getElementById('password').value.trim();
  const err = document.getElementById('errMsg');
  if (!id || !pw) { err.className = 'err-msg show'; err.textContent = 'Please enter your index number and password.'; return; }
  if (pw.length < 4) { err.className = 'err-msg show'; err.textContent = 'Invalid index number or password. Please try again.'; return; }
  err.className = 'err-msg';
  document.getElementById('loginPage').style.display = 'none';
  document.getElementById('mainApp').style.display = 'block';
  document.getElementById('welcomeText').textContent = 'Welcome, ' + id;
  addMsg('Hello! Welcome to the WIUC Kumasi Campus Library Portal. I can assist you with research, finding resources, library hours, and referencing. How can I help you today?', 'bot');
}
function doLogout() {
  document.getElementById('loginPage').style.display = 'block';
  document.getElementById('mainApp').style.display = 'none';
  document.getElementById('studentId').value = '';
  document.getElementById('password').value = '';
  document.getElementById('chatArea').innerHTML = '';
  switchTab('chat');
}
function forgotPw() { alert('Please visit the library desk or contact library.kumasi@wiuc.edu.gh to reset your password.'); }
function helpMsg() { alert('For login assistance, contact the library at library.kumasi@wiuc.edu.gh or call +233 32 000 0000.'); }
const chatArea = document.getElementById('chatArea');
function addMsg(text, sender) {
  const wrap = document.createElement('div'); wrap.className = 'msg ' + sender;
  const av = document.createElement('div'); av.className = 'avatar ' + (sender === 'bot' ? 'bot' : 'user');
  av.textContent = sender === 'bot' ? 'LIB' : 'YOU';
  const bub = document.createElement('div'); bub.className = 'bubble ' + (sender === 'bot' ? 'bot' : 'user');
  bub.textContent = text;
  wrap.appendChild(av); wrap.appendChild(bub);
  chatArea.appendChild(wrap); chatArea.scrollTop = chatArea.scrollHeight;
}
function showTyping() {
  const wrap = document.createElement('div'); wrap.className = 'msg bot'; wrap.id = 'typing-indicator';
  const av = document.createElement('div'); av.className = 'avatar bot'; av.textContent = 'LIB';
  const bub = document.createElement('div'); bub.className = 'bubble bot typing';
  bub.innerHTML = '<span></span><span></span><span></span>';
  wrap.appendChild(av); wrap.appendChild(bub);
  chatArea.appendChild(wrap); chatArea.scrollTop = chatArea.scrollHeight;
}
function removeTyping() { const t = document.getElementById('typing-indicator'); if (t) t.remove(); }
function sendMessage() {
  const input = document.getElementById('userInput');
  const text = input.value.trim(); if (!text) return;
  input.value = ''; addMsg(text, 'user'); showTyping();
  setTimeout(() => { removeTyping(); addMsg(getReply(text), 'bot'); }, 900 + Math.random() * 300);
}
function sendChip(text) { document.getElementById('userInput').value = text; sendMessage(); }
function switchTab(tab) {
  document.getElementById('tab-chat').style.display = tab === 'chat' ? 'block' : 'none';
  document.getElementById('tab-hours').className = 'info-panel' + (tab === 'hours' ? ' visible' : '');
  document.getElementById('tab-citation').className = 'citation-panel' + (tab === 'citation' ? ' visible' : '');
  document.querySelectorAll('.nav button').forEach((b, i) => { b.className = (['chat','hours','citation'][i] === tab) ? 'active' : ''; });
}
function setCiteStyle(s) {
  citeStyle = s;
  document.querySelectorAll('.cite-btn').forEach(b => b.className = 'cite-btn' + (b.textContent.startsWith(s) ? ' active' : ''));
}
function generateCite() {
  const author = document.getElementById('citeAuthor').value.trim() || 'Author, A.';
  const title = document.getElementById('citeTitle').value.trim() || 'Untitled Work';
  const year = document.getElementById('citeYear').value.trim() || 'n.d.';
  const pub = document.getElementById('citePublisher').value.trim() || 'Publisher';
  const doi = document.getElementById('citeDoi').value.trim();
  const doiStr = doi ? ' https://doi.org/' + doi.replace(/^https?:\/\/(doi\.org\/)?/, '') : '';
  let result = '';
  if (citeStyle === 'APA') result = author + ' (' + year + '). ' + title + '. ' + pub + '.' + doiStr;
  else if (citeStyle === 'MLA') result = author + ' "' + title + '." ' + pub + ', ' + year + '.' + (doi ? ' doi:' + doi : '');
  else if (citeStyle === 'Chicago') result = author + ' "' + title + '." ' + pub + ' (' + year + ').' + doiStr;
  else result = author + ' (' + year + ") '" + title + "', " + pub + '.' + doiStr;
  document.getElementById('citeStyleLabel').textContent = citeStyle;
  document.getElementById('citeOutput').textContent = result;
  document.getElementById('citeResult').style.display = 'block';
}
</script>
</body>
</html>
 
