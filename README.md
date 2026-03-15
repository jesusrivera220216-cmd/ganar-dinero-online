<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>DineroApp</title>
<script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="bg-gray-900 text-white">

<div class="max-w-xl mx-auto p-6">

<h1 class="text-4xl font-bold text-center mb-6">
💰 DineroApp
</h1>

<div class="bg-gray-800 p-6 rounded">

<input id="email" placeholder="Correo"
class="w-full p-3 mb-3 text-black">

<input id="pass" type="password"
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

<script>

let users = JSON.parse(localStorage.getItem("users") || "[]")

function register(){

let email=document.getElementById("email").value
let pass=document.getElementById("pass").value

if(!email||!pass){
alert("Completa los campos")
return
}

if(users.find(u=>u.email===email)){
alert("Usuario ya existe")
return
}

users.push({
email,
pass,
balance:0
})

localStorage.setItem("users",JSON.stringify(users))

alert("Cuenta creada")

}

function login(){

let email=document.getElementById("email").value
let pass=document.getElementById("pass").value

let user=users.find(u=>u.email===email&&u.pass===pass)

if(!user){
alert("Datos incorrectos")
return
}

localStorage.setItem("currentUser",email)

location.href="dashboard.html"

}

</script>

</body>
</html>
