# Steps to use Solver for project-2 (Q3)
## Step 1: Data fetching
1. Go to our Assignment portal and wait for it to reolad all questions
2. Press F12 and Go to console
3. Paste given script in console and hit enter.
```
/* OMEGA PORTAL SIPHON v5.1 (Aggressive Q3 Search) */
(function() {
    console.log("%c CRYPTO-TRACE DISCOVERY ACTIVE v5.1 ", "background: #101723; color: #d9ecff; font-weight: bold;");
    
    const user = JSON.parse(localStorage.getItem('user'));
    if (!user) { console.error("Identity not found."); return; }

    let q3Data = {
        email: user.email,
        quizSign: user.quizSign,
        type: "q3_qr_trace",
        maskedSignature: "",
        qrSvg: ""
    };

    const harvest = (doc) => {
        // Look for the QR SVG by ID
        const svgElement = doc.querySelector('svg#damaged-qr');
        // Look for the Masked Signature by the specific class
        const codeElement = doc.querySelector('.masked code');

        if (svgElement && codeElement) {
            q3Data.qrSvg = svgElement.outerHTML;
            q3Data.maskedSignature = codeElement.innerText.trim();
            return true;
        }
        return false;
    };

    // 1. Check the main document first
    let found = harvest(document);

    // 2. If not found, check all iframes
    if (!found) {
        document.querySelectorAll('iframe').forEach(frame => {
            try {
                const frameDoc = frame.contentDocument || frame.contentWindow.document;
                if (harvest(frameDoc)) {
                    found = true;
                    console.log("%c Found Q3 data in frame: " + (frame.id || frame.name || "unnamed"), "color: #0f0;");
                }
            } catch(e) {}
        });
    }

    if (found) {
        console.log("%c Q3 DATA CAPTURED SUCCESSFULLY ", "color: #0ff; font-weight: bold;");
        console.log(JSON.stringify(q3Data, null, 2));
    } else {
        console.error("CAPTURE FAILED: Could not find the Damaged QR or the Masked Signature. Ensure the Q3 mission is visible on your screen.");
    }
})();
```

4. You will see json format data. eg.
```
{
  "email": "xyz@ds.study.iitm.ac.in",
  "quizSign": "xyz24ur340....",
  "type": "q3_qr_trace",
  "maskedSignature": "3ojRgrCfAFaRSZJ8ybvv4fZWr8bvnioadyQryqnU6Je6qLc5EcH-------jN8UhS9SjcFUGDZqe4",
  "qrSvg": "<svg id=\"damaged-qr\" xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"0 0 406 406\" role=\"img\" aria-lab
  el=\"Damaged QR code containing a seven-character Solana signature fragment\"><rect w
  idth=\"406\" height=\"406\" fill=\"#ffffff\"></rect><path d=\"M56,56h14v14h-14z M70,
  56h14v14h-14z M84,56h14v14h-14z M98,56h14v14h-14z M112,56h14v14h-14z M126,............"}
    
```
5. Copy that json data correctly like given above..

## Step 2: Solver 

1. Go to https://p2-solver.onrender.com/
2. Then Click on Q3
3. There will be an empty box, put there your copied data
4. And then click on "Execute".. 
5. 💥BOOOOOMMM!! your answer will be shown in correct format.. just copy and paste that in portal.. 
