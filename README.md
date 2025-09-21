# cleakawash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cleaka - Mobile Car Wash</title>
  <style>
    body {
      margin: 0;
      font-family: "Segoe UI", sans-serif;
      scroll-behavior: smooth;
      background: #fff;
      color: #111;
    }
    .container {
      max-width: 1100px;
      margin: auto;
    }
    h2 {
      text-align: center;
      margin-bottom: 40px;
    }

    /* Top Options Button */
    .top-options {
      position: fixed;
      top: 15px;
      right: 20px;
      z-index: 1000;
      background: #333;
      color: #fff;
      padding: 10px 20px;
      border-radius: 6px;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    .top-options:hover { background: #666; }

    /* Options Menu */
    .menu {
      position: fixed;
      top: 60px;
      right: 20px;
      background: #111;
      color: #fff;
      padding: 15px;
      border-radius: 8px;
      display: none;
      flex-direction: column;
      gap: 10px;
      z-index: 999;
    }
    .menu a {
      color: #fff;
      text-decoration: none;
      padding: 8px 12px;
      border-radius: 6px;
      transition: background 0.3s;
    }
    .menu a:hover {
      background: #333;
    }
    .menu.show { display: flex; }

    /* Hero Section */
    .hero {
      background: url('professional-washer-blue-uniform-washing-luxury-car-with-water-gun-open-air-car-wash.jpg') center/cover no-repeat;
      color: #000000;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      text-align: center;
      overflow: hidden;
      position: relative;
    }
    .hero h1 {
      font-size: 3rem;
      margin-bottom: 10px;
      opacity: 0;
      animation: fadeInDown 1s ease forwards;
      text-shadow: 2px 2px 6px rgba(0,0,0,0.6);
    }
    .hero p {
      font-size: 1.2rem;
      margin-bottom: 20px;
      opacity: 0;
      animation: fadeInUp 1.2s ease forwards;
      text-shadow: 1px 1px 4px rgba(0,0,0,0.5);
    }
    .hero .btn {
      background: #666;
      color: #fff;
      padding: 12px 24px;
      border-radius: 6px;
      text-decoration: none;
      font-weight: 600;
      opacity: 0;
      transform: scale(0.9);
      animation: fadeInUp 1.5s ease forwards;
      transition: all 0.3s ease;
      margin: 5px;
    }
    .hero .btn:hover {
      background: #fff;
      color: #000;
      transform: scale(1.05);
    }

    /* Story Section */
    .story {
      background: #fff;
      padding: 80px 20px;
      text-align: center;
      opacity: 0;
      transform: translateY(30px);
      transition: all 0.8s ease-out;
    }
    .story.visible { opacity: 1; transform: translateY(0); }
    .story h2 { font-size: 2rem; color: #000; }
    .story p { max-width: 700px; margin: 0 auto; font-size: 1.1rem; line-height: 1.6; color: #333; }

    /* Services Section */
    .services { 
      background: #222222;
      padding: 80px 20px; 
      text-align: center; 
      opacity:0; 
      transform:translateY(30px); 
      transition:0.8s; 
      color:#ffffff;
    }
    .services.visible { opacity:1; transform:translateY(0); }
    .services-grid { 
      display:grid; 
      grid-template-columns:repeat(auto-fit, minmax(250px, 1fr)); 
      gap:20px; 
    }
    .service-card {
      position: relative;
      height: 250px;
      border-radius: 12px;
      overflow: hidden;
      cursor: pointer;
      perspective: 1000px;
    }
    .service-inner {
      position: absolute;
      width: 100%;
      height: 100%;
      transition: transform 0.6s;
      transform-style: preserve-3d;
    }
    .service-card:hover .service-inner,
    .service-card.active .service-inner {
      transform: rotateY(180deg);
    }
    .service-front, .service-back {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      font-size: 1.2rem;
      padding: 20px;
      text-align: center;
    }
    .service-front {
      background-size: cover;
      background-position: center;
    }
    .service-front h3 {
      background: rgba(0,0,0,0.6);
      padding: 10px 15px;
      border-radius: 6px;
    }
    .service-back {
      background: #222;
      transform: rotateY(180deg);
      flex-direction: column;
    }
    .service-back h3 {
      margin-bottom: 10px;
    }
    .service-back span {
      font-size: 1.5rem;
      font-weight: bold;
      color: #25D366;
    }

    /* Showcase */
    .showcase { padding:80px 20px; background:#fff; text-align:center; }
    .showcase-grid {
      display:grid; grid-template-columns:repeat(auto-fit, minmax(250px,1fr)); gap:20px;
    }
    .showcase-grid img {
      width:100%; border-radius:10px; cursor:pointer;
      transition: transform 0.3s ease;
    }
    .showcase-grid img:hover { transform: scale(1.05); }

    /* Lightbox */
    .lightbox {
      position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.8);
      display:none; align-items:center; justify-content:center; z-index:999;
    }
    .lightbox img { max-width:90%; max-height:90%; border-radius:10px; }
    .lightbox:target { display:flex; }

    /* Booking */
    .booking { background:#fff; padding:60px 20px; text-align:center; }
    .booking .btn {
      background:#25D366; color:#fff; padding:15px 30px; border-radius:8px; text-decoration:none;
      font-weight:600; transition:all 0.3s ease; margin:5px; display:inline-block;
    }
    .booking .btn:hover { transform:scale(1.05); }
    .btn-instagram { background:#E1306C; }

    /* Feedback */
    .feedback { background:#f9f9f9; padding:80px 20px; text-align:center; }
    .feedback form { max-width:500px; margin:0 auto 40px auto; display:flex; flex-direction:column; gap:15px; }
    .feedback input, .feedback textarea { padding:10px; border-radius:6px; border:1px solid #ccc; font-size:1rem; }
    .feedback button { padding:12px; border-radius:6px; border:none; background:#666; color:#fff; font-weight:600; cursor:pointer; transition:0.3s; }
    .feedback button:hover { background:#000; }
    .feedback-item { background:#fff; padding:15px 20px; border-radius:6px; margin-bottom:15px; box-shadow:0 2px 4px rgba(0,0,0,0.1); display:flex; gap:15px; align-items:center; }
    .feedback-item img { width:50px; height:50px; border-radius:50%; object-fit:cover; }

    /* Footer */
    footer { background:#000; color:#fff; text-align:center; padding:20px; }
    footer a { color:#aaa; margin:0 10px; text-decoration:none; transition:0.3s; }
    footer a:hover { color:#fff; }

    /* Animations */
    @keyframes fadeInDown { from{opacity:0;transform:translateY(-30px);} to{opacity:1;transform:translateY(0);} }
    @keyframes fadeInUp { from{opacity:0;transform:translateY(30px);} to{opacity:1;transform:translateY(0);} }
  </style>
</head>
<body>

<div class="top-options" id="menu-btn">Options</div>
<div class="menu" id="menu">
  <a href="#hero">Home</a>
  <a href="#services">Services</a>
  <a href="#showcase">Showcase</a>
  <a href="#feedback">Feedback</a>
  <a href="#booking">Book Now</a>
</div>

<!-- Hero -->
<section class="hero" id="hero">
  <h1>Cleaka</h1>
  <p>We bring the shine to your ride</p>
  <a href="https://wa.me/919447947136?text=Hi+I+want+to+book+a+car+wash+with+Cleaka" class="btn">Book Now on WhatsApp</a>
</section>

<!-- Story -->
<section class="story">
  <div class="container">
    <h2>Our Story</h2>
    <p>Cleaka was founded with one mission – to make car washing simple, convenient, and eco-friendly. We bring professional cleaning to your doorstep so your car always shines without wasting your time.</p>
  </div>
</section>

<!-- Services -->
<section class="services" id="services">
  <div class="container">
    <h2>Our Packages</h2>
    <div class="services-grid">
      <div class="service-card">
        <div class="service-inner">
          <div class="service-front" style="background-image:url('man-wash-car-using-shampoo.jpg')">
            <h3>Exterior Wash</h3>
          </div>
          <div class="service-back">
            <h3>Exterior Wash</h3>
            <span>₹199</span>
            <p>Quick and spotless wash for the outside of your car.</p>
          </div>
        </div>
      </div>
      <div class="service-card">
        <div class="service-inner">
          <div class="service-front" style="background-image:url('man-polish-salon-car-garage.jpg')">
            <h3>Interior Detailing</h3>
          </div>
          <div class="service-back">
            <h3>Interior Detailing</h3>
            <span>₹399</span>
            <p>Deep cleaning for seats, dashboard, and all interiors.</p>
          </div>
        </div>
      </div>
      <div class="service-card">
        <div class="service-inner">
          <div class="service-front" style="background-image:url('close-up-car-care-washing.jpg')">
            <h3>Full Package</h3>
          </div>
          <div class="service-back">
            <h3>Full Package</h3>
            <span>₹599</span>
            <p>Complete inside-out cleaning for a showroom shine.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Showcase -->
<section class="showcase" id="showcase">
  <h2>Our Recent Works</h2>
  <div class="showcase-grid">
    <a href="#img1"><img src="car-wash-detailing-station.jpg" alt="Car Wash 1"></a>
    <a href="#img2"><img src="beautiful-car-washing-service.jpg" alt="Car Wash 2"></a>
    <a href="#img3"><img src="close-up-car-care-process.jpg" alt="Car Wash 3"></a>
    <a href="#img4"><img src="man-polish-salon-car-garage.jpg" alt="Car Wash 4"></a>
  </div>
</section>

<!-- Booking -->
<section class="booking" id="booking">
  <h2>Book Your Wash Instantly</h2>
  <a href="https://wa.me/919447947136?text=Hi+I+want+to+book+a+car+wash+with+Cleaka" class="btn">Book via WhatsApp</a>
  <a href="https://instagram.com/cleaka_mobilecarwash" target="_blank" class="btn btn-instagram">Visit our Instagram</a>
</section>

<!-- Feedback -->
<section class="feedback" id="feedback">
  <h2>Customer Feedback</h2>
  <form id="feedback-form">
    <input type="text" id="name" placeholder="Your Name" required>
    <textarea id="message" placeholder="Your Feedback" rows="4" required></textarea>
    <button type="submit">Submit Feedback</button>
  </form>
  <div class="feedback-list" id="feedback-list"></div>
</section>

<!-- Footer -->
<footer>
  <p>© 2025 Cleaka - Mobile Car Wash</p>
  <div><a href="#hero">Home</a> | <a href="#services">Services</a> | <a href="#booking">Book Now</a></div>
</footer>

<script>
  // Options menu toggle
  const menuBtn = document.getElementById("menu-btn");
  const menu = document.getElementById("menu");
  menuBtn.addEventListener("click", () => {
    menu.classList.toggle("show");
  });

  // Reveal animations
  const sections = document.querySelectorAll(".story, .services, .showcase");
  const revealSections = () => {
    const trigger = window.innerHeight * 0.85;
    sections.forEach(s => { if(s.getBoundingClientRect().top < trigger) s.classList.add("visible"); });
  };
  window.addEventListener("scroll", revealSections);
  window.addEventListener("load", revealSections);

  // Mobile flip effect (tap)
  document.querySelectorAll(".service-card").forEach(card => {
    card.addEventListener("click", () => {
      card.classList.toggle("active");
    });
  });

  // Feedback with localStorage
  const form = document.getElementById("feedback-form");
  const feedbackList = document.getElementById("feedback-list");

  const preload = [
    {name:"Amit", message:"Excellent service! My car looks brand new.", avatar:"https://randomuser.me/api/portraits/men/11.jpg"},
    {name:"Sneha", message:"Quick and professional. Highly recommended.", avatar:"https://randomuser.me/api/portraits/women/21.jpg"},
    {name:"Rahul", message:"Loved the attention to detail on interior cleaning.", avatar:"https://randomuser.me/api/portraits/men/31.jpg"}
  ];

  const loadFeedback = () => {
    let stored = JSON.parse(localStorage.getItem("cleakaFeedback")) || preload;
    localStorage.setItem("cleakaFeedback", JSON.stringify(stored));
    feedbackList.innerHTML = "";
    stored.forEach(f => {
      const div = document.createElement("div");
      div.classList.add("feedback-item");
      div.innerHTML = `<img src="${f.avatar||'https://via.placeholder.com/50'}" alt="Avatar"><div><strong>${f.name}:</strong> <p>${f.message}</p></div>`;
      feedbackList.appendChild(div);
    });
  };
  window.addEventListener("load", loadFeedback);

  form.addEventListener("submit", e => {
    e.preventDefault();
    const name = document.getElementById("name").value.trim();
    const message = document.getElementById("message").value.trim();
    if(!name||!message) return;
    let stored = JSON.parse(localStorage.getItem("cleakaFeedback")) || [];
    stored.push({name,message,avatar:"https://via.placeholder.com/50"});
    localStorage.setItem("cleakaFeedback", JSON.stringify(stored));
    const div = document.createElement("div");
    div.classList.add("feedback-item");
    div.innerHTML = `<img src="https://via.placeholder.com/50" alt="Avatar"><div><strong>${name}:</strong> <p>${message}</p></div>`;
    feedbackList.prepend(div);
    form.reset();
  });
</script>
</body>
</html>
