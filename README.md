<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GCTU | Aesthetic Recognition Lab</title>
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

        /* Glassmorphism Container */
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
            max-width: 420px;
            z-index: 10;
        }

        /* Animated Scan Line */
        .scan-container {
            height: 150px;
            border: 1px solid rgba(212, 175, 55, 0.2);
            margin: 25px 0;
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            background: rgba(0,0,0,0.4);
        }

        .scan-line {
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, transparent, var(--gold), transparent);
            position: absolute;
            top: 0;
            animation: scanMove 2.5s infinite ease-in-out;
            box-shadow: 0 0 20px var(--gold);
        }

        @keyframes scanMove {
            0%, 100% { top: 0%; }
            50% { top: 95%; }
        }

        /* Buttons */
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

        /* Final Colorful State */
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
            line-height: 1.6;
        }

        .glow-text {
            color: var(--gold);
            text-shadow: 0 0 10px var(--gold);
            font-size: 1.4rem;
        }

        .heart-icon {
            font-size: 60px;
            margin-bottom: 20px;
            display: inline-block;
            animation: pulse 1s infinite alternate;
        }

        @keyframes pulse { from { transform: scale(1); } to { transform: scale(1.15); } }
    </style>
</head>
<body id="main-body">

    <audio id="bgMusic" loop>
        <source src="song.mp3" type="audio/mpeg">
    </audio>

    <div id="scanner-box">
        <div id="screen-1">
            <h2 style="letter-spacing: 4px; margin-bottom: 5px;">AESTHETIC V.2</h2>
            <p style="font-size: 10px; color: #888; margin-bottom: 20px;">GCTU VISUAL RECOGNITION MODULE</p>
            
            <div class="scan-container">
                <div class="scan-line"></div>
                <div style="margin-top: 60px; color: var(--gold); font-weight: bold; font-size: 12px;">READY TO ANALYZE...</div>
            </div>

            <button onclick="startAnalysis()">Run Style Check</button>
        </div>

        <div id="screen-2" class="hidden">
            <h3 style="color: var(--gold);">ANALYZING...</h3>
            <div id="stats-log"></div>
        </div>

        <div id="screen-3" class="hidden">
            <div class="heart-icon">✨</div>
            <h2 class="glow-text">ANALYSIS COMPLETE</h2>
            <p style="font-size: 1.2rem; line-height: 1.6; color: #fff;">
                System confirms: The new braids are a <span style="color: var(--cyber-blue); font-weight: bold;">10/10 masterpiece</span>. 
                <br><br>
                It’s not just the hair, though—it’s how it perfectly frames your face. You look absolutely stunning.
            </p>
            <p style="font-size: 12px; color: rgba(255,255,255,0.5); margin-top: 25px;">Verified by: Sefa</p>
        </div>
    </div>

    <script>
        function startAnalysis() {
            // Start Music
            const music = document.getElementById('bgMusic');
            music.play().catch(e => console.log("Audio waiting..."));

            document.getElementById('screen-1').classList.add('hidden');
            document.getElementById('screen-2').classList.remove('hidden');

            const log = document.getElementById('stats-log');
            const lines = [
                "> Calibrating lens for high-res...",
                "> Detecting hair symmetry...",
                "> Analyzing braid precision: 100%",
                "> Error: Beauty levels exceeding limits...",
                "> Compiling final compliment..."
            ];

            let i = 0;
            const interval = setInterval(() => {
                const p = document.createElement('div');
                p.innerText = lines[i];
                log.appendChild(p);
                i++;
                if (i >= lines.length) {
                    clearInterval(interval);
                    setTimeout(showFinal, 1000);
                }
            }, 900);
        }

        function showFinal() {
            document.getElementById('screen-2').classList.add('hidden');
            document.getElementById('screen-3').classList.remove('hidden');
            document.getElementById('main-body').classList.add('rainbow-bg');
            document.getElementById('scanner-box').style.borderColor = "var(--cyber-blue)";
            document.getElementById('scanner-box').style.boxShadow = "0 0 50px rgba(0, 212, 255, 0.3)";
        }
    </script>
</body>
</html>
