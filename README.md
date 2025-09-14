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

    .topo {
      width: 750px;
      display: flex;
      justify-content: space-between;
      margin-bottom: 15px;
    }

    .btn-salvar {
      background: #28a745;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    .btn-salvar:hover {
      background: #218838;
    }

    .ranking {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 750px;
      margin-bottom: 30px;
      position: relative;
    }

    .ranking h2 {
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
    tr.pos1_8 td { background: #cce5ff; }
    tr.pos9_17 td { background: #ffcccc; }
    tr.empty td { color: #aaa; }

    tr:hover { background-color: #f1f1f1; }
    td[contenteditable="true"] { background: #ffffcc; }

    .btn-pontos {
      padding: 6px 12px;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 14px;
      cursor: pointer;
      margin: 2px;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .btn-presenca { background: #4CAF50; }
    .btn-segundo { background: #2196F3; }
    .btn-terceiro { background: #9C27B0; }
    .btn-quarto { background: #FF9800; }
    .btn-quinto { background: #795548; }
    .btn-campeao { background: #FF5722; }
  </style>
</head>
<body>
  <!-- Topo com botão salvar -->
  <div class="topo">
    <div><h3>📋 Controle do Ranking</h3></div>
    <button class="btn-salvar" onclick="salvarRanking()">💾 Salvar Ranking</button>
  </div>

  <!-- Legenda -->
  <div class="legenda">
    <div><span class="azul"></span> Classificados para a mesa final semestral</div>
    <div><span class="vermelho"></span> Repescagem final</div>
  </div>

  <div class="ranking">
    <h2>🏆 Ranking Poker</h2>
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

  <script>
    let nomes = [
      "Vitor Augusto", "RacBatis", "Briga", "Jhow Jhow", "Erick", "Roque", "Nono", "Veinho", "Rossi", "Mario",
      "Piscine", "Limoli", "Gabriel Vieira", "Brunno", "Victor Costa", "Brian", "Caio", "Pit", "Ale", "Zaca",
      "Gui Farias", "Leo Conde", "Guido", "Caio Japa", "Chicão", "Yoshida", "Arrais", "Lucas Chaves", "Mnafred", "Rangel",
      "Samuel", "Allan", "Dilam", "Espeto", "Gustavo Alemão", "Mateus Grand", "Ricardo Cipolli", "Pedro Jesus", "Boss", "Phillipe",
      "William", "Mata", "Mariana", "Ronaldão", "David", "Dede", "Bezerra", "Edson Arrais", "Henrique", "Pedro Bolívia",
      "Rafa Estefam", "Danton", "Koiti", "Fe Gregio", "Jorge"
    ];

    let jogadores = [];

    // Carrega do localStorage ou cria zerado
    if(localStorage.getItem("rankingJogadores")){
      jogadores = JSON.parse(localStorage.getItem("rankingJogadores"));
    } else {
      jogadores = nomes.map(nome => ({ nome, pontos: 0, presencas: 0, vitorias: 0 }));
    }

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

      for (let i = 0; i < 60; i++) {
        const linha = tabela.insertRow();

        if (i < jogadores.length) {
          const jogador = jogadores[i];

          linha.insertCell().textContent = i + 1;
          linha.insertCell().textContent = jogador.nome;

          // Campos editáveis
          let tdPontos = linha.insertCell();
          tdPontos.textContent = jogador.pontos;
          tdPontos.contentEditable = "true";
          tdPontos.onblur = () => jogador.pontos = parseInt(tdPontos.textContent) || 0;

          let tdPres = linha.insertCell();
          tdPres.textContent = jogador.presencas;
          tdPres.contentEditable = "true";
          tdPres.onblur = () => jogador.presencas = parseInt(tdPres.textContent) || 0;

          let tdVit = linha.insertCell();
          tdVit.textContent = jogador.vitorias;
          tdVit.contentEditable = "true";
          tdVit.onblur = () => jogador.vitorias = parseInt(tdVit.textContent) || 0;

          // Botões
          const celulaBotoes = linha.insertCell();
          [
            { valor: 10, nome: 'Presença', classe: 'btn-presenca', adicionaPresenca: true, adicionaVitoria: false },
            { valor: 80, nome: 'Segundo', classe: 'btn-segundo' },
            { valor: 60, nome: 'Terceiro', classe: 'btn-terceiro' },
            { valor: 40, nome: 'Quarto', classe: 'btn-quarto' },
            { valor: 20, nome: 'Quinto', classe: 'btn-quinto' },
            { valor: 100, nome: 'Campeão', classe: 'btn-campeao', adicionaVitoria: true }
          ].forEach(item => {
            const btn = document.createElement("button");
            btn.textContent = item.nome;
            btn.className = `btn-pontos ${item.classe}`;
            btn.onclick = () => {
              jogador.pontos += item.valor;
              if(item.adicionaPresenca) jogador.presencas += 1;
              if(item.adicionaVitoria) jogador.vitorias += 1;
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

    function salvarRanking(){
      localStorage.setItem("rankingJogadores", JSON.stringify(jogadores));
      alert("✅ Ranking salvo com sucesso!");
    }

    atualizarTabela();
  </script>
</body>
</html>
