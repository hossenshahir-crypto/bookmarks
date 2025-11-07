# bookmarks
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Ultimate Bookmarklet Library</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Set up Inter Font -->
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #f4f7f9; }
        .bookmarklet-link {
            /* Custom styling for the draggable link/button */
            display: inline-block;
            padding: 0.75rem 1.5rem;
            font-weight: 600;
            color: white;
            background-color: #10b981; /* Emerald 500 */
            border-radius: 0.5rem; /* rounded-lg */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
            transition: transform 0.1s, box-shadow 0.1s;
            cursor: move; /* Indicate drag-ability */
            text-decoration: none;
            text-align: center;
            user-select: none;
        }
        .bookmarklet-link:hover {
            background-color: #059669; /* Emerald 600 */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -4px rgba(0, 0, 0, 0.1);
        }
        .bookmarklet-link:active {
            transform: scale(0.98);
        }
        /* Responsive layout for the grid */
        @media (min-width: 768px) {
            .grid-cols-1-md-2 {
                grid-template-columns: 1fr 2fr;
            }
        }
        .instruction-badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            background-color: #fef3c7; /* Amber 100 */
            color: #b45309; /* Amber 700 */
            font-weight: 700;
            border-radius: 9999px; /* rounded-full */
            font-size: 0.75rem;
            margin-bottom: 0.5rem;
        }
        .flex-container-center {
            display: flex;
            align-items: center;
            height: 100%;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center justify-start p-4 md:p-8">

    <div id="app-container" class="w-full max-w-4xl bg-white shadow-2xl rounded-xl p-6 md:p-10 mt-6">
        <header class="text-center mb-10">
            <h1 class="text-4xl font-extrabold text-gray-900 mb-2">
                The Utility Belt Bookmarklet Hub
            </h1>
            <p class="text-gray-500 text-lg">
                **Drag the link buttons to your bookmarks bar.** For long scripts, use the "**Copy Full Code**" button.
            </p>
        </header>

        <!-- Manual Installation Instructions Box -->
        <div class="mb-10 p-6 bg-red-50 border-l-4 border-red-500 rounded-lg shadow-xl">
            <h2 class="text-xl font-extrabold text-red-800 mb-2">⚠️ Long Script Warning</h2>
            <p class="text-red-700 font-semibold mb-3">
                The **Script Editor**, **Games Hub**, and **Flood History** are too long. To guarantee they work:
            </p>
            <ol class="list-decimal list-inside space-y-3 text-gray-700 font-semibold">
                <li>Click the **Copy Full Code** button.</li>
                <li>**Right-click** your Bookmark Bar, select **Add Page** (or equivalent).</li>
                <li>Give it a name and **paste the copied code** into the URL/Address field.</li>
            </ol>
        </div>

        <!-- Bookmarklets List -->
        <div id="bookmarklet-list" class="space-y-8">

            <!-- 1. Script Editor (Tampermonkey Style) - LONG SCRIPT -->
            <div class="grid grid-cols-1 gap-4 md:grid-cols-1-md-2 items-start p-4 bg-gray-50 rounded-lg border border-gray-100">
                <div class="flex justify-center md:justify-start pt-2 flex-col items-center md:items-start">
                    <!-- DRAGGABLE LINK -->
                    <a class="bookmarklet-link bg-blue-600 hover:bg-blue-700"
                        id="script_editor_link"
                        href='javascript:(function(){var id="__script_editor",c=document.getElementById(id);if(c){c.remove();return}var s="position:fixed;top:5%;left:5%;width:90%;max-width:800px;height:90%;max-height:600px;background:#1f2937;border:3px solid #3b82f6;z-index:2147483647;border-radius:12px;overflow:hidden;font-family:monospace;color:#ccc;box-shadow:0 0 30px rgba(0,0,0,0.5);display:flex;flex-direction:column;";c=document.createElement("div");c.id=id;c.style.cssText=s;var h="<div style=\"background:#3b82f6;color:white;padding:12px 16px;display:flex;justify-content:space-between;align-items:center;font-size:16px;font-weight:bold;\">💻 Script Editor / Dev Console<button onclick=\"document.getElementById(\'"+id+"\').remove()\" style=\"background:none;border:none;color:white;cursor:pointer;font-weight:bold;font-size:24px;\">×</button></div>";var t=document.createElement("div");t.style.cssText="display:flex;flex-direction:row;flex-grow:1;overflow:hidden;";var i=document.createElement("textarea");i.placeholder="// Write JavaScript code here (use console.log() to print to output)";i.style.cssText="flex:1;border:none;resize:none;padding:15px;box-sizing:border-box;background:#111827;color:white;font-size:13px;line-height:1.5;caret-color:#3b82f6;";var o=document.createElement("pre");o.style.cssText="flex:1;padding:15px;margin:0;overflow-y:scroll;font-size:11px;white-space:pre-wrap;background:#374151;color:#10b981;border-left:1px solid #4b5563;";o.textContent="Output Console:\\n";var b=document.createElement("button");b.textContent="Execute Script (F8)";b.style.cssText="width:100%;padding:10px;background:#10b981;color:white;border:none;cursor:pointer;font-size:15px;font-weight:bold;transition:background 0.2s;";b.onmouseover=function(){this.style.background="#059669";};b.onmouseout=function(){this.style.background="#10b981";};b.onclick=function(){var scr=i.value;try{var l=console.log,out="";console.log=function(){for(var j=0;j<arguments.length;j++)out+=(typeof arguments[j]=='object'?JSON.stringify(arguments[j],null,2):arguments[j])+' ';out+='\\n';};var res=eval(scr);console.log=l;var rs=(typeof res=='undefined'?'':(typeof res=='object'?JSON.stringify(res,null,2):String(res)));o.textContent+='> Executing script...\\n';if(out)o.textContent+='LOG:\\n'+out;o.textContent+='RESULT: '+rs+'\\n\\n';}catch(e){o.textContent+='ERROR: '+e.toString()+'\\n\\n';}o.scrollTop=o.scrollHeight;i.focus();};t.appendChild(i);t.appendChild(o);c.innerHTML=h;c.appendChild(t);c.appendChild(b);document.body.appendChild(c);document.addEventListener('keydown',function(e){if(e.key==='F8'){e.preventDefault();b.click();}});})();void(0);'
                        title="Drag or Manually Paste Code">
                        💻 Script Editor
                    </a>
                    <p class="text-xs text-red-500 font-semibold mt-1">
                        (Drag works, but manual paste is safer.)
                    </p>
                </div>
                <div class="text-gray-600">
                    <p class="instruction-badge">LONG SCRIPT - MANUAL PASTE</p>
                    <p class="font-medium text-gray-800">Tampermonkey-Style Console</p>
                    <p class="text-sm mt-1 mb-3">
                        Use this console to write and execute any JavaScript code on the current page.
                    </p>
                    <div class="flex gap-2 items-center">
                        <button class="copy-button px-4 py-2 bg-blue-600 text-white font-bold rounded-lg hover:bg-blue-700 transition"
                                data-target="script_editor_code">
                            Copy Full Code
                        </button>
                        <span id="copy-status-script_editor_code" class="text-sm text-green-600 font-semibold opacity-0 transition-opacity duration-300"></span>
                    </div>
                    <!-- Hidden Textarea to hold the full, long code -->
                    <textarea id="script_editor_code" style="display:none;">javascript:(function(){var id="__script_editor",c=document.getElementById(id);if(c){c.remove();return}var s="position:fixed;top:5%;left:5%;width:90%;max-width:800px;height:90%;max-height:600px;background:#1f2937;border:3px solid #3b82f6;z-index:2147483647;border-radius:12px;overflow:hidden;font-family:monospace;color:#ccc;box-shadow:0 0 30px rgba(0,0,0,0.5);display:flex;flex-direction:column;";c=document.createElement("div");c.id=id;c.style.cssText=s;var h="<div style=\"background:#3b82f6;color:white;padding:12px 16px;display:flex;justify-content:space-between;align-items:center;font-size:16px;font-weight:bold;\">💻 Script Editor / Dev Console<button onclick=\"document.getElementById(\'"+id+"\').remove()\" style=\"background:none;border:none;color:white;cursor:pointer;font-weight:bold;font-size:24px;\">×</button></div>";var t=document.createElement("div");t.style.cssText="display:flex;flex-direction:row;flex-grow:1;overflow:hidden;";var i=document.createElement("textarea");i.placeholder="// Write JavaScript code here (use console.log() to print to output)";i.style.cssText="flex:1;border:none;resize:none;padding:15px;box-sizing:border-box;background:#111827;color:white;font-size:13px;line-height:1.5;caret-color:#3b82f6;";var o=document.createElement("pre");o.style.cssText="flex:1;padding:15px;margin:0;overflow-y:scroll;font-size:11px;white-space:pre-wrap;background:#374151;color:#10b981;border-left:1px solid #4b5563;";o.textContent="Output Console:\\n";var b=document.createElement("button");b.textContent="Execute Script (F8)";b.style.cssText="width:100%;padding:10px;background:#10b981;color:white;border:none;cursor:pointer;font-size:15px;font-weight:bold;transition:background 0.2s;";b.onmouseover=function(){this.style.background="#059669";};b.onmouseout=function(){this.style.background="#10b981";};b.onclick=function(){var scr=i.value;try{var l=console.log,out="";console.log=function(){for(var j=0;j<arguments.length;j++)out+=(typeof arguments[j]=='object'?JSON.stringify(arguments[j],null,2):arguments[j])+' ';out+='\\n';};var res=eval(scr);console.log=l;var rs=(typeof res=='undefined'?'':(typeof res=='object'?JSON.stringify(res,null,2):String(res)));o.textContent+='> Executing script...\\n';if(out)o.textContent+='LOG:\\n'+out;o.textContent+='RESULT: '+rs+'\\n\\n';}catch(e){o.textContent+='ERROR: '+e.toString()+'\\n\\n';}o.scrollTop=o.scrollHeight;i.focus();};t.appendChild(i);t.appendChild(o);c.innerHTML=h;c.appendChild(t);c.appendChild(b);document.body.appendChild(c);document.addEventListener('keydown',function(e){if(e.key==='F8'){e.preventDefault();b.click();}});})();void(0);</textarea>
                </div>
            </div>

            <!-- 2. Games Hub - LONG SCRIPT -->
            <div class="grid grid-cols-1 gap-4 md:grid-cols-1-md-2 items-start p-4 bg-gray-50 rounded-lg border border-gray-100">
                <div class="flex justify-center md:justify-start pt-2 flex-col items-center md:items-start">
                    <!-- DRAGGABLE LINK -->
                    <a class="bookmarklet-link bg-indigo-600 hover:bg-indigo-700"
                        id="games_hub_link"
                        href='javascript:(function(){var id="__bm_games",ov=document.getElementById(id);if(ov){ov.remove();return}var style="position:fixed;inset:0;background:rgba(0,0,0,0.95);display:flex;align-items:center;justify-content:center;z-index:2147483646;color:white;font-family:sans-serif;";ov=document.createElement("div");ov.id=id;ov.style.cssText=style;var box=document.createElement("div");box.style.cssText="background:#081124;padding:18px;border-radius:12px;width:760px;max-width:96%;height:560px;max-height:96%;display:flex;flex-direction:column;box-shadow:0 0 30px rgba(0,0,0,0.5);";box.innerHTML="<div style=\"display:flex;justify-content:space-between;align-items:center;width:100%\"><strong style=\"font-size:18px\">🎮 Games Hub</strong><div><button id=\"__games_close\" style=\"background:#ef4444;color:white;border:none;padding:6px 10px;border-radius:8px;cursor:pointer\">Close</button></div></div><div style=\"margin-top:6px;color:#9fb4d6;font-size:13px\">Click a game to play below.</div><div id=\"__glist\" style=\"display:flex;flex-wrap:wrap;gap:10px;margin-top:8px\"></div><div id=\"__garea\" style=\"flex:1;margin-top:8px;display:flex;align-items:center;justify-content:center;overflow:auto;\"></div>";ov.appendChild(box);document.body.appendChild(ov);document.getElementById("__games_close").onclick=function(){ov.remove();};function makeGameButton(name,func){var b=document.createElement("button");b.textContent=name;b.style.cssText="background:#1f9fff;color:#012;border:none;padding:8px 10px;border-radius:8px;cursor:pointer;font-weight:800;margin:4px;transition:background 0.2s;";b.onmouseover=function(){this.style.background="#7dd3fc";};b.onmouseout=function(){this.style.background="#1f9fff";};b.onclick=func;document.getElementById("__glist").appendChild(b);}function showGameOver(score){var el=document.createElement("div");el.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px;background:#ef4444;color:white;border-radius:10px;box-shadow:0 0 20px rgba(0,0,0,0.5);z-index:2147483647;";el.innerHTML=`Game Over! Score: ${score}<button onclick="this.parentElement.remove()" style="margin-left:10px;background:white;color:#ef4444;border:none;padding:5px 10px;border-radius:5px;cursor:pointer;">OK</button>`;document.body.appendChild(el);}makeGameButton("Snake",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("canvas");c.width=400;c.height=400;c.style.background="#000";g.appendChild(c);var ctx=c.getContext("2d"),b=20;var s=[{x:8,y:8}],d={x:1,y:0},f={x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)},score=0;document.addEventListener("keydown",function(e){if(e.key==="ArrowUp"&&d.y!==1)d={x:0,y:-1};if(e.key==="ArrowDown"&&d.y!==-1)d={x:0,y:1};if(e.key==="ArrowLeft"&&d.x!==1)d={x:-1,y:0};if(e.key==="ArrowRight"&&d.x!==-1)d={x:1,y:0};});function l(){ctx.fillStyle="#000";ctx.fillRect(0,0,400,400);s.forEach(s=>{ctx.fillStyle="#1f9fff";ctx.fillRect(s.x*b,s.y*b,b-1,b-1);});ctx.fillStyle="red";ctx.fillRect(f.x*b,f.y*b,b-1,b-1);var nx=s[0].x+d.x,ny=s[0].y+d.y;if(nx<0||nx>=20||ny<0||ny>=20||s.some(s=>s.x===nx&&s.y===ny)){showGameOver(score);return;}s.unshift({x:nx,y:ny});if(nx===f.x&&ny===f.y){score++;f={x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)};}else{s.pop();}setTimeout(l,120);}l();});makeGameButton("Tic Tac Toe",function(){var g=document.getElementById("__garea");g.innerHTML="";var board=["","","","","","","","",""],turn="X";var t=document.createElement("table");t.style="border-collapse:collapse;margin:auto;font-size:28px;text-align:center;color:white";for(var i=0;i<3;i++){var tr=document.createElement("tr");for(var j=0;j<3;j++){var td=document.createElement("td");td.style="width:80px;height:80px;border:1px solid #1f9fff;cursor:pointer";td.dataset.idx=i*3+j;td.onclick=function(){var idx=parseInt(this.dataset.idx);if(!board[idx]){board[idx]=turn;this.textContent=turn;turn=turn==="X"?"O":"X";checkWin();}};tr.appendChild(td);}t.appendChild(tr);}g.appendChild(t);function checkWin(){var w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];w.forEach(w=>{if(board[w[0]]&&board[w[0]]===board[w[1]]&&board[w[0]]===board[w[2]]){var winner=board[w[0]];var el=document.createElement("div");el.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px;background:#10b981;color:white;border-radius:10px;box-shadow:0 0 20px rgba(0,0,0,0.5);z-index:2147483647;";el.innerHTML=`Winner: ${winner}<button onclick="this.parentElement.remove()" style="margin-left:10px;background:white;color:#10b981;border:none;padding:5px 10px;border-radius:5px;cursor:pointer;">OK</button>`;document.body.appendChild(el);}});}
});makeGameButton("2048",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("div");c.style="text-align:center";var grid=[],score=0;var d=document.createElement("div");d.style="margin-bottom:8px;font-size:16px;color:white;";d.textContent="Score: "+score;c.appendChild(d);var t=document.createElement("table");t.style="border-collapse:collapse;margin:auto;background:#0a0f1c;border-radius:6px;padding:6px";for(var i=0;i<4;i++){var tr=document.createElement("tr");grid[i]=[];for(var j=0;j<4;j++){var td=document.createElement("td");td.style="width:60px;height:60px;border:1px solid #1f9fff;text-align:center;font-weight:bold;font-size:18px;color:#dbeafe;";td.textContent="";grid[i][j]=td;tr.appendChild(td);}t.appendChild(tr);}c.appendChild(t);g.appendChild(c);function addRandom(){var e=[];for(var i=0;i<4;i++)for(var j=0;j<4;j++)if(grid[i][j].textContent==="")e.push([i,j]);if(e.length){var r=e[Math.floor(Math.random()*e.length)];grid[r[0]][r[1]].textContent=Math.random()<0.9?"2":"4";}}function updateDisplay(){d.textContent="Score: "+score;}function move(dir){var moved=false;function slide(r){var a=Array.from(r).filter(x=>x.textContent!="");var cells=Array.from(r);for(var i=0;i<a.length-1;i++){if(a[i].textContent===a[i+1].textContent){a[i].textContent=parseInt(a[i].textContent)*2;score+=parseInt(a[i].textContent);a[i+1].textContent="";i++;}}var nR=a.filter(x=>x.textContent!="");while(nR.length<4)nR.push({textContent:""});for(var i=0;i<4;i++){if(cells[i].textContent!==nR[i].textContent){cells[i].textContent=nR[i].textContent;moved=true;}}}if(dir==="ArrowLeft"){for(var i=0;i<4;i++){var rC=Array.from(t.rows[i].cells);slide(rC);}}if(dir==="ArrowRight"){for(var i=0;i<4;i++){var rC=Array.from(t.rows[i].cells);rC.reverse();slide(rC);rC.reverse().forEach((c,idx)=>{t.rows[i].cells[idx].textContent=c.textContent;});}}if(dir==="ArrowUp"){for(var j=0;j<4;j++){var cC=[];for(var i=0;i<4;i++)cC.push(t.rows[i].cells[j]);slide(cC);for(var i=0;i<4;i++)t.rows[i].cells[j].textContent=cC[i].textContent;}}if(dir==="ArrowDown"){for(var j=0;j<4;j++){var cC=[];for(var i=0;i<4;i++)cC.push(t.rows[i].cells[j]);cC.reverse();slide(cC);cC.reverse();for(var i=0;i<4;i++)t.rows[i].cells[j].textContent=cC[i].textContent;}}if(moved)addRandom();updateDisplay();}document.addEventListener("keydown",function(e){if(["ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].includes(e.key)){e.preventDefault();move(e.key);}});addRandom();addRandom();updateDisplay();});makeGameButton("Cookie Clicker",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("button");c.textContent="🍪 Cookie";c.style="font-size:32px;padding:20px 28px;border-radius:12px;background:#1f9fff;color:#012;border:none;cursor:pointer;transition:transform 0.1s;";c.onmousedown=function(){this.style.transform="scale(0.95)";c.onmouseup=function(){this.style.transform="scale(1)";};var s=0;var d=document.createElement("div");d.style="margin-top:8px;font-size:18px;color:white;font-weight:bold;";function u(){d.textContent="Cookies: "+s;}u();g.appendChild(c);g.appendChild(d);var cps=0;var up=document.createElement("button");up.textContent="Upgrade (+1 CPS) - Cost 10";up.style="margin-top:12px;padding:8px 12px;background:#ff9800;color:white;border:none;border-radius:8px;cursor:pointer;font-weight:bold;";up.onclick=function(){if(s>=10){s-=10;cps+=1;up.textContent="Upgrade (+1 CPS) - Cost "+(10+cps*5);u();}};g.appendChild(up);c.onclick=function(){s++;u();}setInterval(function(){s+=cps;u();},1000);});})());void(0);'
                        title="Drag or Manually Paste Code">
                        🎮 Games Hub
                    </a>
                    <p class="text-xs text-red-500 font-semibold mt-1">
                        (Drag works, but manual paste is safer.)
                    </p>
                </div>
                <div class="text-gray-600">
                    <p class="instruction-badge">LONG SCRIPT - MANUAL PASTE</p>
                    <p class="font-medium text-gray-800">In-Page Games Console</p>
                    <p class="text-sm mt-1 mb-3">
                        Launches a hub with Snake, Tic-Tac-Toe, 2048, and Cookie Clicker right over the current page.
                    </p>
                    <div class="flex gap-2 items-center">
                        <button class="copy-button px-4 py-2 bg-indigo-600 text-white font-bold rounded-lg hover:bg-indigo-700 transition"
                                data-target="games_hub_code">
                            Copy Full Code
                        </button>
                        <span id="copy-status-games_hub_code" class="text-sm text-green-600 font-semibold opacity-0 transition-opacity duration-300"></span>
                    </div>
                    <!-- Hidden Textarea to hold the full, long code -->
                    <textarea id="games_hub_code" style="display:none;">javascript:(function(){var id="__bm_games",ov=document.getElementById(id);if(ov){ov.remove();return}var style="position:fixed;inset:0;background:rgba(0,0,0,0.95);display:flex;align-items:center;justify-content:center;z-index:2147483646;color:white;font-family:sans-serif;";ov=document.createElement("div");ov.id=id;ov.style.cssText=style;var box=document.createElement("div");box.style.cssText="background:#081124;padding:18px;border-radius:12px;width:760px;max-width:96%;height:560px;max-height:96%;display:flex;flex-direction:column;box-shadow:0 0 30px rgba(0,0,0,0.5);";box.innerHTML="<div style=\"display:flex;justify-content:space-between;align-items:center;width:100%\"><strong style=\"font-size:18px\">🎮 Games Hub</strong><div><button id=\"__games_close\" style=\"background:#ef4444;color:white;border:none;padding:6px 10px;border-radius:8px;cursor:pointer\">Close</button></div></div><div style=\"margin-top:6px;color:#9fb4d6;font-size:13px\">Click a game to play below.</div><div id=\"__glist\" style=\"display:flex;flex-wrap:wrap;gap:10px;margin-top:8px\"></div><div id=\"__garea\" style=\"flex:1;margin-top:8px;display:flex;align-items:center;justify-content:center;overflow:auto;\"></div>";ov.appendChild(box);document.body.appendChild(ov);document.getElementById("__games_close").onclick=function(){ov.remove();};function makeGameButton(name,func){var b=document.createElement("button");b.textContent=name;b.style.cssText="background:#1f9fff;color:#012;border:none;padding:8px 10px;border-radius:8px;cursor:pointer;font-weight:800;margin:4px;transition:background 0.2s;";b.onmouseover=function(){this.style.background="#7dd3fc";};b.onmouseout=function(){this.style.background="#1f9fff";};b.onclick=func;document.getElementById("__glist").appendChild(b);}function showGameOver(score){var el=document.createElement("div");el.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px;background:#ef4444;color:white;border-radius:10px;box-shadow:0 0 20px rgba(0,0,0,0.5);z-index:2147483647;";el.innerHTML=`Game Over! Score: ${score}<button onclick="this.parentElement.remove()" style="margin-left:10px;background:white;color:#ef4444;border:none;padding:5px 10px;border-radius:5px;cursor:pointer;">OK</button>`;document.body.appendChild(el);}makeGameButton("Snake",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("canvas");c.width=400;c.height=400;c.style.background="#000";g.appendChild(c);var ctx=c.getContext("2d"),b=20;var s=[{x:8,y:8}],d={x:1,y:0},f={x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)},score=0;document.addEventListener("keydown",function(e){if(e.key==="ArrowUp"&&d.y!==1)d={x:0,y:-1};if(e.key==="ArrowDown"&&d.y!==-1)d={x:0,y:1};if(e.key==="ArrowLeft"&&d.x!==1)d={x:-1,y:0};if(e.key==="ArrowRight"&&d.x!==-1)d={x:1,y:0};});function l(){ctx.fillStyle="#000";ctx.fillRect(0,0,400,400);s.forEach(s=>{ctx.fillStyle="#1f9fff";ctx.fillRect(s.x*b,s.y*b,b-1,b-1);});ctx.fillStyle="red";ctx.fillRect(f.x*b,f.y*b,b-1,b-1);var nx=s[0].x+d.x,ny=s[0].y+d.y;if(nx<0||nx>=20||ny<0||ny>=20||s.some(s=>s.x===nx&&s.y===ny)){showGameOver(score);return;}s.unshift({x:nx,y:ny});if(nx===f.x&&ny===f.y){score++;f={x:Math.floor(Math.random()*20),y:Math.floor(Math.random()*20)};}else{s.pop();}setTimeout(l,120);}l();});makeGameButton("Tic Tac Toe",function(){var g=document.getElementById("__garea");g.innerHTML="";var board=["","","","","","","","",""],turn="X";var t=document.createElement("table");t.style="border-collapse:collapse;margin:auto;font-size:28px;text-align:center;color:white";for(var i=0;i<3;i++){var tr=document.createElement("tr");for(var j=0;j<3;j++){var td=document.createElement("td");td.style="width:80px;height:80px;border:1px solid #1f9fff;cursor:pointer";td.dataset.idx=i*3+j;td.onclick=function(){var idx=parseInt(this.dataset.idx);if(!board[idx]){board[idx]=turn;this.textContent=turn;turn=turn==="X"?"O":"X";checkWin();}};tr.appendChild(td);}t.appendChild(tr);}g.appendChild(t);function checkWin(){var w=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];w.forEach(w=>{if(board[w[0]]&&board[w[0]]===board[w[1]]&&board[w[0]]===board[w[2]]){var winner=board[w[0]];var el=document.createElement("div");el.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px;background:#10b981;color:white;border-radius:10px;box-shadow:0 0 20px rgba(0,0,0,0.5);z-index:2147483647;";el.innerHTML=`Winner: ${winner}<button onclick="this.parentElement.remove()" style="margin-left:10px;background:white;color:#10b981;border:none;padding:5px 10px;border-radius:5px;cursor:pointer;">OK</button>`;document.body.appendChild(el);}});}
});makeGameButton("2048",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("div");c.style="text-align:center";var grid=[],score=0;var d=document.createElement("div");d.style="margin-bottom:8px;font-size:16px;color:white;";d.textContent="Score: "+score;c.appendChild(d);var t=document.createElement("table");t.style="border-collapse:collapse;margin:auto;background:#0a0f1c;border-radius:6px;padding:6px";for(var i=0;i<4;i++){var tr=document.createElement("tr");grid[i]=[];for(var j=0;j<4;j++){var td=document.createElement("td");td.style="width:60px;height:60px;border:1px solid #1f9fff;text-align:center;font-weight:bold;font-size:18px;color:#dbeafe;";td.textContent="";grid[i][j]=td;tr.appendChild(td);}t.appendChild(tr);}c.appendChild(t);g.appendChild(c);function addRandom(){var e=[];for(var i=0;i<4;i++)for(var j=0;j<4;j++)if(grid[i][j].textContent==="")e.push([i,j]);if(e.length){var r=e[Math.floor(Math.random()*e.length)];grid[r[0]][r[1]].textContent=Math.random()<0.9?"2":"4";}}function updateDisplay(){d.textContent="Score: "+score;}function move(dir){var moved=false;function slide(r){var a=Array.from(r).filter(x=>x.textContent!="");var cells=Array.from(r);for(var i=0;i<a.length-1;i++){if(a[i].textContent===a[i+1].textContent){a[i].textContent=parseInt(a[i].textContent)*2;score+=parseInt(a[i].textContent);a[i+1].textContent="";i++;}}var nR=a.filter(x=>x.textContent!="");while(nR.length<4)nR.push({textContent:""});for(var i=0;i<4;i++){if(cells[i].textContent!==nR[i].textContent){cells[i].textContent=nR[i].textContent;moved=true;}}}if(dir==="ArrowLeft"){for(var i=0;i<4;i++){var rC=Array.from(t.rows[i].cells);slide(rC);}}if(dir==="ArrowRight"){for(var i=0;i<4;i++){var rC=Array.from(t.rows[i].cells);rC.reverse();slide(rC);rC.reverse().forEach((c,idx)=>{t.rows[i].cells[idx].textContent=c.textContent;});}}if(dir==="ArrowUp"){for(var j=0;j<4;j++){var cC=[];for(var i=0;i<4;i++)cC.push(t.rows[i].cells[j]);slide(cC);for(var i=0;i<4;i++)t.rows[i].cells[j].textContent=cC[i].textContent;}}if(dir==="ArrowDown"){for(var j=0;j<4;j++){var cC=[];for(var i=0;i<4;i++)cC.push(t.rows[i].cells[j]);cC.reverse();slide(cC);cC.reverse();for(var i=0;i<4;i++)t.rows[i].cells[j].textContent=cC[i].textContent;}}if(moved)addRandom();updateDisplay();}document.addEventListener("keydown",function(e){if(["ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].includes(e.key)){e.preventDefault();move(e.key);}});addRandom();addRandom();updateDisplay();});makeGameButton("Cookie Clicker",function(){var g=document.getElementById("__garea");g.innerHTML="";var c=document.createElement("button");c.textContent="🍪 Cookie";c.style="font-size:32px;padding:20px 28px;border-radius:12px;background:#1f9fff;color:#012;border:none;cursor:pointer;transition:transform 0.1s;";c.onmousedown=function(){this.style.transform="scale(0.95)";c.onmouseup=function(){this.style.transform="scale(1)";};var s=0;var d=document.createElement("div");d.style="margin-top:8px;font-size:18px;color:white;font-weight:bold;";function u(){d.textContent="Cookies: "+s;}u();g.appendChild(c);g.appendChild(d);var cps=0;var up=document.createElement("button");up.textContent="Upgrade (+1 CPS) - Cost 10";up.style="margin-top:12px;padding:8px 12px;background:#ff9800;color:white;border:none;border-radius:8px;cursor:pointer;font-weight:bold;";up.onclick=function(){if(s>=10){s-=10;cps+=1;up.textContent="Upgrade (+1 CPS) - Cost "+(10+cps*5);u();}};g.appendChild(up);c.onclick=function(){s++;u();}setInterval(function(){s+=cps;u();},1000);});})());void(0);</textarea>
                </div>
            </div>

            <!-- 3. Flood History - LONG SCRIPT -->
            <div class="grid grid-cols-1 gap-4 md:grid-cols-1-md-2 items-start p-4 bg-gray-50 rounded-lg border border-gray-100">
                <div class="flex justify-center md:justify-start pt-2 flex-col items-center md:items-start">
                    <!-- DRAGGABLE LINK -->
                    <a class="bookmarklet-link bg-red-600 hover:bg-red-700"
                        id="flood_history_link"
                        href='javascript:(function(){const m=document.createElement("div");m.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px 30px;background:#1f2937;color:white;border-radius:12px;z-index:9999999;box-shadow:0 10px 25px rgba(0,0,0,0.5);display:flex;flex-direction:column;gap:15px;max-width:350px;font-family:sans-serif;";m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#f87171;'>🌊 Flood History</h2><p style='font-size:14px;color:#d1d5db;'>Enter the title and the number of entries to flood the history with.</p>Title: <input type='text' id='floodTitle' value='Untitled Page' style='padding:8px;border-radius:6px;border:1px solid #4b5563;background:#374151;color:white;'><input type='number' id='floodCount' value='50' min='1' max='500' style='padding:8px;border-radius:6px;border:1px solid #4b5563;background:#374151;color:white;'> <div style='display:flex;justify-content:space-between;gap:10px;'><button id='floodStart' style='flex:1;padding:10px;background:#ef4444;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Start Flood</button><button id='floodCancel' style='flex:1;padding:10px;background:#4b5563;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Cancel</button></div>";document.body.appendChild(m);document.getElementById("floodCancel").onclick=function(){m.remove()};document.getElementById("floodStart").onclick=function(){const t=document.getElementById("floodTitle").value,c=parseInt(document.getElementById("floodCount").value);if(isNaN(c)||c<1){m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#f87171;'>Error!</h2><p style='font-size:14px;color:#d1d5db;'>Please enter a valid count (1-500).</p><button onclick='this.parentElement.remove()' style='padding:10px;background:#ef4444;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Close</button>";return}const u=location.href.split("?")[0];for(let i=1;i<=c;i++){history.pushState({},t+i,u+"?"+Math.random().toString(36).substring(2,15)+i)}m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#10b981;'>Success!</h2><p style='font-size:14px;color:#d1d5db;'>History flooded with "+c+" entries!</p><button onclick='this.parentElement.remove()' style='padding:10px;background:#10b981;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Close</button>"}})();void(0);'
                        title="Drag or Manually Paste Code">
                        🌊 Flood History
                    </a>
                    <p class="text-xs text-red-500 font-semibold mt-1">
                        (Drag works, but manual paste is safer.)
                    </p>
                </div>
                <div class="text-gray-600">
                    <p class="instruction-badge">LONG SCRIPT - MANUAL PASTE</p>
                    <p class="font-medium text-gray-800">History Spam Utility</p>
                    <p class="text-sm mt-1 mb-3">
                        Fills the current browser history list with many entries to make the back button unusable (use with caution).
                    </p>
                    <div class="flex gap-2 items-center">
                        <button class="copy-button px-4 py-2 bg-red-600 text-white font-bold rounded-lg hover:bg-red-700 transition"
                                data-target="flood_history_code">
                            Copy Full Code
                        </button>
                        <span id="copy-status-flood_history_code" class="text-sm text-green-600 font-semibold opacity-0 transition-opacity duration-300"></span>
                    </div>
                    <!-- Hidden Textarea to hold the full, long code -->
                    <textarea id="flood_history_code" style="display:none;">javascript:(function(){const m=document.createElement("div");m.style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);padding:20px 30px;background:#1f2937;color:white;border-radius:12px;z-index:9999999;box-shadow:0 10px 25px rgba(0,0,0,0.5);display:flex;flex-direction:column;gap:15px;max-width:350px;font-family:sans-serif;";m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#f87171;'>🌊 Flood History</h2><p style='font-size:14px;color:#d1d5db;'>Enter the title and the number of entries to flood the history with.</p>Title: <input type='text' id='floodTitle' value='Untitled Page' style='padding:8px;border-radius:6px;border:1px solid #4b5563;background:#374151;color:white;'><input type='number' id='floodCount' value='50' min='1' max='500' style='padding:8px;border-radius:6px;border:1px solid #4b5563;background:#374151;color:white;'> <div style='display:flex;justify-content:space-between;gap:10px;'><button id='floodStart' style='flex:1;padding:10px;background:#ef4444;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Start Flood</button><button id='floodCancel' style='flex:1;padding:10px;background:#4b5563;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Cancel</button></div>";document.body.appendChild(m);document.getElementById("floodCancel").onclick=function(){m.remove()};document.getElementById("floodStart").onclick=function(){const t=document.getElementById("floodTitle").value,c=parseInt(document.getElementById("floodCount").value);if(isNaN(c)||c<1){m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#f87171;'>Error!</h2><p style='font-size:14px;color:#d1d5db;'>Please enter a valid count (1-500).</p><button onclick='this.parentElement.remove()' style='padding:10px;background:#ef4444;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Close</button>";return}const u=location.href.split("?")[0];for(let i=1;i<=c;i++){history.pushState({},t+i,u+"?"+Math.random().toString(36).substring(2,15)+i)}m.innerHTML="<h2 style='font-size:1.5rem;font-weight:bold;color:#10b981;'>Success!</h2><p style='font-size:14px;color:#d1d5db;'>History flooded with "+c+" entries!</p><button onclick='this.parentElement.remove()' style='padding:10px;background:#10b981;color:white;border:none;border-radius:6px;cursor:pointer;font-weight:bold;transition:background 0.2s;'>Close</button>"}})();void(0);</textarea>
                </div>
            </div>

        </div>

    </div>

    <!-- JavaScript for Copy-to-Clipboard functionality -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            /**
             * Copies text from a hidden textarea element to the clipboard and shows status feedback.
             * @param {string} textareaId - The ID of the hidden textarea containing the text to copy.
             * @param {string} statusElementId - The ID of the span element to show copy status.
             */
            function copyTextToClipboard(textareaId, statusElementId) {
                const textarea = document.getElementById(textareaId);
                const statusSpan = document.getElementById(statusElementId);

                if (!textarea) {
                    console.error(`Textarea not found for ID: ${textareaId}`);
                    return;
                }

                // 1. Temporarily make the textarea selectable
                const originalDisplay = textarea.style.display;
                textarea.style.display = 'block'; 
                
                // 2. Select the text
                textarea.select();
                textarea.setSelectionRange(0, 99999); // For mobile devices

                let success = false;
                try {
                    // 3. Execute the copy command (Legacy but required for iFrame environments)
                    success = document.execCommand('copy');
                } catch (err) {
                    console.error('Failed to copy text:', err);
                }

                // 4. Hide the textarea again
                textarea.style.display = originalDisplay;

                // 5. Provide visual feedback
                if (statusSpan) {
                    // Reset classes and set message based on result
                    statusSpan.classList.remove('opacity-0', 'text-red-600');
                    statusSpan.classList.add(success ? 'text-green-600' : 'text-red-600');
                    statusSpan.textContent = success ? 'Copied!' : 'Copy Failed!';
                    
                    // Show message
                    setTimeout(() => {
                        statusSpan.classList.remove('opacity-0');
                    }, 50);

                    // Fade out the status message after a delay
                    setTimeout(() => {
                        statusSpan.classList.add('opacity-0');
                    }, 2000);
                }
            }

            // Attach event listeners to all elements with the 'copy-button' class
            document.querySelectorAll('.copy-button').forEach(button => {
                button.addEventListener('click', (event) => {
                    event.preventDefault(); // Prevent default button submission

                    const targetId = button.dataset.target; // Get the target textarea ID (e.g., 'script_editor_code')
                    const statusId = `copy-status-${targetId}`; // Construct the status span ID

                    copyTextToClipboard(targetId, statusId);
                });
            });

            // Re-apply the initial hidden state to all textareas (a safety measure)
            document.querySelectorAll('textarea[id$="_code"]').forEach(ta => {
                ta.style.display = 'none';
            });
        });
    </script>
</body>
</html>
