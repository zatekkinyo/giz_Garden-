
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Özel Bahçe 🌸</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Handlee&display=swap" rel="stylesheet"> 
    <style>
        :root {
            --header-color: #5D3FD3;
            --grass-color: #4CAF50;
            --sky-color-top: #87CEEB;
            --sky-color-bottom: #B0E0E6;
        }

        body {
            margin: 0;
            overflow: hidden;
            font-family: 'Handlee', cursive;
            color: #333;
            cursor: default; /* Varsayılan imleç */
        }

        /* YouTube Oynatıcısı için Gizleme Stili */
        #youtube-player {
            position: absolute;
            top: 0; left: 0;
            width: 1px; height: 1px;
            overflow: hidden; 
            display: none; 
        }

        /* Başlık Mesajı Stili */
        #garden-title {
            position: absolute;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 50;
            font-family: 'Great Vibes', cursive;
            font-size: 3.5em;
            color: var(--header-color);
            text-shadow: 2px 2px 5px rgba(0,0,0,0.4);
            opacity: 0;
            transition: opacity 1s ease 2s; 
            text-align: center;
        }
        #garden.active #garden-title {
            opacity: 1;
        }

        /* Hoş Geldin Ekranı */
        #welcome-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            z-index: 100;
            transition: opacity 1s ease-out;
            animation: pulseBackground 5s infinite alternate;
        }
        #welcome-screen.hidden {
            opacity: 0;
            pointer-events: none;
        }
        #welcome-screen h1 {
            font-family: 'Great Vibes', cursive; 
            font-size: 5em;
            color: #8A2BE2;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            margin-bottom: 30px;
            animation: slideIn 1.5s ease-out;
        }
        #welcome-screen button {
            padding: 15px 30px;
            font-size: 1.2em;
            background-color: #FF69B4;
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
            animation: bounceIn 1.5s ease-out 0.5s both;
        }

        /* Bahçe Alanı */
        #garden {
            position: relative;
            width: 100vw;
            height: 100vh;
            background: linear-gradient(to bottom, 
                var(--sky-color-top) 0%, 
                var(--sky-color-bottom) 40%, 
                #7CFC00 60%, 
                var(--grass-color) 80%, 
                #8B4513 100% 
            );
            overflow: hidden;
            opacity: 0;
            transition: opacity 2s ease-in-out;
            cursor: crosshair; /* Tıklanabilirliği gösteren imleç */
        }
        #garden.active {
            opacity: 1;
        }

        .flower {
            position: absolute;
            font-size: 4.5em; 
            user-select: none;
            pointer-events: none;
            animation: fadeInRotate 0.7s ease-out forwards, sway var(--sway-duration, 5s) ease-in-out infinite alternate; 
            transform: scale(0);
        }

        /* ******************************************* */
        /* MOBİL UYUMLULUK (RESPONSIVE DESIGN) KISMI */
        /* ******************************************* */
        @media (max-width: 600px) {
            #welcome-screen h1 {
                font-size: 3em; 
            }

            #garden-title {
                font-size: 2em; 
                top: 20px; 
                width: 90%;
            }
            
            .flower {
                font-size: 3em; 
            }
        }
        
        /* Animasyonlar */
        @keyframes fadeInRotate {
            0% { opacity: 0; transform: scale(0) rotate(0deg); }
            100% { opacity: 1; transform: scale(1) rotate(var(--random-rotation, 0deg)); }
        }
        
        @keyframes sway {
            0% { transform: translate(0px, 0px) rotate(var(--random-rotation, 0deg)); }
            100% { transform: translate(5px, -5px) rotate(calc(var(--random-rotation, 0deg) + 2deg)); } 
        }

        @keyframes pulseBackground { 0% { background-color: #e0c3fc; } 100% { background-color: #8ec5fc; } }
        @keyframes slideIn { from { transform: translateY(-50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        @keyframes bounceIn {
            0%, 20%, 40%, 60%, 80%, 100% { transition-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000); }
            0% { opacity: 0; transform: scale3d(.3, .3, .3); }
            20% { transform: scale3d(1.1, 1.1, 1.1); }
            40% { transform: scale3d(.9, .9, .9); }
            60% { opacity: 1; transform: scale3d(1.03, 1.03, 1.03); }
            80% { transform: scale3d(.97, .97, .97); }
            100% { opacity: 1; transform: scale3d(1, 1, 1); }
        }
    </style>
</head>
<body>

    <div id="youtube-player">
        <iframe id="music-frame" width="1" height="1"
            src="https://www.youtube.com/embed/EPMhwX-r8EQ?autoplay=1&loop=1&playlist=EPMhwX-r8EQ&controls=0&disablekb=1&modestbranding=1&fs=0"
            frameborder="0" allow="autoplay; encrypted-media" allowfullscreen>
        </iframe>
    </div>

    <div id="welcome-screen">
        <h1>Hoş Geldin Giz 👋</h1>
        <button id="continue-button">Devam Et ve Bahçeni Gör</button>
    </div>

    <div id="garden">
        <div id="garden-title">Gizmeli Gizemin Bahçesi</div>
    </div>

    <script>
        const continueButton = document.getElementById('continue-button');
        const welcomeScreen = document.getElementById('welcome-screen');
        const garden = document.getElementById('garden');
        const musicPlayer = document.getElementById('youtube-player'); 
        
        const flowerEmojis = ['🌸', '🌺', '🌼', '🌷', '🌻', '🌹', '💐', '♥️', '♥️']; 

        continueButton.addEventListener('click', () => {
            // Müzik çalmayı başlatmak için YouTube oynatıcısını aktif et
            musicPlayer.style.display = 'block'; 
            
            // Hoş geldin ekranını gizle
            welcomeScreen.classList.add('hidden');

            // Bahçe ekranını yavaşça görünür yap
            setTimeout(() => {
                garden.classList.add('active');
            }, 1000); 
        });

        garden.addEventListener('click', (event) => {
            // Sadece bahçe aktifse çiçek çıkar
            if (!garden.classList.contains('active')) {
                return; 
            }
            
            const flower = document.createElement('span');
            flower.classList.add('flower');
            
            flower.textContent = flowerEmojis[Math.floor(Math.random() * flowerEmojis.length)];

            const randomRotation = Math.floor(Math.random() * 360); 
            const randomSwayDuration = `${5 + Math.random() * 3}s`;

            // CSS değişkenlerini ayarla
            flower.style.setProperty('--random-rotation', `${randomRotation}deg`);
            flower.style.setProperty('--sway-duration', randomSwayDuration);

            // Tıklanan yerin koordinatlarına göre çiçeği yerleştir
            // Emojiyi merkeze getirmek için kaydırıyoruz
            flower.style.left = `${event.clientX - 30}px`; 
            flower.style.top = `${event.clientY - 30}px`;

            garden.appendChild(flower);
        });
    </script>

</body>
</html>
