# bookmarks
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>🔖 Bookmarklet Hub — Fixed</title>
<style>
  :root{--bg:#071026;--panel:#0e1724;--accent:#1f9fff;--muted:#9fb4d6}
  html,body{height:100%;margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial;color:#e6eef8;background:linear-gradient(180deg,#050814,#071026);display:flex;justify-content:center;padding:36px}
  .container{width:920px;max-width:96%}
  header{background:linear-gradient(90deg,rgba(31,159,255,0.12),rgba(31,159,255,0.04));border-radius:12px;padding:18px 22px;margin-bottom:20px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 8px 30px rgba(3,6,23,0.6)}
  header h1{margin:0;font-size:1.4rem}
  header .sub{color:var(--muted);font-size:0.9rem}
  .table{display:flex;flex-direction:column;gap:12px}
  .row{display:flex;align-items:center;justify-content:space-between;background:var(--panel);padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.02)}
  .desc{flex:1;padding-right:18px;color:#dbeafe}
  .desc .title{font-weight:700;margin-bottom:6px}
  .desc .note{color:var(--muted);font-size:0.92rem}
  .btn{background:var(--accent);color:#012026;padding:10px 16px;border-radius:10px;font-weight:800;text-decoration:none;display:inline-block;cursor:grab;min-width:160px;text-align:center;box-shadow:0 8px 18px rgba(31,159,255,0.08)}
  .btn:hover{filter:brightness(1.06)}
  .yt{display:inline-block;margin-top:18px;padding:10px 14px;border-radius:10px;background:#ff3b3b;color:white;text-decoration:none;font-weight:800;box-shadow:0 8px 18px rgba(255,59,59,0.08)}
  footer{color:var(--muted);text-align:center;margin-top:18px;font-size:0.85rem}
</style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>🔖 Bookmarklet Hub</h1>
        <div class="sub">Drag the blue buttons to your bookmarks bar</div>
      </div>
      <div style="text-align:right">
        <div style="font-weight:700">Your Tools</div>
        <div style="color:var(--muted);font-size:0.9rem">Safe demos & utilities</div>
      </div>
    </header>

    <div class="table" id="table"></div>

    <div style="text-align:center">
      <a class="yt" href="https://www.youtube.com/@cursedgamer2?sub_confirmation=1" target="_blank" rel="noopener">▶️ Sub to my YT channel</a>
    </div>

    <footer>Drag a button to your bookmarks bar to save the tool.</footer>
  </div>

<script>
/* Robust builder: wait for DOM, create bookmarklets from function sources (avoids escaping/template issues) */
document.addEventListener('DOMContentLoaded', function(){

  function makeBookmarkletHref(fn){
    // Wrap function source in an IIFE and URI-encode
    var code = '(' + fn.toString() + ')();';
    return 'javascript:' + encodeURIComponent(code);
  }

  function addRow(titleEmoji, titleText, noteText, fn, buttonLabel){
    var table = document.getElementById('table');
    var row = document.createElement('div'); row.className = 'row';
    var desc = document.createElement('div'); desc.className = 'desc';
    var t = document.createElement('div'); t.className = 'title'; t.textContent = titleEmoji + ' ' + titleText;
    var n = document.createElement('div'); n.className = 'note'; n.textContent = noteText || '';
    desc.appendChild(t); desc.appendChild(n);

    var wrapper = document.createElement('div'); wrapper.style = 'flex:0 0 auto';
    var a = document.createElement('a'); a.className = 'btn';
    a.textContent = buttonLabel || ('Drag: ' + titleText);
    a.href = makeBookmarkletHref(fn);
    a.setAttribute('title','Drag this to your bookmarks bar');
    a.setAttribute('draggable','false');
    wrapper.appendChild(a);

    row.appendChild(desc);
    row.appendChild(wrapper);
    table.appendChild(row);
  }

  /* ----------------- Bookmarklet functions ----------------- */

  function bm_edit(){
    document.designMode = document.designMode === 'on' ? 'off' : 'on';
    document.body.contentEditable = document.designMode === 'on';
    alert('Edit mode: ' + document.designMode + '\nClick any text to edit. Reload to restore.');
  }

  function bm_devConsole(){
    if (window.__bm_devconsole_open){
      var old = document.getElementById('__bm_devconsole'); if (old) old.remove(); window.__bm_devconsole_open = false; return;
    }
    window.__bm_devconsole_open = true;
    var w = document.createElement('div');
    w.id = '__bm_devconsole';
    w.style = 'position:fixed;right:18px;bottom:18px;width:420px;height:280px;background:rgba(3,6,12,0.96);color:#e6eef8;border-radius:10px;padding:8px;z-index:2147483646;display:flex;flex-direction:column;';
    var t = document.createElement('div'); t.style='display:flex;justify-content:space-between;align-items:center;padding:6px;';
    var ti = document.createElement('div'); ti.textContent='Mini Console'; ti.style.fontWeight='700';
    var btns = document.createElement('div'); var clearBtn = document.createElement('button'); clearBtn.textContent='Clear'; clearBtn.style='margin-right:6px;background:transparent;color:white;border:0;cursor:pointer;';
    var closeBtn = document.createElement('button'); closeBtn.textContent='✕'; closeBtn.style='background:transparent;color:white;border:0;cursor:pointer;';
    btns.appendChild(clearBtn); btns.appendChild(closeBtn);
    t.appendChild(ti); t.appendChild(btns);
    var out = document.createElement('pre'); out.style='flex:1;margin:6px 0;padding:8px;overflow:auto;background:rgba(0,0,0,0.4);border-radius:6px;'; out.textContent='Console ready.\n';
    var inputWrap = document.createElement('div'); inputWrap.style='display:flex;gap:8px;';
    var inp = document.createElement('input'); inp.placeholder='Type JS and press Enter →'; inp.style='flex:1;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:white;outline:none;';
    var run = document.createElement('button'); run.textContent='Run'; run.style='padding:8px;border-radius:6px;border:0;background:#1f9fff;color:#012;font-weight:700;cursor:pointer;';
    inputWrap.appendChild(inp); inputWrap.appendChild(run);
    w.appendChild(t); w.appendChild(out); w.appendChild(inputWrap);
    document.body.appendChild(w);
    function log(v){ try { out.textContent += v + '\n'; out.scrollTop = out.scrollHeight; } catch(e) {} }
    run.onclick = function(){ try { var res = eval(inp.value); log('> '+inp.value); log(res); } catch(e) { log('Error:'+e); } inp.value=''; };
    inp.addEventListener('keydown', function(e){ if (e.key === 'Enter') run.onclick(); });
    clearBtn.onclick = function(){ out.textContent = 'Console cleared.\n'; };
    closeBtn.onclick = function(){ w.remove(); window.__bm_devconsole_open = false; };
  }

  function bm_mini(){
    var w = window.open('', '__bm_minibrowser', 'width=900,height=600,resizable=yes,scrollbars=yes');
    if (!w) { alert('Popup blocked — allow popups for this site.'); return; }
    // small safe mini-browser UI
    w.document.write('<!doctype html><html><meta charset="utf-8"><title>Mini Browser</title><style>body{margin:0;font-family:sans-serif;background:#0b1220;color:white}#bar{display:flex;padding:8px;gap:8px}input{flex:1;padding:8px;border-radius:6px;border:0}button{padding:8px;border-radius:6px;border:0;background:#1f9fff;color:#012}</style><div id="bar"><input id="u" placeholder="https://example.com"><button id="g">Go</button></div><iframe id="f" src="about:blank" style="width:100%;height:calc(100vh - 48px);border:0"></iframe><script>const i=document.getElementById("u"),btn=document.getElementById("g"),frame=document.getElementById("f");function nav(){let v=i.value.trim();if(!/^https?:\\/\\//.test(v))v="https://"+v;frame.src=v;}btn.onclick=nav;i.addEventListener("keydown",e=>{if(e.key==="Enter")nav();});</'+'script></html>');
  }

  function bm_injector(){
    if (document.getElementById('__bm_injector_overlay')){ document.getElementById('__bm_injector_overlay').remove(); return; }
    var overlay = document.createElement('div'); overlay.id='__bm_injector_overlay'; overlay.style='position:fixed;inset:0;background:rgba(0,0,0,0.85);z-index:2147483647;display:flex;align-items:center;justify-content:center';
    var box = document.createElement('div'); box.style='width:760px;max-width:96%;background:#071026;padding:12px;border-radius:10px;color:#e6eef8;font-family:monospace';
    box.innerHTML = '<div style="display:flex;justify-content:space-between;align-items:center"><strong>Script Injector</strong><button id="__inj_close" style="background:#ef4444;border:0;padding:6px 10px;border-radius:8px;color:white;cursor:pointer">Close</button></div><div style="margin-top:8px;color:#9fb4d6;font-size:13px">Paste JS below and press Inject (trusted only).</div>';
    var ta = document.createElement('textarea'); ta.style='width:100%;height:300px;margin-top:8px;background:#00101a;color:#e6eef8;border-radius:8px;border:0;padding:8px;font-family:monospace';
    var controls = document.createElement('div'); controls.style='margin-top:8px;display:flex;gap:8px';
    var run = document.createElement('button'); run.textContent='Inject'; run.style='padding:8px 12px;border-radius:8px;border:0;background:#1f9fff;color:#012;font-weight:800;cursor:pointer';
    var save = document.createElement('button'); save.textContent='Save'; save.style='padding:8px 12px;border-radius:8px;border:0;background:#1572e8;color:white;cursor:pointer';
    var load = document.createElement('button'); load.textContent='Load Saved'; load.style='padding:8px 12px;border-radius:8px;border:0;background:#64748b;color:white;cursor:pointer';
    controls.appendChild(run); controls.appendChild(save); controls.appendChild(load);
    box.appendChild(ta); box.appendChild(controls); overlay.appendChild(box); document.body.appendChild(overlay);
    document.getElementById('__inj_close').onclick = function(){ overlay.remove(); };
    run.onclick = function(){ try{ (new Function(ta.value))(); alert('Script executed'); } catch(e){ alert('Injection error: '+e); } };
    save.onclick = function(){ localStorage.setItem('__bm_saved_inject', ta.value); alert('Saved'); };
    load.onclick = function(){ ta.value = localStorage.getItem('__bm_saved_inject') || ''; alert('Loaded'); };
    ta.value = '';
  }

  function bm_crash(){
    // visual-only crash
    if (document.getElementById('__bm_sim_crash')){ document.getElementById('__bm_sim_crash').remove(); return; }
    var o = document.createElement('div'); o.id='__bm_sim_crash'; o.style='position:fixed;inset:0;z-index:2147483647;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,#000,#0b0b0b);color:white;font-family:system-ui;padding:20px';
    o.innerHTML = '<div style="max-width:900px;text-align:center;padding:28px;border-radius:12px;backdrop-filter:blur(3px)"><div style="font-size:28px;font-weight:800;margin-bottom:10px">Aw, snap — the site became unresponsive</div><div style="color:#d1d5db;margin-bottom:16px">This is a safe visual simulation only. Press <kbd>Esc</kbd> or the Restore button to close.</div><div style="display:flex;gap:12px;justify-content:center"><div style="width:56px;height:56px;border-radius:50%;border:6px solid rgba(255,255,255,0.06);border-top-color:#1f9fff;animation:__bmspin 1s linear infinite"></div><button id="__bm_restore" style="padding:10px 14px;border-radius:8px;border:0;background:#1f9fff;color:#012;font-weight:700;cursor:pointer">Restore Page</button><button id="__bm_reload" style="padding:10px 14px;border-radius:8px;border:0;background:#ef4444;color:#fff;font-weight:700;cursor:pointer">Reload</button></div></div><style>@keyframes __bmspin{to{transform:rotate(360deg)}}#__bm_sim_crash button:active{transform:scale(.98)}</style>';
    document.body.appendChild(o);
    document.getElementById('__bm_restore').onclick = function(){ var el = document.getElementById('__bm_sim_crash'); if (el) el.remove(); };
    document.getElementById('__bm_reload').onclick = function(){ location.reload(); };
    document.addEventListener('keydown', function esc(e){ if (e.key==='Escape'){ var el=document.getElementById('__bm_sim_crash'); if(el) el.remove(); document.removeEventListener('keydown', esc); }});
  }

  function bm_history(){
    // harmless but functional small flood (limited to 100) — avoids locking the browser
    var n = parseInt(prompt('How many entries to push into this tab (1–100)?','20'),10);
    if (!n || n < 1) { alert('Cancelled'); return; }
    n = Math.min(100, n);
    var i=0;
    var id = setInterval(function(){
      try { history.pushState({},'', location.pathname + '#h' + Math.random().toString(36).slice(2,7)); } catch(e){}
      i++;
      if (i>=n){ clearInterval(id); alert('Pushed '+n+' entries into this tab session history (demo).'); }
    }, 20);
  }

  /* Simple games hub core (opens overlay + simple Snake & Cookie Clicker in overlay) */
  function bm_games(){
    if (document.getElementById('__bm_games_overlay')){ document.getElementById('__bm_games_overlay').remove(); return; }
    // overlay
    var ov = document.createElement('div'); ov.id='__bm_games_overlay'; ov.style='position:fixed;inset:0;background:rgba(0,0,0,0.95);display:flex;align-items:center;justify-content:center;z-index:2147483646;color:white;font-family:sans-serif;';
    var box = document.createElement('div'); box.style='background:#081124;padding:16px;border-radius:12px;width:760px;max-width:96%;height:560px;max-height:96%;display:flex;flex-direction:column;';
    box.innerHTML = '<div style="display:flex;justify-content:space-between;align-items:center"><strong style="font-size:18px">🎮 Games Hub</strong><button id="__gb_close" style="background:#ef4444;color:white;border:none;padding:6px 10px;border-radius:8px;cursor:pointer">Close</button></div><div style="margin-top:8px;display:flex;gap:8px;flex-wrap:wrap"><button id="__gb_snake" style="background:#1f9fff;color:#012;padding:6px 10px;border-radius:8px;border:0;cursor:pointer">Snake</button><button id="__gb_cookie" style="background:#1f9fff;color:#012;padding:6px 10px;border-radius:8px;border:0;cursor:pointer">Cookie Clicker</button></div><div id="__gb_area" style="flex:1;margin-top:10px;display:flex;align-items:center;justify-content:center;background:#0e1724;border-radius:8px;padding:12px"></div>';
    ov.appendChild(box); document.body.appendChild(ov);

    document.getElementById('__gb_close').onclick = function(){ ov.remove(); };

    /* Snake */
    document.getElementById('__gb_snake').onclick = function(){
      var area = document.getElementById('__gb_area'); area.innerHTML=''; 
      var canvas = document.createElement('canvas'); canvas.width=420; canvas.height=420; area.appendChild(canvas);
      var ctx = canvas.getContext('2d'); var scale=20, cols=21, rows=21;
      var snake=[{x:10,y:10}], dir={x:0,y:0}, food={x:5,y:5}, score=0;
      function draw(){ ctx.fillStyle='#012'; ctx.fillRect(0,0,canvas.width,canvas.height); ctx.fillStyle='#1f9fff'; snake.forEach(s=>ctx.fillRect(s.x*scale, s.y*scale, scale-2, scale-2)); ctx.fillStyle='#ff6666'; ctx.fillRect(food.x*scale, food.y*scale, scale-2, scale-2); }
      function step(){
        var head = {x:snake[0].x + dir.x, y:snake[0].y + dir.y};
        if (head.x<0||head.x>=cols||head.y<0||head.y>=rows||snake.some(s=>s.x===head.x&&s.y===head.y)){ alert('Game Over! Score: '+score); return; }
        snake.unshift(head);
        if (head.x===food.x && head.y===food.y){ score++; food = {x:Math.floor(Math.random()*cols), y:Math.floor(Math.random()*rows)}; } else snake.pop();
        draw(); requestAnimationFrame(step);
      }
      draw();
      var keyHandler = function(e){ if(e.key==='ArrowUp') dir={x:0,y:-1}; else if(e.key==='ArrowDown') dir={x:0,y:1}; else if(e.key==='ArrowLeft') dir={x:-1,y:0}; else if(e.key==='ArrowRight') dir={x:1,y:0}; };
      window.addEventListener('keydown', keyHandler);
      // quick stop when overlay closes (cleanup)
      document.getElementById('__gb_close').onclick = function(){ window.removeEventListener('keydown', keyHandler); ov.remove(); };
      // start after a tiny delay so the key handler is attached
      setTimeout(step, 200);
    };

    /* Cookie Clicker */
    document.getElementById('__gb_cookie').onclick = function(){
      var area = document.getElementById('__gb_area'); area.innerHTML='';
      var wrap = document.createElement('div'); wrap.style='text-align:center;width:100%';
      var cookie = document.createElement('button'); cookie.textContent='🍪'; cookie.style='font-size:64px;padding:24px;border-radius:16px;background:#1f9fff;color:#012;border:none;cursor:pointer;transition:transform .12s';
      var score = 0; var cps = 0;
      var scoreDisplay = document.createElement('div'); scoreDisplay.style='margin-top:12px;font-size:18px'; scoreDisplay.textContent = 'Cookies: 0';
      var upBtn = document.createElement('button'); upBtn.textContent='Upgrade (+1 CPS) — Cost 10'; upBtn.style='margin-top:12px;padding:8px 12px;border-radius:8px;border:0;background:#ff9800;color:white;cursor:pointer';
      cookie.onclick = function(){ score++; cookie.style.transform='scale(1.12)'; setTimeout(()=>cookie.style.transform='',120); scoreDisplay.textContent='Cookies: '+score; };
      upBtn.onclick = function(){ if(score>=10){ score-=10; cps+=1; scoreDisplay.textContent='Cookies: '+score; } };
      wrap.appendChild(cookie); wrap.appendChild(scoreDisplay); wrap.appendChild(upBtn);
      area.appendChild(wrap);
      var interval = setInterval(function(){ score += cps; scoreDisplay.textContent='Cookies: '+score; }, 1000);
      document.getElementById('__gb_close').onclick = function(){ clearInterval(interval); ov.remove(); };
    };

  } // end bm_games

  /* ------------- Add rows to page ------------- */
  addRow('✏️','Edit Page','Toggle editable mode on any page (reload to restore).', bm_edit, 'Drag: Edit Page');
  addRow('💻','Dev Console','Open a small in-page JavaScript console for quick evals.', bm_devConsole, 'Drag: Dev Console');
  addRow('🎮','Games Hub','Open a small games overlay (Snake & Cookie Clicker).', bm_games, 'Drag: Games Hub');
  addRow('🌐','Mini Browser','Open a mini-browser popup to visit websites.', bm_mini, 'Drag: Mini Browser');
  addRow('🧩','Script Injector','Paste JS into an overlay and run (trusted only).', bm_injector, 'Drag: Script Injector');
  addRow('⚡','Simulate Crash','Safe visual crash simulation — press Restore.', bm_crash, 'Drag: Simulate Crash');
  addRow('🕒','History Tool','Push demo entries into this tab session history (limited).', bm_history, 'Drag: History Tool');

}); // DOMContentLoaded
</script>
</body>
</html>
