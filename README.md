<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PixelRobux - Tes Robux Moins Chers !</title>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* CSS intégré */
        :root {
            /* Couleurs Thème Sombre */
            --primary-bg: #1a1a2e; /* Fond principal */
            --secondary-bg: #16213e; /* Fond secondaire/cards */
            --accent-color: #e94560; /* Rouge vif pour accent/boutons */
            --text-color: #e0e0e0; /* Texte clair */
            --heading-color: #ffffff; /* Titres */
            --border-color: #0f3460; /* Bordures subtiles */
            --button-hover-bg: #c93550; /* Rouge plus foncé au survol */
            --old-price-color: #999999; /* Ancien prix */
            --savings-color: #32cd32; /* Vert pour les économies */
            --subscription-color: #ffd700; /* Or pour l'abonnement */

            /* Couleurs Thème Clair (pour le toggle) */
            --light-primary-bg: #f0f2f5;
            --light-secondary-bg: #ffffff;
            --light-accent-color: #007bff;
            --light-text-color: #333333;
            --light-heading-color: #1a1a2e;
            --light-border-color: #dddddd;
            --light-button-hover-bg: #0056b3;
        }

        /* Thème clair quand la classe dark-mode est retirée (optionnel) */
        body.light-mode {
            --primary-bg: var(--light-primary-bg);
            --secondary-bg: var(--light-secondary-bg);
            --accent-color: var(--light-accent-color);
            --text-color: var(--light-text-color);
            --heading-color: var(--light-heading-color);
            --border-color: var(--light-border-color);
            --button-hover-bg: var(--light-button-hover-bg);
            /* old-price et savings peuvent rester les mêmes ou être ajustés */
        }

        /* Styles de base */
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--primary-bg);
            color: var(--text-color);
            line-height: 1.6;
            overflow-x: hidden; /* Empêche le défilement horizontal dû aux animations */
            transition: background-color 0.5s ease; /* Transition pour le mode sombre */
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* --- Loader de Lancement --- */
        .loader-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--primary-bg);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            opacity: 1;
            transition: opacity 1s ease-out, visibility 1s ease-out;
        }

        .loader-overlay.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .loader-content {
            text-align: center;
            animation: bounceIn 1s forwards; /* Animation d'entrée */
        }

        .loader-logo {
            width: 150px;
            height: auto;
            animation: spin 2s infinite linear; /* Animation de rotation du logo */
            margin-bottom: 20px;
        }

        .loader-text {
            font-family: 'Press Start 2P', cursive;
            color: var(--accent-color);
            font-size: 1.2em;
            text-shadow: 0 0 10px var(--accent-color);
        }

        @keyframes bounceIn {
            0% {
                transform: scale(0.5);
                opacity: 0;
            }
            60% {
                transform: scale(1.1);
                opacity: 1;
            }
            100% {
                transform: scale(1);
            }
        }

        @keyframes spin {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }

        /* --- Header --- */
        header {
            background-color: var(--secondary-bg);
            padding: 15px 0;
            border-bottom: 1px solid var(--border-color);
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            transition: background-color 0.5s ease, border-color 0.5s ease;
        }

        header .container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-family: 'Press Start 2P', cursive;
            color: var(--heading-color);
            font-size: 1.8em;
            text-shadow: 2px 2px var(--accent-color);
            transition: color 0.5s ease, text-shadow 0.5s ease;
        }

        nav ul {
            list-style: none;
            margin: 0;
            padding: 0;
            display: flex;
        }

        nav ul li {
            margin-left: 30px;
        }

        nav ul li a {
            color: var(--text-color);
            text-decoration: none;
            font-weight: bold;
            padding: 5px 0;
            position: relative;
            transition: color 0.3s ease;
        }

        nav ul li a::after {
            content: '';
            position: absolute;
            width: 0;
            height: 3px;
            background-color: var(--accent-color);
            left: 50%;
            bottom: -5px;
            transform: translateX(-50%);
            transition: width 0.3s ease, background-color 0.5s ease;
        }

        nav ul li a:hover {
            color: var(--accent-color);
        }

        nav ul li a:hover::after {
            width: 100%;
        }

        .settings-btn {
            background-color: transparent;
            border: none;
            font-size: 1.8em;
            color: var(--text-color);
            cursor: pointer;
            transition: transform 0.3s ease, color 0.3s ease;
        }

        .settings-btn:hover {
            transform: rotate(30deg);
            color: var(--accent-color);
        }

        /* --- Sections Générales --- */
        section {
            padding: 80px 0;
            text-align: center;
            position: relative;
            overflow: hidden; /* Pour les arrière-plans animés */
            transition: background-color 0.5s ease, color 0.5s ease;
        }

        h2, h3 {
            font-family: 'Press Start 2P', cursive;
            color: var(--heading-color);
            margin-bottom: 40px;
            font-size: 2.5em;
            text-shadow: 3px 3px var(--accent-color);
            transition: color 0.5s ease, text-shadow 0.5s ease;
        }

        p {
            font-size: 1.1em;
            color: var(--text-color);
            transition: color 0.5s ease;
        }

        /* --- Hero Section --- */
        .hero-section {
            background: linear-gradient(135deg, var(--primary-bg) 0%, var(--secondary-bg) 100%);
            min-height: 70vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .hero-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('data:image/svg+xml;utf8,<svg width="100" height="100" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><g fill="%230f3460" fill-opacity="0.1"><circle cx="25" cy="25" r="5"/><circle cx="75" cy="75" r="5"/><rect x="0" y="0" width="10" height="10"/></g></svg>'); /* Petits motifs pour un effet pixel */
            background-size: 20px 20px;
            opacity: 0.2;
            animation: backgroundMove 60s linear infinite;
        }

        @keyframes backgroundMove {
            from { background-position: 0 0; }
            to { background-position: 100% 100%; }
        }

        .hero-section h2 {
            font-size: 3.5em;
            margin-bottom: 20px;
            animation: fadeInDown 1s forwards;
        }

        .hero-section p {
            font-size: 1.3em;
            margin-bottom: 40px;
            animation: fadeInUp 1s forwards 0.3s;
        }

        .cta-button {
            background-color: var(--accent-color);
            color: var(--heading-color);
            padding: 15px 30px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            animation: pulse 1.5s infinite;
        }

        .cta-button:hover {
            background-color: var(--button-hover-bg);
            transform: translateY(-5px) scale(1.02);
            animation: none; /* Arrête l'animation au survol */
        }

        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }


        /* --- Packages Section --- */
        .packages-section {
            background-color: var(--secondary-bg);
            padding: 100px 0;
            border-top: 1px solid var(--border-color);
            transition: background-color 0.5s ease, border-color 0.5s ease;
        }

        .package-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-top: 50px;
        }

        .package-card {
            background-color: var(--primary-bg);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
            text-align: center;
            transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.5s ease;
            border: 2px solid transparent;
        }

        .package-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.6);
            border-color: var(--accent-color);
        }

        .package-card.featured {
            border-color: var(--accent-color);
            box-shadow: 0 10px 30px rgba(233, 69, 96, 0.4);
            transform: scale(1.05);
            animation: featuredPulse 2s infinite;
        }

        @keyframes featuredPulse {
            0% { transform: scale(1.05); box-shadow: 0 10px 30px rgba(233, 69, 96, 0.4); }
            50% { transform: scale(1.07); box-shadow: 0 15px 40px rgba(233, 69, 96, 0.6); }
            100% { transform: scale(1.05); box-shadow: 0 10px 30px rgba(233, 69, 96, 0.4); }
        }

        .package-card img {
            width: 120px;
            height: 120px;
            margin-bottom: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
        }

        .package-card h4 {
            font-family: 'Press Start 2P', cursive;
            color: var(--accent-color);
            font-size: 1.5em;
            margin-bottom: 15px;
            transition: color 0.5s ease;
        }

        .package-card .old-price {
            color: var(--old-price-color);
            text-decoration: line-through;
            font-size: 0.95em;
            margin-bottom: 5px;
        }

        .package-card .new-price {
            color: var(--heading-color);
            font-size: 2em;
            font-weight: bold;
            margin-bottom: 10px;
            transition: color 0.5s ease;
        }

        .package-card .savings {
            color: var(--savings-color);
            font-weight: bold;
            margin-bottom: 20px;
        }

        .buy-button {
            background-color: var(--accent-color);
            color: var(--heading-color);
            padding: 12px 25px;
            font-size: 1.1em;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
            font-weight: bold;
        }

        .buy-button:hover {
            background-color: var(--button-hover-bg);
            transform: translateY(-3px);
        }

        /* --- Subscription Section --- */
        .subscription-section {
            background: linear-gradient(135deg, var(--secondary-bg) 0%, #0c1a2f 100%);
            padding: 100px 0;
            border-top: 1px solid var(--border-color);
            border-bottom: 1px solid var(--border-color);
            color: var(--text-color);
        }

        .subscription-card {
            background-color: var(--primary-bg);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            max-width: 700px;
            margin: 0 auto;
            border: 3px solid var(--subscription-color);
            position: relative;
            overflow: hidden;
        }

        .subscription-card::before {
            content: '⭐ PREMIUM ⭐';
            position: absolute;
            top: 20px;
            right: -60px;
            background-color: var(--subscription-color);
            color: #1a1a2e;
            padding: 8px 60px;
            font-weight: bold;
            font-family: 'Press Start 2P', cursive;
            font-size: 0.8em;
            transform: rotate(45deg);
            transform-origin: 100% 0%;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.5);
        }

        .subscription-card h3 {
            color: var(--subscription-color);
            font-size: 2em;
            margin-bottom: 20px;
        }

        .subscription-card ul {
            list-style: none;
            padding: 0;
            margin-bottom: 30px;
            text-align: left;
        }

        .subscription-card ul li {
            font-size: 1.1em;
            margin-bottom: 10px;
            color: var(--text-color);
            display: flex;
            align-items: center;
        }

        .subscription-card ul li::before {
            content: '✅';
            margin-right: 10px;
            color: var(--savings-color);
            font-size: 1.2em;
        }

        .subscribe-button {
            background-color: var(--subscription-color);
            color: #1a1a2e;
            padding: 18px 35px;
            font-size: 1.3em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.3s ease, transform 0.3s ease;
            box-shadow: 0 5px 20px rgba(255, 215, 0, 0.4);
        }

        .subscribe-button:hover {
            background-color: #e6c200;
            transform: translateY(-5px) scale(1.02);
        }

        /* --- Free Robux Section --- */
        .free-robux-section {
            background-color: var(--primary-bg);
            padding: 80px 0;
            border-top: 1px solid var(--border-color);
            color: var(--text-color);
        }

        .free-robux-section h3 {
            color: var(--accent-color);
            margin-bottom: 25px;
        }

        .free-robux-section p {
            font-size: 1.2em;
            margin-bottom: 30px;
        }

        .youtube-link-btn {
            background-color: #ff0000; /* Rouge YouTube */
            color: white;
            padding: 15px 30px;
            font-size: 1.2em;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            transition: background-color 0.3s ease, transform 0.3s ease;
            box-shadow: 0 5px 15px rgba(255, 0, 0, 0.4);
        }

        .youtube-link-btn:hover {
            background-color: #cc0000;
            transform: translateY(-3px);
        }

        .youtube-link-btn svg {
            margin-right: 10px;
        }


        /* --- Features Section --- */
        .features-section {
            background-color: var(--primary-bg);
            padding: 100px 0;
            transition: background-color 0.5s ease;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-top: 50px;
        }

        .feature-item {
            background-color: var(--secondary-bg);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
            transition: transform 0.3s ease, background-color 0.3s ease;
        }

        .feature-item:hover {
            transform: scale(1.03);
            background-color: #1f2a4a; /* Lighter secondary bg on hover */
        }

        .feature-item h4 {
            font-family: 'Press Start 2P', cursive;
            color: var(--accent-color);
            font-size: 1.4em;
            margin-bottom: 15px;
            transition: color 0.5s ease;
        }

        .feature-item p {
            color: var(--text-color);
            font-size: 1em;
            transition: color 0.5s ease;
        }

        /* --- FAQ Section --- */
        .faq-section {
            background-color: var(--secondary-bg);
            padding: 100px 0;
            border-top: 1px solid var(--border-color);
            transition: background-color 0.5s ease, border-color 0.5s ease;
        }

        .faq-item {
            background-color: var(--primary-bg);
            margin-bottom: 20px;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            text-align: left;
            transition: transform 0.2s ease, background-color 0.5s ease;
        }

        .faq-item:hover {
            transform: translateX(10px);
        }

        .faq-item h4 {
            font-family: 'Roboto', sans-serif; /* Plus simple pour les questions */
            color: var(--heading-color);
            font-size: 1.2em;
            margin-bottom: 10px;
            cursor: pointer;
            position: relative;
            padding-right: 30px;
            transition: color 0.5s ease;
        }

        .faq-item h4::after {
            content: '+';
            position: absolute;
            right: 0;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.5em;
            color: var(--accent-color);
            transition: transform 0.3s ease, color 0.5s ease;
        }

        .faq-item h4.active::after {
            content: '-';
            transform: translateY(-50%) rotate(180deg);
        }

        .faq-item p {
            font-size: 0.95em;
            color: var(--text-color);
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease-out;
            padding-left: 10px;
        }

        .faq-item p.active {
            max-height: 100px; /* Valeur suffisante pour afficher le texte */
            margin-top: 10px;
        }

        /* --- Footer --- */
        footer {
            background-color: var(--primary-bg);
            padding: 30px 0;
            border-top: 1px solid var(--border-color);
            text-align: center;
            font-size: 0.9em;
            color: var(--old-price-color);
            transition: background-color 0.5s ease, border-color 0.5s ease, color 0.5s ease;
        }

        .footer-links a {
            color: var(--old-price-color);
            text-decoration: none;
            margin: 0 15px;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: var(--accent-color);
        }

        /* --- Settings Panel --- */
        .settings-panel {
            position: fixed;
            top: 0;
            right: -350px; /* Masqué par défaut */
            width: 300px;
            height: 100%;
            background-color: var(--secondary-bg);
            box-shadow: -5px 0 20px rgba(0, 0, 0, 0.5);
            z-index: 2000;
            transition: right 0.4s ease-out, background-color 0.5s ease, border-left 0.5s ease;
            padding: 20px;
            box-sizing: border-box;
            border-left: 1px solid var(--border-color);
        }

        .settings-panel.open {
            right: 0;
        }

        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px solid var(--border-color);
            transition: border-bottom 0.5s ease;
        }

        .settings-header h3 {
            font-family: 'Press Start 2P', cursive;
            font-size: 1.5em;
            color: var(--heading-color);
            text-shadow: none;
            margin: 0; /* Réinitialise le margin du h3 */
            transition: color 0.5s ease;
        }

        .close-settings-btn {
            background-color: transparent;
            border: none;
            font-size: 1.8em;
            color: var(--text-color);
            cursor: pointer;
            transition: color 0.3s ease;
        }

        .close-settings-btn:hover {
            color: var(--accent-color);
        }

        .setting-option {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid var(--border-color);
            transition: border-bottom 0.5s ease;
        }

        .setting-option:last-child {
            border-bottom: none;
        }

        .setting-option span {
            font-size: 1.1em;
            color: var(--text-color);
            transition: color 0.5s ease;
        }

        .settings-info {
            font-size: 0.9em;
            color: var(--old-price-color);
            margin-top: 30px;
            text-align: center;
            transition: color 0.5s ease;
        }

        /* Toggle Switch (pour Dark Mode / Notifications) */
        .switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 28px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 20px;
            width: 20px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--accent-color);
        }

        input:focus + .slider {
            box-shadow: 0 0 1px var(--accent-color);
        }

        input:checked + .slider:before {
            transform: translateX(22px);
        }

        /* Select Box Styling */
        select {
            background-color: var(--primary-bg);
            color: var(--text-color);
            border: 1px solid var(--border-color);
            padding: 8px 12px;
            border-radius: 8px;
            font-size: 1em;
            cursor: pointer;
            appearance: none; /* Supprime le style par défaut du navigateur */
            -webkit-appearance: none;
            -moz-appearance: none;
            background-image: url('data:image/svg+xml;utf8,<svg fill="%23e0e0e0" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg"><path d="M7 10l5 5 5-5z"/><path d="M0 0h24v24H0z" fill="none"/></svg>'); /* Flèche personnalisée */
            background-repeat: no-repeat;
            background-position: right 8px center;
            padding-right: 30px; /* Espace pour la flèche */
            transition: background-color 0.5s ease, color 0.5s ease, border-color 0.5s ease;
        }

        select:focus {
            outline: none;
            border-color: var(--accent-color);
        }

        /* Media Queries pour la Responsivité */
        @media (max-width: 768px) {
            header .container {
                flex-direction: column;
                text-align: center;
            }
            nav ul {
                margin-top: 15px;
                flex-wrap: wrap;
                justify-content: center;
            }
            nav ul li {
                margin: 0 15px 10px;
            }
            .settings-btn {
                position: absolute;
                top: 20px;
                right: 20px;
            }
            .hero-section h2 {
                font-size: 2.5em;
            }
            .hero-section p {
                font-size: 1em;
            }
            h2, h3 {
                font-size: 2em;
            }
            .package-grid, .feature-grid {
                grid-template-columns: 1fr;
            }
            .package-card.featured {
                transform: scale(1.03); /* Moins de zoom sur mobile */
            }
            @keyframes featuredPulse {
                0% { transform: scale(1.03); }
                50% { transform: scale(1.05); }
                100% { transform: scale(1.03); }
            }
            .settings-panel {
                width: 100%; /* Pleine largeur sur mobile */
            }
        }
    </style>
</head>
<body>
    <div class="loader-overlay" id="loaderOverlay">
        <div class="loader-content">
            <img src="https://yt3.googleusercontent.com/xpsKUsqXvyxMZFQs7MVOMy-Qab4Uo9XXWGFlvMZHQhqOq3Nx54dNF3WePsaIfxEFuCL75QYbFw=s160-c-k-c0x00ffffff-no-rj" alt="Logo Roblox" class="loader-logo">
            <div class="loader-text">Chargement de PixelRobux...</div>
        </div>
    </div>

    <header>
        <div class="container">
            <h1 class="logo">PixelRobux</h1>
            <nav>
                <ul>
                    <li><a href="#accueil">Accueil</a></li>
                    <li><a href="#offres">Nos Offres</a></li>
                    <li><a href="#abonnement">Abonnement</a></li>
                    <li><a href="#robux-gratuits">Robux Gratuits</a></li>
                    <li><a href="#avantages">Pourquoi Nous ?</a></li>
                    <li><a href="#faq">FAQ</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
            <button class="settings-btn" id="settingsBtn">⚙️</button>
        </div>
    </header>

    <main>
        <section id="accueil" class="hero-section">
            <div class="container">
                <h2>Tes Robux, Moins Cher, Tout de Suite !</h2>
                <p>Débloque le jeu comme jamais avec des Robux à prix imbattable.</p>
                <button class="cta-button">Découvrir nos Offres !</button>
            </div>
        </section>

        <section id="offres" class="packages-section">
            <div class="container">
                <h3>Nos Meilleurs Plans Robux</h3>
                <div class="package-grid">
                    <div class="package-card">
                        <img src="https://rewards.bing.com/rewardscdn/images/rewards/rc/large/000400000343_v1_310x216.png" alt="400 Robux">
                        <h4>400 Robux</h4>
                        <p class="old-price">Prix initial : <span>5,00€</span></p>
                        <p class="new-price">Prix PixelRobux : <strong>2,00€</strong></p>
                        <p class="savings">Économise 3,00€ !</p>
                        <button class="buy-button">Acheter</button>
                    </div>
                    <div class="package-card featured">
                        <img src="https://rewards.bing.com/rewardscdn/images/rewards/rc/large/000400000343_v1_310x216.png" alt="800 Robux">
                        <h4>800 Robux</h4>
                        <p class="old-price">Prix initial : <span>10,00€</span></p>
                        <p class="new-price">Prix PixelRobux : <strong>5,00€</strong></p>
                        <p class="savings">Économise 5,00€ !</p>
                        <button class="buy-button">Acheter Maintenant !</button>
                    </div>
                    <div class="package-card">
                        <img src="https://rewards.bing.com/rewardscdn/images/rewards/rc/large/000400000343_v1_310x216.png" alt="1500 Robux">
                        <h4>1500 Robux</h4>
                        <p class="old-price">Prix initial : <span>20,00€</span></p>
                        <p class="new-price">Prix PixelRobux : <strong>10,00€</strong></p>
                        <p class="savings">Économise 10,00€ !</p>
                        <button class="buy-button">Acheter</button>
                    </div>
                </div>
            </div>
        </section>

        <section id="abonnement" class="subscription-section">
            <div class="container">
                <div class="subscription-card">
                    <h3>Abonnement PixelRobux Premium</h3>
                    <p>Débloque les avantages ultimes et économise encore plus !</p>
                    <ul>
                        <li>Accès exclusif à des packs Robux encore plus avantageux.</li>
                        <li>**30% de réduction supplémentaire** sur TOUS les achats de Robux après abonnement.</li>
                        <li>Priorité sur le support client.</li>
                        <li>Participation automatique à des tirages au sort mensuels de Robux géants !</li>
                    </ul>
                    <button class="subscribe-button">S'abonner au Premium (5,99€/mois)</button>
                </div>
            </div>
        </section>

        <section id="robux-gratuits" class="free-robux-section">
            <div class="container">
                <h3>Robux Gratuits : Participez et Gagnez !</h3>
                <p>Envie de remporter des **Robux gratuits** ? C'est simple comme bonjour !</p>
                <p>Pour avoir une chance d'être tiré au sort et de recevoir des Robux directement sur ton compte, suis ces étapes :</p>
                <ul>
                    <li style="list-style: none; margin-bottom: 10px; display: flex; align-items: center; justify-content: center;">👉 Abonne-toi à notre chaîne YouTube **@SK_PixelRobux**</li>
                    <li style="list-style: none; margin-bottom: 10px; display: flex; align-items: center; justify-content: center;">👍 Laisse un "J'aime" sous nos vidéos.</li>
                    <li style="list-style: none; display: flex; align-items: center; justify-content: center;">💬 Laisse un commentaire avec ton nom d'utilisateur Roblox (pour qu'on puisse t'envoyer tes Robux via PLS Donate) !</li>
                </ul>
                <p style="margin-top: 30px;">Les Robux seront envoyés via l'application **PLS Donate**. Bonne chance à tous !</p>
                <a href="https://www.youtube.com/channel/UCSX_RTLfnFsRW7ODUvGufDQ" target="_blank" class="youtube-link-btn">
                    <svg height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg" fill="#fff"><path d="M12 0c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm6.275 11.233c-.22-.647-.923-1.104-1.637-1.127-1.077-.035-2.155-.07-3.232-.105-1.178-.039-2.355-.078-3.533-.117-.67-.023-1.342-.047-2.012-.07-1.15-.039-2.302-.078-3.454-.117-.643-.024-1.286-.048-1.928-.072-.71-.026-1.42-.052-2.13-.078-.71-.026-1.42-.052-2.13-.078zM12 18c-3.313 0-6-2.687-6-6s2.687-6 6-6 6 2.687 6 6-2.687 6-6 6z"/></svg>
                    Visite la Chaîne YouTube !
                </a>
            </div>
        </section>

        <section id="avantages" class="features-section">
            <div class="container">
                <h3>Pourquoi Choisir PixelRobux ?</h3>
                <div class="feature-grid">
                    <div class="feature-item">
                        <h4>💰 Prix Imbattables</h4>
                        <p>Les meilleurs prix pour tes Robux, garantis.</p>
                    </div>
                    <div class="feature-item">
                        <h4>⚡ Livraison Instantanée</h4>
                        <p>Reçois tes Robux en quelques minutes.</p>
                    </div>
                    <div class="feature-item">
                        <h4>🔒 100% Sécurisé</h4>
                        <p>Transactions fiables et données protégées.</p>
                    </div>
                    <div class="feature-item">
                        <h4>⭐ Support Client 24/7</h4>
                        <p>Toujours là pour t'aider si tu as des questions.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="faq" class="faq-section">
            <div class="container">
                <h3>Questions Fréquentes</h3>
                <div class="faq-item">
                    <h4>Comment fonctionne la livraison ?</h4>
                    <p>Vos Robux sont livrés via des méthodes sûres et vérifiées, souvent directement sur votre compte après validation de l'achat.</p>
                </div>
                <div class="faq-item">
                    <h4>Est-ce légal et sûr ?</h4>
                    <p>Oui, toutes nos méthodes sont 100% légales et sécurisées. Vos informations personnelles et bancaires sont protégées.</p>
                </div>
                <div class="faq-item">
                    <h4>Puis-je obtenir des Robux gratuitement ?</h4>
                    <p>Oui ! Participe à nos concours sur notre chaîne YouTube PixelRobux en t'abonnant et en likant nos vidéos pour tenter de gagner des Robux ! (Voir la section "Robux Gratuits" et la description de la chaîne pour plus de détails)</p>
                </div>
            </div>
        </section>
    </main>

    <footer>
        <div class="container">
            <p>&copy; 2025 PixelRobux. Tous droits réservés.</p>
            <div class="footer-links">
                <a href="#">Politique de Confidentialité</a>
                <a href="#">Conditions d'Utilisation</a>
            </div>
        </div>
    </footer>

    <div class="settings-panel" id="settingsPanel">
        <div class="settings-header">
            <h3>Paramètres</h3>
            <button class="close-settings-btn" id="closeSettingsBtn">✖️</button>
        </div>
        <div class="settings-content">
            <div class="setting-option">
                <span>Mode sombre</span>
                <label class="switch">
                    <input type="checkbox" id="darkModeToggle">
                    <span class="slider round"></span>
                </label>
            </div>
            <div class="setting-option">
                <span>Langue</span>
                <select>
                    <option value="fr">Français</option>
                    <option value="en">English</option>
                </select>
            </div>
            <div class="setting-option">
                <span>Notifications</span>
                <label class="switch">
                    <input type="checkbox" checked>
                    <span class="slider round"></span>
                </label>
            </div>
            <p class="settings-info">Plus d'options à venir !</p>
        </div>
    </div>

    <script>
        // JavaScript intégré
        document.addEventListener('DOMContentLoaded', () => {
            // --- Animation de Lancement ---
            const loaderOverlay = document.getElementById('loaderOverlay');
            if (loaderOverlay) {
                setTimeout(() => {
                    loaderOverlay.classList.add('hidden');
                }, 2000); // Disparaît après 2 secondes
            }

            // --- Gestion du Panel de Paramètres ---
            const settingsBtn = document.getElementById('settingsBtn');
            const closeSettingsBtn = document.getElementById('closeSettingsBtn');
            const settingsPanel = document.getElementById('settingsPanel');

            if (settingsBtn && closeSettingsBtn && settingsPanel) {
                settingsBtn.addEventListener('click', () => {
                    settingsPanel.classList.add('open');
                });

                closeSettingsBtn.addEventListener('click', () => {
                    settingsPanel.classList.remove('open');
                });
            }

            // --- Toggle Mode Sombre ---
            const darkModeToggle = document.getElementById('darkModeToggle');
            if (darkModeToggle) {
                // Vérifie si le mode sombre est déjà activé (par ex. depuis une session précédente)
                // Par défaut, le site est en mode sombre. Ce toggle active/désactive une classe 'light-mode' si tu veux un vrai thème clair.
                // localStorage.getItem('darkMode') peut stocker 'enabled' ou 'disabled'
                if (localStorage.getItem('darkMode') === 'disabled') {
                    document.body.classList.add('light-mode'); // Active le mode clair si c'était désactivé
                    darkModeToggle.checked = false; // Décoche le bouton
                } else {
                    // Si rien en localStorage ou 'enabled', le site reste en mode sombre par défaut
                    darkModeToggle.checked = true; // Coche le bouton pour indiquer mode sombre actif
                }

                darkModeToggle.addEventListener('change', () => {
                    if (!darkModeToggle.checked) { // Si on décoche, on va en mode clair
                        document.body.classList.add('light-mode');
                        localStorage.setItem('darkMode', 'disabled');
                    } else { // Si on coche, on retourne en mode sombre
                        document.body.classList.remove('light-mode');
                        localStorage.setItem('darkMode', 'enabled');
                    }
                });
            }


            // --- FAQ Accordion (Animation d'ouverture/fermeture) ---
            const faqItems = document.querySelectorAll('.faq-item h4');

            faqItems.forEach(item => {
                item.addEventListener('click', () => {
                    const answer = item.nextElementSibling; // Le paragraphe <p> juste après le <h4>
                    item.classList.toggle('active'); // Ajoute/retire la classe "active" sur le titre
                    answer.classList.toggle('active'); // Ajoute/retire la classe "active" sur la réponse
                });
            });

            // --- Boutons d'achat (Exemple simple d'alerte) ---
            const buyButtons = document.querySelectorAll('.buy-button, .cta-button, .subscribe-button');
            buyButtons.forEach(button => {
                button.addEventListener('click', () => {
                    alert('Fonctionnalité à développer ! Redirection vers la page de paiement ou de souscription...');
                    // Ici, tu pourrais rediriger vers une page de paiement ou ouvrir une modale.
                });
            });
        });
    </script>
</body>
</html>
