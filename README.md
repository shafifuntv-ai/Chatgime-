<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Introducing Chatgime</title>
  <meta name="description" content="Chatgime — a multilingual, human-like AI assistant created by Shahriar Haque Shafi." />
  <style>
    :root{
      --bg:#ffffff;         /* সাদা ব্যাকগ্রাউন্ড */
      --text:#111827;       /* ডার্ক টেক্সট */
      --muted:#6b7280;      /* ধূসর টেক্সট */
      --card:#ffffff;       /* কার্ড ব্যাকগ্রাউন্ড */
      --border:#e5e7eb;     /* হালকা বর্ডার */
      --brand:#1f3a8a;      /* নীল বাটন */
      --brand-hover:#1e40af;
      --note-bg:#f8fafc;    /* হালকা ধূসর নোট */
      --note-border:#e2e8f0;
      --fab:#000000;        /* কালো চ্যাট আইকন */
      --fab-border:#2b2b2b;
    }
    *{box-sizing:border-box}
    body{
      margin:0; background:var(--bg); color:var(--text);
      font-family:system-ui,-apple-system,Segoe UI,Roboto,"Noto Sans Bengali",sans-serif;
    }
    .hero-wrap{max-width:900px;margin:40px auto 20px;padding:0 20px}
    .hero-card{
      background:var(--card);
      border:1px solid var(--border);
      border-radius:16px;
      padding:24px;
      box-shadow:0 6px 20px rgba(0,0,0,.06);
    }
    .hero-eyebrow{color:var(--muted);font-size:12px;letter-spacing:.04em;text-transform:uppercase}
    .hero-title{font-size:42px;line-height:1.2;font-weight:800;margin:10px 0 16px}
    .hero-actions{display:flex;gap:10px;flex-wrap:wrap}
    .btn-primary{
      background:var(--brand);color:#fff;border:none;border-radius:999px;
      padding:10px 18px;font-weight:700;cursor:pointer;font-size:15px
    }
    .btn-primary:hover{background:var(--brand-hover)}
    .note{
      margin-top:14px;color:var(--muted);font-size:14px;
      background:var(--note-bg);border:1px solid var(--note-border);
      border-radius:12px;padding:10px 12px
    }
    footer{max-width:900px;margin:40px auto 30px;padding:0 20px;color:var(--muted);font-size:13px;text-align:center}

    /* Floating chat icon (bottom-right) */
    .chat-fab{
      position:fixed;right:18px;bottom:18px;width:56px;height:56px;border-radius:50%;
      background:var(--fab);color:#fff;border:1px solid var(--fab-border);
      display:flex;align-items:center;justify-content:center;font-size:22px;cursor:pointer;
      box-shadow:0 10px 30px rgba(0,0,0,.18);z-index:9999
    }
    .chat-fab:hover{transform:translateY(-1px)}
  </style>
</head>
<body>

  <div class="hero-wrap">
    <div class="hero-card">
      <!-- ✅ আজকের তারিখ সেট করা হলো -->
      <div class="hero-eyebrow">October 29, 2025 · Product</div>
      <h1 class="hero-title">Introducing Chatgime</h1>

      <div class="hero-actions">
        <button class="btn-primary" onclick="openChat()">Try Chatgime ↗</button>
      </div>

      <div class="note">
        <strong>Tip:</strong> To open the chat, click the <strong>black icon</strong> in the bottom-right.
      </div>
    </div>
  </div>

  <!-- Floating black chat icon -->
  <div class="chat-fab" title="Open Chat" onclick="openChat()">💬</div>

  <footer>
    Chatgime — Created by <strong>Shahriar Haque Shafi</strong>
  </footer>

  <script>
    // Helper to focus/trigger the Chatbase widget after load
    function openChat(){
      try{
        const iframe = document.querySelector('iframe[src*="chatbase"]');
        if (iframe) { iframe.contentWindow?.focus(); }
        // কিছু থিমে কেবল ফোকাসেই ওপেন হয়; না হলে ইউজার নিচের কালো আইকনে ক্লিক করবে
      }catch(e){ console.warn('Chat open fallback:', e); }
    }
  </script>

 <script>
(function(){if(!window.chatbase||window.chatbase("getState")!=="initialized"){window.chatbase=(...arguments)=>{if(!window.chatbase.q){window.chatbase.q=[]}window.chatbase.q.push(arguments)};window.chatbase=new Proxy(window.chatbase,{get(target,prop){if(prop==="q"){return target.q}return(...args)=>target(prop,...args)}})}const onLoad=function(){const script=document.createElement("script");script.src="https://www.chatbase.co/embed.min.js";script.id="MORmd4SOvmlI7onYRKeDK";script.domain="www.chatbase.co";document.body.appendChild(script)};if(document.readyState==="complete"){onLoad()}else{window.addEventListener("load",onLoad)}})();
</script
  <script>
  (function(){
    if(!window.chatbase||window.chatbase("getState")!=="initialized"){
      window.chatbase=(...a)=>{(window.chatbase.q=window.chatbase.q||[]).push(a)};
      window.chatbase=new Proxy(window.chatbase,{get(t,p){if(p==="q")return t.q;return(...a)=>t(p,...a)}});
    }
    const onLoad=function(){
      const s=document.createElement("script");
      s.src="https://www.chatbase.co/embed.min.js";
      s.id="YOUR_EMBED_ID";    /* ← এখানে তোমার Chatbase embed ID বসাও, যেমন: qh-QBSpTeK3Yu7CCsAA6D */
      s.domain="www.chatbase.co";
      document.body.appendChild(s);
    };
    if(document.readyState==="complete") onLoad();
    else window.addEventListener("load",onLoad);
  })();
  </script>

</body>
</html>
