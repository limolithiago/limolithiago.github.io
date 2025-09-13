<Ranking Poker Home Ras>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Ranking Piscine</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 40px;
    }

    .ranking, .formulario {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 750px;
      margin-bottom: 30px;
      position: relative;
    }

    .ranking h2, .formulario h3 {
      text-align: center;
      margin-bottom: 10px;
      color: #333;
    }

    .legenda {
      width: 750px;
      display: flex;
      justify-content: center;
      margin-bottom: 10px;
      gap: 20px;
      font-size: 14px;
    }

    .legenda div {
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .legenda span {
      display: inline-block;
      width: 20px;
      height: 20px;
      border-radius: 3px;
    }

    .azul { background: #cce5ff; }
    .vermelho { background: #ffcccc; }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      padding: 12px;
      text-align: center;
      border-bottom: 1px solid #ddd;
      position: relative;
    }

    th { background-color: #333; color: white; }
    tr.pos1_8 td { background: #cce5ff; } /* azul claro */
    tr.pos9_17 td { background: #ffcccc; } /* vermelho claro */
    tr.empty td { color: #aaa; }

    tr { transition: all 0.5s ease; }
    tr:hover { background-color: #f1f1f1; }

    .fade-in { animation: fadeIn 0.6s ease; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }

    .formulario input {
      width: calc(100% - 20px); padding: 10px; margin-bottom: 10px;
      border: 1px solid #ccc; border-radius: 5px; font-size: 14px;
    }

    .formulario button, .btn-pontos {
      padding: 6px 12px; color: white; border: none; border-radius: 5px;
      font-size: 14px; cursor: pointer; margin: 2px;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .btn-presenca { background: #4CAF50; }   
    .btn-segundo { background: #2196F3; }   
    .btn-terceiro { background: #9C27B0; }  
    .btn-quarto { background: #FF9800; }   
    .btn-quinto { background: #795548; }   
    .btn-campeao { background: #FF5722; }  

    .btn-presenca:hover { background: #45a049; }
    .btn-segundo:hover { background: #1976D2; }
    .btn-terceiro:hover { background: #7B1FA2; }
    .btn-quarto:hover { background: #FB8C00; }
    .btn-quinto:hover { background: #5D4037; }
    .btn-campeao:hover { background: #E64A19; }

    .btn-pontos:active { transform: scale(1.2); box-shadow: 0 0 10px rgba(0,0,0,0.2); }
    .formulario button:hover { background: #555; }

    .animacao-pontos {
      position: absolute; font-weight: bold; color: #ff0000;
      animation: subirFade 1s forwards; pointer-events: none;
    }
    @keyframes subirFade { 0% { opacity: 1; transform: translateY(0); } 100% { opacity: 0; transform: translateY(-30px); } }
  </style>
</head>
<body>
  <!-- Legenda das cores -->
  <div class="legenda">
    <div><span class="azul"></span> Classificados para a mesa final semestral</div>
    <div><span class="vermelho"></span> Repescagem final</div>
  </div>

  <div class="ranking">
    <h2>🏆 Ranking Poker Piscine</h2>
    <table id="rankingTable">
      <tr>
        <th>Posição</th>
        <th>Nome</th>
        <th>Pontos</th>
        <th>Presenças</th>
        <th>Vitórias</th>
        <th>Adicionar Pontos</th>
      </tr>
    </table>
  </div>

  <div class="formulario">
    <h3>➕ Adicionar Jogador</h3>
    <input type="text" id="nome" placeholder="Nome do jogador" required>
    <input type="number" id="pontos" placeholder="Pontos" required>
    <button onclick="adicionarJogador()">Adicionar</button>
  </div>

  <div class="formulario">
    <h3>❌ Remover Jogador</h3>
    <input type="text" id="removerNome" placeholder="Nome do jogador" required>
    <button onclick="removerJogador()">Remover</button>
  </div>

  <script>
    // Jogadores fictícios preenchendo 27 posições
    let jogadores = [
      { nome: "Roque", pontos: 1500, presencas: 0, vitorias: 0 },
      { nome: "Guido", pontos: 1450, presencas: 0, vitorias: 0 },
      { nome: "Matheus", pontos: 1400, presencas: 0, vitorias: 0 },
      { nome: "Brian", pontos: 1350, presencas: 0, vitorias: 0 },
      { nome: "Limoli", pontos: 1300, presencas: 0, vitorias: 0 },
      { nome: "Ana", pontos: 1250, presencas: 0, vitorias: 0 },
      { nome: "Lucas", pontos: 1200, presencas: 0, vitorias: 0 },
      { nome: "Carla", pontos: 1150, presencas: 0, vitorias: 0 },
      { nome: "Pedro", pontos: 1100, presencas: 0, vitorias: 0 },
      { nome: "Mariana", pontos: 1050, presencas: 0, vitorias: 0 },
      { nome: "Felipe", pontos: 1000, presencas: 0, vitorias: 0 },
      { nome: "Julia", pontos: 950, presencas: 0, vitorias: 0 },
      { nome: "Tiago", pontos: 900, presencas: 0, vitorias: 0 },
      { nome: "Fernanda", pontos: 850, presencas: 0, vitorias: 0 },
      { nome: "Rafael", pontos: 800, presencas: 0, vitorias: 0 },
      { nome: "Beatriz", pontos: 750, presencas: 0, vitorias: 0 },
      { nome: "Rodrigo", pontos: 700, presencas: 0, vitorias: 0 },
      { nome: "Patricia", pontos: 650, presencas: 0, vitorias: 0 },
      { nome: "Bruno", pontos: 600, presencas: 0, vitorias: 0 },
      { nome: "Carolina", pontos: 550, presencas: 0, vitorias: 0 },
      { nome: "Diego", pontos: 500, presencas: 0, vitorias: 0 },
      { nome: "Sandra", pontos: 450, presencas: 0, vitorias: 0 },
      { nome: "Vitor", pontos: 400, presencas: 0, vitorias: 0 },
      { nome: "Paula", pontos: 350, presencas: 0, vitorias: 0 },
      { nome: "Igor", pontos: 300, presencas: 0, vitorias: 0 },
      { nome: "Camila", pontos: 250, presencas: 0, vitorias: 0 },
      { nome: "André", pontos: 200, presencas: 0, vitorias: 0 }
    ];

    function atualizarTabela() {
      const tabela = document.getElementById("rankingTable");
      tabela.innerHTML = `
        <tr>
          <th>Posição</th>
          <th>Nome</th>
          <th>Pontos</th>
          <th>Presenças</th>
          <th>Vitórias</th>
          <th>Adicionar Pontos</th>
        </tr>
      `;

      jogadores.sort((a, b) => b.pontos - a.pontos);

      for (let i = 0; i < 27; i++) {
        const linha = tabela.insertRow();
        linha.classList.add("fade-in");

        if (i < jogadores.length) {
          const jogador = jogadores[i];
          linha.insertCell().textContent = i + 1;
          linha.insertCell().textContent = jogador.nome;
          linha.insertCell().textContent = jogador.pontos;
          linha.insertCell().textContent = jogador.presencas;
          linha.insertCell().textContent = jogador.vitorias;

          const celulaBotoes = linha.insertCell();
          [
            { valor: 10, nome: 'Presença', classe: 'btn-presenca', adicionaPresenca: true, adicionaVitoria: false },
            { valor: 50, nome: 'Segundo', classe: 'btn-segundo', adicionaPresenca: false, adicionaVitoria: false },
            { valor: 75, nome: 'Terceiro', classe: 'btn-terceiro', adicionaPresenca: false, adicionaVitoria: false },
            { valor: 60, nome: 'Quarto', classe: 'btn-quarto', adicionaPresenca: false, adicionaVitoria: false },
            { valor: 40, nome: 'Quinto', classe: 'btn-quinto', adicionaPresenca: false, adicionaVitoria: false },
            { valor: 100, nome: 'Campeão', classe: 'btn-campeao', adicionaPresenca: false, adicionaVitoria: true }
          ].forEach(item => {
            const btn = document.createElement("button");
            btn.textContent = item.nome;
            btn.className = `btn-pontos ${item.classe}`;
            btn.onclick = () => {
              jogador.pontos += item.valor;
              if(item.adicionaPresenca) jogador.presencas += 1;
              if(item.adicionaVitoria) jogador.vitorias += 1;
              mostrarAnimacao(linha, item.valor);
              atualizarTabela();
            };
            celulaBotoes.appendChild(btn);
          });

          if(i < 8) linha.classList.add("pos1_8");
          else if(i < 17) linha.classList.add("pos9_17");

        } else {
          linha.classList.add("empty");
          linha.insertCell().textContent = i + 1;
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
        }
      }
    }

    function mostrarAnimacao(linha, valor) {
      const anim = document.createElement("div");
      anim.className = "animacao-pontos";
      anim.textContent = `+${valor}`;
      linha.cells[2].appendChild(anim);
      setTimeout(() => anim.remove(), 1000);
    }

    function adicionarJogador() {
      const nome = document.getElementById("nome").value.trim();
      const pontos = parseInt(document.getElementById("pontos").value);
      if (nome && !isNaN(pontos)) {
        jogadores.push({ nome, pontos, presencas: 0, vitorias: 0 });
        atualizarTabela();
        document.getElementById("nome").value = "";
        document.getElementById("pontos").value = "";
      }
    }

    function removerJogador() {
      const nomeRemover = document.getElementById("removerNome").value.trim();
      if (nomeRemover) {
        jogadores = jogadores.filter(j => j.nome.toLowerCase() !== nomeRemover.toLowerCase());
        atualizarTabela();
        document.getElementById("removerNome").value = "";
      }
    }

    atualizarTabela();
  </script>
</body>
</html>
