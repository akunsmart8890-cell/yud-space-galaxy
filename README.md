<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>BOT-V6 ULTRA PRO</title>
<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:radial-gradient(circle at top,#0f172a,#000000 70%);
    color:white;
    overflow:hidden;
}

.splash{
    position:absolute;
    width:100%;
    height:100%;
    background:#111827;
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
    z-index:10;
    animation:splashFade 2s forwards;
}

@keyframes splashFade{
    0%{opacity:1;}
    100%{opacity:0; pointer-events:none;}
}

.splash h1{
    color:#00f2ff;
    font-size:30px;
    margin-bottom:20px;
    animation:glow 1.5s infinite alternate;
}

@keyframes glow{
    0%{text-shadow:0 0 5px #00f2ff;}
    100%{text-shadow:0 0 25px #00f2ff,0 0 50px #ff00ff;}
}

.card{
    width:340px;
    padding:40px 25px;
    border-radius:25px;
    background:rgba(255,255,255,0.05);
    backdrop-filter:blur(15px);
    text-align:center;
    box-shadow:0 0 50px rgba(0,255,255,0.3);
    position:relative;
    overflow:hidden;
}

.card::before{
    content:"";
    position:absolute;
    width:150%;
    height:150%;
    background:linear-gradient(45deg,#00f2ff,#ff00ff,#00f2ff);
    top:-50%;
    left:-50%;
    animation:rotate 6s linear infinite;
    opacity:0.15;
}

@keyframes rotate{
    0%{transform:rotate(0deg);}
    100%{transform:rotate(360deg);}
}

h1{
    font-size:22px;
    margin-bottom:25px;
    color:#00f2ff;
    letter-spacing:2px;
    position:relative;
}

.score{
    font-size:65px;
    font-weight:bold;
    margin:25px 0;
    color:#ffd700;
    text-shadow:0 0 25px #ffd700;
    transition:0.3s;
    position:relative;
}

button{
    padding:14px 30px;
    border:none;
    border-radius:30px;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
    background:linear-gradient(45deg,#00f2ff,#00c3ff);
    color:black;
    transition:0.3s;
    position:relative;
}

button:hover{
    transform:scale(1.1);
    box-shadow:0 0 30px #00f2ff;
}

.loading{
    font-size:14px;
    margin-top:15px;
    opacity:0.7;
    height:18px;
}
</style>
</head>

<body>

<!-- Splash Screen -->
<div class="splash">
    <h1>🚀 BOT-V6 ULTRA PRO</h1>
    <div>Loading...</div>
</div>

<div class="card">
    <h1>🚀 BOT-V6 ULTRA PRO</h1>
    <div class="score" id="hasil">0.00x</div>
    <button onclick="prediksi()">PREDIKSI</button>
    <div class="loading" id="loading"></div>
</div>

<script>
// Hapus splash setelah 2 detik
setTimeout(()=>{
    document.querySelector('.splash').style.display='none';
},2000);

// Prediksi skor
function prediksi(){
    let loadingText = document.getElementById("loading");
    let hasil = document.getElementById("hasil");

    // Loading effect
    loadingText.innerHTML = "Menganalisis...";
    hasil.style.transform = "scale(0.8)";
    hasil.style.opacity = "0.5";

    // Sound effect & vibration
    playSound();
    if(navigator.vibrate) navigator.vibrate(150);

    setTimeout(function(){
        let angka = (Math.random()*10+1).toFixed(2);
        hasil.innerHTML = angka + "x";
        hasil.style.transform = "scale(1.2)";
        hasil.style.opacity = "1";
        loadingText.innerHTML = "Prediksi Selesai ✔";
        setTimeout(()=>{hasil.style.transform="scale(1)";},200);
    },1000);
}

// Sound effect sederhana
function playSound(){
    let audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    let o = audioCtx.createOscillator();
    let g = audioCtx.createGain();
    o.type = 'sine';
    o.frequency.value = 440; // nada
    o.connect(g);
    g.connect(audioCtx.destination);
    o.start();
    o.stop(audioCtx.currentTime + 0.2);
}
</script>

</body>
</html>
