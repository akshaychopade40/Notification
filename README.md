<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Booking System with Notifications</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 50px;
        }
        .booking-form {
            max-width: 300px;
            margin: auto;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input, select, button {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
        }
        .notification {
            display: none;
            padding: 10px;
            margin-top: 20px;
        }
        .notification.success {
            background-color: #d4edda;
            color: #155724;
        }
        .notification.error {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
<div class="booking-form">
    <h1>Booking System</h1>
    <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" required>
    </div>
    <div class="form-group">
        <label for="phone">Phone Number:</label>
        <input type="tel" id="phone" required>
    </div>
    <div class="form-group">
        <label for="item-select">Select Item:</label>
        <select id="item-select" onchange="checkAvailability()">
            <option value="0" data-available="true">--Select an item--</option>
            <option value="1" data-available="true">Item 1 - Available</option>
            <option value="2" data-available="false">Item 2 - Unavailable</option>
            <option value="3" data-available="true">Item 3 - Available</option>
        </select>
    </div>
    <div class="form-group">
        <label for="quantity">Quantity:</label>
        <input type="number" id="quantity" value="1" min="1">
    </div>
    <button type="button" onclick="submitBooking()">Book Now</button>
    <div class="notification success" id="confirmation-message">Booking confirmed! Notification sent.</div>
    <div class="notification error" id="error-message">Selected seats are unavailable.</div>
</div>
<script>
    function checkAvailability() 
        {
        const itemSelect = document.getElementById('item-select');
        const available = itemSelect.options[itemSelect.selectedIndex].getAttribute('data-available');
        
        if (available === 'false') 
        {
            document.getElementById('error-message').style.display = 'block';
        } 
        else 
        {
            document.getElementById('error-message').style.display = 'none';
        }
    }

    function submitBooking() 
       {
        const email = document.getElementById('email').value;
        const phone = document.getElementById('phone').value;
        const itemSelect = document.getElementById('item-select');
        const available = itemSelect.options[itemSelect.selectedIndex].getAttribute('data-available');

        if (available === 'true') 
        {
            sendNotification(email, phone);
            document.getElementById('confirmation-message').style.display = 'block';
            document.getElementById('error-message').style.display = 'none';
        } 
        else 
        {
            document.getElementById('confirmation-message').style.display = 'none';
            document.getElementById('error-message').style.display = 'block';
        }
    }

    function sendNotification(email, phone) 
           {
        console.log(`Sending booking confirmation to ${email} and ${phone}`);
           }
</script>
</body>
</html>
