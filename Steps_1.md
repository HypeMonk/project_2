# Steps to use Solver for project-2
## Step 1: Data fetching
1. Go to our Assignment portal and wait for it to reolad all questions
2. Press F12 and Go to console
3. Paste given script in console and hit enter.
```
/* OMEGA PORTAL SIPHON v3.0 (Absolute Extraction) */
(function() {
    console.log("%c SINGULARITY DISCOVERY ACTIVE v3.0 ", "background: #000; color: #0f0; font-weight: bold;");
   
    const user = JSON.parse(localStorage.getItem('user'));
    if (!user) { console.error("Identity not found. Please log in first."); return; }

    let results = {
        email: user.email,
        quizSign: user.quizSign,
        mission: []
    };

    // Deep search function using the portal's specific CSS classes
    const harvest = (doc) => {
        doc.querySelectorAll('.question-item').forEach(item => {
            let num = item.querySelector('.q-num')?.innerText.trim() || "";
            let theme = item.querySelector('.q-theme')?.innerText.trim() || "";
            let query = item.querySelector('.q-text')?.innerText.trim() || "";
            let link = item.querySelector('.q-link')?.href || "";
           
            // Extract the Folder ID from the .onion URL pattern
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

    // Search main page and all internal iframes
    harvest(document);
    document.querySelectorAll('iframe').forEach(frame => {
        try {
            harvest(frame.contentDocument || frame.contentWindow.document);
        } catch(e) {}
    });

    if (results.mission.length === 0) {
        console.warn("No tasks found. Ensure the 'questionData' iframe is visible on your screen and run the script again.");
    } else {
        console.log("%c MISSION DATA CAPTURED: ", "color: #0ff; font-weight: bold;");
        console.log(JSON.stringify(results, null, 2));
        console.log("%c Copy this JSON into the Python Solver Hub. ", "color: #aaa;");
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
