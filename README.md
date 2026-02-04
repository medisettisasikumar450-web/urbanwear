<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear – Shopping App</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial;background:#f1f3f6}
header{background:#131921;color:#fff;padding:14px;text-align:center;font-size:22px}
nav{display:flex;position:sticky;top:0;background:#ff9900}
nav button{flex:1;border:none;padding:10px;font-size:13px;cursor:pointer}
nav button:hover{background:#111;color:#fff}

.page{display:none;padding:12px;animation:slide .35s}
.active{display:block}
@keyframes slide{from{opacity:0;transform:translateX(20px)}to{opacity:1}}

input,select{width:100%;padding:7px;margin:5px 0}

.products{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
 gap:10px;
}
.card{
 background:#fff;
 padding:10px;
 border-radius:10px;
 box-shadow:0 0 8px rgba(0,0,0,.1);
}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px}
.price{color:green;font-weight:bold}
.btn{width:100%;padding:7px;border:none;border-radius:5px;background:#ff9900;margin-top:4px}
.btn:hover{background:#111;color:#fff}

.cart-item{background:#fff;padding:7px;margin:5px 0;border-radius:6px}

footer{background:#131921;color:#fff;text-align:center;padding:8px;margin-top:15px}
</style>

<script>
let products=[
 {n:"Black Round T-Shirt",p:499,c:"tshirts",i:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab"},
 {n:"White Printed T-Shirt",p:399,c:"tshirts",i:"https://images.unsplash.com/photo-1503342217505-b0a15ec3261c"},
 {n:"Oversized Blue T-Shirt",p:599,c:"tshirts",i:"https://images.unsplash.com/photo-1562157873-818bc0726f68"},
 {n:"White Formal Shirt",p:999,c:"shirts",i:"https://images.unsplash.com/photo-1598033129183-c4f50c736f10"},
 {n:"Checked Casual Shirt",p:799,c:"shirts",i:"https://images.unsplash.com/photo-1520975916090-3105956dac38"},
 {n:"Denim Shirt",p:899,c:"shirts",i:"https://images.unsplash.com/photo-1620799139507-2a76f79a2f4d"},
 {n:"Blue Jeans",p:1199,c:"pants",i:"https://images.unsplash.com/photo-1541099649105-f69ad21f3246"},
 {n:"Black Chinos",p:899,c:"pants",i:"https://images.unsplash.com/photo-1593032465175-481ac7f401a0"},
 {n:"Green Cargo Pants",p:1099,c:"pants",i:"https://images.unsplash.com/photo-1603252109303-2751441dd157"}
];

let cart=[],wishlist=[],orders=[],user=null,viewItem=null;

function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
 if(p==="shop")render();
 if(p==="cart")renderCart();
 if(p==="orders")renderOrders();
 if(p==="admin")document.getElementById("orderCount").innerText=orders.length;
}

function render(){
 let q=document.getElementById("search").value.toLowerCase();
 let sort=document.getElementById("sort").value;
 let cat=document.getElementById("cat").value;
 let list=[...products].filter(x=>x.n.toLowerCase().includes(q)&&(cat==="all"||x.c===cat));
 if(sort==="l")list.sort((a,b)=>a.p-b.p);
 if(sort==="h")list.sort((a,b)=>b.p-a.p);
 let box=document.getElementById("products");
 box.innerHTML="";
 list.forEach(x=>box.innerHTML+=`
 <div class="card">
 <img src="${x.i}">
 <h4>${x.n}</h4>
 <p class="price">₹${x.p}</p>
 <button class="btn" onclick="view('${x.n}')">View</button>
 <button class="btn" onclick="cart.push(x)">Add Cart</button>
 <button class="btn" onclick="wishlist.push(x)">❤️ Wishlist</button>
 </div>`);
}

function view(n){
 viewItem=products.find(x=>x.n===n);
 show("view");
 document.getElementById("viewBox").innerHTML=`
 <img src="${viewItem.i}" style="width:100%;border-radius:10px">
 <h3>${viewItem.n}</h3>
 <p class="price">₹${viewItem.p}</p>
 <button class="btn" onclick="cart.push(viewItem)">Add to Cart</button>`;
}

function renderCart(){
 let t=0,box=document.getElementById("cartItems");
 box.innerHTML="";
 cart.forEach(x=>{t+=x.p;box.innerHTML+=`<div class="cart-item">${x.n} – ₹${x.p}</div>`});
 document.getElementById("total").innerText=t;
}

function pay(){
 if(!cart.length)return alert("Cart empty");
 orders.push(...cart);
 cart=[];
 alert("Payment Successful (Demo)");
}

function renderOrders(){
 let box=document.getElementById("ordersList");
 box.innerHTML="";
 orders.forEach(x=>box.innerHTML+=`<div class="cart-item">${x.n} – ₹${x.p}</div>`);
}

function login(){
 user=document.getElementById("u").value;
 alert("Logged in as "+user);
 show("home");
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
<button onclick="show('admin')">Admin</button>
<button onclick="show('login')">Login</button>
</nav>

<div id="home" class="page active">
<h2>Welcome to UrbanWear</h2>
<p>Amazon-style demo shopping app</p>
</div>

<div id="shop" class="page">
<input id="search" placeholder="Search..." onkeyup="render()">
<select id="cat" onchange="render()">
<option value="all">All</option>
<option value="tshirts">T-Shirts</option>
<option value="shirts">Shirts</option>
<option value="pants">Pants</option>
</select>
<select id="sort" onchange="render()">
<option value="">Sort</option>
<option value="l">Low → High</option>
<option value="h">High → Low</option>
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

<div id="admin" class="page">
<h3>Admin Panel</h3>
<p>Total Orders: <b id="orderCount">0</b></p>
</div>

<div id="login" class="page">
<h3>Login</h3>
<input id="u" placeholder="Username">
<button class="btn" onclick="login()">Login</button>
</div>

<footer>© 2026 UrbanWear • Demo App</footer>

</body>
</html>
