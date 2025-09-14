<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Ranking Home Ras Poker 2025</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    body {
      font-family: "Trebuchet MS", Arial, sans-serif;
      background: #f4f1ea;
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 30px;
      color: #3e2723;
    }

    .topo {
      width: 750px;
      display: flex;
      justify-content: space-between;
      margin-bottom: 15px;
      gap: 10px;
    }

    .btn-salvar, .btn-add, .btn-exportar {
      background: #ffcc00;
      color: #3e2723;
      border: none;
      padding: 10px 15px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 14px;
      font-weight: bold;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
    }
    .btn-salvar:hover, .btn-add:hover, .btn-exportar:hover {
      background: #ffb300;
    }

    .ranking {
      background: #fff8e1;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      width: 750px;
      margin-bottom: 30px;
      border: 2px solid #ffcc00;
    }

    .ranking h2 {
      text-align: center;
      margin-bottom: 15px;
      color: #3e2723;
      text-transform: uppercase;
      font-weight: bold;
      font-size: 22px;
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
      border: 1px solid #3e2723;
    }

    .azul { background: #cce5ff; }
    .vermelho { background: #ffcccc; }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      padding: 6px;
      text-align: center;
      border-bottom: 1px solid #bbb;
      border-right: 1px solid #ddd;
    }

    th {
      background-color: #ffcc00;
      color: #3e2723;
      border-bottom: 2px solid #3e2723;
      font-size: 14px;
    }

    tr.pos1_8 td { background: #cce5ff; }
    tr.pos9_17 td { background: #ffcccc; }
    tr.empty td { color: #aaa; }

    tr:hover { background-color: #fff3cd; }

    td[contenteditable="true"] { background: #fffde7; border: 1px dashed #ffcc00; }

    .btn-pontos {
      padding: 3px 8px;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 12px;
      cursor: pointer;
      margin: 1px;
    }

    .btn-presenca { background: #4CAF50; }
    .btn-segundo { background: #2196F3; }
    .btn-terceiro { background: #9C27B0; }
    .btn-quarto { background: #FF9800; }
    .btn-quinto { background: #795548; }
    .btn-campeao { background: #FF5722; }

    /* tabela de exportação invisível */
    #rankingExport {
      display: none;
    }
  </style>
</head>
<body>
  <!-- Topo -->
  <div class="topo">
    <button class="btn-salvar" onclick="salvarRanking()">💾 Salvar Ranking</button>
    <button class="btn-add" onclick="adicionarJogador()">➕ Adicionar Jogador</button>
    <button class="btn-exportar" onclick="exportarTabela()">📷 Exportar Tabela</button>
  </div>

  <!-- Legenda -->
  <div class="legenda">
    <div><span class="azul"></span> Classificados para a mesa final semestral</div>
    <div><span class="vermelho"></span> Repescagem final</div>
  </div>

  <!-- Ranking com botões -->
  <div class="ranking" id="rankingContainer">
    <h2>🏆 Ranking Home Ras Poker 2025</h2>
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

  <!-- Ranking somente para exportação -->
  <div class="ranking" id="rankingExport">
    <h2>🏆 Ranking Home Ras Poker 2025</h2>
    <table id="exportTable">
      <tr>
        <th>Posição</th>
        <th>Nome</th>
        <th>Pontos</th>
        <th>Presenças</th>
        <th>Vitórias</th>
      </tr>
    </table>
  </div>

  <script>
    let nomes = [
      "Vitor Augusto","RacBatis","Briga","Jhow Jhow","Erick","Roque","Nono","Veinho","Rossi","Mario",
      "Piscine","Limoli","Gabriel Vieira","Brunno","Victor Costa","Brian","Caio","Pit","Ale","Zaca",
      "Gui Farias","Leo Conde","Guido","Caio Japa","Chicão","Yoshida","Arrais","Lucas Chaves","Mnafred","Rangel",
      "Samuel","Allan","Dilam","Espeto","Gustavo Alemão","Mateus Grand","Ricardo Cipolli","Pedro Jesus","Boss","Phillipe",
      "William","Mata","Mariana","Ronaldão","David","Dede","Bezerra","Edson Arrais","Henrique","Pedro Bolívia",
      "Rafa Estefam","Danton","Koiti","Fe Gregio","Jorge"
    ];

    let jogadores = [];

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

      for (let i = 0; i < jogadores.length; i++) {
        const linha = tabela.insertRow();
        const jogador = jogadores[i];

        linha.insertCell().textContent = i + 1;
        linha.insertCell().textContent = jogador.nome;

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

        const celulaBotoes = linha.insertCell();
        [
          { valor: 10, nome: 'Presença', classe: 'btn-presenca', adicionaPresenca: true },
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
      }
    }

    function atualizarTabelaExport() {
      const tabela = document.getElementById("exportTable");
      tabela.innerHTML = `
        <tr>
          <th>Posição</th>
          <th>Nome</th>
          <th>Pontos</th>
          <th>Presenças</th>
          <th>Vitórias</th>
        </tr>
      `;

      jogadores.sort((a, b) => b.pontos - a.pontos);

      for (let i = 0; i < jogadores.length; i++) {
        const linha = tabela.insertRow();
        const jogador = jogadores[i];
        linha.insertCell().textContent = i + 1;
        linha.insertCell().textContent = jogador.nome;
        linha.insertCell().textContent = jogador.pontos;
        linha.insertCell().textContent = jogador.presencas;
        linha.insertCell().textContent = jogador.vitorias;

        if(i < 8) linha.classList.add("pos1_8");
        else if(i < 17) linha.classList.add("pos9_17");
      }
    }

    function salvarRanking(){
      localStorage.setItem("rankingJogadores", JSON.stringify(jogadores));
      alert("✅ Ranking salvo com sucesso!");
    }

    function adicionarJogador(){
      let nome = prompt("Digite o nome do novo jogador:");
      if(nome && nome.trim() !== ""){
        jogadores.push({ nome: nome.trim(), pontos: 0, presencas: 0, vitorias: 0 });
        atualizarTabela();
      }
    }

    function exportarTabela(){
      atualizarTabelaExport();
      const container = document.getElementById("rankingExport");
      container.style.display = "block";
      html2canvas(container).then(canvas => {
        const link = document.createElement("a");
        link.download = "ranking.png";
        link.href = canvas.toDataURL();
        link.click();
        container.style.display = "none";
      });
    }

    atualizarTabela();
  </script>
</body>
</html>
