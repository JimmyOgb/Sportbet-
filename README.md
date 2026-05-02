<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BetCode Generator - Sports Betting Tool</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f172a, #1e2937);
            color: #e2e8f0;
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: #1e2937;
            border-radius: 16px;
            padding: 30px;
            box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.3);
        }
        h1 {
            text-align: center;
            color: #22d3ee;
            margin-bottom: 10px;
        }
        .subtitle {
            text-align: center;
            color: #94a3b8;
            margin-bottom: 30px;
        }
        .match {
            background: #334155;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 15px;
        }
        input, select, button {
            padding: 12px;
            border-radius: 8px;
            border: none;
            margin: 5px 0;
        }
        input, select {
            background: #475569;
            color: white;
            width: 100%;
        }
        button {
            background: #22d3ee;
            color: #0f172a;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }
        button:hover {
            background: #67e8f9;
            transform: translateY(-2px);
        }
        .bet-slip {
            background: #1e2937;
            border: 2px solid #22d3ee;
            padding: 20px;
            border-radius: 12px;
            margin-top: 30px;
        }
        .code {
            font-family: monospace;
            font-size: 1.5rem;
            background: #0f172a;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            letter-spacing: 4px;
            color: #67e8f9;
        }
        .odds {
            color: #a5f3fc;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>⚽ BetCode Generator</h1>
        <p class="subtitle">Simple Sports Betting Slip Builder • Ready for GitHub Pages</p>

        <div id="matches">
            <!-- Matches added dynamically -->
        </div>

        <button onclick="addMatch()" style="width: 100%; padding: 15px; font-size: 1.1rem;">
            ➕ Add Match
        </button>

        <div class="bet-slip">
            <h2>Your Booking Code</h2>
            <div id="generated-code" class="code">BET-XXXX-XXXX</div>
            <p style="text-align: center; margin: 15px 0; color: #94a3b8;">
                Total Odds: <span id="total-odds" class="odds">1.00</span>
            </p>
            <button onclick="generateCode()" style="width: 100%; margin-top: 10px;">
                Generate Booking Code
            </button>
        </div>

        <div style="margin-top: 30px; text-align: center; font-size: 0.9rem; color: #64748b;">
            Open Source • Host on GitHub Pages • Free to use
        </div>
    </div>

    <script>
        let matchCount = 0;

        function addMatch() {
            matchCount++;
            const matchesDiv = document.getElementById('matches');
            
            const matchHTML = `
                <div class="match" id="match-${matchCount}">
                    <input type="text" placeholder="Match (e.g. Man City vs Arsenal)" id="team-${matchCount}">
                    <select id="prediction-${matchCount}">
                        <option value="">Select Prediction</option>
                        <option value="1">1 - Home Win</option>
                        <option value="X">X - Draw</option>
                        <option value="2">2 - Away Win</option>
                        <option value="Over 2.5">Over 2.5 Goals</option>
                        <option value="Under 2.5">Under 2.5 Goals</option>
                    </select>
                    <input type="number" step="0.01" placeholder="Odds (e.g. 2.15)" id="odds-${matchCount}" value="2.00">
                    <button onclick="removeMatch(${matchCount})" style="background: #ef4444; color: white; width: auto; padding: 8px 12px; margin-top: 8px;">
                        Remove
                    </button>
                </div>
            `;
            matchesDiv.innerHTML += matchHTML;
        }

        function removeMatch(id) {
            const match = document.getElementById(`match-${id}`);
            if (match) match.remove();
        }

        function calculateTotalOdds() {
            let total = 1;
            document.querySelectorAll('input[id^="odds-"]').forEach(input => {
                const odds = parseFloat(input.value) || 1;
                total *= odds;
            });
            return total.toFixed(2);
        }

        function generateCode() {
            const matches = [];
            let valid = true;

            document.querySelectorAll('.match').forEach(match => {
                const id = match.id.split('-')[1];
                const team = document.getElementById(`team-${id}`).value.trim();
                const pred = document.getElementById(`prediction-${id}`).value;
                const odds = document.getElementById(`odds-${id}`).value;

                if (!team || !pred) {
                    valid = false;
                }

                matches.push({
                    team: team || "Unknown",
                    prediction: pred || "N/A",
                    odds: odds
                });
            });

            if (!valid || matches.length === 0) {
                alert("Please add at least one complete match!");
                return;
            }

            // Generate random-looking booking code
            const prefix = ["BK", "BET", "SLIP", "GG"][Math.floor(Math.random() * 4)];
            const code = `\( {prefix} \){Math.floor(100000 + Math.random() * 900000)}-${Math.floor(1000 + Math.random() * 9000)}`;

            document.getElementById('generated-code').textContent = code;
            document.getElementById('total-odds').textContent = calculateTotalOdds();

            // Optional: Console log for copying to real bookmaker
            console.log("=== BET SLIP ===");
            matches.forEach(m => {
                console.log(`${m.team} - ${m.prediction} @ ${m.odds}`);
            });
            console.log(`Booking Code: ${code}`);
            console.log(`Total Odds: ${calculateTotalOdds()}`);
        }

        // Add one default match when page loads
        window.onload = () => {
            addMatch();
        };
    </script>
</body>
</html>
