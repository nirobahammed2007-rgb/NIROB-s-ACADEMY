index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NIROB'S ACADEMY – PDF Store</title>
  <style>
    :root {
      --bg: #f5f5f5;
      --card: #ffffff;
      --text: #000;
      --primary: #1a73e8;
      --shadow: rgba(0,0,0,0.1);
    }

    body.dark {
      --bg: #0d1117;
      --card: #161b22;
      --text: #e6edf3;
      --primary: #4493f8;
      --shadow: rgba(255,255,255,0.08);
    }

    body {
      margin: 0;
      padding: 0;
      background: var(--bg);
      font-family: Arial, sans-serif;
      color: var(--text);
      transition: 0.3s;
    }

    header {
      background: var(--primary);
      color: white;
      padding: 25px;
      text-align: center;
      font-size: 30px;
      font-weight: bold;
      box-shadow: 0 3px 8px var(--shadow);
    }

    /* Homepage */
    .home {
      max-width: 900px;
      margin: 40px auto;
      text-align: center;
    }

    .home button {
      margin-top: 20px;
      background: var(--primary);
      border: none;
      padding: 12px 25px;
      color: white;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
    }

    /* Store Section */
    .container {
      max-width: 1000px;
      margin: 30px auto;
      padding: 20px;
      display: none;
    }

    .search-box {
      width: 100%;
      padding: 12px;
      font-size: 18px;
      border-radius: 8px;
      border: 1px solid #ccc;
      margin-bottom: 20px;
    }

    .categories {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    .cat-btn {
      padding: 8px 18px;
      border-radius: 8px;
      cursor: pointer;
      border: none;
      background: var(--primary);
      color: white;
      font-size: 16px;
    }

    .products {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }

    .product {
      background: var(--card);
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 2px 6px var(--shadow);
      transition: 0.3s;
    }

    .product:hover {
      transform: translateY(-5px);
    }

    .product-title {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 8px;
    }

    .download-btn {
      margin-top: 10px;
      background: var(--primary);
      padding: 8px 15px;
      color: white;
      border-radius: 8px;
      display: inline-block;
      text-decoration: none;
    }

    /* Dark Mode Button */
    .dark-toggle {
      position: fixed;
      right: 20px;
      bottom: 20px;
      background: var(--primary);
      padding: 12px 18px;
      border-radius: 50%;
      cursor: pointer;
      color: white;
      font-size: 18px;
      border: none;
    }
  </style>
</head>
<body>

<header>NIROB'S ACADEMY</header>

<!-- Homepage -->
<div class="home" id="homePage">
  <h2>Welcome to NIROB'S ACADEMY PDF Store</h2>
  <p>Find all lecture sheets easily in one place.</p>
  <button onclick="openStore()">Enter Store</button>
</div>

<!-- Store Page -->
<div class="container" id="storePage">

  <input type="text" class="search-box" id="search" placeholder="Search lecture sheets..." onkeyup="filterProducts()" />

  <div class="categories">
    <button class="cat-btn" onclick="filterCategory('All')">All</button>
    <button class="cat-btn" onclick="filterCategory('Biology')">Biology</button>
    <button class="cat-btn" onclick="filterCategory('Chemistry')">Chemistry</button>
    <button class="cat-btn" onclick="filterCategory('Physics')">Physics</button>
    <button class="cat-btn" onclick="filterCategory('Math')">Math</button>
    <button class="cat-btn" onclick="filterCategory('ICT')">ICT</button>
  </div>

  <div class="products" id="productList"></div>

</div>

<!-- Dark Mode Button -->
<button class="dark-toggle" onclick="toggleDark()">🌙</button>

<script>
  const products = [
    { title: "Biology Lecture Sheet – Chapter 1", file: "bio1.pdf", cat: "Biology" },
    { title: "Biology Practical Notes", file: "bio_practical.pdf", cat: "Biology" },
    { title: "Chemistry Organic Intro", file: "chem_org.pdf", cat: "Chemistry" },
    { title: "Physics – Motion Chapter", file: "phy_motion.pdf", cat: "Physics" },
    { title: "Math – Algebra Sheet", file: "math_alg.pdf", cat: "Math" },
    { title: "ICT – Chapter 1", file: "ict1.pdf", cat: "ICT" }
  ];

  function loadProducts() {
    const list = document.getElementById("productList");
    list.innerHTML = "";
    products.forEach(p => {
      list.innerHTML += `
        <div class='product'>
          <div class='product-title'>${p.title}</div>
          <div>Category: ${p.cat}</div>
          <a class='download-btn' href="pdfs/${p.file}" download>Download</a>
        </div>`;
    });
  }

  function filterProducts() {
    let search = document.getElementById("search").value.toLowerCase();
    document.querySelectorAll('.product').forEach(p => {
      p.style.display = p.innerText.toLowerCase().includes(search) ? "block" : "none";
    });
  }

  function filterCategory(c) {
    document.querySelectorAll('.product').forEach(p => {
      if (c === "All" || p.innerText.includes(c)) p.style.display = "block";
      else p.style.display = "none";
    });
  }

  function toggleDark() {
    document.body.classList.toggle('dark');
  }

  function openStore() {
    document.getElementById('homePage').style.display = "none";
    document.getElementById('storePage').style.display = "block";
    loadProducts();
  }
</script>

</body>
</html>
