<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>💖 Tengo algo que decirte 💖</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: #ffe6e6;
            color: #d63384;
            width: 100vw;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            font-family: Arial, sans-serif;
        }
        .section1 h1 {
            text-align: center;
        }
        .section1 .span-1 { font-size: 4rem; color: #ff4081; }
        .section1 .span-2 { font-size: 2rem; }
        .section1 .span-3 { font-size: 3rem; }
        .section1 .span-4 { font-size: 2.5rem; }
        .section1 button {
            width: 90px;
            height: 40px;
            border: none;
            border-radius: 20px;
            color: white;
            background: #d63384;
            margin-top: 20px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .section1 button:hover { background: #ff4081; }
        .letras span { font-size: 3rem; color: #ff4081; }
        .meme-final {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            font-size: 2.5rem;
            color: #d63384;
        }
        .meme-final img { width: 150px; margin-top: 10px; }
        .desactivado { display: none; }
        .oculto { visibility: hidden; }
        
        /* Estilos de la carta */
        .carta {
            margin-top: 20px;
            cursor: pointer;
            transition: transform 0.3s ease;
        }
        .carta:hover {
            transform: scale(1.1);
        }
    </style>
</head>
<body>

    <div class="section1" id="s1">
        <h1>
            <span class="span-1">Hey 💖</span><br />
            <span class="span-2">tengo que</span><br />
            <span class="span-3">decirte</span><br />
            <span class="span-4">algo...</span><br />
            <button id="btn">ver 💌</button>
        </h1>
    </div>

    <div class="section2 desactivado" id="s2">
        <!-- Audio con controles ocultos -->
        <audio id="myAudio" src="./amor.mp3" preload="auto"></audio>
        <p class="letras" id="pLetras"></p>
    </div>

    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const $ = (e) => document.getElementById(e);
            const section1 = $("s1");
            const btn = $("btn");
            const audio = $("myAudio");
            const section2 = $("s2");
            const pLetras = $("pLetras");

            const letrasConfig = [
                { palabras: ["El", "amor"], tiempo: 0 },
                { palabras: ["está", "en"], tiempo: 1500 },
                { palabras: ["el", "aire"], tiempo: 3000 },
                { palabras: ["Hoy", "es"], tiempo: 4500 },
                { palabras: ["nuestro", "día"], tiempo: 6000, esUltimo: true, cita: "El amor y la amistad son los regalos más hermosos que podemos compartir, porque son los que nos hacen sentir verdaderamente vivos." },  // Aquí añadí la cita
            ];

            btn.addEventListener("click", () => {
                section1.classList.add("desactivado");
                section2.classList.remove("desactivado");

                // Reproducir audio cuando el usuario haga clic
                audio.volume = 1.0;
                audio.play().catch((error) => {
                    console.error("Error al reproducir el audio:", error);
                });

                mostrarLetras(letrasConfig);
            });

            function mostrarLetras(config) {
                config.forEach((letraObj) => {
                    setTimeout(() => {
                        pLetras.innerHTML = "";

                        const span1 = document.createElement("span");
                        span1.textContent = letraObj.palabras[0];
                        pLetras.appendChild(span1);

                        const saltoDeLinea = document.createElement("br");
                        pLetras.appendChild(saltoDeLinea);

                        if (letraObj.esUltimo) {
                            setTimeout(() => {
                                pLetras.innerHTML = "";
                                const gif = document.createElement("img");
                                const span = document.createElement("span");

                                span.innerHTML = "💖 ¡FELIZ DÍA DEL CARIÑO! 💖";
                                gif.src = "./corazon.gif"; // Reemplázalo con un gif de corazón

                                pLetras.appendChild(span);
                                pLetras.appendChild(document.createElement("br"));
                                pLetras.appendChild(gif);
                                pLetras.classList.add("meme-final");

                                // Agregar la cita
                                const cita = document.createElement("p");
                                cita.style.fontSize = "1.5rem";
                                cita.style.color = "#ff4081";
                                cita.innerText = letraObj.cita;  // Aquí se añade la cita
                                pLetras.appendChild(cita);

                                // Agregar la carta descargable
                                const carta = document.createElement("a");
                                const imgCarta = document.createElement("img");

                                carta.href = "./carta.pdf"; // Ruta del archivo PDF
                                carta.download = "carta.pdf";
                                carta.classList.add("carta");

                                imgCarta.src = "./carta.gif"; // Imagen de la carta
                                imgCarta.alt = "Descargar carta";
                                imgCarta.width = 150; // Ajustar el tamaño de la carta

                                carta.appendChild(imgCarta);
                                pLetras.appendChild(document.createElement("br"));
                                pLetras.appendChild(carta);
                            }, 2500);
                        } else {
                            const span2 = document.createElement("span");
                            span2.textContent = letraObj.palabras[1];
                            span2.classList.add("oculto");
                            pLetras.appendChild(span2);

                            setTimeout(() => {
                                span2.classList.remove("oculto");
                            }, 520);
                        }
                    }, letraObj.tiempo);
                });
            }
        });
    </script>

</body>
</html>
