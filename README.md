<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>🏆 Ranking Home Ras Poker 2025</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f5f5dc;
      margin: 0;
      padding: 20px;
    }

    .ranking {
      max-width: 1200px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
    }

    .ranking h2 {
      text-align: center;
      margin-bottom: 15px;
      color: #222; /* escuro */
      text-transform: uppercase;
      font-weight: bold;
      font-size: 22px;
      text-decoration: underline; /* sublinhado */
    }

    .legenda {
      margin-bottom: 15px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background: #fafafa;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 15px;
      font-size: 14px;
    }

    th, td {
      border: 1px solid #ccc;
      padding: 6px;
      text-align: center;
    }

    th {
      background: #ffcc00;
      color: #222;
    }

    tr.azul {
      background-color: #cce5ff;
    }

    tr.vermelho {
      background-color: #f8d7da;
    }

    td button {
      margin: 2px;
      padding: 4px 6px;
      font-size: 12px;
      cursor: pointer;
      border-radius: 6px;
      border: none;
      background-color: #ffcc00;
      color: #222;
      font-weight: bold;
    }

    td:last-child {
      display: flex;
      justify-content: center; /* centraliza */
      flex-wrap: wrap;         /* quebra linha se necessário */
      gap: 4px;                /* espaçamento entre botões */
    }

    .controls {
      margin-bottom: 15px;
      text-align: center;
    }

    .controls button {
      margin: 5px;
      padding: 8px 14px;
      background: #ffcc00;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
      color: #222;
    }
  </style>
</head>
<body>
  <div class="ranking">
    <h2>🏆 Ranking Home Ras Poker 2025</h2>

    <div class="legenda">
      🔵 Jogadores em <span style="background:#cce5ff; padding:2px 6px; border-radius:4px;">AZUL CLARO</span> → Classificados para a <b>Mesa Final Semestral</b><br>
      🔴 Jogadores em <span style="background:#f8d7da; padding:2px 6px; border-radius:4px;">VERMELHO CLARO</span> → Estão na <b>Repescagem Final</b>
    </div>

    <div class="controls">
      <button onclick="salvarRanking()">💾 Salvar Ranking</button>
      <button onclick="adicionarJogador()">➕ Adicionar Jogador</button>
      <button onclick="exportarTabela()">📸 Exportar Tabela (PNG)</button>
    </div>

    <table id="rankingTable">
      <thead>
        <tr>
          <th>Posição</th>
          <th>Nome</th>
          <th>Pontos</th>
          <th>Vitórias</th>
          <th>Presenças</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody id="rankingBody"></tbody>
    </table>
  </div>

  <script>
    let jogadores = JSON.parse(localStorage.getItem("ranking")) || [
      "Vitor Augusto","RacBatis","Briga","Jhow Jhow","Erick","Roque","Nono","Veinho","Rossi","Mario",
      "Piscine","Limoli","Gabriel Vieira","Brunno","Victor Costa","Brian","Caio","Pit","Ale","Zaca",
      "Gui Farias","Leo Conde","Guido","Caio Japa","Chicão","Yoshida","Arrais","Lucas Chaves","Mnafred","Rangel",
      "Samuel","Allan","Dilam","Espeto","Gustavo Alemão","Mateus Grand","Ricardo Cipolli","Pedro Jesus","Boss","Phillipe",
      "William","Mata","Mariana","Ronaldão","David","Dede","Bezerra","Edson Arrais","Henrique","Pedro Bolívia",
      "Rafa Estefam","Danton","Koiti","Fe Gregio","Jorge","Carlos","Felipe","André","Thiago","Ruan"
    ].map(nome => ({nome, pontos:0, vitorias:0, presencas:0}));

    function atualizarTabela() {
      // ordenação: vitórias > presenças > pontos
      jogadores.sort((a,b) => 
        b.vitorias - a.vitorias || 
        b.presencas - a.presencas || 
        b.pontos - a.pontos
      );

      const tbody = document.getElementById("rankingBody");
      tbody.innerHTML = "";

      jogadores.forEach((jogador, i) => {
        const tr = document.createElement("tr");

        if (i < 8) tr.classList.add("azul");
        else if (i < 17) tr.classList.add("vermelho");

        tr.innerHTML = `
          <td>${i+1}</td>
          <td contenteditable="true" oninput="editarNome(${i}, this.innerText)">${jogador.nome}</td>
          <td contenteditable="true" oninput="editarCampo(${i}, 'pontos', this.innerText)">${jogador.pontos}</td>
          <td contenteditable="true" oninput="editarCampo(${i}, 'vitorias', this.innerText)">${jogador.vitorias}</td>
          <td contenteditable="true" oninput="editarCampo(${i}, 'presencas', this.innerText)">${jogador.presencas}</td>
          <td>
            <button onclick="adicionarPontos(${i},10,'presencas')">Presença</button>
            <button onclick="adicionarPontos(${i},50)">Segundo</button>
            <button onclick="adicionarPontos(${i},100,'vitorias')">Campeão</button>
            <button onclick="adicionarPontos(${i},30)">Terceiro</button>
            <button onclick="adicionarPontos(${i},20)">Quarto</button>
            <button onclick="adicionarPontos(${i},10)">Quinto</button>
          </td>
        `;
        tbody.appendChild(tr);
      });
    }

    function adicionarPontos(i, pontos, extra) {
      jogadores[i].pontos += pontos;
      if (extra === "vitorias") jogadores[i].vitorias++;
      if (extra === "presencas") jogadores[i].presencas++;
      atualizarTabela();
    }

    function editarNome(i, novoNome) {
      jogadores[i].nome = novoNome;
    }

    function editarCampo(i, campo, valor) {
      jogadores[i][campo] = parseInt(valor) || 0;
      atualizarTabela();
    }

    function salvarRanking() {
      localStorage.setItem("ranking", JSON.stringify(jogadores));
      alert("✅ Ranking salvo com sucesso!");
    }

    function adicionarJogador() {
      jogadores.push({nome:"Novo Jogador", pontos:0, vitorias:0, presencas:0});
      atualizarTabela();
    }

    function exportarTabela() {
      const clone = document.createElement("div");
      clone.innerHTML = `
        <h2>🏆 Ranking Home Ras Poker 2025</h2>
        <table>
          <thead>
            <tr>
              <th>Posição</th>
              <th>Nome</th>
              <th>Pontos</th>
              <th>Vitórias</th>
              <th>Presenças</th>
            </tr>
          </thead>
          <tbody>
            ${jogadores.map((j,i)=>`
              <tr class="${i<8?'azul':i<17?'vermelho':''}">
                <td>${i+1}</td>
                <td>${j.nome}</td>
                <td>${j.pontos}</td>
                <td>${j.vitorias}</td>
                <td>${j.presencas}</td>
              </tr>`).join("")}
          </tbody>
        </table>
      `;
      document.body.appendChild(clone);
      html2canvas(clone).then(canvas => {
        const link = document.createElement("a");
        link.download = "ranking.png";
        link.href = canvas.toDataURL();
        link.click();
        document.body.removeChild(clone);
      });
    }

    atualizarTabela();
  </script>
</body>
</html>
