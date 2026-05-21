[dashboard-facturacion.html](https://github.com/user-attachments/files/28103587/dashboard-facturacion.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard Facturación · PersonalFit Ourense</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --bg: #0f1419;
    --bg-card: #1a2028;
    --bg-card-hover: #222a35;
    --border: #2a3441;
    --text: #e6edf3;
    --text-dim: #8b96a5;
    --text-faint: #5a6573;
    --accent: #6ea8fe;
    --green: #3fb950;
    --green-soft: rgba(63, 185, 80, 0.12);
    --red: #f85149;
    --red-soft: rgba(248, 81, 73, 0.12);
    --yellow: #d29922;
    --yellow-soft: rgba(210, 153, 34, 0.15);
    --purple: #a371f7;
    --orange: #f0883e;
  }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Inter", sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.5;
    -webkit-font-smoothing: antialiased;
    padding: 32px 24px 64px;
  }
  .container { max-width: 1280px; margin: 0 auto; }

  /* Header */
  .header {
    margin-bottom: 32px;
    padding-bottom: 24px;
    border-bottom: 1px solid var(--border);
  }
  .header-top { display: flex; align-items: flex-start; justify-content: space-between; flex-wrap: wrap; gap: 12px; }
  .header h1 { font-size: 28px; font-weight: 700; letter-spacing: -0.5px; margin-bottom: 6px; }
  .header .subtitle { color: var(--text-dim); font-size: 14px; }
  .header .meta { display: flex; gap: 24px; margin-top: 16px; flex-wrap: wrap; }
  .header .meta-item { font-size: 13px; color: var(--text-dim); }
  .header .meta-item strong { color: var(--text); font-weight: 600; }
  .logo-badge {
    background: linear-gradient(135deg, #6ea8fe22, #a371f722);
    border: 1px solid #3a4553;
    border-radius: 10px;
    padding: 10px 18px;
    font-size: 13px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 0.5px;
  }

  /* Section title */
  .section-title {
    font-size: 12px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--text-faint);
    margin: 40px 0 16px;
  }

  /* KPI grid */
  .kpi-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 16px; }
  .kpi {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px 22px;
    transition: all 0.15s;
  }
  .kpi:hover { background: var(--bg-card-hover); border-color: #3a4553; }
  .kpi .label { font-size: 12px; color: var(--text-dim); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 8px; font-weight: 500; }
  .kpi .value { font-size: 28px; font-weight: 700; letter-spacing: -0.5px; line-height: 1.1; }
  .kpi .value .currency { font-size: 18px; color: var(--text-dim); margin-left: 4px; }
  .kpi .sub { font-size: 12px; color: var(--text-dim); margin-top: 8px; }
  .kpi.green .value { color: var(--green); }
  .kpi.red .value { color: var(--red); }
  .kpi.blue .value { color: var(--accent); }
  .kpi.purple .value { color: var(--purple); }
  .kpi.yellow .value { color: var(--yellow); }
  .kpi.orange .value { color: var(--orange); }

  /* Card */
  .card { background: var(--bg-card); border: 1px solid var(--border); border-radius: 12px; padding: 24px; margin-bottom: 16px; }
  .card h3 { font-size: 16px; font-weight: 600; margin-bottom: 16px; }
  .card-grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .card-grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
  @media (max-width: 900px) { .card-grid-2, .card-grid-3 { grid-template-columns: 1fr; } }

  /* Bar chart */
  .chart { display: flex; align-items: flex-end; gap: 8px; height: 220px; padding: 16px 0 8px; border-bottom: 1px solid var(--border); }
  .chart .month { flex: 1; display: flex; flex-direction: column; align-items: center; height: 100%; justify-content: flex-end; gap: 2px; }
  .chart .bars { display: flex; gap: 3px; align-items: flex-end; height: 100%; width: 100%; justify-content: center; }
  .chart .bar { width: 16px; border-radius: 4px 4px 0 0; transition: opacity 0.2s; position: relative; cursor: default; min-height: 2px; }
  .chart .bar:hover { opacity: 0.8; }
  .chart .bar.income { background: linear-gradient(180deg, #4cc266, #3fb950); }
  .chart .bar.expense { background: linear-gradient(180deg, #ff6b63, #f85149); }
  .chart .bar .tooltip {
    position: absolute; bottom: 100%; left: 50%; transform: translateX(-50%);
    background: #000; color: #fff; font-size: 11px; padding: 4px 8px;
    border-radius: 4px; white-space: nowrap; opacity: 0; pointer-events: none;
    transition: opacity 0.15s; margin-bottom: 4px;
  }
  .chart .bar:hover .tooltip { opacity: 1; }
  .chart-labels { display: flex; gap: 8px; margin-top: 8px; }
  .chart-labels .month-label { flex: 1; text-align: center; font-size: 10px; color: var(--text-dim); }
  .legend { display: flex; gap: 16px; margin-top: 12px; font-size: 12px; color: var(--text-dim); }
  .legend-item { display: flex; align-items: center; gap: 6px; }
  .legend-dot { width: 10px; height: 10px; border-radius: 2px; }
  .legend-dot.income { background: #3fb950; }
  .legend-dot.expense { background: #f85149; }

  /* Donut-style tipo breakdown */
  .tipo-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .tipo-item { background: rgba(255,255,255,0.03); border-radius: 8px; padding: 14px 16px; border: 1px solid var(--border); }
  .tipo-label { font-size: 12px; color: var(--text-dim); margin-bottom: 4px; }
  .tipo-value { font-size: 20px; font-weight: 700; color: var(--text); }
  .tipo-sub { font-size: 11px; color: var(--text-faint); margin-top: 2px; }
  .tipo-bar-wrap { background: rgba(255,255,255,0.06); height: 4px; border-radius: 2px; margin-top: 10px; overflow: hidden; }
  .tipo-bar { height: 100%; border-radius: 2px; }
  .tipo-bar.cuotas { background: var(--green); }
  .tipo-bar.bonos { background: var(--accent); }
  .tipo-bar.nutricion { background: var(--purple); }
  .tipo-bar.empresa { background: var(--orange); }

  /* Table */
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  th, td { text-align: left; padding: 10px 8px; border-bottom: 1px solid var(--border); }
  th { color: var(--text-dim); font-weight: 500; text-transform: uppercase; font-size: 11px; letter-spacing: 0.5px; }
  td.num { text-align: right; font-variant-numeric: tabular-nums; }
  th.num { text-align: right; }
  tr:last-child td { border-bottom: none; }
  tbody tr:hover { background: rgba(255,255,255,0.02); }

  /* Cliente bars */
  .cliente-row { display: grid; grid-template-columns: 1fr 80px; gap: 12px; align-items: center; margin-bottom: 14px; }
  .cliente-info { min-width: 0; }
  .cliente-nombre { font-weight: 500; font-size: 13px; margin-bottom: 4px; display: flex; justify-content: space-between; align-items: baseline; flex-wrap: wrap; gap: 4px; }
  .cliente-importe { color: var(--text-dim); font-size: 12px; font-variant-numeric: tabular-nums; font-weight: 400; }
  .cliente-bar-wrap { background: rgba(255,255,255,0.05); height: 5px; border-radius: 3px; overflow: hidden; }
  .cliente-bar { height: 100%; background: linear-gradient(90deg, var(--accent), var(--purple)); border-radius: 3px; }
  .cliente-pct { font-size: 12px; color: var(--text-dim); text-align: right; font-variant-numeric: tabular-nums; }

  /* Alerts */
  .alert { display: flex; gap: 12px; padding: 14px 16px; border-radius: 8px; margin-bottom: 10px; font-size: 13px; border-left: 3px solid; }
  .alert .icon { font-size: 16px; flex-shrink: 0; }
  .alert.info { background: rgba(110, 168, 254, 0.08); border-color: var(--accent); }
  .alert.warning { background: var(--yellow-soft); border-color: var(--yellow); }
  .alert.success { background: var(--green-soft); border-color: var(--green); }
  .alert.danger { background: var(--red-soft); border-color: var(--red); }
  .alert strong { color: var(--text); }

  /* Badge */
  .badge { display: inline-block; padding: 2px 8px; border-radius: 4px; font-size: 11px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.3px; }
  .badge.ingreso { background: var(--green-soft); color: var(--green); }
  .badge.gasto { background: var(--red-soft); color: var(--red); }

  .neg { color: var(--red); }
  .pos { color: var(--green); }

  /* Footer */
  .footer { margin-top: 48px; padding-top: 24px; border-top: 1px solid var(--border); font-size: 12px; color: var(--text-faint); text-align: center; }

  @media print {
    body { background: white; color: black; padding: 16px; }
    .card, .kpi { background: white; border-color: #ccc; }
  }
</style>
</head>
<body>
<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="header-top">
      <div>
        <h1>Dashboard de Facturación</h1>
        <div class="subtitle">PersonalFit · NIF 32456789-B · Entrenamiento personal individual · Ourense</div>
      </div>
      <div class="logo-badge">PERSONALFIT</div>
    </div>
    <div class="meta">
      <div class="meta-item"><strong>Periodo:</strong> enero — diciembre 2025</div>
      <div class="meta-item"><strong>41 facturas procesadas</strong> (25 ingresos + 16 gastos)</div>
      <div class="meta-item"><strong>10 clientes</strong> (9 particulares + 1 empresa)</div>
      <div class="meta-item"><strong>0 errores</strong> de extracción</div>
    </div>
  </div>

  <!-- KPIs -->
  <div class="section-title">Resumen ejecutivo 2025</div>
  <div class="kpi-grid">
    <div class="kpi green">
      <div class="label">Facturación neta</div>
      <div class="value">15.430,00<span class="currency">€</span></div>
      <div class="sub">25 facturas · ticket medio 617,20 €</div>
    </div>
    <div class="kpi red">
      <div class="label">Gastos netos</div>
      <div class="value">7.720,00<span class="currency">€</span></div>
      <div class="sub">16 facturas recibidas</div>
    </div>
    <div class="kpi blue">
      <div class="label">Beneficio bruto</div>
      <div class="value">7.710,00<span class="currency">€</span></div>
      <div class="sub">Margen 49,97 %</div>
    </div>
    <div class="kpi yellow">
      <div class="label">IVA a liquidar</div>
      <div class="value">1.680,00<span class="currency">€</span></div>
      <div class="sub">3.240,30 € repercutido − 1.560,30 € soportado</div>
    </div>
    <div class="kpi purple">
      <div class="label">IRPF retenido</div>
      <div class="value">162,00<span class="currency">€</span></div>
      <div class="sub">Solo facturas a empresa (Clínica Dental)</div>
    </div>
    <div class="kpi orange">
      <div class="label">Clientes activos (pico)</div>
      <div class="value">7</div>
      <div class="sub">Junio y sept. · mínimo 3 (agosto)</div>
    </div>
  </div>

  <!-- TIPOS DE INGRESO -->
  <div class="section-title">Composición de ingresos</div>
  <div class="card">
    <h3>Desglose por tipo de servicio</h3>
    <div class="tipo-grid">
      <div class="tipo-item">
        <div class="tipo-label">Cuotas mensuales</div>
        <div class="tipo-value">9.750,00 €</div>
        <div class="tipo-sub">63,2 % del total · 12 facturas grupales</div>
        <div class="tipo-bar-wrap"><div class="tipo-bar cuotas" style="width: 100%"></div></div>
      </div>
      <div class="tipo-item">
        <div class="tipo-label">Bonos de sesiones</div>
        <div class="tipo-value">4.000,00 €</div>
        <div class="tipo-sub">25,9 % del total · 8 bonos × 500 €</div>
        <div class="tipo-bar-wrap"><div class="tipo-bar bonos" style="width: 41.03%"></div></div>
      </div>
      <div class="tipo-item">
        <div class="tipo-label">Cliente empresa</div>
        <div class="tipo-value">1.080,00 €</div>
        <div class="tipo-sub">7,0 % del total · 2 programas bienestar</div>
        <div class="tipo-bar-wrap"><div class="tipo-bar empresa" style="width: 11.08%"></div></div>
      </div>
      <div class="tipo-item">
        <div class="tipo-label">Asesoramiento nutricional</div>
        <div class="tipo-value">600,00 €</div>
        <div class="tipo-sub">3,9 % del total · 3 planes × 200 €</div>
        <div class="tipo-bar-wrap"><div class="tipo-bar nutricion" style="width: 6.15%"></div></div>
      </div>
    </div>
  </div>

  <!-- EVOLUCIÓN MENSUAL -->
  <div class="section-title">Evolución mensual</div>
  <div class="card">
    <h3>Ingresos vs gastos mes a mes (base imponible) — escala máx. 2.300 €</h3>
    <div class="chart">
      <!-- Jan: in 1100, exp 2215 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:47.83%"><div class="tooltip">Ingresos: 1.100 €</div></div>
          <div class="bar expense" style="height:96.30%"><div class="tooltip">Gastos: 2.215 €</div></div>
        </div>
      </div>
      <!-- Feb: in 1250, exp 0 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:54.35%"><div class="tooltip">Ingresos: 1.250 €</div></div>
          <div class="bar expense" style="height:0%"><div class="tooltip">Gastos: 0 €</div></div>
        </div>
      </div>
      <!-- Mar: in 1100, exp 95 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:47.83%"><div class="tooltip">Ingresos: 1.100 €</div></div>
          <div class="bar expense" style="height:4.13%"><div class="tooltip">Gastos: 95 €</div></div>
        </div>
      </div>
      <!-- Apr: in 1250, exp 1425 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:54.35%"><div class="tooltip">Ingresos: 1.250 €</div></div>
          <div class="bar expense" style="height:61.96%"><div class="tooltip">Gastos: 1.425 €</div></div>
        </div>
      </div>
      <!-- May: in 1400, exp 185 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:60.87%"><div class="tooltip">Ingresos: 1.400 €</div></div>
          <div class="bar expense" style="height:8.04%"><div class="tooltip">Gastos: 185 €</div></div>
        </div>
      </div>
      <!-- Jun: in 2090, exp 320 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:90.87%"><div class="tooltip">Ingresos: 2.090 €</div></div>
          <div class="bar expense" style="height:13.91%"><div class="tooltip">Gastos: 320 €</div></div>
        </div>
      </div>
      <!-- Jul: in 950, exp 1735 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:41.30%"><div class="tooltip">Ingresos: 950 €</div></div>
          <div class="bar expense" style="height:75.43%"><div class="tooltip">Gastos: 1.735 €</div></div>
        </div>
      </div>
      <!-- Aug: in 450, exp 0 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:19.57%"><div class="tooltip">Ingresos: 450 €</div></div>
          <div class="bar expense" style="height:0%"><div class="tooltip">Gastos: 0 €</div></div>
        </div>
      </div>
      <!-- Sep: in 1550, exp 0 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:67.39%"><div class="tooltip">Ingresos: 1.550 €</div></div>
          <div class="bar expense" style="height:0%"><div class="tooltip">Gastos: 0 €</div></div>
        </div>
      </div>
      <!-- Oct: in 1400, exp 1425 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:60.87%"><div class="tooltip">Ingresos: 1.400 €</div></div>
          <div class="bar expense" style="height:61.96%"><div class="tooltip">Gastos: 1.425 €</div></div>
        </div>
      </div>
      <!-- Nov: in 1100, exp 0 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:47.83%"><div class="tooltip">Ingresos: 1.100 €</div></div>
          <div class="bar expense" style="height:0%"><div class="tooltip">Gastos: 0 €</div></div>
        </div>
      </div>
      <!-- Dec: in 1790, exp 320 -->
      <div class="month">
        <div class="bars">
          <div class="bar income" style="height:77.83%"><div class="tooltip">Ingresos: 1.790 €</div></div>
          <div class="bar expense" style="height:13.91%"><div class="tooltip">Gastos: 320 €</div></div>
        </div>
      </div>
    </div>
    <div class="chart-labels">
      <div class="month-label">Ene</div>
      <div class="month-label">Feb</div>
      <div class="month-label">Mar</div>
      <div class="month-label">Abr</div>
      <div class="month-label">May</div>
      <div class="month-label">Jun</div>
      <div class="month-label">Jul</div>
      <div class="month-label">Ago</div>
      <div class="month-label">Sep</div>
      <div class="month-label">Oct</div>
      <div class="month-label">Nov</div>
      <div class="month-label">Dic</div>
    </div>
    <div class="legend">
      <div class="legend-item"><div class="legend-dot income"></div>Ingresos</div>
      <div class="legend-item"><div class="legend-dot expense"></div>Gastos (pago trimestral alquiler y gestoría)</div>
    </div>
  </div>

  <!-- IVA + CLIENTES -->
  <div class="card-grid-2">
    <div class="card">
      <h3>Liquidación de IVA por trimestre</h3>
      <table>
        <thead>
          <tr>
            <th>Trimestre</th>
            <th class="num">Repercutido</th>
            <th class="num">Soportado</th>
            <th class="num">A liquidar</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>Q1 2025</strong></td>
            <td class="num">724,50 €</td>
            <td class="num">424,20 €</td>
            <td class="num"><strong>300,30 €</strong></td>
          </tr>
          <tr>
            <td><strong>Q2 2025</strong></td>
            <td class="num">995,40 €</td>
            <td class="num">405,30 €</td>
            <td class="num"><strong>590,10 €</strong></td>
          </tr>
          <tr>
            <td><strong>Q3 2025</strong></td>
            <td class="num">619,50 €</td>
            <td class="num">364,35 €</td>
            <td class="num"><strong>255,15 €</strong></td>
          </tr>
          <tr>
            <td><strong>Q4 2025</strong></td>
            <td class="num">900,90 €</td>
            <td class="num">366,45 €</td>
            <td class="num"><strong>534,45 €</strong></td>
          </tr>
          <tr style="border-top: 2px solid var(--border);">
            <td><strong>Total</strong></td>
            <td class="num"><strong>3.240,30 €</strong></td>
            <td class="num"><strong>1.560,30 €</strong></td>
            <td class="num"><strong style="color: var(--yellow);">1.680,00 €</strong></td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="card">
      <h3>Top clientes por facturación (base)</h3>
      <div class="cliente-row">
        <div class="cliente-info">
          <div class="cliente-nombre">Laura Sánchez Vázquez <span class="cliente-importe">2.500 € · 3 facturas</span></div>
          <div class="cliente-bar-wrap"><div class="cliente-bar" style="width: 100%"></div></div>
        </div>
        <div class="cliente-pct">16,20 %</div>
      </div>
      <div class="cliente-row">
        <div class="cliente-info">
          <div class="cliente-nombre">Carlos López Fernández <span class="cliente-importe">2.300 € · 2 facturas</span></div>
          <div class="cliente-bar-wrap"><div class="cliente-bar" style="width: 92%"></div></div>
        </div>
        <div class="cliente-pct">14,91 %</div>
      </div>
      <div class="cliente-row">
        <div class="cliente-info">
          <div class="cliente-nombre">Javier Gómez Novo <span class="cliente-importe">2.050 € · 2 facturas</span></div>
          <div class="cliente-bar-wrap"><div class="cliente-bar" style="width: 82%"></div></div>
        </div>
        <div class="cliente-pct">13,29 %</div>
      </div>
      <div class="cliente-row">
        <div class="cliente-info">
          <div class="cliente-nombre">María Rodríguez García <span class="cliente-importe">2.000 € · 2 facturas</span></div>
          <div class="cliente-bar-wrap"><div class="cliente-bar" style="width: 80%"></div></div>
        </div>
        <div class="cliente-pct">12,96 %</div>
      </div>
      <div class="cliente-row">
        <div class="cliente-info">
          <div class="cliente-nombre">Ana Martínez Pérez <span class="cliente-importe">2.000 € · 2 facturas</span></div>
          <div class="cliente-bar-wrap"><div class="cliente-bar" style="width: 80%"></div></div>
        </div>
        <div class="cliente-pct">12,96 %</div>
      </div>
    </div>
  </div>

  <!-- GASTOS DESGLOSE -->
  <div class="section-title">Estructura de gastos</div>
  <div class="card">
    <h3>Gastos por categoría (base imponible)</h3>
    <table>
      <thead>
        <tr>
          <th>Categoría</th>
          <th class="num">Base</th>
          <th class="num">% s/gastos</th>
          <th class="num">% s/ingresos</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Alquiler sala entrenamiento</td>
          <td class="num">4.800,00 €</td>
          <td class="num">62,18 %</td>
          <td class="num">31,11 %</td>
        </tr>
        <tr>
          <td>Gestoría / asesoría fiscal</td>
          <td class="num">900,00 €</td>
          <td class="num">11,66 %</td>
          <td class="num">5,83 %</td>
        </tr>
        <tr>
          <td>Suministro eléctrico</td>
          <td class="num">630,00 €</td>
          <td class="num">8,16 %</td>
          <td class="num">4,08 %</td>
        </tr>
        <tr>
          <td>Material deportivo</td>
          <td class="num">505,00 €</td>
          <td class="num">6,54 %</td>
          <td class="num">3,27 %</td>
        </tr>
        <tr>
          <td>Seguro RC entrenador personal</td>
          <td class="num">290,00 €</td>
          <td class="num">3,75 %</td>
          <td class="num">1,88 %</td>
        </tr>
        <tr>
          <td>Formación (nutrición deportiva)</td>
          <td class="num">320,00 €</td>
          <td class="num">4,14 %</td>
          <td class="num">2,07 %</td>
        </tr>
        <tr>
          <td>Plataforma gestión clientes</td>
          <td class="num">180,00 €</td>
          <td class="num">2,33 %</td>
          <td class="num">1,17 %</td>
        </tr>
        <tr>
          <td>Hosting web y dominio</td>
          <td class="num">95,00 €</td>
          <td class="num">1,23 %</td>
          <td class="num">0,62 %</td>
        </tr>
        <tr style="border-top: 2px solid var(--border);">
          <td><strong>Total gastos</strong></td>
          <td class="num"><strong>7.720,00 €</strong></td>
          <td class="num"><strong>100 %</strong></td>
          <td class="num"><strong>50,03 %</strong></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- ALERTAS -->
  <div class="section-title">Análisis y observaciones</div>
  <div class="card">
    <div class="alert warning">
      <span class="icon">!</span>
      <div><strong>Agosto crítico.</strong> Solo 450 € de ingresos (−78 % vs junio). Es el comportamiento típico de negocios de fitness en Galicia en verano. Considerar bonos de "verano" o contratos de continuidad para reducir este bache.</div>
    </div>
    <div class="alert success">
      <span class="icon">↗</span>
      <div><strong>Vuelta de vacaciones muy fuerte.</strong> Septiembre repunta a 1.550 € (+244 % vs agosto) con 7 clientes activos. La gestión de la espera y los recordatorios pre-septiembre están funcionando.</div>
    </div>
    <div class="alert warning">
      <span class="icon">!</span>
      <div><strong>El alquiler se lleva el 62 % de los gastos</strong> (4.800 €/año). Con el margen actual del 50 %, cualquier subida del arrendamiento impacta directamente en beneficio. Valorar renegociar o explorar espacios alternativos.</div>
    </div>
    <div class="alert info">
      <span class="icon">i</span>
      <div><strong>Ingresos recurrentes sólidos:</strong> las cuotas mensuales representan el 63,2 % de la facturación. Base estable. El siguiente palanca de crecimiento es convertir los compradores de bonos en clientes de cuota fija.</div>
    </div>
    <div class="alert info">
      <span class="icon">i</span>
      <div><strong>Asesoramiento nutricional infrautilizado:</strong> solo 600 € (3,9 %). Con la formación completada en junio, hay margen para sistematizar este servicio y aumentar el ticket medio por cliente.</div>
    </div>
    <div class="alert info">
      <span class="icon">i</span>
      <div><strong>IRPF retenido:</strong> 162 € (solo facturas a empresa). Como autónomo con clientes mayoritariamente particulares, el grueso del IRPF se declara directamente en la renta anual, no vía retenciones.</div>
    </div>
    <div class="alert info">
      <span class="icon">i</span>
      <div><strong>Mejor mes:</strong> junio 2025 con 2.090 € (cuotas + bono + programa empresa) · <strong>Peor mes:</strong> agosto con 450 €.</div>
    </div>
  </div>

  <!-- DETALLE FACTURAS -->
  <div class="section-title">Detalle de facturas</div>
  <div class="card">
    <table>
      <thead>
        <tr>
          <th>Tipo</th>
          <th>Fecha</th>
          <th>Nº</th>
          <th>Cliente / Proveedor</th>
          <th>Concepto</th>
          <th class="num">Base</th>
          <th class="num">IVA</th>
          <th class="num">IRPF</th>
          <th class="num">Total</th>
        </tr>
      </thead>
      <tbody>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/01/25</td><td>PF-2025-001</td><td>Varios particulares</td><td>Cuotas enero (4 clientes)</td><td class="num">600,00</td><td class="num">126,00</td><td class="num">—</td><td class="num"><strong>726,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>02/01/25</td><td>ALQ-Q1-2025</td><td>Inmobiliaria Gestión Ourense</td><td>Alquiler sala Q1</td><td class="num">1.200,00</td><td class="num">252,00</td><td class="num">—</td><td class="num"><strong>1.452,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>08/01/25</td><td>SEG-2025-001</td><td>MAPFRE España</td><td>Seguro RC anual</td><td class="num">290,00</td><td class="num">0,00</td><td class="num">—</td><td class="num"><strong>290,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>15/01/25</td><td>MAT-2025-001</td><td>Decathlon Ourense</td><td>Material deportivo (inicio)</td><td class="num">320,00</td><td class="num">67,20</td><td class="num">—</td><td class="num"><strong>387,20</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>20/01/25</td><td>PLT-2025-001</td><td>TrueCoach Inc</td><td>Plataforma gestión clientes anual</td><td class="num">180,00</td><td class="num">37,80</td><td class="num">—</td><td class="num"><strong>217,80</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>31/01/25</td><td>GES-Q1-2025</td><td>Asesoría Gestión Galicia</td><td>Gestoría Q1</td><td class="num">225,00</td><td class="num">47,25</td><td class="num">—</td><td class="num"><strong>272,25</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>15/01/25</td><td>PF-2025-002</td><td>Laura Sánchez Vázquez</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/02/25</td><td>PF-2025-003</td><td>Varios particulares</td><td>Cuotas febrero (5 clientes)</td><td class="num">750,00</td><td class="num">157,50</td><td class="num">—</td><td class="num"><strong>907,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>12/02/25</td><td>PF-2025-004</td><td>Javier Gómez Novo</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>10/03/25</td><td>WEB-2025-001</td><td>Hostinger UAB</td><td>Hosting web + dominio anual</td><td class="num">95,00</td><td class="num">19,95</td><td class="num">—</td><td class="num"><strong>114,95</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/03/25</td><td>PF-2025-005</td><td>Varios particulares</td><td>Cuotas marzo (6 clientes)</td><td class="num">900,00</td><td class="num">189,00</td><td class="num">—</td><td class="num"><strong>1.089,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>10/03/25</td><td>PF-2025-006</td><td>Pilar Fernández Cid</td><td>Plan nutricional 1 mes</td><td class="num">200,00</td><td class="num">42,00</td><td class="num">—</td><td class="num"><strong>242,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>01/04/25</td><td>ALQ-Q2-2025</td><td>Inmobiliaria Gestión Ourense</td><td>Alquiler sala Q2</td><td class="num">1.200,00</td><td class="num">252,00</td><td class="num">—</td><td class="num"><strong>1.452,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/04/25</td><td>PF-2025-007</td><td>Varios particulares</td><td>Cuotas abril (5 clientes)</td><td class="num">750,00</td><td class="num">157,50</td><td class="num">—</td><td class="num"><strong>907,50</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>30/04/25</td><td>GES-Q2-2025</td><td>Asesoría Gestión Galicia</td><td>Gestoría Q2</td><td class="num">225,00</td><td class="num">47,25</td><td class="num">—</td><td class="num"><strong>272,25</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>18/04/25</td><td>PF-2025-008</td><td>Elena Vázquez Novo</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/05/25</td><td>PF-2025-009</td><td>Varios particulares</td><td>Cuotas mayo (6 clientes)</td><td class="num">900,00</td><td class="num">189,00</td><td class="num">—</td><td class="num"><strong>1.089,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>12/05/25</td><td>MAT-2025-002</td><td>Amazon Spain</td><td>Material deportivo adicional</td><td class="num">185,00</td><td class="num">38,85</td><td class="num">—</td><td class="num"><strong>223,85</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>15/05/25</td><td>PF-2025-010</td><td>David Blanco Seoane</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/06/25</td><td>PF-2025-011</td><td>Varios particulares</td><td>Cuotas junio (7 clientes)</td><td class="num">1.050,00</td><td class="num">220,50</td><td class="num">—</td><td class="num"><strong>1.270,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>10/06/25</td><td>PF-2025-012</td><td>Laura Sánchez Vázquez</td><td>Bono 10 sesiones (2.º)</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>20/06/25</td><td>FOR-2025-001</td><td>Instituto Europeo Fitness</td><td>Curso nutrición deportiva</td><td class="num">320,00</td><td class="num">67,20</td><td class="num">—</td><td class="num"><strong>387,20</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>30/06/25</td><td>PF-2025-013</td><td>Clínica Dental Rodríguez SL</td><td>Programa bienestar empresa Q2</td><td class="num">540,00</td><td class="num">113,40</td><td class="num neg">−81,00</td><td class="num"><strong>572,40</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>01/07/25</td><td>ALQ-Q3-2025</td><td>Inmobiliaria Gestión Ourense</td><td>Alquiler sala Q3</td><td class="num">1.200,00</td><td class="num">252,00</td><td class="num">—</td><td class="num"><strong>1.452,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>15/07/25</td><td>LUZ-2025-H1</td><td>Naturgy Iberia</td><td>Electricidad sala ene–jun</td><td class="num">310,00</td><td class="num">65,10</td><td class="num">—</td><td class="num"><strong>375,10</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>31/07/25</td><td>GES-Q3-2025</td><td>Asesoría Gestión Galicia</td><td>Gestoría Q3</td><td class="num">225,00</td><td class="num">47,25</td><td class="num">—</td><td class="num"><strong>272,25</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/07/25</td><td>PF-2025-014</td><td>Varios particulares</td><td>Cuotas julio (5 clientes)</td><td class="num">750,00</td><td class="num">157,50</td><td class="num">—</td><td class="num"><strong>907,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>20/07/25</td><td>PF-2025-015</td><td>María Rodríguez García</td><td>Plan nutricional 1 mes</td><td class="num">200,00</td><td class="num">42,00</td><td class="num">—</td><td class="num"><strong>242,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/08/25</td><td>PF-2025-016</td><td>Varios particulares</td><td>Cuotas agosto (3 clientes)</td><td class="num">450,00</td><td class="num">94,50</td><td class="num">—</td><td class="num"><strong>544,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/09/25</td><td>PF-2025-017</td><td>Varios particulares</td><td>Cuotas septiembre (7 clientes)</td><td class="num">1.050,00</td><td class="num">220,50</td><td class="num">—</td><td class="num"><strong>1.270,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>20/09/25</td><td>PF-2025-018</td><td>Carlos López Fernández</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>01/10/25</td><td>ALQ-Q4-2025</td><td>Inmobiliaria Gestión Ourense</td><td>Alquiler sala Q4</td><td class="num">1.200,00</td><td class="num">252,00</td><td class="num">—</td><td class="num"><strong>1.452,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/10/25</td><td>PF-2025-019</td><td>Varios particulares</td><td>Cuotas octubre (6 clientes)</td><td class="num">900,00</td><td class="num">189,00</td><td class="num">—</td><td class="num"><strong>1.089,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>15/10/25</td><td>PF-2025-020</td><td>Roberto Iglesias Durán</td><td>Bono 10 sesiones</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>31/10/25</td><td>GES-Q4-2025</td><td>Asesoría Gestión Galicia</td><td>Gestoría Q4</td><td class="num">225,00</td><td class="num">47,25</td><td class="num">—</td><td class="num"><strong>272,25</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/11/25</td><td>PF-2025-021</td><td>Varios particulares</td><td>Cuotas noviembre (6 clientes)</td><td class="num">900,00</td><td class="num">189,00</td><td class="num">—</td><td class="num"><strong>1.089,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>18/11/25</td><td>PF-2025-022</td><td>Ana Martínez Pérez</td><td>Plan nutricional 1 mes</td><td class="num">200,00</td><td class="num">42,00</td><td class="num">—</td><td class="num"><strong>242,00</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>05/12/25</td><td>PF-2025-023</td><td>Varios particulares</td><td>Cuotas diciembre (5 clientes)</td><td class="num">750,00</td><td class="num">157,50</td><td class="num">—</td><td class="num"><strong>907,50</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>10/12/25</td><td>PF-2025-024</td><td>Javier Gómez Novo</td><td>Bono 10 sesiones (2.º)</td><td class="num">500,00</td><td class="num">105,00</td><td class="num">—</td><td class="num"><strong>605,00</strong></td></tr>
        <tr><td><span class="badge gasto">Gasto</span></td><td>20/12/25</td><td>LUZ-2025-H2</td><td>Naturgy Iberia</td><td>Electricidad sala jul–dic</td><td class="num">320,00</td><td class="num">67,20</td><td class="num">—</td><td class="num"><strong>387,20</strong></td></tr>
        <tr><td><span class="badge ingreso">Ingreso</span></td><td>28/12/25</td><td>PF-2025-025</td><td>Clínica Dental Rodríguez SL</td><td>Programa bienestar empresa Q4</td><td class="num">540,00</td><td class="num">113,40</td><td class="num neg">−81,00</td><td class="num"><strong>572,40</strong></td></tr>
      </tbody>
    </table>
  </div>

  <div class="footer">
    Generado el 21 de mayo de 2026 · Datos simulados para <strong>PersonalFit</strong> · Ourense · ejercicio fiscal 2025
  </div>

</div>
</body>
</html>
