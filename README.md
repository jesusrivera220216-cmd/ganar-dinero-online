<!DOCTYPE html>
<html lang="es">

<head>
<meta charset="UTF-8">
<title>DineroApp PRO</title>

<script src="https://cdn.tailwindcss.com"></script>

</head>

<body class="bg-gray-900 text-white">

<div class="max-w-4xl mx-auto p-6">

<h1 class="text-4xl font-bold text-center mb-6">
💰 DineroApp PRO
</h1>

<!-- HOME -->

<div id="home">

<div class="bg-gray-800 p-6 rounded mb-6">

<h2 class="text-2xl mb-4">
Crear cuenta
</h2>

<input id="email"
placeholder="Correo"
class="w-full p-3 text-black mb-3">

<input id="pass"
type="password"
placeholder="Contraseña"
class="w-full p-3 text-black mb-3">

<input id="ref"
placeholder="Código de referido (opcional)"
class="w-full p-3 text-black mb-4">

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

<!-- DASHBOARD -->

<div id="dashboard" class="hidden">

<h2 class="text-2xl">
Panel de usuario
</h2>

<p class="mt-2">
Usuario:
<span id="userEmail"></span>
</p>

<!-- BALANCE -->

<div class="bg-gray-800 p-6 rounded mt-6">

<h3 class="text-xl mb-2">
Balance
</h3>

<p class="text-3xl">
$ <span id="balance">0</span>
</p>

</div>

<!-- ANUNCIOS -->

<div class="bg-gray-800 p-6 rounded mt-6">

<h3 class="text-xl mb-3">
Ver anuncios
</h3>

<button onclick="watchAd()"
class="bg-purple-500 px-6 py-3 rounded">
Ver anuncio
</button>

</div>

<!-- ENCUESTAS -->

<div class="bg-gray-800 p-6 rounded mt-6">

<h3 class="text-xl mb-3">
Encuestas pagadas
</h3>

<button onclick="survey()"
class="bg-yellow-500 px-6 py-3 rounded">
Ir a encuestas
</button>

</div>

<!-- REFERIDOS -->

<div class="bg-gray-800 p-6 rounded mt-6">

<h3 class="text-xl mb-2">
Tu link de referido
</h3>

<p id="refLink"></p>

</div>

<!-- RETIRO -->

<div class="bg-gray-800 p-6 rounded mt-6">

<h3 class="text-xl mb-3">
Solicitar retiro
</h3>

<input id="withdrawAmount"
placeholder="Monto"
class="p-3 text-black mb-3">

<button onclick="withdraw()"
class="bg-green-500 px-6 py-3 rounded">
Solicitar retiro
</button>

</div>

<button onclick="logout()"
class="bg-red-500 px-6 py-3 rounded mt-6">
Cerrar sesión
</button>

</div>

</div>

<script>

let users = JSON.parse(localStorage.getItem("users") || "[]")

let withdrawals = JSON.parse(localStorage.getItem("withdrawals") || "[]")

let currentUser = null

function register(){

let email = document.getElementById("email").value
let pass = document.getElementById("pass").value
let ref = document.getElementById("ref").value

if(!email || !pass){

alert("Completa los campos")

return

}

if(users.find(u => u.email === email)){

alert("Este usuario ya existe")

return

}

users.push({

email,
pass,
balance:0,
ref

})

save()

alert("Cuenta creada")

}

function login(){

let email = document.getElementById("email").value
let pass = document.getElementById("pass").value

let user = users.find(
u => u.email === email && u.pass === pass
)

if(!user){

alert("Datos incorrectos")

return

}

currentUser = user

document.getElementById("home").style.display="none"
document.getElementById("dashboard").style.display="block"

document.getElementById("userEmail").innerText = email
document.getElementById("balance").innerText = user.balance

document.getElementById("refLink").innerText =
location.href + "?ref=" + email

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

function withdraw(){

let amount =
document.getElementById("withdrawAmount").value

if(amount > currentUser.balance){

alert("Saldo insuficiente")

return

}

withdrawals.push({

user:currentUser.email,
amount:amount,
status:"pendiente"

})

currentUser.balance -= amount

save()

alert("Solicitud enviada")

}

function save(){

localStorage.setItem("users",JSON.stringify(users))
localStorage.setItem("withdrawals",JSON.stringify(withdrawals))

}

</script>

</body>
</html>
