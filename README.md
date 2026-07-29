# Closba-Website
html_code = '''<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CLOSBA</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            background-color: #000;
        }

        /* Background Container */
        .background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            z-index: 1;
        }

        /* Desktop Background */
        .bg-desktop {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Mobile Background */
        .bg-mobile {
            display: none;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        @media (max-width: 768px) {
            .bg-desktop {
                display: none;
            }
            .bg-mobile {
                display: block;
            }
        }

        /* Button Container */
        .button-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
            transition: opacity 0.8s ease-out;
        }

        .button-container.hidden {
            opacity: 0;
            pointer-events: none;
        }

        /* Enter Button */
        .enter-btn {
            background: transparent;
            border: 2px solid #fff;
            color: #fff;
            padding: 20px 60px;
            font-size: 18px;
            letter-spacing: 4px;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
            text-transform: uppercase;
            font-weight: bold;
        }

        .enter-btn:hover {
            background: rgba(255, 255, 255, 0.1);
            box-shadow: 0 0 30px rgba(255, 255, 255, 0.3);
        }

        /* White Powder Lines Animation */
        .powder-line {
            position: absolute;
            background: linear-gradient(90deg, 
                transparent 0%, 
                rgba(255, 255, 255, 0.9) 20%, 
                rgba(255, 255, 255, 1) 50%, 
                rgba(255, 255, 255, 0.9) 80%, 
                transparent 100%);
            height: 2px;
            width: 0;
            opacity: 0;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
        }

        .powder-line.active {
            animation: powderSpread 1.5s ease-out forwards;
        }

        @keyframes powderSpread {
            0% {
                width: 0;
                opacity: 0;
            }
            20% {
                opacity: 1;
            }
            100% {
                width: 300px;
                opacity: 0;
            }
        }

        /* Message Container */
        .message-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 5;
            text-align: center;
            opacity: 0;
            transition: opacity 1.5s ease-in;
            padding: 20px;
        }

        .message-container.visible {
            opacity: 1;
        }

        .message-text {
            color: #fff;
            font-size: 28px;
            line-height: 1.6;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
            letter-spacing: 2px;
        }

        .message-text .brand {
            font-size: 48px;
            font-weight: bold;
            display: block;
            margin-bottom: 20px;
            letter-spacing: 8px;
        }

        .message-text .signature {
            font-size: 20px;
            margin-top: 30px;
            font-style: italic;
            opacity: 0.8;
        }

        @media (max-width: 768px) {
            .message-text {
                font-size: 20px;
            }
            .message-text .brand {
                font-size: 36px;
            }
            .message-text .signature {
                font-size: 16px;
            }
            .enter-btn {
                padding: 15px 40px;
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <!-- Background Images -->
    <div class="background">
        <img src="images/background-desktop.jpg" alt="CLOSBA Background" class="bg-desktop">
        <img src="images/background-mobile.jpg" alt="CLOSBA Background Mobile" class="bg-mobile">
    </div>

    <!-- Enter Button with Powder Animation -->
    <div class="button-container" id="buttonContainer">
        <button class="enter-btn" id="enterBtn">ENTRAR</button>
    </div>

    <!-- Message -->
    <div class="message-container" id="messageContainer">
        <div class="message-text">
            <span class="brand">CLOSBA</span>
            Lo mejor está por venir,<br>espéralo.
            <div class="signature">- Angelus</div>
        </div>
    </div>

    <script>
        const enterBtn = document.getElementById('enterBtn');
        const buttonContainer = document.getElementById('buttonContainer');
        const messageContainer = document.getElementById('messageContainer');

        enterBtn.addEventListener('click', function() {
            // Create powder lines animation
            createPowderLines();
            
            // Hide button after animation
            setTimeout(() => {
                buttonContainer.classList.add('hidden');
                
                // Show message
                setTimeout(() => {
                    messageContainer.classList.add('visible');
                }, 800);
            }, 1500);
        });

        function createPowderLines() {
            const btnRect = enterBtn.getBoundingClientRect();
            const centerX = btnRect.left + btnRect.width / 2;
            const centerY = btnRect.top + btnRect.height / 2;
            
            // Create multiple powder lines radiating from button
            for (let i = 0; i < 12; i++) {
                setTimeout(() => {
                    const line = document.createElement('div');
                    line.className = 'powder-line';
                    
                    // Random angle
                    const angle = (i / 12) * Math.PI * 2;
                    const distance = 100;
                    
                    line.style.left = centerX + 'px';
                    line.style.top = centerY + 'px';
                    line.style.transform = `rotate(${angle}rad)`;
                    line.style.transformOrigin = '0 50%';
                    
                    document.body.appendChild(line);
                    
                    // Trigger animation
                    setTimeout(() => {
                        line.classList.add('active');
                    }, 50);
                    
                    // Remove line after animation
                    setTimeout(() => {
                        line.remove();
                    }, 1500);
                }, i * 100);
            }
        }
    </script>
</body>
</html>'''
