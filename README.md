<style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');

    body {
        background-color: #050a14; /* Fundo liso escuro */
        color: #00d4ff;
        font-family: 'Orbitron', sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    .box {
        width: 320px; /* Formulário pequeno e compacto */
        padding: 20px;
        border: 2px solid #00d4ff;
        background: rgba(0, 20, 40, 0.9);
        box-shadow: 0 0 15px #00d4ff;
        border-radius: 8px;
    }

    h2 {
        font-size: 18px;
        text-align: center;
        margin-top: 0;
        text-transform: uppercase;
        letter-spacing: 2px;
    }

    .campo {
        margin-bottom: 12px;
    }

    label {
        font-size: 9px;
        display: block;
        margin-bottom: 4px;
    }

    input, textarea {
        width: 100%;
        background: #000;
        border: 1px solid #00d4ff;
        color: #fff;
        padding: 8px;
        font-size: 11px;
        box-sizing: border-box;
        outline: none;
    }

    textarea {
        height: 80px;
        resize: none;
    }

    .foto-area {
        border: 1px dashed #00d4ff;
        height: 100px;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
        font-size: 10px;
        position: relative;
    }

    #img-preview {
        width: 100%;
        height: 100%;
        object-fit: cover;
        display: none;
        position: absolute;
    }

    button {
        width: 100%;
        padding: 10px;
        margin-top: 15px;
        background: transparent;
        border: 1px solid #00d4ff;
        color: #00d4ff;
        font-family: 'Orbitron', sans-serif;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
    }

    button:hover {
        background: #00d4ff;
        color: #000;
    }
</style>

<div class="box">
    <h2>Criar Personagem</h2>
    
    <div class="campo">
        <label>NOME</label>
        <input type="text" id="nome">
    </div>

    <div style="display: flex; gap: 5px;">
        <div class="campo">
            <label>IDADE</label>
            <input type="number" id="idade">
        </div>
        <div class="campo">
            <label>GÊNERO</label>
            <input type="text" id="genero">
        </div>
    </div>

    <div class="campo">
        <label>HISTÓRIA</label>
        <textarea id="historia"></textarea>
    </div>

    <label>FOTO DO PERSONAGEM</label>
    <div class="foto-area" onclick="document.getElementById('file').click()">
        <span id="txt">GALERIA</span>
        <img id="img-preview">
        <input type="file" id="file" hidden accept="image/*" onchange="loadImg(event)">
    </div>

    <button onclick="enviar()">ENVIAR AO DISCORD</button>
</div>

<script>
    function loadImg(e) {
        const reader = new FileReader();
        reader.onload = function() {
            const img = document.getElementById('img-preview');
            img.src = reader.result;
            img.style.display = 'block';
            document.getElementById('txt').style.display = 'none';
        }
        reader.readAsDataURL(e.target.files[0]);
    }

    async function enviar() {
        const webhook = "https://discord.com/api/webhooks/1463212379700461803/Mg62USUEcsuJPk-ZCtL1N2EsL5ZnCFaRFntvY8hF0tRfCZ-AegOfSwWiwMm7yyiM6o6J";
        const dados = {
            embeds: [{
                title: "NOVO PERSONAGEM",
                color: 5814783,
                fields: [
                    { name: "Nome", value: document.getElementById('nome').value, inline: true },
                    { name: "Idade", value: document.getElementById('idade').value, inline: true },
                    { name: "Gênero", value: document.getElementById('genero').value, inline: true },
                    { name: "História", value: document.getElementById('historia').value }
                ]
            }]
        };

        await fetch(webhook, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify(dados)
        });
        alert("Enviado!");
    }
</script>
