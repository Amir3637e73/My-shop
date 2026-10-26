<!DOCTYPE html><html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>PARSA SHOP | فروشگاه خدمات مجازی</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#0a0a12;color:#fff;font-family:Tahoma,Arial,sans-serif}
header{padding:30px 15px;text-align:center;background:linear-gradient(135deg,#52118b,#151020)}
header h1{font-size:30px;color:#e2b8ff;margin:0}
header p{color:#ddd}
nav{display:flex;justify-content:center;gap:18px;flex-wrap:wrap;background:#171522;padding:15px}
nav a{color:white;text-decoration:none;font-size:13px}
.container{max-width:1100px;margin:auto;padding:18px}
.search{width:100%;padding:14px;border:1px solid #40334f;border-radius:10px;background:#171522;color:white;margin:12px 0}
.categories{display:flex;gap:8px;overflow-x:auto;padding:8px 0 15px}
.categories button{white-space:nowrap;background:#21182d}
button{border:0;border-radius:9px;padding:11px;background:#913fe0;color:white;cursor:pointer}
button:hover{background:#ad68f0}
h2{color:#d7a4ff;font-size:20px}
.products{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:14px}
.card{background:#171522;border:1px solid #352944;border-radius:15px;padding:17px;text-align:center}
.icon{font-size:36px}
.card h3{font-size:15px}
.card p{font-size:12px;color:#c6c0d0;line-height:1.8}
.price{color:#e0b0ff!important;font-size:15px!important;font-weight:bold}
.card button{width:100%}
.cart{background:#171522;border:1px solid #352944;border-radius:15px;padding:18px;margin-top:28px}
.cart-item{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:12px 0;border-bottom:1px solid #332840;font-size:13px}
.remove{background:#702a40;padding:7px}
.total{font-size:18px;color:#e1b5ff;margin:20px 0}
.telegram{display:block;text-align:center;text-decoration:none;background:#168bd0;color:white;padding:14px;border-radius:10px;margin-top:12px}
footer{text-align:center;padding:25px;color:#999;font-size:12px}
</style>
</head>
<body><header>
<h1>💜 PARSA SHOP</h1>
<p>فروشگاه خدمات مجازی، گیمینگ و محصولات دیجیتال</p>
</header><nav>
<a href="#shop">🏪 فروشگاه</a>
<a href="#cart">🛒 سبد خرید (<span id="count">۰</span>)</a>
<a href="#support">💬 پشتیبانی</a>
</nav><main class="container" id="shop">
<h2>✨ محصولات فروشگاه</h2>
<input id="search" class="search" placeholder="🔎 نام محصول را جست‌وجو کن..."><div class="categories">
<button onclick="setCat('همه',this)" class="active">همه محصولات</button>
<button onclick="setCat('تلگرام',this)">✈️ خدمات تلگرام</button>
<button onclick="setCat('شماره مجازی',this)">📱 شماره مجازی</button>
<button onclick="setCat('کارت پرداخت',this)">💳 کارت پرداخت</button>
<button onclick="setCat('PS5',this)">🎮 بازی PS5</button>
<button onclick="setCat('PC',this)">🖥️ بازی PC</button>
<button onclick="setCat('اینترنت',this)">🌐 خدمات اینترنت</button>
</div><div id="products" class="products"></div><section id="cart" class="cart">
<h2>🛒 سبد خرید</h2>
<div id="items">سبد خرید خالی است.</div>
<div class="total">مجموع: <span id="total">۰</span> تومان</div>
<button onclick="checkout()" style="width:100%">ثبت سفارش در تلگرام 💬</button>
</section><section id="support" class="cart">
<h2>💬 پشتیبانی</h2>
<p>برای پرسش درباره محصولات یا پیگیری سفارش با ما ارتباط بگیر.</p>
<a id="supportLink" class="telegram" href="https://t.me/YOUR_TELEGRAM">ورود به تلگرام</a>
</section>
</main><footer>© PARSA SHOP</footer><script>
// آیدی تلگرام خودت را بدون @ وارد کن
const TELEGRAM="YOUR_TELEGRAM";

// قیمت‌ها و محصولات زیر نمونه‌اند و باید قبل از فروش اصلاح شوند.
const products=[
{id:1,name:"ویو تلگرام",cat:"تلگرام",icon:"👁️",desc:"خدمات بازدید پست",price:30000},
{id:2,name:"ممبر تلگرام",cat:"تلگرام",icon:"👥",desc:"خدمات اعضای کانال",price:50000},
{id:3,name:"ری‌اکشن تلگرام",cat:"تلگرام",icon:"❤️",desc:"خدمات واکنش به پست",price:25000},
{id:4,name:"تلگرام پریمیوم",cat:"تلگرام",icon:"⭐",desc:"اشتراک رسمی؛ قیمت نمونه",price:200000},
{id:5,name:"تلگرام استارز",cat:"تلگرام",icon:"🌟",desc:"محصول دیجیتال؛ قیمت نمونه",price:100000},
{id:6,name:"شماره مجازی",cat:"شماره مجازی",icon:"📱",desc:"برای سرویس‌های پشتیبانی‌شده",price:50000},
{id:7,name:"گیفت‌کارت Visa",cat:"کارت پرداخت",icon:"💳",desc:"محصول معتبر؛ شرایط استفاده را بررسی کن",price:300000},
{id:8,name:"خدمات Mastercard",cat:"کارت پرداخت",icon:"💳",desc:"خدمات پرداخت مجاز",price:350000},
{id:9,name:"بازی PS5 - اکشن",cat:"PS5",icon:"🎮",desc:"نسخه قانونی؛ عنوان و منطقه را مشخص کن",price:500000},
{id:10,name:"بازی PS5 - ورزشی",cat:"PS5",icon:"⚽",desc:"نسخه قانونی؛ عنوان و منطقه را مشخص کن",price:450000},
{id:11,name:"بازی PC - اکشن",cat:"PC",icon:"🖥️",desc:"نسخه قانونی بازی",price:300000},
{id:12,name:"بازی PC - مسابقه‌ای",cat:"PC",icon:"🏎️",desc:"نسخه قانونی بازی",price:280000},
{id:13,name:"خدمات اینترنت",cat:"اینترنت",icon:"🌐",desc:"سرویس مجاز اینترنت",price:70000}
];

let category="همه",cart=[];
const fmt=n=>n.toLocaleString("fa-IR");

function renderProducts(){
 const q=document.getElementById("search").value.trim().toLowerCase();
 const list=products.filter(p=>(category==="همه"||p.cat===category)&&(p.name.toLowerCase().includes(q)||p.desc.toLowerCase().includes(q)));
 document.getElementById("products").innerHTML=list.length?list.map(p=>`
 <article class="card">
 <div class="icon">${p.icon}</div><h3>${p.name}</h3><p>${p.desc}</p>
 <p class="price">${fmt(p.price)} تومان</p>
 <button onclick="add(${p.id})">افزودن به سبد خرید</button>
 </article>`).join(""):"محصولی پیدا نشد.";
}
function setCat(c,b){
 category=c;
 document.querySelectorAll(".categories button").forEach(x=>x.classList.remove("active"));
 b.classList.add("active");renderProducts();
}
function add(id){
 const p=cart.find(x=>x.id===id);
 if(p)p.qty++;else cart.push({...products.find(x=>x.id===id),qty:1});
 renderCart();
}
function change(id,n){
 const p=cart.find(x=>x.id===id);if(!p)return;
 p.qty+=n;if(p.qty<=0)cart=cart.filter(x=>x.id!==id);
 renderCart();
}
function renderCart(){
 document.getElementById("count").textContent=fmt(cart.reduce((s,p)=>s+p.qty,0));
 document.getElementById("items").innerHTML=cart.length?cart.map(p=>`
 <div class="cart-item"><span>${p.icon} ${p.name}<br>${fmt(p.price)} تومان</span>
 <span><button onclick="change(${p.id},-1)">−</button> ${fmt(p.qty)} <button onclick="change(${p.id},1)">+</button>
 <button class="remove" onclick="change(${p.id},-${p.qty})">حذف</button></span></div>`).join(""):"سبد خرید خالی است.";
 document.getElementById("total").textContent=fmt(cart.reduce((s,p)=>s+p.price*p.qty,0));
}
function checkout(){
 if(!cart.length){alert("سبد خرید خالی است!");return}
 if(TELEGRAM==="YOUR_TELEGRAM"){alert("ابتدا آیدی تلگرامت را در کد وارد کن.");return}
 const lines=cart.map(p=>p.name+" × "+p.qty+" = "+fmt(p.price*p.qty)+" تومان");
 const total=cart.reduce((s,p)=>s+p.price*p.qty,0);
 const msg="سلام، برای این محصولات سفارش دارم:\n"+lines.join("\n")+"\nمجموع: "+fmt(total)+" تومان";
 window.open("https://t.me/"+TELEGRAM+"?text="+encodeURIComponent(msg),"_blank");
}
document.getElementById("search").addEventListener("input",renderProducts);
document.getElementById("supportLink").href="https://t.me/"+TELEGRAM;
renderProducts();renderCart();
</script></body>
</html>
