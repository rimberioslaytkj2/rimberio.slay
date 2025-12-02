<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>RIMBERIO.SLAY | Belanja gampang, hasilnya pasti — no zonk, no worries.</title>
  <meta name="description" content="RIMBERIO - layanan jastip dan penyedia alat jaringan yang aman, cepat, dan terpercaya. Apa pun yang sulit kamu jangkau, biar kami yang urus—tanpa ribet, tanpa takut zonk.">
  <link rel="icon" type="image/png" href="logo rimberio 1.png">
  <style>
    /* ---------- global ---------- */
    :root{
      --pink: #ff6ea6;
      --blue: #87CEFA;
      --white: #ffffff;
      --dark: #111111;
    }
    body{
      margin:0;
      font-family: "Montserrat", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background-color: #ffffff;
      color: #F81894;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    /* ---------- header ---------- */
    header{
      display:flex;
      justify-content:space-between;
      align-items:center;
      padding:20px 24px;
      border-bottom:1px solid var(--pink);
      gap:12px;
      flex-wrap:wrap;
    }
    .logo-box{
      display:flex;
      align-items:center;
      gap:12px;
    }
    .logo-box img{
      height:80px; /* kecilkan supaya pas di HP */
      width:80px;
      object-fit:cover;
      border-radius:8px;
    }
    header h1{
      margin:0;
      font-size:1.2rem;
      letter-spacing:2px;
      color:var(--pink);
    }
    nav{
      display:flex;
      gap:14px;
      align-items:center;
    }
    nav a{
      color:var(--pink);
      text-decoration:none;
      font-weight:600;
      font-size:0.95rem;
    }
    nav a:hover{ color:#000; }

    .cart-icon{ position:relative; cursor:pointer; display:flex; align-items:center; gap:8px; }
    .cart-icon img{ width:44px; height:44px; }
    .cart-count{
      position:absolute;
      top:-6px;
      right:-6px;
      background:var(--pink);
      color:white;
      font-size:0.7rem;
      padding:3px 6px;
      border-radius:999px;
      font-weight:700;
    }

    /* ---------- section & tentang ---------- */
    section{ padding:48px 20px; text-align:center; }
    #tentang{
      max-width:700px;
      margin:30px auto;
      padding:12px;
      line-height:1.6;
      text-align:left;
    }
    #tentang h2{ text-align:center; margin-bottom:8px; font-size:22px; }
    #tentang p{ margin:0; font-size:15px; }

    /* ---------- produk grid ---------- */
    .produk-container{
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(200px, 1fr));
      gap:18px;
      padding:0 20px;
      margin-top:20px;
    }
    .produk{
      background:#fff;
      border:1px solid var(--pink);
      border-radius:8px;
      overflow:hidden;
      transition:transform .18s ease, box-shadow .18s ease;
      text-align:center;
      padding-bottom:12px;
    }
    .produk:hover{ transform:translateY(-4px); box-shadow:0 8px 22px rgba(0,0,0,0.08); }
    .produk img{ width:100%; height:140px; object-fit:cover; border-bottom:1px solid var(--pink); }
    .produk h3{ margin:10px 8px 4px; font-size:1rem; color:var(--dark); }
    .produk p{ margin:6px 8px; color:#666; font-size:0.9rem; }

    .jumlah-box{ display:flex; justify-content:center; align-items:center; gap:8px; margin:8px 0; }
    .jumlah-input{
      width:56px; text-align:center; border-radius:6px; padding:6px; border:1px solid var(--pink);
      font-weight:600;
    }
    .minus, .plus{
      background:var(--white);
      color:var(--dark);
      border:none;
      border-radius:6px;
      font-size:16px;
      font-weight:700;
      width:32px; height:32px;
      cursor:pointer;
    }
    .minus:hover, .plus:hover{ transform:scale(1.05); background:var(--blue); color:#000; }

    .produk button.add-btn{
      background:var(--blue);
      color:#fff;
      border:none;
      padding:8px 12px;
      border-radius:6px;
      font-weight:700;
      cursor:pointer;
      margin-top:6px;
    }
    .produk button.add-btn:hover{ background:var(--pink); color:#000; }

    /* ---------- cart popup ---------- */
    .cart-popup{
      position:fixed;
      top:70px;
      right:20px;
      width:320px;
      max-width:90%;
      background:var(--blue);
      border:1px solid var(--pink);
      border-radius:10px;
      padding:14px;
      display:none;
      z-index:1000;
      box-shadow:0 14px 40px rgba(0,0,0,0.18);
    }
    .cart-popup .close-btn{
      float:right; background:transparent; border:none; font-size:18px; cursor:pointer; color:#000;
    }
    .cart-popup h3{ margin:6px 0 10px; color:#000; }
    .cart-item{ display:flex; justify-content:space-between; align-items:center; padding:8px 0; border-bottom:1px solid rgba(0,0,0,0.08); }
    .cart-item span.name{ color:#000; font-weight:600; }
    .cart-item span.price{ color:#333; }
    .cart-item button.remove{ background:transparent; border:none; color:red; font-size:16px; cursor:pointer; }

    .cart-popup .checkout, .cart-popup .clear{
      background:var(--pink); color:#000; border:none; width:100%; padding:10px; margin-top:10px; border-radius:8px; cursor:pointer; font-weight:700;
    }
    .cart-popup .checkout:hover, .cart-popup .clear:hover{ opacity:0.95; }

    /* ---------- admin/login popup ---------- */
    .overlay-popup{
      position:fixed;
      top:0; left:0; right:0; bottom:0;
      display:none;
      z-index:1200;
      align-items:center;
      justify-content:center;
      background:rgba(0,0,0,0.35);
    }
    .popup-box{
      background:var(--white);
      border-radius:10px;
      padding:16px;
      width:320px;
      max-width:94%;
      box-shadow:0 12px 36px rgba(0,0,0,0.22);
    }
    .popup-box .close-btn{ float:right; background:transparent; border:none; font-size:18px; cursor:pointer; }
    .popup-box h3{ margin-top:0; color:var(--dark); }

    .popup-box input, .popup-box select{
      width:100%; padding:8px; margin-top:8px; border-radius:6px; border:1px solid #ddd; box-sizing:border-box;
    }
    .popup-box button.action{
      background:var(--blue); color:#000; border:none; padding:10px; border-radius:8px; width:100%; margin-top:10px; font-weight:700; cursor:pointer;
    }
    .popup-box button.action:hover{ background:var(--pink); }

    /* ---------- notif ---------- */
    #notif{
      position:fixed; top:18px; right:18px; padding:10px 14px; border-radius:8px; font-weight:700;
      background:rgba(212,175,55,0.95); color:#000; box-shadow:0 10px 30px rgba(0,0,0,0.18);
      transform:translateY(-8px); opacity:0; transition:all .35s ease; z-index:2000;
    }
    #notif.show{ opacity:1; transform:translateY(0); }
    #notif.type-red{ background:#ff4d4d; color:#fff; }
    #notif.type-green{ background:#28b463; color:#fff; }
    #notif.type-orange{ background:orange; color:#000; }

    /* ---------- responsive ---------- */
    @media (max-width:640px){
      header{ padding:12px 14px; }
      .logo-box img{ height:56px; width:56px; }
      .produk img{ height:120px; }
      .cart-popup{ right:10px; top:64px; width:90%; }
    }

  </style>
</head>
<body>

  <header>
    <div class="logo-box">
      <img src="logo rimberio 1.png" alt="Logo RIMBERIO">
      <div>
        <h1>RIMBERIO</h1>
        <div style="font-size:12px; color:#666;">Belanja gampang, hasilnya pasti — no zonk</div>
      </div>
    </div>

    <nav>
      <a href="#home">Home</a>
      <a href="#produk">Produk</a>
      <a href="#tentang">Tentang</a>
      <a href="#kontak">Kontak</a>
    </nav>

    <div class="cart-icon" onclick="toggleCart()">
      <img src="keranjang.png" alt="Keranjang">
      <div class="cart-count" id="cart-count">0</div>
    </div>
  </header>

  <section id="home">
    <h2>WELCOME TO RIMBERIO</h2>
    <h3 style="margin-top:8px; font-weight:600; color:#333;">Rimberio - Your reliable shopping partner</h3>
    <p style="max-width:760px; margin:14px auto 0; color:#444;">
      Rimberio merupakan layanan Jastip dan penyedia perlengkapan jaringan yang berkomitmen memberikan pengalaman belanja aman dan terpercaya.
      Kami menghadirkan berbagai produk yang sulit dijangkau pelanggan, dari kebutuhan sehari-hari sampai perlengkapan jaringan.
    </p>
  </section>

  <section id="produk">
    <h2 style="text-align:center;">Produk Kami</h2>
    <div class="produk-container" id="produk-container"></div>
  </section>

  <!-- cart popup -->
  <div class="cart-popup" id="cart-popup" aria-hidden="true">
    <button class="close-btn" onclick="closeCart()">X</button>
    <h3>Keranjang</h3>
    <div id="cart-items" style="margin-top:8px;"></div>
    <p id="cart-total" style="font-weight:700; margin-top:10px;">Total: Rp0</p>
    <button class="checkout" onclick="checkout()">Checkout (WhatsApp)</button>
    <button class="checkout" onclick="checkoutEmail()">Checkout (Email)</button>
    <button class="clear" onclick="clearCart()">Kosongkan Keranjang</button>
  </div>

  <!-- overlay popups (login/admin) -->
  <div id="overlay-login" class="overlay-popup" style="display:none; align-items:center;">
    <div class="popup-box" role="dialog" aria-modal="true">
      <button class="close-btn" onclick="closeLogin()">X</button>
      <h3>Login Admin</h3>
      <input type="password" id="admin-password" placeholder="Masukkan password">
      <button class="action" onclick="checkPassword()">Login</button>
    </div>
  </div>

  <div id="overlay-admin" class="overlay-popup" style="display:none; align-items:center;">
    <div class="popup-box" role="dialog" aria-modal="true">
      <button class="close-btn" onclick="closeAdmin()">X</button>
      <h3>Admin Panel</h3>
      <select id="admin-produk-select"></select>
      <input type="number" id="admin-harga" placeholder="Harga (contoh: 3000)">
      <input type="number" id="admin-stok" placeholder="Stok (contoh: 10)">
      <button class="action" onclick="updateProduk()">Update Produk</button>
    </div>
  </div>

  <section id="tentang">
    <div id="tentang">
      <h2>Tentang RIMBERIO.SLAY</h2>
      <p>
        Rimberio adalah layanan Jastip (Jasa Titip) dan penyedia alat jaringan yang membantu proses belanja.
        Pelanggan dapat menitipkan pembelian barang apa saja — mulai dari kebutuhan sehari-hari, fashion, aksesoris, alat elektronik,
        hingga perlengkapan jaringan seperti kabel LAN, konektor,dan perangkat pendukung lainnya.
        <br><br>
        Kami mengutamakan: <strong>Kepercayaan, Kemudahan, Kualitas,</strong> dan <strong>Kecepatan</strong>.
        Dengan motto "Trusted shopping, zero worries", Rimberio berkomitmen memberikan pengalaman belanja yang aman dan nyaman.
      </p>
    </div>
  </section>

  <section id="kontak">
    <h2 style="text-align:center;">Kontak Kami</h2>
    <p style="text-align:center;">
      <img src="email.png" alt="email" style="width:18px; vertical-align:middle;">&nbsp;
      <a href="https://mail.google.com/mail/?view=cm&to=rimberiotkj2@gmail.com">rimberiotkj2@gmail.com</a>
      <br><br>
      <img src="instagram.png" alt="ig" style="width:18px; vertical-align:middle;">&nbsp;
      <a href="https://www.instagram.com/rimberio.slay" target="_blank">rimberio.slay</a>
      &nbsp;|&nbsp;
      <img src="tiktok.png" alt="tiktok" style="width:18px; vertical-align:middle;">&nbsp;
      <a href="https://www.tiktok.com/@rimberio.slay?_r=1&_t=ZS-91sXB154ibU" target="_blank">rimberio278</a>
    </p>
  </section>

  <footer style="text-align:center; padding:18px; border-top:1px solid #eee;">
    <small>© 2025 RIMBERIO. All Rights Reserved.</small>
  </footer>

  <div id="notif" role="status" aria-live="polite"></div>

  <script>
    /* =====================
       Data persistence + init
       ===================== */

    // Jika belum ada produkData di localStorage, isi default; kalau sudah ada, gunakan yang tersimpan
    let defaultProduk = [
      { id: 1, nama: "KABEL UTP CAT 5e", harga: 3000, stok: 10, gambar: "gambar1.jfif" },
      { id: 2, nama: "KONEKTOR RJ-45", harga: 3000, stok: 5, gambar: "gambar2.jfif" },
      { id: 3, nama: "CARGER HANDPHONE", harga: 20000, stok: 100, gambar: "gambar5.jfif" },
      { id: 4, nama: "MIKRO USB", harga: 10000, stok: 12, gambar: "gambar3.jfif" },
      { id: 5, nama: "HEADSET Kabel", harga: 15000, stok: 3, gambar: "gambar7.jpg" }
    ];

    // load produkData (tetap setelah refresh)
    let produkData = JSON.parse(localStorage.getItem("produkData")) || defaultProduk;
    // jika tidak ada di storage, simpan default agar tetap persist setelah pertama load
    if (!localStorage.getItem("produkData")) {
      localStorage.setItem("produkData", JSON.stringify(produkData));
    }

    // cart (tidak perlu persist kecuali mau)
    let cart = JSON.parse(localStorage.getItem("cartData")) || [];

    // elemen
    const container = document.getElementById('produk-container');
    const cartPopup = document.getElementById('cart-popup');
    const cartCount = document.getElementById('cart-count');
    const cartItemsContainer = document.getElementById('cart-items');
    const cartTotal = document.getElementById('cart-total');
    const notif = document.getElementById('notif');
    const overlayLogin = document.getElementById('overlay-login');
    const overlayAdmin = document.getElementById('overlay-admin');

    /* ---------- helpers ---------- */
    function saveProduk() {
      localStorage.setItem("produkData", JSON.stringify(produkData));
    }
    function saveCart() {
      localStorage.setItem("cartData", JSON.stringify(cart));
    }

    function showNotif(text, type = "default") {
      notif.className = '';
      notif.textContent = text;
      if (type === "red") notif.classList.add('type-red');
      else if (type === "green") notif.classList.add('type-green');
      else if (type === "orange") notif.classList.add('type-orange');
      notif.classList.add('show');
      setTimeout(() => notif.classList.remove('show'), 2200);
    }

    /* ---------- render produk ---------- */
    function renderProduk() {
      container.innerHTML = '';
      produkData.forEach(p => {
        const div = document.createElement('div');
        div.className = 'produk';
        div.innerHTML = `
          <img src="${p.gambar}" alt="${p.nama}">
          <h3>${p.nama}</h3>
          <p>Harga: Rp${p.harga.toLocaleString()}</p>
          <p>Stok: ${p.stok}</p>
          <div class="jumlah-box">
            <button class="minus" onclick="ubahJumlah(${p.id}, -1)">-</button>
            <input type="number" id="jumlah-${p.id}" value="1" min="1" max="${p.stok}" class="jumlah-input">
            <button class="plus" onclick="ubahJumlah(${p.id}, 1)">+</button>
          </div>
          <button class="add-btn" id="btn-${p.id}" onclick="addToCart(${p.id})" ${p.stok <= 0 ? 'disabled style="background:#ccc;cursor:not-allowed;"' : ''}>${p.stok > 0 ? 'Tambah ke Keranjang' : 'Stok Habis'}</button>
        `;
        container.appendChild(div);
      });
    }

    function ubahJumlah(id, perubahan) {
      const input = document.getElementById(`jumlah-${id}`);
      if (!input) return;
      let nilai = parseInt(input.value) || 1;
      nilai += perubahan;
      if (nilai < 1) nilai = 1;
      const produk = produkData.find(p => p.id === id);
      if (produk && nilai > produk.stok) nilai = produk.stok;
      input.value = nilai;
    }

    /* ---------- cart functions ---------- */
    function addToCart(id) {
      const produk = produkData.find(p => p.id === id);
      const jumlahInput = document.getElementById(`jumlah-${id}`);
      const jumlah = parseInt(jumlahInput.value) || 0;
      if (jumlah <= 0) return showNotif("Masukkan jumlah!", "red");
      if (jumlah > produk.stok) return showNotif("Stok tidak cukup!", "red");

      const item = cart.find(c => c.id === id);
      if (item) {
        if (item.jumlah + jumlah > produk.stok) return showNotif("Stok tidak cukup!", "red");
        item.jumlah += jumlah;
      } else {
        cart.push({ id, jumlah });
      }
      saveCart();
      showNotif(`${jumlah}x ${produk.nama} ditambahkan`, "green");
      updateCart();
    }

    function toggleCart() {
      const isVisible = cartPopup.style.display === 'block';
      cartPopup.style.display = isVisible ? 'none' : 'block';
    }
    function closeCart() { cartPopup.style.display = 'none'; }

    function updateCart() {
      cartCount.textContent = cart.reduce((a,c)=>a+c.jumlah, 0);
      cartItemsContainer.innerHTML = '';
      let total = 0;
      cart.forEach(c => {
        const p = produkData.find(x => x.id === c.id);
        total += c.jumlah * p.harga;
        const div = document.createElement('div');
        div.className = 'cart-item';
        div.innerHTML = `<span class="name">${p.nama} x${c.jumlah}</span><span class="price">Rp${(p.harga*c.jumlah).toLocaleString()}</span>
          <button class="remove" onclick="removeCart(${c.id})" title="Hapus">X</button>`;
        cartItemsContainer.appendChild(div);
      });
      cartTotal.textContent = `Total: Rp${total.toLocaleString()}`;
    }

    function removeCart(id) {
      cart = cart.filter(c => c.id !== id);
      saveCart();
      updateCart();
      showNotif("Item dihapus dari keranjang!", "orange");
    }

    function clearCart(){
      if (cart.length === 0) { showNotif("Keranjang sudah kosong", "orange"); return; }
      cart = [];
      saveCart();
      updateCart();
      showNotif("Keranjang dikosongkan", "orange");
    }

    function checkout(){
      if (cart.length === 0) { alert("Keranjang kosong!"); return; }

      // cek stok lagi & kurangi stok
      for (let c of cart) {
        const p = produkData.find(x => x.id === c.id);
        if (!p || p.stok < c.jumlah) {
          alert("Stok tidak cukup untuk " + (p ? p.nama : "produk"));
          return;
        }
      }

      cart.forEach(c => {
        const p = produkData.find(x => x.id === c.id);
        p.stok -= c.jumlah;
      });

      saveProduk();
      renderProduk();

      // buat pesan WA
      let message = "Halo, saya ingin memesan:%0A%0A";
      cart.forEach(c => {
        const p = produkData.find(x => x.id === c.id);
        message += `- ${p.nama} x${c.jumlah}%0A`;
      });
      const total = cart.reduce((a,c)=>a + produkData.find(p=>p.id===c.id).harga*c.jumlah,0);
      message += `%0ATotal: Rp${total.toLocaleString()}%0A%0ATerima kasih.`;

      const encodedMessage = encodeURIComponent(decodeURIComponent(message));
      // buka WA (ganti nomor jika perlu)
      window.open(`https://wa.me/6283152859084?text=${encodedMessage}`, '_blank');

      cart = [];
      saveCart();
      updateCart();
      showNotif("Checkout berhasil! (WA terbuka)", "green");
      closeCart();
    }

    function checkoutEmail(){
      if (cart.length === 0) { showNotif("Keranjang kosong!", "orange"); return; }
      let body = "Halo, saya ingin memesan:%0A%0A";
      cart.forEach(c => {
        const p = produkData.find(x => x.id === c.id);
        body += `- ${p.nama} x${c.jumlah}%0A`;
      });
      const total = cart.reduce((a,c)=>a + produkData.find(p=>p.id===c.id).harga*c.jumlah,0);
      body += `%0ATotal: Rp${total.toLocaleString()}%0A%0ATerima kasih.`;
      window.location.href = `mailto:rimberiotkj2@gmail.com?subject=Pesanan RIMBERIO&body=${encodeURIComponent(body)}`;
      showNotif("Checkout via Email dibuka", "green");
      closeCart();
    }

    /* ---------- admin/login ---------- */
    function showLogin(){
      overlayLogin.style.display = 'flex';
    }
    function closeLogin(){
      overlayLogin.style.display = 'none';
    }
    function showAdmin(){
      // isi select
      const sel = document.getElementById('admin-produk-select');
      sel.innerHTML = '';
      produkData.forEach(p => {
        const opt = document.createElement('option');
        opt.value = p.id;
        opt.textContent = p.nama;
        sel.appendChild(opt);
      });
      overlayAdmin.style.display = 'flex';
    }
    function closeAdmin(){
      overlayAdmin.style.display = 'none';
    }
    function checkPassword(){
      const pass = document.getElementById('admin-password').value;
      if (pass === "rimberiotkj2") {
        closeLogin();
        showAdmin();
      } else {
        showNotif("Password salah!", "red");
      }
    }
    function updateProduk(){
      const id = parseInt(document.getElementById('admin-produk-select').value);
      const harga = parseInt(document.getElementById('admin-harga').value);
      const stok = parseInt(document.getElementById('admin-stok').value);
      const p = produkData.find(x => x.id === id);
      if (!p) return showNotif("Pilih produk dulu", "orange");
      if (!isNaN(harga) && harga > 0) p.harga = harga;
      if (!isNaN(stok) && stok >= 0) p.stok = stok;
      saveProduk();
      renderProduk();
      showNotif("Produk diperbarui!", "green");
      closeAdmin();
    }

    /* ---------- init render ---------- */
    function init(){
      renderProduk();
      updateCart();
      // jika mau tampilkan tombol admin (misal di kanan bawah), kita pake event:
      document.getElementById('admin-btn')?.remove?.(); // jika ada duplicate from previous copies, bersihkan
      // buat tombol admin kecil (tetap ada agar mudah buka login)
      const adminBtn = document.createElement('button');
      adminBtn.id = 'admin-btn-top';
      adminBtn.style.position = 'fixed';
      adminBtn.style.bottom = '20px';
      adminBtn.style.left = '20px';
      adminBtn.style.background = 'var(--pink)';
      adminBtn.style.color = '#fff';
      adminBtn.style.border = 'none';
      adminBtn.style.padding = '8px 12px';
      adminBtn.style.borderRadius = '999px';
      adminBtn.style.cursor = 'pointer';
      adminBtn.style.zIndex = 1500;
      adminBtn.textContent = 'Admin';
      adminBtn.onclick = showLogin;
      document.body.appendChild(adminBtn);
    }

    // jalankan init
    init();

    // expose beberapa fungsi ke global supaya onclick inline bisa memanggilnya
    window.ubahJumlah = ubahJumlah;
    window.addToCart = addToCart;
    window.toggleCart = toggleCart;
    window.closeCart = closeCart;
    window.removeCart = removeCart;
    window.clearCart = clearCart;
    window.checkout = checkout;
    window.checkoutEmail = checkoutEmail;
    window.showLogin = showLogin;
    window.closeLogin = closeLogin;
    window.checkPassword = checkPassword;
    window.closeAdmin = closeAdmin;
    window.updateProduk = updateProduk;

  </script>
</body>
</html>
