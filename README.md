<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BloomPods – Fraser Valley Hobby Greenhouse Rentals</title>

<style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: Arial, sans-serif; }
    body { background: #f9f9f9; color: #333; }
    .navbar { display: flex; justify-content: space-between; padding: 20px 40px; background: #2e6f45; color: white; }
    .navbar .logo { font-size: 26px; font-weight: bold; }
    .nav-links { list-style: none; display: flex; gap: 20px; }
    .nav-links a { color: white; text-decoration: none; font-weight: bold; }
    .hero { background: url('https://via.placeholder.com/1400x600?text=Fraser+Valley+Greenhouses') center/cover no-repeat; padding: 150px 40px; color: white; text-shadow: 2px 2px 6px black; }
    .hero h1 { font-size: 48px; }
    .btn { display: inline-block; padding: 10px 20px; background: #2e6f45; color: white; text-decoration: none; border-radius: 5px; margin-top: 20px; cursor: pointer; }
    .section { padding: 60px 40px; text-align: center; }
    .light { background: #eef6f0; }
    .pod-container { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; }
    .pod-card { background: white; width: 300px; padding: 20px; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
    .price { font-size: 22px; font-weight: bold; color: #2e6f45; margin-top: 10px; }
    .form-popup { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.5); justify-content:center; align-items:center; z-index:999; }
    .form-container { background:white; padding:20px; width:320px; border-radius:10px; text-align:left; }
    .form-container input, .form-container select, .form-container textarea { width:100%; padding:10px; margin:8px 0; border:1px solid #ccc; border-radius:5px; }
    #paypal-button-container { margin-top: 15px; }
    .btn.cancel { background: #777; }
    footer { margin-top: 40px; padding: 20px; background: #2e6f45; color: white; text-align: center; }
</style>
</head>

<body>

<nav class="navbar">
    <div class="logo">BloomPods – Fraser Valley</div>
    <ul class="nav-links">
        <li><a href="#pods">Pods</a></li>
        <li><a href="#pricing">Pricing</a></li>
    </ul>
</nav>

<div class="hero">
    <h1>Rent Your Own Greenhouse Pod in the Fraser Valley</h1>
    <p>Grow fresh plants year-round in a private hobby greenhouse pod.</p>
    <button class="btn" onclick="openForm()">Book a Pod</button>
</div>

<section id="pods" class="section">
    <h2>Choose Your Greenhouse Pod</h2>
    <div class="pod-container">
        <div class="pod-card">
            <h3>Mini Pod</h3>
            <p>Perfect for herbs, succulents & starter plants.</p>
            <div class="price">$80/mo</div>
        </div>
        <div class="pod-card">
            <h3>Standard Pod</h3>
            <p>Great for veggies, flowers & orchids.</p>
            <div class="price">$140/mo</div>
        </div>
        <div class="pod-card">
            <h3>Premium Pod</h3>
            <p>Large greenhouse for serious hobby growers.</p>
            <div class="price">$200/mo</div>
        </div>
    </div>
</section>

<section id="pricing" class="section light">
    <h2>Simple Monthly Pricing</h2>
    <p>All located in the beautiful Fraser Valley, BC.</p>
</section>

<div id="bookingForm" class="form-popup">
    <div class="form-container">
        <h2>Book a Pod</h2>
        <label>Your Name</label>
        <input id="name" placeholder="Enter your name">
        <label>Your Email</label>
        <input id="email" placeholder="Enter your email">
        <label>Select Pod</label>
        <select id="podType">
            <option value="80">Mini Pod - $80/mo</option>
            <option value="140">Standard Pod - $140/mo</option>
            <option value="200">Premium Pod - $200/mo</option>
        </select>
        <label>Start Date</label>
        <input type="date" id="date">
        <label>Notes (optional)</label>
        <textarea id="message" placeholder="Add any notes…"></textarea>
        <h3>Complete Payment</h3>
        <div id="paypal-button-container"></div>
        <button class="btn cancel" onclick="closeForm()">Cancel</button>
    </div>
</div>

<footer>
    © 2025 BloomPods – Fraser Valley Hobby Greenhouse Rentals
</footer>

<script src="https://www.paypal.com/sdk/js?client-id=AR46mMp0GLrwditJeBF2LuMJpVVY34P2TT_GJq_QPB2id0EOADzClduLs15WPOWkN6GOYu4eCfwORzpS&currency=CAD&enable-funding=card"></script>

<script>
function openForm() { document.getElementById("bookingForm").style.display = "flex"; }
function closeForm() { document.getElementById("bookingForm").style.display = "none"; }

paypal.Buttons({
    style: { color: 'green', shape: 'rect', label: 'pay', layout: 'vertical' },
    funding: { allowed: [ paypal.FUNDING.CARD, paypal.FUNDING.PAYPAL ] },

    createOrder: function(data, actions) {
        const amount = document.getElementById("podType").value;
        return actions.order.create({ purchase_units: [{ amount: { value: amount } }] });
    },

    onApprove: function(data, actions) {
        return actions.order.capture().then(function(details) {
            alert(
                "Payment received! 🎉\n\n" +
                "Thank you, " + document.getElementById("name").value +
                ". Your greenhouse pod is now booked."
            );
            closeForm();
        });
    }

}).render('#paypal-button-container');
</script>

</body>
</html>

