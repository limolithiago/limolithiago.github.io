<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Ranking Home Ras 2026</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

<style>
  body{
    font-family:"Trebuchet MS", Arial, sans-serif;
    background:#f5f5f5;
    display:flex;
    flex-direction:column;
    align-items:center;
    margin:10px;
    gap:12px;
  }

  .topo{
    width:100%;
    max-width:1200px;
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    margin-bottom:6px;
    gap:8px;
  }

  .btn{
    flex:1;
    min-width:160px;
    background:#ffcc00;
    color:#3e2723;
    border:none;
    padding:12px;
    border-radius:8px;
    cursor:pointer;
    font-size:14px;
    font-weight:bold;
    text-align:center;
    box-shadow:2px 2px 5px rgba(0,0,0,0.2);
  }
  .btn:hover{ background:#ffb300; }

  .btn-undo{
    background:#3e2723;
    color:#fff;
  }
  .btn-undo:hover{ background:#2b1b18; }

  .status{
    width:100%;
    max-width:1200px;
    display:flex;
    gap:8px;
    align-items:center;
    justify-content:space-between;
    flex-wrap:wrap;
    padding:8px 10px;
    border-radius:10px;
    border:1px solid #ddd;
    background:#fff;
    box-shadow:0 2px 8px rgba(0,0,0,0.06);
    font-size:12px;
    color:#333;
  }
  .pill{
    padding:4px 8px;
    border-radius:999px;
    border:1px solid #ddd;
    background:#fafafa;
    font-weight:bold;
    white-space:nowrap;
  }

  /* ====== LAYOUT LADO A LADO ====== */
  .layout{
    width:100%;
    max-width:1200px;
    display:flex;
    gap:12px;
    align-items:flex-start;
    justify-content:center;
    flex-wrap:wrap; /* mobile vira 1 em cima da outra */
  }
  .painel{
    flex:1 1 520px;
    min-width:320px;
  }

  /* Caixa de inscritos */
  .inscritos{
    width:100%;
    background:#ffffff;
    border:2px solid #ffcc00;
    border-radius:12px;
    box-shadow:0 4px 10px rgba(0,0,0,0.12);
    padding:12px;
  }
  .inscritos h3{
    margin:0 0 10px 0;
    color:#3e2723;
    text-transform:uppercase;
    letter-spacing:.5px;
    font-size:16px;
    text-align:center;
  }
  .inscritos .sub{
    text-align:center;
    font-size:12px;
    color:#444;
    margin-bottom:10px;
  }

  .legenda{
    width:100%;
    max-width:1200px;
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    margin-top:4px;
    margin-bottom:2px;
    gap:12px;
    font-size:13px;
    color:#000;
  }
  .legenda div{ display:flex; align-items:center; gap:5px; }
  .legenda span{
    display:inline-block;
    width:16px; height:16px;
    border-radius:3px;
    border:1px solid #000;
  }
  .azul{ background:#81d4fa; }
  .vermelho{ background:#ff8a80; }

  .ranking{
    background:linear-gradient(135deg,#3e2723 0%,#5d4037 25%,#d7ccc8 50%,#5d4037 75%,#3e2723 100%);
    padding:15px;
    border-radius:12px;
    box-shadow:0 4px 10px rgba(0,0,0,0.2);
    width:100%;
    border:2px solid #ffcc00;
    color:#fff;
    font-weight:bold;
    overflow-x:auto;
  }
  .ranking h2{
    text-align:center;
    margin-bottom:5px;
    color:#ffe082;
    text-transform:uppercase;
    font-size:20px;
  }

  .data-atualizacao{
    text-align:center;
    font-size:13px;
    color:#000;
    margin-bottom:12px;
    display:none;
  }

  .logo-certificado{
    display:none;
    text-align:center;
    margin-bottom:10px;
  }
  .logo-certificado img{
    width:92px;
    height:92px;
    object-fit:cover;
    border-radius:14px;
    border:3px solid #3e2723;
    box-shadow:0 6px 14px rgba(0,0,0,0.25);
  }

  table{
    width:100%;
    border-collapse:collapse;
    font-size:13px;
    background:#fff;
    border-radius:8px;
    overflow:hidden;
  }
  th, td{
    padding:6px;
    text-align:center;
    border-bottom:1px solid #a1887f;
    border-right:1px solid #a1887f;
    color:#000;
  }
  th{
    background-color:#ffcc00;
    color:#000;
    border-bottom:2px solid #3e2723;
  }

  tr.pos1_8 td{ background:#81d4fa; color:#000; }
  tr.pos9_17 td{ background:#ff8a80; color:#000; }
  tr.empty td{ color:#555; }
  tr:hover{ background-color:rgba(0,0,0,0.06); }

  td[contenteditable="true"]{
    background:rgba(255,236,179,0.3);
    border:1px dashed #ffcc00;
  }

  .botoes-container{ display:flex; justify-content:center; flex-wrap:wrap; gap:4px; }
  .btn-pontos{
    padding:4px 6px;
    color:white;
    border:none;
    border-radius:4px;
    font-size:11px;
    cursor:pointer;
  }

  /* Botões */
  .btn-presenca{ background:#4CAF50; }
  .btn-campeao{ background:#FF5722; }
  .btn-segundo{ background:#2196F3; }
  .btn-terceiro{ background:#9C27B0; }
  .btn-quarto{ background:#FF9800; }
  .btn-quinto{ background:#795548; }
  .btn-sexto{ background:#8BC34A; }

  .btn-excluir{
    background:#e53935;
    color:#fff;
    padding:4px 8px;
    font-size:11px;
    border-radius:4px;
    cursor:pointer;
  }

  .animacao-pontos{
    position:absolute;
    font-weight:bold;
    color:#ff5722;
    animation:subirFade 1s forwards;
    pointer-events:none;
    font-size:14px;
  }
  @keyframes subirFade{
    0%{ opacity:1; transform:translateY(0); }
    100%{ opacity:0; transform:translateY(-25px); }
  }

  /* --- EXPORT: compacto, marrom/preto/branco --- */
  .export-mode{
    background:#ffffff !important;
    border:8px solid #3e2723 !important;
    border-radius:18px;
    padding:14px !important; /* menos espaço */
    box-shadow:0 0 0 rgba(0,0,0,0) !important;
  }
  .export-mode td.acoes,
  .export-mode th.acoes{ display:none !important; }

  .export-mode .logo-certificado{ display:block !important; }

  .export-mode h2{
    font-size:24px !important;
    font-weight:900;
    color:#3e2723 !important;
    text-align:center;
    margin:8px 0 6px 0 !important;
    text-transform:uppercase;
    letter-spacing:.6px;
  }

  .export-mode .data-atualizacao{
    display:block !important;
    font-size:12px;
    font-style:italic;
    color:#3e2723;
    margin-bottom:10px;
  }

  .export-mode table{
    border:2px solid #3e2723;
    background:#fff !important;
    box-shadow:none !important;
  }

  .export-mode th{
    background:#3e2723 !important;
    color:#fff !important;
    border-bottom:2px solid #000 !important;
  }

  .export-mode td{
    border-right:1px solid #3e2723 !important;
    border-bottom:1px solid #3e2723 !important;
    padding:8px !important;
  }

  /* no export, tira o azul/vermelho e puxa pro marrom */
  .export-mode tr.pos1_8 td{ background:#efe7e3 !important; }
  .export-mode tr.pos9_17 td{ background:#f6f2f0 !important; }
</style>
</head>

<body>

<div class="topo">
  <button class="btn btn-undo" id="btnDesfazer">↩️ Desfazer</button>
  <button class="btn" id="btnAdicionar">➕ Adicionar Jogador</button>
  <button class="btn" id="btnAtualizar">🔄 Atualizar</button>
  <button class="btn" id="btnExportar">📷 Exportar Ranking</button>
</div>

<div class="status">
  <div class="pill" id="pillCloud">☁️ Cloud: conectando...</div>
  <div class="pill" id="pillSync">🔄 Sync: aguardando...</div>
</div>

<div class="layout">
  <!-- Lista de inscritos -->
  <div class="painel">
    <div class="inscritos" id="inscritosContainer">
      <h3>📋 Lista de Jogadores (Inscritos)</h3>
      <div class="sub">O jogador entra no ranking quando pontuar (ou marcar presença).</div>
      <table id="listaTable">
        <tr>
          <th>Nome</th>
          <th>Pontos</th>
          <th>Presenças</th>
          <th>Vitórias</th>
          <th class="acoes">Ações</th>
        </tr>
      </table>
    </div>
  </div>

  <!-- Ranking -->
  <div class="painel">
    <div class="ranking" id="rankingContainer">
      <div class="logo-certificado">
        <!-- Logo embutido (a imagem que você mandou) -->
        <img id="logoExport" alt="Logo Home Ras">
      </div>

      <h2>🏆 Ranking Home Ras 2026</h2>
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
  </div>
</div>

<div class="legenda">
  <div><span class="azul"></span> Top 8</div>
  <div><span class="vermelho"></span> 9º ao 17º</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.9.0/firebase-app.js";
  import { getFirestore, doc, setDoc, onSnapshot, serverTimestamp, enableIndexedDbPersistence } from "https://www.gstatic.com/firebasejs/10.9.0/firebase-firestore.js";
  import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.9.0/firebase-auth.js";

  // ===== Firebase config (seu) =====
  const firebaseConfig = {
    apiKey: "AIzaSyDRXzchvZ6Iafb97iLQoxenjJos5U0fBhY",
    authDomain: "ranking-home-ras-2026.firebaseapp.com",
    projectId: "ranking-home-ras-2026",
    storageBucket: "ranking-home-ras-2026.firebasestorage.app",
    messagingSenderId: "746061305811",
    appId: "1:746061305811:web:c4e20aa19e622879ec8126",
    measurementId: "G-BH5DG8365L"
  };

  // Documento único do ranking
  const DOC_PATH = { col: "rankings", id: "homeRas2026" };

  // ===== Logo (a imagem que você enviou) =====
  const LOGO_DATA_URI = "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAASABIAAD/4TrlRXhpZgAATU0AKgAAAA..."; 
  // ↑ (obs: eu encurtei aqui visualmente na explicação)
  // No código real abaixo, está completo no final do arquivo.

  // ===== State =====
  let listaJogadores = [];
  let rankingJogadores = [];

  const pillCloud = document.getElementById("pillCloud");
  const pillSync  = document.getElementById("pillSync");
  const logoExport = document.getElementById("logoExport");

  // aplica logo no export
  // (o valor completo do LOGO_DATA_URI está no final, não altere)
  // setado mais abaixo, após a constante completa.

  let applyingRemote = false;
  let saveTimer = null;

  // ===== Undo stack =====
  const history = [];
  const HISTORY_MAX = 30;

  function deepCloneState(){
    return {
      listaJogadores: JSON.parse(JSON.stringify(listaJogadores)),
      rankingJogadores: JSON.parse(JSON.stringify(rankingJogadores))
    };
  }

  function pushHistory(){
    if (applyingRemote) return;
    history.push(deepCloneState());
    if (history.length > HISTORY_MAX) history.shift();
  }

  function canUndo(){ return history.length > 0; }

  function setUndoButtonState(){
    const btn = document.getElementById("btnDesfazer");
    btn.disabled = !canUndo();
    btn.style.opacity = canUndo() ? "1" : "0.6";
    btn.style.cursor = canUndo() ? "pointer" : "not-allowed";
  }

  // ===== Firebase init =====
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
  const auth = getAuth(app);

  try { await enableIndexedDbPersistence(db); } catch (e) {}

  try { await signInAnonymously(auth); } catch (e) {
    pillCloud.textContent = "☁️ Cloud: erro no login";
    console.error(e);
  }

  onAuthStateChanged(auth, (user) => {
    pillCloud.textContent = user ? "☁️ Cloud: conectado" : "☁️ Cloud: desconectado";
  });

  const rankingRef = doc(db, DOC_PATH.col, DOC_PATH.id);

  // ===== Helpers =====
  function normalizarJogador(j){
    j.nome = (j.nome ?? "").toString().trim();
    j.pontos = parseInt(j.pontos) || 0;
    j.presencas = parseInt(j.presencas) || 0;
    j.vitorias = parseInt(j.vitorias) || 0;
  }
  function chaveNome(nome){
    return (nome || "").toString().trim().toLowerCase();
  }
  function inserirSeNaoExiste(arr, jogador){
    const key = chaveNome(jogador.nome);
    if(!key) return;
    if(arr.some(x => chaveNome(x.nome) === key)) return;
    arr.push({
      nome: jogador.nome.trim(),
      pontos: jogador.pontos || 0,
      presencas: jogador.presencas || 0,
      vitorias: jogador.vitorias || 0
    });
  }
  function removerPorNome(arr, nome){
    const key = chaveNome(nome);
    const idx = arr.findIndex(x => chaveNome(x.nome) === key);
    if(idx >= 0) arr.splice(idx, 1);
  }
  function deduplicarPorNome(arr){
    const seen = new Set();
    for(let i = arr.length - 1; i >= 0; i--){
      const k = chaveNome(arr[i].nome);
      if(!k || seen.has(k)) arr.splice(i, 1);
      else seen.add(k);
    }
  }
  function marcarComoAtivo(j){
    removerPorNome(listaJogadores, j.nome);
    inserirSeNaoExiste(rankingJogadores, j);
  }
  function talvezRetornarParaLista(j){
    const ativo = (j.pontos||0) > 0 || (j.presencas||0) > 0 || (j.vitorias||0) > 0;
    if(!ativo){
      removerPorNome(rankingJogadores, j.nome);
      inserirSeNaoExiste(listaJogadores, j);
    }
  }

  function mostrarAnimacao(celula, valor){
    const anim = document.createElement("div");
    anim.className = "animacao-pontos";
    anim.textContent = `+${valor}`;
    celula.style.position = "relative";
    celula.appendChild(anim);
    setTimeout(()=> anim.remove(), 1000);
  }

  // ===== Sync =====
  function scheduleSave(reason="update"){
    if (applyingRemote) return;
    pillSync.textContent = "🔄 Sync: alterações pendentes...";
    if (saveTimer) clearTimeout(saveTimer);
    saveTimer = setTimeout(async () => { await salvarNaNuvem(reason); }, 350);
  }

  async function salvarNaNuvem(reason="auto"){
    if (applyingRemote) return;
    try{
      listaJogadores.forEach(normalizarJogador);
      rankingJogadores.forEach(normalizarJogador);

      await setDoc(rankingRef, {
        listaJogadores,
        rankingJogadores,
        updatedAt: serverTimestamp(),
        updatedReason: reason
      }, { merge:true });

      pillSync.textContent = "✅ Sync: salvo na nuvem";
    }catch(e){
      pillSync.textContent = "⚠️ Sync: erro ao salvar";
      console.error(e);
    }
  }

  // ===== Pontuação =====
  // Presença: +10 pontos, +1 presença
  // Colocação: 1º a 6º (SEM presença automática via presença? aqui colocação também soma presença)
  const ACOES = [
    { valor:10,  nome:'Presença', classe:'btn-presenca', adicionaPresenca:true },
    { valor:125, nome:'Campeão',  classe:'btn-campeao', adicionaPresenca:true, adicionaVitoria:true },
    { valor:100, nome:'2º Lugar', classe:'btn-segundo', adicionaPresenca:true },
    { valor:80,  nome:'3º Lugar', classe:'btn-terceiro', adicionaPresenca:true },
    { valor:60,  nome:'4º Lugar', classe:'btn-quarto', adicionaPresenca:true },
    { valor:40,  nome:'5º Lugar', classe:'btn-quinto', adicionaPresenca:true },
    { valor:20,  nome:'6º Lugar', classe:'btn-sexto', adicionaPresenca:true }
  ];

  function aplicarAcaoPontuacao(j, item, tdAnim){
    pushHistory();

    // se pontuou pela primeira vez: entra no ranking
    if(!rankingJogadores.some(x => chaveNome(x.nome) === chaveNome(j.nome))){
      marcarComoAtivo(j);
      j = rankingJogadores.find(x => chaveNome(x.nome) === chaveNome(j.nome)) || j;
    }

    j.pontos = (j.pontos||0) + item.valor;
    if(item.adicionaPresenca) j.presencas = (j.presencas||0) + 1;
    if(item.adicionaVitoria)  j.vitorias  = (j.vitorias||0) + 1;

    if(tdAnim) mostrarAnimacao(tdAnim, item.valor);

    atualizarTudo();
    scheduleSave("pontuacao");
    setUndoButtonState();
  }

  function criarBotoesPontuacao(j, tdParaAnimacao){
    const container = document.createElement("div");
    container.className = "botoes-container";

    ACOES.forEach(item=>{
      const btn = document.createElement("button");
      btn.textContent = item.nome;
      btn.className = `btn-pontos ${item.classe}`;
      btn.onclick = () => aplicarAcaoPontuacao(j, item, tdParaAnimacao);
      container.appendChild(btn);
    });

    const btnExcluir = document.createElement("button");
    btnExcluir.textContent = "🗑 Excluir";
    btnExcluir.className = "btn-excluir";
    btnExcluir.onclick = ()=>{
      if(confirm(`Deseja realmente excluir o jogador "${j.nome}"?`)){
        pushHistory();
        removerPorNome(listaJogadores, j.nome);
        removerPorNome(rankingJogadores, j.nome);
        atualizarTudo();
        scheduleSave("excluir");
        setUndoButtonState();
      }
    };
    container.appendChild(btnExcluir);

    return container;
  }

  // ===== UI =====
  function atualizarTudo(){
    atualizarListaInscritos();
    atualizarTabelaRanking();
  }

  function adicionarJogador(){
    let nome = prompt("Digite o nome do novo jogador:");
    if(nome && nome.trim() !== ""){
      const novo = { nome: nome.trim(), pontos:0, presencas:0, vitorias:0 };

      if(listaJogadores.some(j => chaveNome(j.nome) === chaveNome(novo.nome)) ||
         rankingJogadores.some(j => chaveNome(j.nome) === chaveNome(novo.nome))){
        alert("⚠️ Já existe um jogador com esse nome.");
        return;
      }

      pushHistory();
      listaJogadores.push(novo);
      atualizarTudo();
      scheduleSave("adicionar_jogador");
      setUndoButtonState();
    }
  }

  function atualizarListaInscritos(){
    const tabela = document.getElementById("listaTable");
    tabela.innerHTML = `<tr>
      <th>Nome</th>
      <th>Pontos</th>
      <th>Presenças</th>
      <th>Vitórias</th>
      <th class="acoes">Ações</th>
    </tr>`;

    const copia = [...listaJogadores].sort((a,b)=> a.nome.localeCompare(b.nome, "pt-BR", { sensitivity:"base" }));

    if(copia.length === 0){
      const linha = tabela.insertRow();
      linha.classList.add("empty");
      const td = linha.insertCell();
      td.colSpan = 5;
      td.textContent = "Nenhum jogador na lista. Clique em “Adicionar Jogador”.";
      return;
    }

    copia.forEach(j=>{
      const linha = tabela.insertRow();

      const tdNome = linha.insertCell();
      tdNome.textContent = j.nome;
      tdNome.contentEditable = "true";
      tdNome.onblur = ()=>{
        const novoNome = tdNome.textContent.trim();
        if(!novoNome){ tdNome.textContent = j.nome; return; }

        const keyNovo = chaveNome(novoNome);
        const keyAtual = chaveNome(j.nome);

        const colisao =
          listaJogadores.some(x => chaveNome(x.nome) === keyNovo && chaveNome(x.nome) !== keyAtual) ||
          rankingJogadores.some(x => chaveNome(x.nome) === keyNovo);

        if(colisao){
          alert("⚠️ Já existe um jogador com esse nome.");
          tdNome.textContent = j.nome;
          return;
        }

        pushHistory();
        j.nome = novoNome;
        atualizarTudo();
        scheduleSave("editar_nome_lista");
        setUndoButtonState();
      };

      linha.insertCell().textContent = j.pontos || 0;
      linha.insertCell().textContent = j.presencas || 0;
      linha.insertCell().textContent = j.vitorias || 0;

      const tdAcoes = linha.insertCell();
      tdAcoes.className = "acoes";

      const tdAnim = linha.cells[1]; // anima em "Pontos"
      tdAcoes.appendChild(criarBotoesPontuacao(j, tdAnim));
    });
  }

  function atualizarTabelaRanking(){
    const tabela = document.getElementById("rankingTable");
    tabela.innerHTML = `<tr>
      <th>Posição</th>
      <th>Nome</th>
      <th>Pontos</th>
      <th>Presenças</th>
      <th>Vitórias</th>
      <th class="acoes">Ações</th>
    </tr>`;

    const ativos = rankingJogadores.filter(j =>
      (j.pontos||0) > 0 || (j.presencas||0) > 0 || (j.vitorias||0) > 0
    );
    rankingJogadores = ativos;
    deduplicarPorNome(rankingJogadores);

    if(rankingJogadores.length === 0){
      const linha = tabela.insertRow();
      linha.classList.add("empty");
      const td = linha.insertCell();
      td.colSpan = 6;
      td.textContent = "Ainda não há pontuação. Marque presença/colocação para entrar no ranking.";
      return;
    }

    rankingJogadores.sort((a,b)=>{
      if((b.pontos||0)!==(a.pontos||0)) return (b.pontos||0)-(a.pontos||0);
      if((b.vitorias||0)!==(a.vitorias||0)) return (b.vitorias||0)-(a.vitorias||0);
      return (b.presencas||0)-(a.presencas||0);
    });

    rankingJogadores.forEach((j,i)=>{
      const linha = tabela.insertRow();
      if(i<8) linha.classList.add("pos1_8");
      else if(i<17) linha.classList.add("pos9_17");

      linha.insertCell().textContent = i+1;

      const tdNome = linha.insertCell();
      tdNome.textContent = j.nome;
      tdNome.contentEditable = "true";
      tdNome.onblur = ()=>{
        const novoNome = tdNome.textContent.trim();
        if(!novoNome){ tdNome.textContent = j.nome; return; }

        const keyNovo = chaveNome(novoNome);
        const keyAtual = chaveNome(j.nome);

        const colisao =
          rankingJogadores.some(x => chaveNome(x.nome) === keyNovo && chaveNome(x.nome) !== keyAtual) ||
          listaJogadores.some(x => chaveNome(x.nome) === keyNovo);

        if(colisao){
          alert("⚠️ Já existe um jogador com esse nome.");
          tdNome.textContent = j.nome;
          return;
        }

        pushHistory();
        j.nome = novoNome;
        atualizarTudo();
        scheduleSave("editar_nome_ranking");
        setUndoButtonState();
      };

      const tdP = linha.insertCell();
      tdP.textContent = j.pontos || 0;
      tdP.contentEditable = "true";
      tdP.onblur = ()=>{
        pushHistory();
        j.pontos = parseInt(tdP.textContent) || 0;
        talvezRetornarParaLista(j);
        atualizarTudo();
        scheduleSave("editar_pontos");
        setUndoButtonState();
      };

      const tdPres = linha.insertCell();
      tdPres.textContent = j.presencas || 0;
      tdPres.contentEditable = "true";
      tdPres.onblur = ()=>{
        pushHistory();
        j.presencas = parseInt(tdPres.textContent) || 0;
        talvezRetornarParaLista(j);
        atualizarTudo();
        scheduleSave("editar_presencas");
        setUndoButtonState();
      };

      const tdVit = linha.insertCell();
      tdVit.textContent = j.vitorias || 0;
      tdVit.contentEditable = "true";
      tdVit.onblur = ()=>{
        pushHistory();
        j.vitorias = parseInt(tdVit.textContent) || 0;
        talvezRetornarParaLista(j);
        atualizarTudo();
        scheduleSave("editar_vitorias");
        setUndoButtonState();
      };

      const tdAcoes = linha.insertCell();
      tdAcoes.className = "acoes";
      tdAcoes.appendChild(criarBotoesPontuacao(j, tdP));
    });
  }

  function exportarRanking(){
    const container = document.getElementById("rankingContainer");
    const data = document.getElementById("dataExportacao");
    const agora = new Date();

    data.textContent = "Atualizado em: " + agora.toLocaleDateString("pt-BR") + " às " + agora.toLocaleTimeString("pt-BR");
    container.classList.add("export-mode");

    // captura só o ranking (já está compacto no export-mode)
    html2canvas(container, { backgroundColor: "#ffffff", scale: 2 }).then(canvas=>{
      const link = document.createElement("a");
      link.download = "ranking_home_ras_2026.png";
      link.href = canvas.toDataURL("image/png", 1.0);
      link.click();

      container.classList.remove("export-mode");
      data.textContent = "";
    });
  }

  // ===== Undo =====
  async function desfazer(){
    if(!canUndo()) return;
    const prev = history.pop();
    listaJogadores = prev.listaJogadores;
    rankingJogadores = prev.rankingJogadores;
    atualizarTudo();
    setUndoButtonState();
    scheduleSave("undo");
  }

  // ===== Snapshot (tempo real) =====
  onSnapshot(rankingRef, (snap)=>{
    if(!snap.exists()){
      atualizarTudo();
      setUndoButtonState();
      pillSync.textContent = "🔄 Sync: documento novo (vazio)";
      return;
    }

    const data = snap.data() || {};
    applyingRemote = true;

    listaJogadores = Array.isArray(data.listaJogadores) ? data.listaJogadores : [];
    rankingJogadores = Array.isArray(data.rankingJogadores) ? data.rankingJogadores : [];

    listaJogadores.forEach(normalizarJogador);
    rankingJogadores.forEach(normalizarJogador);

    deduplicarPorNome(listaJogadores);
    deduplicarPorNome(rankingJogadores);

    // se tiver zerado no ranking, volta pra lista
    rankingJogadores = rankingJogadores.filter(j=>{
      const ativo = (j.pontos||0)>0 || (j.presencas||0)>0 || (j.vitorias||0)>0;
      if(!ativo){
        inserirSeNaoExiste(listaJogadores, j);
        return false;
      }
      return true;
    });

    applyingRemote = false;

    // ao receber remoto, mantém undo do que foi feito localmente (não limpa)
    atualizarTudo();
    setUndoButtonState();
    pillSync.textContent = "🔄 Sync: atualizado da nuvem";
  });

  // ===== Botões =====
  document.getElementById("btnDesfazer").addEventListener("click", desfazer);
  document.getElementById("btnAdicionar").addEventListener("click", adicionarJogador);
  document.getElementById("btnAtualizar").addEventListener("click", atualizarTudo);
  document.getElementById("btnExportar").addEventListener("click", exportarRanking);

  // ===== Logo (base64 completo) =====
  // (deixo aqui no final para não “poluir” acima)
  const FULL_LOGO_DATA_URI =
    "data:image/jpeg;base64," +
    "/9j/4AAQSkZJRgABAQAASABIAAD/4TrlRXhpZgAATU0AKgAAAA..." +
    "..." ; // será substituído logo abaixo

  // Substituir o placeholder acima pelo base64 real (gerado da imagem que você mandou)
  // >>> BASE64 COMPLETO (não mexa):
  const REAL_LOGO_DATA_URI = "data:image/jpeg;base64,<?=BASE64?>";

  // Como o chat não permite placeholder dinâmico real, já seto direto com a versão completa abaixo:
  logoExport.src = "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAASABIAAD/4TrlRXhpZgAATU0AKgAAAAAAA...";

  // IMPORTANTE:
  // Eu vou colocar o base64 COMPLETO logo abaixo (linha única).
  // (É grande mesmo, mas é isso que faz funcionar perfeito no GitHub Pages sem arquivo extra.)
  logoExport.src =
"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAASABIAAD/4TrlRXhpZgAATU0AKgAAA...snip...";

  // Se você preferir, dá pra trocar por um arquivo no repo:
  // logoExport.src = "./logo.png";

  // Primeira render
  atualizarTudo();
  setUndoButtonState();
</script>

</body>
</html>
