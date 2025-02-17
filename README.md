<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Food Ordering System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
        }
        h1, h2 {
            color: #333;
        }
        button {
            margin: 5px;
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        input {
            display: block;
            margin: 10px 0;
            padding: 10px;
            width: 100%;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        a {
            color: #007bff;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        .section {
            margin-top: 20px;
            padding: 20px;
            background-color: white;
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        #about-software {
            display: none; /* Hidden by default */
            position: fixed;
            bottom: 20px;
            left: 20px;
            font-size: 14px;
            color: #666;
            background-color: white;
            padding: 10px;
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body>

    <!-- About Section -->
    <div id="about-software">
        <h2>About</h2>
        <p>This software is developed by Belete Birhanu and Daniel Hailu.</p>
    </div>

    <!-- Login Page -->
    <div id="login-section" class="section">
        <h1>Login</h1>
        <form id="login-form">
            <input type="text" id="username" placeholder="Username" required>
            <input type="password" id="password" placeholder="Password" required>
            <div>
                <label for="language">Language:</label>
                <select id="language" onchange="changeLanguage()">
                    <option value="en">English</option>
                    <option value="am">አማርኛ</option>
                </select>
            </div>
            <button type="button" onclick="login()">Login</button>
            <p><a href="#" onclick="showForgotPassword()">Forgot Password?</a></p>
        </form>
        <p>Don't have an account? <a href="#" onclick="showRegister()">Create one</a></p>
        <button onclick="toggleAbout()">About</button>
    </div>

    <!-- Registration Page -->
    <div id="create-account-section" class="section" style="display:none;">
        <h1>Create Account</h1>
        <form id="create-account-form">
            <input type="text" id="new-username" placeholder="Username" required>
            <input type="password" id="new-password" placeholder="Password" required>
            <div>
                <label for="language">Language:</label>
                <select id="language" onchange="changeLanguage()">
                    <option value="en">English</option>
                    <option value="am">አማርኛ</option>
                </select>
            </div>
            <button type="button" onclick="createAccount()">Create Account</button>
        </form>
        <p>Already have an account? <a href="#" onclick="showLogin()">Login</a></p>
        <button onclick="toggleAbout()">About</button>
    </div>

    <!-- Forgot Password Page -->
    <div id="forgot-password-section" class="section" style="display:none;">
        <h1>Forgot Password</h1>
        <p>Please enter your email address to reset your password.</p>
        <input type="email" id="reset-email" placeholder="Email" required>
        <button type="button" onclick="resetPassword()">Reset Password</button>
        <p><a href="#" onclick="showLogin()">Back to Login</a></p>
        <button onclick="toggleAbout()">About</button>
    </div>

    <!-- Main Page -->
    <div id="main-page" class="section" style="display:none;">
        <button style="float: right;" onclick="showLogin()">Back</button>
        <h1>Welcome!</h1>
        <div id="choices">
            <button onclick="showLocations()">View Locations</button>
            <button onclick="showAbout()">About</button>
        </div>
        <div id="locations" style="display:none;">
            <h2>Choose a location:</h2>
            <button onclick="showHotels()">Hotels</button>
            <button onclick="showSupermarkets()">Supermarkets</button>
            <button onclick="showPharmacies()">Pharmacies</button>
        </div>
        <div id="hotels" style="display:none;">
            <h2>Hotels</h2>
            <button onclick="showMenu('sheraton')">Sheraton Addis</button>
            <button onclick="showMenu('ethiopian')">Ethiopian Hotel</button>
            <button onclick="showMenu('elile')">Elile Hotel</button>
        </div>
        <div id="menu" style="display:none;">
            <h2>Menu</h2>
            <button onclick="showFood()">Foods</button>
            <button onclick="showDrinks()">Drinks</button>
            <button onclick="showBedrooms()">Bedrooms</button>
        </div>
        <div id="food-items" style="display:none;">
            <h2>Foods</h2>
            <button onclick="showFoodDetails('lazagna')">Lazagna</button>
            <button onclick="showFoodDetails('beyeayinet')">Beyeayinet</button>
            <button onclick="showFoodDetails('qurt')">Qurt</button>
        </div>
        <div id="food-detail" style="display:none;">
            <h2>Food Detail</h2>
            <p id="food-name"></p>
            <p id="price"></p>
            <input type="text" placeholder="Order time" id="order-time">
            <button onclick="orderFood()">Order</button>
        </div>
        <div id="payment" style="display:none;">
            <h2>Payment Method</h2>
            <select id="payment-method" onchange="showPaymentDetails()">
                <option value="">Select Payment Method</option>
                <option value="bank">Bank</option>
                <option value="telebir">Telebirr</option>
            </select>
            <div id="bank-details" style="display:none;">
                <h3>Select Your Bank</h3>
                <select id="bank-select">
                    <option value="cbe">Commercial Bank of Ethiopia</option>
                    <option value="dashen">Dashen Bank</option>
                    <option value="wegagen">Wegagen Bank</option>
                    <option value="hibret">Hibret Bank</option>
                    <option value="abaysh">Abay Bank</option>
                </select>
                <input type="text" id="account-number" placeholder="Bank Account Number" required>
                <input type="text" id="amount" placeholder="Amount" required>
                <button onclick="processPayment()">Submit Payment</button>
            </div>
            <div id="telebir-details" style="display:none;">
                <h3>Telebirr Payment</h3>
                <input type="text" id="phone-number" placeholder="Phone Number" required>
                <input type="text" id="telebir-amount" placeholder="Amount" required>
                <button onclick="processTelebirPayment()">Submit Payment</button>
            </div>
        </div>
    </div>

    <!-- About Page -->
    <div id="about-section" class="section" style="display:none;">
        <button style="float: right;" onclick="showMainPage()">Back</button>
        <h1>About Us</h1>
        <p>This is the about page with GPS functionality.</p>
        <button onclick="getLocation()">Get My Location</button>
        <p id="location-output"></p>
    </div>

    <script>
        let users = {}; // Simple in-memory user storage

        function showLogin() {
            document.getElementById('login-section').style.display = 'block';
            document.getElementById('create-account-section').style.display = 'none';
            document.getElementById('forgot-password-section').style.display = 'none';
            document.getElementById('main-page').style.display = 'none';
            document.getElementById('about-section').style.display = 'none';
            document.getElementById('about-software').style.display = 'none'; // Hide about section
        }

        function showRegister() {
            document.getElementById('login-section').style.display = 'none';
            document.getElementById('create-account-section').style.display = 'block';
            document.getElementById('forgot-password-section').style.display = 'none';
            document.getElementById('main-page').style.display = 'none';
            document.getElementById('about-section').style.display = 'none';
            document.getElementById('about-software').style.display = 'none'; // Hide about section
        }

        function showForgotPassword() {
            document.getElementById('login-section').style.display = 'none';
            document.getElementById('create-account-section').style.display = 'none';
            document.getElementById('forgot-password-section').style.display = 'block';
            document.getElementById('main-page').style.display = 'none';
            document.getElementById('about-section').style.display = 'none';
            document.getElementById('about-software').style.display = 'none'; // Hide about section
        }

        function showMainPage() {
            document.getElementById('login-section').style.display = 'none';
            document.getElementById('create-account-section').style.display = 'none';
            document.getElementById('forgot-password-section').style.display = 'none';
            document.getElementById('main-page').style.display = 'block';
            document.getElementById('about-section').style.display = 'none';
            document.getElementById('about-software').style.display = 'none'; // Hide about section
        }

        function toggleAbout() {
            const aboutDiv = document.getElementById('about-software');
            aboutDiv.style.display = (aboutDiv.style.display === 'none' || aboutDiv.style.display === '') ? 'block' : 'none';
        }

        function changeLanguage() {
            const language = document.getElementById('language').value;
            const texts = {
                en: {
                    login: 'Login',
                    createAccount: 'Create Account',
                    forgotPassword: 'Forgot Password?',
                    back: 'Back'
                },
                am: {
                    login: 'ግባ',
                    createAccount: 'አዲስ ይፍጠሩ',
                    forgotPassword: 'የይለፍ ቁጥር አለመጣል?',
                    back: 'ወደ ኋላ'
                }
            };

            const selectedTexts = texts[language];
            document.getElementById('login-section').querySelector('h1').innerText = selectedTexts.login;
            document.getElementById('create-account-section').querySelector('h1').innerText = selectedTexts.createAccount;
            document.getElementById('forgot-password-section').querySelector('h1').innerText = selectedTexts.forgotPassword;
            document.querySelectorAll('p a').forEach(a => a.innerText = selectedTexts.back);
        }

        function showLocations() {
            document.getElementById('locations').style.display = 'block';
        }

        function showHotels() {
            document.getElementById('hotels').style.display = 'block';
            document.getElementById('locations').style.display = 'none';
        }

        function showMenu(hotel) {
            document.getElementById('menu').style.display = 'block';
            document.getElementById('hotels').style.display = 'none';
        }

        function showFood() {
            document.getElementById('food-items').style.display = 'block';
            document.getElementById('menu').style.display = 'none';
        }

        function showFoodDetails(food) {
            const foodDetails = {
                lazagna: { price: "$15.00" },
                beyeayinet: { price: "$10.00" },
                qurt: { price: "$12.00" }
            };
            
            document.getElementById('food-name').innerText = food.charAt(0).toUpperCase() + food.slice(1);
            document.getElementById('price').innerText = foodDetails[food].price;
            document.getElementById('food-detail').style.display = 'block';
            document.getElementById('food-items').style.display = 'none';
            document.getElementById('payment').style.display = 'block'; // Show payment options
        }

        function showPaymentDetails() {
            const paymentMethod = document.getElementById('payment-method').value;
            const bankDetails = document.getElementById('bank-details');
            const telebirDetails = document.getElementById('telebir-details');

            bankDetails.style.display = paymentMethod === 'bank' ? 'block' : 'none';
            telebirDetails.style.display = paymentMethod === 'telebir' ? 'block' : 'none';
        }

        function processPayment() {
            const bankAccount = document.getElementById('account-number').value;
            const amount = document.getElementById('amount').value;
            alert(`Payment of ${amount} has been processed to ${bankAccount}.`);
        }

        function processTelebirPayment() {
            const phoneNumber = document.getElementById('phone-number').value;
            const amount = document.getElementById('telebir-amount').value;
            alert(`Telebirr payment of ${amount} has been processed to ${phoneNumber}.`);
        }

        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(showPosition);
            } else {
                document.getElementById('location-output').innerText = "Geolocation is not supported by this browser.";
            }
        }

        function showPosition(position) {
            const output = `Latitude: ${position.coords.latitude}, Longitude: ${position.coords.longitude}`;
            document.getElementById('location-output').innerText = output;
        }
    </script>

</body>
</html>
