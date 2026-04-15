<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BL-Simi 🌈</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #fce4ec; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        #chat-container { width: 400px; height: 500px; background: white; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); display: flex; flex-direction: column; overflow: hidden; }
        #chat-header { background: #f06292; color: white; padding: 15px; text-align: center; font-weight: bold; font-size: 1.2em; }
        #chat-box { flex: 1; padding: 15px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; }
        .message { max-width: 80%; padding: 10px; border-radius: 10px; font-size: 0.9em; line-height: 1.4; }
        .bot { background: #f8bbd0; align-self: flex-start; color: #880e4f; }
        .user { background: #e1f5fe; align-self: flex-end; color: #01579b; }
        #input-area { display: flex; border-top: 1px solid #eee; padding: 10px; }
        input { flex: 1; border: 1px solid #ddd; border-radius: 20px; padding: 10px 15px; outline: none; }
        button { background: #f06292; border: none; color: white; padding: 10px 15px; margin-left: 5px; border-radius: 50%; cursor: pointer; }
    </style>
</head>
<body>

<div id="chat-container">
    <div id="chat-header">BL-Simi 🌸</div>
    <div id="chat-box" id="chatBox">
        <div class="message bot">¡Hola fujoshi/fudanshi! ✨ Soy BL-Simi. Pregúntame por recomendaciones o cuéntame una trama y trataré de adivinar el nombre.</div>
    </div>
    <div id="input-area">
        <input type="text" id="userInput" placeholder="Escribe algo..." onkeypress="handleKeyPress(event)">
        <button onclick="sendMessage()">➔</button>
    </div>
</div>

<script>
    const knowledgeBase = [
        { keywords: ["hola", "buen", "saludos"], response: "¡Hola! ¿Buscas algo tierno o algo con mucho drama hoy? 🔥" },
        { keywords: ["recomienda", "recomendacion", "leer"], response: "Te recomiendo: 'The Night Beyond the Tricornered Window' (misterio) o 'Given' (si quieres llorar con música). 🎸" },
        { keywords: ["omegaverse", "feromonas", "alfa"], response: "¡Ah, el clásico! Si buscas uno icónico, lee 'Love is an Illusion' o 'Megumi y Tsugumi'. 🐺" },
        { keywords: ["mafia", "boxeo", "joo jaekyung"], response: "Ese suena a 'Jinx'. ¡Ten cuidado con el corazón (y la cartera) de Dan! 🥊" },
        { keywords: ["universidad", "error", "semantica"], response: "¡Definitivamente estás hablando de 'Semantic Error'! Un clásico enemies-to-lovers. 💻" },
        { keywords: ["pintor", "corea", "antiguo"], response: "Ese es 'Pintor Nocturno' (Painter of the Night). ¡Pobre Nakyum! 🎨" },
        { keywords: ["gracias", "ty"], response: "¡De nada! Disfruta tu lectura. 📚✨" }
    ];

    function sendMessage() {
        const input = document.getElementById("userInput");
        const chatBox = document.getElementById("chat-box");
        if (input.value.trim() === "") return;

        // Mensaje del usuario
        chatBox.innerHTML += `<div class="message user">${input.value}</div>`;
        
        const reply = getBotResponse(input.value.toLowerCase());
        
        // Respuesta del bot
        setTimeout(() => {
            chatBox.innerHTML += `<div class="message bot">${reply}</div>`;
            chatBox.scrollTop = chatBox.scrollHeight;
        }, 500);

        input.value = "";
    }

    function getBotResponse(text) {
        for (let item of knowledgeBase) {
            if (item.keywords.some(key => text.includes(key))) {
                return item.response;
            }
        }
        return "Mmm, no estoy seguro de cuál es, pero suena interesante. ¿Tienes más detalles sobre el color de pelo o la profesión? 🤔";
    }

    function handleKeyPress(e) {
        if (e.key === 'Enter') sendMessage();
    }
</script>

</body>
</html>
