<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neural Beauty Analyzer v2.1</title>
    <style>
        :root {
            --gold: #d4af37;
            --purple: #bc13fe;
            --cyber-blue: #00d4ff;
            --bg: #050505;
        }

        body {
            background-color: var(--bg);
            color: #fff;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
            transition: background 2s ease;
        }

        #scanner-box {
            position: relative;
            border: 1px solid rgba(212, 175, 55, 0.3);
            padding: 40px;
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(15px);
            border-radius: 30px;
            text-align: center;
            box-shadow: 0 0 40px rgba(0, 0, 0, 0.5);
            width: 85%;
            max-width: 440px;
            z-index: 10;
        }

        .scan-container {
            height: 180px;
            border: 1px solid rgba(212, 175, 55, 0.2);
            margin: 25px 0;
            position: relative;
            overflow: hidden;
            border-radius: 12px;
            background: rgba(0,0,0,0.5);
        }

        .scan-line {
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, transparent, var(--gold), transparent);
            position: absolute;
            top: 0;
            animation: scanMove 2.8s infinite ease-in-out;
            box-shadow: 0 0 20px var(--gold);
        }

        /* Animated braid weave */
        .braid-weave {
            position: absolute;
            top: 40px;
            left: 50%;
            transform: translateX(-50%);
            width: 140px;
            height: 80px;
            display: flex;
            justify-content: space-around;
            opacity: 0.7;
        }

        .strand {
            width: 6px;
            background: linear-gradient(#ff69b4, #9370db, #00fa9a);
            animation: braidTwist 3s infinite alternate ease-in-out;
        }

        .strand:nth-child(2) { animation-delay: 0.3s; height: 92px; }
        .strand:nth-child(3) { animation-delay: 0.6s; }

        @keyframes scanMove {
            0%, 100% { top: 0%; }
            50% { top: 95%; }
        }

        @keyframes braidTwist {
            from { transform: rotate(-12deg) translateY(0); }
            to { transform: rotate(12deg) translateY(8px); }
        }

        button {
            background: linear-gradient(45deg, var(--gold), #f9e295);
            color: #000;
            border: none;
            padding: 15px 35px;
            font-weight: bold;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 2px;
            border-radius: 50px;
            cursor: pointer;
            transition: 0.3s;
            box-shadow: 0 5px 15px rgba(212, 175, 55, 0.4);
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(212, 175, 55, 0.6);
        }

        .hidden { display: none; }

        .rainbow-bg {
            background: linear-gradient(-45deg, #050505, #1a0033, #001a33, #050505);
            background-size: 400% 400%;
            animation: gradientMove 8s ease infinite;
        }

        @keyframes gradientMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        #stats-log {
            text-align: left;
            font-family: 'Courier New', monospace;
            font-size: 13px;
            color: var(--cyber-blue);
            margin-top: 15px;
            line-height: 1.7;
        }

        .glow-text {
            color: var(--gold);
            text-shadow: 0 0 12px var(--gold);
            font-size: 1.45rem;
            animation: glitch 1.5s infinite alternate;
        }

        @keyframes glitch {
            0% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(2px, -2px); }
            100% { transform: translate(0); }
        }

        .heart-icon {
            font-size: 65px;
            margin-bottom: 20px;
            animation: pulse 1.2s infinite alternate;
        }

        @keyframes pulse { from { transform: scale(1); } to { transform: scale(1.18); } }
    </style>
</head>
<body id="main-body">

    <div id="scanner-box">
        <!-- Screen 1: Ready -->
        <div id="screen-1">
            <h2 style="letter-spacing: 4px; margin-bottom: 8px;">NEURAL BEAUTY ANALYZER v2.1</h2>
            <p style="font-size: 11px; color: #888; margin-bottom: 25px;">HAIR INTEGRITY • VISUAL PROCESSING MODULE</p>
            
            <div class="scan-container">
                <div class="scan-line"></div>
                <div class="braid-weave">
                    <div class="strand"></div>
                    <div class="strand"></div>
                    <div class="strand"></div>
                </div>
                <div style="margin-top: 115px; color: var(--gold); font-weight: bold; font-size: 13px;">
                    TARGET ACQUIRED: NEW BRAIDS DETECTED
                </div>
            </div>

            <button onclick="startAnalysis()">RUN STYLE ANALYSIS</button>
        </div>

        <!-- Screen 2: Analyzing -->
        <div id="screen-2" class="hidden">
            <h3 style="color: var(--gold);">ANALYZING BRAID INTEGRITY...</h3>
            <div id="stats-log"></div>
        </div>

        <!-- Screen 3: Final Result -->
        <div id="screen-3" class="hidden">
            <div class="heart-icon">💇‍♀️✨</div>
            <h2 class="glow-text">ANALYSIS COMPLETE</h2>
            <p style="font-size: 1.25rem; line-height: 1.65; color: #fff; margin: 20px 0;">
                System confirms: The new braids are a <span style="color: var(--cyber-blue); font-weight: bold;">perfect 10/10 compilation</span>.<br><br>
                Zero bugs. Flawless symmetry. The way the strands interweave with zero merge conflicts? 
                Absolute chef's kiss. You didn't just do your hair — you deployed pure beauty.
            </p>
            <p style="font-size: 13px; color: rgba(255,255,255,0.6); margin-top: 30px;">
                Verified by: Your secret IT admirer ❤️
            </p>
        </div>
    </div>

    <script>
        function startAnalysis() {
            document.getElementById('screen-1').classList.add('hidden');
            document.getElementById('screen-2').classList.remove('hidden');

            const log = document.getElementById('stats-log');
            const lines = [
                "> Initializing high-res visual scanner...",
                "> Detecting hair symmetry... 100%",
                "> Analyzing braid precision: No loose ends detected",
                "> Cross-referencing with known IT girl standards...",
                "> Warning: Beauty overflow error...",
                "> Compiling final compliment module..."
            ];

            let i = 0;
            const interval = setInterval(() => {
                const p = document.createElement('div');
                p.innerText = lines[i];
                log.appendChild(p);
                log.scrollTop = log.scrollHeight;
                i++;
                if (i >= lines.length) {
                    clearInterval(interval);
                    setTimeout(showFinal, 1200);
                }
            }, 850);
        }

        function showFinal() {
            document.getElementById('screen-2').classList.add('hidden');
            document.getElementById('screen-3').classList.remove('hidden');
            document.getElementById('main-body').classList.add('rainbow-bg');
            
            const box = document.getElementById('scanner-box');
            box.style.borderColor = "var(--cyber-blue)";
            box.style.boxShadow = "0 0 55px rgba(0, 212, 255, 0.35)";
        }
    </script>
</body>
</html>
