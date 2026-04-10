<!DOCTYPE html>
<html lang="pt-br">
<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>THE BARBER</title>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial;
}

body{
background:#000;
color:white;
overflow-x:hidden;
}

/* LOADER */

#loader{
position:fixed;
width:100%;
height:100%;
background:black;
display:flex;
justify-content:center;
align-items:center;
z-index:999;
}

.loader-barber{
font-size:40px;
color:red;
animation:pulse 1.5s infinite;
}

@keyframes pulse{
0%{transform:scale(1)}
50%{transform:scale(1.2)}
100%{transform:scale(1)}
}

/* NAV */

nav{
display:flex;
justify-content:space-between;
padding:20px;
background:black;
border-bottom:2px solid red;
position:sticky;
top:0;
}

nav h1{
color:red;
}

nav a{
color:white;
margin:0 10px;
text-decoration:none;
}

/* HERO */

.hero{
height:90vh;
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
text-align:center;
background:linear-gradient(rgba(0,0,0,0.7),rgba(0,0,0,0.9)),
url("https://images.unsplash.com/photo-1621605815971-fbc98d665033");
background-size:cover;
animation:fade 2s;
}

@keyframes fade{
from{opacity:0}
to{opacity:1}
}

.hero h2{
font-size:60px;
margin-bottom:20px;
}

.hero button{
padding:15px 35px;
background:red;
border:none;
color:white;
font-size:18px;
cursor:pointer;
border-radius:5px;
box-shadow:0 0 15px red;
transition:.3s;
}

.hero button:hover{
transform:scale(1.1);
box-shadow:0 0 25px red;
}

/* SERVIÇOS */

.servicos{
padding:80px 10%;
text-align:center;
}

.cards{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
gap:25px;
margin-top:40px;
}

.card{
background:#111;
padding:30px;
border-radius:12px;
border:1px solid #333;
transition:.4s;
transform-style:preserve-3d;
}

.card:hover{
transform:rotateY(10deg) scale(1.05);
border-color:red;
box-shadow:0 0 20px red;
}

.card input{
margin-top:10px;
transform:scale(1.2);
}

/* AGENDAMENTO */

.agendamento{
padding:80px 10%;
text-align:center;
}

.agendamento input,
.agendamento select{
padding:12px;
margin:10px;
font-size:16px;
border:none;
border-radius:5px;
}

.agendamento button{
padding:15px 30px;
background:red;
border:none;
color:white;
font-size:18px;
border-radius:6px;
cursor:pointer;
box-shadow:0 0 10px red;
transition:.3s;
}

.agendamento button:hover{
transform:scale(1.1);
box-shadow:0 0 20px red;
}

/* MAPA */

.mapa{
padding:80px 10%;
text-align:center;
}

iframe{
width:100%;
height:350px;
border:none;
border-radius:10px;
margin-top:20px;
}

/* FOOTER */

footer{
background:#111;
padding:30px;
text-align:center;
border-top:2px solid red;
}

/* SCROLL ANIMATION */

.reveal{
opacity:0;
transform:translateY(60px);
transition:1s;
}

.reveal.active{
opacity:1;
transform:translateY(0);
}

</style>
</head>

<body>

<div id="loader">
<div class="loader-barber">💈 THE BARBER</div>
</div>

<nav>

<h1>💈 THE BARBER</h1>

<div>
<a href="#servicos">Serviços</a>
<a href="#agendamento">Agendar</a>
<a href="#mapa">Localização</a>
</div>

</nav>

<section class="hero">

<h2>Corte Profissional</h2>
<p>Mais de 3 anos no mercado</p>

<button onclick="scrollAgendar()">Agendar Agora</button>

</section>

<section class="servicos reveal" id="servicos">

<h2>Escolha seus serviços</h2>

<div class="cards">

<div class="card">
<h3>Corte de cabelo</h3>
<input type="checkbox" value="Corte de cabelo">
</div>

<div class="card">
<h3>Barba</h3>
<input type="checkbox" value="Barba">
</div>

<div class="card">
<h3>Barba navalha</h3>
<input type="checkbox" value="Barba com navalha">
</div>

<div class="card">
<h3>Coloração</h3>
<input type="checkbox" value="Coloração de cabelo">
</div>

<div class="card">
<h3>Alisamento</h3>
<input type="checkbox" value="Alisamento de cabelo">
</div>

</div>

</section>

<section class="agendamento reveal" id="agendamento">

<h2>Agendar horário</h2>

<input type="text" id="data" placeholder="Escolher data">

<br>

<select id="hora">

<option>08:00</option>
<option>09:00</option>
<option>10:00</option>
<option>11:00</option>
<option>13:00</option>
<option>14:00</option>
<option>15:00</option>
<option>16:00</option>
<option>17:00</option>

</select>

<br><br>

<button onclick="agendar()">Confirmar Agendamento</button>

</section>

<section class="mapa reveal" id="mapa">

<h2>Localização</h2>

<p>Rua Pref. Raul da Cunha Pereira - Peçanha MG</p>

<iframe src="https://maps.google.com/maps?q=Peçanha%20MG&t=&z=15&ie=UTF8&iwloc=&output=embed"></iframe>

</section>

<footer>

<p>THE BARBER • Peçanha MG</p>
<p>(33) 99812-8333</p>

</footer>

<script>

window.onload = function(){
setTimeout(()=>{
document.getElementById("loader").style.display="none"
},1500)
}

flatpickr("#data",{
dateFormat:"d/m/Y",
minDate:"today"
});

function agendar(){

let servicos=[];

document.querySelectorAll("input[type=checkbox]").forEach(cb=>{
if(cb.checked) servicos.push(cb.value);
});

let data=document.getElementById("data").value;
let hora=document.getElementById("hora").value;

let msg="Olá! Quero agendar:%0A";

servicos.forEach(s=>{
msg+="• "+s+"%0A";
});

msg+="Data: "+data+"%0A";
msg+="Horário: "+hora;

window.open("https://wa.me/5533998128333?text="+msg)

}

function scrollAgendar(){
document.getElementById("agendamento").scrollIntoView({behavior:"smooth"})
}

/* SCROLL ANIMATION */

window.addEventListener("scroll",function(){

let reveals=document.querySelectorAll(".reveal")

reveals.forEach(el=>{

let top=el.getBoundingClientRect().top
let height=window.innerHeight

if(top < height-100){
el.classList.add("active")
}

})

})

</script>

</body>
</html>
