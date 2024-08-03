<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personagem em Movimento</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: lightblue;
        }
        .game-container {
            position: relative;
            width: 600px;
            height: 600px;
            background-color: white;
            border: 2px solid black;
        }
        .character {
            position: absolute;
            width: 40px;
            height: 40px;
            background-color: red;
            border-radius: 50%;
            top: 0;
            left: 0;
            transition: top 0.1s, left 0.1s; /* Suaviza a movimentação */
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="character" id="character"></div>
    </div>
    <audio id="collision-sound" src="collision-sound.mp3"></audio> <!-- Adiciona o som de colisão -->
    <script>
        const character = document.getElementById('character');
        const collisionSound = document.getElementById('collision-sound');
        const step = 10; // Define o tamanho do passo em pixels
        let x = 0;
        let y = 0;

        document.addEventListener('keydown', (e) => {
            let newX = x;
            let newY = y;

            switch(e.key) {
                case 'ArrowUp':
                    newY = y - step;
                    break;
                case 'ArrowDown':
                    newY = y + step;
                    break;
                case 'ArrowLeft':
                    newX = x - step;
                    break;
                case 'ArrowRight':
                    newX = x + step;
                    break;
            }

            if (canMoveTo(newX, newY)) {
                x = newX;
                y = newY;
                character.style.top = `${y}px`;
                character.style.left = `${x}px`;
            } else {
                collisionSound.play();
            }
        });

        function canMoveTo(newX, newY) {
            return (newX >= 0 && newX <= 560 && newY >= 0 && newY <= 560);
        }

        // Inicializa a posição do personagem
        character.style.top = `${y}px`;
        character.style.left = `${x}px`;
    </script>
</body>
</html>
