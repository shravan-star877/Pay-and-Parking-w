<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🚗 Pay & Park - Smart Booking</title>
  <style>
    body {
      margin: 0;
      font-family: 'Arial', sans-serif;
      background-color: #f0f8ff;
    }
    h2, h3 { color: #333; }

    /* ===================== LOGIN PAGE ===================== */
    .login-container {
      position: relative;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      overflow: hidden;
    }
    .bg-slideshow {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background-size: cover;
      background-position: center;
      animation: slideShow 25s infinite;
      z-index: -2;
    }
    @keyframes slideShow {
      0% {background-image: url('https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=1600&q=80');}
      25% {background-image: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1600&q=80');}
      50% {background-image: url('https://images.unsplash.com/photo-1502877338535-766e1452684a?auto=format&fit=crop&w=1600&q=80');}
      75% {background-image: url('https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=1600&q=80');}
      100% {background-image: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1600&q=80');}
    }
    .login-overlay {
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.5));
      backdrop-filter: blur(4px);
      z-index: -1;
    }
    .login-card {
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(14px);
      padding: 35px 25px;
      border-radius: 20px;
      width: 330px;
      text-align: center;
      color: white;
      box-shadow: 0 8px 25px rgba(0,0,0,0.4);
      animation: fadeIn 1.2s ease-in-out;
    }
    .login-card h2 {margin-bottom: 10px; font-size: 24px;}
    .login-card .subtitle {font-size: 14px; margin-bottom: 20px; color: #ddd;}
    .input-group {
      display: flex; align-items: center;
      background: rgba(255,255,255,0.2);
      border-radius: 8px;
      padding: 10px; margin-bottom: 15px;
    }
    .input-group span {font-size: 18px; margin-right: 8px;}
    .input-group input {
      border: none; outline: none; background: transparent;
      flex: 1; font-size: 14px; color: white;
    }
    .input-group input::placeholder {color: #eee;}
    input[type="submit"], input[type="reset"] {
      padding: 12px; width: 48%; margin: 5px 1%;
      border: none; border-radius: 8px; cursor: pointer; font-size: 15px;
      transition: 0.3s; color: white;
    }
    input[type="submit"] {background: linear-gradient(135deg, #4CAF50, #2196F3);}
    input[type="submit"]:hover {transform: scale(1.05);}
    input[type="reset"] {background: rgba(255,255,255,0.3);}
    input[type="reset"]:hover {background: rgba(255,255,255,0.5);transform: scale(1.05);}
    @keyframes fadeIn {from {opacity: 0;transform: translateY(-20px);}to {opacity: 1;transform: translateY(0);}}

    /* ===================== HEADER ===================== */
    .parking-header {
      background: linear-gradient(135deg, #2196F3, #4CAF50);
      color: white;
      text-align: center;
      padding: 30px 10px;
      border-bottom-left-radius: 50px;
      border-bottom-right-radius: 50px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      position: relative;
    }
    .header-buttons {
      position: absolute;
      top: 20px;
      right: 20px;
      display: flex;
      gap: 10px;
    }
    .header-buttons button {
      padding: 8px 12px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 14px;
      color: white;
    }
    .back-btn {background-color: #ff9800;}
    .logout-btn {background-color: #e53935;}
    .back-btn:hover {background-color: #f57c00;}
    .logout-btn:hover {background-color: #c62828;}

    /* ===================== PARKING CARDS ===================== */
    .parking-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
      padding: 30px;
      max-width: 1000px;
      margin: 0 auto;
    }
    .parking-card {
      background-color: white;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      cursor: pointer;
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .parking-card:hover {transform: translateY(-8px); box-shadow: 0 10px 15px rgba(0,0,0,0.3);}
    .parking-card img {width: 100%; height: 180px; object-fit: cover;}
    .parking-card .info {padding: 15px; text-align: left;}
    .parking-card .info h3 {margin: 0 0 8px; color: #4CAF50;}
    .parking-card .info p {margin: 4px 0; color: #555; font-size: 14px;}

    /* ===================== SLOTS PAGE ===================== */
    .slots-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
      gap: 10px;
      padding: 20px;
      max-width: 900px;
      margin: 20px auto;
    }
    .slot {
      background-color: #fff;
      border-radius: 8px;
      padding: 15px 0;
      text-align: center;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      cursor: pointer;
      transition: 0.3s;
      font-weight: bold;
    }
    .slot:hover {background-color: #e3f2fd;}
    .slot.booked {background-color: #ff5252; color: white;}
    .slot.booked:hover {background-color: #e53935;}

    /* ===================== MODAL ===================== */
    .modal {
      display: none; /* ✅ FIXED: modal hidden by default */
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.6);
      align-items: center;
      justify-content: center;
      z-index: 10;
    }
    .modal-content {
      background: white;
      padding: 25px;
      border-radius: 10px;
      width: 300px;
      text-align: center;
      position: relative;
    }
    .modal-content input {
      width: 90%;
      padding: 8px;
      margin: 8px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .modal-content button {
      padding: 10px 15px;
      margin-top: 10px;
      border: none;
      background: linear-gradient(135deg, #4CAF50, #2196F3);
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
    .modal-content .close-btn {
      background: #999;
      position: absolute;
      top: 10px; right: 10px;
      padding: 5px 10px;
      border: none;
      color: white;
      border-radius: 4px;
      cursor: pointer;
    }

    /* ===================== FOOTER ===================== */
    footer {
      text-align: center;
      background: #eee;
      padding: 10px;
      color: #444;
      font-size: 14px;
    }

    /* ===================== RESPONSIVE ===================== */
    @media (max-width: 600px) {
      .login-card { width: 85%; padding: 25px; }
      .parking-card img { height: 140px; }
      .slots-grid { grid-template-columns: repeat(auto-fit, minmax(60px, 1fr)); }
    }
  </style>
</head>
<body>

<!-- ===================== LOGIN PAGE ===================== -->
<div id="loginPage" class="login-container">
  <div class="bg-slideshow"></div>
  <div class="login-overlay"></div>
  <div class="login-card">
    <h2>🚗 Pay & Park</h2>
    <p class="subtitle">Login to manage your parking easily</p>
    <form onsubmit="loginUser(event)">
      <div class="input-group">
        <span>👤</span>
        <input type="text" id="username" placeholder="Enter Username" required>
      </div>
      <div class="input-group">
        <span>🔑</span>
        <input type="password" id="password" placeholder="Enter Password" required>
      </div>
      <input type="submit" value="Login">
      <input type="reset" value="Clear">
    </form>
  </div>
</div>

<!-- ===================== LOCATION PAGE ===================== -->
<div id="parkingPage" style="display: none;">
  <div class="parking-header">
    <h2>Welcome, <span id="currentUser"></span> 👋</h2>
    <div class="header-buttons">
      <button class="logout-btn" onclick="logout()">Logout</button>
    </div>
    <p>Select a Pay & Park location to book your slot.</p>
  </div>
  <div class="parking-grid">
    <div class="parking-card" onclick="openSlots('Bindu Chouk Pay & Park',150)">
      <img src="https://images.unsplash.com/photo-1552519507-da3b142c6e3d?auto=format&fit=crop&w=800&q=60" alt="">
      <div class="info">
        <h3>Bindu Chouk Pay & Park</h3>
        <p>📍 Near Bindu Chouk</p>
        <p>💰 ₹20 per hour</p>
      </div>
    </div>
    <div class="parking-card" onclick="openSlots('Bus Stand Parking',25)">
      <img src="https://images.unsplash.com/photo-1525609004556-c46c7d6cf023?auto=format&fit=crop&w=800&q=60" alt="">
      <div class="info">
        <h3>Bus Stand Parking</h3>
        <p>📍 Central Bus Stand</p>
        <p>💰 ₹30 for 2 hours</p>
      </div>
    </div>
    <div class="parking-card" onclick="openSlots('CBS Chamber Parking',70)">
      <img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=800&q=60" alt="">
      <div class="info">
        <h3>CBS Chamber Parking</h3>
        <p>📍 Shahupuri CBS</p>
        <p>💰 ₹40 for 3 hours</p>
      </div>
    </div>
  </div>
</div>

<!-- ===================== SLOTS PAGE ===================== -->
<div id="slotsPage" style="display: none;">
  <div class="parking-header">
    <h2 id="slotLocationName"></h2>
    <div class="header-buttons">
      <button class="back-btn" onclick="goBack()">Back</button>
      <button class="logout-btn" onclick="logout()">Logout</button>
    </div>
    <p>Click on a slot to book or unbook.</p>
  </div>
  <div id="slotsContainer" class="slots-grid"></div>
</div>

<!-- ===================== BOOKING MODAL ===================== -->
<div id="bookingModal" class="modal">
  <div class="modal-content">
    <button class="close-btn" onclick="closeBookingForm()">X</button>
    <h3>Book Slot <span id="slotNumberText"></span></h3>
    <input type="text" id="userName" placeholder="Enter Your Name" required>
    <input type="time" id="bookingTime" required>
    <input type="text" id="carNumber" placeholder="Car No. (e.g., MH123456)" required>
    <button onclick="confirmBooking()">Confirm Booking</button>
  </div>
</div>

<!-- ===================== FOOTER ===================== -->
<footer>
  © 2025 Pay & Park - Kolhapur | Smart Parking System
</footer>

<script>
  const users = {
    "Parth": "parth@123",
    "Kshitija": "kshitija@123",
    "Shravan": "shravan@123",
    "Samiksha": "Samiksha@123",
    "Arpita": "arpita@1234",
    "admin": "1234"
  };

  let currentUser = "";
  let selectedSlot = null;
  let slots = [];
  let totalSlots = 0;

  function loginUser(event) {
    event.preventDefault(); 
    let user = document.getElementById("username").value.trim();
    let pass = document.getElementById("password").value.trim();
    if(users[user] && users[user] === pass) {
      currentUser = user;
      document.getElementById("loginPage").style.display = "none";
      document.getElementById("parkingPage").style.display = "block";
      document.getElementById("currentUser").innerText = user;
    } else {
      alert("Invalid username or password!");
    }
  }

  function logout() {
    currentUser = "";
    document.getElementById("loginPage").style.display = "flex";
    document.getElementById("parkingPage").style.display = "none";
    document.getElementById("slotsPage").style.display = "none";
  }

  function goBack() {
    document.getElementById("slotsPage").style.display = "none";
    document.getElementById("parkingPage").style.display = "block";
  }

  function openSlots(locationName, slotCount) {
    totalSlots = slotCount;
    document.getElementById("parkingPage").style.display = "none";
    document.getElementById("slotsPage").style.display = "block";
    document.getElementById("slotLocationName").innerText = 🚘 ${locationName} - ${slotCount} Slots;
    slots = Array.from({ length: slotCount }, (_, i) => ({
      number: i + 1,
      booked: false,
      details: null
    }));
    renderSlots();
  }

  function renderSlots() {
    const container = document.getElementById("slotsContainer");
    container.innerHTML = "";
    slots.forEach(slot => {
      const div = document.createElement("div");
      div.classList.add("slot");
      if (slot.booked) div.classList.add("booked");
      div.textContent = slot.number;
      div.onclick = () => handleSlotClick(slot);
      container.appendChild(div);
    });
  }

  function handleSlotClick(slot) {
    if (slot.booked) {
      const confirmUnbook = confirm(Slot ${slot.number} is booked by ${slot.details.name}. Unbook it?);
      if (confirmUnbook) {
        slot.booked = false;
        slot.details = null;
        renderSlots();
        alert(Slot ${slot.number} has been unbooked ✅);
      }
    } else {
      selectedSlot = slot;
      document.getElementById("slotNumberText").textContent = #${slot.number};
      document.getElementById("bookingModal").style.display = "flex";
    }
  }

  function closeBookingForm() {
    document.getElementById("bookingModal").style.display = "none";
    document.getElementById("userName").value = "";
    document.getElementById("bookingTime").value = "";
    document.getElementById("carNumber").value = "";
  }

  function confirmBooking() {
    const name = document.getElementById("userName").value.trim();
    const time = document.getElementById("bookingTime").value.trim();
    const carNo = document.getElementById("carNumber").value.trim();
    const carPattern = /^[A-Za-z]{2}\d{6}$/;
    if (!name || !time || !carNo) {
      alert("Please fill all fields!");
      return;
    }
    if (!carPattern.test(carNo)) {
      alert("Invalid Car Number! Use 2 letters followed by 6 digits. Example: MH123456");
      return;
    }
