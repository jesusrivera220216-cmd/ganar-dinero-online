<!DOCTYPE html>
<html lang="es">

<head>

<meta charset="UTF-8">
<title>DineroApp - Ganar Dinero Online</title>

<script src="https://cdn.tailwindcss.com"></script>

</head>

<body class="bg-gray-900 text-white">

<div class="max-w-4xl mx-auto p-6">

<h1 class="text-4xl font-bold mb-6 text-center">
💰 Plataforma Ganar Dinero Online
</h1>

<div id="home">

<div class="bg-gray-800 p-6 rounded-xl mb-6">

<h2 class="text-2xl mb-2">
📘 Ebook recomendado
</h2>

<p class="mb-4">
La Biblia del Dinero Digital 2026
</p>

<button onclick="buyPDF()"
class="bg-green-500 px-6 py-3 rounded">
Comprar ahora
</button>

</div>

<div class="bg-gray-800 p-6 rounded-xl">

<h2 class="text-2xl mb-4">
Crear cuenta
</h2>

<input id="email"
placeholder="Correo"
class="w-full p-3 mb-3 text-black">

<input id="pass"
type="password"
placeholder="Contraseña"
class="w-full p-3 mb-4 text-black">

<button onclick="register()"
class="bg-blue-500 px-6 py-3 rounded mr-2">
Registrarse
</button>

<button onclick="login()"
class="bg-green-500 px-6 py-3 rounded">
Entrar
</button>

</div>

</div>

<div id="dashboard" class="hidden">

<h2 class="text-3xl mt-6">
Panel de usuario
</h2>

<p class="mt-2">
Usuario:
<span id="userEmail"></span>
</p>

<div class="bg-gray-800 p-6 rounded-xl mt-6">

<h3 class="text-xl mb-2">
Ganancias
</h3>

<p class="text-3xl">
$ <span id="balance">0</span>
</p>

</div>

<div class="bg-gray-800 p-6 rounded-xl mt-6">

<h3 class="text-xl mb-4">
Ver anuncio y ganar
</h3>

<button onclick="watchAd()"
class="bg-purple-500 px-6 py-3 rounded">
Ver anuncio
</button>

</div>

<div class="bg-gray-800 p-6 rounded-xl mt-6">

<h3 class="text-xl mb-2">
Encuestas
</h3>

<button onclick="survey()"
class="bg-yellow-500 px-6 py-3 rounded">
Ir a encuesta
</button>

</div>

<div class="bg-gray-800 p-6 rounded-xl mt-6">

<h3 class="text-xl mb-2">
Comprar guía premium
</h3>

<button onclick="buyPDF()"
class="bg-green-500 px-6 py-3 rounded">
Comprar guía
</button>

</div>

<div class="bg-gray-800 p-6 rounded-xl mt-6">

<h3 class="text-xl mb-2">
Tu link de referido
</h3>

<p id="refLink"></p>

</div>

<div class="bg-gray-800 p-6 rounded-xl mt-6 text-center">

Espacio para anuncios (Adsense)

</div>

<button onclick="logout()"
class="bg-red-500 px-6 py-3 rounded mt-6">
Cerrar sesión
</button>

</div>

</div>

<script>

let users = JSON.parse(localStorage.getItem("users") || "[]")

let currentUser = null

function register(){

let email = document.getElementById("email").value
let pass = document.getElementById("pass").value

users.push({
email,
pass,
balance:0
})

localStorage.setItem("users",JSON.stringify(users))

alert("Cuenta creada")

}

function login(){

let email = document.getElementById("email").value
let pass = document.getElementById("pass").value

let user = users.find(
u => u.email === email && u.pass === pass
)

if(user){

currentUser = user

document.getElementById("home").style.display="none"
document.getElementById("dashboard").style.display="block"

document.getElementById("userEmail").innerText = email
document.getElementById("balance").innerText = user.balance

document.getElementById("refLink").innerText =
location.href + "?ref=" + email

}else{

alert("Datos incorrectos")

}

}

function logout(){

location.reload()

}

function watchAd(){

currentUser.balance += 0.02

document.getElementById("balance").innerText =
currentUser.balance.toFixed(2)

save()

}

function survey(){

window.open("https://example.com","_blank")

}

function buyPDF(){

window.open("https://go.hotmart.com/TU_LINK","_blank")

}

function save(){

localStorage.setItem("users",JSON.stringify(users))

}

let params = new URLSearchParams(window.location.search)

let ref = params.get("ref")

if(ref){

localStorage.setItem("referrer",ref)

}

</script>

</body>
</html>
