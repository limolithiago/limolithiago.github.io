<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Ranking Home Ras Poker 2025</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f5f5dc;
    margin: 0;
    padding: 20px;
    color: #222;
  }

  .ranking {
    max-width: 1200px;
    margin: auto;
    background: #fff8dc;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
  }

  .ranking h2 {
    text-align: center;
    margin-bottom: 15px;
    color: #222;
    text-transform: uppercase;
    font-weight: bold;
    font-size: 22px;
    text-decoration: underline;
  }

  .legenda {
    margin-bottom: 15px;
    font-size: 14px;
    color: #222;
  }

  .legenda span {
    display: inline-block;
    width: 20px;
    height: 20px;
    margin-right: 5px;
    border-radius: 4px;
    border: 1px solid #000;
  }

  .azul { background-color: #cce5ff; }
  .vermelho { background-color: #f8d7da; }

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
    color: #222;
  }

  th {
    background: #ffcc00;
    color: #222;
  }

  tr.azul td { background-color: #cce5ff; color: #222; }
  tr.vermelho td { background-color: #f8d7da; color: #222; }
  tr.empty td { color: #555; }
  tr:hover { background-color: rgba(0,0,0,0.05); }

  td[contenteditable="true"] {
    background: rgba(255,236,179,0.3);
    border: 1px dashed #ffcc00;
  }

  td:last-child {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 4px;
  }

  td button {
    margin: 2px;
    padding: 4px 6px;
    font-size: 12px;
    cursor: pointer;
    border-radius: 6px;
    border: none;
    font-weight: bold;
    color: #fff;
  }

  .btn-presenca { background: #4CAF50; }
  .btn-segundo { background: #2196F3; }
  .btn-terceiro { background: #9C27B0; }
  .btn-quarto { background: #FF9800; }
  .btn-quinto { background: #795548; }
  .btn-campeao { background: #FF5722; }

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
    <span class="azul"></span> Classificados para a Mesa Final Semestral
    &nbsp;&nbsp;&nbsp;
    <span class="vermelho"></span> Repescagem Final
  </div>

  <div class="controls">
    <button onclick="salvarRanking()">💾 Salvar Ranking</button>
    <button onclick="adicionarJogador()">➕ Adicionar Jogador</button>
    <button onclick="exportarTabela()">📸 Exportar Tabela</button>
  </div>

  <table>
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
  let nomes = [
    "Vitor Augusto","RacBatis","Briga","Jhow Jhow","Erick","Roque","Nono","Veinho","Rossi","Mario",
    "Piscine","Limoli","Gabriel Vieira","Brunno","Victor Costa","Brian","Caio","Pit","Ale","Zaca",
    "Gui Farias","Leo Conde","Guido","Caio Japa","Chicão","Yoshida","Arrais","Lucas Chaves","Mnafred","Rangel",
    "Samuel","Allan","Dilam","Espeto","Gustavo Alemão","Mateus Grand","Ricardo Cipolli","Pedro Jesus","Boss","Phillipe",
    "William","Mata","Mariana","Ronaldão","David","Dede","Bezerra","Edson Arrais","Henrique","Pedro Bolívia",
    "Rafa Estefam","Danton","Koiti","Fe Gregio","Jorge","Carlos","Felipe","André","Thiago","Ruan"
  ];

  let jogadores = JSON.parse(localStorage.getItem("ranking")) || nomes.map(n => ({nome:n,pontos:0,vitorias:0,presencas:0}));

  function atualizarTabela() {
    jogadores.sort((a,b) => b.vitorias - a.vitorias || b.presencas - a.presencas || b.pontos - a.pontos);
    const tbody = document.getElementById("rankingBody");
    tbody.innerHTML = "";
    jogadores.forEach((j, i) => {
      const tr = document.createElement("tr");
      if(i<8) tr.classList.add("azul");
      else if(i<17) tr.classList.add("vermelho");
      tr.innerHTML = `
        <td>${i+1}</td>
        <td contenteditable="true" oninput="editarNome(${i},this.innerText)">${j.nome}</td>
        <td contenteditable="true" oninput="editarCampo(${i},'pontos',this.innerText)">${j.pontos}</td>
        <td contenteditable="true" oninput="editarCampo(${i},'vitorias',this.innerText)">${j.vitorias}</td>
        <td contenteditable="true" oninput="editarCampo(${i},'presencas',this.innerText)">${j.presencas}</td>
        <td>
          <button class="btn-presenca" onclick="adicionarPontos(${i},10,'presencas')">Presença</button>
          <button class="btn-segundo" onclick="adicionarPontos(${i},50)">Segundo</button>
          <button class="btn-terceiro" onclick="adicionarPontos(${i},30)">Terceiro</button>
          <button class="btn-quarto" onclick="adicionarPontos(${i},20)">Quarto</button>
          <button class="btn-quinto" onclick="adicionarPontos(${i},10)">Quinto</button>
          <button class="btn-campeao" onclick="adicionarPontos(${i},100,'vitorias')">Campeão</button>
        </td>
      `;
      tbody.appendChild(tr);
    });
  }

  function adicionarPontos(i,pontos,extra) {
    jogadores[i].pontos += pontos;
    if(extra==='vitorias') jogadores[i].vitorias++;
    if(extra==='presencas') jogadores[i].presencas++;
    atualizarTabela();
  }

  function editarNome(i,novo){ jogadores[i].nome=novo; }
  function editarCampo(i,campo,valor){ jogadores[i][campo]=parseInt(valor)||0; atualizarTabela(); }
  function salvarRanking(){ localStorage.setItem("ranking",JSON.stringify(jogadores)); alert("✅ Ranking salvo!"); }

  function adicionarJogador(){ 
    const nome = prompt("Nome do novo jogador:"); 
    if(nome && nome.trim()!=="") { 
      jogadores.push({nome:nome.trim(),pontos:0,vitorias:0,presencas:0}); 
      atualizarTabela(); 
    }
  }

  function exportarTabela(){
    const clone = document.createElement("div");
    clone.innerHTML = `<h2>🏆 Ranking Home Ras Poker 2025</h2>
      <table>
        <thead><tr><th>Posição</th><th>Nome</th><th>Pontos</th><th>Vitórias</th><th>Presenças</th></tr></thead>
        <tbody>${jogadores.map((j,i)=>`
          <tr class="${i<8?'azul':i<17?'vermelho':''}">
            <td>${i+1}</td><td>${j.nome}</td><td>${j.pontos}</td><td>${j.vitorias}</td><td>${j.presencas}</td>
          </tr>`).join('')}
        </tbody>
      </table>`;
    document.body.appendChild(clone);
    html2canvas(clone).then(canvas=>{
      const link = document.createElement("a");
      link.download="ranking.png";
      link.href = canvas.toDataURL();
      link.click();
      document.body.removeChild(clone);
    });
  }

  atualizarTabela();
</script>
</body>
</html>
