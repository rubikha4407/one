<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Product Catalogue with Multi-Level Filters</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="min-h-screen bg-slate-100">
  <!-- Navbar -->
  <header class="bg-slate-900 text-white">
    <div class="max-w-6xl mx-auto px-4 py-4 flex items-center justify-between">
      <h1 class="text-xl font-bold">MyShop Catalogue</h1>
      <span class="text-sm opacity-80">HTML5 • Tailwind CSS • JavaScript</span>
    </div>
  </header>

  <!-- Main Content -->
  <main class="max-w-6xl mx-auto px-4 py-6">
    <!-- Filters Section -->
    <section class="mb-6 bg-white rounded-2xl shadow p-4 md:p-6">
      <h2 class="text-lg font-semibold mb-4">Filters & Search</h2>

      <div class="grid gap-4 md:grid-cols-4">
        <!-- Search -->
        <div class="flex flex-col gap-1">
          <label for="searchInput" class="text-sm font-medium">Search (name)</label>
          <input
            id="searchInput"
            type="text"
            placeholder="Search products..."
            class="border rounded-xl px-3 py-2 text-sm focus:outline-none focus:ring focus:ring-slate-300"
          />
        </div>

        <!-- Category Filter -->
        <div class="flex flex-col gap-1">
          <label for="categoryFilter" class="text-sm font-medium">Category</label>
          <select
            id="categoryFilter"
            class="border rounded-xl px-3 py-2 text-sm focus:outline-none focus:ring focus:ring-slate-300"
          >
            <option value="all">All</option>
            <option value="electronics">Electronics</option>
            <option value="fashion">Fashion</option>
            <option value="books">Books</option>
            <option value="home">Home & Kitchen</option>
          </select>
        </div>

        <!-- Price Filter -->
        <div class="flex flex-col gap-1">
          <label for="priceFilter" class="text-sm font-medium">Price Range</label>
          <select
            id="priceFilter"
            class="border rounded-xl px-3 py-2 text-sm focus:outline-none focus:ring focus:ring-slate-300"
          >
            <option value="all">All</option>
            <option value="low">₹0 - ₹999</option>
            <option value="mid">₹1000 - ₹4999</option>
            <option value="high">₹5000 & above</option>
          </select>
        </div>

        <!-- Sort -->
        <div class="flex flex-col gap-1">
          <label for="sortSelect" class="text-sm font-medium">Sort By</label>
          <select
            id="sortSelect"
            class="border rounded-xl px-3 py-2 text-sm focus:outline-none focus:ring focus:ring-slate-300"
          >
            <option value="default">Default</option>
            <option value="price-asc">Price: Low to High</option>
            <option value="price-desc">Price: High to Low</option>
          </select>
        </div>
      </div>
    </section>

    <!-- Products Section -->
    <section>
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-semibold">Products</h2>
        <p id="resultCount" class="text-sm text-slate-600"></p>
      </div>

      <div
        id="productGrid"
        class="grid gap-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4"
      >
        <!-- JS will inject product cards here -->
      </div>
    </section>
  </main>

  <!-- Footer -->
  <footer class="mt-8 border-t bg-white">
    <div class="max-w-6xl mx-auto px-4 py-4 text-xs text-slate-500 flex flex-wrap gap-2 justify-between">
      <span>Made for SDLC • DOM Manipulation • Version Control (GitHub)</span>
      <span>©️ 2025 MyShop</span>
    </div>
  </footer>

  <!-- JavaScript Logic -->
  <script>
    // 1. Product data (in real project this may come from database / API)
    const products = [
      {
        id: 1,
        name: "Wireless Earbuds",
        category: "electronics",
        price: 1499,
        description: "Bluetooth earbuds with noise cancellation.",
      },
      {
        id: 2,
        name: "Smartphone",
        category: "electronics",
        price: 12999,
        description: "4G smartphone with 6.5-inch display.",
      },
      {
        id: 3,
        name: "Cotton T-Shirt",
        category: "fashion",
        price: 499,
        description: "Comfortable unisex cotton T-shirt.",
      },
      {
        id: 4,
        name: "Jeans",
        category: "fashion",
        price: 999,
        description: "Slim fit blue denim jeans.",
      },
      {
        id: 5,
        name: "Java Programming Book",
        category: "books",
        price: 699,
        description: "Beginner to advanced Java concepts.",
      },
      {
        id: 6,
        name: "UI/UX Design Guide",
        category: "books",
        price: 899,
        description: "Basics of UI and UX design principles.",
      },
      {
        id: 7,
        name: "Non-stick Pan",
        category: "home",
        price: 1199,
        description: "Durable non-stick frying pan.",
      },
      {
        id: 8,
        name: "LED Table Lamp",
        category: "home",
        price: 799,
        description: "Study lamp with adjustable brightness.",
      },
    ];

    // 2. Get DOM elements
    const productGrid = document.getElementById("productGrid");
    const resultCount = document.getElementById("resultCount");
    const searchInput = document.getElementById("searchInput");
    const categoryFilter = document.getElementById("categoryFilter");
    const priceFilter = document.getElementById("priceFilter");
    const sortSelect = document.getElementById("sortSelect");

    // 3. Render product cards
    function renderProducts(productList) {
      productGrid.innerHTML = ""; // Clear grid

      if (productList.length === 0) {
        productGrid.innerHTML =
          '<p class="col-span-full text-center text-slate-500 text-sm">No products found. Try changing filters.</p>';
        resultCount.textContent = "0 products found";
        return;
      }

      productList.forEach((product) => {
        const card = document.createElement("article");
        card.className =
          "bg-white rounded-2xl shadow-sm border hover:shadow-md transition p-3 flex flex-col";

        card.innerHTML = `
          <div class="h-32 bg-slate-100 rounded-xl mb-3 flex items-center justify-center text-xs text-slate-400">
            Image Placeholder
          </div>
          <h3 class="font-semibold text-sm mb-1">${product.name}</h3>
          <p class="text-xs text-slate-500 mb-2 capitalize">${product.category}</p>
          <p class="text-xs text-slate-600 mb-3">${product.description}</p>
          <div class="mt-auto flex items-center justify-between">
            <span class="font-bold text-sm">₹${product.price}</span>
            <button class="text-xs px-3 py-1 rounded-full border border-slate-300 hover:bg-slate-100">
              Add to Cart
            </button>
          </div>
        `;

        productGrid.appendChild(card);
      });

      resultCount.textContent = productList.length + " products found";
    }

    // 4. Filter function (multi-level filters + search + sort)
    function applyFilters() {
      const searchText = searchInput.value.trim().toLowerCase();
      const selectedCategory = categoryFilter.value;
      const selectedPrice = priceFilter.value;
      const selectedSort = sortSelect.value;

      // Step 1: Filter by search + category + price
      let filtered = products.filter((product) => {
        // Search filter
        const matchesSearch =
          product.name.toLowerCase().includes(searchText) ||
          product.description.toLowerCase().includes(searchText);

        // Category filter
        const matchesCategory =
          selectedCategory === "all" || product.category === selectedCategory;

        // Price filter
        let matchesPrice = true;
        if (selectedPrice === "low") {
          matchesPrice = product.price >= 0 && product.price <= 999;
        } else if (selectedPrice === "mid") {
          matchesPrice = product.price >= 1000 && product.price <= 4999;
        } else if (selectedPrice === "high") {
          matchesPrice = product.price >= 5000;
        }

        return matchesSearch && matchesCategory && matchesPrice;
      });

      // Step 2: Sort
      if (selectedSort === "price-asc") {
        filtered.sort((a, b) => a.price - b.price);
      } else if (selectedSort === "price-desc") {
        filtered.sort((a, b) => b.price - a.price);
      }
      // "default" -> no sorting (original order)

      // Step 3: Render
      renderProducts(filtered);
    }

    // 5. Attach event listeners (DOM manipulation)
    searchInput.addEventListener("input", applyFilters);
    categoryFilter.addEventListener("change", applyFilters);
    priceFilter.addEventListener("change", applyFilters);
    sortSelect.addEventListener("change", applyFilters);

    // 6. Initial render
    renderProducts(products);
  </script>
</body>
</html>
