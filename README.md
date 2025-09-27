<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sana Özel Bahçe 🌸</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Handlee&display=swap" rel="stylesheet"> 
    <style>
        :root {
            --header-color: #5D3FD3; /* Mistik Mor */
            --grass-color: #4CAF50; /* Canlı Çimen Yeşili */
            --sky-color-top: #87CEEB;
            --sky-color-bottom: #B0E0E6;
        }

        body {
            margin: 0;
            overflow: hidden;
            font-family: 'Handlee', cursive;
            color: #333;
            cursor: pointer;
            background: linear-gradient(135deg, #FFC0CB 0%, #ADD8E6 100%);
        }

        /* YouTube Oynatıcısı için Gizleme Stili */
        #youtube-player {
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
            font-size: 3.5em; /* Masaüstü boyutu */
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
            font-size: 5em; /* Masaüstü boyutu */
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
        }
        #garden.active {
            opacity: 1;
        }

        .flower {
            position: absolute;
            font-size: 4.5em; /* Masaüstü boyutu */
            user-select: none;
            pointer-events: none;
            animation: fadeInRotate 0.7s ease-out forwards, sway var(--sway-duration, 5s) ease-in-out infinite alternate; 
            transform: scale(0);
        }

        /* ******************************************* */
        /* MOBİL UYUMLULUK (RESPONSIVE DESIGN) KISMI */
        /* ******************************************* */
        @media (max-width: 600px) {
            /* 600 piksel altındaki (çoğu mobil ekran) cihazlar için ayarlar */
            
            #welcome-screen h1 {
                font-size: 3em; /* Hoş Geldin yazısını küçült */
            }

            #garden-title {
                font-size: 2em; /* Bahçe başlığını küçült */
                top: 20px; /* Üste daha yakın konumlandır */
                width: 90%; /* Başlık için mobil ekranlarda yer aç */
            }
            
            .flower {
                font-size: 3em; /* Çiçeklerin boyutunu küçült */
            }
        }
        
        /* Animasyonlar (Öncekiyle Aynı) */
        @keyframes fadeInRotate { /* ... */ }
        @keyframes sway { /* ... */ }
        @keyframes pulseBackground { /* ... */ }
        @keyframes slideIn { /* ... */ }
        @keyframes bounceIn { /* ... */ }

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
        const musicFrame = document.getElementById('music-frame'); 
        
        const flowerEmojis = ['🌸', '🌺', '🌼', '🌷', '🌻', '🌹', '💐', '♥️', '♥️']; 

        continueButton.addEventListener('click', () => {
            document.getElementById('youtube-player').style.display = 'block'; 
            
            welcomeScreen.classList.add('hidden');

            setTimeout(() => {
                garden.classList.add('active');
            }, 1000); 
        });

        garden.addEventListener('click', (event) => {
            const flower = document.createElement('span');
            flower.classList.add('flower');
            
            flower.textContent = flowerEmojis[Math.floor(Math.random() * flowerEmojis.length)];

            const randomRotation = Math.floor(Math.random() * 360); 
            const randomSwayDuration = `${5 + Math.random() * 3}s`;

            flower.style.setProperty('--random-rotation', `${randomRotation}deg`);
            flower.style.setProperty('--sway-duration', randomSwayDuration);

            // Tıklanan yerin koordinatlarına göre çiçeği yerleştir
            flower.style.left = `${event.clientX - 30}px`; 
            flower.style.top = `${event.clientY - 30}px`;

            garden.appendChild(flower);
        });
    </script>

</body>
</html>
