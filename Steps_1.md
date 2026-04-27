# Steps to use Solver for project-2
## Step 1: Data fetching
1. Go to our Assignment portal and wait for it to reolad all questions
2. Press F12 and Go to console
3. Paste given script in console and hit enter.
```
/* OMEGA PORTAL SIPHON v4.1 (Onion-Server Targeted) */
(function() {
    console.log("%c SINGULARITY DISCOVERY ACTIVE v4.1 ", "background: #000; color: #0f0; font-weight: bold;");
    
    const user = JSON.parse(localStorage.getItem('user'));
    if (!user) { console.error("Identity not found. Please log in first."); return; }

    let results = {
        email: user.email,
        quizSign: user.quizSign,
        mission: []
    };

    const harvest = (doc) => {
        // Look for the standard task structure inside the target frame
        doc.querySelectorAll('.question-item').forEach(item => {
            let num = item.querySelector('.q-num')?.innerText.trim() || "";
            let theme = item.querySelector('.q-theme')?.innerText.trim() || "";
            let query = item.querySelector('.q-text')?.innerText.trim() || "";
            let link = item.querySelector('.q-link')?.href || "";
            
            let folder = null;
            if (link) {
                let match = link.match(/\.onion\/(\d+)\//);
                if (match) folder = parseInt(match[1]);
            }

            if (num) {
                results.mission.push({ num, theme, query, folder, link });
            }
        });
    };

    // --- NEW TARGETED SELECTION ---
    // We look for the iframe by ID or Name: 'q-onion-scrape-server' or 'questionId'
    const selectors = [
        'iframe#q-onion-scrape-server',
        'iframe[name="q-onion-scrape-server"]',
        'iframe#questionId',
        'iframe[name="questionId"]'
    ];
    
    let targetFrame = null;
    for (let selector of selectors) {
        targetFrame = document.querySelector(selector);
        if (targetFrame) break;
    }
    
    if (targetFrame) {
        console.log("%c Target Frame Locked: " + (targetFrame.id || targetFrame.name), "color: #0f0; font-weight: bold;");
        try {
            harvest(targetFrame.contentDocument || targetFrame.contentWindow.document);
        } catch(e) {
            console.error("Access blocked by browser security (CORS). Try running this script while the iframe is focused.");
        }
    } else {
        // Absolute fallback: Search all iframes but ONLY harvest the one containing '.onion'
        console.warn("Target ID not found. Searching for Onion-linked frames...");
        document.querySelectorAll('iframe').forEach(frame => {
            try {
                const frameDoc = frame.contentDocument || frame.contentWindow.document;
                if (frameDoc.body.innerHTML.includes('.onion')) {
                    console.log("%c Auto-detected Onion Frame!", "color: #0ff;");
                    harvest(frameDoc);
                }
            } catch(e) {}
        });
    }

    if (results.mission.length === 0) {
        console.warn("CAPTURE FAILED: No tasks found in the 'q-onion-scrape-server' frame.");
    } else {
        console.log("%c SUCCESS: Q1 DATA EXTRACTED ", "color: #0ff; font-weight: bold;");
        console.log(JSON.stringify(results, null, 2));
    }
})();

```

4. You will see json format data. eg.
```
{
  "email": "xyz@ds.study.iitm.ac.in",
  "quizSign": "xyz24ur340....",
  "mission": [
    {
      "num": "TASK 1",
      "theme": "E-COMMERCE",
      "query": "What is the total combined inventory value (current_price * stock) for all products in the \"electronics\" category? (Provide answer rounded to 2 decimal places)",
      "folder": 27,
      "link": "http://tds26vu3ptapxx6igo6n26kuwfpn2l5omkmagc4hc7g7yn2o3xb25syd.onion/27/cat/electronics/index.html"
    },
    .........
    .........
    {
      "num": "TASK 12",
      "theme": "FORUM",
      "query": "....",
      "folder": 25,
      "link": "http://tds26vu3ptapxx6igo6n26kuwfpn2l5omkmagc4hc7g7yn2o3xb25syd.onion/25/b/leaks/index.html"
    }
  ]
}
```
5. Copy that json data correctly like given above..

## Step 2: Solver 

1. Go to https://p2-solver.onrender.com/
2. Then Click on Q1
3. There will be an empty box, put there your copied data
4. And then click on "Execute".. 
5. 💥BOOOOOMMM!! your answer will be shown in correct format.. just copy and paste that in portal.. 
6. 12/12 is yours.🎉🎉
