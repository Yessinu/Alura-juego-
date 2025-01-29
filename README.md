# Alura-juego-
primer juego 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego del Amigo Secreto</title>
    <style>
        :root {
            --color-primary: #FF7F50;
            --color-secondary: #F0E68C;
            --color-tertiary: #FFD700;
            --color-button: #008CBA;
            --color-button-hover: #005F6A;
            --color-text: #333333;
            --color-white: #FFFFFF;
        }

        /* Estilos generales */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            height: 100vh;
            background-color: var(--color-primary);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .main-content {
            display: flex;
            flex-direction: column;
            height: 100%;
            width: 100%;
            padding: 20px;
        }

        /* Banner */
        .header-banner {
            flex: 40%;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px 0 0;
        }

        /* Sección de entrada */
        .input-section {
            flex: 60%;
            background-color: var(--color-secondary);
            border: 1px solid #000;
            border-radius: 64px 64px 0 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            width: 100%;
        }

        /* Títulos */
        .main-title {
            font-size: 48px;
            font-family: "Merriweather", serif;
            font-weight: 900;
            font-style: italic;
            color: var(--color-white);
        }

        /* Contenedores de entrada y botón */
        .input-wrapper {
            display: flex;
            justify-content: center;
            width: 100%;
            max-width: 600px;
            margin-top: 20px;
        }

        .button-container {
            width: 300px;
            justify-content: center;
        }

        /* Estilos de botón */
        button {
            padding: 15px 30px;
            font-family: "Inter", sans-serif;
            font-size: 16px;
            border: 2px solid #000;
            border-radius: 25px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
            cursor: pointer;
        }

        .button-draw {
            display: flex;
            align-items: center;
            width: 100%;
            padding: 10px 40px;
            color: var(--color-white);
            background-color: var(--color-button);
            font-size: 16px;
        }

        .button-draw:hover {
            background-color: var(--color-button-hover);
        }

        /* Listas */
        ul {
            list-style-type: none;
            color: var(--color-text);
            font-family: "Inter", sans-serif;
            font-size: 18px;
            margin: 20px 0;
        }

        .result-list {
            margin-top: 15px;
            color: #32CD32;
            font-size: 22px;
            font-weight: bold;
            text-align: center;
        }

    </style>
</head>
<body>
    <div class="main-content">
        <div class="header-banner">
            <h1 class="main-title">Juego del Amigo Secreto</h1>
        </div>
        <div class="input-section">
            <p>Participantes:</p>
            <ul id="listaParticipantes"></ul>
            <button onclick="asignarAmigosSecretos()" id="asignar" class="button-draw">Asignar Amigos Secretos</button>
            <button onclick="reiniciarJuego()" id="reiniciar" class="button-draw">Reiniciar Juego</button>
            <p id="resultado" class="result-list"></p>
        </div>
    </div>

    <script>
        let participantes = ["María", "Luis", "Alba", "Carlos", "Javier"];
        let amigosSecretos = [];

        function inicializarLista() {
            let listaHTML = "";
            participantes.forEach(nombre => {
                listaHTML += `<li>${nombre}</li>`;
            });
            document.getElementById('listaParticipantes').innerHTML = listaHTML;
        }

        function asignarAmigosSecretos() {
            amigosSecretos = [...participantes];
            let asignacionValida = false;

            while (!asignacionValida) {
                shuffleArray(amigosSecretos);
                asignacionValida = true;
                for (let i = 0; i < participantes.length; i++) {
                    if (participantes[i] === amigosSecretos[i]) {
                        asignacionValida = false;
                        break;
                    }
                }
            }

            mostrarResultados();
            document.getElementById('reiniciar').removeAttribute('disabled');
        }

        function mostrarResultados() {
            let resultado = "";
            for (let i = 0; i < participantes.length; i++) {
                resultado += `${participantes[i]} tiene como amigo secreto a: ${amigosSecretos[i]}<br>`;
            }
            document.getElementById('resultado').innerHTML = resultado;
        }

        function reiniciarJuego() {
            amigosSecretos = [];
            document.getElementById('resultado').innerHTML = '';
        }

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        // Inicializar la lista al cargar la página
        inicializarLista();
    </script>
</body>
</html>
