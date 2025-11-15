<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YPS Whitepaper - The Future of Digital Currency</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/build/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/examples/js/controls/OrbitControls.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.132.2/examples/js/loaders/GLTFLoader.js"></script>
    <style>
        :root {
            --primary: #0a0e17;
            --secondary: #1a2a3a;
            --accent: #00c3ff;
            --highlight: #ff6b00;
            --success: #00ff88;
            --text: #e0e0e0;
            --light-bg: #121a24;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--primary);
            color: var(--text);
            line-height: 1.6;
            overflow-x: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 4rem 0;
            position: relative;
            overflow: hidden;
            border-bottom: 2px solid var(--accent);
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(circle at 20% 80%, rgba(0, 195, 255, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(255, 107, 0, 0.1) 0%, transparent 50%);
        }
        
        .logo {
            font-size: 4rem;
            font-weight: 800;
            margin-bottom: 0.5rem;
            background: linear-gradient(135deg, var(--accent), var(--highlight));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(0, 195, 255, 0.3);
        }
        
        .tagline {
            font-size: 1.5rem;
            opacity: 0.9;
            color: var(--text);
            margin-bottom: 1.5rem;
        }
        
        .section-title {
            position: relative;
            padding-bottom: 0.5rem;
            margin-bottom: 2rem;
            color: var(--accent);
            font-weight: 700;
            font-size: 2.2rem;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 80px;
            height: 4px;
            background: linear-gradient(90deg, var(--accent), var(--highlight));
            border-radius: 2px;
        }
        
        .card {
            border: none;
            border-radius: 12px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.4);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            margin-bottom: 2rem;
            background: linear-gradient(145deg, var(--light-bg), #0d131d);
            color: var(--text);
            overflow: hidden;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--accent), var(--highlight));
        }
        
        .card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
        }
        
        .staking-card {
            border-top: 4px solid var(--highlight);
        }
        
        .staking-period {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--accent);
        }
        
        .staking-return {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--highlight);
            text-shadow: 0 0 10px rgba(255, 107, 0, 0.3);
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--accent), #0088cc);
            border: none;
            font-weight: 600;
            padding: 12px 30px;
            border-radius: 8px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 195, 255, 0.3);
        }
        
        .btn-primary:hover {
            background: linear-gradient(135deg, #0088cc, var(--accent));
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 195, 255, 0.4);
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, var(--highlight), #cc5500);
            border: none;
            color: white;
            font-weight: 600;
            padding: 12px 30px;
            border-radius: 8px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 107, 0, 0.3);
        }
        
        .btn-secondary:hover {
            background: linear-gradient(135deg, #cc5500, var(--highlight));
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 107, 0, 0.4);
        }
        
        .roadmap-item {
            position: relative;
            padding: 2rem;
            margin-bottom: 2rem;
            background: linear-gradient(145deg, var(--light-bg), #0d131d);
            border-radius: 12px;
            border-left: 4px solid var(--highlight);
        }
        
        .roadmap-item::before {
            content: '';
            position: absolute;
            left: -10px;
            top: 2rem;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: var(--highlight);
            box-shadow: 0 0 20px rgba(255, 107, 0, 0.5);
        }
        
        .token-distribution-container {
            height: 500px;
            position: relative;
            margin: 2rem 0;
        }
        
        .team-member {
            text-align: center;
            margin-bottom: 3rem;
            transition: transform 0.3s ease;
        }
        
        .team-member:hover {
            transform: translateY(-5px);
        }
        
        .team-photo {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            object-fit: cover;
            margin: 0 auto 1.5rem;
            border: 4px solid var(--accent);
            box-shadow: 0 0 25px rgba(0, 195, 255, 0.4);
            transition: all 0.3s ease;
        }
        
        .team-member:hover .team-photo {
            border-color: var(--highlight);
            box-shadow: 0 0 30px rgba(255, 107, 0, 0.5);
        }
        
        .download-section {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            padding: 4rem 0;
            text-align: center;
            border-top: 2px solid var(--accent);
            border-bottom: 2px solid var(--accent);
        }
        
        .animation-container {
            height: 400px;
            margin: 3rem 0;
            border-radius: 15px;
            overflow: hidden;
            background: linear-gradient(145deg, var(--light-bg), #0d131d);
            border: 1px solid var(--secondary);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        
        .exchange-features {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 3rem;
            border-radius: 15px;
            margin: 3rem 0;
            border: 1px solid var(--accent);
            position: relative;
            overflow: hidden;
        }
        
        .exchange-features::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(0,195,255,0.1) 0%, transparent 70%);
            animation: pulse 8s infinite linear;
        }
        
        @keyframes pulse {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        footer {
            background-color: var(--secondary);
            color: white;
            padding: 3rem 0;
            margin-top: 4rem;
            border-top: 2px solid var(--accent);
        }
        
        .contract-address {
            background: linear-gradient(145deg, var(--light-bg), #0d131d);
            padding: 1.5rem;
            border-radius: 10px;
            font-family: monospace;
            border-left: 4px solid var(--highlight);
            font-size: 1.1rem;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .token-distribution-list {
            list-style-type: none;
            padding: 0;
        }
        
        .token-distribution-list li {
            padding: 1rem 0;
            border-bottom: 1px solid var(--secondary);
            position: relative;
            padding-right: 60px;
            font-size: 1.1rem;
        }
        
        .distribution-percentage {
            position: absolute;
            right: 0;
            font-weight: bold;
            color: var(--highlight);
            font-size: 1.3rem;
        }
        
        .distribution-percentage::before {
            content: '⟶';
            margin-right: 10px;
            color: var(--accent);
            font-size: 1.5rem;
        }
        
        .feature-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            color: var(--accent);
        }
        
        .use-case-card {
            text-align: center;
            padding: 2rem;
            height: 100%;
            transition: all 0.3s ease;
        }
        
        .use-case-card:hover {
            background: linear-gradient(145deg, #1a2a3a, #0d131d);
        }
        
        .floating {
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        .glow-text {
            text-shadow: 0 0 10px currentColor;
        }
        
        .particle-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        
        @media (max-width: 768px) {
            .staking-card {
                margin-bottom: 2rem;
            }
            
            .team-member {
                margin-bottom: 2rem;
            }
            
            .logo {
                font-size: 3rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <header class="header">
        <div class="particle-container" id="header-particles"></div>
        <div class="container text-center position-relative" style="z-index: 2;">
            <div class="logo">YPS COIN</div>
            <p class="tagline">Revolutionizing Global Payments with Blockchain Technology</p>
            <p class="lead">The Future of Digital Currency - Spend YPS Anywhere in the World</p>
            <div class="contract-address d-inline-block mt-3">
                Contract: Coming Soon
            </div>
        </div>
    </header>

    <!-- Navigation -->
    <nav class="navbar navbar-expand-lg navbar-dark sticky-top" style="background-color: rgba(26, 42, 58, 0.95); backdrop-filter: blur(10px);">
        <div class="container">
            <a class="navbar-brand fw-bold" href="#" style="color: var(--accent);">YPS</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item"><a class="nav-link" href="#abstract">Vision</a></li>
                    <li class="nav-item"><a class="nav-link" href="#staking">Staking</a></li>
                    <li class="nav-item"><a class="nav-link" href="#tokenomics">Tokenomics</a></li>
                    <li class="nav-item"><a class="nav-link" href="#usecases">Use Cases</a></li>
                    <li class="nav-item"><a class="nav-link" href="#roadmap">Roadmap</a></li>
                    <li class="nav-item"><a class="nav-link" href="#exchange">Exchange</a></li>
                    <li class="nav-item"><a class="nav-link" href="#team">Team</a></li>
                    <li class="nav-item"><a class="nav-link" href="#download">Download</a></li>
                </ul>
            </div>
        </div>
    </nav>

    <div class="container my-5">
        <!-- Abstract Section -->
        <section id="abstract" class="mb-5 py-5">
            <h2 class="section-title text-center">Our Vision</h2>
            <div class="row align-items-center">
                <div class="col-lg-6">
                    <p class="fs-5">YPS Coin is not just another cryptocurrency - it's a comprehensive financial ecosystem designed to revolutionize how people transact globally. Our vision is to create a borderless financial system where YPS becomes the preferred medium of exchange for everyday transactions.</p>
                    <p class="fs-5">With our upcoming YPS ATM cards, global flight ticket booking system, and merchant adoption program, you'll be able to use YPS coins anywhere in the world instead of traditional dollars or local currencies.</p>
                    <p class="fs-5">Imagine booking flights to Tokyo, shopping in Paris, or dining in New York - all with your YPS coins, enjoying zero foreign exchange fees and instant transactions.</p>
                </div>
                <div class="col-lg-6">
                    <div class="animation-container" id="vision-animation"></div>
                </div>
            </div>
        </section>

        <!-- Staking Plans Section -->
        <section id="staking" class="mb-5 py-5">
            <h2 class="section-title text-center">High-Yield Staking Plans</h2>
            <p class="text-center mb-5 fs-5">Maximize your returns with our industry-leading staking programs</p>
            
            <div class="row">
                <div class="col-md-3">
                    <div class="card staking-card text-center p-4 floating" style="animation-delay: 0s;">
                        <div class="staking-period">30 Days</div>
                        <div class="mb-2">VPS</div>
                        <div class="staking-return">15%</div>
                        <p class="my-3">Earn 15% return on your investment</p>
                        <button class="btn btn-primary w-100">Select Plan</button>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="card staking-card text-center p-4 floating" style="animation-delay: 0.5s;">
                        <div class="staking-period">100 Days</div>
                        <div class="mb-2">VPS</div>
                        <div class="staking-return">45%</div>
                        <p class="my-3">Earn 45% return on your investment</p>
                        <button class="btn btn-primary w-100">Select Plan</button>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="card staking-card text-center p-4 floating" style="animation-delay: 1s;">
                        <div class="staking-period">200 Days</div>
                        <div class="mb-2">VPS</div>
                        <div class="staking-return">70%</div>
                        <p class="my-3">Earn 70% return on your investment</p>
                        <button class="btn btn-primary w-100">Select Plan</button>
                    </div>
                </div>
                <div class="col-md-3">
                    <div class="card staking-card text-center p-4 floating" style="animation-delay: 1.5s;">
                        <div class="staking-period">360 Days</div>
                        <div class="mb-2">VPS</div>
                        <div class="staking-return">100%</div>
                        <p class="my-3">Earn 100% return on your investment</p>
                        <button class="btn btn-primary w-100">Select Plan</button>
                    </div>
                </div>
            </div>
            
            <div class="animation-container mt-5" id="staking-animation"></div>
        </section>

        <!-- Tokenomics Section -->
        <section id="tokenomics" class="mb-5 py-5">
            <h2 class="section-title text-center">Token Economics</h2>
            
            <div class="row">
                <div class="col-lg-6">
                    <div class="card p-5">
                        <h4 class="mb-4">Token Details</h4>
                        <ul class="list-unstyled fs-5">
                            <li class="mb-3"><strong>Total Supply:</strong> 1.02 Billion YPS</li>
                            <li class="mb-3"><strong>Token Name:</strong> YPS Coin</li>
                            <li class="mb-3"><strong>Token Symbol:</strong> YPS</li>
                            <li class="mb-3"><strong>Blockchain:</strong> Binance Smart Chain</li>
                            <li class="mb-3"><strong>Contract Address:</strong> Coming Soon</li>
                        </ul>
                        
                        <h5 class="mt-5 mb-4">Token Distribution</h5>
                        <ul class="token-distribution-list">
                            <li>Reserve <span class="distribution-percentage">73.7%</span></li>
                            <li>Airdrop (Stakers) <span class="distribution-percentage">17.2%</span></li>
                            <li>Community <span class="distribution-percentage">5%</span></li>
                            <li>Partners <span class="distribution-percentage">4.1%</span></li>
                        </ul>
                    </div>
                </div>
                <div class="col-lg-6">
                    <div class="token-distribution-container" id="token-distribution"></div>
                </div>
            </div>
        </section>

        <!-- Use Cases Section -->
        <section id="usecases" class="mb-5 py-5">
            <h2 class="section-title text-center">Real-World Use Cases</h2>
            <p class="text-center mb-5 fs-5">YPS Coin is designed for everyday use across multiple industries</p>
            
            <div class="row">
                <div class="col-md-4">
                    <div class="card use-case-card">
                        <div class="feature-icon">💳</div>
                        <h4>YPS ATM Cards</h4>
                        <p>Withdraw local currency from ATMs worldwide using your YPS balance. No foreign transaction fees, real-time conversion rates.</p>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card use-case-card">
                        <div class="feature-icon">✈️</div>
                        <h4>Flight Ticket Booking</h4>
                        <p>Book flights with major airlines using YPS coins. Enjoy exclusive discounts and loyalty rewards for YPS holders.</p>
                    </div>
                </div>
                <div class="col-md-4">
                    <div class="card use-case-card">
                        <div class="feature-icon">🛒</div>
                        <h4>Global E-Commerce</h4>
                        <p>Shop at thousands of online stores worldwide. YPS is accepted at major retailers an
