# bookmarks
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Utility Bookmarklet Hub</title>
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
            width: 1000px;
        }
        /* Custom card styling for visual appeal */
        .bookmarklet-card {
            transition: all 0.3s ease-in-out;
            cursor: move; /* Indicate drag-and-drop */
            border: 2px solid transparent;
        }
        .bookmarklet-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
            border-color: #4c56e0;
        }
        .instructions {
            background-color: #ffffff;
            border-left: 5px solid #4c56e0;
        }
    </style>
</head>
<body>

<div class="container mx-auto p-4 sm:p-10">

    <header class="text-center mb-10">
        <h1 class="text-5xl font-extrabold text-gray-900 mb-4">
            Utility Bookmarklet Hub
        </h1>
        <p class="text-lg text-gray-600">
            Drag the links below directly to your browser's bookmarks bar to install them.
        </p>
    </header>

    <div class="instructions p-6 rounded-lg shadow-lg mb-10 bg-white">
        <h2 class="text-2xl font-bold text-gray-800 mb-3">How to Install ⚙️</h2>
        <ul class="list-disc list-inside space-y-2 text-gray-700">
            <li>To install a tool, **click and drag** the blue link (e.g., "**Stealth Mode**") below to your browser's bookmarks bar.</li>
            <li>Click the new bookmark while viewing **any page** to activate the script.</li>
            <li>*Note:* Since these are single-line bookmarklets, feedback will be minimal (e.g., Console log or simple prompts).</li>
        </ul>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">

        <!-- 1. Stealth Mode -->
        <a href="javascript:(function(){document.title='My Drive - Google Drive';var l=document.querySelector('link[rel*=\'icon\']')||document.createElement('link');l.type='image/x-icon';l.rel='shortcut icon';l.href='data:image/svg+xml,<svg viewBox=\'0 0 100 100\' xmlns=\'http://www.w3.org/2000/svg\'><text y=\'.9em\' font-size=\'90\'>G</text></svg>';document.getElementsByTagName('head')[0].appendChild(l);console.log('Tab cloaked.');})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Stealth Mode (Tab Cloaker)</h3>
            <p class="text-gray-500">Changes the page title and icon to look like a generic Google Drive document.</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                Stealth Mode
            </span>
        </a>

        <!-- 2. Dev Tools Injector -->
        <a href="javascript:(function(){document.addEventListener('contextmenu',e=>e.stopPropagation(),true);document.addEventListener('keydown',e=>{if(e.key==='F12'){e.stopPropagation();}},true);if(window.oncontextmenu)window.oncontextmenu=null;if(window.onkeydown)window.onkeydown=null;console.log('Dev tools unlocked.');})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Dev Tools Injector</h3>
            <p class="text-gray-500">Attempts to re-enable F12/Inspect Element and right-click menus on restricted pages.</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                Dev Tools Unlock
            </span>
        </a>

        <!-- 3. History Flooder -->
        <a href="javascript:(function(){var u=['https://www.google.com/search?q=weather+today','https://en.wikipedia.org/wiki/Main_Page','https://www.google.com/search?q=cute+cat+videos','https://www.nasa.gov/','https://www.nationalgeographic.com/magazine/'];var c=100;var s={page:'filler',time:Date.now()};var p=0;for(var i=0;i<c;i++){var url=u[Math.floor(Math.random()*u.length)];try{history.pushState(s,'',url+'&_='+i);p++;}catch(e){break;}}console.log('History Flooded with '+p+' entries.');})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">History Flooder</h3>
            <p class="text-gray-500">Adds 100 random, innocuous entries to your browser history to obscure recent activity.</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                History Flooder
            </span>
        </a>
        
        <!-- 4. Quick Search -->
        <a href="javascript:(function(){var q=prompt('Enter search term (e.g., \'unblocked games site\'):','unblocked games');if(q){var s='https://www.google.com/search?q='+encodeURIComponent(q);window.open(s,'_blank');}})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Quick Search</h3>
            <p class="text-gray-500">Prompts for a search term and opens Google results in a new, unblocked window.</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                Quick Search
            </span>
        </a>

        <!-- 5. Full Screen Toggle -->
        <a href="javascript:(function(){if(!document.fullscreenElement){document.documentElement.requestFullscreen().catch(err=>console.error(err));}else{if(document.exitFullscreen){document.exitFullscreen();}}})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Full Screen Toggle</h3>
            <p class="text-gray-500">Forces the current page into native full-screen mode (Press ESC to exit).</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                Full Screen Toggle
            </span>
        </a>

        <!-- 6. Simple Mini Browser (iFrame Injector) -->
        <a href="javascript:(function(){var url=prompt('Enter URL to load:','https://news.google.com');if(url){if(!url.startsWith('http')){url='https://'+url;}var i=document.createElement('iframe');i.src=url;i.style='position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);width:600px;height:400px;border:5px solid #4c56e0;border-radius:12px;z-index:99999;box-shadow:0 10px 25px rgba(0,0,0,0.3);';document.body.appendChild(i);}})();" 
           class="bookmarklet-card bg-white p-6 rounded-xl shadow-md flex flex-col space-y-3">
            <h3 class="text-2xl font-bold text-gray-800">Simple Mini Browser (iFrame)</h3>
            <p class="text-gray-500">Injects a simple, centered iframe on the page to browse a custom URL.</p>
            <span class="text-sm font-semibold text-white bg-blue-500 hover:bg-blue-600 px-4 py-2 rounded-lg text-center w-48">
                Simple Mini Browser
            </span>
        </a>
    </div>

</div>
</body>
</html>
