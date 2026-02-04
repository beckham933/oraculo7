<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Oráculo do Tarô</title>
<link href="https://fonts.googleapis.com/css2?family=Cinzel&family=Montserrat&display=swap" rel="stylesheet">

<style>
body {
    margin: 0;
    font-family: 'Montserrat', sans-serif;
    background: radial-gradient(circle at top, #2b1055, #000);
    color: #fff;
}

header {
    text-align: center;
    padding: 40px 20px;
}

header h1 {
    font-family: 'Cinzel', serif;
    font-size: 3em;
    color: #f5d76e;
}

nav {
    display: flex;
    justify-content: center;
    gap: 25px;
    margin-top: 20px;
    flex-wrap: wrap;
}

nav a {
    color: #fff;
    text-decoration: none;
    font-weight: bold;
}

section {
    padding: 60px 20px;
    max-width: 1000px;
    margin: auto;
}

.card {
    background: rgba(255,255,255,0.08);
    border-radius: 15px;
    padding: 30px;
    box-shadow: 0 0 20px rgba(245,215,110,0.3);
}

button {
    background: #f5d76e;
    border: none;
    padding: 15px 30px;
    border-radius: 30px;
    font-size: 1em;
    cursor: pointer;
    margin-top: 20px;
}

button:disabled {
    background: #777;
    cursor: not-allowed;
}

button:hover:not(:disabled) {
    background: #ffec99;
}

img {
    max-width: 100%;
    height: auto;
}

.cartas {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 30px;
    margin-top: 30px;
    text-align: center;
}

.cartas img {
    border-radius: 12px;
    box-shadow: 0 0 15px rgba(245,215,110,0.4);
}

.whatsapp {
    background: #25D366;
    color: #000;
    text-decoration: none;
    display: inline-block;
    padding: 15px 30px;
    border-radius: 30px;
    margin-top: 20px;
    font-weight: bold;
}

footer {
    text-align: center;
    padding: 30px;
    opacity: 0.7;
}
</style>
</head>

<body>

<header>
    <h1>🔮 Oráculo do Tarô</h1>
    <nav>
        <a href="#valores">Valores</a>
        <a href="#pix">Pix</a>
        <a href="#tiragem">Tiragem</a>
        <a href="#contato">Contato</a>
    </nav>
</header>

<section id="valores">
    <div class="card">
        <h2>Tabela de Valores</h2>
        <p>Consultas acessíveis e objetivas</p>
        <ul>
            <li>1 pergunta – <strong>R$ 5,00</strong></li>
            <li>3 perguntas – <strong>R$ 12,00</strong></li>
            <li>5 perguntas – <strong>R$ 20,00</strong></li>
            <li>Tiragem completa – <strong>R$ 30,00</strong></li>
        </ul>
    </div>
</section>

<section id="pix">
    <div class="card">
        <h2>Pagamento via Pix</h2>
        <p><strong>Chave Pix:</strong></p>
        <p><em>SEU_PIX_AQUI</em></p>
        <p>
            Após o pagamento, marque a confirmação abaixo
            para liberar a leitura.
        </p>
    </div>
</section>

<section id="tiragem">
    <div class="card">
        <h2>Tiragem de 3 Cartas</h2>
        <p>Passado • Presente • Futuro</p>

        <label>
            <input type="checkbox" id="pagamentoConfirmado">
            Já realizei o pagamento via Pix
        </label>

        <br><br>

        <button id="btnTiragem" disabled>
            Revelar Cartas
        </button>

        <div id="resultado" class="cartas"></div>
    </div>
</section>

<section id="contato">
    <div class="card">
        <h2>Consulta pelo WhatsApp</h2>
        <p>Envie o comprovante junto com sua pergunta.</p>

        <a class="whatsapp" target="_blank"
           href="https://wa.me/5599999999999?text=Olá!%20Já%20paguei%20a%20consulta%20de%20tarô%20via%20Pix.%20Segue%20o%20comprovante.">
           📲 Falar no WhatsApp
        </a>
    </div>
</section>

<footer>
    ✨ Que as cartas revelem o que você está pronto para enxergar ✨
</footer>

<script>
const cartas = [
    { nome: "O Louco", significado: "Novos começos e liberdade.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar00.jpg" },
    { nome: "O Mago", significado: "Ação e poder pessoal.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar01.jpg" },
    { nome: "A Sacerdotisa", significado: "Intuição e mistério.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar02.jpg" },
    { nome: "A Imperatriz", significado: "Abundância e criação.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar03.jpg" },
    { nome: "O Imperador", significado: "Estrutura e liderança.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar04.jpg" },
    { nome: "A Morte", significado: "Transformação profunda.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar13.jpg" },
    { nome: "A Estrela", significado: "Esperança e cura.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar17.jpg" },
    { nome: "O Sol", significado: "Alegria e clareza.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar19.jpg" },
    { nome: "O Mundo", significado: "Conclusão e realização.", img: "https://www.sacred-texts.com/tarot/pkt/img/ar21.jpg" }
];

const checkbox = document.getElementById("pagamentoConfirmado");
const botao = document.getElementById("btnTiragem");
const resultado = document.getElementById("resultado");

checkbox.addEventListener("change", () => {
    botao.disabled = !checkbox.checked;
});

// Tiragem de 3 cartas com efeito de revelar uma a uma
botao.addEventListener("click", () => {
    resultado.innerHTML = "<p>🔮 Embaralhando as cartas...</p>";
    botao.disabled = true; // desabilita para evitar múltiplos clicks

    setTimeout(() => {
        resultado.innerHTML = "";
        const sorteadas = [...cartas].sort(() => 0.5 - Math.random()).slice(0, 3);
        const posicoes = ["Passado", "Presente", "Futuro"];

        sorteadas.forEach((carta, i) => {
            setTimeout(() => {
                resultado.innerHTML += `
                    <div>
                        <h3>${posicoes[i]}</h3>
                        <img src="${carta.img}" alt="${carta.nome}">
                        <h4>${carta.nome}</h4>
                        <p>${carta.significado}</p>
                    </div>
                `;
                if (i === sorteadas.length - 1) {
                    botao.disabled = false; // reabilita o botão após revelar todas
                }
            }, i * 1500); // delay de 1,5s entre cada carta
        });
    }, 2000);
});
</script>

</body>
</html>
