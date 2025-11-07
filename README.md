# bookmarks
javascript:(function(){
if(document.getElementById('bookmarkletToolbox')){alert('Toolbox already loaded'); return;}
const style=document.createElement('style');
style.textContent=`:root{--bg:#f6f7fb;--card:#fff;--accent:#0b5fff;--muted:#6b7280;--radius:12px;}body{font-family:Arial,sans-serif;}
#bookmarkletToolbox{position:fixed;top:50px;left:50px;width:360px;background:var(--card);border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.1);padding:12px;z-index:99999;cursor:move;}
#bookmarkletToolbox h3{margin:6px 0;font-size:16px;}
#bookmarkletToolbox button{margin:2px;padding:6px 10px;border-radius:8px;border:none;background:var(--accent);color:#fff;cursor:pointer;font-size:13px;}
#bookmarkletToolbox button.secondary{background:transparent;color:var(--accent);border:1px solid rgba(11,95,255,0.2);}
#bookmarkletStudyPanel{position:fixed;bottom:20px;right:20px;width:360px;height:450px;background:#fff;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.2);padding:12px;z-index:99998;overflow:auto;display:none;}
#bookmarkletStudyPanel h4{margin:4px 0;font-size:14px;}
#bookmarkletStudyPanel textarea{width:100%;height:80px;margin-top:4px;padding:6px;border-radius:6px;border:1px solid #ccc;resize:none;}
.highlighted{background:yellow;}
.flashcard{background:#e9f1ff;padding:6px;margin:4px 0;border-radius:6px;font-size:13px;}
#bookmarkletFlashcardList div.correct{background:#d0f0c0;}
#bookmarkletPomodoro{position:fixed;top:10px;right:10px;width:180px;background:#fff;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.2);padding:10px;z-index:99999;text-align:center;}
#bookmarkletPomodoro button{margin:2px;padding:4px 8px;font-size:12px;}`;
document.head.appendChild(style);

// Toolbox HTML
const toolbox=document.createElement('div');
toolbox.id='bookmarkletToolbox';
toolbox.innerHTML=`<h3>Bookmarklets Toolbox</h3>
<button id="bmHistorySimBtn">History Flooder (Sim)</button>
<button id="bmCrashSimBtn">Crash Sim</button>
<button id="bmUserscriptBtn">Userscript Builder</button>
<button id="bmStudyHelperBtn">Study Helper</button>
<button id="bmPomodoroBtn">Pomodoro Timer</button>`;
document.body.appendChild(toolbox);

// Study Panel
const studyPanel=document.createElement('div');
studyPanel.id='bookmarkletStudyPanel';
studyPanel.innerHTML=`<h4>Study Helper</h4>
<button id="bmHighlightBtn">Highlight Selected</button>
<button id="bmHideImagesBtn">Hide Images</button>
<button id="bmShowImagesBtn">Show Images</button>
<button id="bmExtractKeywordsBtn">Auto-Detect Keywords</button>
<button id="bmGenerateMCBtn">Generate Multiple Choice</button>
<button id="bmExportFlashcardsBtn">Export Flashcards</button>
<button id="bmImportFlashcardsBtn">Import Flashcards</button>
<div><h4>Notes</h4><textarea id="bmStudyNotes"></textarea></div>
<div><h4>Flashcards</h4><textarea id="bmFlashcards"></textarea><div id="bmFlashcardList"></div></div>
<button id="bmCloseStudyPanel" class="secondary">Close</button>`;
document.body.appendChild(studyPanel);

// Pomodoro Panel
const pomodoro=document.createElement('div');
pomodoro.id='bookmarkletPomodoro';
pomodoro.innerHTML=`<h4>Pomodoro Timer</h4>
<div id="bmTimerDisplay">25:00</div>
<button id="bmStartPomodoroBtn">Start</button>
<button id="bmPausePomodoroBtn">Pause</button>
<button id="bmResetPomodoroBtn">Reset</button>`;
document.body.appendChild(pomodoro);
pomodoro.style.display='none';

// --- Drag toolbox ---
let drag=false, offsetX=0, offsetY=0;
toolbox.addEventListener('mousedown',e=>{if(e.target.tagName==='BUTTON') return; drag=true; offsetX=e.clientX-toolbox.offsetLeft; offsetY=e.clientY-toolbox.offsetTop;});
document.addEventListener('mousemove',e=>{if(!drag) return; toolbox.style.left=(e.clientX-offsetX)+'px'; toolbox.style.top=(e.clientY-offsetY)+'px';});
document.addEventListener('mouseup',()=>drag=false);

// --- Buttons ---
document.getElementById('bmHistorySimBtn').onclick=()=>alert('History flood simulation (safe)');
document.getElementById('bmCrashSimBtn').onclick=()=>{
const o=document.createElement('div'); o.style.position='fixed'; o.style.inset='0'; o.style.background='rgba(200,0,0,0.8)'; o.style.color='white';
o.style.zIndex='999999'; o.style.display='flex'; o.style.alignItems='center'; o.style.justifyContent='center'; o.style.fontSize='24px';
o.textContent='⚠️ Simulated Crash'; document.body.appendChild(o); setTimeout(()=>o.remove(),2000);
};
document.getElementById('bmUserscriptBtn').onclick=()=>{
const code=prompt('Paste JS code (safe bookmarklet, no reload)'); if(!code) return;
alert('Bookmarklet: javascript:(function(){try{'+code+'}catch(e){alert(e);}})();');
};

// Study Helper Buttons
const sp=document.getElementById('bookmarkletStudyPanel');
const notes=document.getElementById('bmStudyNotes');
const flashcards=document.getElementById('bmFlashcards');
const flashList=document.getElementById('bmFlashcardList');
document.getElementById('bmStudyHelperBtn').onclick=()=>sp.style.display='block';
document.getElementById('bmCloseStudyPanel').onclick=()=>sp.style.display='none';
document.getElementById('bmHighlightBtn').onclick=()=>{
const sel=window.getSelection(); if(!sel.rangeCount) return;
const r=sel.getRangeAt(0); const span=document.createElement('span'); span.className='highlighted'; r.surroundContents(span); sel.removeAllRanges();
};
let hiddenImgs=[];
document.getElementById('bmHideImagesBtn').onclick=()=>{hiddenImgs=Array.from(document.images); hiddenImgs.forEach(i=>i.style.display='none');};
document.getElementById('bmShowImagesBtn').onclick=()=>hiddenImgs.forEach(i=>i.style.display='');
document.getElementById('bmExtractKeywordsBtn').onclick=()=>{
const text=document.body.innerText.replace(/\s+/g,' ').toLowerCase(); const words=text.match(/\b[a-z]{4,}\b/g)||[];
const freq={}; words.forEach(w=>{if(!['this','that','with','from','have','your','page','only'].includes(w)) freq[w]=(freq[w]||0)+1;});
const sorted=Object.keys(freq).sort((a,b)=>freq[b]-freq[a]).slice(0,10);
const cards=sorted.map(w=>`What is "${w}"? ?`).join('\n'); flashcards.value+=(flashcards.value?'\n':'')+cards; renderFlashcards(); alert('Keywords detected');
};
document.getElementById('bmGenerateMCBtn').onclick=()=>{
const lines=flashcards.value.split('\n').filter(l=>l.includes('?')); const words = flashcards.value.match(/\b[a-z]{4,}\b/g)||[];
const mcLines=lines.map(l=>{const [q,a]=l.split('?').map(s=>s.trim()); const choices=[a]; while(choices.length<4){const d=words[Math.floor(Math.random()*words.length)]; if(d&&!choices.includes(d)) choices.push(d);} choices.sort(()=>Math.random()-0.5); return q+'? '+choices.join(', ');});
flashcards.value=mcLines.join('\n'); renderFlashcards(); alert('MC generated');
};
function renderFlashcards(){flashList.innerHTML=''; flashcards.value.split('\n').filter(l=>l.includes('?')).forEach(l=>{const [q,a]=l.split('?').map(s=>s.trim()); const div=document.createElement('div'); div.className='flashcard'; div.innerHTML='<strong>Q:</strong> '+q+'?<br><strong>A:</strong> '+(a||''); flashList.appendChild(div);});}

// Pomodoro
const pom=document.getElementById('bookmarkletPomodoro');
const timerDisplay=document.getElementById('bmTimerDisplay'); let timer=null, remaining=25*60;
function updateTimer(){const m=Math.floor(remaining/60).toString().padStart(2,'0'); const s=(remaining%60).toString().padStart(2,'0'); timerDisplay.textContent=m+':'+s;}
document.getElementById('bmPomodoroBtn').onclick=()=>pom.style.display='block';
document.getElementById('bmStartPomodoroBtn').onclick=()=>{
if(timer) clearInterval(timer); timer=setInterval(()=>{if(remaining>0){remaining--; updateTimer();}else{clearInterval(timer); alert('Pomodoro finished!'); remaining=25*60; updateTimer();}},1000);
};
document.getElementById('bmPausePomodoroBtn').onclick=()=>clearInterval(timer);
document.getElementById('bmResetPomodoroBtn').onclick=()=>{clearInterval(timer); remaining=25*60; updateTimer();};
updateTimer();
})();
