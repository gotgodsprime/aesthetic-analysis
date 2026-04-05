<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neural Face & Braid Scanner v2.1</title>
    <style>
        :root {
            --gold: #d4af37;
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
            max-width: 460px;
            z-index: 10;
        }

        .scan-container {
            height: 200px;
            border: 1px solid rgba(212, 175, 55, 0.2);
            margin: 25px 0;
            position: relative;
            overflow: hidden;
            border-radius: 12px;
            background: rgba(0,0,0,0.6);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .scan-line {
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, transparent, var(--gold), transparent);
            position: absolute;
            top: 0;
            animation: scanMove 2.8s infinite ease-in-out;
            box-shadow: 0 0 25px var(--gold);
        }

        /* Simple face + braid placeholder */
        .face-placeholder {
            width: 110px;
            height: 140px;
            border: 3px solid rgba(255,255,255,0.2);
            border-radius: 50% 50% 40% 40%;
            position: relative;
            background: rgba(255,255,255,0.08);
        }

        .face-placeholder::before {
            content: '';
            position: absolute;
            top: 45px;
            left: 50%;
            transform: translateX(-50%);
            width: 70px;
            height: 25px;
            background: linear-gradient(#ff69b4, #9370db);
            border-radius: 10px;
            opacity: 0.6;
        }

        @keyframes scanMove {
            0%, 100% { top: 0%; }
            50% { top: 95%; }
        }

        button {
            background: linear-gradient(45deg, var(--gold), #f9e295);
            color: #000;
            border: none;
            padding: 15px 40px;
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
            font-size: 13.5px;
            color: var(--cyber-blue);
            margin-top: 15px;
            line-height: 1.75;
        }

        .glow-text {
            color: var(--gold);
            text-shadow: 0 0 12px var(--gold);
            font-size: 1.5rem;
            animation: glitch 1.5s infinite alternate;
        }

        @keyframes glitch {
            0% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(2px, -2px); }
            100% { transform: translate(0); }
        }

        .heart-icon {
            font-size: 70px;
            margin-bottom: 15px;
            animation: pulse 1.3s infinite alternate;
        }

        @keyframes pulse { from { transform: scale(1); } to { transform: scale(1.2); } }
    </style>
</head>
<body id="main-body">

    <div id="scanner-box">
        <!-- Screen 1: Ready to Scan Face -->
        <div id="screen-1">
            <h2 style="letter-spacing: 4px; margin-bottom: 8px;">NEURAL FACE & BRAID SCANNER v2.1</h2>
            <p style="font-size: 11px; color: #888; margin-bottom: 25px;">FACIAL RECOGNITION + HAIR INTEGRITY MODULE</p>
            
            <div class="scan-container">
                <div class="scan-line"></div>
                <div class="face-placeholder"></div>
                <div style="position: absolute; bottom: 25px; color: var(--gold); font-size: 13px;