<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Ranking Home Ras Poker 2025</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 30px;
    }

    .ranking, .formulario {
      background: #fff;
      padding: 15px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 750px;
      margin-bottom: 20px;
      position: relative;
    }

    h2 {
      text-align: center;
      margin-bottom: 15px;
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
      background: #fff;
    }

    th, td {
      padding: 8px;
      text-align: center;
      border: 1px solid #ddd;
      font-size: 14px;
    }

    th {
      background-color: #333;
      color: white;
    }

    tr.pos1_8 td { background: #cce5ff; }
    tr.pos9_17 td { background: #ffcccc; }

    td[contenteditable="true"] {
      background: #fafafa;
      cursor: text;
    }

    /* Botões */
    .formulario button, .top-buttons button {
      padding: 8px 12px;
      margin: 5px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      background: #ffcc00;
      color: #000;
      font-weight: bold;
    }

    .formulario button:hover, .top-buttons button:hover {
      background: #e6b800;
    }

    .top-buttons {
      margin-bottom: 15px;
    }

    /* Estilo exclusivo para exportação PNG */
    #rankingExport {
      display: none;
      background: #3e2723 url("https://www.transparenttextures.com/patterns/wood-pattern.png");
      padding: 20px;
      border-radius: 15px;
      border: 3px solid #ffcc00;
      box-shadow: 10px 10px 25px rgba(0,0,0,0.7);
      width: 750px;
      color: #fff;
    }

    #rankingExport h2 {
      text-align: center;
      color: #ffcc00;
      font-size: 20px;
      margin-bottom: 15px;
    }

    #rankingExport table {
      width: 100%;
      border-collapse: collapse;
    }

    #rankingExport th, #rankingExport td {
      padding: 8px;
      text-align: center;
      border: 1px solid #a1887f;
      color: #fff;
    }

    #rankingExport th {
      background-color: #ffcc00;
      color: #000;
    }

    #rankingExport tr.pos1_8 td {
      background: #1565c0;
      color: #fff;
    }

    #rankingExport tr.pos9_17 td {
      background: #b71c1c;
      color: #fff;
    }
  </style>
</head>
<body>
  <div class="top-buttons">
    <button onclick="salvarRanking()">💾 Salvar Ranking</button>
    <button onclick="exportarPNG()">📸 Exportar PNG</button>
  </div>

  <div class="legenda">
    <div><span class="azul"></span> Classificados</div>
    <div><span class="vermelho"></span> Repescagem</div>
  </div>

  <!-- Ranking interativo -->
  <div class="ranking">
    <h2>🏆 Ranking Home Ras Poker 2025</h2>
    <table id="rankingTable">
      <tr>
        <th>Posição</th>
        <th>Nome</th>
        <th>Pontos</th>
        <th>Presenças</th>
        <th>Vitórias</th>
      </tr>
    </table>
  </div>

  <div class="formulario">
    <h3>➕ Adicionar Jogador</h3>
    <input type="text" id="nome" placeholder="Nome do jogador">
    <button onclick="adicionarJogador()">Adicionar</button>
  </div>

  <!-- Ranking para exportação -->
  <div id="rankingExport">
    <h2>🏆 Ranking Home Ras Poker 2025</h2>
    <table id="exportTable"></table>
  </div>

  <script>
    let jogadores = JSON.parse(localStorage.getItem("ranking")) || [];

    // Lista inicial até 60 jogadores
    if (jogadores.length === 0) {
      const nomes = [
        "Vitor Augusto","RacBatis","Briga","Jhow Jhow","Erick","Roque","Nono","Veinho","Rossi","Mario",
        "Piscine","Limoli","Gabriel Vieira","Brunno","Victor Costa","Brian","Caio","Pit","Ale","Zaca",
        "Gui Farias","Leo Conde","Guido","Caio Japa","Chicão","Yoshida","Arrais","Lucas Chaves","Mnafred","Rangel",
        "Samuel","Allan","Dilam","Espeto","Gustavo Alemão","Mateus Grand","Ricardo Cipolli","Pedro Jesus","Boss","Phillipe",
        "William","Mata","Mariana","Ronaldão","David","Dede","Bezerra","Edson Arrais","Henrique","Pedro Bolívia",
        "Rafa Estefam","Danton","Koiti","Fe Gregio","Jorge","Igor","Camila","André","Paula","Carolina"
      ];
      jogadores = nomes.map(n => ({ nome: n, pontos: 0, presencas: 0, vitorias: 0 }));
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
        </tr>
      `;

      jogadores.sort((a, b) => 
        b.vitorias - a.vitorias || 
        b.presencas - a.presencas || 
        b.pontos - a.pontos
      );

      jogadores.forEach((jogador, i) => {
        const linha = tabela.insertRow();
        if (i < 8) linha.classList.add("pos1_8");
        else if (i < 17) linha.classList.add("pos9_17");

        linha.insertCell().textContent = i + 1;
        linha.insertCell().textContent = jogador.nome;
        linha.insertCell().contentEditable = "true";
        linha.cells[1].onblur = e => { jogador.nome = e.target.textContent; salvarRanking(); };

        linha.insertCell().textContent = jogador.pontos;
        linha.cells[2].contentEditable = "true";
        linha.cells[2].onblur = e => { jogador.pontos = parseInt(e.target.textContent) || 0; salvarRanking(); };

        linha.insertCell().textContent = jogador.presencas;
        linha.cells[3].contentEditable = "true";
        linha.cells[3].onblur = e => { jogador.presencas = parseInt(e.target.textContent) || 0; salvarRanking(); };

        linha.insertCell().textContent = jogador.vitorias;
        linha.cells[4].contentEditable = "true";
        linha.cells[4].onblur = e => { jogador.vitorias = parseInt(e.target.textContent) || 0; salvarRanking(); };
      });
    }

    function salvarRanking() {
      localStorage.setItem("ranking", JSON.stringify(jogadores));
      atualizarTabela();
    }

    function adicionarJogador() {
      const nome = document.getElementById("nome").value.trim();
      if (nome) {
        jogadores.push({ nome, pontos: 0, presencas: 0, vitorias: 0 });
        salvarRanking();
        document.getElementById("nome").value = "";
      }
    }

    function exportarPNG() {
      const exportDiv = document.getElementById("rankingExport");
      const exportTable = document.getElementById("exportTable");

      exportTable.innerHTML = `
        <tr>
          <th>Posição</th>
          <th>Nome</th>
          <th>Pontos</th>
          <th>Presenças</th>
          <th>Vitórias</th>
        </tr>
      `;

      jogadores.forEach((jogador, i) => {
        const linha = exportTable.insertRow();
        if (i < 8) linha.classList.add("pos1_8");
        else if (i < 17) linha.classList.add("pos9_17");

        linha.insertCell().textContent = i + 1;
        linha.insertCell().textContent = jogador.nome;
        linha.insertCell().textContent = jogador.pontos;
        linha.insertCell().textContent = jogador.presencas;
        linha.insertCell().textContent = jogador.vitorias;
      });

      exportDiv.style.display = "block";
      html2canvas(exportDiv).then(canvas => {
        const link = document.createElement("a");
        link.download = "ranking.png";
        link.href = canvas.toDataURL();
        link.click();
        exportDiv.style.display = "none";
      });
    }

    atualizarTabela();
  </script>
</body>
</html>
