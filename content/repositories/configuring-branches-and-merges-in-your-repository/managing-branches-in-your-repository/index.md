<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>VegX – Fresh Vegetables</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>
body{font-family:Arial;background:#f5f5f5;margin:0}
header{background:#0a8f08;color:#fff;padding:12px;text-align:center;font-size:20px}
.container{padding:10px}
.product{background:#fff;border-radius:8px;padding:10px;margin-bottom:10px;display:flex;gap:10px}
.product img{width:80px;height:80px;object-fit:cover;border-radius:6px}
.product input{width:60px}
.cart{background:#fff;padding:10px;border-radius:8px;margin-top:10px}
button{background:#0a8f08;color:#fff;border:none;padding:12px;width:100%;font-size:16px;border-radius:6px;margin-top:10px}
input,select,textarea{width:100%;padding:8px;margin:6px 0}
.total{font-size:18px;font-weight:bold}
</style>
</head>

<body>

<header>VegX – Fresh Vegetables</header>

<div class="container" id="products"></div>

<div class="container cart">
<h3>Customer Details</h3>

<input id="name" placeholder="Customer Name">
<input id="mobile" placeholder="Mobile Number">
<textarea id="address" placeholder="Delivery Address"></textarea>

<select id="payment">
<option value="">Select Payment Mode</option>
<option value="Cash on Delivery">Cash on Delivery (COD)</option>
<option value="UPI">UPI</option>
</select>

<div class="total">Total: ₹ <span id="total">0</span></div>

<button onclick="placeOrder()">Order on WhatsApp</button>
</div>

<script>
const SHOP_PHONE = "917208487215"; // ✅ तुझा WhatsApp number

const products = [
{name:"Potato",price:40,img:"potato.png"},
{name:"Onion",price:40,img:"onion.png"},
{name:"Tomato",price:30,img:"tomato.png"},
{name:"Lemon",price:20,img:"lemon.jpg"},
{name:"Green Chilli",price:20,img:"green-chilli.png"},
{name:"Carrot",price:50,img:"carrot.png"},
{name:"French Beans",price:60,img:"french-beans.jpg"},
{name:"Drumstick",price:60,img:"drumstick.png"}
];

const box=document.getElementById("products");

products.forEach((p,i)=>{
box.innerHTML+=`
<div class="product">
<img src="${p.img}">
<div>
<b>${p.name}</b><br>₹${p.price}<br>
Qty: <input type="number" min="0" value="0" id="q${i}" onchange="calc()">
</div>
</div>`;
});

function calc(){
let t=0;
products.forEach((p,i)=>{
t+=p.price*Number(document.getElementById("q"+i).value);
});
document.getElementById("total").innerText=t;
}

function placeOrder(){
const name=document.getElementById("name").value;
const mobile=document.getElementById("mobile").value;
const address=document.getElementById("address").value;
const payment=document.getElementById("payment").value;
const total=document.getElementById("total").innerText;

if(!name||!mobile||!address||!payment||total==0){
alert("Please fill all details & select products");
return;
}

let order="🛒 VegX Order%0A%0A";
products.forEach((p,i)=>{
let q=document.getElementById("q"+i).value;
if(q>0) order+=${p.name} x ${q} = ₹${p.price*q}%0A;
});

order+=%0A*Total:* ₹${total}%0A;
order+=Name: ${name}%0A;
order+=Mobile: ${mobile}%0A;
order+=Address: ${address}%0A;
order+=Payment Mode: ${payment}%0A;

window.open(https://wa.me/${SHOP_PHONE}?text=${order},"_blank");
}
</script>

</body>
</html>---

