<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Batcomputer - Affan bin Hassan</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            color: #00ffff;
            font-family: 'Courier New', monospace;
            overflow: hidden;
            position: relative;
        }

        .grid-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 255, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 255, 255, 0.03) 1px, transparent 1px);
            background-size: 20px 20px;
            pointer-events: none;
            z-index: 1;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 2;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 2px solid #00ffff;
            padding-bottom: 20px;
        }

        .bat-logo {
            width: 150px;
            height: auto;
            margin-bottom: 20px;
            filter: drop-shadow(0 0 10px #00ffff);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .system-time {
            font-size: 48px;
            font-weight: bold;
            text-shadow: 0 0 20px #00ffff;
            margin: 10px 0;
        }

        .system-date {
            font-size: 20px;
            color: #ffd43b;
            margin-bottom: 10px;
        }

        .greeting {
            font-size: 18px;
            color: #ffd43b;
            margin-bottom: 20px;
        }

        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .widget {
            background: rgba(0, 20, 40, 0.8);
            border: 1px solid #00ffff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
            transition: all 0.3s;
        }

        .widget:hover {
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.5);
            transform: translateY(-5px);
        }

        .widget-title {
            font-size: 24px;
            color: #ffd43b;
            margin-bottom: 15px;
            border-bottom: 1px solid #00ffff;
            padding-bottom: 10px;
            text-transform: uppercase;
        }

        .widget-content {
            font-size: 16px;
            line-height: 1.8;
        }

        .stat-row {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            padding: 8px;
            background: rgba(0, 255, 255, 0.1);
            border-radius: 5px;
        }

        .stat-label {
            color: #00ffff;
        }

        .stat-value {
            color: #ffd43b;
            font-weight: bold;
        }

        .quick-links {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }

        .quick-link {
            display: inline-block;
            padding: 10px 20px;
            background: rgba(0, 255, 255, 0.2);
            border: 1px solid #00ffff;
            color: #00ffff;
            text-decoration: none;
            border-radius: 5px;
            transition: all 0.3s;
            cursor: pointer;
        }

        .quick-link:hover {
            background: #00ffff;
            color: #000;
            box-shadow: 0 0 15px #00ffff;
        }

        .weather-info {
            text-align: center;
        }

        .weather-temp {
            font-size: 48px;
            color: #ffd43b;
            margin: 10px 0;
        }

        .weather-condition {
            font-size: 20px;
            margin-bottom: 10px;
        }

        .weather-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
        }

        .mission-status {
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 10px 0;
        }

        .status-indicator {
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background: #32cd32;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        .terminal {
            background: rgba(0, 0, 0, 0.9);
            border: 1px solid #00ffff;
            border-radius: 10px;
            padding: 20px;
            font-family: 'Courier New', monospace;
            height: 300px;
            overflow-y: auto;
        }

        .terminal-line {
            margin: 5px 0;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }

        @keyframes fadeIn {
            to { opacity: 1; }
        }

        .terminal-prompt {
            color: #ffd43b;
        }

        .terminal-text {
            color: #00ffff;
        }

        .profile-section {
            text-align: center;
            margin: 30px 0;
        }

        .profile-name {
            font-size: 32px;
            color: #ffd43b;
            margin-bottom: 10px;
        }

        .profile-title {
            font-size: 20px;
            color: #00ffff;
            margin-bottom: 20px;
        }

        .skills-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .skill-badge {
            padding: 10px 20px;
            background: rgba(255, 212, 59, 0.2);
            border: 1px solid #ffd43b;
            border-radius: 20px;
            color: #ffd43b;
            font-weight: bold;
        }

        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            border-top: 1px solid #00ffff;
            color: #00ffff;
            font-size: 14px;
        }

        @media (max-width: 768px) {
            .system-time {
                font-size: 32px;
            }
            .dashboard {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="grid-overlay"></div>
    
    <div class="container">
        <!-- Header -->
        <div class="header">
            <svg class="bat-logo" viewBox="0 0 100 50" fill="#00ffff">
                <path d="M50 5 C40 15, 35 20, 30 25 C25 20, 20 15, 10 20 C15 25, 20 30, 25 35 C20 40, 15 45, 5 45 C15 45, 25 40, 35 35 C40 40, 45 45, 50 45 C55 45, 60 40, 65 35 C75 40, 85 45, 95 45 C85 45, 80 40, 75 35 C80 30, 85 25, 90 20 C80 15, 75 20, 70 25 C65 20, 60 15, 50 5 Z"/>
            </svg>
            
            <div class="greeting">GOOD EVENING, SIR.</div>
            <div class="system-time" id="clock">00:00:00</div>
            <div class="system-date" id="date">Loading...</div>
            <div style="color: #ffd43b; margin-top: 10px;">HAVE A GOOD NIGHT, MASTER WAYNE.</div>
        </div>

        <!-- Profile Section -->
        <div class="profile-section">
            <div class="profile-name">🦇 Affan bin Hassan</div>
            <div class="profile-title">AI & Data Science Developer | Engineering Student</div>
            <div style="color: #00ffff; margin: 20px 0;">
                "It's not who I am underneath, but what I code that defines me."
            </div>
            
            <div class="skills-container">
                <span class="skill-badge">Python</span>
                <span class="skill-badge">Data Science</span>
                <span class="skill-badge">AI/ML</span>
                <span class="skill-badge">Git/GitHub</span>
                <span class="skill-badge">Problem Solving</span>
            </div>
        </div>

        <!-- Dashboard -->
        <div class="dashboard">
            <!-- System Status -->
            <div class="widget">
                <div class="widget-title">⚙️ System Status</div>
                <div class="widget-content">
                    <div class="stat-row">
                        <span class="stat-label">Machine:</span>
                        <span class="stat-value">HP Pavilion x360</span>
                    </div>
                    <div class="stat-row">
                        <span class="stat-label">Processor:</span>
                        <span class="stat-value">Intel i5-1235U</span>
                    </div>
                    <div class="stat-row">
                        <span class="stat-label">Memory:</span>
                        <span class="stat-value">8GB RAM</span>
                    </div>
                    <div class="stat-row">
                        <span class="stat-label">OS:</span>
                        <span class="stat-value">Windows 11</span>
                    </div>
                    <div class="stat-row">
                        <span class="stat-label">Status:</span>
                        <span class="stat-value" style="color: #32cd32;">● ONLINE</span>
                    </div>
                </div>
            </div>

            <!-- Current Missions -->
            <div class="widget">
                <div class="widget-title">🚀 Current Missions</div>
                <div class="widget-content">
                    <div class="mission-status">
                        <div class="status-indicator"></div>
                        <span>Dominating Python</span>
                    </div>
                    <div class="mission-status">
                        <div class="status-indicator"></div>
                        <span>Data Science Foundations</span>
                    </div>
                    <div class="mission-status">
                        <div class="status-indicator"></div>
                        <span>System Integrity (Git/GitHub)</span>
                    </div>
                    <div class="mission-status">
                        <div class="status-indicator"></div>
                        <span>AI/ML Exploration</span>
                    </div>
                </div>
            </div>

            <!-- Quick Links -->
            <div class="widget">
                <div class="widget-title">🔗 Quick Links</div>
                <div class="quick-links">
                    <a href="https://github.com/Affanbinhassan" class="quick-link" target="_blank">GitHub</a>
                    <a href="https://linkedin.com/in/Affan-Bin-Hassan" class="quick-link" target="_blank">LinkedIn</a>
                    <a href="https://instagram.com/affan.bin.hassan" class="quick-link" target="_blank">Instagram</a>
                    <a href="mailto:affanbinhassan17@gmail.com" class="quick-link">Email</a>
                </div>
            </div>

            <!-- Terminal -->
            <div class="widget" style="grid-column: span 2;">
                <div class="widget-title">💻 Batcomputer Terminal</div>
                <div class="terminal" id="terminal">
                    <div class="terminal-line"><span class="terminal-prompt">BATCOMPUTER></span> <span class="terminal-text">Initializing systems...</span></div>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <footer>
            <p>🦇 Batcomputer v2.4.1 | Gotham Standard Time | All protocols active</p>
            <p style="margin-top: 10px;">Systems monitored by Affan bin Hassan</p>
        </footer>
    </div>

    <script>
        // Real-time Clock
        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('en-US', { 
                hour12: false,
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            });
            const dateString = now.toLocaleDateString('en-US', {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
            
            document.getElementById('clock').textContent = timeString;
            document.getElementById('date').textContent = dateString;
        }

        setInterval(updateClock, 1000);
        updateClock();

        // Terminal Simulation
        const terminalLines = [
            "Loading Bat-OS interface...",
            "Connecting to Wayne Enterprises network...",
            "Identity verified: Affan bin Hassan",
            "Loading Python development environment...",
            "Data Science modules initialized...",
            "Git repository sync complete...",
            "AI training protocols active...",
            "All systems operational. Welcome back, sir."
        ];

        let lineIndex = 0;
        function addTerminalLine() {
            if (lineIndex < terminalLines.length) {
                const terminal = document.getElementById('terminal');
                const line = document.createElement('div');
                line.className = 'terminal-line';
                line.style.animationDelay = '0s';
                line.innerHTML = `<span class="terminal-prompt">BATCOMPUTER></span> <span class="terminal-text">${terminalLines[lineIndex]}</span>`;
                terminal.appendChild(line);
                terminal.scrollTop = terminal.scrollHeight;
                lineIndex++;
                setTimeout(addTerminalLine, 800);
            }
        }

        setTimeout(addTerminalLine, 1000);

        // Add some random terminal updates
        setInterval(() => {
            const terminal = document.getElementById('terminal');
            const messages = [
                "Scanning Gotham network...",
                "Analyzing data patterns...",
                "System optimization complete",
                "Background processes running normally",
                "Security protocols active"
            ];
            const randomMsg = messages[Math.floor(Math.random() * messages.length)];
            const line = document.createElement('div');
            line.className = 'terminal-line';
            line.innerHTML = `<span class="terminal-prompt">BATCOMPUTER></span> <span class="terminal-text">${randomMsg}</span>`;
            terminal.appendChild(line);
            terminal.scrollTop = terminal.scrollHeight;
            
            // Keep only last 20 lines
            while (terminal.children.length > 20) {
                terminal.removeChild(terminal.firstChild);
            }
        }, 5000);
    </script>
</body>
</html>
