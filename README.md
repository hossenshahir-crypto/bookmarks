# bookmarks
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>🔖 Bookmarklet Hub — Offline Games</title>
<style>
:root{--bg:#071026;--panel:#0e1724;--accent:#1f9fff;--muted:#9fb4d6}
html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,Arial;color:#e6eef8;background:linear-gradient(180deg,#050814,#071026);display:flex;justify-content:center;padding:28px}
.container{width:960px;max-width:96%}
header{background:linear-gradient(90deg,rgba(31,159,255,0.12),rgba(31,159,255,0.04));border-radius:12px;padding:18px 22px;margin-bottom:18px;display:flex;align-items:center;justify-content:space-between}
header h1{margin:0;font-size:1.4rem}
header .sub{color:var(--muted);font-size:0.9rem}
.table{display:flex;flex-direction:column;gap:12px}
.row{display:flex;align-items:center;justify-content:space-between;background:var(--panel);padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.02)}
.desc{flex:1;padding-right:18px;color:#dbeafe}
.desc .title{font-weight:700;margin-bottom:6px}
.desc .note{color:var(--muted);font-size:0.92rem}
.btn{background:var(--accent);color:#012026;padding:10px 16px;border-radius:10px;font-weight:800;text-decoration:none;display:inline-block;cursor:grab;min-width:160px;text-align:center;box-shadow:0 8px 18px rgba(31,159,255,0.08)}
.btn:hover{filter:brightness(1.06)}
.yt{display:inline-block;margin-top:18px;padding:10px 14px;border-radius:10px;background:#ff3b3b;color:white;text-decoration:none;font-weight:800}
footer{color:var(--muted);text-align:center;margin-top:18px;font-size:0.85rem}
.overlay{position:fixed;inset:0;background:rgba(0,0,0,0.85);z-index:2147483646;display:flex;align-items:center;justify-content:center;padding:18px}
.panel{background:#081124;border-radius:12px;width:900px;max-width:96%;height:680px;max-height:96%;display:flex;flex-direction:column;padding:12px;box-shadow:0 10px 40px rgba(0,0,0,0.6)}
.controls{display:flex;gap:8px;align-items:center}
.tablist{display:flex;gap:8px;margin-top:8px}
.small{padding:6px 10px;border-radius:8px;background:#1f9fff;border:0;color:#012;font-weight:800;cursor:pointer}
.closeBtn{background:#ef4444;border:0;padding:6px 10px;border-radius:8px;color:white;cursor:pointer}
.iframeWrap{flex:1;border-radius:8px;overflow:hidden;background:#000}
.iframeWrap iframe{width:100%;height:100%;border:0}
.gameArea{flex:1;display:flex;align-items:center;justify-content:center;overflow:auto;background:#0e1724;border-radius:8px;padding:12px}
canvas{background:#012;border-radius:8px}
kbd{background:#0b1220;padding:4px 6px;border-radius:4px;border:1px solid rgba(255,255,255,0.04)}
</style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>🔖 Bookmarklet Hub</h1>
        <div class="sub">All-in-one — drag the blue buttons to your bookmarks bar</div>
      </div>
      <div style="text-align:right">
        <div style="font-weight:700">Tools & Games</div>
        <div style="color:var(--muted);font-size:0.9rem">Safe demos + offline games</div>
      </div>
    </header>

    <div class="table" id="table"></div>

    <div style="text-align:center">
      <a class="yt" href="https://www.youtube.com/@cursedgamer2?sub_confirmation=1" target="_blank" rel="noopener">▶️ Sub to my YT channel</a>
    </div>

    <footer>Drag a button to your bookmarks bar to save the bookmarklet. History demo limited to avoid harm.</footer>
  </div>

<script>
/* Build draggable bookmarklet anchors from function sources to avoid quoting issues */
function makeBookmarkletHref(fn){
  var code = '(' + fn.toString() + ')();';
  return 'javascript:' + encodeURIComponent(code);
}
function addRow(emoji, title, note, fn, label){
  var table = document.getElementById('table');
  var row = document.createElement('div'); row.className='row';
  var desc = document.createElement('div'); desc.className='desc';
  var t=document.createElement('div'); t.className='title'; t.textContent = emoji+' '+title;
  var n=document.createElement('div'); n.className='note'; n.textContent = note || '';
  desc.appendChild(t); desc.appendChild(n);
  var wrapper=document.createElement('div'); wrapper.style='flex:0 0 auto';
  var a=document.createElement('a'); a.className='btn'; a.textContent = label||('Drag: '+title);
  a.href = makeBookmarkletHref(fn);
  a.title='Drag to bookmarks bar';
  a.draggable = true;
  a.addEventListener('dragstart', function(e){
    try{ e.dataTransfer.setData('text/uri-list', a.href); }catch(e){}
    try{ e.dataTransfer.setData('text/plain', a.href); }catch(e){}
    e.dataTransfer.effectAllowed='copy';
  });
  wrapper.appendChild(a);
  row.appendChild(desc);
  row.appendChild(wrapper);
  table.appendChild(row);
}

/* ---------------- Bookmarklet functions ---------------- */

/* Edit: toggle page editable */
function bm_edit(){
  document.designMode = document.designMode === 'on' ? 'off' : 'on';
  document.body.contentEditable = document.designMode === 'on';
  alert('Edit mode: '+document.designMode+' — reload to restore.');
}

/* Dev console overlay */
function bm_devConsole(){
  if(document.getElementById('__bm_devconsole')){ document.getElementById('__bm_devconsole').remove(); return; }
  var w=document.createElement('div'); w.id='__bm_devconsole'; w.style='position:fixed;right:18px;bottom:18px;width:480px;height:320px;background:rgba(3,6,12,0.96);color:#e6eef8;border-radius:10px;padding:8px;z-index:2147483647;display:flex;flex-direction:column;font-family:monospace';
  w.innerHTML='<div style="display:flex;justify-content:space-between"><strong>Mini Console</strong><button id="__bm_dc_close" style="background:transparent;border:0;color:white;cursor:pointer">✕</button></div><pre id="__bm_dc_out" style="flex:1;margin:8px 0;padding:8px;overflow:auto;background:rgba(0,0,0,0.4);border-radius:6px">Console ready.\\n</pre><div style="display:flex;gap:8px"><input id="__bm_dc_in" placeholder="Type JS and press Enter" style="flex:1;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:white"><button id="__bm_dc_run" style="background:#1f9fff;border:0;padding:8px 12px;border-radius:6px;color:#012;cursor:pointer">Run</button></div>';
  document.body.appendChild(w);
  var out=document.getElementById('__bm_dc_out'), inp=document.getElementById('__bm_dc_in');
  document.getElementById('__bm_dc_run').onclick = function(){ try{ var res = eval(inp.value); out.textContent += '> '+inp.value+'\\n'+String(res)+'\\n'; }catch(e){ out.textContent += 'Error: '+e+'\\n'; } inp.value=''; out.scrollTop = out.scrollHeight; };
  document.getElementById('__bm_dc_close').onclick = function(){ w.remove(); };
  inp.addEventListener('keydown', function(e){ if(e.key==='Enter') document.getElementById('__bm_dc_run').click(); });
}

/* Mini Browser: prompt then overlay (or new tab) */
function bm_minibrowser(){
  var url = prompt('Enter a website URL (e.g. https://example.com):','https://');
  if(!url) return;
  if(!/^https?:\\/\\//i.test(url)) url = 'https://'+url;
  // overlay
  if(document.getElementById('__bm_minioverlay')) document.getElementById('__bm_minioverlay').remove();
  var ov=document.createElement('div'); ov.id='__bm_minioverlay'; ov.className='overlay';
  ov.innerHTML = '<div class="panel"><div style="display:flex;justify-content:space-between;align-items:center"><strong>Mini Browser</strong><div><button id="__bm_mininew" class="small">Open in new tab</button> <button id="__bm_miniclose" class="closeBtn">Close</button></div></div><div style="margin-top:8px" class="controls"><input id="__bm_minibox" style="flex:1;padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:#e6eef8' + '" value="'+url.replace(/"/g,'&quot;')+'"><button id="__bm_minigo" class="small">Go</button></div><div style="flex:1;margin-top:8px" class="iframeWrap"><iframe id="__bm_miniframe" sandbox="allow-scripts allow-forms allow-same-origin" src="'+url+'"></iframe></div></div>';
  document.body.appendChild(ov);
  document.getElementById('__bm_miniclose').onclick = function(){ ov.remove(); };
  document.getElementById('__bm_minigo').onclick = function(){ var v=document.getElementById('__bm_minibox').value.trim(); if(!/^https?:\\/\\//i.test(v)) v='https://'+v; document.getElementById('__bm_miniframe').src = v; };
  document.getElementById('__bm_minibox').addEventListener('keydown', function(e){ if(e.key==='Enter') document.getElementById('__bm_minigo').click(); });
  document.getElementById('__bm_mininew').onclick = function(){ window.open(document.getElementById('__bm_minibox').value.trim(), '_blank'); };
}

/* Script injector overlay */
function bm_injector(){
  if(document.getElementById('__bm_injector')){ document.getElementById('__bm_injector').remove(); return; }
  var ov=document.createElement('div'); ov.className='overlay'; ov.id='__bm_injector';
  ov.innerHTML = '<div class="panel"><div style="display:flex;justify-content:space-between;align-items:center"><strong>Script Injector</strong><div><button id="__inj_close" class="closeBtn">Close</button></div></div><div style="margin-top:8px;color:#9fb4d6">Paste JS below (trusted only).</div><textarea id="__inj_area" style="width:100%;height:420px;margin-top:8px;background:#00101a;color:#e6eef8;border-radius:8px;border:0;padding:8px;font-family:monospace"></textarea><div style="display:flex;gap:8px;margin-top:8px"><button id="__inj_run" class="small">Inject</button><button id="__inj_save" class="small">Save</button><button id="__inj_load" class="small">Load</button></div></div>';
  document.body.appendChild(ov);
  document.getElementById('__inj_close').onclick = function(){ ov.remove(); };
  document.getElementById('__inj_run').onclick = function(){ try{ (new Function(document.getElementById('__inj_area').value))(); alert('Script executed'); } catch(e){ alert('Injection error: '+e); } };
  document.getElementById('__inj_save').onclick = function(){ localStorage.setItem('__bm_inject_code', document.getElementById('__inj_area').value); alert('Saved'); };
  document.getElementById('__inj_load').onclick = function(){ document.getElementById('__inj_area').value = localStorage.getItem('__bm_inject_code') || ''; alert('Loaded'); };
}

/* Crash visual simulation */
function bm_crash(){
  if(document.getElementById('__bm_crash')){ document.getElementById('__bm_crash').remove(); return; }
  var ov = document.createElement('div'); ov.id='__bm_crash'; ov.className='overlay';
  ov.innerHTML = '<div class="panel" style="max-width:820px;text-align:center"><div style="font-size:22px;font-weight:800">Simulated Crash</div><div style="color:#9fb4d6;margin-top:8px">Harmless visual simulation. Press Restore or Esc.</div><div style="margin-top:18px"><button id="__cr_restore" class="small">Restore</button> <button id="__cr_reload" class="closeBtn">Reload</button></div></div>';
  document.body.appendChild(ov);
  document.getElementById('__cr_restore').onclick = function(){ ov.remove(); };
  document.getElementById('__cr_reload').onclick = function(){ location.reload(); };
  window.addEventListener('keydown', function esc(e){ if(e.key==='Escape'){ ov.remove(); window.removeEventListener('keydown', esc); }});
}

/* History demo (limited) */
function bm_history(){
  var n = parseInt(prompt('How many demo entries to push into this tab (max 200)?','40'),10);
  if(!n || n<1) return;
  n = Math.min(200, n);
  var i=0;
  var id = setInterval(function(){ try{ history.pushState({},'', location.pathname + '#h' + Math.random().toString(36).slice(2,7)); }catch(e){} i++; if(i>=n){ clearInterval(id); alert('Pushed '+n+' demo entries into this tab history (limited).'); } }, 20);
}

/* ---------------- Games Hub: offline self-contained games ---------------- */
function bm_games(){
  if(document.getElementById('__bm_games')){ document.getElementById('__bm_games').remove(); return; }

  // audio helper (simple beeps)
  function makeAudio(){ var ctx = new (window.AudioContext||window.webkitAudioContext)(); function beep(freq,t){ var o=ctx.createOscillator(), g=ctx.createGain(); o.type='sine'; o.frequency.value=f; g.gain.value=0.04; o.connect(g); g.connect(ctx.destination); o.start(); o.stop(ctx.currentTime+t); } return { click:function(){beep(800,0.05)}, pop:function(){beep(520,0.07)}, hit:function(){beep(180,0.08)} }; }
  var audio = makeAudio();

  var ov=document.createElement('div'); ov.id='__bm_games'; ov.className='overlay';
  ov.innerHTML = '<div class="panel"><div style="display:flex;justify-content:space-between;align-items:center"><div><strong>🎮 Games Hub</strong><div style="color:#9fb4d6;font-size:13px">Offline games — 2048, Flappy Bird, Cookie Clicker</div></div><div><button id="__gh_close" class="closeBtn">Close</button></div></div><div class="tablist" id="__gh_tabs"></div><div class="gameArea" id="__gh_area"></div></div>';
  document.body.appendChild(ov);
  document.getElementById('__gh_close').onclick = function(){ ov.remove(); };

  var tabs = document.getElementById('__gh_tabs'), area = document.getElementById('__gh_area');
  function createTab(name,fn){ var b=document.createElement('button'); b.className='small'; b.textContent=name; b.onclick=function(){ audio.click(); area.innerHTML=''; fn(area); }; tabs.appendChild(b); }

  /* ---------- Cookie Clicker (simple offline) ---------- */
  createTab('Cookie Clicker', function(area){
    var wrap=document.createElement('div'); wrap.style='text-align:center;width:100%';
    var cookie=document.createElement('button'); cookie.textContent='🍪'; cookie.style='font-size:64px;padding:24px;border-radius:16px;background:#1f9fff;color:#012;border:none;cursor:pointer;transition:transform .12s';
    var score=0,cps=0; var scoreDisplay=document.createElement('div'); scoreDisplay.style='margin-top:12px;font-size:18px'; scoreDisplay.textContent='Cookies: 0';
    var upBtn=document.createElement('button'); upBtn.textContent='Upgrade (+1 CPS) — Cost 10'; upBtn.style='margin-top:12px;padding:8px 12px;border-radius:8px;border:0;background:#ff9800;color:white;cursor:pointer';
    cookie.onclick=function(){ score++; audio.pop(); cookie.style.transform='scale(1.12)'; setTimeout(()=>cookie.style.transform='',120); scoreDisplay.textContent='Cookies: '+score; };
    upBtn.onclick=function(){ if(score>=10){ score-=10; cps+=1; audio.pop(); scoreDisplay.textContent='Cookies: '+score; } else audio.hit(); };
    wrap.appendChild(cookie); wrap.appendChild(scoreDisplay); wrap.appendChild(upBtn); area.appendChild(wrap);
    var id=setInterval(function(){ score+=cps; scoreDisplay.textContent='Cookies: '+score; },1000);
    // cleanup on close:
    area._cleanup = function(){ clearInterval(id); };
  });

  /* ---------- 2048 (canvas) ---------- */
  createTab('2048', function(area){
    var canvas=document.createElement('canvas'); canvas.width=420; canvas.height=420; area.appendChild(canvas);
    var ctx=canvas.getContext('2d'); var N=4, cell=canvas.width/N; var grid=[];
    for(var r=0;r<N;r++){ grid[r]=[]; for(var c=0;c<N;c++) grid[r][c]=0; }
    function addTile(){ var empt=[]; for(var r=0;r<N;r++) for(var c=0;c<N;c++) if(grid[r][c]===0) empt.push([r,c]); if(!empt.length) return; var p=empt[Math.floor(Math.random()*empt.length)]; grid[p[0]][p[1]] = Math.random()<0.9?2:4; }
    function draw(){ ctx.fillStyle='#012'; ctx.fillRect(0,0,canvas.width,canvas.height); for(var r=0;r<N;r++){ for(var c=0;c<N;c++){ ctx.fillStyle = grid[r][c]===0 ? '#0b1220' : '#1f9fff'; ctx.fillRect(c*cell+8, r*cell+8, cell-16, cell-16); if(grid[r][c]){ ctx.fillStyle='#012'; ctx.font='bold '+(cell/3)+'px sans-serif'; ctx.textAlign='center'; ctx.textBaseline='middle'; ctx.fillText(grid[r][c], c*cell+cell/2, r*cell+cell/2); }}} }
    function slideRow(row){ row = row.filter(v=>v!==0); for(var i=0;i<row.length-1;i++){ if(row[i]===row[i+1]){ row[i]*=2; row[i+1]=0; audio.pop(); } } row = row.filter(v=>v!==0); while(row.length<N) row.push(0); return row; }
    function move(dir){ var moved=false;
      if(dir==='left'){ for(var r=0;r<N;r++){ var row=grid[r].slice(); var sl=slideRow(row); for(var c=0;c<N;c++){ if(grid[r][c]!==sl[c]) moved=true; grid[r][c]=sl[c]; } } }
      else if(dir==='right'){ for(var r=0;r<N;r++){ var row=grid[r].slice().reverse(); var sl=slideRow(row); sl.reverse(); for(var c=0;c<N;c++){ if(grid[r][c]!==sl[c]) moved=true; grid[r][c]=sl[c]; } } }
      else if(dir==='up'){ for(var c=0;c<N;c++){ var col=[]; for(var r=0;r<N;r++) col.push(grid[r][c]); var sl=slideRow(col); for(var r=0;r<N;r++){ if(grid[r][c]!==sl[r]) moved=true; grid[r][c]=sl[r]; } } }
      else if(dir==='down'){ for(var c=0;c<N;c++){ var col=[]; for(var r=N-1;r>=0;r--) col.push(grid[r][c]); var sl=slideRow(col); sl.reverse(); for(var r=0;r<N;r++){ if(grid[r][c]!==sl[r]) moved=true; grid[r][c]=sl[r]; } } }
      if(moved){ addTile(); draw(); }
    }
    addTile(); addTile(); draw();
    function keyHandler(e){ var map={ArrowLeft:'left',ArrowRight:'right',ArrowUp:'up',ArrowDown:'down'}; if(map[e.key]){ e.preventDefault(); move(map[e.key]); } }
    window.addEventListener('keydown', keyHandler);
    area._cleanup = function(){ window.removeEventListener('keydown', keyHandler); try{ canvas.remove(); }catch(e){} };
  });

  /* ---------- Flappy Bird (canvas) ---------- */
  createTab('Flappy Bird', function(area){
    var canvas=document.createElement('canvas'); canvas.width=420; canvas.height=420; area.appendChild(canvas);
    var ctx=canvas.getContext('2d'); var bird={x:60,y:200,vy:0,w:20,h:16}; var gravity=0.6, flap=-10; var pipes=[], frame=0, score=0, running=true;
    function spawn(){ pipes.push({x:canvas.width, top:60 + Math.random()*180, gap:110}); }
    function loop(){
      if(!running) return;
      ctx.fillStyle='#012'; ctx.fillRect(0,0,canvas.width,canvas.height);
      bird.vy += gravity; bird.y += bird.vy; ctx.fillStyle='yellow'; ctx.fillRect(bird.x,bird.y,bird.w,bird.h);
      if(frame % 90 === 0) spawn();
      for(var i=pipes.length-1;i>=0;i--){ pipes[i].x -= 3; ctx.fillStyle='green'; ctx.fillRect(pipes[i].x,0,38,pipes[i].top); ctx.fillRect(pipes[i].x,pipes[i].top+pipes[i].gap,38,canvas.height-pipes[i].top-pipes[i].gap);
        if(bird.x + bird.w > pipes[i].x && bird.x < pipes[i].x + 38 && (bird.y < pipes[i].top || bird.y + bird.h > pipes[i].top + pipes[i].gap)){ audio.hit(); running=false; setTimeout(()=>alert('Game Over! Score: '+score),10); return; }
        if(pipes[i].x + 38 < 0){ pipes.splice(i,1); score++; audio.pop(); }
      }
      if(bird.y > canvas.height || bird.y < 0){ audio.hit(); running=false; setTimeout(()=>alert('Game Over! Score: '+score),10); return; }
      ctx.fillStyle='#fff'; ctx.fillText('Score: '+score, 10, 20); frame++; requestAnimationFrame(loop);
    }
    function keyHandler(e){ if(e.key===' '){ bird.vy = flap; audio.click(); } }
    window.addEventListener('keydown', keyHandler);
    loop();
    area._cleanup = function(){ window.removeEventListener('keydown', keyHandler); running=false; try{ canvas.remove(); }catch(e){} };
  });

  // When closing overlay, call cleanup functions if present
  var closeBtn = document.getElementById('__gh_close');
  closeBtn.onclick = function(){ 
    // run cleanup on the area if defined
    try{ if(area._cleanup) area._cleanup(); } catch(e) {}
    ov.remove(); 
  };
}

/* ---------- Add rows to page ---------- */
addRow('✏️','Edit Page','Toggle editable mode on any page (reload to restore).', bm_edit, 'Drag: Edit Page');
addRow('💻','Dev Console','Open a mini in-page JS console.', bm_devConsole, 'Drag: Dev Console');
addRow('🌐','Mini Browser','Prompt for URL then open mini overlay (or new tab).', bm_minibrowser, 'Drag: Mini Browser');
addRow('🧩','Script Injector','Paste JS into overlay and run (trusted only).', bm_injector, 'Drag: Script Injector');
addRow('🎮','Games Hub','Open offline games overlay (2048, Flappy, Cookie).', bm_games, 'Drag: Games Hub');
addRow('⚡','Simulate Crash','Safe visual crash simulation — press Restore.', bm_crash, 'Drag: Simulate Crash');
addRow('🕒','History Tool','Push demo entries into this tab history (limited).', bm_history, 'Drag: History Tool');

</script>
</body>
</html>
