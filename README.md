# Boikini.com
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>বই কিনি.কম - ই-কমার্স</title>
  <style>
    *{box-sizing:border-box;margin:0;padding:0;font-family: 'Noto Sans', sans-serif;}
    body{background:#f4f6f8;color:#222;}
    header{
      background:#4a3aff;color:#fff;padding:15px 20px;display:flex;justify-content:space-between;align-items:center;
      position:sticky;top:0;z-index:1000;
    }
    header h1{font-size:24px;cursor:pointer;}
    nav a{
      color:#fff;margin-left:20px;text-decoration:none;font-weight:600;
      transition:color 0.3s;
    }
    nav a:hover{color:#c8c8ff;}
    .container{max-width:1100px;margin:20px auto;padding:0 15px;}
    .products{
      display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:20px;
    }
    .card{
      background:#fff;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.05);
      overflow:hidden;display:flex;flex-direction:column;transition:transform 0.3s;
    }
    .card:hover{transform:translateY(-5px);}
    .card img{
      width:100%;height:220px;object-fit:cover;
    }
    .card-body{
      padding:15px;flex:1;display:flex;flex-direction:column;
    }
    .card-body h3{
      font-size:18px;margin-bottom:8px;color:#3b3b3b;
    }
    .card-body p{
      color:#777;font-size:14px;flex-grow:1;
    }
    .price{
      font-weight:700;color:#4a3aff;margin-top:10px;font-size:18px;
    }
    button{
      margin-top:12px;padding:10px;cursor:pointer;background:#4a3aff;color:#fff;border:none;border-radius:8px;
      font-weight:600;transition:background 0.3s;
    }
    button:hover{
      background:#3a2ecb;
    }
    /* Cart Floating Button */
    #cartBtn{
      position:fixed;bottom:20px;right:20px;background:#4a3aff;color:#fff;padding:12px 18px;
      border-radius:50px;cursor:pointer;box-shadow:0 6px 15px rgba(74,58,255,0.5);
      font-weight:700;z-index:2000;display:flex;align-items:center;gap:8px;
    }
    #cartBtn span{
      background:#fff;color:#4a3aff;padding:2px 8px;border-radius:12px;font-weight:700;font-size:14px;
    }
    /* Cart Modal */
    #cartModal{
      position:fixed;top:50%;left:50%;transform:translate(-50%, -50%);
      background:#fff;max-width:420px;width:90%;max-height:70vh;overflow-y:auto;
      border-radius:15px;box-shadow:0 10px 30px rgba(0,0,0,0.2);
      display:none;flex-direction:column;z-index:3000;
    }
    #cartModal.open{
      display:flex;
    }
    #cartModal header{
      padding:15px 20px;border-bottom:1px solid #eee;display:flex;justify-content:space-between;align-items:center;
      font-weight:700;font-size:18px;
    }
    #cartModal .body{
      padding:15px 20px;flex-grow:1;
    }
    #cartModal .cart-item{
      display:flex;gap:12px;margin-bottom:15px;align-items:center;
    }
    #cartModal .cart-item img{
      width:64px;height:90px;object-fit:cover;border-radius:10px;
    }
    #cartModal .cart-item-details{
      flex-grow:1;
    }
    #cartModal .cart-item-details h4{
      margin-bottom:5px;font-size:16px;color:#333;
    }
    #cartModal .cart-item-details .price{
      font-weight:700;color:#4a3aff;
    }
    #cartModal .qty-controls{
      display:flex;gap:6px;align-items:center;
    }
    #cartModal .qty-controls button{
      width:28px;height:28px;border:none;background:#4a3aff;color:#fff;font-weight:700;
      border-radius:6px;cursor:pointer;
      font-size:20px;line-height:20px;
    }
    #cartModal .qty-controls span{
      min-width:24px;text-align:center;display:inline-block;
      font-weight:700;font-size:16px;
    }
    #cartModal footer{
      padding:15px 20px;border-top:1px solid #eee;
      display:flex;justify-content:space-between;align-items:center;
      font-weight:700;font-size:18px;
    }
    #cartModal footer button{
      background:#4a3aff;padding:10px 18px;border:none;border-radius:8px;
      color:#fff;cursor:pointer;
      transition:background 0.3s;
    }
    #cartModal footer button:hover{
      background:#3a2ecb;
    }
    /* Responsive */
    @media(max-width:600px){
      header h1{font-size:20px;}
      nav a{margin-left:12px;font-size:14px;}
      #cartModal{max-width:95%;}
      .products{grid-template-columns:1fr;}
    }
  </style>
</head>
<body>

<header>
  <h1 onclick="window.location.reload()">📚 বই কিনি.কম</h1>
  <nav>
    <a href="#home" onclick="window.scrollTo({top:0,behavior:'smooth'})">হোম</a>
    <a href="#products" onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">বইসমূহ</a>
    <a href="#contact" onclick="document.getElementById('contact').scrollIntoView({behavior:'smooth'})">যোগাযোগ</a>
  </nav>
</header>

<main class="container" id="home">
  <section style="margin-bottom:40px;text-align:center;">
    <h2>আপনার পছন্দের বই কিনুন দ্রুত ও সহজে</h2>
    <p style="color:#555;margin-top:8px;">নির্ভরযোগ্য অনলাইন বুকস্টোর</p>
  </section>

  <section id="products">
    <h2 style="margin-bottom:20px;">নতুন বইসমূহ</h2>
    <div class="products" id="productsGrid">
      <!-- প্রোডাক্টগুলো এখানে ডাইনামিক্যালি যুক্ত হবে -->
    </div>
  </section>
</main>

<!-- কার্ট বাটন -->
<div id="cartBtn" title="আপনার কার্ট">
  🛒 <span id="cartCount">0</span>
</div>

<!-- কার্ট মডাল -->
<div id="cartModal" role="dialog" aria-modal="true" aria-labelledby="cartTitle">
  <header>
    <div id="cartTitle">আপনার কার্ট</div>
    <button onclick="closeCart()" aria-label="কার্ট বন্ধ করুন" style="background:none;border:none;font-size:24px;cursor:pointer;">×</button>
  </header>
  <div class="body" id="cartItems">
    <!-- কার্ট আইটেমগুলো এখানে দেখানো হবে -->
  </div>
  <footer>
    <div>মোট: ৳<span id="cartTotal">0</span></div>
    <button onclick="checkout()">চেকআউট</button>
  </footer>
</div>

<section class="container" id="contact" style="margin-top:80px; text-align:center;">
  <h2>যোগাযোগ করুন</h2>
  <p>📞 ফোন: 01300-000000 | 📧 ইমেইল: support@boikini.com</p>
  <p style="font-size:14px;color:#666;margin-top:8px;">© 2025 বই কিনি.কম - সর্বস্বত্ব সংরক্ষিত</p>
</section>

<script>
  // Sample প্রোডাক্ট ডাটা
  const products = [
    {id: 1, title: 'প্রযুক্তির মৌলিক ধারণা', author: 'ড. রাহাত কবির', price: 450, img: 'https://images.unsplash.com/photo-1512820790803-83ca734da794?auto=format&fit=crop&w=800&q=60'},
    {id: 2, title: 'বাংলা উপন্যাস: ছায়ার গল্প', author: 'আরিফা হক', price: 320, img: 'https://images.unsplash.com/photo-1519681393784-d120267933ba?auto=format&fit=crop&w=800&q=60'},
    {id: 3, title: 'শিশুদের কল্পকাহিনি', author: 'মিতা রহমান', price: 220, img: 'https://images.unsplash.com/photo-1524985069026-dd778a71c7b4?auto=format&fit=crop&w=800&q=60'},
    {id: 4, title: 'জাভাস্ক্রিপ্ট হাতে-কলমে', author: 'সুমন দত্ত', price: 550, img: 'https://images.unsplash.com/photo-1518779578993-ec3579fee39f?auto=format&fit=crop&w=800&q=60'},
    {id: 5, title: 'বাংলা কবিতার সংগ্রহ', author: 'শাহরিয়া সবুজ শিশির', price: 280, img: 'https://images.unsplash.com/photo-1481627834876-b7833e8f5570?auto=format&fit=crop&w=800&q=60'}
  ];

  let cart = {};

  // Load cart from localStorage
  try {
    const saved = JSON.parse(localStorage.getItem('boikini_cart')||'{}');
    if(saved && typeof saved === 'object') cart = saved;
  } catch(e) {
    cart = {};
  }

  // Save cart to localStorage
  function saveCart(){
    localStorage.setItem('boikini_cart', JSON.stringify(cart));
    updateCartUI();
  }

  // Update cart UI count and total
  function updateCartUI(){
    const count = Object.values(cart).reduce((a,v)=>a+v.qty, 0);
    const total = Object.values(cart).reduce((a,v)=>a+v.qty*v.price, 0);
    document.getElementById('cartCount').innerText = count;
    document.getElementById('cartTotal').innerText = total;
    renderCartItems();
  }

  // Render products to page
  function renderProducts(){
    const grid = document.getElementById('productsGrid');
    grid.innerHTML = '';
    for(const p of products){
      const card = document.createElement('div');
      card.className = 'card';
      card.innerHTML = `
        <img src="${p.img}" alt="${p.title}" />
        <div class="card-body">
          <h3>${p.title}</h3>
          <p>লেখক: ${p.author}</p>
          <div class="price">৳${p.price}</div>
          <button onclick="addToCart(${p.id})">কার্টে যোগ করুন</button>
        </div>
      `;
      grid.appendChild(card);
    }
  }

  // Add product to cart
  function addToCart(id){
    const product = products.find(p => p.id === id);
    if(!product) return;
    if(cart[id]){
      cart[id].qty += 1;
    } else {
      cart[id] = {...product, qty: 1};
    }
    saveCart();
    alert(`${product.title} কার্টে যোগ করা হয়েছে!`);
  }

  // Render cart items in modal
  function renderCartItems(){
    const container = document.getElementById('cartItems');
    container.innerHTML = '';
    const items = Object.values(cart);
    if(items.length === 0){
      container.innerHTML = '<p style="text-align:center;color:#777;">আপনার কার্ট খালি</p>';
      return;
    }
    for(const item of items){
      const div = document.createElement('div');
      div.className = 'cart-item';
      div.innerHTML = `
        <img src="${item.img}" alt="${item.title}" />
        <div class="cart-item-details">
          <h4>${item.title}</h4>
          <p>লেখক: ${item.author}</p>
          <div class="price">৳${item.price} × ${item.qty} = ৳${item.price * item.qty}</div>
          <div class="qty-controls">
            <button onclick="changeQty(${item.id}, -1)">−</button>
            <span>${item.qty}</span>
            <button onclick="changeQty(${item.id}, 1)">+</button>
          </div>
        </div>
      `;
      container.appendChild(div);
    }
  }

  // Change quantity of an item in cart
  function changeQty(id, delta){
    if(!cart[id]) return;
    cart[id].qty += delta;
    if(cart[id].qty <= 0) delete cart[id];
    saveCart();
  }

  // Open cart modal
  document.getElementById('cartBtn').addEventListener('click', ()=>{
    document.getElementById('cartModal').classList.add('open');
  });

  // Close cart modal
  function closeCart(){
    document.getElementById('cartModal').classList.remove('open');
  }

  // Checkout simulation
  function checkout(){
    const items = Object.values(cart);
    if(items.length === 0){
      alert('প্রথমে কার্টে কিছু যোগ করুন!');
      return;
    }
    let total = items.reduce((a,v)=>a+v.qty*v.price, 0);
    if(confirm(`আপনি মোট ৳${total} পরিশোধ করতে চান? (সিমুলেটেড)`)){
      cart = {};
      saveCart();
      closeCart();
      alert('অর্ডার সম্পন্ন হয়েছে, ধন্যবাদ!');
    }
  }

  // Initialize site
  renderProducts();
  updateCartUI();

  // Expose functions to global for inline onclick
  window.addToCart = addToCart;
  window.changeQty = changeQty;
  window.closeCart = closeCart;
  window.checkout = checkout;
</script>
