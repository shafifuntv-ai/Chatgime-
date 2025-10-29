<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Chatgime — Live Multilingual AI</title>
  <style>
    *{box-sizing:border-box;margin:0;padding:0}
    body{
      background:#0f172a;color:#e2e8f0;font-family:"Noto Sans Bengali",sans-serif;
      display:flex;flex-direction:column;height:100vh;
    }
    header{background:#1e3a8a;color:#fff;text-align:center;padding:12px;font-weight:bold}
    main{flex:1;overflow-y:auto;padding:12px;display:flex;flex-direction:column}
    .msg{margin:8px 0;padding:10px 14px;border-radius:10px;max-width:80%;line-height:1.5}
    .user{align-self:flex-end;background:#2563eb;color:#fff}
    .bot{align-self:flex-start;background:#1e293b;color:#cbd5e1}
    footer{background:#111827;display:flex;gap:8px;padding:10px;border-top:1px solid #1e293b}
    input{flex:1;background:#0b1220;color:#fff;border:none;border-radius:8px;padding:10px}
    button{background:#22d3ee;border:none;border-radius:8px;padding:10px 14px;font-weight:bold;cursor:pointer;color:#001016}
    #mic{background:#10b981}
    .credit{text-align:center;color:#94a3b8;font-size:13px;padding:6px}
  </style>
</head>
<body>
  <header>💬 Chatgime — Live AI</header>
  <main id="chatbox">
    <div class="msg bot">হ্যালো! আমি Chatgime 🤖 — যে কোনো ভাষায় কথা বলো। আমি লাইভ AI উত্তর দেবো।</div>
  </main>
  <footer>
    <input id="q" placeholder="বাংলায় লিখুন বা বলুন ..." />
    <button id="mic">🎤</button>
    <button id="send">পাঠান</button>
  </footer>
  <div class="credit">🚀 Chatgime — Created by Shahariar Haque Shafi</div>

<script>
const chat=document.getElementById("chatbox");
const input=document.getElementById("q");
const mic=document.getElementById("mic");
const send=document.getElementById("send");

function add(text,cls){const d=document.createElement("div");d.className="msg "+cls;d.innerHTML=text;chat.appendChild(d);chat.scrollTop=chat.scrollHeight;}

async function sendMsg(){
  const txt=input.value.trim();
  if(!txt)return;
  add(txt,"user");
  input.value="";
  add("🤖 চিন্তা করছি ...","bot");
  const reply=await askAI(txt);
  document.querySelector(".msg.bot:last-child").innerHTML=reply;
  speak(reply);
}

// 🔑 তোমার OpenAI API key এখানে দাও
const OPENAI_KEY=

async function askAI(q){
  try{
    const r=await fetch("https://api.openai.com/v1/chat/completions",{
      method:"POST",
      headers:{
        "Content-Type":"application/json",
        "Authorization":"Bearer "+OPENAI_KEY
      },
      body:JSON.stringify({
        model:"gpt-3.5-turbo",
        messages:[{role:"system",content:"You are Chatgime, a helpful multilingual AI assistant."},{role:"user",content:q}],
        temperature:0.8
      })
    });
    const data=await r.json();
    return data.choices?.[0]?.message?.content?.trim()||"❌ উত্তর পাওয়া যায়নি।";
  }catch(e){return "⚠️ সার্ভার এরর — পরে চেষ্টা করুন।";}
}

// 🎤 Voice input
const SR=window.SpeechRecognition||window.webkitSpeechRecognition;
if(SR){
  const recog=new SR();recog.lang="bn-BD";
  mic.onclick=()=>{try{recog.start();mic.textContent="🎙️";}catch(e){}};
  recog.onresult=e=>{input.value=e.results[0][0].transcript;mic.textContent="🎤";};
  recog.onend=()=>mic.textContent="🎤";
}else mic.disabled=true;

// 🔊 Voice output
function speak(t){const m=new SpeechSynthesisUtterance(t);m.lang="bn-BD";speechSynthesis.speak(m);}

send.onclick=sendMsg;
input.addEventListener("keypress",e=>e.key==="Enter"&&sendMsg());
</script>
</body>
</html>
