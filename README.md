# TN-VPN
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TopNotch VPN</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0d1117; /* Dark background */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: #e6e6e6; /* Light text color */
        }
        .vpn-container {
            background-color: #161b22; /* Slightly lighter dark for container */
            border-radius: 1.5rem; /* More rounded corners */
            padding: 2.5rem; /* Increased padding */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4); /* Enhanced shadow */
            max-width: 450px; /* Wider container */
            width: 90%; /* Responsive width */
            border: 1px solid #30363d; /* Subtle border */
            display: flex;
            flex-direction: column;
            gap: 1.5rem; /* Space between sections */
            position: relative;
            overflow: hidden;
        }

        .vpn-container::before {
            content: '';
            position: absolute;
            top: -50px;
            left: -50px;
            width: 200px;
            height: 200px;
            background: radial-gradient(circle, rgba(68, 182, 174, 0.2) 0%, rgba(68, 182, 174, 0) 70%);
            border-radius: 50%;
            filter: blur(40px);
            animation: pulse-glow 5s infinite alternate;
        }

        .vpn-container::after {
            content: '';
            position: absolute;
            bottom: -50px;
            right: -50px;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle, rgba(106, 75, 170, 0.2) 0%, rgba(106, 75, 170, 0) 70%);
            border-radius: 50%;
            filter: blur(35px);
            animation: pulse-glow-reverse 6s infinite alternate;
        }

        @keyframes pulse-glow {
            0% { transform: scale(1); opacity: 0.2; }
            100% { transform: scale(1.2); opacity: 0.35; }
        }

        @keyframes pulse-glow-reverse {
            0% { transform: scale(1.2); opacity: 0.35; }
            100% { transform: scale(1); opacity: 0.2; }
        }

        .action-button {
            padding: 1rem 2rem;
            font-size: 1.5rem; /* Larger font size */
            font-weight: 700; /* Bold */
            border-radius: 0.75rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.75rem;
            border: none;
        }

        .connect-button {
            background: linear-gradient(145deg, #28a745, #218838); /* Green gradient */
            color: white;
            box-shadow: 0 5px 15px rgba(40, 167, 69, 0.4);
        }
        .connect-button.disconnect {
            background: linear-gradient(145deg, #dc3545, #c82333); /* Red gradient */
            box-shadow: 0 5px 15px rgba(220, 53, 69, 0.4);
        }
        .connect-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
        }
        .connect-button:active {
            transform: translateY(0);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
        }

        .privacy-tip-button {
            background: linear-gradient(145deg, #44b6ae, #3a9c94); /* Teal gradient */
            color: white;
            box-shadow: 0 5px 15px rgba(68, 182, 174, 0.4);
        }
        .privacy-tip-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
        }
        .privacy-tip-button:active {
            transform: translateY(0);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
        }

        .register-button {
            background: linear-gradient(145deg, #0d6efd, #0a58ca); /* Blue gradient */
            color: white;
            box-shadow: 0 5px 15px rgba(13, 110, 253, 0.4);
        }
        .register-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
        }
        .register-button:active {
            transform: translateY(0);
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
        }

        .customer-care-button {
            background: linear-gradient(145deg, #6f42c1, #563d7c); /* Purple gradient */
            color: white;
            box-shadow: 0 5px 15px rgba(111, 66, 193, 0.4);
            font-size: 1rem; /* Smaller font for these specific buttons */
            padding: 0.75rem 1.5rem;
        }
        .customer-care-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.4);
        }
        .customer-care-button:active {
            transform: translateY(0);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }

        .status-indicator {
            width: 1rem;
            height: 1rem;
            border-radius: 50%;
            background-color: #ffc107; /* Orange for pending */
            transition: background-color 0.5s ease;
        }
        .status-indicator.connected {
            background-color: #28a745; /* Green for connected */
        }
        .status-indicator.disconnected {
            background-color: #dc3545; /* Red for disconnected */
        }
        .status-indicator.loading {
            background-color: #0d6efd; /* Blue for loading Gemini API or connection */
        }

        .location-select, .proxy-select, .registration-input {
            width: 100%;
            padding: 0.75rem 1rem;
            border-radius: 0.5rem;
            background-color: #222933; /* Darker input background */
            border: 1px solid #30363d;
            color: #e6e6e6;
            appearance: none; /* Remove default select arrow */
            -webkit-appearance: none;
            -moz-appearance: none;
            cursor: pointer;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }
        .location-select:focus, .proxy-select:focus, .registration-input:focus {
            outline: none;
            border-color: #44b6ae; /* Accent color on focus */
            box-shadow: 0 0 0 3px rgba(68, 182, 174, 0.3);
        }

        .location-select-wrapper, .proxy-select-wrapper {
            position: relative;
        }
        .location-select-wrapper::after, .proxy-select-wrapper::after {
            content: '▼'; /* Custom arrow */
            font-size: 0.8rem;
            color: #e6e6e6;
            position: absolute;
            right: 1rem;
            top: 50%;
            transform: translateY(-50%);
            pointer-events: none; /* Make sure it doesn't block clicks */
        }

        .privacy-tip-display, .registration-message, .customer-care-message {
            background-color: #222933;
            border-radius: 0.75rem;
            padding: 1.5rem;
            font-size: 0.95rem;
            min-height: 80px; /* Ensure some height even when empty */
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: #c9d1d9;
            border: 1px solid #30363d;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.3);
        }
        .privacy-tip-display p, .registration-message p, .customer-care-message p {
            margin: 0;
        }

        /* Toggle switch styling */
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 28px;
        }

        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            -webkit-transition: .4s;
            transition: .4s;
            border-radius: 34px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 20px;
            width: 20px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            -webkit-transition: .4s;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: #44b6ae; /* Teal when checked */
        }

        input:focus + .slider {
            box-shadow: 0 0 1px #44b6ae;
        }

        input:checked + .slider:before {
            -webkit-transform: translateX(22px);
            -ms-transform: translateX(22px);
            transform: translateX(22px);
        }

        .proxy-settings-section, .registration-section, .customer-care-section {
            background-color: #1f2a3a; /* Slightly different background for section */
            border-radius: 0.75rem;
            padding: 1.5rem;
            border: 1px solid #30363d;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .loading-overlay {
            position: absolute;
            inset: 0;
            background-color: rgba(13, 17, 23, 0.8); /* Match body background with transparency */
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 1.5rem; /* Match container radius */
            z-index: 10;
        }
        .loading-overlay p {
            margin-left: 1rem;
            color: #e6e6e6;
            font-size: 1.2rem;
            font-weight: 500;
        }
    </style>
</head>
<body>
    <div class="vpn-container">
        <h1 class="text-3xl font-bold text-center mb-4 text-emerald-400">TopNotch VPN</h1>

        <!-- Status Section -->
        <div class="flex items-center justify-between bg-gray-800 bg-opacity-50 p-4 rounded-xl shadow-inner border border-gray-700">
            <div class="flex items-center gap-3">
                <div id="statusIndicator" class="status-indicator disconnected"></div>
                <span id="connectionStatus" class="text-xl font-medium">Disconnected</span>
            </div>
            <span id="ipAddress" class="text-sm text-gray-400">IP: ---.---.---.---</span>
        </div>

        <!-- Location Selector -->
        <div class="location-select-wrapper">
            <label for="serverLocation" class="block text-gray-300 text-sm font-medium mb-2">Server Location:</label>
            <select id="serverLocation" class="location-select">
                <option value="auto">Optimal Location (Auto)</option>
                <option value="us-newyork">United States (New York)</option>
                <option value="de-frankfurt">Germany (Frankfurt)</option>
                <option value="sg-singapore">Singapore</option>
                <option value="gb-london">United Kingdom (London)</option>
                <option value="jp-tokyo">Japan (Tokyo)</option>
                <option value="au-sydney">Australia (Sydney)</option>
            </select>
        </div>

        <!-- Proxy Settings Section -->
        <div class="proxy-settings-section">
            <h2 class="text-xl font-semibold text-teal-400">Proxy Settings</h2>
            <div class="flex items-center justify-between">
                <label for="proxyToggle" class="text-gray-300 font-medium">Enable Proxy:</label>
                <label class="toggle-switch">
                    <input type="checkbox" id="proxyToggle">
                    <span class="slider"></span>
                </label>
            </div>
            <div class="proxy-select-wrapper">
                <label for="proxyType" class="block text-gray-300 text-sm font-medium mb-2">Proxy Type:</label>
                <select id="proxyType" class="proxy-select" disabled>
                    <option value="none">No Proxy</option>
                    <option value="http">HTTP Proxy</option>
                    <option value="https">HTTPS Proxy</option>
                    <option value="socks4">SOCKS4 Proxy</option>
                    <option value="socks5">SOCKS5 Proxy</option>
                </select>
            </div>
        </div>

        <!-- Phone Number Registration Section -->
        <div class="registration-section">
            <h2 class="text-xl font-semibold text-blue-400">Phone Number Registration</h2>
            <div class="flex flex-col gap-2">
                <label for="phoneNumber" class="block text-gray-300 text-sm font-medium">Enter Phone Number:</label>
                <input type="tel" id="phoneNumber" class="registration-input" placeholder="+1234567890" pattern="^\+[1-9]\d{1,14}$" required>
                <button id="registerButton" class="action-button register-button text-base px-4 py-2 mt-2">Register Number</button>
            </div>
            <div id="registrationMessage" class="registration-message hidden">
                <p>Enter your phone number and click Register.</p>
            </div>
        </div>

        <!-- Customer Care Service Section -->
        <div class="customer-care-section">
            <h2 class="text-xl font-semibold text-purple-400">Customer Care Service</h2>
            <div class="flex flex-col gap-3">
                <button id="liveChatButton" class="customer-care-button">Live Chat (AI Assistant)</button>
                <div class="flex items-center gap-2 text-gray-300 text-sm">
                    <span>Email Support:</span>
                    <a href="mailto:support@topnotchvpn.com" class="text-purple-300 hover:underline">support@topnotchvpn.com</a>
                </div>
                <button id="faqButton" class="customer-care-button">Frequently Asked Questions</button>
            </div>
            <div id="customerCareMessage" class="customer-care-message hidden">
                <p>Click a button above to get support.</p>
            </div>
        </div>


        <!-- Connect/Disconnect Button -->
        <button id="connectButton" class="action-button connect-button">
            <svg id="buttonIcon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor" class="w-8 h-8">
                <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 10.5V6.75a4.5 4.5 0 1 1 9 0v3.75M3.75 21h10.5a2.25 2.25 0 0 0 2.25-2.25V6.75a2.25 2.25 0 0 0-2.25-2.25H3.75m11.25 11.25H9.75v-4.5m5.25 4.5H9.75m6 0h3v-3.375M16.5 9.75h0.008v0.008H16.5zm-3 0h0.008v0.008H13.5zm-3 0h0.008v0.008H10.5zm-3 0h0.008v0.008H7.5z" />
            </svg>
            <span id="buttonText">Connect</span>
        </button>

        <!-- Get Privacy Tip Button -->
        <button id="getPrivacyTipButton" class="action-button privacy-tip-button">
            ✨ Get Privacy Tip ✨
        </button>

        <!-- Privacy Tip Display Area -->
        <div id="privacyTipDisplay" class="privacy-tip-display">
            <p>Click 'Get Privacy Tip' to learn more about online privacy!</p>
        </div>


        <!-- Loading Spinners (reusing geminiLoadingSpinner for AI chat) -->
        <div id="loadingSpinner" class="hidden loading-overlay">
            <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-b-4 border-emerald-500"></div>
            <p>Connecting...</p>
        </div>

        <div id="geminiLoadingSpinner" class="hidden loading-overlay">
            <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-b-4 border-indigo-500"></div>
            <p>Processing request...</p>
        </div>

        <div id="registrationLoadingSpinner" class="hidden loading-overlay">
            <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-b-4 border-blue-500"></div>
            <p>Registering number...</p>
        </div>

    </div>

    <script>
        // Get references to DOM elements
        const connectButton = document.getElementById('connectButton');
        const buttonText = document.getElementById('buttonText');
        const buttonIcon = document.getElementById('buttonIcon');
        const connectionStatus = document.getElementById('connectionStatus');
        const statusIndicator = document.getElementById('statusIndicator');
        const ipAddressDisplay = document.getElementById('ipAddress');
        const serverLocationSelect = document.getElementById('serverLocation');
        const proxyToggle = document.getElementById('proxyToggle');
        const proxyTypeSelect = document.getElementById('proxyType');
        const phoneNumberInput = document.getElementById('phoneNumber');
        const registerButton = document.getElementById('registerButton');
        const registrationMessage = document.getElementById('registrationMessage');
        const liveChatButton = document.getElementById('liveChatButton');
        const faqButton = document.getElementById('faqButton');
        const customerCareMessage = document.getElementById('customerCareMessage');
        const loadingSpinner = document.getElementById('loadingSpinner');
        const getPrivacyTipButton = document.getElementById('getPrivacyTipButton');
        const privacyTipDisplay = document.getElementById('privacyTipDisplay');
        const geminiLoadingSpinner = document.getElementById('geminiLoadingSpinner');
        const registrationLoadingSpinner = document.getElementById('registrationLoadingSpinner');

        // Initial state
        let isConnected = false;
        let isProxyEnabled = false;
        let currentIP = '---.---.---.---';
        let connectionTimeout = null; // To store the timeout ID
        let registrationTimeout = null; // To store the registration timeout ID

        // Function to update the UI based on connection status
        function updateUI() {
            if (isConnected) {
                // Change button to disconnect state
                connectButton.classList.add('disconnect');
                buttonText.textContent = 'Disconnect';
                // Update icon to represent lock/secure (example path, replace with actual)
                buttonIcon.setAttribute('d', 'M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25V6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v10.5A2.25 2.25 0 0 0 6.75 21Z');

                // Update status text and indicator
                connectionStatus.textContent = isProxyEnabled ? 'Connected (Proxy On)' : 'Connected';
                statusIndicator.classList.remove('disconnected', 'loading');
                statusIndicator.classList.add('connected');

                // Display a simulated IP address
                currentIP = generateRandomIP(isProxyEnabled);
                ipAddressDisplay.textContent = `IP: ${currentIP}`;

                // Disable location selection and proxy settings while connected
                serverLocationSelect.disabled = true;
                proxyToggle.disabled = true;
                proxyTypeSelect.disabled = true;
                phoneNumberInput.disabled = true;
                registerButton.disabled = true;
                liveChatButton.disabled = true; // Disable customer care buttons
                faqButton.disabled = true; // Disable customer care buttons

            } else {
                // Change button to connect state
                connectButton.classList.remove('disconnect');
                buttonText.textContent = 'Connect';
                // Update icon to represent unlock/unsecure (example path, replace with actual)
                buttonIcon.setAttribute('d', 'M13.5 10.5V6.75a4.5 4.5 0 1 1 9 0v3.75M3.75 21h10.5a2.25 2.25 0 0 0 2.25-2.25V6.75a2.25 2.25 0 0 0-2.25-2.25H3.75m11.25 11.25H9.75v-4.5m5.25 4.5H9.75m6 0h3v-3.375M16.5 9.75h0.008v0.008H16.5zm-3 0h0.008v0.008H13.5zm-3 0h0.008v0.008H10.5zm-3 0h0.008v0.008H7.5z');

                // Update status text and indicator
                connectionStatus.textContent = 'Disconnected';
                statusIndicator.classList.remove('connected', 'loading');
                statusIndicator.classList.add('disconnected');

                // Clear IP address
                currentIP = '---.---.---.---';
                ipAddressDisplay.textContent = `IP: ${currentIP}`;

                // Enable all controls when disconnected
                serverLocationSelect.disabled = false;
                proxyToggle.disabled = false;
                proxyTypeSelect.disabled = !isProxyEnabled; // Based on proxy toggle state
                phoneNumberInput.disabled = false;
                registerButton.disabled = false;
                liveChatButton.disabled = false; // Enable customer care buttons
                faqButton.disabled = false; // Enable customer care buttons
            }
        }

        // Function to simulate IP address generation
        function generateRandomIP(isProxy) {
            let ip = Array(4).fill(0).map(() => Math.floor(Math.random() * 255) + 1).join('.');
            if (isProxy) {
                // Simulate a slightly different IP when proxy is enabled
                ip = `10.${Math.floor(Math.random() * 255) + 1}.${Math.floor(Math.random() * 255) + 1}.${Math.floor(Math.random() * 255) + 1}`;
            }
            return ip;
        }

        // Function to disable all interactive elements
        function disableAllControls() {
            connectButton.disabled = true;
            getPrivacyTipButton.disabled = true;
            serverLocationSelect.disabled = true;
            proxyToggle.disabled = true;
            proxyTypeSelect.disabled = true;
            phoneNumberInput.disabled = true;
            registerButton.disabled = true;
            liveChatButton.disabled = true; // Disable customer care buttons
            faqButton.disabled = true; // Disable customer care buttons
        }

        // Function to enable all interactive elements based on current state
        function enableAllControls() {
            connectButton.disabled = false;
            getPrivacyTipButton.disabled = false;
            serverLocationSelect.disabled = false;
            proxyToggle.disabled = false;
            proxyTypeSelect.disabled = !isProxyEnabled;
            phoneNumberInput.disabled = false;
            registerButton.disabled = false;
            liveChatButton.disabled = false; // Enable customer care buttons
            faqButton.disabled = false; // Enable customer care buttons
            updateUI(); // Re-evaluate and apply correct disabled states based on connection
        }


        // Handle connect/disconnect button click
        connectButton.addEventListener('click', () => {
            if (connectionTimeout) {
                clearTimeout(connectionTimeout);
                connectionTimeout = null;
            }

            if (isConnected) {
                isConnected = false;
                updateUI();
                console.log('Disconnected from VPN.');
            } else {
                console.log('Attempting to connect to VPN...');
                loadingSpinner.classList.remove('hidden');
                disableAllControls();

                connectionTimeout = setTimeout(() => {
                    isConnected = true;
                    loadingSpinner.classList.add('hidden');
                    enableAllControls();
                    console.log(`Connected to VPN via ${serverLocationSelect.value}${isProxyEnabled ? ' with proxy' : ''}.`);
                }, 2000);
            }
        });

        // Handle Get Privacy Tip button click
        getPrivacyTipButton.addEventListener('click', async () => {
            geminiLoadingSpinner.classList.remove('hidden');
            disableAllControls();

            statusIndicator.classList.remove('connected', 'disconnected');
            statusIndicator.classList.add('loading');
            connectionStatus.textContent = 'Fetching tip...';

            try {
                let chatHistory = [];
                const prompt = "Give a concise, actionable tip about online privacy or cybersecurity. Make it friendly and easy to understand for a general user.";
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                const payload = { contents: chatHistory };
                const apiKey = ""; // Canvas will provide this in runtime

                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();

                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const text = result.candidates[0].content.parts[0].text;
                    privacyTipDisplay.innerHTML = `<p>${text}</p>`;
                } else {
                    privacyTipDisplay.innerHTML = `<p class="text-red-400">Failed to get tip. Please try again.</p>`;
                    console.error("Gemini API response structure unexpected:", result);
                }
            } catch (error) {
                privacyTipDisplay.innerHTML = `<p class="text-red-400">Error fetching tip: ${error.message}</p>`;
                console.error("Error calling Gemini API:", error);
            } finally {
                geminiLoadingSpinner.classList.add('hidden');
                enableAllControls();
            }
        });

        // Handle proxy toggle change
        proxyToggle.addEventListener('change', () => {
            isProxyEnabled = proxyToggle.checked;
            proxyTypeSelect.disabled = !isProxyEnabled;
            if (isConnected) {
                currentIP = generateRandomIP(isProxyEnabled);
                ipAddressDisplay.textContent = `IP: ${currentIP}`;
                connectionStatus.textContent = isProxyEnabled ? 'Connected (Proxy On)' : 'Connected';
            }
            console.log(`Proxy ${isProxyEnabled ? 'enabled' : 'disabled'}.`);
        });

        // Handle registration button click
        registerButton.addEventListener('click', () => {
            const phoneNumber = phoneNumberInput.value.trim();
            if (!phoneNumber) {
                registrationMessage.classList.remove('hidden');
                registrationMessage.innerHTML = '<p class="text-red-400">Please enter a phone number.</p>';
                return;
            }

            // Basic validation for phone number format (starts with +, followed by 1-14 digits)
            const phonePattern = /^\+[1-9]\d{1,14}$/;
            if (!phonePattern.test(phoneNumber)) {
                registrationMessage.classList.remove('hidden');
                registrationMessage.innerHTML = '<p class="text-red-400">Please enter a valid phone number (e.g., +1234567890).</p>';
                return;
            }

            // Clear any previous registration timeout
            if (registrationTimeout) {
                clearTimeout(registrationTimeout);
                registrationTimeout = null;
            }

            console.log(`Attempting to register phone number: ${phoneNumber}`);
            registrationLoadingSpinner.classList.remove('hidden');
            registrationMessage.classList.add('hidden'); // Hide previous message
            disableAllControls(); // Disable all controls during registration

            // Simulate registration success/failure
            registrationTimeout = setTimeout(() => {
                const success = Math.random() > 0.3; // 70% chance of success
                if (success) {
                    registrationMessage.classList.remove('hidden');
                    registrationMessage.innerHTML = `<p class="text-green-400">Number ${phoneNumber} registered successfully!</p>`;
                    phoneNumberInput.value = ''; // Clear input on success
                } else {
                    registrationMessage.classList.remove('hidden');
                    registrationMessage.innerHTML = `<p class="text-red-400">Registration failed for ${phoneNumber}. Please try again.</p>`;
                }
                registrationLoadingSpinner.classList.add('hidden');
                enableAllControls(); // Re-enable all controls after registration
                console.log(`Registration ${success ? 'successful' : 'failed'}.`);
            }, 2500); // 2.5-second simulated registration delay
        });

        // Function to display messages in the customer care section
        // Renamed to handle AI responses more naturally
        async function displayCustomerCareResponse(message, isError = false) {
            customerCareMessage.classList.remove('hidden');
            customerCareMessage.innerHTML = `<p class="${isError ? 'text-red-400' : 'text-c9d1d9'}">${message}</p>`;
        }

        // Handle Live Chat button click (now AI Assistant)
        liveChatButton.addEventListener('click', async () => {
            geminiLoadingSpinner.classList.remove('hidden');
            disableAllControls();

            // Clear previous customer care message
            customerCareMessage.classList.add('hidden');

            statusIndicator.classList.remove('connected', 'disconnected');
            statusIndicator.classList.add('loading');
            connectionStatus.textContent = 'Connecting to AI...';

            try {
                let chatHistory = [];
                const prompt = "Act as a friendly VPN customer support AI assistant. Greet the user and ask how you can help them with their VPN service. Keep your response concise and welcoming.";
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                const payload = { contents: chatHistory };
                const apiKey = ""; // Canvas will provide this in runtime

                const apiUrl = `https://generativelanguage.googleapis.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();

                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const aiResponse = result.candidates[0].content.parts[0].text;
                    displayCustomerCareResponse(`**AI Assistant:** ${aiResponse}`);
                } else {
                    displayCustomerCareResponse('Sorry, I am unable to connect to the AI assistant. Please try again later.', true);
                    console.error("Gemini API response structure unexpected for AI assistant:", result);
                }
            } catch (error) {
                displayCustomerCareResponse(`Error connecting to AI assistant: ${error.message}`, true);
                console.error("Error calling Gemini API for AI assistant:", error);
            } finally {
                geminiLoadingSpinner.classList.add('hidden');
                enableAllControls();
                updateUI(); // Ensure status indicator reverts correctly
            }
        });

        // Handle FAQ button click
        faqButton.addEventListener('click', () => {
            displayCustomerCareResponse('Opening FAQ section in a new tab (simulated)...', false);
            console.log('FAQ button clicked.');
            // In a real app, you might open a new tab or modal here: window.open('https://your-vpn.com/faq', '_blank');
            setTimeout(() => { customerCareMessage.classList.add('hidden'); }, 5000); // Hide after a delay
        });


        // Initial UI update on page load
        window.onload = function() {
            updateUI();
            // Initial message for registration section
            registrationMessage.classList.remove('hidden');
            registrationMessage.innerHTML = '<p>Enter your phone number to register.</p>';
            // Initial message for customer care section
            customerCareMessage.classList.remove('hidden');
            customerCareMessage.innerHTML = '<p>Click a button above to get support.</p>';
        };

        // Handle server location change (optional, for future expansion)
        serverLocationSelect.addEventListener('change', (event) => {
            console.log(`Server location changed to: ${event.target.value}`);
            // In a real application, changing the server would trigger a re-connection
            // For this simulation, it just logs the change.
        });
    </script>
</body>
</html>