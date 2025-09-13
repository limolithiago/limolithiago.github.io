<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Ranking Piscine - Atualização Automática</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f5f5f5; display: flex; flex-direction: column; align-items: center; margin-top: 40px; }
    .ranking { background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); width: 750px; margin-bottom: 30px; }
    h2 { text-align: center; margin-bottom: 10px; color: #333; }
    .legenda { width: 750px; display: flex; justify-content: center; margin-bottom: 10px; gap: 20px; font-size: 14px; }
    .legenda div { display: flex; align-items: center; gap: 5px; }
    .legenda span { display: inline-block; width: 20px; height: 20px; border-radius: 3px; }
    .azul { background: #cce5ff; } .vermelho { background: #ffcccc; }
    table { width: 100%; border-collapse: collapse; }
    th, td { padding: 12px; text-align: center; border-bottom: 1px solid #ddd; }
    th { background-color: #333; color: white; }
    tr.pos1_8 td { background: #cce5ff; }
    tr.pos9_17 td { background: #ffcccc; }
    tr.empty td { color: #aaa; }
    tr:hover { background-color: #f1f1f1; }
  </style>
</head>
<body>
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
      </tr>
    </table>
  </div>

  <script>
    async function carregarJogadores() {
      try {
        const response = await fetch('jogadores.json');
        const jogadores = await response.json();
        atualizarTabela(jogadores);
      } catch (error) {
        console.error("Erro ao carregar jogadores:", error);
      }
    }

    function atualizarTabela(jogadores) {
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
      const ordenados = [...jogadores].sort((a,b)=>b.pontos-a.pontos);

      for(let i=0;i<27;i++){
        const linha = tabela.insertRow();
        if(i < ordenados.length){
          const j = ordenados[i];
          linha.insertCell().textContent = i+1;
          linha.insertCell().textContent = j.nome;
          linha.insertCell().textContent = j.pontos;
          linha.insertCell().textContent = j.presencas;
          linha.insertCell().textContent = j.vitorias;

          if(i<8) linha.classList.add("pos1_8");
          else if(i<17) linha.classList.add("pos9_17");
        } else {
          linha.classList.add("empty");
          linha.insertCell().textContent = i+1;
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
          linha.insertCell().textContent = "-";
        }
      }
    }

    // Atualiza automaticamente a cada 10 segundos
    carregarJogadores();
    setInterval(carregarJogadores, 10000);
  </script>
</body>
</html>
