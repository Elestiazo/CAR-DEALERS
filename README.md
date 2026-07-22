# CAR-DEALERS
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CAR DEALERS</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>🚗 CAR DEALERS 🚗</h1>
    <p>Brand New & Luxury Cars – Prices in Ghana Cedis</p>
  </header>

  <section class="cars">
    <h2>Available Cars</h2>
    <div class="car-card">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/6e/Lamborghini_Aventador.jpg" alt="Lamborghini">
      <h3>Lamborghini Aventador</h3>
      <p>₵2,500,000</p>
    </div>
    <div class="car-card">
      <img src="https://upload.wikimedia.org/wikipedia/commons/2/2e/Ferrari_488_GT3.jpg" alt="Ferrari">
      <h3>Ferrari 488 GT3</h3>
      <p>₵2,200,000</p>
    </div>
    <div class="car-card">
      <img src="https://upload.wikimedia.org/wikipedia/commons/3/3d/BMW_M8.jpg" alt="BMW">
      <h3>BMW M8</h3>
      <p>₵950,000</p>
    </div>
    <div class="car-card">
      <img src="https://upload.wikimedia.org/wikipedia/commons/4/4e/Toyota_Supra.jpg" alt="Toyota">
      <h3>Toyota Supra</h3>
      <p>₵600,000</p>
    </div>
    <!-- Add more cars like Dodge, Opel, Nissan, Honda, Hyundai, Citroën, Devil 16 -->
  </section>

  <section class="order-form">
    <h2>Place Your Delivery Order</h2>
    <form id="deliveryForm">
      <label for="name">Full Name:</label>
      <input type="text" id="name" required>

      <label for="phone">Phone Number:</label>
      <input type="tel" id="phone" required>

      <label for="car">Select Car:</label>
      <select id="car" required>
        <option value="Lamborghini Aventador">Lamborghini Aventador</option>
        <option value="Ferrari 488 GT3">Ferrari 488 GT3</option>
        <option value="BMW M8">BMW M8</option>
        <option value="Toyota Supra">Toyota Supra</option>
      </select>

      <label for="address">Delivery Address:</label>
      <textarea id="address" required></textarea>

      <button type="submit">Submit Order</button>
    </form>
    <p id="confirmation"></p>
  </section>

  <footer>
    <p>© 2026 CAR DEALERS | Luxury Cars in Ghana</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: 'Impact', 'Segoe UI', Arial, sans-serif;
  margin: 0;
  background: linear-gradient(to right, #ff0000, #000000, #ffcc00);
  color: #333;
}

header {
  text-align: center;
  padding: 30px;
  background: #111;
  color: #fff;
}

header h1 {
  font-size: 4em;
  color: #ffcc00;
  text-shadow: 3px 3px #ff0000;
}

header p {
  font-size: 1.3em;
  margin-top: 10px;
  color: #00ccff;
}

.cars {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 30px;
}

.car-card {
  background: #fff;
  margin: 15px;
  padding: 20px;
  border-radius: 15px;
  width: 300px;
  text-align: center;
  box-shadow: 0 6px 12px rgba(0,0,0,0.25);
  transition: transform 0.3s ease;
}

.car-card:hover {
  transform: scale(1.05);
  background: linear-gradient(to bottom, #ffcc00, #ff0000);
  color: #fff;
}

.car-card img {
  width: 100%;
  border-radius: 10px;
}

.order-form {
  background: #fff;
  margin: 30px;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 6px 12px rgba(0,0,0,0.25);
}

.order-form h2 {
  text-align: center;
  color: #ff0000;
}

form label {
  display: block;
  margin-top: 12px;
  font-weight: bold;
}

form input, form select, form textarea {
  width: 100%;
  padding: 10px;
  margin-top: 6px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

button {
  margin-top: 20px;
  padding: 12px;
  background: #00ccff;
  color: #fff;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1.1em;
  font-weight: bold;
}

button:hover {
  background: #0099cc;
}

#confirmation {
  margin-top: 15px;
  font-size: 1.1em;
  color: green;
  text-align: center;
}

footer {
  text-align: center;
  padding: 20px;
  background: #111;
  color: #fff;
}
document.addEventListener("DOMContentLoaded", function() {
  
  const form = document.getElementById("deliveryForm");
  const confirmation = document.getElementById("confirmation");

  let orders = JSON.parse(localStorage.getItem("orders")) || [];

  form.addEventListener("submit", function(event) {
    event.preventDefault();

    const name = document.getElementById("name").value.trim();
    const phone = document.getElementById("phone").value.trim();
    const car = document.getElementById("car").value;
    const address = document.getElementById("address").value.trim();

    if (!name || !phone || !car || !address) {
      confirmation.style.color = "red";
      confirmation.innerText = "⚠️ Please fill in all fields.";
      return;
    }

    const newOrder = {
      customerName: name,
      phoneNumber: phone,
      carModel: car,
      deliveryAddress: address,
      orderDate: new Date().toLocaleString()
    };

    orders.push(newOrder);
    localStorage.setItem("orders", JSON.stringify(orders));

    confirmation.style.color = "green";
    confirmation.innerText = 
      `✅ Thank you, ${name}! Your order for ${car} has been received. 
      Delivery to: ${address}. 
      We will contact you at ${phone}.`;

    form.reset();
  });

  console.log("All Orders:", orders);
});
