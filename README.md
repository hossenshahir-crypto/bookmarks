# bookmarks
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Bookmarklet Utility Hub</title>
    <!-- Load Tailwind CSS from CDN for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f4f7fa;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .container {
            max-width: 90%;
            width: 1200px;
        }
        .bookmarklet-card {
            transition: all 0.3s ease-in-out;
            border: 2px solid transparent;
        }
        /* Style for the button container */
        .action-container a {
            cursor: move;
        }
        .instructions {
            background-color: #ffffff;
            border-left: 5px solid #ef4444; /* Red emphasis on manual steps */
        }
        /* Hidden textarea for reliable copy functionality */
        .hidden-textarea {
            position: absolute;
            left: -9999px;
            top: -9999px;
        }
    </style>
</head>
<body>

<div class="container mx-auto p-4 sm:p-10">

    <header class="text-center mb-10">
        <h1 class="text-5xl font-extrabold text-gray-900 mb-4">
            Advanced Bookmarklet Hub
        </h1>
        <p class="text-lg text-gray-600">
            If dragging fails, use the **"Copy Code"** button to manually create the bookmark.
        </p>
    </header>

    <div class="instructions p-6 rounded-lg shadow-lg mb-10 bg-white">
        <h2 class="text-2xl font-bold text-gray-800 mb-3 text-red-600">🛑 Critical Installation Steps</h2>
        <ol class="list-decimal list-inside space-y-3 text-gray-700">
            <li>**Try Dragging:** Click and drag the blue link (**e.g., Stealth Mode**) to your bookmarks bar.</li>
            <li>**If Dragging Fails (Most Reliable Method):**
                <ul class="list-disc list-inside ml-5 mt-1 space-y-1">
                    <li>Click the **Copy Code** button next to the utility you want.</li>
                    <li>Right-click on your bookmarks bar and choose **Add Page** or **Add Bookmark**.</li>
                    <li>For the **URL/Address**, **paste the copied code** (it starts with `javascript:`).</li>
                </ul>
            </li>
            <li>Click the new bookmark while viewing **any page** to run the script.</li>
        </ol>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

        <!-- 1. Stealth Mode (Unchanged) -->
        <div class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Stealth Mode (Tab Cloaker)</h3>
            <p class="text-gray-500">Changes the page title and icon to look like a generic Google Drive document.</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="stealth-mode-link" href="javascript:(function(){document.title='My Drive - Google Drive';var l=document.querySelector('link[rel*=\'icon\']')||document.createElement('link');l.type='image/x-icon';l.rel='shortcut icon';l.href='data:image/svg+xml,<svg viewBox=\'0 0 100 100\' xmlns=\'http://www.w3.org/2000/svg\'><text y=\'.9em\' font-size=\'90\'>G</text></svg>';document.getElementsByTagName('head')[0].appendChild(l);})();" 
                   class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Stealth Mode
                </a>
                <button onclick="copyToClipboard('stealth-mode-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>

        <!-- 2. Dev Tools Injector (REVISED) -->
        <div class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Dev Tools Unlock (REVISED)</h3>
            <p class="text-gray-500">Aggressively tries to re-enable F12, right-click, and common inspection keyboard shortcuts.</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="dev-tools-link" href="javascript:(function(){document.addEventListener('contextmenu',e=>e.stopPropagation(),true);document.addEventListener('keydown',e=>{if(e.key==='F12'||(e.ctrlKey&&e.shiftKey&&(e.key==='I'||e.key==='J'||e.key==='C'))||(e.ctrlKey&&e.key==='u')){e.stopPropagation();e.preventDefault();}},true);if(window.oncontextmenu)window.oncontextmenu=null;if(window.onkeydown)window.onkeydown=null;})();" 
                   class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Dev Tools Unlock
                </a>
                <button onclick="copyToClipboard('dev-tools-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>

        <!-- 3. History Flooder (REVISED) -->
        <div class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">History Flooder (REVISED)</h3>
            <p class="text-gray-500">Adds 100 entries to your history using generic web searches, without using alerts.</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="history-flooder-link" href="javascript:(function(){var u=['https://www.google.com/search?q=weather+today','https://en.wikipedia.org/wiki/Main_Page','https://www.google.com/search?q=cute+dog+pictures','https://www.nasa.gov/','https://www.nationalgeographic.com/'];var c=100;var s={page:'filler',time:Date.now()};var p=0;for(var i=0;i<c;i++){var url=u[Math.floor(Math.random()*u.length)];try{history.pushState(s,'',url+'&_='+i);p++;}catch(e){break;}}console.log('History Flooded with '+p+' entries.');})();" 
                   class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    History Flooder
                </a>
                <button onclick="copyToClipboard('history-flooder-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>

        <!-- 4. Quick Search (Unchanged) -->
        <div class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Quick Search</h3>
            <p class="text-gray-500">Prompts for a search term and opens Google results in a new, unblocked window.</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="quick-search-link" href="javascript:(function(){var q=prompt('Enter search term (e.g., \'unblocked games site\'):','unblocked games');if(q){var s='https://www.google.com/search?q='+encodeURIComponent(q);window.open(s,'_blank');}})();" 
                   class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Quick Search
                </a>
                <button onclick="copyToClipboard('quick-search-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>
        
        <!-- 5. New Tab URL Opener (REPLACED MINI-BROWSER) -->
        <div class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">New Tab URL Opener (NEW)</h3>
            <p class="text-gray-500">Replaces the blocked mini-browser by opening a provided URL in a standard new tab.</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="new-tab-link" href="javascript:(function(){var u=prompt('Enter URL to open (e.g., duckduckgo.com):','https://');if(u){if(!u.startsWith('http')){u='https://'+u;}window.open(u,'_blank');}})();" 
                   class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    New Tab URL Opener
                </a>
                <button onclick="copyToClipboard('new-tab-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>

        <!-- 6. Crash Simulator (NEW FEATURE) -->
        <div class="bookmarklet-card bg-red-50 p-6 rounded-xl shadow-md flex flex-col space-y-3 border-red-500">
            <h3 class="text-2xl font-bold text-red-700">⚠️ Crash Simulator (NEW)</h3>
            <p class="text-red-600 font-semibold">**WARNING:** This script intentionally locks up the browser tab using an infinite loop. **You must close the tab manually to recover.**</p>
            <div class="action-container flex space-x-4 pt-2">
                <a id="crash-sim-link" href="javascript:(function(){var d=document;var a=d.createElement('div');a.style='position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(255,0,0,0.8);color:white;text-align:center;padding-top:10%;font-size:3em;z-index:999999;font-family:sans-serif;';a.innerHTML='ATTEMPTING SYSTEM CRASH... CLOSE TAB NOW!';d.body.appendChild(a);let i=0,arr=[];for(i=0;i<1000000;i++){arr.push(Math.random().toString(36).substring(2, 15));}while(true){};})();" 
                   class="text-sm font-semibold text-white bg-red-500 hover:bg-red-600 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Crash Simulation
                </a>
                <button onclick="copyToClipboard('crash-sim-link')" class="text-sm font-semibold text-gray-700 bg-gray-200 hover:bg-gray-300 px-4 py-2 rounded-lg text-center w-full transition duration-150">
                    Copy Code
                </button>
            </div>
        </div>
    </div>

</div>

<!-- Hidden textarea for reliable copy functionality -->
<textarea id="temp-clipboard" class="hidden-textarea"></textarea>

<script>
    /**
     * Copies the href attribute of the specified element ID to the clipboard.
     * Uses the document.execCommand('copy') fallback method for iframe compatibility.
     * @param {string} elementId - The ID of the <a> tag whose href should be copied.
     */
    function copyToClipboard(elementId) {
        const linkElement = document.getElementById(elementId);
        if (!linkElement) {
            console.error('Link element not found:', elementId);
            return;
        }

        const bookmarkletCode = linkElement.href;
        
        // Use a hidden textarea to hold the text for copying
        const tempTextArea = document.getElementById('temp-clipboard');
        tempTextArea.value = bookmarkletCode;
        tempTextArea.select();
        
        try {
            const successful = document.execCommand('copy');
            if (successful) {
                // Flash a success message
                const button = linkElement.nextElementSibling;
                const originalText = button.textContent;
                button.textContent = 'Copied!';
                button.classList.remove('bg-gray-200');
                button.classList.add('bg-green-500', 'text-white');
                
                setTimeout(() => {
                    button.textContent = originalText;
                    button.classList.remove('bg-green-500', 'text-white');
                    button.classList.add('bg-gray-200');
                }, 1500);
            } else {
                // Fallback if execCommand fails
                console.error('Copy command failed.');
                alert('Copying failed. Please manually select the code from the console.');
            }
        } catch (err) {
            console.error('Unable to copy using execCommand:', err);
            // Fallback for extreme restrictions
            alert('The code is: ' + bookmarkletCode + '. Please copy it manually.');
        }

        // Deselect the text
        tempTextArea.blur();
    }
</script>

</body>
</html>
