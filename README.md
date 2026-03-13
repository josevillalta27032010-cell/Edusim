<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1">
<meta name="theme-color" content="#070b18">
<title>Atlas</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{--bg:#070b18;--bg2:#0d1225;--bg3:#111829;--card:#141c2e;--bd:#1e2a42;--ac:#3b82f6;--ac2:#8b5cf6;--gold:#f59e0b;--gr:#10b981;--re:#ef4444;--tx:#e2e8f0;--tx2:#94a3b8;--tx3:#64748b}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'DM Sans',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh;overflow-x:hidden}
canvas{position:fixed;top:0;left:0;z-index:0;pointer-events:none}
nav{position:fixed;top:0;left:0;right:0;z-index:100;background:rgba(7,11,24,.96);border-bottom:1px solid var(--bd);height:48px;display:flex;align-items:center;padding:0 8px;gap:2px;overflow-x:auto}
nav::-webkit-scrollbar{display:none}
.logo{font-family:'Syne',sans-serif;font-weight:800;font-size:16px;color:var(--ac);letter-spacing:2px;margin-right:6px;flex-shrink:0}
.nb{flex-shrink:0;background:none;border:none;color:var(--tx2);font-size:11px;letter-spacing:.8px;text-transform:uppercase;padding:5px 8px;border-radius:6px;cursor:pointer;white-space:nowrap}
.nb:hover{color:var(--tx);background:var(--bg3)}
.nb.on{color:var(--ac);background:rgba(59,130,246,.1)}
.pg{display:none;padding:60px 12px 80px;position:relative;z-index:1;min-height:100vh}
.pg.on{display:block}
.hero{text-align:center;padding:24px 0 16px}
.hero h1{font-family:'Syne',sans-serif;font-weight:800;font-size:42px;letter-spacing:3px;background:linear-gradient(135deg,#60a5fa,#a78bfa,#22d3ee);-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.hero p{color:var(--tx2);font-size:11px;margin-top:6px}
.srow{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin:14px 0}
.sc{background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:12px 6px;text-align:center}
.sv{font-family:'Syne',sans-serif;font-size:20px;font-weight:700;color:var(--ac)}
.sl{font-size:9px;color:var(--tx3);letter-spacing:1px;text-transform:uppercase;margin-top:2px}
.sec{font-family:'Syne',sans-serif;font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--tx2);margin:14px 0 8px;padding-bottom:5px;border-bottom:1px solid var(--bd)}
.sw{position:relative;margin-bottom:8px}
.sw input{width:100%;background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:10px 36px 10px 12px;color:var(--tx);font-size:13px;outline:none}
.sw input:focus{border-color:var(--ac)}
.si{position:absolute;right:10px;top:50%;transform:translateY(-50%);color:var(--tx3)}
.pills{display:flex;gap:5px;overflow-x:auto;padding-bottom:6px;margin-bottom:10px}
.pills::-webkit-scrollbar{display:none}
.pill{flex-shrink:0;background:var(--card);border:1px solid var(--bd);border-radius:20px;padding:4px 11px;font-size:11px;color:var(--tx2);cursor:pointer;transition:.2s;white-space:nowrap}
.pill.on,.pill:hover{background:var(--ac);border-color:var(--ac);color:#fff}
.sgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:7px}
.sc2{background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;transition:.2s}
.sc2:hover{border-color:var(--ac);transform:translateY(-2px)}
.sc2 .si2{font-size:20px;margin-bottom:3px}
.sc2 .sn{font-size:9px;color:var(--tx2);letter-spacing:.5px;text-transform:uppercase;line-height:1.3}
select,textarea,input[type=text]{width:100%;background:var(--bg3);border:1px solid var(--bd);border-radius:8px;padding:10px 12px;color:var(--tx);font-family:'DM Sans',sans-serif;font-size:13px;outline:none;line-height:1.5}
textarea{resize:vertical}
select:focus,textarea:focus,input[type=text]:focus{border-color:var(--ac)}
::placeholder{color:var(--tx3)}
.btn{width:100%;background:linear-gradient(135deg,var(--ac),var(--ac2));border:none;border-radius:10px;padding:13px;color:#fff;font-family:'Syne',sans-serif;font-size:13px;letter-spacing:1px;cursor:pointer;margin-top:8px;transition:.2s}
.btn:hover{transform:translateY(-1px);box-shadow:0 4px 20px rgba(59,130,246,.3)}
.btn2{background:var(--card);border:1px solid var(--bd);border-radius:8px;padding:9px 12px;color:var(--tx2);font-size:12px;cursor:pointer;transition:.2s;text-align:center}
.btn2.on,.btn2:hover{border-color:var(--ac);color:var(--ac);background:rgba(59,130,246,.08)}
.dr{display:flex;gap:6px;margin-bottom:8px}
.dr .btn2{flex:1}
.mg{display:grid;grid-template-columns:repeat(2,1fr);gap:7px;margin-bottom:10px}
.mc{background:var(--card);border:2px solid var(--bd);border-radius:10px;padding:12px 8px;text-align:center;cursor:pointer;transition:.2s}
.mc.on,.mc:hover{border-color:var(--ac)}
.mc .mi{font-size:22px;margin-bottom:3px}
.mc .mn{font-size:10px;color:var(--tx2)}
.bbl{background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:12px;margin-bottom:8px;position:relative}
.bbl::before{content:'ATLAS';font-size:9px;color:var(--ac);letter-spacing:2px;display:block;margin-bottom:6px;font-family:monospace}
.bbl p{font-size:13px;line-height:1.7}
.ol{list-style:none;margin-top:8px}
.ol li{background:var(--bg3);border:1px solid var(--bd);border-radius:8px;padding:9px 11px;margin-bottom:5px;font-size:13px;cursor:pointer;transition:.2s}
.ol li:hover{border-color:var(--ac)}
.ol li.ok{border-color:var(--gr)!important;background:rgba(16,185,129,.1);color:var(--gr)}
.ol li.no{border-color:var(--re)!important;background:rgba(239,68,68,.1);color:var(--re)}
.score{text-align:center;padding:20px;background:var(--card);border:1px solid var(--bd);border-radius:12px;margin-bottom:10px}
.snum{font-family:'Syne',sans-serif;font-size:52px;font-weight:800;background:linear-gradient(135deg,var(--ac),var(--ac2));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.tabs{display:flex;gap:5px;margin-bottom:10px;overflow-x:auto}
.tabs::-webkit-scrollbar{display:none}
.tab{flex-shrink:0;background:var(--card);border:1px solid var(--bd);border-radius:8px;padding:6px 12px;font-size:11px;color:var(--tx2);cursor:pointer;transition:.2s}
.tab.on{background:var(--ac);border-color:var(--ac);color:#fff}
.lc{background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:12px;margin-bottom:7px;cursor:pointer;transition:.2s}
.lc:hover{border-color:var(--ac)}
.lc h4{font-family:'Syne',sans-serif;font-size:13px;margin-bottom:3px}
.lc p{font-size:12px;color:var(--tx2);line-height:1.5}
.lc .lm{font-size:10px;color:var(--tx3);margin-top:4px;font-family:monospace}
.hi{background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:10px;margin-bottom:6px;display:flex;justify-content:space-between;align-items:center}
.hs{font-family:'Syne',sans-serif;font-size:16px;font-weight:700;padding:4px 10px;border-radius:7px}
.hs.h{color:var(--gr);background:rgba(16,185,129,.1)}
.hs.m{color:var(--gold);background:rgba(245,158,11,.1)}
.hs.l{color:var(--re);background:rgba(239,68,68,.1)}
.ach{background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:10px;display:flex;align-items:center;gap:10px;margin-bottom:6px}
.ach.ok{border-color:var(--gold);background:rgba(245,158,11,.05)}
.ach.no{opacity:.4;filter:grayscale(1)}
.eg{display:grid;grid-template-columns:1fr 1fr;gap:7px}
.ec{background:rgba(239,68,68,.07);border:1px solid rgba(239,68,68,.25);border-radius:10px;padding:12px 8px;text-align:center;cursor:pointer;transition:.2s}
.ec:hover{border-color:var(--re)}
.ec .ei{font-size:22px;margin-bottom:3px}
.ec p{font-size:10px;color:var(--tx2)}
.ov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.87);z-index:200;padding:16px;align-items:center;justify-content:center}
.ov.on{display:flex}
.md{background:var(--bg2);border:1px solid var(--bd);border-radius:14px;padding:18px;width:100%;max-width:420px;max-height:84vh;overflow-y:auto}
.md h2{font-family:'Syne',sans-serif;font-size:16px;margin-bottom:12px}
.xb{float:right;background:none;border:none;color:var(--tx2);font-size:20px;cursor:pointer;margin-top:-4px}
.pb{background:var(--bd);border-radius:4px;height:4px;margin-bottom:10px}
.pf{background:var(--ac);height:4px;border-radius:4px;width:0%;transition:width .3s}
.sr{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:8px}
.cg{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.cc{background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:14px 10px;cursor:pointer;transition:.2s;text-align:center}
.cc:hover{border-color:var(--gold);transform:translateY(-2px)}
.cc .ci{font-size:24px;margin-bottom:6px}
.cc h4{font-family:'Syne',sans-serif;font-size:12px;color:var(--gold);margin-bottom:2px}
.cc p{font-size:10px;color:var(--tx3);line-height:1.4}
</style>
</head>
<body>
<canvas id="cv"></canvas>
<nav>
  <div class="logo">ATLAS</div>
  <button class="nb on" id="nb-inicio">Inicio</button>
  <button class="nb" id="nb-sim">Simular</button>
  <button class="nb" id="nb-tarea">📝 Tarea</button>
  <button class="nb" id="nb-bib">Biblioteca</button>
  <button class="nb" id="nb-aux">🚨 Aux</button>
  <button class="nb" id="nb-hist">Historial</button>
  <button class="nb" id="nb-prof" style="display:none">Profesor</button>
  <button class="nb" id="nb-crea" style="display:none">⭐</button>
</nav>

<div id="pg-inicio" class="pg on">
  <div class="hero"><h1>ATLAS</h1><p>Educación sin límites · Funciona offline · Sin internet</p></div>
  <div class="srow">
    <div class="sc"><div class="sv" id="stS">0</div><div class="sl">Sesiones</div></div>
    <div class="sc"><div class="sv" id="stA">—</div><div class="sl">Promedio</div></div>
    <div class="sc"><div class="sv" id="stB">—</div><div class="sl">Mejor</div></div>
  </div>
  <div class="sec">TU ROL</div>
  <div class="dr" style="margin-bottom:12px" id="roleBtns">
    <div class="btn2 on" data-role="student">🎓 Estudiante</div>
    <div class="btn2" data-role="teacher">👩‍🏫 Profesor</div>
    <div class="btn2" data-role="creator">⭐ Creador</div>
  </div>
  <div class="sec">MATERIAS</div>
  <div class="sw"><input id="sSearch" placeholder="Buscar materia..."><span class="si">🔍</span></div>
  <div class="pills" id="cPills"></div>
  <div class="sgrid" id="sGrid"></div>
  <div class="sec" style="margin-top:16px">LOGROS</div>
  <div id="achList"></div>
</div>

<div id="pg-sim" class="pg">
  <div class="sec">SIMULADOR</div>
  <div class="tabs" id="simTabs">
    <div class="tab on" data-stab="p">📚 Practicar</div>
    <div class="tab" data-stab="e">📋 Examen</div>
  </div>
  <div id="sTP">
    <div id="s0">
      <div class="sr"><select id="sSub"></select><select id="sLng"><option>Español</option><option>English</option></select></div>
      <div class="dr" id="diffBtns">
        <div class="btn2 on" data-diff="Fácil">Fácil</div>
        <div class="btn2" data-diff="Medio">Medio</div>
        <div class="btn2" data-diff="Difícil">Difícil</div>
      </div>
      <input type="text" id="sTm" placeholder="📌 Tema (ej: Cinemática, Física...)" style="margin-bottom:8px">
      <textarea id="sDe" rows="3" placeholder="📝 Descripción opcional — pega tu apunte..."></textarea>
      <div class="mg" id="modeBtns">
        <div class="mc on" data-mode="m"><div class="mi">🔘</div><div class="mn">10 Opción Múltiple</div></div>
        <div class="mc" data-mode="v"><div class="mi">✅</div><div class="mn">10 Verdadero/Falso</div></div>
        <div class="mc" data-mode="e"><div class="mi">📐</div><div class="mn">Ejercicios</div></div>
        <div class="mc" data-mode="n"><div class="mi">🎬</div><div class="mn">Narración</div></div>
        <div class="mc" data-mode="a"><div class="mi">🎲</div><div class="mn">Al Azar</div></div>
        <div class="mc" data-mode="t"><div class="mi">🎯</div><div class="mn">Del Tema</div></div>
      </div>
      <button class="btn" id="btnStartSim">▶ INICIAR</button>
    </div>
    <div id="s1" style="display:none">
      <div class="pb"><div class="pf" id="sPr"></div></div>
      <div id="sQB"></div>
      <button class="btn" id="sEv" style="display:none">✓ Evaluar</button>
    </div>
    <div id="s2" style="display:none">
      <div class="score"><div class="snum" id="sFin">—</div><div style="font-size:11px;color:var(--tx2)">PUNTUACIÓN</div></div>
      <div class="bbl" id="sFB"><p>Bien hecho.</p></div>
      <button class="btn" id="btnResetSim">Nueva práctica</button>
    </div>
  </div>
  <div id="sTE" style="display:none">
    <div class="bbl"><p>Ingresa los temas y Atlas generará un examen con el contenido disponible.</p></div>
    <input type="text" id="exT" placeholder="Nombre del examen..." style="margin-bottom:8px">
    <textarea id="exTm" rows="4" placeholder="Escribe los temas del examen..."></textarea>
    <div class="sr" style="margin-top:8px">
      <select id="exD"><option>Fácil</option><option selected>Medio</option><option>Difícil</option></select>
      <select id="exC"><option>10 preguntas</option><option selected>20 preguntas</option><option>30 preguntas</option></select>
    </div>
    <button class="btn" id="btnGenExam">📋 GENERAR EXAMEN</button>
    <div id="exO" style="margin-top:10px"></div>
  </div>
</div>

<div id="pg-tarea" class="pg">
  <div class="sec">ASISTENTE DE TAREAS</div>
  <div class="tabs" id="tareaTabs">
    <div class="tab on" data-ttab="x">🎓 Explícame</div>
    <div class="tab" data-ttab="r">✏️ Resolver</div>
  </div>
  <div id="tX">
    <input type="text" id="tNiv" placeholder="Nivel (básico, secundaria, universitario)..." style="margin-bottom:8px">
    <textarea id="tTm" rows="3" placeholder="¿Qué tema quieres que te explique?..."></textarea>
    <button class="btn" id="btnExplicar">🎓 Explicar tema</button>
    <div id="tXO" style="margin-top:10px"></div>
  </div>
  <div id="tR" style="display:none">
    <div class="dr" id="tdBtns">
      <div class="btn2 on" data-td="b">Solo resp.</div>
      <div class="btn2" data-td="d">Paso a paso</div>
      <div class="btn2" data-td="c">Completo</div>
    </div>
    <textarea id="tTx" rows="5" placeholder="Escribe tu ejercicio o pregunta aquí..."></textarea>
    <button class="btn" id="btnResolver">✏️ Resolver</button>
    <div id="tRO" style="margin-top:10px"></div>
  </div>
</div>

<div id="pg-bib" class="pg">
  <div class="sec">BIBLIOTECA</div>
  <div class="sw"><input id="bS" placeholder="Buscar..."><span class="si">🔍</span></div>
  <div class="tabs" id="libTabs">
    <div class="tab on" data-ltab="t">Teoría</div>
    <div class="tab" data-ltab="f">Fórmulas</div>
    <div class="tab" data-ltab="h">Historia</div>
    <div class="tab" data-ltab="s">Salud</div>
    <div class="tab" data-ltab="a">Ancestral</div>
  </div>
  <div id="libC"></div>
</div>

<div id="pg-aux" class="pg">
  <div class="sec">🚨 PRIMEROS AUXILIOS</div>
  <div class="tabs" id="auxTabs">
    <div class="tab on" data-atab="e">Emergencias</div>
    <div class="tab" data-atab="s">Síntomas</div>
    <div class="tab" data-atab="a">Animales</div>
    <div class="tab" data-atab="p">Plantas</div>
  </div>
  <div id="auxC"></div>
</div>

<div id="pg-hist" class="pg">
  <div class="sec">HISTORIAL</div>
  <div id="histC"><p style="color:var(--tx3);text-align:center;padding:40px 0">Sin sesiones aún</p></div>
</div>

<div id="pg-prof" class="pg">
  <div class="sec">MODO PROFESOR</div>
  <div class="tabs" id="profTabs">
    <div class="tab on" data-ptab="c">Crear tarea</div>
    <div class="tab" data-ptab="a">Alumnos</div>
  </div>
  <div id="profC"></div>
</div>

<div id="pg-crea" class="pg">
  <div class="sec">MODO CREADOR</div>
  <div class="cg" id="creaTools">
    <div class="cc" data-tool="stats"><div class="ci">📊</div><h4>Estadísticas</h4><p>Materias más estudiadas</p></div>
    <div class="cc" data-tool="ideas"><div class="ci">💡</div><h4>Ideas</h4><p>Ver ideas enviadas</p></div>
    <div class="cc" data-tool="mod"><div class="ci">🛡️</div><h4>Moderar</h4><p>Panel general</p></div>
    <div class="cc" data-tool="exp"><div class="ci">📤</div><h4>Exportar</h4><p>Descargar datos</p></div>
  </div>
  <div id="creaO" style="margin-top:10px"></div>
  <div style="background:var(--card);border:1px solid var(--bd);border-radius:12px;padding:14px;margin-top:10px">
    <div class="sec" style="margin-top:0">💡 CAJITA DE IDEAS</div>
    <div id="ideasL"></div>
    <textarea id="ideaI" rows="2" placeholder="¿Qué mejorarías en Atlas?" style="margin-top:8px"></textarea>
    <button class="btn" id="btnSendIdea">Enviar idea</button>
  </div>
</div>

<div class="ov" id="ov">
  <div class="md">
    <button class="xb" id="btnCloseM">✕</button>
    <h2 id="mT"></h2>
    <div id="mC"></div>
  </div>
</div>

<script>
var SUBS=JSON.parse("{\"Colegio\":{\"icon\":\"🏫\",\"items\":[{\"n\":\"Matemáticas\",\"i\":\"➗\"},{\"n\":\"Física\",\"i\":\"⚡\"},{\"n\":\"Química\",\"i\":\"🧪\"},{\"n\":\"Biología\",\"i\":\"🧬\"},{\"n\":\"Historia\",\"i\":\"⏳\"},{\"n\":\"Geografía\",\"i\":\"🗺️\"},{\"n\":\"Inglés\",\"i\":\"🇬🇧\"},{\"n\":\"Lengua\",\"i\":\"✍️\"},{\"n\":\"Filosofía\",\"i\":\"🤔\"},{\"n\":\"Cívica\",\"i\":\"🏛️\"},{\"n\":\"Emprendimiento\",\"i\":\"💡\"},{\"n\":\"Electrónica\",\"i\":\"🔌\"},{\"n\":\"TICs\",\"i\":\"📱\"},{\"n\":\"Programación\",\"i\":\"👨‍💻\"},{\"n\":\"Cinemática\",\"i\":\"🏃\"},{\"n\":\"Ofimática\",\"i\":\"📄\"}]},\"Ciencias\":{\"icon\":\"🔬\",\"items\":[{\"n\":\"Astronomía\",\"i\":\"🌌\"},{\"n\":\"Paleontología\",\"i\":\"🦕\"},{\"n\":\"Ecología\",\"i\":\"🌿\"},{\"n\":\"Geología\",\"i\":\"🪨\"},{\"n\":\"Estadística\",\"i\":\"📊\"},{\"n\":\"Lógica\",\"i\":\"🧠\"}]},\"Tecnología\":{\"icon\":\"💻\",\"items\":[{\"n\":\"IA\",\"i\":\"🤖\"},{\"n\":\"Robótica\",\"i\":\"🦾\"},{\"n\":\"Ciberseguridad\",\"i\":\"🔐\"},{\"n\":\"Redes\",\"i\":\"🌐\"},{\"n\":\"Bases de Datos\",\"i\":\"🗄️\"}]},\"Humanidades\":{\"icon\":\"📚\",\"items\":[{\"n\":\"Psicología\",\"i\":\"🧠\"},{\"n\":\"Sociología\",\"i\":\"👥\"},{\"n\":\"Economía\",\"i\":\"💰\"},{\"n\":\"Antropología\",\"i\":\"🏺\"},{\"n\":\"Lingüística\",\"i\":\"🗣️\"}]},\"Salud\":{\"icon\":\"🏥\",\"items\":[{\"n\":\"Medicina\",\"i\":\"⚕️\"},{\"n\":\"Nutrición\",\"i\":\"🥗\"},{\"n\":\"Veterinaria\",\"i\":\"🐾\"},{\"n\":\"Enfermería\",\"i\":\"🩺\"}]},\"Artes\":{\"icon\":\"🎨\",\"items\":[{\"n\":\"Música\",\"i\":\"🎵\"},{\"n\":\"Pintura\",\"i\":\"🖼️\"},{\"n\":\"Arquitectura\",\"i\":\"🏗️\"},{\"n\":\"Fotografía\",\"i\":\"📷\"}]}}");
var DATA=JSON.parse("{\"Cinemática\":{\"exp\":\"CINEMÁTICA\\n\\nEstudia el movimiento sin considerar las fuerzas.\\n\\nFÓRMULAS:\\nVelocidad: v = d/t\\nAceleración: a = (vf-vi)/t\\nPosición: x = v₀t + ½at²\\nvf² = vi² + 2ax\\nGravedad: g = 9.8 m/s²\",\"mc\":[{\"p\":\"¿Qué estudia la cinemática?\",\"o\":[\"Las fuerzas del movimiento\",\"El movimiento sin considerar fuerzas\",\"La energía cinética\",\"La gravedad\"],\"c\":1},{\"p\":\"Fórmula de velocidad:\",\"o\":[\"v=F/m\",\"v=d/t\",\"v=ma\",\"v=½mv²\"],\"c\":1},{\"p\":\"En el MRU la velocidad es:\",\"o\":[\"Variable\",\"Acelerada\",\"Constante\",\"Nula\"],\"c\":2},{\"p\":\"Unidad de aceleración en el SI:\",\"o\":[\"m/s\",\"km/h\",\"m/s²\",\"N/kg\"],\"c\":2},{\"p\":\"Velocidad a los 3s con a=9.8 m/s²:\",\"o\":[\"19.6 m/s\",\"29.4 m/s\",\"9.8 m/s\",\"39.2 m/s\"],\"c\":1},{\"p\":\"MRUA significa:\",\"o\":[\"Movimiento Rectilíneo Uniforme Acelerado\",\"Movimiento Rotacional Uniforme\",\"Movimiento Relativo Angular\",\"Movimiento Rectilíneo Universal\"],\"c\":0},{\"p\":\"Aceleración de la gravedad terrestre:\",\"o\":[\"5.6 m/s²\",\"9.8 m/s²\",\"12.3 m/s²\",\"15 m/s²\"],\"c\":1},{\"p\":\"A 60 km/h durante 2 horas recorres:\",\"o\":[\"30 km\",\"60 km\",\"120 km\",\"180 km\"],\"c\":2},{\"p\":\"La pendiente en gráfica posición-tiempo es:\",\"o\":[\"La aceleración\",\"La fuerza\",\"La velocidad\",\"El desplazamiento\"],\"c\":2},{\"p\":\"La cinemática pertenece a:\",\"o\":[\"Química\",\"Biología\",\"Física\",\"Matemática pura\"],\"c\":2}],\"vf\":[{\"a\":\"La cinemática estudia las fuerzas que causan el movimiento.\",\"r\":false,\"e\":\"FALSO. Estudia el movimiento SIN fuerzas. Las fuerzas son objeto de la dinámica.\"},{\"a\":\"La fórmula v = d/t calcula la velocidad.\",\"r\":true,\"e\":\"VERDADERO. Velocidad = distancia dividida entre tiempo.\"},{\"a\":\"En el MRU la aceleración es 9.8 m/s².\",\"r\":false,\"e\":\"FALSO. En MRU la aceleración es CERO. La velocidad es constante.\"},{\"a\":\"El m/s² es la unidad de aceleración.\",\"r\":true,\"e\":\"VERDADERO. Metro por segundo cuadrado en el SI.\"},{\"a\":\"En MRU la gráfica posición-tiempo es una parábola.\",\"r\":false,\"e\":\"FALSO. En MRU es una línea recta. La parábola ocurre en MRUA.\"},{\"a\":\"Un cuerpo en caída libre tiene aceleración constante.\",\"r\":true,\"e\":\"VERDADERO. La gravedad g=9.8 m/s² es constante.\"},{\"a\":\"La velocidad siempre va en la dirección del movimiento.\",\"r\":true,\"e\":\"VERDADERO. Velocidad es un vector en la dirección del desplazamiento.\"},{\"a\":\"Velocidad negativa significa que el objeto está acelerando.\",\"r\":false,\"e\":\"FALSO. Velocidad negativa indica dirección contraria al eje, no aceleración.\"},{\"a\":\"Las gráficas v-t y x-t son herramientas de cinemática.\",\"r\":true,\"e\":\"VERDADERO. Son herramientas fundamentales para analizar movimiento.\"},{\"a\":\"La aceleración centrípeta apunta hacia el centro del círculo.\",\"r\":true,\"e\":\"VERDADERO. La aceleración centrípeta siempre apunta al centro.\"}],\"ej\":[{\"p\":\"Auto de 0 a 90 km/h en 10s. Calcular aceleración.\",\"s\":\"90 km/h = 25 m/s\\na = (25-0)/10 = 2.5 m/s²\"},{\"p\":\"Caída libre desde 80m. Calcular tiempo.\",\"s\":\"h = ½gt² → t = raíz(2×80/9.8) ≈ 4.04 s\"},{\"p\":\"Tren a 120 km/h frena con a=-3 m/s². Tiempo hasta detenerse:\",\"s\":\"120 km/h = 33.3 m/s\\nt = 33.3/3 ≈ 11.1 s\"},{\"p\":\"Desde reposo con a=4 m/s² durante 6s. Calcular distancia:\",\"s\":\"x = ½at² = ½×4×36 = 72 metros\"},{\"p\":\"Lanzado hacia arriba a 15 m/s. Altura máxima:\",\"s\":\"h = v²/2g = 225/19.6 ≈ 11.5 metros\"}]},\"Física\":{\"exp\":\"FÍSICA\\n\\nCiencia que estudia la materia, energía e interacciones.\\n\\nLEYES DE NEWTON:\\n1ª Ley (Inercia): sin fuerza neta el movimiento no cambia\\n2ª Ley: F = m × a\\n3ª Ley: Acción = Reacción (igual magnitud, opuesta)\\n\\nFÓRMULAS:\\nF=ma | Ec=½mv² | Ep=mgh | P=W/t | V=IR\",\"mc\":[{\"p\":\"Segunda Ley de Newton:\",\"o\":[\"F=mv\",\"F=ma\",\"F=m/a\",\"F=a/m\"],\"c\":1},{\"p\":\"La termodinámica estudia:\",\"o\":[\"El movimiento\",\"Calor y temperatura\",\"La luz\",\"El sonido\"],\"c\":1},{\"p\":\"Unidad de fuerza en el SI:\",\"o\":[\"Joule\",\"Pascal\",\"Newton\",\"Watt\"],\"c\":2},{\"p\":\"Primera Ley de Newton establece:\",\"o\":[\"F=ma\",\"Sin fuerza neta el cuerpo no cambia su movimiento\",\"La energía se conserva\",\"Acción y reacción iguales\"],\"c\":1},{\"p\":\"Energía potencial gravitatoria:\",\"o\":[\"½mv²\",\"mgh\",\"F×d\",\"P×t\"],\"c\":1},{\"p\":\"Velocidad de la luz en el vacío:\",\"o\":[\"300 km/s\",\"3×10⁸ m/s\",\"3×10⁶ m/s\",\"300 m/s\"],\"c\":1},{\"p\":\"Potencia =\",\"o\":[\"F×d\",\"m×a\",\"W/t\",\"E×v\"],\"c\":2},{\"p\":\"Energía cinética de 2kg a 3 m/s:\",\"o\":[\"3 J\",\"6 J\",\"9 J\",\"12 J\"],\"c\":2},{\"p\":\"Presión =\",\"o\":[\"F×A\",\"F/A\",\"m/V\",\"P×d\"],\"c\":1},{\"p\":\"Ley de Ohm: V =\",\"o\":[\"I/R\",\"I×R\",\"R/I\",\"I+R\"],\"c\":1}],\"vf\":[{\"a\":\"La fuerza se mide en Newtons.\",\"r\":true,\"e\":\"VERDADERO. El Newton (N) es la unidad de fuerza en el SI.\"},{\"a\":\"La energía cinética depende de la posición del objeto.\",\"r\":false,\"e\":\"FALSO. Ec=½mv² depende de masa y velocidad, no de posición.\"},{\"a\":\"La energía se conserva en sistemas cerrados.\",\"r\":true,\"e\":\"VERDADERO. Principio de conservación de la energía.\"},{\"a\":\"El sonido viaja más rápido que la luz.\",\"r\":false,\"e\":\"FALSO. Luz: 3×10⁸ m/s. Sonido: aprox 340 m/s en el aire.\"},{\"a\":\"La 3ª Ley dice que toda acción tiene reacción igual y opuesta.\",\"r\":true,\"e\":\"VERDADERO. Principio de acción y reacción de Newton.\"},{\"a\":\"El peso y la masa son lo mismo.\",\"r\":false,\"e\":\"FALSO. Masa: cantidad de materia (kg). Peso: fuerza gravitatoria (N=m×g).\"},{\"a\":\"Trabajo = Fuerza × distancia.\",\"r\":true,\"e\":\"VERDADERO. W = F×d cuando son paralelas.\"},{\"a\":\"La gravedad en la Luna es igual a la de la Tierra.\",\"r\":false,\"e\":\"FALSO. Gravedad lunar aprox 1.62 m/s², la terrestre aprox 9.8 m/s².\"},{\"a\":\"Los electrones tienen carga negativa.\",\"r\":true,\"e\":\"VERDADERO. Electrones: carga negativa.\"},{\"a\":\"La temperatura se mide en Newtons.\",\"r\":false,\"e\":\"FALSO. La temperatura se mide en Kelvin, Celsius o Fahrenheit.\"}],\"ej\":[{\"p\":\"Fuerza para acelerar 5kg a 3 m/s²:\",\"s\":\"F = m×a = 5×3 = 15 Newton\"},{\"p\":\"Energía cinética de 4kg a 10 m/s:\",\"s\":\"Ec = ½×4×100 = 200 Joules\"},{\"p\":\"Energía potencial de 3kg a 5m de altura:\",\"s\":\"Ep = 3×9.8×5 = 147 Joules\"},{\"p\":\"Potencia si realiza 600J de trabajo en 30s:\",\"s\":\"P = 600/30 = 20 Watts\"},{\"p\":\"Presión con F=200N sobre 0.5m²:\",\"s\":\"P = 200/0.5 = 400 Pascal\"}]},\"Química\":{\"exp\":\"QUÍMICA\\n\\nEstudia la materia, su composición y transformaciones.\\n\\nCONCEPTOS CLAVE:\\nNúmero atómico: cantidad de protones\\npH neutro = 7, ácido menor que 7, básico mayor que 7\\nMol: 6.022×10²³ partículas\\n\\nTABLA PERIÓDICA: 118 elementos organizados por número atómico\",\"mc\":[{\"p\":\"Elementos en la tabla periódica:\",\"o\":[\"92\",\"100\",\"118\",\"126\"],\"c\":2},{\"p\":\"Símbolo del oro:\",\"o\":[\"Go\",\"Au\",\"Or\",\"Ag\"],\"c\":1},{\"p\":\"pH neutro:\",\"o\":[\"0\",\"7\",\"14\",\"5\"],\"c\":1},{\"p\":\"Enlace que comparte electrones:\",\"o\":[\"Iónico\",\"Metálico\",\"Covalente\",\"Hidrógeno\"],\"c\":2},{\"p\":\"Fórmula del agua:\",\"o\":[\"H₃O\",\"HO₂\",\"H₂O\",\"OH\"],\"c\":2},{\"p\":\"El número atómico indica:\",\"o\":[\"La masa atómica\",\"El número de protones\",\"El número de neutrones\",\"La valencia\"],\"c\":1},{\"p\":\"El CO₂ es un:\",\"o\":[\"Elemento\",\"Mezcla\",\"Compuesto\",\"Átomo\"],\"c\":2},{\"p\":\"Gas más abundante en la atmósfera:\",\"o\":[\"Oxígeno\",\"CO₂\",\"Nitrógeno\",\"Argón\"],\"c\":2},{\"p\":\"Fórmula de la sal de mesa:\",\"o\":[\"KCl\",\"NaCl\",\"CaCl₂\",\"MgCl\"],\"c\":1},{\"p\":\"Una reacción exotérmica:\",\"o\":[\"Absorbe calor\",\"Libera calor\",\"No involucra calor\",\"Solo con luz\"],\"c\":1}],\"vf\":[{\"a\":\"El hidrógeno es el elemento más ligero de la tabla periódica.\",\"r\":true,\"e\":\"VERDADERO. H, número atómico 1, es el más ligero.\"},{\"a\":\"Una solución ácida tiene pH mayor que 7.\",\"r\":false,\"e\":\"FALSO. Ácido = pH MENOR que 7. Básico = pH mayor a 7.\"},{\"a\":\"Los átomos son los bloques fundamentales de la materia.\",\"r\":true,\"e\":\"VERDADERO. Toda la materia está formada por átomos.\"},{\"a\":\"El hierro se oxida al reaccionar con oxígeno y agua.\",\"r\":true,\"e\":\"VERDADERO. Fe + O₂ + H₂O produce óxido de hierro.\"},{\"a\":\"El agua pura conduce bien la electricidad.\",\"r\":false,\"e\":\"FALSO. Agua pura es mal conductor. Conduce solo con iones disueltos.\"},{\"a\":\"El carbono tiene 4 electrones de valencia.\",\"r\":true,\"e\":\"VERDADERO. Carbono tiene 4 electrones en su capa externa.\"},{\"a\":\"Las reacciones endotérmicas liberan energía.\",\"r\":false,\"e\":\"FALSO. Endotérmicas ABSORBEN energía. Las exotérmicas la liberan.\"},{\"a\":\"El símbolo del oxígeno es O.\",\"r\":true,\"e\":\"VERDADERO. O es el símbolo del oxígeno, número atómico 8.\"},{\"a\":\"Las mezclas se separan por métodos físicos.\",\"r\":true,\"e\":\"VERDADERO. Filtración, destilación, decantación son métodos físicos.\"},{\"a\":\"El oro es un metal alcalino.\",\"r\":false,\"e\":\"FALSO. El oro es un metal de transición. Alcalinos: Li, Na, K...\"}],\"ej\":[{\"p\":\"Protones del carbono y del oxígeno:\",\"s\":\"Carbono: 6 protones (número atómico 6)\\nOxígeno: 8 protones (número atómico 8)\"},{\"p\":\"Balancea la reacción: H₂ + O₂ → H₂O\",\"s\":\"2H₂ + O₂ → 2H₂O\"},{\"p\":\"Gramos en 1 mol de agua (H=1, O=16):\",\"s\":\"H₂O = 2(1)+16 = 18 g/mol\"},{\"p\":\"Si el pH es 3, la solución es ácida o básica?\",\"s\":\"ÁCIDA. pH menor que 7 indica acidez.\"},{\"p\":\"Electrones del sodio Na (número atómico 11):\",\"s\":\"11 electrones. En átomo neutro: electrones = número atómico.\"}]},\"Biología\":{\"exp\":\"BIOLOGÍA\\n\\nEstudia los seres vivos, sus procesos y evolución.\\n\\nTEORÍA CELULAR:\\nTodos los seres vivos están formados por células\\nProcariota: sin núcleo (bacterias)\\nEucariota: con núcleo (animales, plantas, hongos)\\n\\nFOTOSÍNTESIS:\\n6CO₂ + 6H₂O + luz → C₆H₁₂O₆ + 6O₂\\n\\nSer humano: 46 cromosomas (23 pares)\",\"mc\":[{\"p\":\"Unidad básica de la vida:\",\"o\":[\"El átomo\",\"La molécula\",\"La célula\",\"El tejido\"],\"c\":2},{\"p\":\"El ADN en células eucariotas está en:\",\"o\":[\"La mitocondria\",\"El núcleo\",\"El citoplasma\",\"La membrana\"],\"c\":1},{\"p\":\"La fotosíntesis ocurre en:\",\"o\":[\"Las mitocondrias\",\"Los ribosomas\",\"Los cloroplastos\",\"El núcleo\"],\"c\":2},{\"p\":\"Célula sin núcleo definido:\",\"o\":[\"Eucariota\",\"Procariota\",\"Animal\",\"Vegetal\"],\"c\":1},{\"p\":\"El ADN está formado por:\",\"o\":[\"Aminoácidos\",\"Nucleótidos\",\"Lípidos\",\"Carbohidratos\"],\"c\":1},{\"p\":\"Pares de cromosomas humanos:\",\"o\":[\"23\",\"46\",\"36\",\"48\"],\"c\":0},{\"p\":\"La respiración celular produce principalmente:\",\"o\":[\"Glucosa\",\"Oxígeno\",\"ATP (energía)\",\"Solo CO₂\"],\"c\":2},{\"p\":\"División que produce 2 células idénticas:\",\"o\":[\"Meiosis\",\"Mitosis\",\"Fecundación\",\"Transcripción\"],\"c\":1},{\"p\":\"Función de los ribosomas:\",\"o\":[\"Producir energía\",\"Sintetizar proteínas\",\"Almacenar ADN\",\"Digestión celular\"],\"c\":1},{\"p\":\"La teoría evolutiva fue propuesta por:\",\"o\":[\"Mendel\",\"Newton\",\"Darwin\",\"Pasteur\"],\"c\":2}],\"vf\":[{\"a\":\"Las bacterias son células eucariotas.\",\"r\":false,\"e\":\"FALSO. Las bacterias son PROCARIOTAS: sin núcleo definido.\"},{\"a\":\"Las mitocondrias producen la mayor parte del ATP.\",\"r\":true,\"e\":\"VERDADERO. Las mitocondrias son la central energética de la célula.\"},{\"a\":\"Los virus son considerados seres vivos.\",\"r\":false,\"e\":\"FALSO. Los virus no tienen células propias ni metabolismo independiente.\"},{\"a\":\"El ARN copia la información del ADN para fabricar proteínas.\",\"r\":true,\"e\":\"VERDADERO. El ARN mensajero lleva la información del ADN a los ribosomas.\"},{\"a\":\"Humanos y chimpancés comparten el 98% del ADN.\",\"r\":true,\"e\":\"VERDADERO. Esta similitud apoya la teoría evolutiva.\"},{\"a\":\"La meiosis produce 2 células idénticas.\",\"r\":false,\"e\":\"FALSO. La meiosis produce 4 células con la mitad de cromosomas.\"},{\"a\":\"Las plantas producen oxígeno en la fotosíntesis.\",\"r\":true,\"e\":\"VERDADERO. CO₂ + H₂O + luz → glucosa + O₂.\"},{\"a\":\"Todo organismo está formado por al menos una célula.\",\"r\":true,\"e\":\"VERDADERO. La célula es la unidad básica de la vida.\"},{\"a\":\"Los genes son segmentos de proteínas.\",\"r\":false,\"e\":\"FALSO. Los genes son segmentos de ADN que codifican proteínas.\"},{\"a\":\"La homeostasis mantiene el equilibrio interno del organismo.\",\"r\":true,\"e\":\"VERDADERO. Regula temperatura, pH, glucosa, etc.\"}],\"ej\":[{\"p\":\"Diferencia entre célula procariota y eucariota:\",\"s\":\"Procariota: sin núcleo, sin organelos, pequeña (bacterias)\\nEucariota: con núcleo, con organelos (animales, plantas, hongos)\"},{\"p\":\"Explica la fotosíntesis:\",\"s\":\"Las plantas capturan luz con clorofila. Combinan CO₂ del aire y H₂O del suelo, produciendo glucosa y liberando O₂.\"},{\"p\":\"Cromosomas humanos después de la meiosis:\",\"s\":\"23 cromosomas. La meiosis reduce a la mitad para formar gametos.\"},{\"p\":\"Genotipo y fenotipo:\",\"s\":\"Genotipo: información genética en el ADN.\\nFenotipo: características observables (genotipo + ambiente).\"},{\"p\":\"3 diferencias célula animal vs vegetal:\",\"s\":\"1. Vegetal tiene pared celular; animal no.\\n2. Vegetal tiene cloroplastos; animal no.\\n3. Vegetal tiene vacuola central grande; animal tiene vacuolas pequeñas.\"}]},\"Historia\":{\"exp\":\"HISTORIA\\n\\nCiencia social que estudia el pasado humano.\\n\\nPERÍODOS UNIVERSALES:\\nPrehistoria: hasta aprox 3000 a.C.\\nEdad Antigua: 3000 a.C. - 476 d.C.\\nEdad Media: 476 - 1492\\nEdad Moderna: 1492 - 1789\\nEdad Contemporánea: 1789 - presente\\n\\nECUADOR:\\nValdivia (3500 a.C.) → Conquista española (1534)\\nBatalla de Pichincha: 24 mayo 1822\\nRepública independiente: 1830\",\"mc\":[{\"p\":\"Batalla de Pichincha:\",\"o\":[\"1810\",\"1822\",\"1830\",\"1809\"],\"c\":1},{\"p\":\"Quién conquistó Quito en 1534:\",\"o\":[\"Cristóbal Colón\",\"Sebastián de Belalcázar\",\"Francisco Pizarro\",\"Hernán Cortés\"],\"c\":1},{\"p\":\"¿Cuándo terminó la Edad Media?\",\"o\":[\"1492\",\"1789\",\"476\",\"1000\"],\"c\":0},{\"p\":\"Ecuador se separó de la Gran Colombia en:\",\"o\":[\"1822\",\"1825\",\"1830\",\"1835\"],\"c\":2},{\"p\":\"La Revolución Francesa ocurrió en:\",\"o\":[\"1776\",\"1789\",\"1804\",\"1815\"],\"c\":1},{\"p\":\"Primera civilización en usar escritura:\",\"o\":[\"Egipcia\",\"Griega\",\"Sumeria\",\"Fenicia\"],\"c\":2},{\"p\":\"Fin de la Segunda Guerra Mundial:\",\"o\":[\"1944\",\"1945\",\"1946\",\"1943\"],\"c\":1},{\"p\":\"Cultura más antigua del Ecuador:\",\"o\":[\"Inca\",\"Shuar\",\"Valdivia\",\"Cañari\"],\"c\":2},{\"p\":\"Caída del Imperio Romano de Occidente:\",\"o\":[\"476 d.C.\",\"395 d.C.\",\"1453 d.C.\",\"753 a.C.\"],\"c\":0},{\"p\":\"Inicio de la Edad Contemporánea:\",\"o\":[\"Revolución Industrial\",\"Revolución Francesa\",\"Descubrimiento de América\",\"Caída de Roma\"],\"c\":1}],\"vf\":[{\"a\":\"La Batalla de Pichincha fue el 24 de mayo de 1822.\",\"r\":true,\"e\":\"VERDADERO. Sucre derrotó a los realistas en el volcán Pichincha.\"},{\"a\":\"Ecuador fue colonia española durante aproximadamente 300 años.\",\"r\":true,\"e\":\"VERDADERO. Desde 1534 hasta 1822 son casi 3 siglos.\"},{\"a\":\"Colón llegó a América buscando una ruta a África.\",\"r\":false,\"e\":\"FALSO. Colón buscaba una ruta a Asia. Llegó al Caribe el 12 oct 1492.\"},{\"a\":\"La Gran Colombia incluyó a Ecuador, Colombia y Venezuela.\",\"r\":true,\"e\":\"VERDADERO. La Gran Colombia también incluyó Panamá.\"},{\"a\":\"La Primera Guerra Mundial comenzó en 1914.\",\"r\":true,\"e\":\"VERDADERO. Comenzó el 28 julio 1914.\"},{\"a\":\"Los aztecas vivían en lo que hoy es Perú.\",\"r\":false,\"e\":\"FALSO. Los aztecas estaban en México. En Perú estaban los Incas.\"},{\"a\":\"La Revolución Industrial comenzó en Francia.\",\"r\":false,\"e\":\"FALSO. Comenzó en Inglaterra en el siglo XVIII.\"},{\"a\":\"Simón Bolívar fue clave en la independencia latinoamericana.\",\"r\":true,\"e\":\"VERDADERO. Bolívar liberó Venezuela, Colombia, Ecuador, Perú y Bolivia.\"},{\"a\":\"El Muro de Berlín cayó en 1989.\",\"r\":true,\"e\":\"VERDADERO. El 9 de noviembre de 1989 marcó el fin de la Guerra Fría.\"},{\"a\":\"Los faraones gobernaron en la antigua Grecia.\",\"r\":false,\"e\":\"FALSO. Los faraones gobernaron en el antiguo Egipto.\"}],\"ej\":[{\"p\":\"Los 5 períodos de la historia universal:\",\"s\":\"1. Prehistoria (hasta aprox 3000 a.C.)\\n2. Edad Antigua (3000 a.C. - 476 d.C.)\\n3. Edad Media (476 - 1492)\\n4. Edad Moderna (1492 - 1789)\\n5. Edad Contemporánea (1789 - presente)\"},{\"p\":\"Proceso de independencia de Ecuador:\",\"s\":\"1809: Primer Grito de Independencia (10 agosto, Quito)\\n1820: Independencia de Guayaquil (9 octubre)\\n1822: Batalla de Pichincha con el Mariscal Sucre\\n1830: Ecuador se declara república independiente\"},{\"p\":\"¿Qué fue la Guerra Fría?\",\"s\":\"Conflicto político (1947-1991) entre EE.UU. (capitalismo) y URSS (comunismo). Sin combate directo, con carrera armamentista y espacial.\"},{\"p\":\"3 culturas precolombinas del Ecuador:\",\"s\":\"1. Valdivia: cerámica más antigua de América (3500 a.C.)\\n2. Cañari: orfebres y agricultores andinos\\n3. Shuar: cultura amazónica con medicina tradicional\"},{\"p\":\"Causas de la Primera Guerra Mundial:\",\"s\":\"1. Alianzas militares (Triple Entente vs Triple Alianza)\\n2. Nacionalismo extremo en Europa\\n3. Imperialismo colonial\\n4. Asesinato del archiduque Francisco Fernando (28 jun 1914)\"}]},\"Matemáticas\":{\"exp\":\"MATEMÁTICAS\\n\\nCiencia de los números, estructuras y patrones.\\n\\nFÓRMULAS ESENCIALES:\\nÁrea círculo: A = πr²\\nPitágoras: a² + b² = c²\\nCuadrática: x = (-b ± raíz(b²-4ac)) / 2a\\nÁrea triángulo: A = base×altura/2\\nPendiente: m = (y₂-y₁)/(x₂-x₁)\\n\\nEJEMPLO: x²-5x+6=0\\na=1, b=-5, c=6 → x=(5±1)/2 → x=3 o x=2\",\"mc\":[{\"p\":\"¿Cuánto es la raíz de 144?\",\"o\":[\"11\",\"12\",\"13\",\"14\"],\"c\":1},{\"p\":\"Si 2x+6=18, entonces x=\",\"o\":[\"4\",\"5\",\"6\",\"7\"],\"c\":2},{\"p\":\"Área de círculo con r=5 (π≈3.14):\",\"o\":[\"31.4\",\"78.5\",\"15.7\",\"50\"],\"c\":1},{\"p\":\"¿Cuánto es 2 elevado a 3?\",\"o\":[\"6\",\"8\",\"9\",\"12\"],\"c\":1},{\"p\":\"Suma de ángulos de un triángulo:\",\"o\":[\"90°\",\"180°\",\"270°\",\"360°\"],\"c\":1},{\"p\":\"Pendiente de y=3x+2:\",\"o\":[\"2\",\"3\",\"5\",\"1\"],\"c\":1},{\"p\":\"El 30% de 200 =\",\"o\":[\"30\",\"50\",\"60\",\"70\"],\"c\":2},{\"p\":\"Catetos 3 y 4, la hipotenusa es:\",\"o\":[\"5\",\"6\",\"7\",\"8\"],\"c\":0},{\"p\":\"log base 10 de 1000 =\",\"o\":[\"2\",\"3\",\"4\",\"10\"],\"c\":1},{\"p\":\"Probabilidad de cara en una moneda:\",\"o\":[\"1/4\",\"1/3\",\"1/2\",\"2/3\"],\"c\":2}],\"vf\":[{\"a\":\"El número π es exactamente igual a 22/7.\",\"r\":false,\"e\":\"FALSO. 22/7 es una aproximación. π es irracional: 3.14159265...\"},{\"a\":\"Un número negativo elevado a exponente par da positivo.\",\"r\":true,\"e\":\"VERDADERO. (-2)²=4, (-3)⁴=81.\"},{\"a\":\"El cero es un número par.\",\"r\":true,\"e\":\"VERDADERO. El 0 es divisible entre 2.\"},{\"a\":\"La raíz cuadrada de un número negativo existe en los reales.\",\"r\":false,\"e\":\"FALSO. Solo existe en los complejos.\"},{\"a\":\"Todo cuadrado es también un rectángulo.\",\"r\":true,\"e\":\"VERDADERO. El cuadrado es un rectángulo con todos los lados iguales.\"},{\"a\":\"El factorial de 0 es 0.\",\"r\":false,\"e\":\"FALSO. Por definición, 0! = 1.\"},{\"a\":\"Una ecuación cuadrática puede tener 0, 1 o 2 soluciones reales.\",\"r\":true,\"e\":\"VERDADERO. Depende del discriminante b²-4ac.\"},{\"a\":\"La suma de los primeros 100 naturales es 5050.\",\"r\":true,\"e\":\"VERDADERO. Fórmula de Gauss: n(n+1)/2 = 100×101/2 = 5050.\"},{\"a\":\"Dos rectas paralelas se intersectan en el infinito.\",\"r\":false,\"e\":\"FALSO. Las paralelas NUNCA se intersectan en geometría euclidiana.\"},{\"a\":\"El número 1 es primo.\",\"r\":false,\"e\":\"FALSO. Un número primo tiene exactamente 2 divisores. El 1 solo tiene uno.\"}],\"ej\":[{\"p\":\"Resuelve: 3x² - 12 = 0\",\"s\":\"3x² = 12 → x² = 4 → x = ±2\"},{\"p\":\"Área y perímetro de un rectángulo de 8×5 cm:\",\"s\":\"Área = 8×5 = 40 cm²\\nPerímetro = 2(8+5) = 26 cm\"},{\"p\":\"Probabilidad de sacar azul (3 rojas, 4 azules, 5 verdes):\",\"s\":\"Total=12 → P(azul)=4/12=1/3 ≈ 33.3%\"},{\"p\":\"Pendiente entre los puntos (2,3) y (6,11):\",\"s\":\"m = (11-3)/(6-2) = 8/4 = 2\"},{\"p\":\"Artículo de $85 con 20% de descuento:\",\"s\":\"Descuento = 0.20×85 = $17\\nPrecio final = 85-17 = $68\"}]},\"Inglés\":{\"exp\":\"INGLÉS\\n\\nIdioma más hablado como segunda lengua.\\n\\nVERBO TO BE: I am / You are / He-She-It is / We-They are\\n\\nTIEMPOS VERBALES:\\nPresent Simple: I study / She studies\\nPresent Continuous: I am studying (ahora)\\nPast Simple: I studied / She went\\nFuture: I will study\\nPresent Perfect: I have studied\\n\\nADJETIVOS van ANTES del sustantivo:\\nA beautiful house\",\"mc\":[{\"p\":\"Casa en inglés:\",\"o\":[\"Car\",\"House\",\"Home\",\"Land\"],\"c\":1},{\"p\":\"Completar: She ___ a doctor.\",\"o\":[\"are\",\"am\",\"is\",\"be\"],\"c\":2},{\"p\":\"Pasado del verbo to go:\",\"o\":[\"Goed\",\"Gone\",\"Went\",\"Goes\"],\"c\":2},{\"p\":\"Como preguntas el nombre en inglés:\",\"o\":[\"How old are you?\",\"What is your name?\",\"Where are you from?\",\"How are you?\"],\"c\":1},{\"p\":\"Oración correcta en inglés:\",\"o\":[\"I don't like chocolate\",\"I not like chocolate\",\"I doesn't like chocolate\",\"I no like chocolate\"],\"c\":0},{\"p\":\"Plural de child:\",\"o\":[\"Childs\",\"Children\",\"Childrens\",\"Childer\"],\"c\":1},{\"p\":\"Completar: Yesterday I ___ to school.\",\"o\":[\"go\",\"goes\",\"went\",\"will go\"],\"c\":2},{\"p\":\"Mañana (futuro) en inglés:\",\"o\":[\"Yesterday\",\"Today\",\"Tomorrow\",\"Later\"],\"c\":2},{\"p\":\"Beautiful significa:\",\"o\":[\"Feo\",\"Regular\",\"Hermoso\",\"Grande\"],\"c\":2},{\"p\":\"I have lived here for 10 years. Este tiempo verbal es:\",\"o\":[\"Past Simple\",\"Present Perfect\",\"Future\",\"Present Continuous\"],\"c\":1}],\"vf\":[{\"a\":\"I am es la primera persona singular del verbo TO BE.\",\"r\":true,\"e\":\"TRUE. I am, You are, He/She/It is, We/They are.\"},{\"a\":\"Does se usa con I y You.\",\"r\":false,\"e\":\"FALSE. Does es para He, She, It. Do para I, You, We, They.\"},{\"a\":\"El pasado de eat es eated.\",\"r\":false,\"e\":\"FALSE. Eat es irregular: pasado es ATE.\"},{\"a\":\"There is se usa con sustantivos singulares.\",\"r\":true,\"e\":\"TRUE. There is a book (singular) vs There are books (plural).\"},{\"a\":\"El alfabeto inglés tiene 26 letras.\",\"r\":true,\"e\":\"TRUE. 26 letras, igual que el español.\"},{\"a\":\"Could es el pasado de can.\",\"r\":true,\"e\":\"TRUE. Can (presente) → Could (pasado).\"},{\"a\":\"Los adjetivos en inglés van después del sustantivo.\",\"r\":false,\"e\":\"FALSE. En inglés van ANTES: a beautiful house.\"},{\"a\":\"Much se usa con sustantivos contables.\",\"r\":false,\"e\":\"FALSE. Much es para incontables (much water). Many para contables (many books).\"},{\"a\":\"She don't like pizza es una oración correcta.\",\"r\":false,\"e\":\"FALSE. Correcto: She DOESN'T like pizza.\"},{\"a\":\"Going to expresa planes futuros.\",\"r\":true,\"e\":\"TRUE. I am going to study tomorrow = plan futuro.\"}],\"ej\":[{\"p\":\"Traduce: Ella está comiendo una manzana ahora mismo.\",\"s\":\"She is eating an apple right now.\\nPresent Continuous: Subject + am/is/are + verb-ing\"},{\"p\":\"Ordena las palabras: school / goes / she / to / every day\",\"s\":\"She goes to school every day.\\nSubject + verb + complement en Present Simple\"},{\"p\":\"Escribe 5 oraciones sobre ti en inglés.\",\"s\":\"1. My name is [nombre].\\n2. I am [edad] years old.\\n3. I live in Ecuador.\\n4. I study at [colegio].\\n5. I like [hobby].\"},{\"p\":\"Cambia al pasado: Today I wake up early and go to school.\",\"s\":\"Yesterday I woke up early and went to school.\\nwake → woke, go → went\"},{\"p\":\"Escribe preguntas con WHO, WHAT y WHERE.\",\"s\":\"WHO: Who is your best friend?\\nWHAT: What is your favorite subject?\\nWHERE: Where do you live?\"}]}}");
var LIB=JSON.parse("{\"t\":[{\"t\":\"Leyes de Newton\",\"x\":\"1ª: Inercia. 2ª: F=ma. 3ª: Acción-reacción igual y opuesta.\",\"m\":\"Física\"},{\"t\":\"La Célula\",\"x\":\"Unidad básica de vida. Procariota: sin núcleo (bacterias). Eucariota: con núcleo.\",\"m\":\"Biología\"},{\"t\":\"Tabla Periódica\",\"x\":\"118 elementos por número atómico. Grupos: propiedades similares. Períodos: niveles de energía.\",\"m\":\"Química\"},{\"t\":\"Sistema Solar\",\"x\":\"Sol + 8 planetas: Mercurio, Venus, Tierra, Marte, Júpiter, Saturno, Urano, Neptuno.\",\"m\":\"Astronomía\"},{\"t\":\"ADN y Genética\",\"x\":\"Doble hélice de nucleótidos (A-T, G-C). Genes codifican proteínas. Mendel: leyes de herencia.\",\"m\":\"Biología\"},{\"t\":\"Cinemática\",\"x\":\"MRU: velocidad constante, v=d/t. MRUA: aceleración constante, x=v₀t+½at².\",\"m\":\"Física\"}],\"f\":[{\"t\":\"Fórmulas de Física\",\"x\":\"F=ma | v=d/t | E=mc² | Ec=½mv² | Ep=mgh | P=W/t | V=IR | p=F/A\",\"m\":\"Física General\"},{\"t\":\"Fórmulas de Matemáticas\",\"x\":\"Área círculo=πr² | Pitágoras: a²+b²=c² | Cuadrática: x=(-b±raíz(b²-4ac))/2a | Triángulo=bh/2\",\"m\":\"Matemáticas\"},{\"t\":\"Fórmulas de Química\",\"x\":\"PV=nRT | pH=-log[H+] | Densidad=m/V | n=m/M\",\"m\":\"Química\"},{\"t\":\"Electricidad\",\"x\":\"V=IR (Ohm) | P=VI | P=I²R | Serie: R=R₁+R₂ | Paralelo: 1/R=1/R₁+1/R₂\",\"m\":\"Física\"},{\"t\":\"Trigonometría\",\"x\":\"sen=opuesto/hipotenusa | cos=adyacente/hipotenusa | tan=sen/cos | sen²+cos²=1\",\"m\":\"Matemáticas\"}],\"h\":[{\"t\":\"Historia del Ecuador\",\"x\":\"Valdivia (3500 a.C.) → Incas (s.XV) → Conquista española (1534) → Independencia Pichincha (1822) → República (1830).\",\"m\":\"Historia\"},{\"t\":\"Revolución Industrial\",\"x\":\"Siglo XVIII-XIX en Inglaterra. Máquina de vapor. Transformó la sociedad agraria en industrial.\",\"m\":\"Historia Moderna\"},{\"t\":\"Segunda Guerra Mundial\",\"x\":\"1939-1945. Eje vs Aliados. Holocausto. Hiroshima y Nagasaki. Aprox 70 millones de muertos.\",\"m\":\"Historia Contemporánea\"},{\"t\":\"Independencias Latinoamericanas\",\"x\":\"Siglo XIX. Bolívar liberó Venezuela, Colombia, Ecuador, Perú. San Martín: Argentina y Chile.\",\"m\":\"Historia de América\"},{\"t\":\"Civilizaciones Antiguas\",\"x\":\"Mesopotamia (escritura), Egipto (faraones), Grecia (democracia, filosofía), Roma (derecho).\",\"m\":\"Historia Antigua\"}],\"s\":[{\"t\":\"Sistema Digestivo\",\"x\":\"Boca → esófago → estómago → intestino delgado → intestino grueso → recto.\",\"m\":\"Anatomía\"},{\"t\":\"Sistema Circulatorio\",\"x\":\"Corazón (4 cámaras) bombea sangre. Arterias: del corazón. Venas: al corazón.\",\"m\":\"Anatomía\"},{\"t\":\"Vitaminas\",\"x\":\"A: visión. B12: nervios. C: inmunidad. D: huesos (sol). E: piel. K: coagulación.\",\"m\":\"Nutrición\"},{\"t\":\"Primeros Auxilios Básicos\",\"x\":\"RCP: 30 compresiones + 2 respiraciones. Hemorragia: presión directa. Quemadura: agua fría 10min.\",\"m\":\"Primeros Auxilios\"}],\"a\":[{\"t\":\"Plantas Medicinales Ecuador\",\"x\":\"Uña de gato (artritis), Sangre de drago (heridas), Matico (cicatrización), Manzanilla (digestión).\",\"m\":\"Etnomedicina\"},{\"t\":\"Cosmovisión Kichwa\",\"x\":\"Pachamama (Madre Tierra), Inti (Sol), Quilla (Luna). Sumak Kawsay = Buen Vivir.\",\"m\":\"Espiritualidad Andina\"},{\"t\":\"Medicina Shuar\",\"x\":\"Pueblo amazónico que usa plantas en rituales de sanación. El uwishin (chamán) guía el proceso.\",\"m\":\"Medicina Ancestral\"},{\"t\":\"Calendario Inca\",\"x\":\"12 meses basados en sol y luna. Inti Raymi (junio) y Coya Raymi (septiembre) eran las fiestas más importantes.\",\"m\":\"Historia Andina\"}]}");
var AUX=JSON.parse("{\"e\":[{\"i\":\"💓\",\"t\":\"RCP\",\"x\":\"1. Verifica que no respira\\n2. Llama al 911\\n3. Talón de la mano en centro del pecho\\n4. 30 compresiones profundas (5cm), 100/min\\n5. 2 respiraciones de rescate\\n6. Repite hasta que llegue ayuda\"},{\"i\":\"🩸\",\"t\":\"Hemorragia\",\"x\":\"1. Presiona con tela limpia\\n2. Mantén presión continua SIN quitar la tela\\n3. Eleva la extremidad\\n4. Si la tela se empapa, agrega más encima\\n5. Atención médica urgente\"},{\"i\":\"🔥\",\"t\":\"Quemadura\",\"x\":\"1. Aleja de la fuente de calor\\n2. Agua fría (NO helada) durante 10-20 min\\n3. NO pongas pasta dental ni aceite\\n4. Cubre con tela limpia húmeda\\n5. NO revientes ampollas\"},{\"i\":\"🦴\",\"t\":\"Fractura\",\"x\":\"1. NO muevas el hueso\\n2. Inmoviliza con tablillas o telas\\n3. Aplica hielo envuelto en tela\\n4. Traslada con cuidado al médico\"},{\"i\":\"🤢\",\"t\":\"Intoxicación\",\"x\":\"1. Llama al 911\\n2. NO induzcas vómito\\n3. Si inconsciente: ponlo de lado\\n4. Lleva el envase del producto\"},{\"i\":\"👶\",\"t\":\"Niño atragantado\",\"x\":\"Si puede toser: anímalo a que tosa fuerte.\\n\\nSi no puede:\\n5 palmadas en la espalda + 5 compresiones abdominales (Heimlich).\\nRepite hasta despejar.\"}],\"s\":[{\"i\":\"🤒\",\"t\":\"Fiebre\",\"x\":\"37-38°C: reposo y líquidos.\\n38-39°C: paracetamol, paños fríos.\\nMayor de 39°C: urgente atención médica.\\n\\nEn bebés: CUALQUIER fiebre es urgencia.\"},{\"i\":\"🤧\",\"t\":\"Resfriado\",\"x\":\"Síntomas: tos, estornudos, fiebre leve.\\n\\nEn casa: reposo, líquidos calientes, limón con miel.\\n\\nMédico si: fiebre mayor de 39°C o más de 7 días.\"},{\"i\":\"🤕\",\"t\":\"Dolor de cabeza\",\"x\":\"Causas: deshidratación, estrés, migraña.\\n\\nAlivio: hidratarse, oscuridad, frío en la frente, paracetamol.\\n\\nURGENCIA: dolor súbito intenso, fiebre alta, rigidez de cuello.\"},{\"i\":\"💚\",\"t\":\"Dolor abdominal\",\"x\":\"Médico si: dolor lado derecho inferior, fiebre, vómito intenso, no mejora en horas.\"},{\"i\":\"😮\",\"t\":\"Dificultad respiratoria\",\"x\":\"URGENCIA MÉDICA - Llama al 911\\n\\nSi: labios azules, no puede hablar, respira muy rápido.\"},{\"i\":\"🫀\",\"t\":\"Dolor en el pecho\",\"x\":\"POSIBLE URGENCIA CARDIACA\\nLlama al 911 inmediatamente.\\n\\nSeñales de infarto: dolor opresivo, irradia al brazo izquierdo, sudor frío, náuseas.\"}],\"a\":[{\"i\":\"🐕\",\"t\":\"Perro o Gato enfermo\",\"x\":\"Señales: vómito repetido, diarrea con sangre, no come 2+ días, convulsiones.\\n\\nAísla del resto. Lleva al veterinario.\"},{\"i\":\"🐠\",\"t\":\"Peces enfermos\",\"x\":\"Señales: nadan de lado, manchas blancas, aletas dobladas.\\n\\nAcción: cambia 30% del agua, mejora oxigenación, sal no yodada 1g/L.\"},{\"i\":\"🐔\",\"t\":\"Aves de corral\",\"x\":\"Señales: plumas erizadas, no comen, secreción nasal, muerte súbita.\\n\\nAísla INMEDIATAMENTE. Puede ser enfermedad contagiosa. Llama al veterinario avícola.\"},{\"i\":\"🌿\",\"t\":\"Mordedura de serpiente\",\"x\":\"1. Aleja sin correr\\n2. Inmoviliza la extremidad\\n3. Mantén por debajo del corazón\\n4. NO hagas incisiones ni chupe el veneno\\n5. Hospital urgente\"}],\"p\":[{\"i\":\"🌿\",\"t\":\"Plantas medicinales\",\"x\":\"Manzanilla: digestión (té)\\nToronjil: nervios, insomnio (té)\\nOrtiga: anemia, artritis (infusión)\\nMatico: cicatrización (cataplasma)\\nSangre de drago: heridas (látex)\\nUña de gato: inmunidad\"},{\"i\":\"⚠️\",\"t\":\"Plantas tóxicas\",\"x\":\"Ricino/Higuerilla: semillas muy tóxicas\\nDifenbaquia: ardor boca y garganta\\nAdelfa: cardiotóxica\\nEstramonio: alucinaciones, peligrosa\\n\\nSi hay ingestión: NO induzcas vómito, ve a urgencias.\"},{\"i\":\"🍃\",\"t\":\"Identificar plantas\",\"x\":\"Observa: forma de hoja, margen, venación, color, olor, flor, fruto, hábitat.\\n\\nUsa apps: iNaturalist, PlantNet.\\nNunca consumas sin identificación de experto.\"}]}");

var ST={
  role: localStorage.getItem('at_role')||'student',
  hist: JSON.parse(localStorage.getItem('at_hist')||'[]'),
  ideas: JSON.parse(localStorage.getItem('at_ideas')||'[]'),
  ints: JSON.parse(localStorage.getItem('at_ints')||'{}'),
  diff:'Fácil', mode:'m', tema:'', ans:{}, cors:{}, tot:0,
  lt:'t', at:'e', pt:'c', tt:'x', td:'b', cat:'Todas'
};

function sf(a){for(var i=a.length-1;i>0;i--){var j=Math.floor(Math.random()*(i+1));var t=a[i];a[i]=a[j];a[j]=t;}return a;}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function nl(s){return esc(s).replace(/\n/g,'<br>');}
function openM(title,content){
  document.getElementById('mT').textContent=title;
  document.getElementById('mC').innerHTML=content;
  document.getElementById('ov').classList.add('on');
}

window.addEventListener('load',function(){
  initStars();
  buildGrid();
  buildSel();
  loadSt();
  renderLib();
  renderAux();
  renderProf();
  renderIdeas();
  renderHist();
  renderAch();
  applyRole(ST.role);
  document.querySelectorAll('[data-role]').forEach(function(el){
    el.classList.toggle('on', el.dataset.role===ST.role);
  });
  bindAll();
});

function bindAll(){
  // Nav
  document.querySelectorAll('.nb[id^="nb-"]').forEach(function(btn){
    btn.addEventListener('click',function(){go(btn.id.replace('nb-',''),btn);});
  });
  // Role
  document.querySelectorAll('[data-role]').forEach(function(el){
    el.addEventListener('click',function(){setRole(el.dataset.role);});
  });
  // Diff
  document.querySelectorAll('[data-diff]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-diff]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.diff=el.dataset.diff;
    });
  });
  // Mode
  document.querySelectorAll('[data-mode]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-mode]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.mode=el.dataset.mode;
    });
  });
  // Sim tabs
  document.querySelectorAll('[data-stab]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-stab]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on');
      var t=el.dataset.stab;
      document.getElementById('sTP').style.display=t==='p'?'block':'none';
      document.getElementById('sTE').style.display=t==='e'?'block':'none';
    });
  });
  // Tarea tabs
  document.querySelectorAll('[data-ttab]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-ttab]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.tt=el.dataset.ttab;
      document.getElementById('tX').style.display=el.dataset.ttab==='x'?'block':'none';
      document.getElementById('tR').style.display=el.dataset.ttab==='r'?'block':'none';
    });
  });
  // TD btns
  document.querySelectorAll('[data-td]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-td]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.td=el.dataset.td;
    });
  });
  // Lib tabs
  document.querySelectorAll('[data-ltab]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-ltab]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.lt=el.dataset.ltab; renderLib();
    });
  });
  // Aux tabs
  document.querySelectorAll('[data-atab]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-atab]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.at=el.dataset.atab; renderAux();
    });
  });
  // Prof tabs
  document.querySelectorAll('[data-ptab]').forEach(function(el){
    el.addEventListener('click',function(){
      document.querySelectorAll('[data-ptab]').forEach(function(x){x.classList.remove('on');});
      el.classList.add('on'); ST.pt=el.dataset.ptab; renderProf();
    });
  });
  // Crea tools
  document.querySelectorAll('[data-tool]').forEach(function(el){
    el.addEventListener('click',function(){creaTool(el.dataset.tool);});
  });
  // Buttons
  document.getElementById('btnStartSim').addEventListener('click',startSim);
  document.getElementById('sEv').addEventListener('click',evalSim);
  document.getElementById('btnResetSim').addEventListener('click',resetSim);
  document.getElementById('btnGenExam').addEventListener('click',genExam);
  document.getElementById('btnExplicar').addEventListener('click',explicar);
  document.getElementById('btnResolver').addEventListener('click',resolver);
  document.getElementById('btnSendIdea').addEventListener('click',sendIdea);
  document.getElementById('btnCloseM').addEventListener('click',function(){document.getElementById('ov').classList.remove('on');});
  // Search
  document.getElementById('sSearch').addEventListener('input',function(){renderGrid(ST.cat,this.value);});
  document.getElementById('bS').addEventListener('input',function(){renderLib(this.value);});
}

function initStars(){
  var c=document.getElementById('cv'),ctx=c.getContext('2d');
  c.width=window.innerWidth; c.height=window.innerHeight;
  var s=[];
  for(var i=0;i<80;i++) s.push({x:Math.random()*c.width,y:Math.random()*c.height,r:Math.random()*1.2,a:Math.random(),sp:Math.random()*.005});
  (function draw(){
    ctx.clearRect(0,0,c.width,c.height);
    s.forEach(function(st){
      st.a+=st.sp; if(st.a>1||st.a<0) st.sp*=-1;
      ctx.beginPath(); ctx.arc(st.x,st.y,st.r,0,Math.PI*2);
      ctx.fillStyle='rgba(148,163,184,'+(st.a*.5)+')'; ctx.fill();
    });
    requestAnimationFrame(draw);
  })();
}

function go(id,el){
  document.querySelectorAll('.pg').forEach(function(p){p.classList.remove('on');});
  document.querySelectorAll('.nb').forEach(function(b){b.classList.remove('on');});
  var pg=document.getElementById('pg-'+id);
  if(pg) pg.classList.add('on');
  if(el) el.classList.add('on');
  window.scrollTo(0,0);
}

function setRole(r){
  ST.role=r; localStorage.setItem('at_role',r);
  document.querySelectorAll('[data-role]').forEach(function(el){el.classList.toggle('on',el.dataset.role===r);});
  applyRole(r);
}
function applyRole(r){
  document.getElementById('nb-prof').style.display=(r==='teacher'||r==='creator')?'block':'none';
  document.getElementById('nb-crea').style.display=r==='creator'?'block':'none';
}

function buildGrid(){
  var pills=document.getElementById('cPills');
  var cats=['Todas'].concat(Object.keys(SUBS));
  pills.innerHTML=cats.map(function(c){
    return '<div class="pill'+(c==='Todas'?' on':'')+'" data-cat="'+c+'">'+(c==='Todas'?'Todas':(SUBS[c].icon+' '+c))+'</div>';
  }).join('');
  pills.addEventListener('click',function(e){
    var pill=e.target.closest('.pill');
    if(!pill) return;
    document.querySelectorAll('.pill').forEach(function(p){p.classList.remove('on');});
    pill.classList.add('on');
    ST.cat=pill.dataset.cat;
    renderGrid(ST.cat,document.getElementById('sSearch').value);
  });
  renderGrid('Todas');
}

function renderGrid(cat,srch){
  srch=srch||'';
  var items=[];
  Object.entries(SUBS).forEach(function(entry){
    var c=entry[0], d=entry[1];
    if(cat==='Todas'||cat===c){
      d.items.forEach(function(it){
        if(!srch||it.n.toLowerCase().indexOf(srch.toLowerCase())>=0) items.push(it);
      });
    }
  });
  var grid=document.getElementById('sGrid');
  grid.innerHTML=items.map(function(it){
    return '<div class="sc2" data-name="'+esc(it.n)+'"><div class="si2">'+it.i+'</div><div class="sn">'+esc(it.n)+'</div></div>';
  }).join('');
  grid.addEventListener('click',function(e){
    var card=e.target.closest('.sc2');
    if(!card) return;
    var name=card.dataset.name;
    ST.ints[name]=(ST.ints[name]||0)+1;
    localStorage.setItem('at_ints',JSON.stringify(ST.ints));
    document.getElementById('sTm').value=name;
    go('sim', document.getElementById('nb-sim'));
  });
}

function buildSel(){
  var sel=document.getElementById('sSub');
  var o='<option value="">Materia...</option>';
  Object.entries(SUBS).forEach(function(entry){
    o+='<optgroup label="'+entry[0]+'">'+entry[1].items.map(function(it){return '<option>'+esc(it.n)+'</option>';}).join('')+'</optgroup>';
  });
  sel.innerHTML=o;
}

function startSim(){
  var tema=document.getElementById('sTm').value.trim();
  var desc=document.getElementById('sDe').value.trim();
  if(!tema){alert('Escribe un tema');return;}
  ST.tema=tema;
  ST.ints[tema]=(ST.ints[tema]||0)+1;
  localStorage.setItem('at_ints',JSON.stringify(ST.ints));
  document.getElementById('s0').style.display='none';
  document.getElementById('s1').style.display='block';
  document.getElementById('sEv').style.display='none';
  if(!desc){
    document.getElementById('sQB').innerHTML=
      '<div class="bbl"><p>Tema: <strong>'+esc(tema)+'</strong><br><br>¿Cómo quieres estudiar?</p></div>'+
      '<div style="display:flex;flex-direction:column;gap:8px" id="optBtns">'+
      '<button class="btn" style="background:linear-gradient(135deg,#3b82f6,#06b6d4)" id="opt0">📖 Contexto — Que Atlas explique primero</button>'+
      '<button class="btn" style="background:linear-gradient(135deg,#8b5cf6,#ec4899)" id="opt1">🔘 Solo preguntas — Ir directo</button>'+
      '<button class="btn" style="background:linear-gradient(135deg,#f59e0b,#10b981)" id="opt2">⚡ Todo junto — Explicación + preguntas</button>'+
      '</div>';
    document.getElementById('opt0').addEventListener('click',function(){runOpt(0);});
    document.getElementById('opt1').addEventListener('click',function(){runOpt(1);});
    document.getElementById('opt2').addEventListener('click',function(){runOpt(2);});
    return;
  }
  buildQ(tema);
}

function runOpt(opt){
  var tema=ST.tema;
  var d=DATA[tema];
  if(opt===0){
    var exp=d?d.exp:'No hay contenido pregenerado para este tema.';
    document.getElementById('sQB').innerHTML=
      '<div class="bbl"><p>'+nl(exp)+'</p></div>'+
      '<button class="btn" id="btnCont">Continuar a preguntas →</button>';
    document.getElementById('btnCont').addEventListener('click',function(){buildQ(tema);});
  } else if(opt===1){
    buildQ(tema);
  } else {
    var exp2=d?d.exp:'';
    document.getElementById('sQB').innerHTML='<div class="bbl"><p>'+nl(exp2)+'</p></div>';
    setTimeout(function(){buildQ(tema);},100);
  }
}

function buildQ(tema){
  var d=DATA[tema];
  ST.ans={}; ST.cors={};
  if(!d){
    document.getElementById('sQB').innerHTML='<div class="bbl"><p>No hay preguntas para <strong>'+esc(tema)+'</strong> en modo offline.<br><br>Temas disponibles:<br>'+Object.keys(DATA).map(function(k){return '• '+k;}).join('<br>')+'</p></div>';
    return;
  }
  var box=document.getElementById('sQB');
  if(ST.mode==='m'||ST.mode==='a'||ST.mode==='t'){
    var qs=sf(d.mc.slice()).slice(0,10);
    ST.tot=qs.length; box.innerHTML='';
    qs.forEach(function(q,i){
      var shuffled=sf(q.o.map(function(op,oi){return {t:op,o:oi};}));
      var ci=shuffled.findIndex(function(x){return x.o===q.c;});
      ST.cors[i]=ci;
      var html2='<div class="bbl" id="q'+i+'"><p style="font-weight:500;margin-bottom:6px">'+(i+1)+'. '+esc(q.p)+'</p><ul class="ol">';
      shuffled.forEach(function(op,oi){
        html2+='<li data-qi="'+i+'" data-oi="'+oi+'">'+esc(op.t)+'</li>';
      });
      html2+='</ul></div>';
      box.innerHTML+=html2;
    });
    box.addEventListener('click',function(e){
      var li=e.target.closest('li[data-qi]');
      if(!li) return;
      var qi=parseInt(li.dataset.qi);
      document.getElementById('q'+qi).querySelectorAll('li').forEach(function(l){l.style.cssText='';});
      li.style.borderColor='var(--ac)'; li.style.background='rgba(59,130,246,.12)';
      ST.ans[qi]=parseInt(li.dataset.oi);
      updPr(Object.keys(ST.ans).length,ST.tot);
    });
    updPr(0,ST.tot);
    document.getElementById('sEv').style.display='block';
  } else if(ST.mode==='v'){
    var qs2=sf(d.vf.slice()).slice(0,10);
    ST.tot=qs2.length; box.innerHTML='';
    qs2.forEach(function(q,i){
      ST.cors[i]=q.r?'V':'F';
      box.innerHTML+='<div class="bbl" id="q'+i+'">'+
        '<p style="font-weight:500;margin-bottom:6px">'+(i+1)+'. '+esc(q.a)+'</p>'+
        '<div style="display:flex;gap:7px">'+
        '<button class="btn2" data-qi="'+i+'" data-v="V">✅ Verdadero</button>'+
        '<button class="btn2" data-qi="'+i+'" data-v="F">❌ Falso</button>'+
        '</div>'+
        '<p id="ex'+i+'" style="display:none;font-size:11px;color:var(--tx2);margin-top:5px;padding:6px;background:var(--bg3);border-radius:6px">'+esc(q.e)+'</p>'+
        '</div>';
    });
    box.addEventListener('click',function(e){
      var btn=e.target.closest('[data-v]');
      if(!btn) return;
      var qi=parseInt(btn.dataset.qi);
      document.getElementById('q'+qi).querySelectorAll('[data-v]').forEach(function(b){b.classList.remove('on');});
      btn.classList.add('on');
      ST.ans[qi]=btn.dataset.v;
      updPr(Object.keys(ST.ans).length,ST.tot);
    });
    updPr(0,ST.tot);
    document.getElementById('sEv').style.display='block';
  } else if(ST.mode==='e'){
    box.innerHTML=d.ej.map(function(e2,i){
      return '<div class="bbl"><p><strong>Ejercicio '+(i+1)+'</strong><br><br>'+esc(e2.p)+'</p>'+
        '<button class="btn2 showSol" style="width:100%;margin-top:8px">Ver solución</button>'+
        '<div class="solBox" style="display:none;margin-top:7px;padding:8px;background:var(--bg3);border-radius:6px;font-size:12px;color:var(--gr)">'+nl(e2.s)+'</div></div>';
    }).join('');
    box.querySelectorAll('.showSol').forEach(function(btn){
      btn.addEventListener('click',function(){
        btn.nextElementSibling.style.display='block'; btn.style.display='none';
      });
    });
    var btn3=document.createElement('button');
    btn3.className='btn'; btn3.style.marginTop='10px'; btn3.textContent='✓ Terminé los ejercicios';
    btn3.addEventListener('click',function(){showRes(90,tema);});
    box.appendChild(btn3);
  } else if(ST.mode==='n'){
    box.innerHTML='<div class="bbl"><p>'+nl(d.exp)+'</p></div>';
    var btn4=document.createElement('button');
    btn4.className='btn'; btn4.style.marginTop='10px'; btn4.textContent='✓ Leído — ir a preguntas';
    btn4.addEventListener('click',function(){ST.mode='m'; buildQ(tema);});
    box.appendChild(btn4);
  }
}

function updPr(d2,t){document.getElementById('sPr').style.width=t?(d2/t*100)+'%':'0%';}

function evalSim(){
  var correct=0;
  Object.entries(ST.cors).forEach(function(entry){
    var qi=entry[0], c=entry[1];
    var ua=ST.ans[parseInt(qi)];
    var qEl=document.getElementById('q'+qi);
    if(typeof c==='string'){
      var ex=document.getElementById('ex'+qi);
      if(ex) ex.style.display='block';
      qEl.querySelectorAll('[data-v]').forEach(function(b){
        if(b.dataset.v===c) b.style.borderColor='var(--gr)';
      });
      if(ua===c) correct++;
    } else {
      qEl.querySelectorAll('li').forEach(function(li,i){
        if(i===c) li.classList.add('ok');
        else if(i===ua) li.classList.add('no');
      });
      if(ua===c) correct++;
    }
  });
  var score=ST.tot>0?Math.round(correct/ST.tot*100):0;
  document.getElementById('sEv').style.display='none';
  showRes(score,ST.tema);
}

function showRes(score,tema){
  document.getElementById('s1').style.display='none';
  document.getElementById('s2').style.display='block';
  document.getElementById('sFin').textContent=score+'%';
  var msg=score>=90?'¡Excelente! Dominas este tema. 🏆':score>=75?'¡Muy bien! Hay algunos puntos a reforzar.':score>=60?'Bien. Repasa los errores marcados en rojo.':'Sigue practicando. Cada intento mejora. 💪';
  document.getElementById('sFB').innerHTML='<p>'+msg+'<br><br>Resultado: '+score+'% en "'+esc(tema)+'".</p>';
  ST.hist.unshift({date:new Date().toLocaleDateString('es-EC'),subject:tema,mode:ST.mode,score:score});
  if(ST.hist.length>60) ST.hist.pop();
  localStorage.setItem('at_hist',JSON.stringify(ST.hist));
  loadSt(); renderAch(); renderHist();
}

function resetSim(){
  document.getElementById('s0').style.display='block';
  document.getElementById('s1').style.display='none';
  document.getElementById('s2').style.display='none';
  document.getElementById('sPr').style.width='0%';
  ST.ans={}; ST.cors={};
}

function genExam(){
  var titulo=document.getElementById('exT').value||'Examen Atlas';
  var temas=document.getElementById('exTm').value.trim();
  if(!temas){alert('Escribe los temas');return;}
  var cant=parseInt(document.getElementById('exC').value)||20;
  var all=[];
  Object.keys(DATA).forEach(function(k){
    if(temas.toLowerCase().indexOf(k.toLowerCase())>=0){
      DATA[k].mc.forEach(function(q){all.push(Object.assign({},q,{tema:k}));});
    }
  });
  if(!all.length){
    document.getElementById('exO').innerHTML='<div class="bbl"><p>No hay contenido para esos temas.<br>Disponibles: <strong>'+Object.keys(DATA).join(', ')+'</strong></p></div>';
    return;
  }
  var sel=sf(all).slice(0,Math.min(cant,all.length));
  var h='<div class="bbl"><p style="font-family:monospace;font-size:11px;line-height:2">'+
    '━━━━━━━━━━━━━━━━━━━━━━━<br>📋 <strong>'+esc(titulo.toUpperCase())+'</strong><br>'+
    'Nombre: _____________________ Fecha: _______<br>━━━━━━━━━━━━━━━━━━━━━━━<br><br>';
  sel.forEach(function(q,i){
    h+='<strong>'+(i+1)+'.</strong> '+esc(q.p)+'<br>';
    q.o.forEach(function(op,oi){h+='&nbsp;&nbsp;'+String.fromCharCode(65+oi)+') '+esc(op)+'<br>';});
    h+='<br>';
  });
  h+='━━━━━━━━━━━━━━━━━━━━━━━<br><strong>RESPUESTAS:</strong> '+sel.map(function(q,i){return (i+1)+':'+String.fromCharCode(65+q.c);}).join(' | ');
  h+='</p></div>';
  document.getElementById('exO').innerHTML=h;
}

function explicar(){
  var tema=document.getElementById('tTm').value.trim();
  if(!tema){alert('Escribe un tema');return;}
  var d=DATA[tema];
  var out=document.getElementById('tXO');
  if(d){
    out.innerHTML='<div class="bbl"><p>'+nl(d.exp)+'</p>'+
      '<div style="display:flex;gap:6px;margin-top:10px">'+
      '<button class="btn2" id="btnVEj" style="flex:1">📐 Ejercicios</button>'+
      '<button class="btn2" id="btnPrac" style="flex:1">🔘 Practicar</button>'+
      '</div></div>';
    document.getElementById('btnVEj').addEventListener('click',function(){
      var html2='<div class="bbl"><p><strong>Ejercicios de '+esc(tema)+'</strong><br><br>';
      d.ej.forEach(function(e2,i){
        html2+='<strong>'+(i+1)+'.</strong> '+esc(e2.p)+'<br>'+
          '<details style="margin:3px 0"><summary style="color:var(--ac);cursor:pointer;font-size:12px">Ver solución</summary>'+
          '<p style="font-size:12px;color:var(--gr);padding:6px;background:var(--bg3);border-radius:6px;margin-top:3px">'+nl(e2.s)+'</p></details><br>';
      });
      out.innerHTML+=html2+'</p></div>';
    });
    document.getElementById('btnPrac').addEventListener('click',function(){
      document.getElementById('sTm').value=tema;
      go('sim', document.getElementById('nb-sim'));
    });
  } else {
    var found=null;
    Object.values(LIB).forEach(function(cat){
      cat.forEach(function(it){
        if(!found&&it.t.toLowerCase().indexOf(tema.toLowerCase())>=0) found=it;
      });
    });
    if(found) out.innerHTML='<div class="bbl"><p><strong>'+esc(found.t)+'</strong><br><br>'+esc(found.x)+'</p></div>';
    else out.innerHTML='<div class="bbl"><p>Tema no disponible offline.<br><br>Disponibles: '+Object.keys(DATA).join(', ')+'</p></div>';
  }
}

function resolver(){
  var txt=document.getElementById('tTx').value.trim();
  if(!txt){alert('Escribe tu ejercicio');return;}
  var lc=txt.toLowerCase();
  var r='';
  if(lc.indexOf('cinemat')>=0||lc.indexOf('velocidad')>=0||lc.indexOf('acelerac')>=0||lc.indexOf('distancia')>=0){
    r='⚡ <strong>Cinemática</strong><br><br>Fórmulas:<br>v=d/t | a=(vf-vi)/t | x=v₀t+½at² | vf²=vi²+2ax<br><br>Pasos: 1) Identifica datos 2) Identifica incógnita 3) Elige fórmula 4) Despeja y calcula';
  } else if(lc.indexOf('x²')>=0||lc.indexOf('x2')>=0||lc.indexOf('cuadrat')>=0){
    r='📐 <strong>Ecuación cuadrática</strong><br><br>x = (-b ± raíz(b²-4ac)) / 2a<br><br>1) Identifica a, b, c<br>2) Calcula Δ=b²-4ac<br>3) Si Δ>0: 2 soluciones<br>4) Aplica la fórmula';
  } else if(lc.indexOf('área')>=0||lc.indexOf('perímetro')>=0||lc.indexOf('volumen')>=0){
    r='📐 <strong>Geometría</strong><br><br>Círculo: A=πr² | P=2πr<br>Rectángulo: A=b×h | P=2(b+h)<br>Triángulo: A=b×h/2<br>Esfera: V=4/3πr³';
  } else if(lc.indexOf('ph')>=0||lc.indexOf('mol')>=0||lc.indexOf('átomo')>=0){
    r='🧪 <strong>Química</strong><br><br>Moles: n=m/M<br>pH=-log[H+]<br>PV=nRT (gas ideal)<br><br>Identifica el tipo y aplica la fórmula.';
  } else if(lc.indexOf('%')>=0||lc.indexOf('porcent')>=0||lc.indexOf('descuento')>=0){
    r='💰 <strong>Porcentajes</strong><br><br>X% de N = (X÷100)×N<br>Descuento: Precio×(1-desc%/100)';
  } else {
    r='📝 Para resolver este ejercicio offline revisa:<br>• Fórmulas en Biblioteca<br>• Explicaciones en Explícame<br><br>Temas con resolución: física, cinemática, ecuaciones cuadráticas, geometría, química, porcentajes.';
  }
  document.getElementById('tRO').innerHTML='<div class="bbl"><p>'+r+'</p></div>';
}

function renderLib(srch){
  srch=srch||'';
  var data=(LIB[ST.lt]||[]).filter(function(it){
    return !srch||it.t.toLowerCase().indexOf(srch.toLowerCase())>=0||it.x.toLowerCase().indexOf(srch.toLowerCase())>=0;
  });
  var c=document.getElementById('libC');
  c.innerHTML=data.map(function(it,i){
    return '<div class="lc" data-li="'+i+'"><h4>'+esc(it.t)+'</h4><p>'+esc(it.x.substring(0,80))+'...</p><div class="lm">'+esc(it.m)+'</div></div>';
  }).join('');
  c.querySelectorAll('.lc').forEach(function(el){
    el.addEventListener('click',function(){
      var it=LIB[ST.lt][parseInt(el.dataset.li)];
      openM(it.t,'<p style="font-size:13px;line-height:1.8">'+nl(it.x)+'</p>');
    });
  });
}

function renderAux(){
  var data=AUX[ST.at]||[];
  var c=document.getElementById('auxC');
  c.innerHTML='<div class="eg">'+data.map(function(it,i){
    return '<div class="ec" data-ai="'+i+'"><div class="ei">'+it.i+'</div><p>'+esc(it.t)+'</p></div>';
  }).join('')+'</div>';
  c.querySelectorAll('.ec').forEach(function(el){
    el.addEventListener('click',function(){
      var it=AUX[ST.at][parseInt(el.dataset.ai)];
      openM(it.t,'<p style="font-size:13px;line-height:1.9">'+nl(it.x)+'</p>');
    });
  });
}

function renderHist(){
  var c=document.getElementById('histC');
  if(!ST.hist.length){c.innerHTML='<p style="color:var(--tx3);text-align:center;padding:40px 0">Sin sesiones aún</p>';return;}
  c.innerHTML=ST.hist.map(function(h){
    return '<div class="hi"><div><div style="font-size:13px;font-weight:500">'+esc(h.subject)+'</div><div style="font-size:11px;color:var(--tx2)">'+h.date+' · '+h.mode+'</div></div><div class="hs '+(h.score>=80?'h':h.score>=60?'m':'l')+'">'+h.score+'%</div></div>';
  }).join('');
}

function loadSt(){
  document.getElementById('stS').textContent=ST.hist.length;
  if(ST.hist.length){
    document.getElementById('stA').textContent=Math.round(ST.hist.reduce(function(a,h){return a+h.score;},0)/ST.hist.length)+'%';
    document.getElementById('stB').textContent=Math.max.apply(null,ST.hist.map(function(h){return h.score;}))+'%';
  }
}

var ACHS=[
  {id:'f1',i:'🌟',t:'Primera sesión',d:'Completa una práctica',ck:function(){return ST.hist.length>=1;}},
  {id:'f5',i:'📚',t:'Estudiante',d:'5 sesiones completadas',ck:function(){return ST.hist.length>=5;}},
  {id:'f10',i:'🔥',t:'Constante',d:'10 sesiones completadas',ck:function(){return ST.hist.length>=10;}},
  {id:'p',i:'💯',t:'Perfecto',d:'Obtén 100%',ck:function(){return ST.hist.some(function(h){return h.score===100;});}},
  {id:'poly',i:'🌍',t:'Políglota',d:'Estudia 3 materias distintas',ck:function(){return new Set(ST.hist.map(function(h){return h.subject;})).size>=3;}}
];
function renderAch(){
  document.getElementById('achList').innerHTML=ACHS.map(function(a){
    return '<div class="ach '+(a.ck()?'ok':'no')+'"><div style="font-size:24px">'+a.i+'</div><div><div style="font-size:13px;font-weight:500">'+a.t+'</div><div style="font-size:11px;color:var(--tx2)">'+a.d+'</div></div></div>';
  }).join('');
}

function renderProf(){
  var c=document.getElementById('profC');
  if(ST.pt==='c'){
    c.innerHTML='<div style="background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:14px">'+
      '<label style="font-size:11px;color:var(--tx2);display:block;margin-bottom:6px">Tema:</label>'+
      '<input type="text" id="ptT" placeholder="Ej: Cinemática, Historia..." style="margin-bottom:8px">'+
      '<select id="ptTipo" style="margin-bottom:8px"><option>10 opción múltiple</option><option>10 verdadero/falso</option><option>5 ejercicios</option></select>'+
      '<button class="btn" id="btnCrearTarea">Generar tarea</button>'+
      '<div id="ptO" style="margin-top:10px"></div></div>';
    document.getElementById('btnCrearTarea').addEventListener('click',crearTarea);
  } else {
    var students=JSON.parse(localStorage.getItem('at_students')||'[]');
    c.innerHTML='<div style="background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:14px;margin-bottom:10px">'+
      '<input type="text" id="stName" placeholder="Nombre del alumno..." style="margin-bottom:8px">'+
      '<button class="btn" id="btnAddStud">Agregar alumno</button></div>'+
      (students.map(function(s){return '<div class="hi"><div style="font-size:13px">'+esc(s.n)+'</div><div class="hs h">'+(s.avg||'—')+'</div></div>';}).join('')||'<p style="color:var(--tx3);text-align:center;padding:20px">Sin alumnos</p>');
    document.getElementById('btnAddStud').addEventListener('click',function(){
      var n=document.getElementById('stName').value.trim();
      if(!n) return;
      var students2=JSON.parse(localStorage.getItem('at_students')||'[]');
      students2.push({n:n,avg:'—'});
      localStorage.setItem('at_students',JSON.stringify(students2));
      renderProf();
    });
  }
}

function crearTarea(){
  var tema=document.getElementById('ptT').value.trim();
  if(!tema){alert('Escribe un tema');return;}
  var tipo=document.getElementById('ptTipo').value;
  var d=DATA[tema];
  var out=document.getElementById('ptO');
  if(!d){out.innerHTML='<div class="bbl"><p>No hay contenido para ese tema. Disponibles: '+Object.keys(DATA).join(', ')+'</p></div>';return;}
  var h='<div class="bbl"><p style="font-family:monospace;font-size:11px;line-height:2">━━━━━━━━━━━━━━━━━━━━━━━<br>📋 TAREA: '+esc(tema.toUpperCase())+'<br>Nombre: _____________________ Fecha: _______<br>━━━━━━━━━━━━━━━━━━━━━━━<br><br>';
  if(tipo.indexOf('ejercicio')>=0){
    d.ej.forEach(function(e2,i){h+=(i+1)+'. '+esc(e2.p)+'<br><br>';});
    h+='━━━━━━━━━━━━━━━━━━━━━━━<br><strong>Soluciones:</strong><br><br>';
    d.ej.forEach(function(e2,i){h+=''+(i+1)+'. '+nl(e2.s)+'<br><br>';});
  } else if(tipo.indexOf('verdadero')>=0){
    var qs3=sf(d.vf.slice()).slice(0,10);
    qs3.forEach(function(q,i){h+=''+(i+1)+'. '+esc(q.a)+'<br>( ) Verdadero &nbsp; ( ) Falso<br><br>';});
    h+='━━━━━━━━━━━━━━━━━━━━━━━<br>Respuestas: '+qs3.map(function(q,i){return ''+(i+1)+':'+(q.r?'V':'F');}).join(' | ');
  } else {
    var qs4=sf(d.mc.slice()).slice(0,10);
    qs4.forEach(function(q,i){h+=''+(i+1)+'. '+esc(q.p)+'<br>';q.o.forEach(function(op,oi){h+='&nbsp;'+String.fromCharCode(65+oi)+') '+esc(op)+'<br>';});h+='<br>';});
    h+='━━━━━━━━━━━━━━━━━━━━━━━<br>Respuestas: '+qs4.map(function(q,i){return ''+(i+1)+':'+String.fromCharCode(65+q.c);}).join(' | ');
  }
  out.innerHTML=h+'</p></div>';
}

function creaTool(tool){
  var out=document.getElementById('creaO');
  if(tool==='stats'){
    var top=Object.entries(ST.ints).sort(function(a,b){return b[1]-a[1];}).slice(0,8);
    out.innerHTML='<div class="bbl"><p>📊 <strong>Top materias:</strong><br><br>'+(top.length?top.map(function(e2){return e2[0]+': '+e2[1]+' vez'+(e2[1]>1?'es':'');}).join('<br>'):'Sin datos aún')+'</p></div>';
  } else if(tool==='ideas'){
    out.innerHTML='<div class="bbl"><p>💡 Ideas: '+ST.ideas.length+'<br><br>'+(ST.ideas.map(function(id,i){return ''+(i+1)+'. '+esc(id.t);}).join('<br>')||'Ninguna aún')+'</p></div>';
  } else if(tool==='mod'){
    out.innerHTML='<div class="bbl"><p>🛡️ Sesiones: '+ST.hist.length+'<br>Ideas: '+ST.ideas.length+'<br>Alumnos: '+JSON.parse(localStorage.getItem('at_students')||'[]').length+'</p></div>';
  } else if(tool==='exp'){
    var blob=new Blob([JSON.stringify({hist:ST.hist,ints:ST.ints,ideas:ST.ideas},null,2)],{type:'application/json'});
    var a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='atlas_datos.json'; a.click();
    out.innerHTML='<div class="bbl"><p>✅ Datos exportados.</p></div>';
  }
}

function sendIdea(){
  var txt=document.getElementById('ideaI').value.trim();
  if(!txt) return;
  ST.ideas.push({t:txt,d:new Date().toLocaleDateString('es-EC')});
  localStorage.setItem('at_ideas',JSON.stringify(ST.ideas));
  document.getElementById('ideaI').value='';
  renderIdeas(); alert('¡Idea enviada!');
}

function renderIdeas(){
  document.getElementById('ideasL').innerHTML=ST.ideas.length?
    ST.ideas.map(function(id,i){return '<div style="background:var(--bg3);border-radius:7px;padding:7px;margin-bottom:5px;font-size:12px;color:var(--tx2)">'+esc(id.t)+' <span style="color:var(--tx3)">('+id.d+')</span></div>';}).join(''):
    '<p style="color:var(--tx3);font-size:12px">Sin ideas aún</p>';
}
</script>
</body>
</html>
