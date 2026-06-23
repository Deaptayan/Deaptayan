<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deaptayan Bondopadhay - Profile HUD</title>
    <style>
        :root {
            --bg-black: #0a0b0d;
            --panel-bg: #10141b;
            --neon-blue: #00d2ff;
            --neon-green: #00ff66;
            --text-gray: #8b949e;
            --text-light: #c9d1d9;
            --border-color: #21262d;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Courier New', Courier, monospace;
        }

        body {
            background-color: var(--bg-black);
            color: var(--text-light);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        /* Drone/CNC Grid Background Effect */
        .hud-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 210, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 210, 255, 0.03) 1px, transparent 1px);
            background-size: 20px 20px;
            pointer-events: none;
            z-index: 1;
        }

        /* CNC Laser Scanning Line Animation */
        .hud-overlay::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--neon-green), transparent);
            top: 0;
            animation: cnc-scan 6s linear infinite;
        }

        @keyframes cnc-scan {
            0% { top: 0%; opacity: 0; }
            5% { opacity: 1; }
            95% { opacity: 1; }
            100% { top: 100%; opacity: 0; }
        }

        /* Core Container */
        .profile-container {
            position: relative;
            z-index: 2;
            width: 100%;
            max-width: 950px;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 4px;
            padding: 20px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.7);
        }

        /* UI Header */
        .hud-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            border-bottom: 2px dashed var(--border-color);
            padding-bottom: 15px;
            margin-bottom: 15px;
        }

        .identity h1 {
            font-size: 1.6rem;
            color: #fff;
            letter-spacing: 1px;
        }

        .identity h1 span {
            color: var(--neon-blue);
        }

        .identity h3 {
            font-size: 0.9rem;
            color: var(--neon-green);
            margin-top: 4px;
            font-weight: normal;
        }

        .bio {
            font-size: 0.8rem;
            color: var(--text-gray);
            margin-top: 8px;
            max-width: 650px;
            line-height: 1.4;
        }

        .telemetry-status {
            text-align: right;
            font-size: 0.75rem;
            color: var(--neon-blue);
        }

        .status-pulse {
            display: inline-block;
            width: 8px;
            height: 8px;
            background-color: var(--neon-green);
            border-radius: 50%;
            margin-right: 5px;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(0, 255, 102, 0.7); }
            70% { box-shadow: 0 0 0 6px rgba(0, 255, 102, 0); }
            100% { box-shadow: 0 0 0 0 rgba(0, 255, 102, 0); }
        }

        /* Compact Dashboard Columns */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr 1.3fr;
            gap: 15px;
        }

        .panel {
            background: rgba(10, 11, 13, 0.6);
            border: 1px solid var(--border-color);
            padding: 12px;
            position: relative;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }

        /* Robotic Target Lock Hover Effect */
        .panel:hover {
            border-color: var(--neon-blue);
            box-shadow: 0 0 8px rgba(0, 210, 255, 0.2);
        }

        .panel-title {
            font-size: 0.85rem;
            text-transform: uppercase;
            color: var(--neon-blue);
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 4px;
        }

        /* Lists and Details */
        .panel-list {
            list-style: none;
        }

        .panel-list li {
            font-size: 0.8rem;
            margin-bottom: 6px;
            line-height: 1.4;
            display: flex;
            align-items: flex-start;
        }

        .panel-list li::before {
            content: "⌖";
            color: var(--neon-green);
            margin-right: 8px;
        }

        .panel-list li strong {
            color: #fff;
        }

        /* Tech Badges / Vectors tags */
        .tech-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-top: 5px;
        }

        .tag {
            font-size: 0.7rem;
            background: rgba(0, 210, 255, 0.08);
            border: 1px solid rgba(0, 210, 255, 0.3);
            color: var(--neon-blue);
            padding: 2px 6px;
            border-radius: 2px;
        }

        .tag.green {
            background: rgba(0, 255, 102, 0.08);
            border: 1px solid rgba(0, 255, 102, 0.3);
            color: var(--neon-green);
        }

        /* Project UI Card Design */
        .project-card {
            border-left: 2px solid var(--neon-blue);
            background: rgba(255,255,255,0.02);
            padding: 8px;
            margin-bottom: 10px;
        }

        .project-card:last-child {
            margin-bottom: 0;
        }

        .project-title {
            font-size: 0.85rem;
            color: #fff;
            display: flex;
            justify-content: space-between;
        }

        .project-title span {
            font-size: 0.7rem;
            color: var(--neon-green);
        }

        .project-desc {
            font-size: 0.75rem;
            color: var(--text-gray);
            margin: 4px 0;
        }

        /* Footer/System Info */
        .hud-footer {
            margin-top: 15px;
            border-top: 1px solid var(--border-color);
            padding-top: 10px;
            display: flex;
            justify-content: space-between;
            font-size: 0.7rem;
            color: var(--text-gray);
        }

        .hud-footer a {
            color: var(--neon-blue);
            text-decoration: none;
        }

        .hud-footer a:hover {
            text-decoration: underline;
        }

        /* Responsive scaling */
        @media (max-width: 768px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            .hud-header {
                flex-direction: column;
                gap: 10px;
            }
            .telemetry-status {
                text-align: left;
            }
        }
    </style>
</head>
<body>

    <div class="hud-overlay"></div>

    <div class="profile-container">
        <!-- HEADER MODULE -->
        <header class="hud-header">
            <div class="identity">
                <h1>Hi 👋, I'm <span>Deaptayan Bondopadhay</span></h1>
                <h3>Developer • Embedded Systems Enthusiast • Open Source Contributor</h3>
                <p class="bio">
                    Building software, firmware, and hardware projects with a focus on autonomous drones, CNC systems, robotics, IoT, and embedded automation ecosystems.
                </p>
            </div>
            <div class="telemetry-status">
                <div><span class="status-pulse"></span>SYS_STATUS: ACTIVE</div>
                <div style="margin-top: 4px; color: var(--text-gray);">LOC: KOLKATA_IN</div>
            </div>
        </header>

        <!-- MAIN DASHBOARD CONTENT -->
        <main class="dashboard-grid">
            
            <!-- LEFT COLUMN: SYSTEM OVERVIEW & TOOLS -->
            <div style="display: flex; flex-direction: column; gap: 15px;">
                
                <!-- ABOUT / CORE DATA -->
                <section class="panel">
                    <div class="panel-title"><span>[01] System Core</span> <span>BCA_UNIT</span></div>
                    <ul class="panel-list">
                        <li>🎓 <strong>BCA Student</strong> & Tech Innovator</li>
                        <li>🤖 <strong>RedShift Robotic</strong> Leader</li>
                        <li>🖨️ Enthusiastic about <strong>3D Printing</strong> & Hardware Architecture</li>
                        <li>⚡ Fun Fact: College-famous for Competitive Line Following Robots.</li>
                    </ul>
                </section>

                <!-- TECH MATRIX -->
                <section class="panel">
                    <div class="panel-title"><span>[02] Firmware & Software Stack</span> <span>ENV</span></div>
                    <div style="margin-bottom: 8px; font-size: 0.75rem; color: var(--text-gray);">Core Environments:</div>
                    <div class="tech-tags">
                        <span class="tag">C++</span>
                        <span class="tag">Python</span>
                        <span class="tag">Embedded Systems</span>
                        <span class="tag">CNC Software Dev</span>
                    </div>
                    <div style="margin: 10px 0 8px 0; font-size: 0.75rem; color: var(--text-gray);">Hardware Interfacing:</div>
                    <div class="tech-tags">
                        <span class="tag green">ESP32</span>
                        <span class="tag green">STM32</span>
                        <span class="tag green">ArduPilot</span>
                        <span class="tag green">IoT / Automation</span>
                    </div>
                </section>
            </div>

            <!-- RIGHT COLUMN: ACTIVE PROJECTS -->
            <div style="display: flex; flex-direction: column; gap: 15px;">
                <section class="panel" style="height: 100%;">
                    <div class="panel-title"><span>[03] Project Operations</span> <span>LIVE_DEPLOYMENTS</span></div>
                    
                    <!-- PROJECT 1 -->
                    <div class="project-card">
                        <div class="project-title">
                            <strong>🚁 Autonomous Drone Platform</strong>
                            <span>ArduPilot Base</span>
                        </div>
                        <p class="project-desc">Custom autonomous drone architecture execution.</p>
                        <ul class="panel-list" style="margin-top: 4px;">
                            <li style="font-size: 0.7rem; margin-bottom: 2px;">Ported DeveBox STM32H743VIT6 board to ArduPilot</li>
                            <li style="font-size: 0.7rem; margin-bottom: 2px;">Engineered dedicated custom hardware definitions</li>
                        </ul>
                    </div>

                    <!-- PROJECT 2 -->
                    <div class="project-card">
                        <div class="project-title">
                            <strong>⌖ PlotterNC Ecosystem</strong>
                            <span>Open Source CAM</span>
                        </div>
                        <p class="project-desc">Developing PlotterNC Studio and PlotterNC firmware ecosystem optimized strictly for precise multi-axis CNC plotters.</p>
                    </div>

                    <!-- PROJECT 3 -->
                    <div class="project-card">
                        <div class="project-title">
                            <strong>🏎️ Black Beauty & RedShift Tech</strong>
                            <span>Robotics Competitive</span>
                        </div>
                        <p class="project-desc">Designing rapid, high-performance competitive Line Following Robots optimized for advanced speed and sensory precision tracing.</p>
                    </div>

                </section>
            </div>
        </main>

        <!-- FOOTER MODULE -->
        <footer class="hud-footer">
            <div>COMMS_LINK: <a href="mailto:deaptayanbondopadhay@gmail.com">deaptayanbondopadhay@gmail.com</a></div>
            <div>© 2026 // DEAPTAYAN_BONDOPADHAY // GROUND_CONTROL_OK</div>
        </footer>
    </div>

</body>
</html>
