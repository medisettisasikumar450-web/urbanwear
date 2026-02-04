<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear | Online Clothing Store</title>

<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  background:#f5f5f5;
}
header{
  background:#111;
  color:white;
  padding:15px;
  text-align:center;
  font-size:28px;
}
nav{
  background:#ff9800;
  display:flex;
  justify-content:center;
  gap:20px;
  padding:10px;
}
nav button{
  background:white;
  border:none;
  padding:10px 20px;
  font-size:16px;
  cursor:pointer;
  border-radius:5px;
}
nav button:hover{background:#222;color:white;}

.section{display:none;padding:30px;text-align:center;}
.active{display:block;}

.products{
  display:flex;
  justify-content:center;
  flex-wrap:wrap;
  gap:20px;
}
.card{
  background:white;
  width:220px;
  padding:15px;
  border-radius:10px;
  box-shadow:0 0 10px rgba(0,0,0,0.1);
}
.card img{
  width:100%;
  border-radius:8px;
}
.card h3{margin:10px 0;}
.price{color:green;font-weight:bold;}

button.buy{
  background:#ff9800;
  border:none;
  padding:8px 15px;
  cursor:pointer;
  border-radius:5px;
}
button.buy:hover{background:#111;color:white;}

footer{
  background:#111;
  color:white;
  text-align:center;
  padding:10px;
}
</style>

<script>
function show(page){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.getElementById(page).classList.add('active');
}
function buy(item){
  alert("Proceeding to payment for " + item);
}
</script>
</head>

<body>

<header>URBANWEAR</header>

<nav>
  <button onclick="show('home')">Home</button>
  <button onclick="show('tshirts')">T-Shirts</button>
  <button onclick="show('shirts')">Shirts</button>
  <button onclick="show('pants')">Pants</button>
</nav>

<!-- HOME -->
<div id="home" class="section active">
  <h1>Welcome to UrbanWear</h1>
  <p>Trendy fashion • Affordable prices • Easy shopping</p>
</div>

<!-- TSHIRTS -->
<div id="tshirts" class="section">
  <h2>T-Shirts</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Tshirt+1">
      <h3>Black Tee</h3>
      <p class="price">₹499</p>
      <button class="buy" onclick="buy('Black Tee')">Buy</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Tshirt+2">
      <h3>White Tee</h3>
      <p class="price">₹399</p>
      <button class="buy" onclick="buy('White Tee')">Buy</button>
    </div>
  </div>
</div>

<!-- SHIRTS -->
<div id="shirts" class="section">
  <h2>Shirts</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Shirt+1">
      <h3>Formal Shirt</h3>
      <p class="price">₹999</p>
      <button class="buy" onclick="buy('Formal Shirt')">Buy</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Shirt+2">
      <h3>Casual Shirt</h3>
      <p class="price">₹799</p>
      <button class="buy" onclick="buy('Casual Shirt')">Buy</button>
    </div>
  </div>
</div>

<!-- PANTS -->
<div id="pants" class="section">
  <h2>Pants</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Pants+1">
      <h3>Jeans</h3>
      <p class="price">₹1199</p>
      <button class="buy" onclick="buy('Jeans')">Buy</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Pants+2">
      <h3>Chinos</h3>
      <p class="price">₹899</p>
      <button class="buy" onclick="buy('Chinos')">Buy</button>
    </div>
  </div>
</div>

<footer>© 2026 UrbanWear | Online Clothing Store</footer>

</body>
</html>
