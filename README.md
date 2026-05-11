<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Projeto Interativo</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Meu Projeto Interativo</h1>
  </header>

  <nav class="botoes">
    <button class="btn ativo" data-aba="aba1">Aba 1</button>
    <button class="btn" data-aba="aba2">Aba 2</button>
    <button class="btn" data-aba="aba3">Aba 3</button>
  </nav>

  <main>
    <section id="aba1" class="conteudo ativo">
      <h2>Conteúdo da Aba 1</h2>
      <div class="contador" data-data="2026-06-01T00:00:00"></div>
    </section>

    <section id="aba2" class="conteudo">
      <h2>Conteúdo da Aba 2</h2>
      <div class="contador" data-data="2026-07-01T00:00:00"></div>
    </section>

    <section id="aba3" class="conteudo">
      <h2>Conteúdo da Aba 3</h2>
      <div class="contador" data-data="2026-08-01T00:00:00"></div>
    </section>
  </main>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

header {
  background: #4CAF50;
  color: white;
  width: 100%;
  text-align: center;
  padding: 1rem;
}

.botoes {
  display: flex;
  gap: 10px;
  margin: 1rem 0;
  flex-wrap: wrap;
  justify-content: center;
}

.btn {
  padding: 10px 20px;
  border: 2px solid #ccc;
  border-radius: 0;
  cursor: pointer;
  background: white;
  transition: 0.3s;
}

.btn:hover {
  border-color: #4CAF50;
}

.btn.ativo {
  border: 2px solid #4CAF50;
  color: #4CAF50;
  font-weight: bold;
}

.conteudo {
  display: none;
  text-align: center;
  padding: 1rem;
}

.conteudo.ativo {
  display: block;
}

.contador {
  font-size: 2rem;
  margin-top: 1rem;
}

/* Responsividade */
@media (min-width: 600px) {
  .botoes {
    flex-direction: row;
  }

  .btn:first-child {
    border-radius: 8px 0 0 8px;
  }

  .btn:last-child {
    border-radius: 0 8px 8px 0;
  }
}
// Seleciona botões e abas
const botoes = document.querySelectorAll('.btn');
const abas = document.querySelectorAll('.conteudo');

// Função para alternar abas
botoes.forEach(botao => {
  botao.addEventListener('click', () => {
    // Remove ativo dos botões
    botoes.forEach(b => b.classList.remove('ativo'));
    botao.classList.add('ativo');

    // Mostra a aba correspondente
    const abaSelecionada = botao.dataset.aba;
    abas.forEach(aba => {
      aba.classList.remove('ativo');
      if (aba.id === abaSelecionada) {
        aba.classList.add('ativo');
      }
    });
  });
});

// Função para contagem regressiva
function atualizarContadores() {
  const contadores = document.querySelectorAll('.contador');

  contadores.forEach(contador => {
    const dataFinal = new Date(contador.dataset.data);
    const agora = new Date();
    const diff = dataFinal - agora;

    if (diff <= 0) {
      contador.textContent = "Tempo esgotado!";
      return;
    }

    const dias = Math.floor(diff / (1000 * 60 * 60 * 24));
    const horas = Math.floor((diff / (1000 * 60 * 60)) % 24);
    const minutos = Math.floor((diff / (1000 * 60)) % 60);
    const segundos = Math.floor((diff / 1000) % 60);

    contador.textContent = `${dias}d ${horas}h ${minutos}m ${segundos}s`;
  });
}

// Atualiza a cada segundo
setInterval(atualizarContadores, 1000);
atualizarContadores();
