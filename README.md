# paginawebppa


<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tienda de Camisas - Colombia</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #eef2f5;
      color: #333;
    }

    header {
      background: linear-gradient(45deg, #004aad, #007bff);
      color: white;
      padding: 20px;
      text-align: center;
    }

    header h1 {
      margin: 0;
      font-size: 2.5em;
    }

    header p {
      margin: 5px 0;
    }

    .container {
      max-width: 1200px;
      margin: 20px auto;
      padding: 0 15px;
    }

    .products, .cart {
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      padding: 20px;
      margin-bottom: 20px;
      overflow: hidden;
    }

    .products h2, .cart h2 {
      margin-top: 0;
    }

    .product {
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid #ddd;
      padding: 10px 0;
    }

    .product img {
      width: 80px;
      height: 80px;
      border-radius: 8px;
      margin-right: 10px;
      transition: transform 0.3s;
    }

    .product img:hover {
      transform: scale(1.1);
    }

    .product-details {
      flex-grow: 1;
    }

    .product button {
      background-color: #004aad;
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .product button:hover {
      background-color: #003580;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 0;
    }

    .cart-item button {
      background-color: #e63946;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 5px;
      cursor: pointer;
    }

    .cart-item button:hover {
      background-color: #c92a33;
    }

    .cart-summary {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
      font-weight: bold;
    }

    .cart-summary span {
      font-size: 1.2em;
    }

    .empty-cart {
      text-align: center;
      font-style: italic;
      color: #666;
    }
  </style>
</head>
<body>
  <header>
    <h1>Tienda de Camisas</h1>
    <p>¡Las mejores camisas en Colombia!</p>
  </header>

  <div class="container">
    <div class="products">
      <h2>Catálogo de Productos</h2>
      <div id="products">
        <!-- Productos generados dinámicamente -->
      </div>
    </div>
    <div class="cart">
      <h2>Carrito de Compras</h2>
      <div id="cart-items" class="empty-cart">
        Tu carrito está vacío.
      </div>
      <div class="cart-summary">
        <span>Total: $<span id="total">0</span> COP</span>
        <span>Productos: <span id="item-count">0</span></span>
      </div>
    </div>
  </div>

  <script>
    const products = [
      { id: 1, name: "Camisa Blanca", price: 50000, image: "https://via.placeholder.com/80/ffffff/000000?text=Blanca" },
      { id: 2, name: "Camisa Negra", price: 60000, image: "https://via.placeholder.com/80/000000/ffffff?text=Negra" },
      { id: 3, name: "Camisa Azul", price: 55000, image: "https://via.placeholder.com/80/0000ff/ffffff?text=Azul" },
      { id: 4, name: "Camisa Roja", price: 52000, image: "https://via.placeholder.com/80/ff0000/ffffff?text=Roja" },
    ];

    let cart = [];

    function displayProducts() {
      const productsDiv = document.getElementById("products");
      productsDiv.innerHTML = ""; // Limpiar productos existentes
      products.forEach(product => {
        const productDiv = document.createElement("div");
        productDiv.classList.add("product");
        productDiv.innerHTML = `
          <img src="${product.image}" alt="${product.name}">
          <div class="product-details">
            <h4>${product.name}</h4>
            <p>$${product.price.toLocaleString()} COP</p>
          </div>
          <button onclick="addToCart(${product.id})">Agregar al carrito</button>
        `;
        productsDiv.appendChild(productDiv);
      });
    }

    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      cart.push(product);
      updateCart();
    }

    function removeFromCart(index) {
      cart.splice(index, 1);
      updateCart();
    }

    function updateCart() {
      const cartItemsDiv = document.getElementById("cart-items");
      const itemCount = document.getElementById("item-count");
      const totalDiv = document.getElementById("total");
      cartItemsDiv.innerHTML = ""; // Limpiar carrito

      let total = 0;

      if (cart.length === 0) {
        cartItemsDiv.classList.add("empty-cart");
        cartItemsDiv.innerHTML = "Tu carrito está vacío.";
        itemCount.textContent = 0;
        totalDiv.textContent = "0";
        return;
      }

      cartItemsDiv.classList.remove("empty-cart");

      cart.forEach((item, index) => {
        const cartItemDiv = document.createElement("div");
        cartItemDiv.classList.add("cart-item");
        cartItemDiv.innerHTML = `
          <span>${item.name} - $${item.price.toLocaleString()} COP</span>
          <button onclick="removeFromCart(${index})">Eliminar</button>
        `;
        cartItemsDiv.appendChild(cartItemDiv);
        total += item.price;
      });

      itemCount.textContent = cart.length;
      totalDiv.textContent = total.toLocaleString();
    }

    // Inicializar
    displayProducts();
  </script>
</body>
</html>
