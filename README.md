<html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>Verb Move Challenge</title>
<style>
/* ===== STYLE (semua ukuran dalam em; 1em = 1% lebar layar 16:9) ===== */
*{box-sizing:border-box;margin:0}
:root{--y:#ffd23f;--a:#2f6bff;--b:#ff3d5a;--g:#2ee59d;--ink:#12103a}
body{background:#05041a;height:100vh;display:grid;place-items:center;overflow:hidden;font-family:"Trebuchet MS","Segoe UI",system-ui,sans-serif;color:#fff}
#stage{position:relative;width:min(100vw,177.78vh);aspect-ratio:16/9;overflow:hidden;background:radial-gradient(circle at 20% 10%,#3b2a9c,transparent 50%),radial-gradient(circle at 85% 90%,#0e6b8f,transparent 50%),var(--ink)}
.screen{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;justify-content:center;gap:1.6em;padding:3em;text-align:center}
.screen.on{display:flex;animation:in .5s}
@keyframes in{from{opacity:0;transform:scale(.96)}}
h1{font-size:6.4em;line-height:1;font-weight:900;text-shadow:0 .08em 0 #0006,0 0 .6em #ffd23f55}
h1 span{color:var(--y)}
.brand{font-size:2.2em;font-weight:800;color:var(--g)}
.sub{font-size:3em;font-weight:800;letter-spacing:.12em;color:var(--y)}
.chips{display:flex;gap:2em;font-size:2.2em;font-weight:700}
.chips div{background:#ffffff18;padding:.4em 1em;border-radius:1em}
.btn{font:inherit;font-weight:900;font-size:2.4em;padding:.45em 1.4em;border:0;border-radius:2em;background:var(--y);color:#1a1440;box-shadow:0 .25em 0 #c79a00,0 0 2em #ffd23f66;cursor:pointer;transition:transform .15s}
.btn:hover,.btn:focus-visible{transform:scale(1.06);outline:none}
.btn.alt{background:#ffffff22;color:#fff;box-shadow:0 .25em 0 #0005}
.row{display:flex;gap:1.5em;align-items:center}
.corner{position:absolute;top:1.2em;right:1.2em;z-index:20;display:flex;gap:.8em}
.corner button{font:inherit;font-size:1.5em;font-weight:800;padding:.4em .9em;border:0;border-radius:1em;background:#ffffff26;color:#fff;cursor:pointer}
/* camera check */
.camwrap{position:relative;width:46em;height:26em;border-radius:2em;overflow:hidden;border:.35em solid var(--y);background:#000}
video.mir{width:100%;height:100%;object-fit:cover;transform:scaleX(-1)}
.zones{position:absolute;inset:0;display:flex;font-size:1.8em;font-weight:900}
.zones div{display:flex;align-items:flex-end;justify-content:center;padding:.4em;border-right:.1em dashed #fff9}
.zones div:last-child{border:0}
.zL{width:40%;background:#2f6bff44}.zC{width:20%;background:#2ee59d33}.zR{width:40%;background:#ff3d5a44}
.mk{position:absolute;top:50%;width:3em;height:3em;margin:-1.5em 0 0 -1.5em;border-radius:50%;background:var(--y);box-shadow:0 0 2em var(--y);transition:left .12s}
#zlabel{font-size:4em;font-weight:900;animation:pulse 1s infinite}
@keyframes pulse{50%{transform:scale(1.07)}}
/* game */
#game{justify-content:flex-start;gap:.8em;padding:2em 3em 2.5em}
.top{display:flex;justify-content:space-between;align-items:center;width:100%;font-weight:900;font-size:3.2em}
.top .tm{background:#fff;color:var(--ink);border-radius:1em;padding:0 .6em;min-width:2.4em}
.top .tm.low{background:var(--b);color:#fff;animation:pulse .5s infinite}
#cb{color:var(--y);font-size:.7em;min-width:7em}
.pbar{width:100%;height:1.1em;border-radius:1em;background:#ffffff22;overflow:hidden}
#pb{height:100%;width:100%;background:linear-gradient(90deg,var(--g),var(--y))}
#qt{flex:1;display:flex;align-items:center;font-size:4.6em;font-weight:900;line-height:1.15;max-width:85%}
.track{position:relative;width:100%;height:1.6em;border-radius:1em;background:linear-gradient(90deg,#2f6bff88 40%,#2ee59d55 40% 60%,#ff3d5a88 60%)}
.track .mk{width:2.4em;height:2.4em;margin:-.4em 0 0 -1.2em;top:0}
#mv{height:1.4em;font-size:2.4em;font-weight:900;color:var(--y)}
.panels{display:flex;gap:2em;width:100%;height:20em}
.pan{position:relative;flex:1;border-radius:2em;display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:5.4em;font-weight:900;overflow:hidden;transition:.3s}
.pan small{font-size:.8em}
.pan.A{background:linear-gradient(#4a82ff,#1b3fd0)}.pan.B{background:linear-gradient(#ff5470,#c4153a)}
.pan.win{box-shadow:0 0 .8em #2ee59d,0 0 0 .08em #2ee59d inset;transform:scale(1.03)}.pan.dim{opacity:.3}
.hb{position:absolute;left:0;bottom:0;height:.14em;width:0;background:var(--y)}
.pip{position:absolute;right:2.5em;top:12em;width:15em;text-align:center;font-size:1.3em;font-weight:800}
.pip video{width:100%;aspect-ratio:4/3;border-radius:1em;border:.2em solid #fff;object-fit:cover;background:#000}
#warn{color:#ff8da1;font-size:.9em}
#fb{position:absolute;inset:0;display:none;flex-direction:column;align-items:center;justify-content:center;background:#000a;z-index:10}
#fb.on{display:flex;animation:pop .4s}
#fbT{font-size:9em;font-weight:900}#fbS{font-size:3.4em;font-weight:800}
@keyframes pop{from{transform:scale(.4);opacity:0}}
.shake{animation:sh .5s}
@keyframes sh{20%,60%{transform:translateX(-2em)}40%,80%{transform:translateX(2em)}}
#rs{font-size:9em;font-weight:900;color:var(--y);text-shadow:0 0 .4em #ffd23f88}
.stats{font-size:2.6em;font-weight:800}
/* modal */
.modal{position:absolute;inset:0;background:#000b;z-index:30;display:none;align-items:center;justify-content:center}
.modal.on{display:flex}
.box{background:#241d63;border:.2em solid var(--y);border-radius:2em;padding:2.5em 3.5em;display:flex;flex-direction:column;gap:1em;align-items:center;font-size:2em;max-width:80%;text-align:left}
.box h3{font-size:1.5em;color:var(--y)}.box label{display:flex;justify-content:space-between;gap:2em;width:100%;font-weight:700}
.box select,.box input{font:inherit;font-size:.9em}
#fx{position:absolute;inset:0;pointer-events:none;z-index:40}
</style></head><body>
<div id="stage">
<video id="src" muted playsinline style="position:absolute;opacity:0;width:1px;height:1px"></video>
<div class="corner"><button id="snd">🔊 SOUND ON</button><button id="gear">⚙️ TEACHER SETTINGS</button></div>

<!-- START -->
<section id="start" class="screen on">
 <div class="brand">🎮 VERB MOVE CHALLENGE</div>
 <h1>REGULAR &amp;<br><span>IRREGULAR VERBS</span></h1>
 <div class="sub">MOVE • THINK • ANSWER!</div>
 <div class="chips"><div>🎯 <b id="cQ">20</b> Questions</div><div>⏱️ <b id="cT">10</b> Seconds</div><div>🏆 Get the Highest Score!</div></div>
 <div class="row"><button class="btn" id="bStart">START GAME</button><button class="btn alt" id="bHow">HOW TO PLAY</button></div>
</section>

<!-- CAMERA CHECK -->
<section id="cam" class="screen">
 <h1 style="font-size:4.4em">📷 CAMERA CHECK</h1>
 <p style="font-size:2.2em;font-weight:700">Get Ready! Stand in front of the camera.</p>
 <div class="camwrap"><video id="camVid" class="mir" muted playsinline></video>
  <div class="zones"><div class="zL">LEFT ZONE</div><div class="zC">CENTER ZONE</div><div class="zR">RIGHT ZONE</div></div><div class="mk" id="mk"></div></div>
 <div id="zlabel">…</div>
 <div class="row"><button class="btn" id="bGo">LET'S GO!</button><button class="btn alt" id="bBack1">BACK</button></div>
</section>

<!-- GAME -->
<section id="game" class="screen">
 <div class="top"><span id="qn">Q 01/20</span><span id="cb"></span><span id="sc">SCORE 000</span><span class="tm" id="tm">10</span></div>
 <div class="pbar"><div id="pb"></div></div>
 <div id="qt">…</div>
 <div id="mv"></div>
 <div class="track"><div class="mk" id="mk2"></div></div>
 <div class="panels">
  <div class="pan A" id="pA"><span id="ta"></span><small>⬅️</small><div class="hb" id="hA"></div></div>
  <div class="pan B" id="pB"><span id="tb"></span><small>➡️</small><div class="hb" id="hB"></div></div>
 </div>
 <div class="pip"><video id="pipVid" class="mir" muted playsinline></video><div id="trk">🟢 TRACKING</div><div id="warn"></div></div>
 <div id="fb"><div id="fbT"></div><div id="fbS"></div></div>
</section>

<!-- RESULT -->
<section id="result" class="screen">
 <h1 style="font-size:5.4em">🎉 GAME COMPLETE!</h1>
 <div class="stats">YOUR SCORE</div><div id="rs">0</div>
 <div class="stats" id="rc"></div>
 <div class="stats" style="color:var(--y);font-size:4em" id="rf"></div>
 <div class="row"><button class="btn" id="bAgain">PLAY AGAIN</button><button class="btn alt" id="bMenu">BACK TO MENU</button></div>
</section>

<!-- MODALS -->
<div class="modal" id="how"><div class="box"><h3>HOW TO PLAY</h3>
 <div>1️⃣ Stand in front of the camera.</div><div>2️⃣ Look at the two answers.</div><div>3️⃣ Move your body to the LEFT or RIGHT.</div>
 <div>4️⃣ Stay in position until your answer is detected.</div><div>5️⃣ Get points for every correct answer.</div><div>6️⃣ Try to get the highest score!</div>
 <button class="btn" id="bHowOk" style="font-size:1em">LET'S PLAY!</button></div></div>
<div class="modal" id="nocam"><div class="box"><h3>CAMERA NOT AVAILABLE</h3><p id="ncMsg">Camera access is required for movement-based gameplay.</p>
 <div class="row"><button class="btn" id="bDemo" style="font-size:.9em">USE DEMO MODE</button><button class="btn alt" id="bRetry" style="font-size:.9em">TRY AGAIN</button></div></div></div>
<div class="modal" id="set"><div class="box"><h3>TEACHER SETTINGS</h3>
 <label>Number of Questions <select id="sN"><option>10</option><option>15</option><option selected>20</option><option>25</option></select></label>
 <label>Timer (seconds) <select id="sT"><option>5</option><option selected>10</option><option>15</option><option>20</option></select></label>
 <label>Sound <input type="checkbox" id="sS" checked></label><label>Camera <input type="checkbox" id="sC" checked></label>
 <label>Demo Mode (← → keys) <input type="checkbox" id="sD"></label><label>Random Questions <input type="checkbox" id="sR" checked></label>
 <div class="row"><button class="btn" id="bSetOk" style="font-size:.9em">SAVE</button><button class="btn alt" id="bReset" style="font-size:.9em">RESET GAME</button></div></div></div>
<canvas id="fx"></canvas>
</div>

<script>
/* ============ DATA SOAL (guru bisa edit/tambah di sini) ============
   q("pertanyaan","jawaban A","jawaban B","A atau B yang benar")
   Posisi jawaban otomatis diacak saat game dimulai. */
const q=(question,answerA,answerB,correct='A')=>({question,answerA,answerB,correct});
const questions=[
 q('What is the past form of "GO"?','WENT','GOED'), q('What is the past form of "PLAY"?','PLAYED','PLAYD'),
 q('What is the past form of "EAT"?','ATE','EATED'), q('What is the past form of "SEE"?','SAW','SEED'),
 q('What is the past form of "TAKE"?','TOOK','TAKED'), q('What is the past form of "WRITE"?','WROTE','WRITED'),
 q('What is the past form of "STUDY"?','STUDIED','STUDYED'), q('What is the past form of "BUY"?','BOUGHT','BUYED'),
 q('What is the past form of "WASH"?','WASHED','WASHT'), q('What is the past form of "DRINK"?','DRANK','DRINKED'),
 q('What is the past form of "MAKE"?','MADE','MAKED'), q('What is the past form of "GET"?','GOT','GETED'),
 q('What is the past form of "HAVE"?','HAD','HAVED'), q('What is the base form of "BEGAN"?','BEGIN','BEGAIN'),
 q('What is the base form of "SPOKE"?','SPEAK','SPEEK'), q('What is the base form of "RAN"?','RUN','REN'),
 q('What is the base form of "GAVE"?','GIVE','GAVEN'), q('What is the base form of "CAME"?','COME','CAM'),
 q('She ____ to school yesterday.','WENT','GO','A'), q('They ____ football last Sunday.','PLAYED','PLAY'),
 q('I ____ a new bike last week.','BOUGHT','BUY'), q('He ____ a letter to his friend.','WROTE','WRITE'),
 q('We ____ the museum yesterday.','VISITED','VISIT'), q('Yesterday, I ____ the window.','OPENED','OPEN'),
 q('Which verb is REGULAR?','WORK','COME'), q('Which verb is REGULAR?','CLEAN','DRINK'),
 q('Which verb is IRREGULAR?','MAKE','OPEN'), q('Which verb is IRREGULAR?','HAVE','HELP'),
 q('Which verb is IRREGULAR?','EAT','CALL'), q('Which verb is REGULAR?','WATCH','TAKE')
];

/* ============ PENGATURAN (default) ============ */
const DEF={n:20,t:10,snd:true,cam:true,demo:false,rnd:true};
let S={...DEF};
const HOLD=800,GRACE=1200,$=id=>document.getElementById(id),st=$('stage');
let cur='start',G={};
function show(id){cur=id;document.querySelectorAll('.screen').forEach(e=>e.classList.toggle('on',e.id==id))}
function shuffle(a){for(let i=a.length-1;i>0;i--){const j=Math.random()*(i+1)|0;[a[i],a[j]]=[a[j],a[i]]}return a}

/* ============ SUARA (Web Audio, tanpa file) ============ */
let AC;
function tone(f,d=.15,t='sine',at=0,v=.15){if(!S.snd)return;try{AC=AC||new(window.AudioContext||window.webkitAudioContext)();const o=AC.createOscillator(),g=AC.createGain(),T=AC.currentTime+at;o.type=t;o.frequency.value=f;g.gain.setValueAtTime(v,T);g.gain.exponentialRampToValueAtTime(.001,T+d);o.connect(g).connect(AC.destination);o.start(T);o.stop(T+d)}catch(e){}}
const SFX={start:()=>[392,523,659,784].forEach((f,i)=>tone(f,.15,'square',i*.1)),tick:()=>tone(880,.08,'square'),
 ok:()=>[523,659,784].forEach((f,i)=>tone(f,.2,'triangle',i*.09)),bad:()=>{tone(200,.3,'sawtooth');tone(150,.35,'sawtooth',.15)},
 time:()=>[440,330,220].forEach((f,i)=>tone(f,.2,'square',i*.15)),combo:()=>[784,988,1175,1568].forEach((f,i)=>tone(f,.1,'triangle',.3+i*.07)),
 end:()=>[523,659,784,1047,784,1047].forEach((f,i)=>tone(f,.22,'triangle',i*.12))};

/* ============ CONFETTI ============ */
const fx=$('fx'),cx=fx.getContext('2d');let P=[];
function confetti(){for(let i=0;i<110;i++)P.push({x:fx.width/2,y:fx.height*.6,vx:(Math.random()-.5)*26,vy:-Math.random()*24-6,s:Math.random()*12+6,c:`hsl(${Math.random()*360},90%,60%)`,r:Math.random()*6})}
(function loop(){cx.clearRect(0,0,fx.width,fx.height);P=P.filter(p=>p.y<fx.height+30);P.forEach(p=>{p.x+=p.vx;p.y+=p.vy;p.vy+=.7;p.r+=.2;cx.fillStyle=p.c;cx.save();cx.translate(p.x,p.y);cx.rotate(p.r);cx.fillRect(-p.s/2,-p.s/4,p.s,p.s/2);cx.restore()});requestAnimationFrame(loop)})();
function resize(){st.style.fontSize=st.clientWidth/100+'px';fx.width=st.clientWidth;fx.height=st.clientHeight}
addEventListener('resize',resize);resize();

/* ============ KAMERA + POSE (MediaPipe) ============ */
let stream=null,pos=null,lastSeen=0,camOK=false,poseReady=false;
const loadScript=u=>new Promise((r,j)=>{const s=document.createElement('script');s.src=u;s.crossOrigin='anonymous';s.onload=r;s.onerror=j;document.head.appendChild(s)});
async function initCam(){
 if(camOK)return true;
 try{stream=await navigator.mediaDevices.getUserMedia({video:{width:640,height:480,facingMode:'user'},audio:false})}catch(e){return 'denied'}
 ['src','camVid','pipVid'].forEach(i=>{$(i).srcObject=stream;$(i).play().catch(()=>{})});
 try{
  const B='https://cdn.jsdelivr.net/npm/@mediapipe/pose@0.5.1675469404/';
  await loadScript(B+'pose.js');
  const pose=new Pose({locateFile:f=>B+f});
  pose.setOptions({modelComplexity:0,smoothLandmarks:true,minDetectionConfidence:.5,minTrackingConfidence:.5});
  pose.onResults(onPose);
  (async function feed(){const v=$('src');if(v.readyState>=2){try{await pose.send({image:v})}catch(e){}}requestAnimationFrame(feed)})();
 }catch(e){return 'nopose'}
 camOK=true;return true;
}
/* Titik acuan: rata-rata bahu + pinggul (lebih stabil dari kepala). Cadangan: hidung. x dibalik (mirror). */
function onPose(r){
 const L=r.poseLandmarks,now=Date.now();
 if(!L){if(now-lastSeen>800)pos=null;return}
 const p=[11,12,23,24].map(i=>L[i]).filter(p=>p&&p.visibility>.4);
 let x;
 if(p.length>=2)x=p.reduce((a,b)=>a+b.x,0)/p.length;else if(L[0]&&L[0].visibility>.5)x=L[0].x;else{if(now-lastSeen>800)pos=null;return}
 x=1-x;pos=pos==null?x:pos*.6+x*.4;lastSeen=now; // smoothing anti-goyang
}
const demoActive=()=>S.demo||!S.cam||!camOK;
const zoneOf=p=>p==null?null:p<.4?'L':p>.6?'R':'C'; // 40% / 60%

/* ============ ALUR GAME ============ */
function buildQs(){let a=questions.map(x=>({...x}));if(S.rnd)shuffle(a);a=a.slice(0,Math.min(S.n,a.length));
 return a.map(x=>{if(Math.random()<.5){[x.answerA,x.answerB]=[x.answerB,x.answerA];x.correct=x.correct=='A'?'B':'A'}return x})} // acak sisi jawaban benar
function startGame(){G={qs:buildQs(),i:-1,score:0,combo:0,ok:0,locked:true};show('game');SFX.start();setTimeout(next,600)}
function next(){
 if(cur!='game')return;G.i++;if(G.i>=G.qs.length)return finish();
 const x=G.qs[G.i];G.locked=false;G.t0=Date.now();G.hz=null;G.lt=-1;
 $('qn').textContent=`Q ${String(G.i+1).padStart(2,'0')}/${String(G.qs.length).padStart(2,'0')}`;
 $('sc').textContent='SCORE '+String(G.score).padStart(3,'0');$('cb').textContent=G.combo>=2?'🔥 COMBO x'+G.combo:'';
 $('qt').textContent=x.question;$('ta').textContent='A. '+x.answerA;$('tb').textContent='B. '+x.answerB;
 $('pA').className='pan A';$('pB').className='pan B';$('fb').className='';$('pb').style.width='100%';$('tm').textContent=S.t;$('tm').className='tm tm';
}
function lock(z,timeout){
 if(G.locked)return;G.locked=true; // jawaban hanya terkunci 1x
 const x=G.qs[G.i],c=x.correct=='A'?'L':'R',good=!timeout&&z==c;
 $('pA').classList.add(c=='L'?'win':'dim');$('pB').classList.add(c=='R'?'win':'dim');$('hA').style.width=$('hB').style.width=0;
 if(good){G.combo++;G.ok++;G.score+=100;$('sc').textContent='SCORE '+String(G.score).padStart(3,'0');SFX.ok();if(G.combo>=2)SFX.combo();confetti();
  fbk('🎉 CORRECT!','+100'+(G.combo>=2?'   🔥 COMBO x'+G.combo:''),'#2ee59d')}
 else{G.combo=0;timeout?SFX.time():SFX.bad();st.classList.add('shake');setTimeout(()=>st.classList.remove('shake'),500);
  fbk(timeout?"⏰ TIME'S UP!":'❌ WRONG!','Answer: '+(c=='L'?x.answerA:x.answerB),'#ff5470')}
 setTimeout(next,2400);
}
function fbk(t,s,c){$('fbT').textContent=t;$('fbT').style.color=c;$('fbS').textContent=s;$('fb').className='on'}
function finish(){
 const n=G.qs.length,a=Math.round(G.ok/n*100);show('result');
 $('rs').textContent=G.score.toLocaleString('en-US');
 $('rc').innerHTML=`CORRECT: ${G.ok}/${n} &nbsp;•&nbsp; WRONG: ${n-G.ok}/${n} &nbsp;•&nbsp; ACCURACY: ${a}%`;
 $('rf').textContent=a>=90?'🏆 VERB MASTER!':a>=75?'🌟 GREAT JOB!':a>=60?'👍 GOOD TRY!':'💪 KEEP PRACTICING!';
 SFX.end();if(a>=60)[0,500,1000].forEach(t=>setTimeout(confetti,t));
}
/* Loop utama 50ms: timer + penguncian jawaban */
setInterval(()=>{
 if(cur!='game'||G.locked)return;
 const el=(Date.now()-G.t0)/1000,left=S.t-el;
 if(left<=0)return lock(null,true);
 const sec=Math.ceil(left);$('tm').textContent=sec;$('pb').style.width=left/S.t*100+'%';
 if(sec<=3){$('tm').className='tm low';if(G.lt!=sec){G.lt=sec;SFX.tick()}}
 if(demoActive()||el*1000<GRACE){G.hz=null;return}
 const z=zoneOf(pos);
 if(z&&z!='C'){if(G.hz!=z){G.hz=z;G.hs=Date.now()}
  const h=(Date.now()-G.hs)/HOLD;$('h'+(z=='L'?'A':'B')).style.width=Math.min(h,1)*100+'%';$('h'+(z=='L'?'B':'A')).style.width=0;
  if(h>=1)lock(z)}
 else{G.hz=null;$('hA').style.width=$('hB').style.width=0}
},50);
addEventListener('keydown',e=>{if(cur=='game'&&demoActive()&&!G.locked&&(Date.now()-G.t0)>300){if(e.key=='ArrowLeft')lock('L');if(e.key=='ArrowRight')lock('R')}});

/* ============ UI REALTIME (label, marker, status) ============ */
(function ui(){
 const z=zoneOf(pos),m=(pos==null?.5:pos)*100+'%';
 $('mk').style.left=m;$('mk2').style.left=m;
 if(cur=='cam')$('zlabel').textContent={L:'⬅️ LEFT',R:'RIGHT ➡️',C:'⬆️ CENTER'}[z]||'🔴 PLAYER NOT DETECTED';
 if(cur=='game'){
  const d=demoActive();
  $('trk').textContent=d?'⌨️ DEMO MODE (← →)':pos==null?'🔴 PLAYER NOT DETECTED':'🟢 TRACKING';
  $('warn').textContent=!d&&pos==null?'Please stand in front of the camera.':'';
  $('mv').textContent=G.locked?'':d?'Press ⬅️ or ➡️':(Date.now()-G.t0<GRACE)?'Get ready… stay in the CENTER':z=='L'?'MOVE LEFT! ⬅️':z=='R'?'MOVE RIGHT! ➡️':'';
 }
 requestAnimationFrame(ui);
})();

/* ============ TOMBOL & MENU ============ */
const modal=(id,on)=>$(id).classList.toggle('on',on);
function syncChips(){$('cQ').textContent=Math.min(S.n,questions.length);$('cT').textContent=S.t;$('snd').textContent=S.snd?'🔊 SOUND ON':'🔇 SOUND OFF'}
async function beginFlow(){
 if(S.demo||!S.cam){startGame();return}
 const r=await initCam();
 if(r!==true){$('ncMsg').textContent=r=='denied'?'Camera access is required for movement-based gameplay.':'Pose detection could not load (internet needed). Use Demo Mode instead.';modal('nocam',true);return}
 show('cam')}
$('bStart').onclick=()=>{SFX.start();beginFlow()};
$('bHow').onclick=()=>modal('how',true);$('bHowOk').onclick=()=>{modal('how',false);beginFlow()};
$('bGo').onclick=startGame;$('bBack1').onclick=()=>show('start');
$('bDemo').onclick=()=>{S.demo=true;$('sD').checked=true;modal('nocam',false);startGame()};
$('bRetry').onclick=()=>{modal('nocam',false);beginFlow()};
$('bAgain').onclick=startGame;$('bMenu').onclick=()=>show('start');
$('snd').onclick=()=>{S.snd=!S.snd;$('sS').checked=S.snd;syncChips()};
$('gear').onclick=()=>modal('set',true);
$('bSetOk').onclick=()=>{S.n=+$('sN').value;S.t=+$('sT').value;S.snd=$('sS').checked;S.cam=$('sC').checked;S.demo=$('sD').checked;S.rnd=$('sR').checked;syncChips();modal('set',false)};
$('bReset').onclick=()=>{S={...DEF};G={locked:true};$('sN').value=20;$('sT').value=10;$('sS').checked=$('sC').checked=$('sR').checked=true;$('sD').checked=false;syncChips();modal('set',false);show('start')};
syncChips();
</script></body></html>
