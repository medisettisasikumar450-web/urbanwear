<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear Store</title>

<style>
body{margin:0;font-family:Arial;background:#f2f2f2}
header{background:#131921;color:#fff;padding:15px;text-align:center;font-size:22px}
nav{display:flex;background:#ff9900;position:sticky;top:0}
nav button{flex:1;border:none;padding:10px;font-size:13px}
nav button:hover{background:#111;color:#fff}

.page{display:none;padding:12px;animation:fade .3s}
.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(10px)}to{opacity:1}}

.products{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:10px;
}

.card{
background:#fff;
padding:10px;
border-radius:10px;
box-shadow:0 2px 8px rgba(0,0,0,.1);
}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.price{color:green;font-weight:bold}
.btn{width:100%;padding:7px;border:none;border-radius:5px;background:#ff9900;margin-top:5px}
.btn:hover{background:#111;color:#fff}

.cart-item{background:#fff;padding:8px;margin:5px 0;border-radius:6px}
</style>

<script>
let products=[];
let cart=[],orders=[];
let viewItem=null;

/* 🔥 AUTO CREATE 120 PRODUCTS */
function createProducts(){
 let id=1;

 for(let i=1;i<=40;i++){
  products.push({
   name:`T-Shirt Model ${i}`,
   price:399+(i*5),
   cat:"tshirts",
   img:`images/tshirt${(i%5)+1}.jpg`
  });
 }

 for(let i=1;i<=40;i++){
  products.push({
   name:`Shirt Model ${i}`,
   price:799+(i*6),
   cat:"shirts",
   img:`images/shirt${(i%5)+1}.jpg`
  });
 }

 for(let i=1;i<=40;i++){
  products.push({
   name:`Pant Model ${i}`,
   price:999+(i*7),
   cat:"pants",
   img:`images/pant${(i%5)+1}.jpg`
  });
 }
}
createProducts();

function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
 if(p==="shop")render();
 if(p==="cart")renderCart();
 if(p==="orders")renderOrders();
}

function render(){
 let cat=document.getElementById("cat").value;
 let q=document.getElementById("search").value.toLowerCase();
 let box=document.getElementById("products");
 box.innerHTML="";
 products.filter(p=>
  (cat==="all"||p.cat===cat)&&
  p.name.toLowerCase().includes(q)
 ).forEach(p=>{
  box.innerHTML+=`
  <div class="card">
   <img src="${p.img}">
   <h4>${p.name}</h4>
   <p class="price">₹${p.price}</p>
   <button class="btn" onclick="view('${p.name}')">View</button>
   <button class="btn" onclick="cart.push(p)">Add to Cart</button>
  </div>`;
 });
}

function view(name){
 viewItem=products.find(p=>p.name===name);
 show("view");
 document.getElementById("viewBox").innerHTML=`
 <img src="${viewItem.img}" style="width:100%;border-radius:10px">
 <h3>${viewItem.name}</h3>
 <p class="price">₹${viewItem.price}</p>
 <button class="btn" onclick="cart.push(viewItem)">Add to Cart</button>`;
}

function renderCart(){
 let t=0,box=document.getElementById("cartItems");
 box.innerHTML="";
 cart.forEach(p=>{
  t+=p.price;
  box.innerHTML+=`<div class="cart-item">${p.name} – ₹${p.price}</div>`;
 });
 document.getElementById("total").innerText=t;
}

function pay(){
 if(!cart.length)return alert("Cart empty");
 orders.push(...cart);
 cart=[];
 alert("Payment Successful (Demo)");
 renderCart();
}

function renderOrders(){
 let box=document.getElementById("ordersList");
 box.innerHTML="";
 orders.forEach(p=>{
  box.innerHTML+=`<div class="cart-item">${p.name} – ₹${p.price}</div>`;
 });
}
</script>
</head>

<body>

<header>URBANWEAR</header>

<nav>
<button onclick="show('home')">Home</button>
<button onclick="show('shop')">Shop</button>
<button onclick="show('cart')">Cart</button>
<button onclick="show('orders')">Orders</button>
</nav>

<div id="home" class="page active">
<h2>Welcome to UrbanWear</h2>
<p>100+ products • Offline • Amazon-style demo</p>
</div>

<div id="shop" class="page">
<input id="search" placeholder="Search..." onkeyup="render()">
<select id="cat" onchange="render()">
<option value="all">All</option>
<option value="tshirts">T-Shirts</option>
<option value="shirts">Shirts</option>
<option value="pants">Pants</option>
</select>
<div id="products" class="products"></div>
</div>

<div id="view" class="page">
<div id="viewBox"></div>
</div>

<div id="cart" class="page">
<h3>Cart</h3>
<div id="cartItems"></div>
<h4>Total ₹<span id="total">0</span></h4>
<button class="btn" onclick="pay()">Pay</button>
</div>

<div id="orders" class="page">
<h3>Order History</h3>
<div id="ordersList"></div>
</div>

</body>
</html>
