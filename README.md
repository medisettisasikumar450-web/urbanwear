<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear Mart</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{margin:0;font-family:Arial;background:#f5f5f5}
header{background:#0f1111;color:#fff;padding:15px;text-align:center;font-size:24px}
nav{display:flex;justify-content:space-around;background:#ff9900;padding:10px}
nav button{border:none;padding:10px 14px;border-radius:5px;font-size:14px;cursor:pointer}
.page{display:none;animation:fade .3s}
.active{display:block}
@keyframes fade{from{opacity:0}to{opacity:1}}

.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:15px;padding:15px}
.card{background:#fff;padding:10px;border-radius:8px;box-shadow:0 0 8px rgba(0,0,0,.1)}
.card img{width:100%;height:140px;object-fit:cover;border-radius:6px}
.price{color:green;font-weight:bold}
button.buy{background:#ff9900;border:none;padding:6px;width:100%;border-radius:5px;margin-top:5px}

footer{background:#0f1111;color:white;text-align:center;padding:10px}
</style>

<script>
let cart=[], buy=[],orders=[];

function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
}

function add(name,price){
 cart.push({name,price});
 alert(name+" added to cart");
}

function viewCart(){
 let t="";
 let total=0;
 cart.forEach(i=>{t+=i.name+" - ₹"+i.price+"<br>";total+=i.price});
 document.getElementById("cartItems").innerHTML=t+"<hr>Total ₹"+total;
 show('cart');
}

function pay(){
 orders.push(...cart);
 cart=[];
 alert("Payment Successful ✅");
 show('orders');
}

function loadOrders(){
 let t="";
 orders.forEach(o=>t+=o.name+" - ₹"+o.price+"<br>");
 document.getElementById("orderList").innerHTML=t || "No orders yet";
}
</script>
</head>

<body>

<header>🛒 UrbanWear Mart</header>

<nav>
<button onclick="show('home')">Home</button>
<button onclick="show('food')">Food</button>
<button onclick="show('grocery')">Grocery</button>
<button onclick="viewCart()">Cart</button>
<button onclick="loadOrders();show('orders')">Orders</button>
<button onclick="show('admin')">Admin</button>
</nav>

<!-- HOME -->
<div id="home" class="page active">
<h2 style="text-align:center">Welcome to UrbanWear Mart</h2>
<p style="text-align:center">Food • Groceries • Fast Delivery</p>
</div>

<!-- FOOD -->
<div id="food" class="page">
<div class="products">
<script>
["Pizza","Burger","Biryani","Pasta","Sandwich","Noodles","Fried Rice","Cake","Ice Cream","Fries",
"Chicken Curry","Paneer","Dosa","Idli","Samosa","Pav Bhaji","Tacos","Hotdog","Soup","Salad"]
.forEach((i,n)=>{
document.write(`<div class="card">
<img src="https://source.unsplash.com/300x200/?${i},food">
<h4>${i}</h4>
<p class="price">₹${100+n*10}</p>
<button class="buy" onclick="add('${i}',${100+n*10})">Add to Cart</button>
</div>`);
});
</script>
</div>
</div>

<!-- GROCERY -->
<div id="grocery" class="page">
<div class="products">
<script>
["Rice","Wheat Flour","Sugar","Salt","Milk","Eggs","Bread","Oil","Butter","Cheese",
"Tea","Coffee","Biscuits","Apples","Bananas","Potatoes","Onions","Tomatoes","Dal","Spices"]
.forEach((i,n)=>{
document.write(`<div class="card">
<img src="https://source.unsplash.com/300x200/?${i},grocery">
<h4>${i}</h4>
<p class="price">₹${50+n*8}</p>
<button class="buy" onclick="add('${i}',${50+n*8})">Add to Cart</button>
</div>`);
});
</script>
</div>
</div>

<!-- CART -->
<div id="cart" class="page">
<h3 style="padding:15px">Cart</h3>
<div id="cartItems" style="padding:15px"></div>
<button class="buy" onclick="pay()" style="margin:15px">Pay Now</button>
</div>

<!-- ORDERS -->
<div id="orders" class="page">
<h3 style="padding:15px">Order History</h3>
<div id="orderList" style="padding:15px"></div>
</div>

<!-- ADMIN -->
<div id="admin" class="page">
<h3 style="padding:15px">Admin Panel (Demo)</h3>
<p style="padding:15px">Total Orders: <b><script>document.write(orders.length)</script></b></p>
</div>

<footer>© 2026 UrbanWear Mart</footer>

</body>
</html>
