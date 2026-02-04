<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear – Amazon Style Store</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial, sans-serif;
  background:#eaeded;
}

/* TOP BAR */
.header{
  background:#131921;
  color:white;
  padding:10px;
  display:flex;
  align-items:center;
  gap:15px;
}
.logo{
  font-size:24px;
  font-weight:bold;
  color:#ff9900;
}
.search{
  flex:1;
}
.search input{
  width:100%;
  padding:8px;
  border:none;
}
.cart{
  cursor:pointer;
}

/* NAV */
.nav{
  background:#232f3e;
  color:white;
  padding:10px;
}
.nav button{
  background:none;
  border:none;
  color:white;
  margin-right:15px;
  cursor:pointer;
}

/* PAGES */
.page{display:none;padding:20px}
.active{display:block}

/* PRODUCTS */
.products{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(200px,1fr));
  gap:20px;
}
.card{
  background:white;
  padding:15px;
  border-radius:5px;
}
.card img{
  width:100%;
}
.price{
  color:#B12704;
  font-weight:bold;
}

/* BUTTONS */
button{
  padding:8px;
  width:100%;
  background:#ffd814;
  border:1px solid #fcd200;
  cursor:pointer;
}
button:hover{background:#f7ca00}

/* CART */
.cart-item{
  background:white;
  padding:10px;
  margin-bottom:10px;
}
</style>

<script>
let cart=[];

function show(page){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(page).classList.add('active');
}

function addToCart(name,price){
  cart.push({name,price});
  document.getElementById("cartCount").innerText=cart.length;
  alert("Added to cart");
}

function openCart(){
  let box=document.getElementById("cartItems");
  box.innerHTML="";
  let total=0;
  cart.forEach(i=>{
    total+=i.price;
    box.innerHTML+=`
      <div class="cart-item">
        ${i.name} - ₹${i.price}
      </div>`;
  });
  document.getElementById("total").innerText=total;
  show('cart');
}

function checkout(){
  alert("Payment successful (Demo)");
  cart=[];
  document.getElementById("cartCount").innerText=0;
  show('home');
}
</script>
</head>

<body>

<!-- HEADER -->
<div class="header">
  <div class="logo">UrbanWear</div>
  <div class="search"><input placeholder="Search clothes..."></div>
  <div class="cart" onclick="openCart()">Cart 🛒 (<span id="cartCount">0</span>)</div>
</div>

<!-- NAV -->
<div class="nav">
  <button onclick="show('home')">Home</button>
  <button onclick="show('tshirts')">T-Shirts</button>
  <button onclick="show('shirts')">Shirts</button>
  <button onclick="show('pants')">Pants</button>
</div>

<!-- HOME -->
<div id="home" class="page active">
  <h2>Welcome to UrbanWear</h2>
  <p>Shop like Amazon – Fashion at best prices</p>
</div>

<!-- TSHIRTS -->
<div id="tshirts" class="page">
  <h2>T-Shirts</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=TShirt">
      <h4>Black T-Shirt</h4>
      <p class="price">₹499</p>
      <button onclick="addToCart('Black T-Shirt',499)">Add to Cart</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=TShirt">
      <h4>White T-Shirt</h4>
      <p class="price">₹399</p>
      <button onclick="addToCart('White T-Shirt',399)">Add to Cart</button>
    </div>
  </div>
</div>

<!-- SHIRTS -->
<div id="shirts" class="page">
  <h2>Shirts</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Shirt">
      <h4>Formal Shirt</h4>
      <p class="price">₹999</p>
      <button onclick="addToCart('Formal Shirt',999)">Add to Cart</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Shirt">
      <h4>Casual Shirt</h4>
      <p class="price">₹799</p>
      <button onclick="addToCart('Casual Shirt',799)">Add to Cart</button>
    </div>
  </div>
</div>

<!-- PANTS -->
<div id="pants" class="page">
  <h2>Pants</h2>
  <div class="products">
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Pants">
      <h4>Jeans</h4>
      <p class="price">₹1199</p>
      <button onclick="addToCart('Jeans',1199)">Add to Cart</button>
    </div>
    <div class="card">
      <img src="https://via.placeholder.com/200x250?text=Pants">
      <h4>Chinos</h4>
      <p class="price">₹899</p>
      <button onclick="addToCart('Chinos',899)">Add to Cart</button>
    </div>
  </div>
</div>

<!-- CART -->
<div id="cart" class="page">
  <h2>Your Cart</h2>
  <div id="cartItems"></div>
  <h3>Total: ₹<span id="total">0</span></h3>
  <button onclick="checkout()">Proceed to Checkout</button>
</div>

</body>
</html>
