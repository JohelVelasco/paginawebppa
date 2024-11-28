# paginawebppa
ppa 


<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tienda de Camisas</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f9f9f9;
      color: #333;
    }
    header {
      background-color: #007BFF;
      color: white;
      padding: 10px 20px;
      text-align: center;
    }
    .container {
      padding: 20px;
    }
    .product {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
      margin-bottom: 10px;
      border: 1px solid #ddd;
      background-color: #fff;
      border-radius: 5px;
    }
    .product button {
      background-color: #007BFF;
      color: white;
      border: none;
      padding: 10px;
      border-radius: 5px;
      cursor: pointer;
    }
    .product button:hover {
      background-color: #0056b3;
    }
    .cart {
      margin-top: 20px;
      padding: 10px;
      border: 1px solid #ddd;
      background-color: #fff;
      border-radius: 5px;
    }
    .cart-item {
      display: flex;
      justify-content: space-between;
      padding: 5px 0;
    }
  </style>
</head>
<body>
  <header>
    <h1>Tienda de Camisas</h1>
  </header>
  <div class="container">
    <div id="products">
      <!-- Los productos se generarán aquí con JavaScript -->
    </div>
    <div class="cart">
      <h2>Carrito de Compras</h2>
      <div id="cart-items">
        <p>El carrito está vacío.</p>
      </div>
      <p><strong>Total:</strong> $<span id="total">0.00</span></p>
    </div>
  </div>

  <script>
    const products = [
      { id: 1, name: "Camisa Blanca", price: 20.0 },
      { id: 2, name: "Camisa Negra", price: 25.0 },
      { id: 3, name: "Camisa Azul", price: 22.0 },
    ];

    const cart = [];

    function displayProducts() {
      const productsDiv = document.getElementById("products");
      products.forEach(product => {
        const productDiv = document.createElement("div");
        productDiv.classList.add("product");
        productDiv.innerHTML = `
          <span>${product.name} - $${product.price.toFixed(2)}</span>
          <button onclick="addToCart(${product.id})">Agregar</button>
        `;
        productsDiv.appendChild(productDiv);
      });
    }

    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      cart.push(product);
      updateCart();
    }

    function updateCart() {
      const cartItemsDiv = document.getElementById("cart-items");
      cartItemsDiv.innerHTML = "";
      let total = 0;

      if (cart.length === 0) {
        cartItemsDiv.innerHTML = "<p>El carrito está vacío.</p>";
      } else {
        cart.forEach(item => {
          const cartItemDiv = document.createElement("div");
          cartItemDiv.classList.add("cart-item");
          cartItemDiv.innerHTML = `
            <span>${item.name}</span>
            <span>$${item.price.toFixed(2)}</span>
          `;
          cartItemsDiv.appendChild(cartItemDiv);
          total += item.price;
        });
      }

      document.getElementById("total").textContent = total.toFixed(2);
    }

    // Inicializar la página
    displayProducts();
  </script>
</body>
</html>
