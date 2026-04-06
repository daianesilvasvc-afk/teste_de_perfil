<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Seleção SDR — Podium Educação</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #111;
    --white: #fafaf8;
    --gray-100: #f4f3f0;
    --gray-200: #e8e7e2;
    --gray-400: #999890;
    --gray-600: #666560;
    --green: #1a5c38;
    --green-light: #d4eddf;
    --amber: #7a4d00;
    --amber-light: #fdecc8;
    --red: #8b1a1a;
    --red-light: #fde8e8;
    --accent: #c8430a;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'DM Sans', sans-serif; background: var(--white); color: var(--black); min-height: 100vh; }

  nav {
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 32px; border-bottom: 1px solid var(--gray-200);
    background: var(--white); position: sticky; top: 0; z-index: 100;
  }
  .nav-brand { font-family: 'DM Serif Display', serif; font-size: 18px; letter-spacing: -0.3px; }
  .nav-brand span { color: var(--accent); }
  .nav-tabs { display: flex; gap: 4px; }
  .tab-btn {
    font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 400;
    padding: 7px 16px; border: 1px solid transparent; border-radius: 20px;
    cursor: pointer; background: transparent; color: var(--gray-600); transition: all 0.15s;
  }
  .tab-btn.active { background: var(--black); color: var(--white); border-color: var(--black); }
  .tab-btn:not(.active):hover { border-color: var(--gray-200); color: var(--black); }

  .page { display: none; }
  .page.active { display: block; }

  /* CANDIDATO */
  .test-wrap { max-width: 640px; margin: 0 auto; padding: 48px 24px 80px; }
  .test-header { margin-bottom: 40px; }
  .test-header h1 { font-family: 'DM Serif Display', serif; font-size: 32px; line-height: 1.2; margin-bottom: 10px; }
  .test-header p { font-size: 15px; color: var(--gray-600); line-height: 1.7; }

  .progress-bar-wrap { margin-bottom: 36px; }
  .progress-label { display: flex; justify-content: space-between; font-size: 12px; color: var(--gray-400); margin-bottom: 8px; }
  .progress-track { height: 3px; background: var(--gray-200); border-radius: 2px; }
  .progress-fill { height: 3px; background: var(--accent); border-radius: 2px; width: 0%; transition: width 0.4s ease; }

  .step { display: none; }
  .step.active { display: block; }

  .info-card { background: var(--gray-100); border-radius: 12px; padding: 28px; margin-bottom: 24px; }
  .info-card h2 { font-family: 'DM Serif Display', serif; font-size: 22px; margin-bottom: 6px; }
  .info-card p { font-size: 14px; color: var(--gray-600); line-height: 1.7; }

  .field-group { margin-bottom: 18px; }
  .field-group label { display: block; font-size: 13px; font-weight: 500; margin-bottom: 6px; }
  .field-group input {
    width: 100%; padding: 11px 14px; border: 1px solid var(--gray-200);
    border-radius: 8px; font-family: 'DM Sans', sans-serif; font-size: 14px;
    background: var(--white); color: var(--black); transition: border-color 0.15s;
  }
  .field-group input:focus { outline: none; border-color: var(--black); }

  .q-block { margin-bottom: 36px; }
  .q-section-tag {
    display: inline-block; font-size: 11px; font-weight: 500;
    letter-spacing: 0.07em; text-transform: uppercase; color: var(--accent); margin-bottom: 20px;
  }
  .q-title { font-family: 'DM Serif Display', serif; font-size: 21px; line-height: 1.35; margin-bottom: 18px; }
  .q-subtitle { font-size: 13px; color: var(--gray-600); margin-bottom: 18px; margin-top: -10px; }

  .options-grid { display: flex; flex-direction: column; gap: 8px; }
  .opt-btn {
    display: flex; align-items: flex-start; gap: 12px; padding: 14px 16px;
    border: 1px solid var(--gray-200); border-radius: 10px; cursor: pointer;
    background: var(--white); text-align: left; font-family: 'DM Sans', sans-serif;
    font-size: 14px; color: var(--black); line-height: 1.5; transition: all 0.12s;
  }
  .opt-btn:hover { border-color: var(--black); }
  .opt-btn.selected { border-color: var(--black); background: var(--black); color: var(--white); }
  .opt-letter { font-size: 11px; font-weight: 500; color: var(--gray-400); min-width: 18px; padding-top: 1px; }
  .opt-btn.selected .opt-letter { color: var(--gray-400); }

  .scale-wrap { padding: 8px 0; }
  .scale-labels { display: flex; justify-content: space-between; font-size: 12px; color: var(--gray-400); margin-bottom: 10px; }
  .scale-options { display: flex; gap: 8px; }
  .scale-opt {
    flex: 1; height: 44px; border: 1px solid var(--gray-200); border-radius: 8px;
    cursor: pointer; background: var(--white); font-family: 'DM Sans', sans-serif;
    font-size: 14px; font-weight: 500; color: var(--gray-600); transition: all 0.12s;
  }
  .scale-opt:hover { border-color: var(--black); color: var(--black); }
  .scale-opt.selected { background: var(--black); color: var(--white); border-color: var(--black); }

  .q-textarea {
    width: 100%; min-height: 120px; padding: 14px; border: 1px solid var(--gray-200);
    border-radius: 10px; font-family: 'DM Sans', sans-serif; font-size: 14px;
    color: var(--black); line-height: 1.6; resize: vertical; background: var(--white); transition: border-color 0.15s;
  }
  .q-textarea:focus { outline: none; border-color: var(--black); }

  .btn-row { display: flex; gap: 10px; justify-content: space-between; margin-top: 32px; align-items: center; }
  .btn-primary {
    padding: 13px 28px; background: var(--black); color: var(--white); border: none;
    border-radius: 8px; font-family: 'DM Sans', sans-serif; font-size: 14px;
    font-weight: 500; cursor: pointer; transition: opacity 0.15s;
  }
  .btn-primary:hover { opacity: 0.85; }
  .btn-back {
    padding: 13px 20px; background: transparent; color: var(--gray-600);
    border: 1px solid var(--gray-200); border-radius: 8px; font-family: 'DM Sans', sans-serif;
    font-size: 14px; cursor: pointer; transition: all 0.15s;
  }
  .btn-back:hover { border-color: var(--black); color: var(--black); }
  .required-note { font-size: 12px; color: var(--red); margin-top: 8px; display: none; }

  .success-wrap { text-align: center; padding: 60px 0; }
  .success-icon { font-size: 48px; margin-bottom: 20px; }
  .success-wrap h2 { font-family: 'DM Serif Display', serif; font-size: 28px; margin-bottom: 10px; }
  .success-wrap p { font-size: 15px; color: var(--gray-600); line-height: 1.7; }

  /* PAINEL */
  .painel-wrap { padding: 40px 32px; max-width: 1100px; margin: 0 auto; }
  .painel-top { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 32px; flex-wrap: wrap; gap: 16px; }
  .painel-top h2 { font-family: 'DM Serif Display', serif; font-size: 26px; }
  .painel-top p { font-size: 14px; color: var(--gray-600); margin-top: 4px; }

  .stats-row { display: flex; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
  .stat-card { background: var(--gray-100); border-radius: 10px; padding: 16px 20px; min-width: 140px; }
  .stat-label { font-size: 12px; color: var(--gray-600); margin-bottom: 4px; }
  .stat-num { font-family: 'DM Serif Display', serif; font-size: 28px; }
  .stat-num.green { color: var(--green); }
  .stat-num.amber { color: var(--amber); }
  .stat-num.red { color: var(--red); }

  .filter-row { display: flex; gap: 8px; margin-bottom: 20px; flex-wrap: wrap; }
  .filter-btn {
    padding: 6px 14px; border: 1px solid var(--gray-200); border-radius: 20px;
    font-family: 'DM Sans', sans-serif; font-size: 12px; cursor: pointer;
    background: var(--white); color: var(--gray-600); transition: all 0.12s;
  }
  .filter-btn.active { background: var(--black); color: var(--white); border-color: var(--black); }

  .candidatos-table { width: 100%; border-collapse: collapse; }
  .candidatos-table th {
    text-align: left; font-size: 11px; font-weight: 500; color: var(--gray-400);
    text-transform: uppercase; letter-spacing: 0.06em; padding: 10px 12px;
    border-bottom: 1px solid var(--gray-200);
  }
  .candidatos-table td { padding: 14px 12px; font-size: 14px; border-bottom: 1px solid var(--gray-200); vertical-align: top; }
  .candidatos-table tr:hover td { background: var(--gray-100); }

  .status-pill { display: inline-block; font-size: 11px; font-weight: 500; padding: 3px 10px; border-radius: 20px; }
  .pill-avancar { background: var(--green-light); color: var(--green); }
  .pill-reserva { background: var(--amber-light); color: var(--amber); }
  .pill-eliminar { background: var(--red-light); color: var(--red); }
  .pill-pendente { background: var(--gray-200); color: var(--gray-600); }

  /* alertas de sinal no painel */
  .flag { display: inline-block; font-size: 10px; font-weight: 500; padding: 2px 7px; border-radius: 10px; margin-left: 4px; }
  .flag-red { background: var(--red-light); color: var(--red); }
  .flag-amber { background: var(--amber-light); color: var(--amber); }

  .pts-bar-wrap { display: flex; align-items: center; gap: 8px; }
  .pts-bar-track { flex: 1; height: 4px; background: var(--gray-200); border-radius: 2px; min-width: 60px; }
  .pts-bar-fill { height: 4px; border-radius: 2px; background: var(--accent); }

  .ver-btn {
    font-size: 12px; padding: 5px 12px; border: 1px solid var(--gray-200);
    border-radius: 6px; background: transparent; cursor: pointer;
    font-family: 'DM Sans', sans-serif; color: var(--black); transition: all 0.12s;
  }
  .ver-btn:hover { background: var(--black); color: var(--white); border-color: var(--black); }
  .empty-state { text-align: center; padding: 60px 0; color: var(--gray-400); font-size: 14px; }

  /* MODAL */
  .modal-overlay {
    display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.5);
    z-index: 200; overflow-y: auto; padding: 40px 20px;
  }
  .modal-overlay.open { display: flex; align-items: flex-start; justify-content: center; }
  .modal-box { background: var(--white); border-radius: 14px; padding: 32px; max-width: 660px; width: 100%; }
  .modal-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 24px; }
  .modal-header h3 { font-family: 'DM Serif Display', serif; font-size: 22px; }
  .modal-close { background: none; border: none; font-size: 22px; cursor: pointer; color: var(--gray-400); line-height: 1; }
  .modal-score { display: flex; align-items: center; gap: 12px; margin-bottom: 24px; padding-bottom: 24px; border-bottom: 1px solid var(--gray-200); }
  .modal-score-num { font-family: 'DM Serif Display', serif; font-size: 40px; }
  .modal-score-sub { font-size: 13px; color: var(--gray-600); }
  .modal-section { margin-bottom: 20px; }
  .modal-section-title { font-size: 11px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.07em; color: var(--gray-400); margin-bottom: 10px; }
  .modal-qa { margin-bottom: 14px; padding-bottom: 14px; border-bottom: 1px solid var(--gray-200); }
  .modal-qa:last-child { border-bottom: none; }
  .modal-q { font-size: 13px; font-weight: 500; margin-bottom: 4px; }
  .modal-a { font-size: 13px; color: var(--gray-600); line-height: 1.6; }
  .modal-pts { font-size: 11px; color: var(--accent); margin-left: 6px; }
  .modal-flag { font-size: 11px; font-weight: 500; padding: 2px 8px; border-radius: 10px; margin-left: 6px; }

  /* alerta de momento de vida no modal */
  .alerta-box {
    background: var(--amber-light); border-radius: 8px; padding: 12px 16px;
    margin-bottom: 20px; font-size: 13px; color: var(--amber); line-height: 1.6;
  }
  .alerta-box strong { display: block; margin-bottom: 4px; }

  .nota-input {
    width: 100%; min-height: 80px; padding: 10px 12px; border: 1px solid var(--gray-200);
    border-radius: 8px; font-family: 'DM Sans', sans-serif; font-size: 13px; resize: vertical; margin-top: 6px;
  }
  .nota-input:focus { outline: none; border-color: var(--black); }
  .save-nota-btn {
    margin-top: 8px; padding: 8px 18px; background: var(--black); color: var(--white);
    border: none; border-radius: 6px; font-family: 'DM Sans', sans-serif; font-size: 13px; cursor: pointer;
  }
  .score-override { display: flex; align-items: center; gap: 10px; margin-top: 8px; }
  .score-override label { font-size: 13px; color: var(--gray-600); }
  .score-override input[type=number] {
    width: 70px; padding: 6px 10px; border: 1px solid var(--gray-200);
    border-radius: 6px; font-family: 'DM Sans', sans-serif; font-size: 13px;
  }

  /* guia de avaliação */
  .guia-box { background: var(--gray-100); border-radius: 10px; padding: 16px; margin-top: 16px; }
  .guia-title { font-size: 11px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.06em; color: var(--gray-400); margin-bottom: 10px; }
  .guia-item { font-size: 12px; color: var(--gray-600); margin-bottom: 6px; line-height: 1.5; }
  .guia-item strong { color: var(--black); }

  @media (max-width: 600px) {
    nav { padding: 14px 16px; }
    .painel-wrap { padding: 24px 16px; }
    .candidatos-table th:nth-child(3), .candidatos-table td:nth-child(3) { display: none; }
  }
</style>
</head>
<body>

<nav>
  <div class="nav-brand">Podium <span>Educação</span></div>
  <div class="nav-tabs">
    <button class="tab-btn active" onclick="showPage('candidato', event)">Teste</button>
    <button class="tab-btn" onclick="showPage('painel', event)">Painel</button>
  </div>
</nav>

<!-- CANDIDATO -->
<div id="page-candidato" class="page active">
  <div class="test-wrap">
    <div id="step-intro" class="step active">
      <div class="test-header">
        <h1>Seleção de SDR</h1>
        <p>Antes de avançar para a entrevista, queremos entender melhor o seu perfil. Responda com sinceridade — não existe resposta certa ou errada, e respostas honestas funcionam melhor pra todo mundo.</p>
      </div>
      <div class="info-card">
        <h2>Como funciona a vaga</h2>
        <p>Você terá um salário fixo de R$4.000 e bônus por agendamentos realizados. A autonomia de horário é total — mas o que importa é resultado. Quem entrega mais, ganha mais.</p>
      </div>
      <div class="field-group"><label>Nome completo</label><input type="text" id="nome" placeholder="Seu nome" /></div>
      <div class="field-group"><label>WhatsApp</label><input type="tel" id="telefone" placeholder="(00) 00000-0000" /></div>
      <div class="field-group"><label>Como ficou sabendo da vaga?</label><input type="text" id="origem" placeholder="Ex: indicação, Instagram, grupo..." /></div>
      <div class="btn-row"><div></div><button class="btn-primary" onclick="startTest()">Começar →</button></div>
    </div>

    <div id="step-questions" class="step">
      <div class="progress-bar-wrap">
        <div class="progress-label">
          <span id="prog-text">Pergunta 1 de 20</span>
          <span id="prog-pct">0%</span>
        </div>
        <div class="progress-track"><div class="progress-fill" id="prog-fill"></div></div>
      </div>
      <div id="question-container"></div>
      <p class="required-note" id="req-note">Por favor, responda antes de continuar.</p>
      <div class="btn-row">
        <button class="btn-back" id="btn-back" onclick="prevQ()">← Voltar</button>
        <button class="btn-primary" id="btn-next" onclick="nextQ()">Continuar →</button>
      </div>
    </div>

    <div id="step-success" class="step">
      <div class="success-wrap">
        <div class="success-icon">✓</div>
        <h2>Teste enviado!</h2>
        <p>Obrigado pela participação.<br>Entraremos em contato pelo WhatsApp em breve.</p>
      </div>
    </div>
  </div>
</div>

<!-- PAINEL -->
<div id="page-painel" class="page">
  <div class="painel-wrap">
    <div class="painel-top">
      <div><h2>Candidatos</h2><p>Resultado do teste de perfil SDR</p></div>
      <button class="btn-primary" onclick="exportCSV()">Exportar CSV</button>
    </div>
    <div class="stats-row">
      <div class="stat-card"><div class="stat-label">Total</div><div class="stat-num" id="stat-total">0</div></div>
      <div class="stat-card"><div class="stat-label">Avançar</div><div class="stat-num green" id="stat-avancar">0</div></div>
      <div class="stat-card"><div class="stat-label">Reserva</div><div class="stat-num amber" id="stat-reserva">0</div></div>
      <div class="stat-card"><div class="stat-label">Eliminar</div><div class="stat-num red" id="stat-eliminar">0</div></div>
      <div class="stat-card"><div class="stat-label">Sinal de alerta</div><div class="stat-num amber" id="stat-flags">0</div></div>
    </div>
    <div class="filter-row">
      <button class="filter-btn active" onclick="setFilter('todos',this)">Todos</button>
      <button class="filter-btn" onclick="setFilter('avancar',this)">Avançar</button>
      <button class="filter-btn" onclick="setFilter('reserva',this)">Reserva</button>
      <button class="filter-btn" onclick="setFilter('eliminar',this)">Eliminar</button>
      <button class="filter-btn" onclick="setFilter('pendente',this)">Pendente</button>
      <button class="filter-btn" onclick="setFilter('flag',this)">Com alerta</button>
    </div>
    <div id="tabela-container"><div class="empty-state">Nenhum candidato ainda. Compartilhe o link da aba "Teste".</div></div>
  </div>
</div>

<!-- MODAL -->
<div class="modal-overlay" id="modal" onclick="closeModalOutside(event)">
  <div class="modal-box" id="modal-box">
    <div class="modal-header">
      <h3 id="modal-nome">—</h3>
      <button class="modal-close" onclick="closeModal()">×</button>
    </div>
    <div class="modal-score">
      <div>
        <div class="modal-score-num" id="modal-pts">—</div>
        <div class="modal-score-sub">pontos automáticos (máx 40)</div>
      </div>
      <div style="flex:1">
        <div id="modal-status-pill"></div>
        <div style="margin-top:8px;font-size:13px;color:var(--gray-600)" id="modal-info"></div>
      </div>
    </div>
    <div id="modal-alerta"></div>
    <div id="modal-content"></div>
    <div class="modal-section" style="margin-top:24px;padding-top:20px;border-top:1px solid var(--gray-200)">
      <div class="modal-section-title">Sua avaliação das respostas abertas (0–25 pts)</div>
      <div class="guia-box">
        <div class="guia-title">Critério de avaliação</div>
        <div class="guia-item"><strong>P11 (0–5):</strong> Episódio real + motivação interna (orgulho/resultado) = 5 · Motivação externa (medo) = 3 · Sem episódio concreto = 0</div>
        <div class="guia-item"><strong>P12 (0–5):</strong> Cita dinheiro, competição, desafio, bater meta = 5 · Resposta genérica = 2 · Não sabe/desvia = 0</div>
        <div class="guia-item"><strong>P13 (0–5):</strong> Exp. real com comissão e fala bem = 5 · Sem exp. mas contexto positivo = 3 · Prefere fixo ou fala mal = 1</div>
        <div class="guia-item"><strong>P14 (0–5):</strong> Ponto fraco real + como lida = 5 · Fraqueza disfarçada de qualidade = 1 · Vago = 2</div>
        <div class="guia-item"><strong>P15 (0–5):</strong> Palavras: determinado, competitivo, focado, ambicioso = 5 · Neutro: organizado, responsável = 3 · Tranquilo, calmo, equilibrado = 1</div>
      </div>
      <div class="score-override">
        <label>Pontos das abertas:</label>
        <input type="number" id="override-input" min="0" max="25" placeholder="0–25" />
      </div>
      <textarea class="nota-input" id="nota-input" placeholder="Suas anotações sobre o candidato..."></textarea>
      <button class="save-nota-btn" onclick="saveNota()">Salvar avaliação</button>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════════════
// BANCO DE PERGUNTAS — 20 PERGUNTAS
// Distribuição:
//   1–5   Cenários de resultado (choice, automático)
//   6–10  Escala de valores e drive (scale, automático)
//   11–15 Perguntas abertas de perfil (open, manual)
//   16–20 Perguntas indiretas de momento de vida (choice/scale, automático + flag)
// ══════════════════════════════════════════
const questions = [

  // ── BLOCO 1: CENÁRIOS (choice, pts automático) ──
  {
    id: 1, section: 'Cenários', type: 'choice',
    text: 'São 18h30 de sexta. Você bateu apenas 60% da meta de agendamentos da semana. Ninguém vai te cobrar. O que você faz?',
    options: [
      { letter: 'A', text: 'Fico além do horário e continuo prospectando até chegar num número que me satisfaz', pts: 3 },
      { letter: 'B', text: 'Fecho o dia, mas já planejo segunda com foco em recuperar', pts: 2 },
      { letter: 'C', text: 'Registro o que deu errado e ajusto a abordagem para a próxima semana', pts: 1 },
      { letter: 'D', text: 'Foi uma semana difícil — descanso e reinicio fresquinho na segunda', pts: 0 },
    ]
  },
  {
    id: 2, section: 'Cenários', type: 'choice',
    text: 'Você já bateu sua meta da semana na quinta-feira. Ainda tem sexta inteira pela frente. O que acontece?',
    options: [
      { letter: 'A', text: 'Continuo prospectando — meta batida é piso, não teto', pts: 3 },
      { letter: 'B', text: 'Faço um dia mais leve mas ainda trabalho', pts: 2 },
      { letter: 'C', text: 'Aproveito para organizar processos e me preparar para a próxima semana', pts: 1 },
      { letter: 'D', text: 'Dou o dia como encerrado — mereci', pts: 0 },
    ]
  },
  {
    id: 3, section: 'Cenários', type: 'choice',
    text: 'Você está prospectando no WhatsApp e uma pessoa te ignora por dois dias seguidos. O que você faz?',
    options: [
      { letter: 'A', text: 'Mando follow-up com abordagem completamente diferente — mudo o ângulo da mensagem', pts: 3 },
      { letter: 'B', text: 'Espero mais um dia e mando um lembrete simples', pts: 2 },
      { letter: 'C', text: 'Marco como inativo e parto para o próximo lead', pts: 1 },
      { letter: 'D', text: 'Entendo que não é o momento e não insisto mais', pts: 0 },
    ]
  },
  {
    id: 4, section: 'Cenários', type: 'choice',
    text: 'Você tem autonomia total de horário. Como costuma estruturar o seu dia de trabalho?',
    options: [
      { letter: 'A', text: 'Monto blocos fixos de prospecção e cumpro sem negociar comigo mesmo', pts: 3 },
      { letter: 'B', text: 'Sigo o horário comercial padrão com organização conforme o dia pede', pts: 2 },
      { letter: 'C', text: 'Trabalho quando me sinto mais produtivo — varia bastante', pts: 1 },
      { letter: 'D', text: 'Não tenho rotina definida, vou conforme as demandas aparecem', pts: 0 },
    ]
  },
  {
    id: 5, section: 'Cenários', type: 'choice',
    text: 'Você está num mês em que o bônus está distante da meta. Faltam 5 dias. O que muda no seu comportamento?',
    options: [
      { letter: 'A', text: 'Aumento o volume e o horário — faço o que for preciso para chegar mais perto', pts: 3 },
      { letter: 'B', text: 'Mantenho o ritmo mas com foco maior nas ações que convertem mais', pts: 2 },
      { letter: 'C', text: 'Aceito que esse mês não vai fechar — foco em aprender para o próximo', pts: 1 },
      { letter: 'D', text: 'O fixo já garante o básico — não vale se estressar', pts: 0 },
    ]
  },

  // ── BLOCO 2: ESCALA DE VALORES (scale, pts automático) ──
  {
    id: 6, section: 'Valores', type: 'scale',
    text: '"Bater uma meta me dá uma satisfação que vai além do dinheiro — é quase uma questão de orgulho."',
  },
  {
    id: 7, section: 'Valores', type: 'scale',
    text: '"Me incomoda profundamente terminar o dia sem ter entregado o que planejei."',
  },
  {
    id: 8, section: 'Valores', type: 'scale',
    text: '"Já fui além do que era exigido em algum trabalho ou projeto por conta própria, sem ninguém pedir."',
  },
  {
    id: 9, section: 'Valores', type: 'scale',
    text: '"Consigo manter o mesmo ritmo de trabalho nos dias em que ninguém está me monitorando."',
  },
  {
    id: 10, section: 'Valores', type: 'scale',
    text: '"Quando vejo alguém da equipe entregando mais do que eu, isso me incomoda e me motiva a reagir."',
  },

  // ── BLOCO 3: ABERTAS DE PERFIL (open, avaliação manual) ──
  {
    id: 11, section: 'Perfil', type: 'open',
    text: 'Descreva um momento em que você trabalhou além do esperado para entregar algo. O que te motivou a não parar?',
    hint: 'Pode ser qualquer contexto — trabalho, estudo, projeto pessoal.'
  },
  {
    id: 12, section: 'Perfil', type: 'open',
    text: 'O que te faz sair da cama com vontade de trabalhar num dia em que a agenda está vazia e ninguém vai te cobrar?',
    hint: 'Sem resposta certa — seja honesto.'
  },
  {
    id: 13, section: 'Perfil', type: 'open',
    text: 'Você já trabalhou com comissão, bônus ou por entrega? Como foi essa experiência para você?',
    hint: 'Se não tiver experiência, conta como imagina que seria.'
  },
  {
    id: 14, section: 'Perfil', type: 'open',
    text: 'Qual é o seu maior ponto fraco quando o assunto é trabalho?',
    hint: 'Seja direto — resposta genérica não ajuda ninguém aqui.'
  },
  {
    id: 15, section: 'Perfil', type: 'open',
    text: 'Em 3 palavras, como pessoas próximas descreveriam você no trabalho?',
    hint: 'Amigos, família, ex-colegas — qualquer pessoa que te conheça bem.'
  },

  // ── BLOCO 4: MOMENTO DE VIDA (indireto, flag automático) ──
  {
    id: 16, section: 'Momento atual', type: 'choice',
    text: 'Como você descreveria sua situação financeira pessoal agora?',
    hint: 'Isso nos ajuda a entender se a estrutura da vaga faz sentido pra você nesse momento.',
    options: [
      { letter: 'A', text: 'Estável — tenho reserva e não dependo do salário para cobrir emergências', pts: 3, flag: false },
      { letter: 'B', text: 'Equilibrada — o salário cobre bem meus gastos com alguma folga', pts: 2, flag: false },
      { letter: 'C', text: 'Apertada — o salário vai cobrir o necessário mas sem margem', pts: 1, flag: true },
      { letter: 'D', text: 'Crítica — tenho dívidas ou pressão financeira alta no momento', pts: 0, flag: true },
    ]
  },
  {
    id: 17, section: 'Momento atual', type: 'choice',
    text: 'Como está sua energia e disposição para trabalhar agora, comparado com seus melhores momentos profissionais?',
    options: [
      { letter: 'A', text: 'Estou num dos meus melhores momentos — animado e com tudo a dar', pts: 3, flag: false },
      { letter: 'B', text: 'Estou bem — com vontade de crescer e provar algo', pts: 2, flag: false },
      { letter: 'C', text: 'Estou ok — saí de um período difícil e estou me recuperando', pts: 1, flag: true },
      { letter: 'D', text: 'Estou cansado — preciso de uma vaga que me reequilibre', pts: 0, flag: true },
    ]
  },
  {
    id: 18, section: 'Momento atual', type: 'choice',
    text: 'Tem alguma situação pessoal (família, saúde, mudança) que pode impactar sua disponibilidade nos próximos 3 meses?',
    options: [
      { letter: 'A', text: 'Não — estou 100% disponível e focado', pts: 3, flag: false },
      { letter: 'B', text: 'Tenho algo pontual mas que não vai interferir no trabalho', pts: 2, flag: false },
      { letter: 'C', text: 'Tenho algo que pode exigir atenção ocasional', pts: 1, flag: true },
      { letter: 'D', text: 'Tenho uma situação relevante que precisa de atenção', pts: 0, flag: true },
    ]
  },
  {
    id: 19, section: 'Momento atual', type: 'scale',
    text: '"Neste momento da minha vida, estou disposto a abrir mão de conforto e lazer para focar em crescer profissionalmente."',
    flagBelow: 3
  },
  {
    id: 20, section: 'Momento atual', type: 'scale',
    text: '"Estou entrando nessa vaga com a mentalidade de construir algo — não apenas de cumprir horário."',
    flagBelow: 3
  },
];

// ══════════════════════
// STATE
// ══════════════════════
let currentQ = 0;
let answers = {};
let candidatoInfo = {};
let activeFilter = 'todos';
let modalIndex = null;

function getKey() { return 'podium_sdrs_v3'; }
function getCandidatos() { try { return JSON.parse(localStorage.getItem(getKey()) || '[]'); } catch { return []; } }
function saveCandidatos(list) { localStorage.setItem(getKey(), JSON.stringify(list)); }

// ══════════════════════
// NAVEGAÇÃO
// ══════════════════════
function showPage(page, evt) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('page-' + page).classList.add('active');
  if (evt && evt.target) evt.target.classList.add('active');
  if (page === 'painel') renderPainel();
}

function showStep(id) {
  document.querySelectorAll('.step').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// ══════════════════════
// TESTE
// ══════════════════════
function startTest() {
  const nome = document.getElementById('nome').value.trim();
  const tel = document.getElementById('telefone').value.trim();
  if (!nome || !tel) { alert('Preencha nome e WhatsApp para continuar.'); return; }
  candidatoInfo = { nome, telefone: tel, origem: document.getElementById('origem').value.trim() };
  currentQ = 0; answers = {};
  showStep('step-questions');
  renderQuestion();
}

function renderQuestion() {
  const q = questions[currentQ];
  document.getElementById('req-note').style.display = 'none';
  const pct = Math.round((currentQ / questions.length) * 100);
  document.getElementById('prog-text').textContent = `Pergunta ${currentQ + 1} de ${questions.length}`;
  document.getElementById('prog-pct').textContent = pct + '%';
  document.getElementById('prog-fill').style.width = pct + '%';
  document.getElementById('btn-back').style.display = currentQ === 0 ? 'none' : '';

  let html = `<div class="q-block">
    <div class="q-section-tag">${q.section}</div>
    <div class="q-title">${q.text}</div>`;
  if (q.hint) html += `<div class="q-subtitle">${q.hint}</div>`;

  if (q.type === 'choice') {
    html += `<div class="options-grid">`;
    q.options.forEach((opt, i) => {
      const sel = answers[q.id] === i ? 'selected' : '';
      html += `<button class="opt-btn ${sel}" onclick="selectOpt(${i})">
        <span class="opt-letter">${opt.letter}</span><span>${opt.text}</span>
      </button>`;
    });
    html += `</div>`;
  } else if (q.type === 'scale') {
    const cur = answers[q.id];
    html += `<div class="scale-wrap">
      <div class="scale-labels"><span>Discordo totalmente</span><span>Concordo totalmente</span></div>
      <div class="scale-options">`;
    [1,2,3,4,5].forEach(v => {
      const sel = cur === v ? 'selected' : '';
      html += `<button class="scale-opt ${sel}" onclick="selectScale(${v})">${v}</button>`;
    });
    html += `</div></div>`;
  } else {
    const val = answers[q.id] || '';
    html += `<textarea class="q-textarea" id="ta-${q.id}" placeholder="Escreva aqui..." oninput="answers[${q.id}]=this.value">${val}</textarea>`;
  }

  html += `</div>`;
  document.getElementById('question-container').innerHTML = html;
}

function selectOpt(i) { answers[questions[currentQ].id] = i; renderQuestion(); }
function selectScale(v) { answers[questions[currentQ].id] = v; renderQuestion(); }
function prevQ() { if (currentQ > 0) { currentQ--; renderQuestion(); } }

function nextQ() {
  const q = questions[currentQ];
  const hasAnswer = answers[q.id] !== undefined && answers[q.id] !== '';
  if (!hasAnswer) { document.getElementById('req-note').style.display = 'block'; return; }
  if (currentQ < questions.length - 1) { currentQ++; renderQuestion(); }
  else submitTest();
}

// ══════════════════════
// PONTUAÇÃO
// ══════════════════════
function calcAutoScore() {
  let pts = 0;
  questions.forEach(q => {
    const ans = answers[q.id];
    if (q.type === 'choice' && ans !== undefined) pts += (q.options[ans].pts || 0);
    else if (q.type === 'scale' && ans !== undefined) pts += ans;
  });
  return pts;
}

function detectFlags(answersObj) {
  const flags = [];
  // P16 — situação financeira crítica
  const p16 = answersObj[16];
  if (p16 !== undefined && questions[15].options[p16].flag) flags.push('Situação financeira pode gerar pressão ou distração');
  // P17 — energia baixa
  const p17 = answersObj[17];
  if (p17 !== undefined && questions[16].options[p17].flag) flags.push('Momento de energia baixa — pode impactar ritmo inicial');
  // P18 — disponibilidade comprometida
  const p18 = answersObj[18];
  if (p18 !== undefined && questions[17].options[p18].flag) flags.push('Situação pessoal pode comprometer disponibilidade');
  // P19 — escala baixa
  if (answersObj[19] !== undefined && answersObj[19] < 3) flags.push('Baixa disposição declarada para abrir mão de conforto');
  // P20 — escala baixa
  if (answersObj[20] !== undefined && answersObj[20] < 3) flags.push('Não demonstra mentalidade de construção — risco de acomodação');
  return flags;
}

function getStatus(auto, manual) {
  const total = auto + (manual || 0);
  if (manual === null || manual === undefined) return 'pendente';
  if (total >= 48) return 'avancar';
  if (total >= 34) return 'reserva';
  return 'eliminar';
}

function submitTest() {
  const autoScore = calcAutoScore();
  const flags = detectFlags(answers);
  const candidato = {
    id: Date.now(),
    ...candidatoInfo,
    data: new Date().toLocaleDateString('pt-BR'),
    hora: new Date().toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit' }),
    answers: { ...answers },
    autoScore,
    manualScore: null,
    nota: '',
    status: 'pendente',
    flags,
  };
  const list = getCandidatos();
  list.unshift(candidato);
  saveCandidatos(list);
  showStep('step-success');
}

// ══════════════════════
// PAINEL
// ══════════════════════
function renderPainel() {
  const list = getCandidatos();
  let filtered = list;
  if (activeFilter === 'flag') filtered = list.filter(c => c.flags && c.flags.length > 0);
  else if (activeFilter !== 'todos') filtered = list.filter(c => c.status === activeFilter);

  document.getElementById('stat-total').textContent = list.length;
  document.getElementById('stat-avancar').textContent = list.filter(c => c.status === 'avancar').length;
  document.getElementById('stat-reserva').textContent = list.filter(c => c.status === 'reserva').length;
  document.getElementById('stat-eliminar').textContent = list.filter(c => c.status === 'eliminar').length;
  document.getElementById('stat-flags').textContent = list.filter(c => c.flags && c.flags.length > 0).length;

  const cont = document.getElementById('tabela-container');
  if (filtered.length === 0) { cont.innerHTML = '<div class="empty-state">Nenhum candidato encontrado.</div>'; return; }

  let html = `<table class="candidatos-table"><thead><tr>
    <th>Candidato</th><th>Pts auto</th><th>Total</th><th>Status</th><th>Alertas</th><th>Data</th><th></th>
  </tr></thead><tbody>`;

  filtered.forEach(c => {
    const realIdx = list.findIndex(x => x.id === c.id);
    const total = c.autoScore + (c.manualScore || 0);
    const pillClass = { avancar:'pill-avancar', reserva:'pill-reserva', eliminar:'pill-eliminar', pendente:'pill-pendente' }[c.status];
    const pillText = { avancar:'Avançar', reserva:'Reserva', eliminar:'Eliminar', pendente:'Pendente' }[c.status];
    const flagsHtml = c.flags && c.flags.length > 0 ? `<span class="flag flag-amber">${c.flags.length} alerta${c.flags.length > 1 ? 's' : ''}</span>` : '<span style="font-size:12px;color:var(--gray-400)">—</span>';

    html += `<tr>
      <td><div style="font-weight:500">${c.nome}</div><div style="font-size:12px;color:var(--gray-400)">${c.telefone}</div></td>
      <td><div class="pts-bar-wrap"><span style="font-weight:500;min-width:28px">${c.autoScore}</span>
        <div class="pts-bar-track"><div class="pts-bar-fill" style="width:${Math.round((c.autoScore/40)*100)}%"></div></div></div></td>
      <td style="font-weight:500">${c.manualScore !== null ? total : '—'}</td>
      <td><span class="status-pill ${pillClass}">${pillText}</span></td>
      <td>${flagsHtml}</td>
      <td style="font-size:13px;color:var(--gray-600)">${c.data} ${c.hora}</td>
      <td><button class="ver-btn" onclick="openModal(${realIdx})">Ver →</button></td>
    </tr>`;
  });
  html += '</tbody></table>';
  cont.innerHTML = html;
}

function setFilter(f, btn) {
  activeFilter = f;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderPainel();
}

// ══════════════════════
// MODAL
// ══════════════════════
function openModal(idx) {
  modalIndex = idx;
  const list = getCandidatos();
  const c = list[idx];
  if (!c) return;

  document.getElementById('modal-nome').textContent = c.nome;
  document.getElementById('modal-pts').textContent = c.autoScore;
  document.getElementById('modal-info').textContent = `${c.telefone} · ${c.origem || 'origem não informada'} · ${c.data}`;

  const total = c.autoScore + (c.manualScore || 0);
  const pillClass = { avancar:'pill-avancar', reserva:'pill-reserva', eliminar:'pill-eliminar', pendente:'pill-pendente' }[c.status];
  const pillText = { avancar:'Avançar', reserva:'Reserva', eliminar:'Eliminar', pendente:'Avaliação pendente' }[c.status];
  document.getElementById('modal-status-pill').innerHTML = `<span class="status-pill ${pillClass}">${pillText}</span>${c.manualScore !== null ? ` <span style="font-size:13px;color:var(--gray-600);margin-left:8px">Total: ${total} pts</span>` : ''}`;

  // Alertas de momento de vida
  let alertaHtml = '';
  if (c.flags && c.flags.length > 0) {
    alertaHtml = `<div class="alerta-box"><strong>Sinais de alerta — momento de vida</strong>`;
    c.flags.forEach(f => { alertaHtml += `<div>• ${f}</div>`; });
    alertaHtml += `</div>`;
  }
  document.getElementById('modal-alerta').innerHTML = alertaHtml;

  const scaleLabels = ['','Discordo totalmente','Discordo','Neutro','Concordo','Concordo totalmente'];
  let html = '';

  // Cenários
  html += `<div class="modal-section"><div class="modal-section-title">Cenários (pontuação automática)</div>`;
  questions.filter(q => q.type === 'choice' && q.id <= 5).forEach(q => {
    const ans = c.answers[q.id];
    const opt = q.options[ans];
    html += `<div class="modal-qa"><div class="modal-q">${q.text}<span class="modal-pts">+${opt ? opt.pts : 0} pts</span></div>
      <div class="modal-a">${opt ? opt.text : '—'}</div></div>`;
  });
  html += `</div>`;

  // Valores
  html += `<div class="modal-section"><div class="modal-section-title">Valores — escala 1–5</div>`;
  questions.filter(q => q.type === 'scale' && q.id <= 10).forEach(q => {
    const val = c.answers[q.id];
    html += `<div class="modal-qa"><div class="modal-q">${q.text}<span class="modal-pts">+${val || 0} pts</span></div>
      <div class="modal-a">${scaleLabels[val] || '—'}</div></div>`;
  });
  html += `</div>`;

  // Abertas
  html += `<div class="modal-section"><div class="modal-section-title">Respostas abertas — avaliar manualmente</div>`;
  questions.filter(q => q.type === 'open').forEach(q => {
    const val = c.answers[q.id];
    html += `<div class="modal-qa"><div class="modal-q">${q.text}</div>
      <div class="modal-a">${val || '—'}</div></div>`;
  });
  html += `</div>`;

  // Momento de vida
  html += `<div class="modal-section"><div class="modal-section-title">Momento de vida (respostas brutas)</div>`;
  questions.filter(q => q.id >= 16).forEach(q => {
    let resposta = '—';
    if (q.type === 'choice' && c.answers[q.id] !== undefined) {
      resposta = q.options[c.answers[q.id]].text;
    } else if (q.type === 'scale' && c.answers[q.id] !== undefined) {
      resposta = `${c.answers[q.id]} — ${scaleLabels[c.answers[q.id]]}`;
    }
    const isFlag = (q.type === 'choice' && c.answers[q.id] !== undefined && q.options[c.answers[q.id]].flag) ||
                   (q.type === 'scale' && c.answers[q.id] !== undefined && q.flagBelow && c.answers[q.id] < q.flagBelow);
    html += `<div class="modal-qa"><div class="modal-q">${q.text}${isFlag ? '<span class="modal-flag" style="background:var(--amber-light);color:var(--amber)">alerta</span>' : ''}</div>
      <div class="modal-a">${resposta}</div></div>`;
  });
  html += `</div>`;

  document.getElementById('modal-content').innerHTML = html;
  document.getElementById('override-input').value = c.manualScore !== null ? c.manualScore : '';
  document.getElementById('nota-input').value = c.nota || '';
  document.getElementById('modal').classList.add('open');
}

function closeModal() { document.getElementById('modal').classList.remove('open'); modalIndex = null; }
function closeModalOutside(e) { if (e.target === document.getElementById('modal')) closeModal(); }

function saveNota() {
  if (modalIndex === null) return;
  const list = getCandidatos();
  const c = list[modalIndex];
  const raw = document.getElementById('override-input').value;
  const manual = raw !== '' ? Math.min(25, Math.max(0, parseInt(raw) || 0)) : null;
  c.manualScore = manual;
  c.nota = document.getElementById('nota-input').value;
  c.status = getStatus(c.autoScore, manual);
  saveCandidatos(list);
  closeModal();
  renderPainel();
}

// ══════════════════════
// EXPORT
// ══════════════════════
function exportCSV() {
  const list = getCandidatos();
  if (!list.length) { alert('Nenhum candidato para exportar.'); return; }
  const headers = ['Nome','Telefone','Origem','Data','Hora','Pts Auto','Pts Manual','Total','Status','Alertas','Nota'];
  const rows = list.map(c => [
    c.nome, c.telefone, c.origem||'', c.data, c.hora,
    c.autoScore, c.manualScore??'',
    c.autoScore + (c.manualScore||0),
    c.status,
    (c.flags||[]).join(' | '),
    (c.nota||'').replace(/,/g,';')
  ]);
  const csv = [headers,...rows].map(r => r.join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv], { type: 'text/csv;charset=utf-8;' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'candidatos-sdr-podium.csv';
  a.click();
}
</script>
</body>
</html>
