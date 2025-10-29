<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Introducing Chatgime</title>
  <style>
    body {
      background: #0f172a;
      color: #e5e7eb;
      font-family: system-ui, -apple-system, "Noto Sans Bengali", sans-serif;
      margin: 0;
      padding: 0;
    }
    .hero-wrap {
      max-width: 900px;
      margin: 40px auto;
      padding: 0 20px;
      text-align: left;
    }
    .hero-card {
      background: #0b1220;
      border: 1px solid #1f2937;
      border-radius: 16px;
      padding: 24px;
      box-shadow: 0 10px 30px rgba(0,0,0,.35);
    }
    .hero-eyebrow {
      color: #9ca3af;
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: .04em;
    }
    .hero-title {
      font-size: 42px;
      line-height: 1.2;
      font-weight: 800;
      margin: 10px 0 20px;
    }
    .hero-actions {
      display: flex;
      gap: 10px;
    }
    .btn-primary {
      background: #1f3a8a;
      color: #fff;
      border: none;
      border-radius: 999px;
      padding: 10px 18px;
      font-weight: 600;
      cursor: pointer;
      font-size: 15px;
    }
    .btn-primary:hover {
      background: #1e40af;
    }
    .note {
      margin-top: 14px;
      color: #9ca3af;
      font-size: 14px;
      background: #0a0f1a;
      border: 1px solid #1e293b;
      border-radius: 12px;
      padding: 10px 12px;
    }
    /* Floating chat icon */
    .chat-fab {
      position: fixed;
      right: 18px;
      bottom: 18px;
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background: #000;
      color: #fff;
      border: 1px solid #2b2b2b;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 22px;
      cursor: pointer;
      box-shadow: 0 10px 30px rgba(0,0,0,.4);
      z-index: 9999;
    }
    .chat-fab:hover {
      transform: translateY(-2px);
    }
    footer {
      text-align: center;
      margin: 60px 0 20px;
      color: #9ca3af;
      font-size: 13px;
    }
  </style>
</head>
<body>

  <div class="hero-wrap">
    <div class="hero-card">
      <div class="hero-eyebrow">November 30, 2022 · Product</div>
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
    function openChat(){
      try {
        const iframe = document.querySelector('iframe[src*="chatbase"]');
        if (iframe) iframe.contentWindow?.focus();
      } catch(e){ console.warn('Chat open fallback:', e); }
    }
  </script>

  <!-- Chatbase Embed -->
  <script>
  (function(){
    if(!window.chatbase||window.chatbase("getState")!=="initialized"){
      window.chatbase=(...a)=>{(window.chatbase.q=window.chatbase.q||[]).push(a)};
      window.chatbase=new Proxy(window.chatbase,{get(t,p){if(p==="q")return t.q;return(...a)=>t(p,...a)}});
    }
    const onLoad=function(){
      const s=document.createElement("script");
      s.src="https://www.chatbase.co/embed.min.js";
      s.id="YOUR_EMBED_ID";    // ← এখানে তোমার Chatbase embed ID বসাও
      s.domain="www.chatbase.co";
      document.body.appendChild(s);
    };
    if(document.readyState==="complete") onLoad();
    else window.addEventListener("load",onLoad);
  })();
  </script>

</body>
</html>
