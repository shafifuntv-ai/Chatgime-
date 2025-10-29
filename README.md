<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Introducing Chatgime — Multilingual AI</title>
  <meta name="description" content="Chatgime — a multilingual, human-like AI assistant created by Shahriar Haque Shafi." />
  <style>
    :root{
      --bg:#ffffff; --text:#111827; --muted:#6b7280;
      --card:#ffffff; --border:#e5e7eb;
      --brand:#1f3a8a; --brand-hover:#1e40af;
      --note-bg:#f8fafc; --note-border:#e2e8f0;
      --fab:#000000; --fab-border:#2b2b2b;
      --ok:#16a34a; --danger:#dc2626; --star:#f59e0b;
    }
    *{box-sizing:border-box}
    body{
      margin:0; background:var(--bg); color:var(--text);
      font-family:system-ui,-apple-system,Segoe UI,Roboto,"Noto Sans Bengali",sans-serif;
    }
    /* Layout */
    .wrap{max-width:980px;margin:40px auto 24px;padding:0 20px}
    .card{
      background:var(--card); border:1px solid var(--border); border-radius:16px;
      padding:24px; box-shadow:0 6px 20px rgba(0,0,0,.06)
    }
    .eyebrow{color:var(--muted);font-size:12px;letter-spacing:.04em;text-transform:uppercase}
    .title{font-size:42px;line-height:1.2;font-weight:800;margin:10px 0 10px}
    .lead{color:var(--muted);font-size:16px}
    .actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:14px}
    .btn{border:none;border-radius:999px;padding:10px 18px;font-weight:700;cursor:pointer}
    .btn.primary{background:var(--brand);color:#fff}
    .btn.primary:hover{background:var(--brand-hover)}
    .note{
      margin-top:14px;color:var(--muted);font-size:14px;
      background:var(--note-bg);border:1px solid var(--note-border);
      border-radius:12px;padding:10px 12px
    }
    footer{text-align:center;color:var(--muted);font-size:13px;margin:40px 0 30px;padding:0 20px}

    /* Floating chat icon (bottom-right) */
    .chat-fab{
      position:fixed; right:18px; bottom:18px; width:56px; height:56px; border-radius:50%;
      background:var(--fab); color:#fff; border:1px solid var(--fab-border);
      display:flex; align-items:center; justify-content:center; font-size:22px; cursor:pointer;
      box-shadow:0 10px 30px rgba(0,0,0,.18); z-index:9999
    }
    .chat-fab:hover{transform:translateY(-1px)}

    /* Rating panel (bottom-left) */
    .rating-panel{
      position:fixed; left:18px; bottom:18px; z-index:9999;
      background:#ffffff; border:1px solid var(--border); border-radius:14px;
      box-shadow:0 10px 30px rgba(0,0,0,.12);
      width:300px; max-width:88vw; padding:12px
    }
    .rating-header{display:flex;align-items:center;gap:8px;font-weight:700}
    .rating-stars{display:flex;gap:6px;margin:8px 0}
    .star-btn{
      width:32px; height:32px; border-radius:8px; border:1px solid var(--border);
      display:flex; align-items:center; justify-content:center; cursor:pointer; background:#fff;
      font-size:18px; transition:.15s
    }
    .star-btn.active, .star-btn:hover{border-color:#fbbf24; background:#fff7ed}
    .star{color:var(--star); line-height:1}
    .rating-msg{font-size:13px; color:var(--muted); margin-top:4px}
    .rating-row{display:flex; gap:6px; margin-top:8px}
    .rating-input{
      flex:1; border:1px solid var(--border); border-radius:8px; padding:8px; font-size:14px
    }
    .send-btn{
      border:none; border-radius:8px; padding:8px 10px; font-weight:700; cursor:pointer;
      background:var(--brand); color:#fff
    }
    .thanks{display:none; margin-top:8px; font-size:13px; color:var(--ok)}
    .minitext{font-size:12px; color:var(--muted); margin-top:6px}

    /* Responsive */
    @media (max-width:640px){
      .title{font-size:34px}
      .chat-fab{right:14px; bottom:14px}
      .rating-panel{left:14px; bottom:14px; width:280px}
    }
  </style>
</head>
<body>
<script>
(function(){if(!window.chatbase||window.chatbase("getState")!=="initialized"){window.chatbase=(...arguments)=>{if(!window.chatbase.q){window.chatbase.q=[]}window.chatbase.q.push(arguments)};window.chatbase=new Proxy(window.chatbase,{get(target,prop){if(prop==="q"){return target.q}return(...args)=>target(prop,...args)}})}const onLoad=function(){const script=document.createElement("script");script.src="https://www.chatbase.co/embed.min.js";script.id="MORmd4SOvmlI7onYRKeDK";script.domain="www.chatbase.co";document.body.appendChild(script)};if(document.readyState==="complete"){onLoad()}else{window.addEventListener("load",onLoad)}})();
</script>
  <div class="wrap">
    <div class="card">
      <!-- ✅ correct date -->
      <div class="eyebrow">October 29, 2025 · Product</div>
      <h1 class="title">Introducing Chatgime</h1>
      <p class="lead">
        Chatgime হলো একটি multilingual, human-like AI assistant—বাংলা সহ যেকোনো ভাষায় কথা বলে।
        “Who created you?” জিজ্ঞেস করলে উত্তর দেয়: <b>“I was created by Shahriar Haque Shafi.”</b>
      </p>

      <div class="actions">
        <button class="btn primary" onclick="openChat()">Try Chatgime ↗</button>
      </div>

      <div class="note">
        <strong>Tip:</strong> To open the chat, click the <strong>black icon</strong> in the bottom-right.
      </div>
    </div>
  </div>

  <!-- Floating black chat icon -->
  <div class="chat-fab" title="Open Chat" onclick="openChat()">💬</div>

  <!-- Rating Panel (bottom-left) -->
  <div class="rating-panel" id="ratingPanel" aria-live="polite">
    <div class="rating-header">⭐ Rate this chat</div>
    <div class="rating-stars" role="radiogroup" aria-label="Rate from 1 to 5">
      <button class="star-btn" data-val="1" aria-label="1 star"><span class="star">★</span></button>
      <button class="star-btn" data-val="2" aria-label="2 stars"><span class="star">★</span></button>
      <button class="star-btn" data-val="3" aria-label="3 stars"><span class="star">★</span></button>
      <button class="star-btn" data-val="4" aria-label="4 stars"><span class="star">★</span></button>
      <button class="star-btn" data-val="5" aria-label="5 stars"><span class="star">★</span></button>
    </div>
    <div class="rating-msg" id="ratingMsg">How was your experience?</div>

    <div class="rating-row">
      <input class="rating-input" id="ratingNote" placeholder="Optional feedback (Bangla/English)…" />
      <button class="send-btn" id="sendFeedback">Send</button>
    </div>
    <div class="thanks" id="thanksMsg">✅ Thanks! Your feedback is saved on this device.</div>
    <div class="minitext">Your rating is stored locally (no server).</div>
  </div>

  <footer>
    Chatgime — Created by <strong>Shahriar Haque Shafi</strong>
  </footer>

  <script>
    // === Chat open helper ===
    function openChat(){
      try{
        const iframe = document.querySelector('iframe[src*="chatbase"]');
        if (iframe) { iframe.contentWindow?.focus(); }
      }catch(e){ console.warn('Chat open fallback:', e); }
    }

    // === Rating logic (localStorage) ===
    (function(){
      const stars = document.querySelectorAll('.star-btn');
      const msg = document.getElementById('ratingMsg');
      const note = document.getElementById('ratingNote');
      const send = document.getElementById('sendFeedback');
      const thanks = document.getElementById('thanksMsg');
      const KEY = 'chatgime_rating_v1';

      // Load previous
      try{
        const saved = JSON.parse(localStorage.getItem(KEY) || '{}');
        if(saved && saved.value){
          setActive(saved.value);
          msg.textContent = `Your rating: ${saved.value}/5`;
          if(saved.note){ note.value = saved.note; }
        }
      }catch(e){}

      function setActive(val){
        stars.forEach(btn=>{
          btn.classList.toggle('active', Number(btn.dataset.val) <= val);
        });
      }

      stars.forEach(btn=>{
        btn.addEventListener('click', ()=>{
          const val = Number(btn.dataset.val);
          setActive(val);
          msg.textContent = `Your rating: ${val}/5`;
          const data = JSON.parse(localStorage.getItem(KEY) || '{}');
          localStorage.setItem(KEY, JSON.stringify({ ...data, value: val, ts: Date.now() }));
          thanks.style.display = 'block';
          setTimeout(()=> thanks.style.display = 'none', 1500);
        });
      });

      send.addEventListener('click', ()=>{
        const data = JSON.parse(localStorage.getItem(KEY) || '{}');
        localStorage.setItem(KEY, JSON.stringify({ ...data, note: note.value || '', ts: Date.now() }));
        thanks.style.display = 'block';
        setTimeout(()=> thanks.style.display = 'none', 1500);
      });
    })();
  </script>

  <!-- === Chatbase Embed (Replace YOUR_EMBED_ID) === -->
  <script>
  (function(){
    if(!window.chatbase||window.chatbase("getState")!=="initialized"){
      window.chatbase=(...a)=>{(window.chatbase.q=window.chatbase.q||[]).push(a)};
      window.chatbase=new Proxy(window.chatbase,{get(t,p){if(p==="q")return t.q;return(...a)=>t(p,...a)}});
    }
    const onLoad=function(){
      const s=document.createElement("script");
      s.src="https://www.chatbase.co/embed.min.js";
      s.id="YOUR_EMBED_ID";  /* ← এখানে তোমার Chatbase embed ID বসাও, যেমন: qh-QBSpTeK3Yu7CCsAA6D */
      s.domain="www.chatbase.co";
      document.body.appendChild(s);
    };
    if(document.readyState==="complete") onLoad();
    else window.addEventListener("load",onLoad);
  })();
  </script>
</body>
</html>
