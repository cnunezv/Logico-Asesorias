<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Reto Costeño — Resultados por Curso</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
  :root {
    --bg: #0b0f1a;
    --surface: #131929;
    --card: #1a2235;
    --border: #263047;
    --accent1: #f4c542;
    --accent2: #4fd1c5;
    --accent3: #f687b3;
    --accent4: #9f7aea;
    --accent5: #68d391;
    --text: #e8edf5;
    --muted: #6b7a9b;
    --mat: #f4c542;
    --len: #4fd1c5;
    --nat: #68d391;
    --soc: #f687b3;
    --ing: #9f7aea;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: 0;
  }

  /* Hero header */
  .hero {
    background: linear-gradient(135deg, #0d1421 0%, #131929 50%, #0f1c2e 100%);
    border-bottom: 1px solid var(--border);
    padding: 48px 48px 36px;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute;
    top: -80px; right: -80px;
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(244,197,66,0.08) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero::after {
    content: '';
    position: absolute;
    bottom: -60px; left: 20%;
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(79,209,197,0.06) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero-tag {
    display: inline-block;
    font-family: 'Syne', sans-serif;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent1);
    background: rgba(244,197,66,0.1);
    border: 1px solid rgba(244,197,66,0.25);
    padding: 6px 14px;
    border-radius: 100px;
    margin-bottom: 20px;
  }
  .hero h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 4vw, 52px);
    font-weight: 800;
    line-height: 1.1;
    letter-spacing: -1px;
    margin-bottom: 8px;
  }
  .hero h1 span { color: var(--accent1); }
  .hero-sub {
    font-size: 15px;
    color: var(--muted);
    font-weight: 300;
    letter-spacing: 0.3px;
    margin-top: 10px;
  }

  /* Stats row */
  .stats-row {
    display: flex;
    gap: 1px;
    background: var(--border);
    border-bottom: 1px solid var(--border);
  }
  .stat-pill {
    flex: 1;
    background: var(--surface);
    padding: 20px 28px;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }
  .stat-pill .val {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    color: var(--text);
  }
  .stat-pill .lbl {
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 0.5px;
    text-transform: uppercase;
  }
  .stat-pill .val.gold { color: var(--accent1); }
  .stat-pill .val.teal { color: var(--accent2); }

  /* Main content */
  .content {
    padding: 36px 48px 60px;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border);
    margin-top: 48px;
  }
  .section-title:first-child { margin-top: 0; }

  /* Grade nav */
  .grade-nav {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 28px;
  }
  .grade-btn {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    padding: 8px 20px;
    border: 1px solid var(--border);
    background: var(--card);
    color: var(--muted);
    border-radius: 100px;
    cursor: pointer;
    transition: all 0.2s ease;
    letter-spacing: 0.3px;
  }
  .grade-btn:hover { border-color: var(--accent2); color: var(--accent2); }
  .grade-btn.active { background: var(--accent1); border-color: var(--accent1); color: #0b0f1a; }

  /* Chart grid */
  .chart-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin-bottom: 20px;
  }
  .chart-grid-3 {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 20px;
  }
  .chart-full { grid-column: 1 / -1; }

  .card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    position: relative;
    overflow: hidden;
  }
  .card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent1), var(--accent2));
    opacity: 0.6;
    border-radius: 16px 16px 0 0;
  }
  .card-title {
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    font-weight: 700;
    color: var(--muted);
    letter-spacing: 1.5px;
    text-transform: uppercase;
    margin-bottom: 20px;
  }
  .card canvas { display: block; }

  /* Student table */
  .student-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13px;
  }
  .student-table th {
    font-family: 'Syne', sans-serif;
    font-size: 10px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--muted);
    padding: 10px 14px;
    text-align: left;
    border-bottom: 1px solid var(--border);
    white-space: nowrap;
  }
  .student-table td {
    padding: 10px 14px;
    border-bottom: 1px solid rgba(38,48,71,0.5);
    color: var(--text);
    white-space: nowrap;
  }
  .student-table tr:last-child td { border-bottom: none; }
  .student-table tr:hover td { background: rgba(255,255,255,0.02); }
  .badge {
    display: inline-block;
    font-size: 10px;
    font-weight: 600;
    font-family: 'Syne', sans-serif;
    padding: 3px 10px;
    border-radius: 100px;
    letter-spacing: 0.5px;
  }
  .badge.bajo { background: rgba(248,113,113,0.15); color: #f87171; border: 1px solid rgba(248,113,113,0.3); }
  .badge.basico { background: rgba(251,191,36,0.15); color: #fbbf24; border: 1px solid rgba(251,191,36,0.3); }
  .badge.alto { background: rgba(52,211,153,0.15); color: #34d399; border: 1px solid rgba(52,211,153,0.3); }
  .badge.superior { background: rgba(96,165,250,0.15); color: #60a5fa; border: 1px solid rgba(96,165,250,0.3); }
  .badge.n1 { background: rgba(248,113,113,0.15); color: #f87171; border: 1px solid rgba(248,113,113,0.3); }
  .badge.n2 { background: rgba(251,191,36,0.15); color: #fbbf24; border: 1px solid rgba(251,191,36,0.3); }
  .badge.n3 { background: rgba(52,211,153,0.15); color: #34d399; border: 1px solid rgba(52,211,153,0.3); }
  .badge.n4 { background: rgba(96,165,250,0.15); color: #60a5fa; border: 1px solid rgba(96,165,250,0.3); }

  .score-bar-wrap { display: flex; align-items: center; gap: 10px; }
  .score-bar-bg { flex: 1; height: 5px; background: var(--border); border-radius: 3px; min-width: 60px; }
  .score-bar-fill { height: 5px; border-radius: 3px; background: linear-gradient(90deg, var(--accent2), var(--accent1)); transition: width 0.6s ease; }
  .score-val { font-family: 'Syne', sans-serif; font-size: 13px; font-weight: 700; min-width: 36px; }

  /* Legend pills */
  .legend-row {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    margin-bottom: 16px;
  }
  .legend-item {
    display: flex;
    align-items: center;
    gap: 7px;
    font-size: 12px;
    color: var(--muted);
  }
  .legend-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  /* Grade detail panel */
  #grade-detail { animation: fadeIn 0.3s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

  .empty-msg {
    color: var(--muted);
    font-size: 14px;
    padding: 32px 0;
    text-align: center;
  }

  @media(max-width: 900px) {
    .hero { padding: 32px 24px 28px; }
    .content { padding: 24px 20px 40px; }
    .chart-grid { grid-template-columns: 1fr; }
    .chart-grid-3 { grid-template-columns: 1fr; }
    .stats-row { flex-direction: column; }
  }
</style>
</head>
<body>

<div class="hero">
  <div class="hero-tag">Colegio El Pilar del Saber</div>
  <h1>Reto Costeño <span>2026</span></h1>
  <p class="hero-sub">Prueba Diagnóstica — Resultados individuales por estudiante — Grados 2° a 10°</p>
</div>

<div class="stats-row">
  <div class="stat-pill">
    <span class="val gold">80</span>
    <span class="lbl">Estudiantes</span>
  </div>
  <div class="stat-pill">
    <span class="val teal">9</span>
    <span class="lbl">Cursos evaluados</span>
  </div>
  <div class="stat-pill">
    <span class="val">5</span>
    <span class="lbl">Áreas evaluadas</span>
  </div>
  <div class="stat-pill">
    <span class="val">2°–5°</span>
    <span class="lbl">Escala 1–10</span>
  </div>
  <div class="stat-pill">
    <span class="val">6°–10°</span>
    <span class="lbl">Escala 0–100%</span>
  </div>
</div>

<div class="content">

  <!-- OVERVIEW CHARTS -->
  <div class="section-title">Visión General</div>
  <div class="chart-grid">
    <div class="card">
      <div class="card-title">Promedio por grado — Todas las áreas</div>
      <canvas id="chartOverall" height="220"></canvas>
    </div>
    <div class="card">
      <div class="card-title">Distribución de niveles por grado</div>
      <canvas id="chartLevels" height="220"></canvas>
    </div>
  </div>

  <div class="chart-grid">
    <div class="card chart-full">
      <div class="card-title">Rendimiento por área según grado (Grados 2°–5° escala 1–10 · Grados 6°–10° escala 0–100%)</div>
      <div class="legend-row">
        <div class="legend-item"><div class="legend-dot" style="background:#f4c542"></div>Matemáticas</div>
        <div class="legend-item"><div class="legend-dot" style="background:#4fd1c5"></div>Lenguaje</div>
        <div class="legend-item"><div class="legend-dot" style="background:#68d391"></div>Naturales</div>
        <div class="legend-item"><div class="legend-dot" style="background:#f687b3"></div>Sociales</div>
        <div class="legend-item"><div class="legend-dot" style="background:#9f7aea"></div>Inglés</div>
      </div>
      <canvas id="chartSubjects" height="160"></canvas>
    </div>
  </div>

  <!-- PER-GRADE DETAIL -->
  <div class="section-title" style="margin-top:52px">Detalle por Grado</div>
  <div class="grade-nav" id="gradeNav"></div>
  <div id="grade-detail"></div>

</div>

<script>
const DATA = [
  // Grado 2° - solo Mat y Leng (escala 1-10)
  { grado:'2°', nombre:'CUESTA ROMERO JULIETTA', mat:8.57, len:8.82, nat:null, soc:null, ing:null, total:8.7, nivMat:'BÁSICO', nivLen:'BÁSICO' },
  { grado:'2°', nombre:'GARCIA CAMACHO LUIS JOSÉ', mat:7.86, len:5.88, nat:null, soc:null, ing:null, total:6.87, nivMat:'BÁSICO', nivLen:'BAJO' },
  { grado:'2°', nombre:'ROMERO LORDUY DAVID LUIZ', mat:4.29, len:5.29, nat:null, soc:null, ing:null, total:4.79, nivMat:'BAJO', nivLen:'BAJO' },
  // Grado 3°
  { grado:'3°', nombre:'ANILLO ARABIA ROBERTO ANDRES', mat:5.24, len:1.11, nat:null, soc:null, ing:null, total:3.17, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'3°', nombre:'FERNANDEZ ROSSI EMMA', mat:7.14, len:9.44, nat:null, soc:null, ing:null, total:8.29, nivMat:'BAJO', nivLen:'ALTO' },
  { grado:'3°', nombre:'GARCIA CAMACHO LUIS ANGEL', mat:6.67, len:4.44, nat:null, soc:null, ing:null, total:5.56, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'3°', nombre:'MEJIA GANEN SARA SOFIA', mat:5.71, len:6.11, nat:null, soc:null, ing:null, total:5.91, nivMat:'BAJO', nivLen:'BAJO' },
  // Grado 4°
  { grado:'4°', nombre:'ALCAZAR CHAVEZ CHRISTOPHER', mat:1.43, len:3.04, nat:null, soc:null, ing:null, total:2.24, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'4°', nombre:'ALVAREZ NAVARRO ISABEL', mat:7.62, len:4.78, nat:null, soc:null, ing:null, total:6.2, nivMat:'BÁSICO', nivLen:'BAJO' },
  { grado:'4°', nombre:'CASTILLA CANTERO ANTOINE', mat:5.71, len:3.48, nat:null, soc:null, ing:null, total:4.6, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'4°', nombre:'LUNA CASTRO VICTORIA', mat:6.19, len:5.22, nat:null, soc:null, ing:null, total:5.7, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'4°', nombre:'MORELO SUAREZ SARA SOFIA', mat:8.57, len:4.35, nat:null, soc:null, ing:null, total:6.46, nivMat:'BÁSICO', nivLen:'BAJO' },
  { grado:'4°', nombre:'PERILLA HERNANDEZ VICTORIA', mat:4.29, len:2.61, nat:null, soc:null, ing:null, total:3.45, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'4°', nombre:'ROMERO LORDUY MARIA FERNANDA', mat:5.71, len:6.09, nat:null, soc:null, ing:null, total:5.9, nivMat:'BAJO', nivLen:'BAJO' },
  // Grado 5°
  { grado:'5°', nombre:'ANILLO ARABIA JUAN CAMILO', mat:3.2, len:2.96, nat:null, soc:null, ing:null, total:3.08, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'5°', nombre:'BEDOYA ROMERO ORIANNA', mat:3.6, len:5.56, nat:null, soc:null, ing:null, total:4.58, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'5°', nombre:'CASTILLA CANTERO BRIANNA', mat:3.2, len:5.19, nat:null, soc:null, ing:null, total:4.19, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'5°', nombre:'PEREIRA CASTILLA EDUARDO', mat:2, len:2.59, nat:null, soc:null, ing:null, total:2.3, nivMat:'BAJO', nivLen:'BAJO' },
  { grado:'5°', nombre:'SOTOMAYOR MARTINEZ ANGELLO', mat:3.6, len:5.93, nat:null, soc:null, ing:null, total:4.76, nivMat:'BAJO', nivLen:'BAJO' },
  // Grado 6°
  { grado:'6°', nombre:'ARIZA DUARTE JORGE LUIS', mat:38.46, len:7.69, nat:24, soc:23.08, ing:24, total:116.8, nivMat:'NIVEL 2', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'6°', nombre:'CUENTAS LLANES VALERIE', mat:23.08, len:42.31, nat:0, soc:0, ing:28, total:86.21, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'6°', nombre:'CUESTA ROMERO SOPHIA', mat:26.92, len:50, nat:28, soc:23.08, ing:48, total:166.15, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'6°', nombre:'GONZALEZ PADILLA ILSA MARIA', mat:42.31, len:61.54, nat:48, soc:38.46, ing:40, total:234.97, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 2', nivIng:'NIVEL 2' },
  { grado:'6°', nombre:'EBRATT DIAZ JUAN PABLO', mat:34.62, len:15.38, nat:16, soc:34.62, ing:28, total:126.86, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'6°', nombre:'UREÑA CANTILLO SANTIAGO', mat:7.69, len:23.08, nat:4, soc:15.38, ing:24, total:67.1, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  // Grado 7°
  { grado:'7°', nombre:'ALVAREZ CASTILLO MARIANGEL', mat:31.82, len:56, nat:32, soc:55, ing:48, total:220.17, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 3', nivIng:'NIVEL 2' },
  { grado:'7°', nombre:'ARNEDO MERCADO ANGELINA', mat:27.27, len:28, nat:36, soc:50, ing:44, total:179.93, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 2', nivSoc:'NIVEL 2', nivIng:'NIVEL 2' },
  { grado:'7°', nombre:'BABILONIA DUARTE EMILY', mat:18.18, len:52, nat:56, soc:70, ing:68, total:252.52, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 3', nivIng:'NIVEL 3' },
  { grado:'7°', nombre:'FORERO PEREZ SALOME', mat:36.36, len:60, nat:32, soc:80, ing:36, total:254.27, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 4', nivIng:'NIVEL 1' },
  { grado:'7°', nombre:'GOMEZ DIAZ LUCIANO', mat:27.27, len:52, nat:32, soc:40, ing:68, total:200.7, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 2', nivIng:'NIVEL 3' },
  { grado:'7°', nombre:'JIMENEZ CUELLO JUAN PABLO', mat:45.45, len:72, nat:56, soc:60, ing:80, total:300.14, nivMat:'NIVEL 2', nivLen:'NIVEL 4', nivNat:'NIVEL 3', nivSoc:'NIVEL 3', nivIng:'NIVEL 4' },
  { grado:'7°', nombre:'MARRIAGA PUELLO ESTEBAN', mat:31.82, len:56, nat:32, soc:60, ing:40, total:222.87, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 3', nivIng:'NIVEL 2' },
  { grado:'7°', nombre:'MENDOZA DURANGO MATHIAS', mat:36.36, len:64, nat:20, soc:55, ing:60, total:225.42, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 3', nivIng:'NIVEL 3' },
  { grado:'7°', nombre:'PERILLA HERNANDEZ VALENTINA', mat:40.91, len:52, nat:52, soc:75, ing:56, total:275.28, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 4', nivIng:'NIVEL 2' },
  { grado:'7°', nombre:'QUINTANA POLO VALERIA', mat:0, len:0, nat:24, soc:5, ing:36, total:47.31, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'7°', nombre:'RAMOS RAMIREZ SALOME', mat:31.82, len:48, nat:20, soc:40, ing:48, total:179.79, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 2', nivIng:'NIVEL 2' },
  { grado:'7°', nombre:'VALOYES ARDILA VALERIA', mat:31.82, len:60, nat:44, soc:60, ing:72, total:253.64, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 3', nivIng:'NIVEL 4' },
  { grado:'7°', nombre:'VILLEGAS JARABA IMANOL', mat:36.36, len:60, nat:48, soc:15, ing:68, total:210.03, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 3' },
  { grado:'7°', nombre:'N.N', mat:0, len:44, nat:12, soc:65, ing:56, total:161.15, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 3', nivIng:'NIVEL 2' },
  // Grado 8°
  { grado:'8°', nombre:'ARCE CHAMORRO MARIANA', mat:30.43, len:52, nat:40.91, soc:4.35, ing:33.33, total:160.16, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'BOHORQUEZ CORONELL ALMA', mat:34.78, len:44, nat:36.36, soc:34.78, ing:13.33, total:178.12, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'CALDERON PIANETA TOMAS', mat:21.74, len:56, nat:59.09, soc:34.78, ing:53.33, total:218.53, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'CUETER DE LA BARRERA SAID', mat:43.48, len:52, nat:59.09, soc:21.74, ing:56.67, total:225.23, nivMat:'NIVEL 2', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'DIAZ CAMARGO SARA SOFIA', mat:21.74, len:56, nat:45.45, soc:26.09, ing:43.33, total:188.91, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'DUNOYER CANTILLO SAMUEL', mat:21.74, len:52, nat:27.27, soc:21.74, ing:40, total:157.02, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'FRANCO ORTIZ JULIETA', mat:34.78, len:60, nat:59.09, soc:30.43, ing:36.67, total:226.77, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'GIL LOPEZ JUAN MANUEL', mat:26.09, len:56, nat:50, soc:30.43, ing:53.33, total:208.04, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'HERNANDEZ PANTANO GABRIEL', mat:21.74, len:56, nat:40.91, soc:17.39, ing:13.33, total:162.1, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'ISAZA MARTELO VALERIA', mat:34.78, len:44, nat:45.45, soc:17.39, ing:30, total:174.96, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'JIMENEZ PALOMARES LAURA', mat:34.78, len:60, nat:59.09, soc:30.43, ing:40, total:228.05, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'MORON GARCIA MARIA ISABEL', mat:21.74, len:44, nat:27.27, soc:34.78, ing:43.33, total:164.12, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'PUERTA RODRIGUEZ EMMANUEL', mat:30.43, len:36, nat:22.73, soc:17.39, ing:23.33, total:131.92, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'REDONDO TRONCOSO MARIA LUCIA', mat:17.39, len:44, nat:40.91, soc:26.09, ing:43.33, total:164.81, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'VERGARA VALENCIA BASTIAN', mat:52.17, len:36, nat:22.73, soc:21.74, ing:26.67, total:163.3, nivMat:'NIVEL 3', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'8°', nombre:'ORTIZ CABARCAS LUIS FELIPE', mat:30.43, len:44, nat:13.64, soc:34.78, ing:36.67, total:155.86, nivMat:'NIVEL 1', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'N.N 1', mat:43.48, len:48, nat:45.45, soc:39.13, ing:56.67, total:224.94, nivMat:'NIVEL 2', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 2', nivIng:'NIVEL 2' },
  { grado:'8°', nombre:'N.N 2', mat:21.74, len:56, nat:31.82, soc:26.09, ing:40, total:171.9, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  // Grado 9°
  { grado:'9°', nombre:'ALVAREZ NAVARRO LUIS ARTURO', mat:70.83, len:45.45, nat:57.14, soc:34.78, ing:43.33, total:256.91, nivMat:'NIVEL 4', nivLen:'NIVEL 2', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'BORJA VILLA CESAR DAVID', mat:33.33, len:31.82, nat:19.05, soc:26.09, ing:36.67, total:141.36, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'BOBADILLA PALOMINO NATHALY', mat:45.83, len:50, nat:38.1, soc:21.74, ing:30, total:191.16, nivMat:'NIVEL 2', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'9°', nombre:'CERVANTES RODRIGUEZ SANTIAGO', mat:54.17, len:50, nat:38.1, soc:26.09, ing:36.67, total:208.35, nivMat:'NIVEL 3', nivLen:'NIVEL 2', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'ESPINOSA RUDAS ANDRES', mat:62.5, len:63.64, nat:42.86, soc:30.43, ing:60, total:253.19, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 3' },
  { grado:'9°', nombre:'GORDILLO BLANCO ALEJANDRA', mat:41.67, len:40.91, nat:33.33, soc:17.39, ing:30, total:165.35, nivMat:'NIVEL 2', nivLen:'NIVEL 2', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'9°', nombre:'ISAZA MARTELO LUCIA', mat:62.5, len:77.27, nat:61.9, soc:34.78, ing:40, total:288.22, nivMat:'NIVEL 3', nivLen:'NIVEL 4', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'LUNA CASTRO PAULA', mat:54.17, len:77.27, nat:38.1, soc:21.74, ing:50, total:239.93, nivMat:'NIVEL 3', nivLen:'NIVEL 4', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'MESTRE DE AVILA JIULIAN', mat:33.33, len:31.82, nat:38.1, soc:34.78, ing:16.67, total:165.67, nivMat:'NIVEL 1', nivLen:'NIVEL 1', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'9°', nombre:'VALDEZ CASTRO CARMEN', mat:58.33, len:54.55, nat:52.38, soc:26.09, ing:46.67, total:238.73, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'ZAMBRANO NÚÑEZ VALERIA', mat:62.5, len:77.27, nat:66.67, soc:34.78, ing:50, total:297.56, nivMat:'NIVEL 3', nivLen:'NIVEL 4', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'9°', nombre:'ZUÑIGA PEREZ CRISTAL', mat:62.5, len:59.09, nat:52.38, soc:34.78, ing:16.67, total:247.28, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 3', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  // Grado 10°
  { grado:'10°', nombre:'ARROYO FERNANDEZ LEONEL', mat:52.38, len:43.48, nat:52, soc:40, ing:35.56, total:230.44, nivMat:'NIVEL 3', nivLen:'NIVEL 2', nivNat:'NIVEL 3', nivSoc:'NIVEL 2', nivIng:'NIVEL 1' },
  { grado:'10°', nombre:'ATENCIA VASQUEZ DAGO', mat:52.38, len:73.91, nat:40, soc:55, ing:53.33, total:275.85, nivMat:'NIVEL 3', nivLen:'NIVEL 4', nivNat:'NIVEL 2', nivSoc:'NIVEL 3', nivIng:'NIVEL 2' },
  { grado:'10°', nombre:'CAVIEDES CONTRERAS SANTIAGO', mat:85.71, len:73.91, nat:40, soc:55, ing:75.56, total:322.86, nivMat:'NIVEL 4', nivLen:'NIVEL 4', nivNat:'NIVEL 2', nivSoc:'NIVEL 3', nivIng:'NIVEL 4' },
  { grado:'10°', nombre:'ESPINOSA RIVERA ISABEL', mat:57.14, len:73.91, nat:36, soc:25, ing:84.44, total:254.08, nivMat:'NIVEL 3', nivLen:'NIVEL 4', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 4' },
  { grado:'10°', nombre:'GIRALDO BUSTOS DAVID', mat:28.57, len:52.17, nat:12, soc:25, ing:26.67, total:146.12, nivMat:'NIVEL 1', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'10°', nombre:'GUERRA MARTELO SOFIA', mat:80.95, len:86.96, nat:44, soc:45, ing:55.56, total:317.8, nivMat:'NIVEL 4', nivLen:'NIVEL 4', nivNat:'NIVEL 2', nivSoc:'NIVEL 2', nivIng:'NIVEL 2' },
  { grado:'10°', nombre:'KELSY PATERNINA VALERIA', mat:57.14, len:60.87, nat:44, soc:45, ing:26.67, total:249.12, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 2', nivIng:'NIVEL 1' },
  { grado:'10°', nombre:'MARTINEZ VARGAS JESUS', mat:57.14, len:52.17, nat:32, soc:35, ing:53.33, total:223.96, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 2' },
  { grado:'10°', nombre:'MERLANO PEREZ ANDRES', mat:38.1, len:21.74, nat:28, soc:15, ing:33.33, total:131.48, nivMat:'NIVEL 2', nivLen:'NIVEL 1', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'10°', nombre:'MOGOLLON DIAZ ESTHEFANY', mat:52.38, len:52.17, nat:36, soc:15, ing:33.33, total:192.31, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 2', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
  { grado:'10°', nombre:'PARRA OROZCO ANDRES', mat:61.9, len:56.52, nat:28, soc:20, ing:17.78, total:198.87, nivMat:'NIVEL 3', nivLen:'NIVEL 3', nivNat:'NIVEL 1', nivSoc:'NIVEL 1', nivIng:'NIVEL 1' },
];

const GRADES = ['2°','3°','4°','5°','6°','7°','8°','9°','10°'];
const SUBJECTS = ['mat','len','nat','soc','ing'];
const SUBJECT_LABELS = ['Matemáticas','Lenguaje','Naturales','Sociales','Inglés'];
const COLORS = ['#f4c542','#4fd1c5','#68d391','#f687b3','#9f7aea'];

function avg(arr) {
  const v = arr.filter(x => x !== null && !isNaN(x));
  return v.length ? v.reduce((a,b)=>a+b,0)/v.length : null;
}

// --- CHART 1: Overall avg per grade ---
const overallAvgs = GRADES.map(g => {
  const students = DATA.filter(d => d.grado === g);
  // Normalize to 0-100 scale for comparison
  const is1_10 = ['2°','3°','4°','5°'].includes(g);
  const vals = students.map(s => {
    const v = s.total;
    return is1_10 ? (v/10)*100 : null; // use total as-is for pct grades
  });
  if (is1_10) return avg(vals.filter(v=>v!==null));
  // For 6-10, total is sum of 5 subjects (each 0-100), avg = total/5
  return avg(students.map(s => s.total / 5));
});

const ctx1 = document.getElementById('chartOverall').getContext('2d');
new Chart(ctx1, {
  type: 'bar',
  data: {
    labels: GRADES,
    datasets: [{
      label: 'Promedio (%)',
      data: overallAvgs,
      backgroundColor: GRADES.map((g,i) => {
        const v = overallAvgs[i] || 0;
        if (v >= 60) return '#68d391';
        if (v >= 40) return '#f4c542';
        return '#f87171';
      }),
      borderRadius: 8,
      borderSkipped: false,
    }]
  },
  options: {
    responsive: true,
    plugins: {
      legend: { display: false },
      tooltip: {
        callbacks: {
          label: ctx => ` ${ctx.raw.toFixed(1)}%`
        }
      }
    },
    scales: {
      x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'Syne', size: 12 } } },
      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'DM Sans' }, callback: v => v + '%' }, max: 100, min: 0 }
    }
  }
});

// --- CHART 2: Level distribution stacked bar ---
function getLevels(g) {
  const students = DATA.filter(d => d.grado === g);
  const is1_10 = ['2°','3°','4°','5°'].includes(g);
  const counts = { bajo: 0, basico: 0, alto: 0, superior: 0, n1: 0, n2: 0, n3: 0, n4: 0 };
  students.forEach(s => {
    if (is1_10) {
      ['nivMat','nivLen'].forEach(k => {
        if (s[k] === 'BAJO') counts.bajo++;
        else if (s[k] === 'BÁSICO') counts.basico++;
        else if (s[k] === 'ALTO') counts.alto++;
        else if (s[k] === 'SUPERIOR') counts.superior++;
      });
    } else {
      ['nivMat','nivLen','nivNat','nivSoc','nivIng'].forEach(k => {
        if (s[k] === 'NIVEL 1') counts.n1++;
        else if (s[k] === 'NIVEL 2') counts.n2++;
        else if (s[k] === 'NIVEL 3') counts.n3++;
        else if (s[k] === 'NIVEL 4') counts.n4++;
      });
    }
  });
  return { is1_10, counts };
}

const ctx2 = document.getElementById('chartLevels').getContext('2d');
const levelData2_5 = GRADES.slice(0,4).map(g => getLevels(g).counts);
const levelData6_10 = GRADES.slice(4).map(g => getLevels(g).counts);

new Chart(ctx2, {
  type: 'bar',
  data: {
    labels: GRADES,
    datasets: [
      {
        label: 'Bajo / Nivel 1',
        data: GRADES.map(g => {
          const { is1_10, counts } = getLevels(g);
          return is1_10 ? counts.bajo : counts.n1;
        }),
        backgroundColor: 'rgba(248,113,113,0.7)',
        borderRadius: 4, stack: 'levels'
      },
      {
        label: 'Básico / Nivel 2',
        data: GRADES.map(g => {
          const { is1_10, counts } = getLevels(g);
          return is1_10 ? counts.basico : counts.n2;
        }),
        backgroundColor: 'rgba(251,191,36,0.7)',
        borderRadius: 4, stack: 'levels'
      },
      {
        label: 'Alto / Nivel 3',
        data: GRADES.map(g => {
          const { is1_10, counts } = getLevels(g);
          return is1_10 ? counts.alto : counts.n3;
        }),
        backgroundColor: 'rgba(52,211,153,0.7)',
        borderRadius: 4, stack: 'levels'
      },
      {
        label: 'Superior / Nivel 4',
        data: GRADES.map(g => {
          const { is1_10, counts } = getLevels(g);
          return is1_10 ? counts.superior : counts.n4;
        }),
        backgroundColor: 'rgba(96,165,250,0.7)',
        borderRadius: 4, stack: 'levels'
      },
    ]
  },
  options: {
    responsive: true,
    plugins: {
      legend: {
        labels: { color: '#6b7a9b', font: { family: 'DM Sans', size: 11 }, boxWidth: 12 }
      }
    },
    scales: {
      x: { stacked: true, grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'Syne', size: 12 } } },
      y: { stacked: true, grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'DM Sans' } } }
    }
  }
});

// --- CHART 3: Subjects per grade ---
const ctx3 = document.getElementById('chartSubjects').getContext('2d');
const subjectDatasets = SUBJECTS.map((s, si) => ({
  label: SUBJECT_LABELS[si],
  data: GRADES.map(g => {
    const students = DATA.filter(d => d.grado === g);
    const is1_10 = ['2°','3°','4°','5°'].includes(g);
    const vals = students.map(st => st[s]).filter(v => v !== null && !isNaN(v));
    if (!vals.length) return null;
    const a = avg(vals);
    return is1_10 ? (a/10)*100 : a;
  }),
  borderColor: COLORS[si],
  backgroundColor: COLORS[si] + '22',
  tension: 0.4,
  fill: false,
  pointBackgroundColor: COLORS[si],
  pointRadius: 5,
  pointHoverRadius: 8,
  borderWidth: 2,
  spanGaps: true,
}));

new Chart(ctx3, {
  type: 'line',
  data: { labels: GRADES, datasets: subjectDatasets },
  options: {
    responsive: true,
    plugins: {
      legend: { display: false },
      tooltip: {
        callbacks: {
          label: ctx => ` ${ctx.dataset.label}: ${ctx.raw !== null ? ctx.raw.toFixed(1)+'%' : 'N/A'}`
        }
      }
    },
    scales: {
      x: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'Syne', size: 12 } } },
      y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#6b7a9b', font: { family: 'DM Sans' }, callback: v => v + '%' }, min: 0, max: 100 }
    }
  }
});

// --- GRADE DETAIL ---
const nav = document.getElementById('gradeNav');
let activeGrade = null;

GRADES.forEach(g => {
  const btn = document.createElement('button');
  btn.className = 'grade-btn';
  btn.textContent = 'Grado ' + g;
  btn.addEventListener('click', () => {
    document.querySelectorAll('.grade-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    renderGrade(g);
  });
  nav.appendChild(btn);
});

// Auto-select first grade
nav.querySelector('.grade-btn').click();

const chartInstances = {};

function badgeClass(nivel) {
  if (!nivel) return '';
  const n = nivel.toUpperCase();
  if (n.includes('SUPERIOR')) return 'superior';
  if (n.includes('ALTO')) return 'alto';
  if (n.includes('BÁSICO') || n==='BASICO') return 'basico';
  if (n === 'BAJO') return 'bajo';
  if (n.includes('NIVEL 4')) return 'n4';
  if (n.includes('NIVEL 3')) return 'n3';
  if (n.includes('NIVEL 2')) return 'n2';
  if (n.includes('NIVEL 1')) return 'n1';
  return '';
}

function renderGrade(g) {
  const students = DATA.filter(d => d.grado === g);
  const is1_10 = ['2°','3°','4°','5°'].includes(g);
  const detail = document.getElementById('grade-detail');

  // Destroy old charts
  Object.values(chartInstances).forEach(c => c.destroy());
  for (const k in chartInstances) delete chartInstances[k];

  const maxTotal = is1_10 ? 10 : 500;

  // Build subjects available for this grade
  const availSubs = is1_10 ? ['mat','len'] : ['mat','len','nat','soc','ing'];
  const availLabels = is1_10 ? ['Matemáticas','Lenguaje'] : SUBJECT_LABELS;
  const availColors = is1_10 ? [COLORS[0],COLORS[1]] : COLORS;

  const sortedStudents = [...students].sort((a,b) => b.total - a.total);

  detail.innerHTML = `
    <div class="chart-grid">
      <div class="card">
        <div class="card-title">Puntuación total — Grado ${g}</div>
        <canvas id="gradeBar" height="220"></canvas>
      </div>
      <div class="card">
        <div class="card-title">Promedio por área — Grado ${g}</div>
        <canvas id="gradeRadar" height="220"></canvas>
      </div>
    </div>
    <div class="card" style="margin-bottom:20px">
      <div class="card-title">Resultados individuales — Grado ${g}</div>
      <div style="overflow-x:auto">
        <table class="student-table">
          <thead>
            <tr>
              <th>#</th>
              <th>Estudiante</th>
              <th>Matemáticas</th>
              <th>Lenguaje</th>
              ${!is1_10 ? '<th>Naturales</th><th>Sociales</th><th>Inglés</th>' : ''}
              <th>Total</th>
            </tr>
          </thead>
          <tbody>
            ${sortedStudents.map((s,i) => `
              <tr>
                <td style="color:var(--muted);font-size:12px">${i+1}</td>
                <td style="font-weight:500;max-width:200px;overflow:hidden;text-overflow:ellipsis">${s.nombre}</td>
                <td>
                  <div style="display:flex;flex-direction:column;gap:4px">
                    <span style="font-family:Syne;font-size:13px;font-weight:700;color:var(--mat)">${s.mat !== null ? s.mat : '—'}</span>
                    ${s.nivMat ? `<span class="badge ${badgeClass(s.nivMat)}">${s.nivMat}</span>` : ''}
                  </div>
                </td>
                <td>
                  <div style="display:flex;flex-direction:column;gap:4px">
                    <span style="font-family:Syne;font-size:13px;font-weight:700;color:var(--len)">${s.len !== null ? s.len : '—'}</span>
                    ${s.nivLen ? `<span class="badge ${badgeClass(s.nivLen)}">${s.nivLen}</span>` : ''}
                  </div>
                </td>
                ${!is1_10 ? `
                <td>
                  <div style="display:flex;flex-direction:column;gap:4px">
                    <span style="font-family:Syne;font-size:13px;font-weight:700;color:var(--nat)">${s.nat !== null ? s.nat : '—'}</span>
                    ${s.nivNat ? `<span class="badge ${badgeClass(s.nivNat)}">${s.nivNat}</span>` : ''}
                  </div>
                </td>
                <td>
                  <div style="display:flex;flex-direction:column;gap:4px">
                    <span style="font-family:Syne;font-size:13px;font-weight:700;color:var(--soc)">${s.soc !== null ? s.soc : '—'}</span>
                    ${s.nivSoc ? `<span class="badge ${badgeClass(s.nivSoc)}">${s.nivSoc}</span>` : ''}
                  </div>
                </td>
                <td>
                  <div style="display:flex;flex-direction:column;gap:4px">
                    <span style="font-family:Syne;font-size:13px;font-weight:700;color:var(--ing)">${s.ing !== null ? s.ing : '—'}</span>
                    ${s.nivIng ? `<span class="badge ${badgeClass(s.nivIng)}">${s.nivIng}</span>` : ''}
                  </div>
                </td>` : ''}
                <td>
                  <div class="score-bar-wrap">
                    <div class="score-bar-bg">
                      <div class="score-bar-fill" style="width:${Math.min(100,(s.total/maxTotal)*100)}%"></div>
                    </div>
                    <span class="score-val">${s.total}</span>
                  </div>
                </td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      </div>
    </div>
  `;

  // Bar chart: total scores per student
  const barCtx = document.getElementById('gradeBar').getContext('2d');
  const barColors = sortedStudents.map(s => {
    const pct = (s.total / maxTotal) * 100;
    if (pct >= 60) return '#68d391';
    if (pct >= 40) return '#f4c542';
    return '#f87171';
  });
  chartInstances['bar'] = new Chart(barCtx, {
    type: 'bar',
    data: {
      labels: sortedStudents.map(s => s.nombre.split(' ')[0]),
      datasets: [{
        label: 'Total',
        data: sortedStudents.map(s => s.total),
        backgroundColor: barColors,
        borderRadius: 6,
        borderSkipped: false,
      }]
    },
    options: {
      responsive: true,
      plugins: { legend: { display: false } },
      scales: {
        x: { grid: { color: 'rgba(255,255,255,0.04)' }, ticks: { color: '#6b7a9b', font: { size: 10, family: 'DM Sans' }, maxRotation: 45 } },
        y: { grid: { color: 'rgba(255,255,255,0.04)' }, ticks: { color: '#6b7a9b', font: { family: 'DM Sans' } } }
      }
    }
  });

  // Radar chart: avg by subject
  const radarAvgs = availSubs.map(s => {
    const vals = students.map(st => st[s]).filter(v => v !== null && !isNaN(v));
    return vals.length ? avg(vals) : 0;
  });

  const radarCtx = document.getElementById('gradeRadar').getContext('2d');
  chartInstances['radar'] = new Chart(radarCtx, {
    type: 'radar',
    data: {
      labels: availLabels,
      datasets: [{
        label: 'Promedio Grado ' + g,
        data: radarAvgs,
        backgroundColor: 'rgba(244,197,66,0.15)',
        borderColor: '#f4c542',
        pointBackgroundColor: availColors,
        pointRadius: 5,
        borderWidth: 2,
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { labels: { color: '#6b7a9b', font: { family: 'DM Sans', size: 11 } } }
      },
      scales: {
        r: {
          grid: { color: 'rgba(255,255,255,0.06)' },
          angleLines: { color: 'rgba(255,255,255,0.06)' },
          ticks: { color: '#6b7a9b', backdropColor: 'transparent', font: { size: 10 } },
          pointLabels: { color: '#e8edf5', font: { family: 'Syne', size: 12, weight: '600' } },
        }
      }
    }
  });
}
</script>
</body>
</html>
