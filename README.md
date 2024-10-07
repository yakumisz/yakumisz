<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YAKUMI - Camisas e Moletons</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            background-color: #1a1a1a;
            color: #ffffff;
            overflow-x: hidden;
        }
        #background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url('https://source.unsplash.com/random/1920x1080/?fashion');
            background-size: cover;
            background-position: center;
            filter: brightness(0.5);
            z-index: -1;
        }
        header {
            background-color: rgba(85, 26, 139, 0.8);
            padding: 20px;
            text-align: center;
        }
        .logo {
            font-family: 'Arial', sans-serif;
            font-size: 3em;
            font-weight: bold;
            color: #00ff00;
            text-shadow: 0 0 10px rgba(0, 255, 0, 0.7);
        }
        nav {
            background-color: rgba(0, 128, 0, 0.8);
            padding: 10px;
            display: flex;
            justify-content: center;
        }
        nav a {
            color: #ffffff;
            text-decoration: none;
            margin: 0 20px;
            font-size: 1.2em;
            position: relative;
            overflow: hidden;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        .product {
            background-color: rgba(26, 26, 26, 0.8);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.5s ease;
            position: relative;
            overflow: hidden;
        }
        .product h2 {
            color: #00ff00;
        }
        #canvas {
            position: fixed;
            top: 0;
            left: 0;
            z-index: -1;
        }
    </style>
</head>
<body>
    <div id="background"></div>
    <canvas id="canvas"></canvas>
    <header>
        <h1 class="logo">YAKUMI</h1>
    </header>
    <nav>
        <a href="#camisas">Camisas</a>
        <a href="#moletons">Moletons</a>
        <a href="#sobre">Sobre</a>
        <a href="#contato">Contato</a>
    </nav>
    <div class="container">
        <div id="camisas" class="product">
            <h2>Camisas</h2>
            <p>Confira nossa coleção de camisas estilosas e confortáveis.</p>
        </div>
        <div id="moletons" class="product">
            <h2>Moletons</h2>
            <p>Descubra nossos moletons quentinhos e modernos.</p>
        </div>
    </div>

    <script>
        // Animação de fundo
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 5 + 1;
                this.speedX = Math.random() * 3 - 1.5;
                this.speedY = Math.random() * 3 - 1.5;
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.size > 0.2) this.size -= 0.1;
            }
            draw() {
                ctx.fillStyle = '#00ff00';
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        const particleArray = [];
        function init() {
            for (let i = 0; i < 100; i++) {
                particleArray.push(new Particle());
            }
        }
        init();

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let i = 0; i < particleArray.length; i++) {
                particleArray[i].update();
                particleArray[i].draw();
                if (particleArray[i].size <= 0.2) {
                    particleArray.splice(i, 1);
                    i--;
                    particleArray.push(new Particle());
                }
            }
            requestAnimationFrame(animate);
        }
        animate();

        // Efeito parallax no fundo
        document.addEventListener('mousemove', (e) => {
            const xAxis = (window.innerWidth / 2 - e.pageX) / 25;
            const yAxis = (window.innerHeight / 2 - e.pageY) / 25;
            document.getElementById('background').style.transform = `translate(${xAxis}px, ${yAxis}px)`;
        });

        // Animação nos produtos
        const products = document.querySelectorAll('.product');
        products.forEach(product => {
            product.addEventListener('click', () => {
                product.style.transform = 'scale(1.05) rotate(5deg)';
                setTimeout(() => {
                    product.style.transform = 'scale(1) rotate(0deg)';
                }, 500);
            });
        });

        // Ajuste do tamanho do canvas quando a janela é redimensionada
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            init();
        });
    </script>
</body>
</html>
