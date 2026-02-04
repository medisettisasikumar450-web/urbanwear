<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>UrbanWear Mart</title>

<style>
body{margin:0;font-family:Arial;background:#f2f2f2}
header{background:#131921;color:white;padding:15px;text-align:center;font-size:24px}
nav{display:flex;justify-content:space-around;background:#ff9900;padding:10px}
nav button{border:none;padding:10px;border-radius:6px;cursor:pointer}
.page{display:none;padding:20px;animation:fade .4s}
.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(10px)}to{opacity:1}}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:15px}
.card{background:white;padding:10px;border-radius:10px;box-shadow:0 2px 5px rgba(0,0,0,.2)}
.card img{width:100%;height:140px;object-fit:cover}
.price{color:green;font-weight:bold}
button.buy{background:#ff9900;border:none;width:100%;padding:8px;margin-top:5px}
footer{background:#131921;color:white;text-align:center;padding:10px}
</style>

<script>
let cart=[],orders=[];
function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
}
function add(n,p){
 cart.push({n,p});
 alert(n+" added to cart");
}
function checkout(){
 if(cart.length==0){alert("Cart empty");return;}
 orders.push(...cart); cart=[];
 alert("Payment Successful (Demo)");
}
</script>
</head>

<body>

<header>🛒 UrbanWear Mart</header>

<nav>
<button onclick="show('home')">Home</button>
<button onclick="show('grocery')">Groceries</button>
<button onclick="show('food')">Food</button>
<button onclick="show('cart')">Cart</button>
</nav>

<div id="home" class="page active">
<h2>Welcome</h2>
<p>All Groceries & Food Items at Best Prices</p>
</div>

<!-- GROCERY (20 ITEMS) -->
<div id="grocery" class="page">
<h2>Groceries</h2>
<div class="products">
<script>
let grocery=[
["Rice 1kg",60],["Wheat Flour",55],["Sugar",45],["Salt",20],["Cooking Oil",160],
["Toor Dal",120],["Chana Dal",95],["Moong Dal",110],["Tea Powder",140],["Coffee",180],
["Milk Packet",30],["Bread",40],["Eggs (6)",55],["Butter",95],["Cheese",120],
["Tomato",25],["Onion",30],["Potato",35],["Apple",120],["Banana",50]
];
for(let g of grocery){
document.write(`<div class="card">
<img src="https://source.unsplash.com/300x200/?grocery,food">
<h4>${g[0]}</h4>
<p class="price">₹${g[1]}</p>
<button class="buy" onclick="add('${g[0]}',${g[1]})">Add to Cart</button>
</div>`);
}
</script>
</div>
</div>

<!-- FOOD (20 ITEMS) -->
<div id="food" class="page">
<h2>Food Items</h2>
<div class="products">
<script>
let food=[
["Veg Burger",99],["Chicken Burger",129],["Veg Pizza",199],["Chicken Pizza",249],
["Paneer Biryani",220],["Chicken Biryani",260],["Veg Noodles",140],["Chicken Noodles",170],
["Veg Fried Rice",150],["Chicken Fried Rice",180],["Masala Dosa",80],["Idli",60],
["Vada",50],["Samosa",25],["French Fries",90],["Ice Cream",70],
["Chocolate Cake",120],["Cold Coffee",90],["Fresh Juice",80],["Milk Shake",100]
];
for(let f of food){
document.write(`<div class="card">
<img src="https://source.unsplash.com/300x200/?food,meal">
<h4>${f[0]}</h4>
<p class="price">₹${f[1]}</p>
<button class="buy" onclick="add('${f[0]}',${f[1]})">Add to Cart</button>
</div>`);
}
</script>
</div>
</div>

<!-- CART -->
<div id="cart" class="page">
<h2>Cart</h2>
<button class="buy" onclick="checkout()">Pay Now</button>
</div>

<footer>© 2026 UrbanWear Mart</footer>

</body>
</html>
