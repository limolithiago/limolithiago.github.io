<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Ranking Poker Piscine 2025</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
  body {
    font-family: "Trebuchet MS", Arial, sans-serif;
    background: #f5f5f5;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 10px;
  }

  .topo {
    width: 100%;
    max-width: 750px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-bottom: 15px;
    gap: 8px;
  }

  .btn {
    flex: 1;
    min-width: 140px;
    background: #ffcc00;
    color: #3e2723;
    border: none;
    padding: 12px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    font-weight: bold;
    text-align: center;
    box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
  }
  .btn:hover { background: #ffb300; }

  .ranking {
    background: linear-gradient(135deg, #3e2723 0%, #5d4037 25%, #d7ccc8 50%, #5d4037 75%, #3e2723 100%);
    padding: 15px;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    width: 100%;
    max-width: 750px;
    margin-bottom: 20px;
    border: 2px solid #ffcc00;
    color: #fff;
    font-weight: bold;
    overflow-x: auto;
  }

  .ranking h2 {
    text-align: center;
    margin-bottom: 5px;
    color: #ffe082;
    text-transform: uppercase;
    font-size: 20px;
  }

  .data-atualizacao {
    text-align: center;
    font-size: 13px;
    color: #000;
    margin-bottom: 15px;
    display: none;
  }

  .logo-certificado {
    display: none;
    text-align: center;
    margin-bottom: 10px;
  }
  .logo-certificado img {
    width: 80px;
    height: 80px;
  }

  .legenda {
    width: 100%;
    max-width: 750px;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 10px;
    gap: 12px;
    font-size: 13px;
    color: #000;
  }
  .legenda div { display: flex; align-items: center; gap: 5px; }
  .legenda span { display: inline-block; width: 16px; height: 16px; border-radius: 3px; border: 1px solid #000; }
  .azul { background: #81d4fa; }
  .vermelho { background: #ff8a80; }

  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th, td { padding: 6px; text-align: center; border-bottom: 1px solid #a1887f; border-right: 1px solid #a1887f; color: #000; }
  th { background-color: #ffcc00; color: #000; border-bottom: 2px solid #3e2723; }
  tr.pos1_8 td { background: #81d4fa; color: #000; }
  tr.pos9_17 td { background: #ff8a80; color: #000; }
  tr.empty td { color: #555; }
  tr:hover { background-color: rgba(0,0,0,0.1); }

  td[contenteditable="true"] {
    background: rgba(255,236,179,0.3);
    border: 1px dashed #ffcc00;
  }

  .botoes-container { display: flex; justify-content: center; flex-wrap: wrap; gap: 4px; }
  .btn-pontos { 
    padding: 4px 6px; 
    color: white; 
    border: none; 
    border-radius: 4px; 
    font-size: 11px; 
    cursor: pointer; 
  }
  .btn-presenca { background: #4CAF50; }
  .btn-segundo { background: #2196F3; }
  .btn-terceiro { background: #9C27B0; }
  .btn-quarto { background: #FF9800; }
  .btn-quinto { background: #795548; }
  .btn-campeao { background: #FF5722; }
  .btn-sexto { background: #8BC34A; }
  .btn-setimo { background: #00BCD4; }
  .btn-oitavo { background: #FFC107; }
  .btn-nono { background: #9E9E9E; }
  .btn-excluir { background: #e53935; color: #fff; padding: 4px 8px; font-size: 11px; border-radius: 4px; cursor: pointer; }

  .animacao-pontos {
    position: absolute;
    font-weight: bold;
    color: #ff5722;
    animation: subirFade 1s forwards;
    pointer-events: none;
    font-size: 14px;
  }
  @keyframes subirFade {
    0% { opacity: 1; transform: translateY(0); }
    100% { opacity: 0; transform: translateY(-25px); }
  }

  /* --- Estilo especial para exportação (certificado) --- */
  .export-mode {
    background: #fff !important;
    border: 6px solid #ffcc00 !important;
    border-radius: 20px;
    padding: 25px !important;
    box-shadow: 0 0 25px rgba(0,0,0,0.3);
  }
  .export-mode td.acoes, 
  .export-mode th.acoes { 
    display: none !important; 
  }
  .export-mode .logo-certificado {
    display: block !important;
  }
  .export-mode h2 {
    font-size: 26px !important;
    font-weight: bold;
    color: #3e2723 !important;
    text-align: center;
    margin-bottom: 10px;
    text-transform: uppercase;
  }
  .export-mode .data-atualizacao {
    display: block !important;
    font-size: 12px;
    font-style: italic;
    color: #444;
  }
  .export-mode table {
    border: 2px solid #3e2723;
    border-radius: 10px;
    background: #fff !important;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  .export-mode th {
    background: #ffcc00 !important;
    color: #000 !important;
    font-size: 14px;
  }
  .export-mode td {
    font-size: 13px;
    padding: 8px;
  }
</style>
</head>
<body>

<div class="topo">
  <button class="btn" onclick="salvarRanking()">💾 Salvar Ranking</button>
  <button class="btn" onclick="adicionarJogador()">➕ Adicionar Jogador</button>
  <button class="btn" onclick="atualizarTabela()">🔄 Atualizar Tabela</button>
  <button class="btn" onclick="exportarTabela()">📷 Exportar Tabela</button>
</div>

<div class="legenda">
  <div><span class="azul"></span> Classificados para a mesa final</div>
  <div><span class="vermelho"></span> Repescagem final</div>
</div>

<div class="ranking" id="rankingContainer">
  <div class="logo-certificado">
    <img src="https://cdn-icons-png.flaticon.com/512/616/616490.png" alt="Logo Poker">
  </div>
  <h2>🏆 Ranking Poker Piscine 2025</h2>
  <div class="data-atualizacao" id="dataExportacao"></div>
  <table id="rankingTable">
    <tr>
      <th>Posição</th>
      <th>Nome</th>
      <th>Pontos</th>
      <th>Presenças</th>
      <th>Vitórias</th>
      <th class="acoes">Ações</th>
    </tr>
  </table>
</div>

<script>
let jogadores = []; 

if(localStorage.getItem("rankingJogadores")){
  jogadores = JSON.parse(localStorage.getItem("rankingJogadores"));
}

function atualizarTabela() {
  const tabela = document.getElementById("rankingTable");
  tabela.innerHTML = `<tr>
    <th>Posição</th>
    <th>Nome</th>
    <th>Pontos</th>
    <th>Presenças</th>
    <th>Vitórias</th>
    <th class="acoes">Ações</th>
  </tr>`;

  jogadores.sort((a,b) => {
    if(b.pontos !== a.pontos) return b.pontos - a.pontos;
    if(b.vitorias !== a.vitorias) return b.vitorias - a.vitorias;
    return b.presencas - a.presencas;
  });

  jogadores.forEach((j,i)=>{
    const linha = tabela.insertRow();
    if(i<8) linha.classList.add("pos1_8");
    else if(i<17) linha.classList.add("pos9_17");

    linha.insertCell().textContent = i+1;
    let tdNome = linha.insertCell(); 
    tdNome.textContent = j.nome; 
    tdNome.contentEditable="true"; 
    tdNome.onblur=()=>j.nome=tdNome.textContent;

    let tdP = linha.insertCell(); 
    tdP.textContent=j.pontos; 
    tdP.contentEditable="true"; 
    tdP.onblur=()=>j.pontos=parseInt(tdP.textContent)||0;

    let tdPres=linha.insertCell(); 
    tdPres.textContent=j.presencas; 
    tdPres.contentEditable="true"; 
    tdPres.onblur=()=>j.presencas=parseInt(tdPres.textContent)||0;

    let tdVit=linha.insertCell(); 
    tdVit.textContent=j.vitorias; 
    tdVit.contentEditable="true"; 
    tdVit.onblur=()=>j.vitorias=parseInt(tdVit.textContent)||0;

    const celulaAcoes = linha.insertCell();
    celulaAcoes.className="acoes";
    const containerBtns = document.createElement("div");
    containerBtns.className = "botoes-container";

    [
      { valor:10, nome:'Presença', classe:'btn-presenca', adicionaPresenca:true },
      { valor:250, nome:'Campeão', classe:'btn-campeao', adicionaVitoria:true },
      { valor:150, nome:'Segundo', classe:'btn-segundo' },
      { valor:100, nome:'Terceiro', classe:'btn-terceiro' },
      { valor:70, nome:'Quarto', classe:'btn-quarto' },
      { valor:50, nome:'Quinto', classe:'btn-quinto' },
      { valor:40, nome:'Sexto', classe:'btn-sexto' },
      { valor:30, nome:'Sétimo', classe:'btn-setimo' },
      { valor:20, nome:'Oitavo', classe:'btn-oitavo' },
      { valor:10, nome:'Nono', classe:'btn-nono' }
    ].forEach(item=>{
      const btn=document.createElement("button");
      btn.textContent=item.nome;
      btn.className=`btn-pontos ${item.classe}`;
      btn.onclick=()=>{
        j.pontos+=item.valor;
        if(item.adicionaPresenca) j.presencas+=1;
        if(item.adicionaVitoria) j.vitorias+=1;
        mostrarAnimacao(tdP,item.valor);
        atualizarTabela();
      };
      containerBtns.appendChild(btn);
    });

    const btnExcluir=document.createElement("button");
    btnExcluir.textContent="🗑 Excluir";
    btnExcluir.className="btn-excluir";
    btnExcluir.onclick=()=>{
      if(confirm(`Deseja realmente excluir o jogador "${j.nome}"?`)){
        jogadores.splice(i,1);
        atualizarTabela();
      }
    };
    containerBtns.appendChild(btnExcluir);

    celulaAcoes.appendChild(containerBtns);
  });
}

function mostrarAnimacao(celula, valor){
  const anim = document.createElement("div");
  anim.className = "animacao-pontos";
  anim.textContent = `+${valor}`;
  celula.style.position = "relative";
  celula.appendChild(anim);
  setTimeout(()=> anim.remove(), 1000);
}

function salvarRanking(){ 
  localStorage.setItem("rankingJogadores",JSON.stringify(jogadores)); 
  alert("✅ Ranking salvo!"); 
}

function adicionarJogador(){ 
  let nome=prompt("Digite o nome do novo jogador:");
  if(nome&&nome.trim()!==""){ 
    jogadores.push({nome:nome.trim(),pontos:0,presencas:0,vitorias:0}); 
    atualizarTabela(); 
  } 
}

function exportarTabela(){
  const container=document.getElementById("rankingContainer");
  const data=document.getElementById("dataExportacao");
  const agora=new Date();
  data.textContent="Atualizado em: "+agora.toLocaleDateString("pt-BR")+" às "+agora.toLocaleTimeString("pt-BR");
  container.classList.add("export-mode"); 
  html2canvas(container).then(canvas=>{
    const link=document.createElement("a");
    link.download="ranking.png";
    link.href=canvas.toDataURL();
    link.click();
    container.classList.remove("export-mode"); 
    data.textContent=""; 
  });
}

atualizarTabela();
</script>
</body>
</html>
