<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Liquid Metrics Dashboard</title>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, sans-serif;
}

body{
    display:flex;
    background:#061326;
    color:white;
    min-height:100vh;
}

/* SIDEBAR */
.sidebar{
    width:280px;
    background:#071a31;
    padding:25px;
    display:flex;
    flex-direction:column;
    justify-content:space-between;
}

.logo{
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:40px;
}

.logo i{font-size:45px;color:#1da1ff;}
.logo span{color:#2eb3ff;}
.logo p{color:#a8c7ff;font-size:14px;}

.menu{list-style:none;}

.menu li{
    padding:16px;
    margin-bottom:15px;
    border-radius:15px;
    cursor:pointer;
}

.menu li:hover,
.menu li.active{
    background:linear-gradient(90deg,#246fff,#2da8ff);
}

/* MAIN */
.main{
    flex:1;
    padding:25px;
}

/* PAGES */
.page{display:none;}
.page.active{display:block;}

/* CARDS */
.cards{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:20px;
}

.card{
    background:#0c203a;
    padding:20px;
    border-radius:20px;
}

.card .value{
    font-size:32px;
    font-weight:bold;
}

/* PANELS */
.panel{
    background:#0c203a;
    padding:20px;
    border-radius:20px;
    margin-top:20px;
}

/* WATER TANK */
.tank{
    width:220px;
    height:260px;
    border:8px solid rgba(255,255,255,0.2);
    border-radius:25px;
    margin:auto;
    position:relative;
    overflow:hidden;
}

.water{
    position:absolute;
    bottom:0;
    width:100%;
    height:78%;
    background:linear-gradient(to top,#1f8fff,#7dd3ff);
}

.level-text{
    text-align:center;
    font-size:28px;
    margin-top:10px;
}

/* QUALITY */
.quality{
    display:grid;
    grid-template-columns:repeat(5,1fr);
    gap:15px;
}

.q-card{
    background:#0c203a;
    padding:15px;
    border-radius:15px;
}

/* ALERTS */
.alert-item{
    padding:12px;
    border-bottom:1px solid rgba(255,255,255,0.1);
}

/* CHART */
canvas{
    max-height:300px;
}
</style>
</head>

<body>

<!-- SIDEBAR -->
<div class="sidebar">

<div>
<div class="logo">
<i class="fa-solid fa-droplet"></i>
<div>
<h1>LIQUID <span>METRICS</span></h1>
<p>Water Monitoring System</p>
</div>
</div>

<ul class="menu">
<li class="active" onclick="showPage('dashboard')">Dashboard</li>
<li onclick="showPage('quantity')">Water Quantity</li>
<li onclick="showPage('quality')">Water Quality</li>
<li onclick="showPage('logs')">History & Logs</li>
<li onclick="showPage('alerts')">Alerts</li>
</ul>
</div>

<div style="background:#0c203a;padding:20px;border-radius:15px;">
<p>System Status</p>
<h2 style="color:#22ff88;">ONLINE</h2>
</div>

</div>

<!-- MAIN -->
<div class="main">

<!-- DASHBOARD -->
<div id="dashboard" class="page active">

<div class="cards">
<div class="card"><h3>Water Level</h3><div class="value" id="wl">78%</div></div>
<div class="card"><h3>Flow Rate</h3><div class="value" id="fr">12.6</div></div>
<div class="card"><h3>Consumption</h3><div class="value" id="cs">245</div></div>
<div class="card"><h3>Status</h3><div class="value">GOOD</div></div>
</div>

<!-- WATER -->
<div class="panel">
<h3>Water Level</h3>
<div class="tank">
<div class="water"></div>
</div>
<div class="level-text" id="wl2">78%</div>
</div>

<!-- GRAPH -->
<div class="panel">
<h3>Water Flow Graph</h3>
<canvas id="flowChart"></canvas>
</div>

<!-- QUALITY ON DASHBOARD -->
<div class="panel">
<h3>Water Quality Overview</h3>

<div class="quality">
<div class="q-card"><h3>pH</h3><h2 id="ph">7.3</h2></div>
<div class="q-card"><h3>Turbidity</h3><h2 id="tur">1.2 NTU</h2></div>
<div class="q-card"><h3>Temp</h3><h2 id="temp">28°C</h2></div>
<div class="q-card"><h3>Conductivity</h3><h2 id="cond">312</h2></div>
<div class="q-card"><h3>TDS</h3><h2 id="tds">156</h2></div>
</div>

</div>

</div>

<!-- WATER QUANTITY -->
<div id="quantity" class="page">
<div class="panel">
<h2>Water Quantity</h2>

<div class="tank">
<div class="water"></div>
</div>

<div class="level-text" id="wl3">78%</div>
</div>
</div>

<!-- QUALITY PAGE -->
<div id="quality" class="page">
<div class="panel">
<h2>Water Quality Details</h2>

<div class="quality">
<div class="q-card"><h3>pH</h3><h2 id="ph2">7.3</h2></div>
<div class="q-card"><h3>Turbidity</h3><h2 id="tur2">1.2</h2></div>
<div class="q-card"><h3>Temperature</h3><h2 id="temp2">28°C</h2></div>
<div class="q-card"><h3>Conductivity</h3><h2 id="cond2">312</h2></div>
<div class="q-card"><h3>TDS</h3><h2 id="tds2">156</h2></div>
</div>

</div>
</div>

<!-- LOGS -->
<div id="logs" class="page">
<div class="panel">
<h2>History & Logs</h2>
<div class="alert-item">System started</div>
<div class="alert-item">Sensor updated</div>
<div class="alert-item">Data recorded</div>
</div>
</div>

<!-- ALERTS -->
<div id="alerts" class="page">
<div class="panel">
<h2>Alerts</h2>
<div class="alert-item">All systems normal</div>
</div>
</div>

</div>

<!-- NAV -->
<script>
function showPage(page){

document.querySelectorAll(".page").forEach(p=>{
p.classList.remove("active");
});

document.getElementById(page).classList.add("active");

document.querySelectorAll(".menu li").forEach(li=>{
li.classList.remove("active");
});

event.target.classList.add("active");
}
</script>

<!-- BACKEND -->
<script>
async function loadData(){

try{
const res = await fetch("/api/sensors");
const d = await res.json();

document.querySelectorAll(".water").forEach(w=>{
w.style.height = d.waterLevel + "%";
});

document.getElementById("wl").innerText = d.waterLevel + "%";
document.getElementById("wl2").innerText = d.waterLevel + "%";
document.getElementById("wl3").innerText = d.waterLevel + "%";

document.getElementById("fr").innerText = d.flowRate;
document.getElementById("cs").innerText = d.consumption;

document.getElementById("ph").innerText = d.ph;
document.getElementById("tur").innerText = d.turbidity;
document.getElementById("temp").innerText = d.temperature + "°C";
document.getElementById("cond").innerText = d.conductivity;
document.getElementById("tds").innerText = d.tds;

}catch(e){
console.log("No backend connected yet");
}
}

setInterval(loadData,2000);
loadData();
</script>

<script>
const ctx = document.getElementById("flowChart");

new Chart(ctx, {
type: "line",
data: {
labels: ["09:00","09:15","09:30","09:45","10:00","10:15","10:30"],
datasets: [{
label: "Flow Rate",
data: [8,12,15,14,18,11,12],
borderColor: "#2da8ff",
backgroundColor: "rgba(45,168,255,0.2)",
fill: true,
tension: 0.4
}]
},
options: {
responsive: true,
plugins:{
legend:{labels:{color:"white"}}
},
scales:{
x:{ticks:{color:"white"}},
y:{ticks:{color:"white"}}
}
}
});
</script>

</body>
</html>
