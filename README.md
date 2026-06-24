<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>E-Commerce Catalog</title>
  <style>
    :root {
      --bg-dark: #0D1B2A;
      --bg-light: #F0EDE8;
      --accent: #008080;
      --text-dark: #F0EDE8;
      --text-light: #0D1B2A;
    }
    body {
      margin: 0;
      font-family: system-ui, sans-serif;
      background: var(--bg-dark);
      color: var(--text-dark);
      transition: background 0.3s, color 0.3s;
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem;
      background: var(--accent);
    }
    nav a {
      margin: 0 1rem;
      color: var(--text-dark);
      text-decoration: none;
      font-weight: bold;
    }
    .container {
      padding: 2rem;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
    }
    .card {
      background: var(--bg-light);
      color: var(--text-light);
      border-radius: 8px;
      padding: 1rem;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      transition: transform 0.2s;
    }
    .card:hover { transform: scale(1.05); }
    .card img {
      max-width: 100%;
      border-radius: 6px;
    }
    .theme-toggle {
      cursor: pointer;
      background: none;
      border: 2px solid var(--text-dark);
      padding: 0.5rem 1rem;
      border-radius: 6px;
      color: var(--text-dark);
    }
    footer {
      text-align: center;
      padding: 1rem;
      background: var(--accent);
      color: var(--text-dark);
    }
  </style>
</head>
<body>
  <header>
    <h1>ShopSmart</h1>
    <nav>
      <a href="#/" data-link>Home</a>
      <a href="#/catalog" data-link>Catalog</a>
      <a href="#/about" data-link>About</a>
    </nav>
    <button class="theme-toggle">Toggle Theme</button>
  </header>

  <main id="app"></main>

  <footer>
    <p>&copy; 2026 ShopSmart. All rights reserved.</p>
  </footer>

  <script>
    // Theme Toggle
    const toggleBtn = document.querySelector('.theme-toggle');
    toggleBtn.addEventListener('click', () => {
      const dark = getComputedStyle(document.documentElement).getPropertyValue('--bg-dark').trim();
      if (document.body.style.background === dark) {
        document.body.style.background = 'var(--bg-light)';
        document.body.style.color = 'var(--text-light)';
      } else {
        document.body.style.background = 'var(--bg-dark)';
        document.body.style.color = 'var(--text-dark)';
      }
    });

    // Client-side Router
    const routes = {
      '/': "<h2>Welcome to ShopSmart</h2><p>Your one-stop shop for modern products.</p>",
      '/catalog': `
        <h2>Product Catalog</h2>
        <div class="container" id="catalog"></div>
      `,
      '/about': "<h2>About Us</h2><p>ShopSmart is a demo e-commerce platform showcasing modern web development.</p>"
    };

    function router() {
      const path = location.hash.replace('#', '') || '/';
      document.getElementById('app').innerHTML = routes[path] || "<h2>404 - Page Not Found</h2>";
      if (path === '/catalog') loadCatalog();
    }

    window.addEventListener('hashchange', router);
    window.addEventListener('load', router);

    // Mock Product Data
    const products = [
      { name: "Wireless Headphones", price: "$99", img: "https://via.placeholder.com/250?text=Headphones" },
      { name: "Smartwatch", price: "$149", img: "https://via.placeholder.com/250?text=Smartwatch" },
      { name: "Gaming Mouse", price: "$59", img: "https://via.placeholder.com/250?text=Mouse" },
      { name: "Mechanical Keyboard", price: "$129", img: "https://via.placeholder.com/250?text=Keyboard" }
    ];

    function loadCatalog() {
      const container = document.getElementById('catalog');
      container.innerHTML = products.map(p => `
        <div class="card">
          <img src="${p.img}" alt="${p.name}" loading="lazy" />
          <h3>${p.name}</h3>
          <p>${p.price}</p>
        </div>
      `).join('');
    }
  </script>
</body>
</html>
