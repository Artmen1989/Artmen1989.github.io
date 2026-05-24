# Artmen1989.github.io
WEB-site

<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>ARTStz | Дерево заказов + выполненные заказы</title>
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/qrcode@1.5.1/build/qrcode.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', sans-serif;
            background: #fbfdff;
            color: #1a2c3e;
            line-height: 1.5;
            scroll-behavior: smooth;
        }

        :root {
            --primary: #2c5f8a;
            --primary-dark: #1e3e5c;
            --accent: #4f9da6;
            --light-bg: #f4f9fe;
            --gray-light: #eef2f6;
            --text-dark: #1e2f3b;
            --text-muted: #5a6e7c;
            --shadow-sm: 0 8px 20px rgba(0, 0, 0, 0.03), 0 2px 4px rgba(0, 0, 0, 0.05);
            --shadow-md: 0 12px 28px rgba(0, 0, 0, 0.08);
            --transition: all 0.25s ease;
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 24px;
        }

        section {
            padding: 80px 0;
        }

        @media (max-width: 768px) {
            section { padding: 56px 0; }
            .container { padding: 0 20px; }
        }

        h1, h2, h3 { font-weight: 700; letter-spacing: -0.02em; }
        h1 { font-size: clamp(2.2rem, 6vw, 3.8rem); line-height: 1.2; margin-bottom: 1rem; }
        h2 { font-size: clamp(1.8rem, 5vw, 2.6rem); margin-bottom: 1rem; text-align: center; }
        .section-subtitle { text-align: center; color: var(--text-muted); max-width: 680px; margin: 0 auto 3rem auto; font-size: 1.1rem; }

        .btn {
            display: inline-flex; align-items: center; justify-content: center;
            background-color: var(--primary); color: white; font-weight: 600;
            padding: 12px 28px; border-radius: 60px; text-decoration: none;
            transition: var(--transition); border: none; cursor: pointer; font-size: 1rem; gap: 8px;
        }
        .btn:hover { background-color: var(--primary-dark); transform: translateY(-2px); box-shadow: var(--shadow-md); }
        .btn-outline { background: transparent; border: 1.5px solid var(--primary); color: var(--primary); }
        .btn-outline:hover { background: var(--primary); color: white; }

        /* ========== НАВИГАЦИЯ ========== */
        #nav-toggle { display: none; }
        .navbar { background: white; box-shadow: 0 1px 2px rgba(0,0,0,0.05); position: sticky; top: 0; z-index: 1000; }
        .nav-container { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; padding: 0.9rem 24px; max-width: 1280px; margin: 0 auto; }
        .logo { font-size: 1.7rem; font-weight: 800; background: linear-gradient(135deg, var(--primary), var(--accent)); background-clip: text; -webkit-background-clip: text; color: transparent; }
        .hamburger-label { display: none; font-size: 1.9rem; cursor: pointer; color: var(--primary); }
        .nav-links { display: flex; gap: 2rem; list-style: none; align-items: center; }
        .nav-links a { text-decoration: none; font-weight: 500; color: var(--text-dark); transition: var(--transition); padding: 0.5rem 0; position: relative; }
        .nav-links a:hover { color: var(--primary); }
        .nav-links a::after { content: ''; position: absolute; bottom: 0; left: 0; width: 0; height: 2px; background: var(--primary); transition: width 0.25s ease; }
        .nav-links a:hover::after { width: 100%; }

        @media (max-width: 768px) {
            .hamburger-label { display: block; }
            .nav-links {
                position: absolute; top: 100%; left: 0; width: 100%; background: white; flex-direction: column;
                gap: 0; max-height: 0; overflow: hidden; opacity: 0; visibility: hidden;
                transition: max-height 0.4s cubic-bezier(0.2,0.9,0.4,1.1), opacity 0.2s ease;
                box-shadow: 0 12px 20px rgba(0,0,0,0.05); border-top: 1px solid var(--gray-light); z-index: 999;
            }
            .nav-links li { width: 100%; border-bottom: 1px solid #edf2f7; }
            .nav-links a { display: block; padding: 1rem 24px; font-size: 1.1rem; }
            #nav-toggle:checked ~ .navbar .nav-links { max-height: 380px; opacity: 1; visibility: visible; }
        }
        @media (min-width: 769px) {
            .nav-links { display: flex !important; max-height: none !important; opacity: 1 !important; visibility: visible !important; position: static; flex-direction: row; background: transparent; box-shadow: none; border: none; }
        }

        /* Hero секция */
        .hero { background: linear-gradient(135deg, #f0f7ff 0%, #ffffff 100%); padding: 60px 0 80px; }
        .hero-grid { display: flex; align-items: center; gap: 3rem; flex-wrap: wrap; }
        .hero-content { flex: 1; min-width: 280px; }
        .hero-image { flex: 1; text-align: center; }
        .hero-image img { max-width: 100%; max-width: 420px; border-radius: 32px; box-shadow: var(--shadow-md); }

        /* Карточки услуг */
        .cards-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px,1fr)); gap: 2rem; margin-top: 1rem; }
        .card { background: white; border-radius: 28px; padding: 2rem 1.5rem; transition: var(--transition); box-shadow: var(--shadow-sm); text-align: center; }
        .card:hover { transform: translateY(-6px); box-shadow: var(--shadow-md); }
        .card-icon { font-size: 3rem; margin-bottom: 1rem; display: inline-block; }

        /* Дерево */
        .tree-section { background: linear-gradient(145deg, #eaf7e6, #d4e2d0); border-radius: 64px; margin: 40px 0; padding: 40px 20px; box-shadow: inset 0 0 0 1px rgba(255,255,255,0.6), var(--shadow-md); }
        .tree-container { display: flex; flex-direction: column; align-items: center; gap: 20px; }
        .tree-canvas-wrapper { background: #fef9e6; border-radius: 48px; padding: 20px; }
        canvas#orderTreeCanvas { display: block; margin: 0 auto; width: 100%; max-width: 500px; height: auto; background: #fef1cf; border-radius: 36px; }
        .tree-stats { text-align: center; background: white; padding: 12px 24px; border-radius: 60px; font-weight: 600; box-shadow: var(--shadow-sm); }
        .tree-progress-bar { width: 260px; height: 12px; background: #ddd; border-radius: 20px; overflow: hidden; margin: 10px auto; }
        .tree-progress-fill { width: 0%; height: 100%; background: linear-gradient(90deg, #4caf50, #2e7d32); border-radius: 20px; transition: width 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1); }

        /* Блок выполненных заказов (иконки) */
        .completed-orders-section {
            background: var(--light-bg);
            border-radius: 48px;
            margin: 40px 0;
            padding: 40px 20px;
        }
        .orders-icons-grid {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 24px;
            margin: 32px 0 20px;
        }
        .order-icon {
            width: 90px;
            height: 90px;
            background: white;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: var(--shadow-md);
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            font-size: 2rem;
            font-weight: 700;
            color: var(--primary);
            position: relative;
        }
        .order-icon:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 30px -12px rgba(0,0,0,0.2);
        }
        .order-icon span {
            font-size: 0.75rem;
            font-weight: 500;
            margin-top: 4px;
            color: var(--text-muted);
        }
        .empty-orders {
            text-align: center;
            color: var(--text-muted);
            padding: 20px;
            font-style: italic;
        }

        /* Всплывающее описание заказа (плавная анимация) */
        .order-detail-popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            background: white;
            border-radius: 40px;
            padding: 28px 32px;
            max-width: 380px;
            width: 90%;
            z-index: 3000;
            box-shadow: 0 40px 60px rgba(0,0,0,0.3);
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transition: transform 0.25s cubic-bezier(0.2, 0.9, 0.4, 1.1), opacity 0.2s, visibility 0s linear 0.25s;
            backdrop-filter: blur(0px);
        }
        .order-detail-popup.active {
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
            visibility: visible;
            transition: transform 0.3s cubic-bezier(0.2, 1.1, 0.4, 1), opacity 0.25s, visibility 0s linear 0s;
        }
        .popup-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            backdrop-filter: blur(2px);
            z-index: 2999;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.25s, visibility 0s linear 0.25s;
        }
        .popup-overlay.active {
            opacity: 1;
            visibility: visible;
            transition: opacity 0.25s, visibility 0s linear 0s;
        }
        .close-popup {
            background: none;
            border: none;
            font-size: 1.8rem;
            position: absolute;
            top: 12px;
            right: 20px;
            cursor: pointer;
            color: #8fadbb;
        }
        .order-detail-popup h4 { font-size: 1.6rem; margin-bottom: 12px; color: var(--primary); }
        .order-detail-popup p { margin: 8px 0; color: #2c3e50; }

        /* QR-блок */
        .qr-card { background: white; border-radius: 48px; padding: 30px 20px; box-shadow: var(--shadow-md); text-align: center; max-width: 480px; margin: 20px auto; }
        .qr-wrapper { display: flex; justify-content: center; margin: 10px 0; cursor: pointer; }
        canvas#qrCanvas { max-width: 260px; width: 100%; height: auto; border-radius: 32px; }

        /* Модалка оплаты */
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.6); backdrop-filter: blur(3px);
            display: flex; justify-content: center; align-items: center;
            visibility: hidden; opacity: 0; transition: 0.2s; z-index: 2000;
        }
        .modal-overlay.active { visibility: visible; opacity: 1; }
        .modal-container {
            background: white; width: 90%; max-width: 460px; border-radius: 56px;
            padding: 2rem 1.5rem; transform: scale(0.2) rotate(-8deg); opacity: 0;
            transition: transform 0.42s cubic-bezier(0.34,1.3,0.55,1), opacity 0.35s;
            position: relative;
        }
        .modal-overlay.active .modal-container {
            transform: scale(1) rotate(0deg);
            opacity: 1;
            animation: bubblePop 0.5s cubic-bezier(0.2,1.2,0.4,1) forwards;
        }
        @keyframes bubblePop {
            0% { transform: scale(0.1) rotate(-12deg); opacity: 0; filter: blur(2px); }
            40% { transform: scale(1.08) rotate(2deg); opacity: 0.95; }
            100% { transform: scale(1) rotate(0deg); opacity: 1; filter: blur(0); }
        }
        .close-modal { position: absolute; top: 18px; right: 24px; background: none; border: none; font-size: 2rem; cursor: pointer; color: #8fadbb; }
        .payment-form .form-group { margin-bottom: 1rem; }
        .payment-form input { width: 100%; padding: 12px; border: 1px solid #d1d9e6; border-radius: 36px; font-size: 1rem; }
        .pay-submit { background: linear-gradient(95deg, #2b8c6e, #1c6c4a); border: none; color: white; font-weight: bold; padding: 12px; width: 100%; border-radius: 60px; cursor: pointer; font-size: 1.1rem; margin-top: 8px; }

        footer { background: #111e28; color: #cbdfeb; padding: 48px 0 24px; margin-top: 40px; }
        .footer-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr)); gap: 2rem; }
        .footer-col a { color: #b6cfdf; text-decoration: none; }
        .footer-bottom { text-align: center; padding-top: 2rem; border-top: 1px solid #2a3b46; margin-top: 2rem; }

        /* Кнопка "Наверх" (стрелка) */
        .scroll-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            background: var(--primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: var(--shadow-md);
            transition: var(--transition);
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s, visibility 0.3s, transform 0.2s;
            font-size: 1.8rem;
            border: none;
        }
        .scroll-to-top.show {
            opacity: 1;
            visibility: visible;
        }
        .scroll-to-top:hover {
            background: var(--primary-dark);
            transform: translateY(-3px);
        }
        @media (max-width: 768px) {
            .scroll-to-top { width: 42px; height: 42px; bottom: 20px; right: 20px; font-size: 1.5rem; }
        }

        .text-center { text-align: center; }
    </style>
</head>
<body>

<input type="checkbox" id="nav-toggle">
<div class="navbar">
    <div class="nav-container">
        <div class="logo">ARTStz<span style="color:var(--accent);">·Pay</span></div>
        <label for="nav-toggle" class="hamburger-label">☰</label>
        <ul class="nav-links">
            <li><a href="#">Главная</a></li>
            <li><a href="#services">Услуги</a></li>
            <li><a href="#tree">Дерево</a></li>
            <li><a href="#orders-history">Заказы</a></li>
            <li><a href="#qrpay">Оплата</a></li>
        </ul>
    </div>
</div>

<main>
    <section class="hero">
        <div class="container hero-grid">
            <div class="hero-content">
                <h1>Создаем для вас адаптивный веб, приложения, корпоративные решения для бизнеса. <br></h1>
                <p>Каждый успешный платёж питает "Дерево-заказов", а выполненные заказы сохраняются в истории заказов.</p>
                <div class="hero-actions"><a href="#qrpay" class="btn">Оплатить заказ</a><a href="#tree" class="btn btn-outline">Смотреть дерево</a></div>
            </div>
<div class="hero-image"><img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 750 280'%3E%3Crect width='750' height='280' fill='%234f9da6'/%3E%3Ctext x='50%25' y='35%25' dominant-baseline='middle' text-anchor='middle' fill='white' font-family='Arial, sans-serif' font-size='26' font-weight='bold' font-style='italic'%3E%3Ctspan x='50%25' dy='0'%3EБлагодаря высокой скорости и новым технологиям,%3C/tspan%3E%3Ctspan x='50%25' dy='32'%3Eмы реализуем задуманное и поддерживаем%3C/tspan%3E%3Ctspan x='50%25' dy='32'%3Eсотрудничество с новыми компаниями.%3C/tspan%3E%3C/text%3E%3C/svg%3E" alt="рост"></div>
        </div>
    </section>

    <section id="services"><div class="container"><h2>Возможности</h2><div class="cards-grid">
        <div class="card"><div class="card-icon">🌳</div><h3>Дерево заказов</h3><p>Рост от каждого платежа. Плоды падают — цикл обновления.</p></div>
        <div class="card"><div class="card-icon">📋</div><h3>История заказов</h3><p>Кликабельные иконки с описанием каждого выполненного заказа.</p></div>
        <div class="card"><div class="card-icon">💳</div><h3>Оплата через QR</h3><p>Интеграция с платежным сервисом.</p></div>
    </div></div></section>

    <!-- ДЕРЕВО -->
    <div class="container tree-section" id="tree"><div class="tree-container">
        <h2>🌳 Дерево процветания</h2>
        <div class="tree-canvas-wrapper"><canvas id="orderTreeCanvas" width="500" height="500"></canvas></div>
        <div class="tree-stats"><div>🌱 Заказов совершено: <span id="ordersCount">0</span></div>
        <div>📈 Рост дерева: <span id="growthPercent">0</span>%</div>
        <div class="tree-progress-bar"><div class="tree-progress-fill" id="growthFill"></div></div>
        <div style="font-size:0.8rem;">✨ При 100% плоды падают, дерево растёт заново ✨</div>
    </div></div></div>

    <!-- ВЫПОЛНЕННЫЕ ЗАКАЗЫ (кликабельные иконки) -->
    <div class="container completed-orders-section" id="orders-history">
        <h2>📋 Выполненные заказы</h2>
        <div class="section-subtitle">Нажмите на иконку, чтобы увидеть детали заказа</div>
        <div id="ordersIconsContainer" class="orders-icons-grid">
            <div class="empty-orders">Пока нет выполненных заказов. Сделайте первый платёж!</div>
        </div>
    </div>

    <!-- QR + ОПЛАТА -->
    <div class="container" id="qrpay"><div class="qr-card"><h3>ARTStz ✦ Оплата по QR</h3>
        <div class="qr-wrapper" id="qrClickZone"><canvas id="qrCanvas" width="300" height="300"></canvas></div>
        <div class="tap-hint" style="background:#e3f0f5; display:inline-block; padding:6px 18px; border-radius:50px;">🔘 Нажмите на QR → оплатить заказ</div>
        <p style="margin-top:12px;">Услуга: Дизайн‑проект / Консультация • 1500 ₽</p>
    </div></div>

    <section><div class="container text-center"><h2>Разработка веб-сайтов и приложений под ваши требования...</h2><a href="#qrpay" class="btn">Оплатить сейчас</a></div></section>
</main>

<footer id="contact"><div class="container"><div class="footer-grid">
    <div class="footer-col"><h4>ARTStz</h4><p>Создадим то, что вам нужно в разумные сроки и бюджет.</p></div>
    <div class="footer-col"><h4>Контакты</h4><p>📧 TrustHR495@gmail.com</p><p>📞 +7 (916) 217-53-33</p></div>
    <div class="footer-col"><h4>Соцсети</h4><p><a href="https://t.me/ARTStz">Telegram</a> | <a href="https://vk.com/artemitsold">VK</a></p><p>©2026</p></div>
</div><div class="footer-bottom">✨ Кликайте на иконки заказов — будем ждать Вас❤️✨</div></div></footer>

<!-- Кнопка "Наверх" (стрелка) -->
<div class="scroll-to-top" id="scrollToTopBtn" aria-label="Наверх">↑</div>

<!-- Модалка оплаты -->
<div id="paymentModal" class="modal-overlay"><div class="modal-container"><button class="close-modal" id="closeModalBtn">&times;</button>
    <h3 style="font-size:1.8rem;">💎 Оплатить заказ</h3><div class="payment-detail" style="background:#f0f7fa; border-radius:40px; padding:1rem; margin:1rem 0;"><p>Услуга: Дизайн-проект / Консультация</p><div style="font-size:2rem; font-weight:800;">1 500 ₽</div></div>
    <form id="paymentGatewayForm" class="payment-form"><div class="form-group"><input type="text" id="cardNumber" placeholder="Номер карты (4242 4242 4242 4242)" required></div>
    <div style="display:flex; gap:12px;"><div class="form-group"><input type="text" id="expiry" placeholder="ММ/ГГ" required></div><div class="form-group"><input type="text" id="cvc" placeholder="CVC" required></div></div>
    <div class="form-group"><input type="text" id="holderName" placeholder="Имя держателя" required></div>
    <button type="submit" class="pay-submit">Оплатить и сделать заказ 🌳</button></form>
    <p id="paymentStatus" style="font-size:0.8rem; text-align:center; margin-top:12px;"></p>
</div></div>

<!-- Попап для описания заказа (плавная анимация) -->
<div id="orderDetailPopup" class="order-detail-popup"><button class="close-popup" id="closePopupBtn">&times;</button>
    <div id="popupContent"><h4>Заказ #</h4><p><strong>Услуга:</strong> <span id="popupService"></span></p><p><strong>Сумма:</strong> <span id="popupAmount"></span> ₽</p><p><strong>Дата:</strong> <span id="popupDate"></span></p><p><strong>Статус:</strong> ✅ Выполнен</p></div>
</div>
<div id="popupOverlay" class="popup-overlay"></div>

<script>
    (function(){
        // ---- ДЕРЕВО (логика роста, падение плодов) ----
        const canvas = document.getElementById('orderTreeCanvas');
        const ctx = canvas.getContext('2d');
        let width = 500, height = 500;
        canvas.width = width; canvas.height = height;
        let ordersCompleted = 0;
        let growthPercent = 0;
        let maxOrdersForFull = 5;
        let fallingFruits = [];
        let isResetting = false;

        // ---- ОБЛАКА ----
        let clouds = [
            { x: 80, y: 70, radius: 30, speed: 0.4 },
            { x: 300, y: 90, radius: 40, speed: 0.3 },
            { x: 420, y: 50, radius: 28, speed: 0.5 },
            { x: 180, y: 120, radius: 25, speed: 0.35 }
        ];

        function updateClouds() {
            for (let c of clouds) {
                c.x += c.speed;
                if (c.x > width + c.radius * 2) c.x = -c.radius * 2;
                if (c.x < -c.radius * 2) c.x = width + c.radius * 2;
            }
        }

        // ---- СОЛНЦЕ (уменьшенная скорость вращения, мягкие и выразительные лучи, освещает табличку) ----
        let sunAngle = 0;
        function drawSun() {
            const sunX = width - 55;
            const sunY = 65;
            // лучи: 24 луча, медленное вращение, полупрозрачные, с градиентом
            const rayCount = 24;
            const now = Date.now() * 0.0008; // уменьшенная скорость (было 0.003, теперь 0.0008)
            for (let i = 0; i < rayCount; i++) {
                let angle = now + i * Math.PI * 2 / rayCount;
                let dx = Math.cos(angle) * 22;
                let dy = Math.sin(angle) * 22;
                // создаём эффект мягкого свечения
                ctx.beginPath();
                ctx.moveTo(sunX + dx * 0.4, sunY + dy * 0.4);
                ctx.lineTo(sunX + dx * 1.2, sunY + dy * 1.2);
                ctx.lineWidth = 4;
                ctx.strokeStyle = `rgba(255, 200, 70, 0.6)`;
                ctx.stroke();
                // второй слой лучей для выразительности
                ctx.beginPath();
                ctx.moveTo(sunX + dx * 0.6, sunY + dy * 0.6);
                ctx.lineTo(sunX + dx * 1.6, sunY + dy * 1.6);
                ctx.lineWidth = 2.5;
                ctx.strokeStyle = `rgba(255, 220, 100, 0.7)`;
                ctx.stroke();
            }
            // свечение вокруг солнца
            ctx.shadowBlur = 20;
            ctx.shadowColor = "#FFD966";
            ctx.beginPath();
            ctx.arc(sunX, sunY, 24, 0, Math.PI * 2);
            ctx.fillStyle = "rgba(255, 193, 7, 0.3)";
            ctx.fill();
            ctx.shadowBlur = 0;
            // само солнце
            ctx.beginPath();
            ctx.arc(sunX, sunY, 20, 0, Math.PI * 2);
            ctx.fillStyle = "#FFC107";
            ctx.fill();
            ctx.fillStyle = "#FFB300";
            ctx.beginPath();
            ctx.arc(sunX - 2, sunY - 2, 6, 0, Math.PI * 2);
            ctx.fill();
            // блик
            ctx.beginPath();
            ctx.arc(sunX - 6, sunY - 6, 3, 0, Math.PI * 2);
            ctx.fillStyle = "rgba(255,255,200,0.8)";
            ctx.fill();
        }

        // ---- ТРАВА И КУСТЫ (много зелени) ----
        function drawGrassAndBushes() {
            for (let i = 0; i < 55; i++) {
                let x = i * 10;
                let h = 12 + Math.sin(i * 0.6) * 6;
                ctx.beginPath();
                ctx.moveTo(x, height - 70);
                ctx.lineTo(x + 4, height - 70 - h);
                ctx.lineTo(x - 4, height - 70 - h);
                ctx.fillStyle = "#5a9e4e";
                ctx.fill();
            }
            ctx.fillStyle = "#4c8b3c";
            ctx.beginPath();
            ctx.ellipse(40, height - 74, 18, 12, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(460, height - 78, 20, 14, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(100, height - 80, 15, 10, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(400, height - 82, 16, 11, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(220, height - 76, 14, 9, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(310, height - 80, 17, 11, 0, 0, Math.PI * 2);
            ctx.fill();
            for (let i = 0; i < 30; i++) {
                let x = 20 + i * 16;
                let y = height - 72 - Math.sin(i) * 5;
                ctx.beginPath();
                ctx.moveTo(x, y);
                ctx.lineTo(x + 5, y - 10);
                ctx.lineTo(x - 5, y - 10);
                ctx.fillStyle = "#6bb84a";
                ctx.fill();
            }
        }

        // ---- ТАБЛИЧКА С ЗАКАЗАМИ (освещается солнцем) ----
        function drawOrderSignboard() {
            const signX = width - 100;
            const signY = height - 130;
            const signW = 80;
            const signH = 35;
            // добавляем эффект освещения от солнца (жёлтый блик сверху)
            ctx.fillStyle = "#C49A6C";
            ctx.shadowBlur = 4;
            ctx.fillRect(signX, signY, signW, signH);
            ctx.fillStyle = "#A57C4C";
            ctx.fillRect(signX + 3, signY + 3, signW - 6, signH - 6);
            // имитация солнечного блика на табличке
            ctx.fillStyle = "rgba(255, 220, 100, 0.4)";
            ctx.fillRect(signX + 2, signY + 2, signW - 4, 8);
            ctx.fillStyle = "#5D3A1A";
            ctx.font = "bold 14px 'Inter'";
            ctx.fillText("ЗАКАЗЫ", signX + 18, signY + 18);
            ctx.fillStyle = "#F5E6D3";
            ctx.font = "bold 18px monospace";
            ctx.fillText(`${ordersCompleted}`, signX + 36, signY + 32);
            ctx.shadowBlur = 0;
        }

        // ---- ОСНОВНАЯ ФУНКЦИЯ ОТРИСОВКИ ----
        function drawTree() {
            ctx.clearRect(0, 0, width, height);
            // небо
            ctx.fillStyle = "#c9e0f0";
            ctx.fillRect(0, 0, width, height);
            // облака
            for (let c of clouds) {
                ctx.beginPath();
                ctx.arc(c.x, c.y, c.radius, 0, Math.PI * 2);
                ctx.arc(c.x - c.radius * 0.6, c.y - c.radius * 0.2, c.radius * 0.7, 0, Math.PI * 2);
                ctx.arc(c.x + c.radius * 0.6, c.y - c.radius * 0.2, c.radius * 0.7, 0, Math.PI * 2);
                ctx.fillStyle = "rgba(255,255,245,0.95)";
                ctx.fill();
            }
            // солнце
            drawSun();
            // земля
            ctx.fillStyle = "#ccaa6e";
            ctx.fillRect(0, height - 70, width, 70);
            ctx.fillStyle = "#a57c44";
            ctx.fillRect(0, height - 65, width, 15);
            // трава
            drawGrassAndBushes();
            // ствол
            let trunkHeight = 90 + (growthPercent / 100) * 50;
            let trunkWidth = 32 + (growthPercent / 100) * 16;
            ctx.fillStyle = "#8B5A2B";
            ctx.fillRect(width / 2 - trunkWidth / 2, height - 70 - trunkHeight, trunkWidth, trunkHeight);
            // крона
            let crownRadius = 60 + (growthPercent / 100) * 55;
            let gradient = ctx.createRadialGradient(width / 2, height - 70 - trunkHeight - 20, 10, width / 2, height - 70 - trunkHeight - 40, crownRadius);
            gradient.addColorStop(0, '#5a9e4e');
            gradient.addColorStop(1, '#2c6e2c');
            ctx.fillStyle = gradient;
            ctx.beginPath();
            ctx.arc(width / 2, height - 70 - trunkHeight - crownRadius * 0.55, crownRadius, 0, Math.PI * 2);
            ctx.fill();
            ctx.fillStyle = "#3c8c40";
            ctx.beginPath();
            ctx.ellipse(width / 2 - crownRadius * 0.5, height - 70 - trunkHeight - crownRadius * 0.3, crownRadius * 0.5, crownRadius * 0.6, 0, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.ellipse(width / 2 + crownRadius * 0.5, height - 70 - trunkHeight - crownRadius * 0.3, crownRadius * 0.5, crownRadius * 0.6, 0, 0, Math.PI * 2);
            ctx.fill();
            // доп. листья
            ctx.fillStyle = "#4a9e3a";
            for (let i = 0; i < 18; i++) {
                let angle = i * Math.PI * 2 / 18;
                let rad = crownRadius * 0.92;
                let x = width / 2 + Math.cos(angle) * rad;
                let y = height - 70 - trunkHeight - crownRadius * 0.48 + Math.sin(angle * 2) * 6;
                ctx.beginPath();
                ctx.ellipse(x, y, 7, 11, angle, 0, Math.PI * 2);
                ctx.fill();
            }
            // плоды
            let fruitCount = Math.floor((growthPercent / 100) * 12);
            for (let i = 0; i < fruitCount; i++) {
                let angle = (i / Math.max(1, fruitCount)) * Math.PI * 2 + Date.now() * 0.003;
                let rad = crownRadius * 0.7;
                let x = width / 2 + Math.cos(angle) * rad * (0.6 + Math.sin(i) * 0.3);
                let y = height - 70 - trunkHeight - crownRadius * 0.4 + Math.sin(angle * 2) * 12;
                ctx.beginPath();
                ctx.fillStyle = "#e34d2b";
                ctx.arc(x, y, 8, 0, Math.PI * 2);
                ctx.fill();
                ctx.fillStyle = "#6b3a1c";
                ctx.beginPath();
                ctx.moveTo(x - 2, y - 5);
                ctx.lineTo(x, y - 10);
                ctx.lineTo(x + 2, y - 5);
                ctx.fill();
            }
            // падающие плоды
            for (let f of fallingFruits) {
                ctx.beginPath();
                ctx.fillStyle = `rgba(227, 77, 43, ${f.alpha})`;
                ctx.arc(f.x, f.y, f.radius || 8, 0, Math.PI * 2);
                ctx.fill();
            }
            // табличка с заказами
            drawOrderSignboard();
        }

        // ---- ЛОГИКА ПАДЕНИЯ ПЛОДОВ ----
        function startFruitFall() {
            if (isResetting) return;
            isResetting = true;
            fallingFruits = [];
            for (let i = 0; i < 14; i++) {
                fallingFruits.push({
                    x: width / 2 + (Math.random() - 0.5) * 130,
                    y: height - 150 + Math.random() * 60,
                    radius: 6 + Math.random() * 5,
                    velocityY: 2 + Math.random() * 4,
                    alpha: 1
                });
            }
            let fallInterval = setInterval(() => {
                let anyActive = false;
                for (let f of fallingFruits) {
                    f.y += f.velocityY;
                    if (f.y > height - 50) {
                        f.y = height - 52;
                        f.alpha -= 0.05;
                        if (f.alpha <= 0) f.alpha = 0;
                    } else anyActive = true;
                }
                fallingFruits = fallingFruits.filter(f => f.alpha > 0.02);
                drawTree();
                if (fallingFruits.length === 0) {
                    clearInterval(fallInterval);
                    ordersCompleted = 0;
                    updateGrowthFromOrders();
                    isResetting = false;
                    drawTree();
                } else drawTree();
            }, 30);
        }

        function updateGrowthFromOrders() {
            let percent = (ordersCompleted / maxOrdersForFull) * 100;
            if (percent > 100) percent = 100;
            growthPercent = percent;
            document.getElementById('ordersCount').innerText = ordersCompleted;
            document.getElementById('growthPercent').innerText = Math.floor(growthPercent);
            document.getElementById('growthFill').style.width = growthPercent + '%';
        }

        // ---- МАССИВ ЗАКАЗОВ (история) ----
        let completedOrders = [];

        function renderOrderIcons() {
            const container = document.getElementById('ordersIconsContainer');
            if (!container) return;
            if (completedOrders.length === 0) {
                container.innerHTML = '<div class="empty-orders">Пока нет выполненных заказов. Сделайте первый платёж!</div>';
                return;
            }
            let html = '';
            completedOrders.forEach((order, idx) => {
                html += `<div class="order-icon" data-order-idx="${idx}">
                            <span>✅</span>
                            <span>Заказ #${order.id}</span>
                         </div>`;
            });
            container.innerHTML = html;
            document.querySelectorAll('.order-icon').forEach(el => {
                el.addEventListener('click', (e) => {
                    const idx = el.getAttribute('data-order-idx');
                    if (idx !== null && completedOrders[parseInt(idx)]) showOrderDetails(completedOrders[parseInt(idx)]);
                });
            });
        }

        const popup = document.getElementById('orderDetailPopup');
        const popupOverlay = document.getElementById('popupOverlay');
        function showOrderDetails(order) {
            document.getElementById('popupService').innerText = order.service;
            document.getElementById('popupAmount').innerText = order.amount;
            document.getElementById('popupDate').innerText = order.date;
            popup.classList.add('active');
            popupOverlay.classList.add('active');
        }
        function closeOrderPopup() {
            popup.classList.remove('active');
            popupOverlay.classList.remove('active');
        }
        document.getElementById('closePopupBtn').addEventListener('click', closeOrderPopup);
        popupOverlay.addEventListener('click', closeOrderPopup);

        function addNewOrder(service, amount) {
            const newId = completedOrders.length + 1;
            const now = new Date();
            const dateStr = `${now.getDate()}.${now.getMonth() + 1}.${now.getFullYear()} ${now.getHours()}:${now.getMinutes()}`;
            const newOrder = {
                id: newId,
                service: service,
                amount: amount,
                date: dateStr,
                description: `Оплата услуги "${service}" на сумму ${amount} руб.`
            };
            completedOrders.unshift(newOrder);
            renderOrderIcons();
            ordersCompleted++;
            updateGrowthFromOrders();
            drawTree();
            if (growthPercent >= 100 && ordersCompleted >= maxOrdersForFull) startFruitFall();
            else drawTree();
        }

        // ---- QR КОД ----
        const qrCanvas = document.getElementById('qrCanvas');
        const paymentUrl = "https://demo-payment.artstz/pay?order=tree";
        QRCode.toCanvas(qrCanvas, paymentUrl, { width: 280, margin: 2, color: { dark: '#1C3A4F', light: '#FFFFFF' }, errorCorrectionLevel: 'H' }, function (err) {
            if (!err) drawLogoInCenter(qrCanvas, 280);
        });
        function drawLogoInCenter(canvas, size) {
            const ctxLogo = canvas.getContext('2d');
            const logoSize = size * 0.24;
            const cx = size / 2, cy = size / 2;
            ctxLogo.save();
            ctxLogo.beginPath();
            ctxLogo.arc(cx, cy, logoSize / 1.8, 0, Math.PI * 2);
            ctxLogo.fillStyle = '#FFFFFF';
            ctxLogo.fill();
            ctxLogo.font = `bold ${Math.floor(logoSize * 0.4)}px 'Segoe UI'`;
            ctxLogo.fillStyle = '#1F4F6E';
            ctxLogo.textAlign = 'center';
            ctxLogo.textBaseline = 'middle';
            ctxLogo.fillText("ARTStz", cx, cy);
            ctxLogo.restore();
        }

        // ---- МОДАЛЬНОЕ ОКНО ОПЛАТЫ ----
        const modal = document.getElementById('paymentModal');
        const qrZone = document.getElementById('qrClickZone');
        const closeModalBtn = document.getElementById('closeModalBtn');
        const payForm = document.getElementById('paymentGatewayForm');
        const statusMsg = document.getElementById('paymentStatus');

        function openModal() { modal.classList.add('active'); }
        function closeModal() { modal.classList.remove('active'); statusMsg.innerText = ''; }
        qrZone.addEventListener('click', openModal);
        closeModalBtn.addEventListener('click', closeModal);
        modal.addEventListener('click', (e) => { if (e.target === modal) closeModal(); });

        payForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const cardNum = document.getElementById('cardNumber').value.trim();
            if (!cardNum) { statusMsg.innerText = '❌ Введите номер карты'; return; }
            statusMsg.innerText = '⏳ Обработка платежа...';
            setTimeout(() => {
                addNewOrder('Дизайн-проект / Консультация', 1500);
                statusMsg.innerHTML = '✅ Оплата успешна! Заказ добавлен в историю, дерево подросло.';
                setTimeout(() => { closeModal(); payForm.reset(); statusMsg.innerText = ''; }, 1300);
            }, 800);
        });

        // ---- АНИМАЦИОННЫЙ ЦИКЛ (облака и солнце) ----
        function animateScene() {
            updateClouds();
            drawTree();
            requestAnimationFrame(animateScene);
        }
        animateScene();

        // ---- КНОПКА "НАВЕРХ" ----
        const scrollBtn = document.getElementById('scrollToTopBtn');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 400) {
                scrollBtn.classList.add('show');
            } else {
                scrollBtn.classList.remove('show');
            }
        });
        scrollBtn.addEventListener('click', () => {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        // ---- ЗАКРЫТИЕ МОБИЛЬНОГО МЕНЮ ----
        const navToggle = document.getElementById('nav-toggle');
        const navLinks = document.querySelectorAll('.nav-links a');
        navLinks.forEach(link => link.addEventListener('click', () => { if (window.innerWidth <= 768 && navToggle.checked) navToggle.checked = false; }));
        window.addEventListener('resize', () => { if (window.innerWidth > 768 && navToggle.checked) navToggle.checked = false; });

        // Инициализация
        updateGrowthFromOrders();
        drawTree();
        renderOrderIcons();
    })();
</script>
</body>
</html>
