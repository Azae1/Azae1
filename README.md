$sql = "SELECT DISTINCT * FROM productos";
$stmt = $conexion->prepare($sql);
$stmt->execute();
$productos = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>
<!DOCTYPE html>
<html lang="es">
<head>
<link rel="stylesheet" href="styles.css">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Carrito de compras</title>
  <!-- Enlace a los estilos CSS -->

</head>
<body>
  <header>
    <h1>Carrito de compras</h1>
  </header>

  <main>
    <div class="productos">
      <h2>Lista de productos</h2>
      <ul>
        <?php foreach ($productos as $producto): ?>
          <li>
            <span><?php echo $producto['nombre']; ?></span>
            <span><?php echo $producto['precio']; ?> USD</span>
            <button onclick="agregarAlCarrito(<?php echo $producto['id']; ?>)">Agregar al carrito</button>
          </li>
        <?php endforeach; ?>
      </ul>
    </div>
     <!-- Carrito de compras -->
     <div class="carrito">
      <h2>Carrito de compras</h2>
      <ul id="carritoContainer"></ul>
      <p>Total: <span id="totalElement">0.00</span> USD</p>
      <button id="vaciarCarrito" onclick="vaciarCarrito()">Vaciar carrito</button>
    </div>

    
  </main>
  
  <script>let carrito = [];

function agregarAlCarrito(id) {
    const productoEncontrado = productos.find((producto) => producto.id === id);
    if (productoEncontrado) {
      carrito.push(productoEncontrado);
      actualizarCarrito();
    }
  }
  function actualizarCarrito() {
  carritoContainer.innerHTML = '';
  let total = 0;

  carrito.forEach((producto) => {
    const productoElement = document.createElement('li');
    productoElement.innerHTML = `
      ${producto.nombre} - ${producto.precio} USD
    `;
    carritoContainer.appendChild(productoElement);
    total += producto.precio;
  });

  totalElement.textContent = total.toFixed(2); // Redondeamos el total a 2 decimales
}
// Función para vaciar el carrito
function vaciarCarrito() {
  carrito.length = 0;
  actualizarCarrito();
}

  </script>
</body>
</html>
![Uploading image.png…]()
