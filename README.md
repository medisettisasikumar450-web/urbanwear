<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UrbanWear | Shop Online</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial;background:#f4f4f4;overflow:hidden}

/* HEADER */
header{
  background:#111;color:#fff;padding:15px;
  display:flex;justify-content:space-between;align-items:center
}
header h2{margin:0}
header button{background:#fff;border:none;padding:6px 12px;cursor:pointer}

/* PAGES */
.page{
  position:absolute;top:0;left:0;width:100%;height:100%;
  background:#f4f4f4;overflow:auto;
  transform:translateX(100%);
  transition:.4s ease;
}
.page.active{transform:translateX(0)}
.page.exit{transform:translateX(-100%)}

/* HOME */
.hero{
  background:linear-gradient(120deg,#000,#444);
  color:#fff;padding:60px;text-align:center
}
.categories{
  display:flex;justify-content:center;gap:30px;padding:40px
}
.cat{
  background:#fff;padding:30px;width:200px;text-align:center;
  border-radius:10px;cursor:pointer;
  box-shadow:0 0 10px rgba(0,0,0,.1)
}

/* PRODUCTS */
.products{
  display:flex;flex-wrap:wrap;justify-content:center;padding:20px
}
.card{
  background:#fff;width:220px;margin:15px;padding:15px;
  border-radius:10px;text-align:center;
  box-shadow:0 0 10px rgba(0,0,0,.1)
}
.card img{width:100%;height:200px;object-fit:cover;border-radius:8px}
.buy{background:#e91e63;color:#fff;border:none;padding:8px 12px;cursor:pointer}

/* CHECKOUT */
.checkout{
  padding:40px;text-align:center
}
.checkout input{
  width:250px;padding:10px;margin:8px
}
</style>
</head>

<body>

<header>
  <h2>URBANWEAR</h2>
  <button onclick="goHome()">Home</button>
</header>

<!-- HOME PAGE -->
<div id="home" class="page active">
  <div class="hero">
    <h1>Shop Smart. Dress Better.</h1>
    <p>T-Shirts • Shirts • Pants</p>
  </div>
  <div class="categories">
    <div class="cat" onclick="openCategory('tshirt')">👕 T-Shirts</div>
    <div class="cat" onclick="openCategory('shirt')">👔 Shirts</div>
    <div class="cat" onclick="openCategory('pant')">👖 Pants</div>
  </div>
</div>

<!-- PRODUCTS PAGE -->
<div id="products" class="page">
  <div class="products" id="productList"></div>
</div>

<!-- CHECKOUT PAGE -->
<div id="checkout" class="page">
  <div class="checkout">
    <h2 id="itemName"></h2>
    <h3 id="itemPrice"></h3>
    <input placeholder="Card Number">
    <input placeholder="Expiry">
    <input placeholder="CVV">
    <br>
    <button class="buy" onclick="pay()">Pay Now</button>
  </div>
</div>

<script>
let currentPage=document.getElementById("home");
let products={
  tshirt:[
    {n:"Black T-Shirt",p:499,img:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab"},
    {n:"White T-Shirt",p:549,img:"https://images.unsplash.com/photo-1503341455253-b2e723bb3dbb"},
    {n:"Printed Tee",p:599,img:"https://images.unsplash.com/photo-1581655353564-df123a1eb820"}
  ],
  shirt:[
    {n:"Formal Shirt",p:899,img:"https://images.unsplash.com/photo-1602810318383-e386cc2a3ccf"},
    {n:"Checked Shirt",p:799,img:"https://images.unsplash.com/photo-1596755094514-f87e34085b2c"},
    {n:"Casual Shirt",p:749,img:"https://images.unsplash.com/photo-1521334884684-d80222895322"}
  ],
  pant:[
    {n:"Denim Jeans",p:1199,img:"https://images.unsplash.com/photo-1603252109303-2751441dd157"},
    {n:"Casual Pants",p:999,img:"https://images.unsplash.com/photo-1473966968600-fa801b869a1a"},
    {n:"Chinos",p:1099,img:"https://images.unsplash.com/photo-1582552938357-32b906df40cb"}
  ]
};

function navigate(to){
  currentPage.classList.add("exit");
  setTimeout(()=>{
    currentPage.classList.remove("active","exit");
    to.classList.add("active");
    currentPage=to;
  },400);
}

function goHome(){
  navigate(document.getElementById("home"));
}

function openCategory(type){
  let list=document.getElementById("productList");
  list.innerHTML="";
  products[type].forEach(i=>{
    list.innerHTML+=`
    <div class="card">
      <img src="${i.img}">
      <h3>${i.n}</h3>
      <p>₹${i.p}</p>
      <button class="buy" onclick="checkout('${i.n}',${i.p})">Buy</button>
    </div>`;
  });
  navigate(document.getElementById("products"));
}

function checkout(name,price){
  document.getElementById("itemName").innerText=name;
  document.getElementById("itemPrice").innerText="Amount: ₹"+price;
  navigate(document.getElementById("checkout"));
}

function pay(){
  alert("Order Placed Successfully ✅");
  goHome();
}
</script>

</body>
</html>
