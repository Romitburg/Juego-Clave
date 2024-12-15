<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Adivina el Número Secreto</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }
        .container {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            box-shadow: 0 15px 25px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
            width: 350px;
        }
        h1 {
            margin-bottom: 20px;
            font-size: 2.5em;
            color: white;
        }
        .input-container {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }
        input {
            width: 50px;
            height: 60px;
            margin: 0 10px;
            text-align: center;
            font-size: 30px;
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 10px;
            background: rgba(255,255,255,0.1);
            color: white;
            outline: none;
            transition: all 0.3s ease;
        }
        input:focus {
            border-color: rgba(255,255,255,0.5);
            box-shadow: 0 0 10px rgba(255,255,255,0.2);
        }
        button {
            background: #4CAF50;
            border: none;
            color: white;
            padding: 15px 30px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 18px;
            margin: 10px 0;
            cursor: pointer;
            border-radius: 10px;
            transition: background 0.3s ease;
        }
        button:hover {
            background: #45a049;
        }
        button:disabled {
            background: #cccccc;
            cursor: not-allowed;
        }
        #resultado {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
            min-height: 30px;
        }
        #intentos {
            font-size: 16px;
            color: rgba(255,255,255,0.7);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Adivina el Número</h1>
        <p>Ingresa 4 dígitos (0-9)</p>
        
        <div class="input-container">
            <input type="number" min="0" max="9" id="digit1" maxlength="1">
            <input type="number" min="0" max="9" id="digit2" maxlength="1">
            <input type="number" min="0" max="9" id="digit3" maxlength="1">
            <input type="number" min="0" max="9" id="digit4" maxlength="1">
        </div>
        
        <button onclick="verificarNumero()">Verificar</button>
        
        <div id="resultado"></div>
        <div id="intentos"></div>
    </div>

    <script>
        // Número secreto establecido como 6391
        const numeroSecreto = [6, 3, 9, 1];
        let intentosRestantes = 3;

        function verificarNumero() {
            const digit1 = parseInt(document.getElementById('digit1').value);
            const digit2 = parseInt(document.getElementById('digit2').value);
            const digit3 = parseInt(document.getElementById('digit3').value);
            const digit4 = parseInt(document.getElementById('digit4').value);

            const intento = [digit1, digit2, digit3, digit4];

            const resultadoDiv = document.getElementById('resultado');
            const intentosDiv = document.getElementById('intentos');

            // Validar que todos los campos estén llenos
            if (isNaN(digit1) || isNaN(digit2) || isNaN(digit3) || isNaN(digit4)) {
                resultadoDiv.innerHTML = 'Por favor, llena todos los campos';
                resultadoDiv.style.color = 'yellow';
                return;
            }

            intentosRestantes--;

            // Comparar el intento con el número secreto
            if (intento.every((valor, index) => valor === numeroSecreto[index])) {
                resultadoDiv.innerHTML = '¡Correcto! Has adivinado el número.';
                resultadoDiv.style.color = '#4CAF50';
                document.querySelector('button').disabled = true;
            } else {
                resultadoDiv.innerHTML = 'Intento incorrecto';
                resultadoDiv.style.color = '#FF6B6B';
            }

            intentosDiv.innerHTML = `Intentos restantes: ${intentosRestantes}`;
            intentosDiv.style.color = 'white';

            if (intentosRestantes === 0 && resultadoDiv.innerHTML === 'Intento incorrecto') {
                resultadoDiv.innerHTML = 'Juego terminado. El número secreto era: ' + numeroSecreto.join('');
                resultadoDiv.style.color = 'white';
                document.querySelector('button').disabled = true;
            }
        }
    </script>
</body>
</html>
