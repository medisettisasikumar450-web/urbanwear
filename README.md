<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear – Clothing Store</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial;background:#f1f3f6}
header{background:#131921;color:#fff;padding:15px;text-align:center;font-size:24px}
nav{display:flex;overflow:auto;background:#ff9900}
nav button{flex:1;border:none;padding:10px;font-size:14px;cursor:pointer}
nav button:hover{background:#111;color:#fff}

.page{display:none;padding:15px;animation:fade .35s}
.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(10px)}to{opacity:1}}

.products{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
  gap:12px;
}
.card{
  background:#fff;
  border-radius:10px;
  padding:10px;
  box-shadow:0 0 10px rgba(0,0,0,.1);
}
.card img{
  width:100%;
  height:200px;
  object-fit:cover;
  border-radius:8px;
}
.price{color:green;font-weight:bold}
.btn{
  width:100%;
  border:none;
  padding:8px;
  margin-top:5px;
  border-radius:5px;
  background:#ff9900;
  cursor:pointer;
}
.btn:hover{background:#111;color:#fff}

.cart-item{background:#fff;padding:8px;margin:6px 0;border-radius:6px}

footer{background:#131921;color:#fff;text-align:center;padding:10px;margin-top:20px}
</style>

<script>
let cart=[],orders=[];
function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
}
function add(name,price){
 cart.push({name,price});
 alert(name+" added to cart");
 renderCart();
}
function renderCart(){
 let box=document.getElementById("cartItems"),t=0;
 box.innerHTML="";
 cart.forEach(i=>{t+=i.price;box.innerHTML+=`<div class="cart-item">${i.name} – ₹${i.price}</div>`});
 document.getElementById("total").innerText=t;
}
function pay(){
 if(!cart.length){alert("Cart empty");return}
 orders.push(...cart);
 cart=[];
 renderCart();
 alert("Payment Successful (Demo)");
}
function loadOrders(){
 let box=document.getElementById("orders");
 box.innerHTML="";
 orders.forEach(o=>box.innerHTML+=`<div class="cart-item">${o.name} – ₹${o.price}</div>`);
 document.getElementById("orderCount").innerText=orders.length;
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
<button onclick="show('cart')">Cart</button>
<button onclick="show('ordersPage');loadOrders()">Orders</button>
<button onclick="show('admin');loadOrders()">Admin</button>
</nav>

<!-- HOME -->
<div id="home" class="page active">
<h2>Welcome to UrbanWear</h2>
<p>Fashion like Amazon • Simple • Fast • Offline-ready</p>
</div>

<!-- TSHIRTS -->
<div id="tshirts" class="page">
<h3>T-Shirts</h3>
<div class="products">
<div class="card"><img src="https://images.unsplash.com/photo-1521572163474-6864f9cf17ab"><h4>Black Round T-Shirt</h4><p class="price">₹499</p><button class="btn" onclick="add('Black Round T-Shirt',499)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1503342217505-b0a15ec3261c"><h4>White Printed T-Shirt</h4><p class="price">₹399</p><button class="btn" onclick="add('White Printed T-Shirt',399)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1562157873-818bc0726f68"><h4>Oversized Street T-Shirt</h4><p class="price">₹599</p><button class="btn" onclick="add('Oversized Street T-Shirt',599)">Add to Cart</button></div>
</div>
</div>

<!-- SHIRTS -->
<div id="shirts" class="page">
<h3>Shirts</h3>
<div class="products">
<div class="card"><img src="https://images.unsplash.com/photo-1598033129183-c4f50c736f10"><h4>White Formal Shirt</h4><p class="price">₹999</p><button class="btn" onclick="add('White Formal Shirt',999)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1520975916090-3105956dac38"><h4>Checked Casual Shirt</h4><p class="price">₹799</p><button class="btn" onclick="add('Checked Casual Shirt',799)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1620799139507-2a76f79a2f4d"><h4>Denim Shirt</h4><p class="price">₹899</p><button class="btn" onclick="add('Denim Shirt',899)">Add to Cart</button></div>
</div>
</div>

<!-- PANTS -->
<div id="pants" class="page">
<h3>Pants</h3>
<div class="products">
<div class="card"><img src="https://images.unsplash.com/photo-1541099649105-f69ad21f3246"><h4>Blue Jeans</h4><p class="price">₹1199</p><button class="btn" onclick="add('Blue Jeans',1199)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1593032465175-481ac7f401a0"><h4>Black Chinos</h4><p class="price">₹899</p><button class="btn" onclick="add('Black Chinos',899)">Add to Cart</button></div>
<div class="card"><img src="https://images.unsplash.com/photo-1603252109303-2751441dd157"><h4>Green Cargo Pants</h4><p class="price">₹1099</p><button class="btn" onclick="add('Green Cargo Pants',1099)">Add to Cart</button></div>
</div>
</div>

<!-- CART -->
<div id="cart" class="page">
<h3>Your Cart</h3>
<div id="cartItems"></div>
<h4>Total: ₹<span id="total">0</span></h4>
<button class="btn" onclick="pay()">Pay (Demo)</button>
</div>

<!-- ORDERS -->
<div id="ordersPage" class="page">
<h3>Order History</h3>
<div id="orders"></div>
</div>

<!-- ADMIN -->
<div id="admin" class="page">
<h3>Admin Panel (Demo)</h3>
<p>Total Orders: <b id="orderCount">0</b></p>
<p>Revenue = Demo Only</p>
</div>

<footer>© 2026 UrbanWear • Demo E-Commerce App</footer>

</body>
</html>
