# dataentry.in
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Entry App</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <style>
        .table-header {
            background-color: #f0f0f0;
            padding: 8px;
            border-bottom: 1px solid #ddd;
        }
        .loading {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border: 8px solid #f3f3f3;
            border-top: 8px solid #3498db;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            animation: spin 2s linear infinite;
        }
        @keyframes spin {
            0% { transform: translate(-50%, -50%) rotate(0deg); }
            100% { transform: translate(-50%, -50%) rotate(360deg); }
        }
    </style>
</head>
<body class="h-screen bg-gray-100 flex justify-center items-center p-4">
    <div class="bg-white p-8 rounded-md shadow-md w-full max-w-sm md:p-12 lg:p-16 xl:p-20">
        <nav class="flex justify-between mb-4">
            <h1 class="text-2xl font-bold text-blue-500">Data Entry App</h1>
            <ul class="flex justify-end">
                <li class="mr-4"><a href="#" class="text-gray-700 hover:text-blue-500">Home</a></li>
                <li><a href="#" class="text-gray-700 hover:text-blue-500">About</a></li>
            </ul>
        </nav>
        <form id="login-form" class="mb-4">
            <div class="mb-4">
                <label for="username" class="block text-gray-700 text-sm font-bold mb-2">Username:</label>
                <input id="username" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" required>
            </div>
            <div class="mb-4">
                <label for="password" class="block text-gray-700 text-sm font-bold mb-2">Password:</label>
                <input id="password" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="password" required>
            </div>
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" id="login-btn">Login</button>
            <p class="mt-2">Don't have an account? <a href="#" id="signup-link" class="text-blue-500 hover:text-blue-700">Sign up</a></p>
        </form>
        <form id="signup-form" class="hidden mb-4">
            <div class="mb-4">
                <label for="signup-username" class="block text-gray-700 text-sm font-bold mb-2">Username:</label>
                <input id="signup-username" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" required>
            </div>
            <div class="mb-4">
                <label for="signup-email" class="block text-gray-700 text-sm font-bold mb-2">Email:</label>
                <input id="signup-email" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="email" required>
            </div>
            <div class="mb-4">
                <label for="signup-password" class="block text-gray-700 text-sm font-bold mb-2">Password:</label>
                <input id="signup-password" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="password" required>
            </div>
            <div class="mb-4">
                <label for="signup-confirm-password" class="block text-gray-700 text-sm font-bold mb-2">Confirm Password:</label>
                <input id="signup-confirm-password" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="password" required>
            </div>
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" id="signup-btn">Sign up</button>
            <p class="mt-2">Already have an account? <a href="#" id="login-link" class="text-blue-500 hover:text-blue-700">Login</a></p>
        </form>
        <form id="data-entry-form" class="hidden mb-4">
            <div class="mb-4">
                <label for="name" class="block text-gray-700 text-sm font-bold mb-2">Name:</label>
                <input id="name" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" required>
            </div>
            <div class="mb-4">
                <label for="email" class="block text-gray-700 text-sm font-bold mb-2">Email:</label>
                <input id="email" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="email" required>
            </div>
            <div class="mb-4">
                <label for="phone" class="block text-gray-700 text-sm font-bold mb-2">Phone:</label>
                <input id="phone" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="tel" required>
            </div>
            <div class="mb-4">
                <label for="address" class="block text-gray-700 text-sm font-bold mb-2">Address:</label>
                <textarea id="address" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required></textarea>
            </div>
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" id="submit-btn">Submit</button>
            <div id="loading" class="loading hidden"></div>
        </form>
        <div id="modal" class="hidden fixed top-0 left-0 right-0 bottom-0 bg-black bg-opacity-50 flex justify-center items-center">
            <div class="bg-white p-8 rounded-md shadow-md w-full max-w-sm md:p-12 lg:p-16 xl:p-20">
                <h2 class="text-2xl font-bold mb-4 text-center text-blue-500">Confirmation</h2>
                <p id="confirmation-message" class="text-lg font-light mb-4"></p>
                <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" id="close-modal">Close</button>
            </div>
        </div>
        <h2 id="stored-data-header" class="text-2xl font-bold mt-8 mb-4 text-center text-blue-500 hidden">Stored Data</h2>
        <table id="stored-data-table" class="w-full table-auto hidden">
            <thead>
                <tr class="table-header">
                    <th class="px-4 py-2">Name</th>
                    <th class="px-4 py-2">Email</th>
                    <th class="px-4 py-2">Phone</th>
                    <th class="px-4 py-2">Address</th>
                </tr>
            </thead>
            <tbody id="data-table-body">
            </tbody>
        </table>
        <button id="clear-data-btn" class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded mt-4 hidden">Clear Data</button>
        <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded mt-4 hidden" id="logout-btn">Logout</button>
    </div>
    <script>
        const loginForm = document.getElementById('login-form');
        const usernameInput = document.getElementById('username');
        const passwordInput = document.getElementById('password');
        const loginBtn = document.getElementById('login-btn');
        const dataEntryForm = document.getElementById('data-entry-form');
        const nameInput = document.getElementById('name');
        const emailInput = document.getElementById('email');
        const phoneInput = document.getElementById('phone');
        const addressInput = document.getElementById('address');
        const submitBtn = document.getElementById('submit-btn');
        const modal = document.getElementById('modal');
        const closeModalBtn = document.getElementById('close-modal');
        const confirmationMessage = document.getElementById('confirmation-message');
        const dataTableBody = document.getElementById('data-table-body');
        const clearDataBtn = document.getElementById('clear-data-btn');
        const logoutBtn = document.getElementById('logout-btn');
        const loading = document.getElementById('loading');
        const signupLink = document.getElementById('signup-link');
        const loginLink = document.getElementById('login-link');
        const signupForm = document.getElementById('signup-form');
        const signupUsernameInput = document.getElementById('signup-username');
        const signupEmailInput = document.getElementById('signup-email');
        const signupPasswordInput = document.getElementById('signup-password');
        const signupConfirmPasswordInput = document.getElementById('signup-confirm-password');
        const signupBtn = document.getElementById('signup-btn');
        const storedDataHeader = document.getElementById('stored-data-header');
        const storedDataTable = document.getElementById('stored-data-table');

        let storedData = [];
        let users = [];
        let isLoggedIn = false;

        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = usernameInput.value;
            const password = passwordInput.value;
            let user = users.find((user) => user.username === username);
            if (user && user.password === password) {
                isLoggedIn = true;
                dataEntryForm.classList.remove('hidden');
                loginForm.classList.add('hidden');
                signupForm.classList.add('hidden');
                logoutBtn.classList.remove('hidden');
                storedDataHeader.classList.remove('hidden');
                storedDataTable.classList.remove('hidden');
                clearDataBtn.classList.remove('hidden');
                if (localStorage.getItem('storedData')) {
                    storedData = JSON.parse(localStorage.getItem('storedData'));
                    updateDataTable();
                }
            } else {
                showConfirmationModal('Invalid username or password');
            }
        });

        submitBtn.addEventListener('click', (e) => {
            e.preventDefault();
            loading.classList.remove('hidden');
            const name = nameInput.value;
            const email = emailInput.value;
            const phone = phoneInput.value;
            const address = addressInput.value;
            storedData.push({ name, email, phone, address });
            localStorage.setItem('storedData', JSON.stringify(storedData));
            updateDataTable();
            showConfirmationModal(`Data saved successfully for ${name}`);
            loading.classList.add('hidden');
        });

        logoutBtn.addEventListener('click', () => {
            isLoggedIn = false;
            dataEntryForm.classList.add('hidden');
            loginForm.classList.remove('hidden');
            signupForm.classList.add('hidden');
            logoutBtn.classList.add('hidden');
            storedDataHeader.classList.add('hidden');
            storedDataTable.classList.add('hidden');
            clearDataBtn.classList.add('hidden');
            localStorage.removeItem('storedData');
            storedData = [];
            updateDataTable();
        });

        closeModalBtn.addEventListener('click', () => {
            modal.classList.add('hidden');
        });

        clearDataBtn.addEventListener('click', () => {
            storedData = [];
            localStorage.removeItem('storedData');
            updateDataTable();
        });

        signupLink.addEventListener('click', (e) => {
            e.preventDefault();
            loginForm.classList.add('hidden');
            signupForm.classList.remove('hidden');
        });

        loginLink.addEventListener('click', (e) => {
            e.preventDefault();
            loginForm.classList.remove('hidden');
            signupForm.classList.add('hidden');
        });

        signupBtn.addEventListener('click', (e) => {
            e.preventDefault();
            const username = signupUsernameInput.value;
            const email = signupEmailInput.value;
            const password = signupPasswordInput.value;
            const confirmPassword = signupConfirmPasswordInput.value;
            if (password !== confirmPassword) {
                showConfirmationModal('Passwords do not match');
                return;
            }
            let user = users.find((user) => user.username === username);
            if (user) {
                showConfirmationModal('Username already taken');
                return;
            }
            users.push({ username, email, password });
            localStorage.setItem('users', JSON.stringify(users));
            showConfirmationModal('Account created successfully');
            loginForm.classList.remove('hidden');
            signupForm.classList.add('hidden');
        });

        function updateDataTable() {
            dataTableBody.innerHTML = '';
            storedData.forEach((data) => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="px-4 py-2">${data.name}</td>
                    <td class="px-4 py-2">${data.email}</td>
                    <td class="px-4 py-2">${data.phone}</td>
                    <td class="px-4 py-2">${data.address}</td>
                `;
                dataTableBody.appendChild(row);
            });
        }

        function showConfirmationModal(message) {
            confirmationMessage.innerText = message;
            modal.classList.remove('hidden');
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 2000);
        }

        if (localStorage.getItem('users')) {
            users = JSON.parse(localStorage.getItem('users'));
        }
    </script>
</body>
</html>
