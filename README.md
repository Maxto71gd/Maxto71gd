<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hash-based Navigation</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        #login, #dashboard { display: none; }
        .active { display: block; }
    </style>
</head>
<body>
    <div id="login" class="active">
        <h1>Login Page</h1>
        <form id="loginForm">
            <input type="text" id="username" placeholder="Enter username" required>
            <button type="submit">Login</button>
        </form>
    </div>

    <div id="dashboard">
        <h1>Dashboard</h1>
        <p>Welcome, <span id="userDisplay"></span>!</p>
        <a href="#login" onclick="logout()">Logout</a>
    </div>

    <script>
        const loginDiv = document.getElementById('login');
        const dashboardDiv = document.getElementById('dashboard');
        const userDisplay = document.getElementById('userDisplay');

        // Handle navigation
        function navigate() {
            if (window.location.hash === '#dashboard') {
                const username = sessionStorage.getItem('username');
                if (username) {
                    loginDiv.classList.remove('active');
                    dashboardDiv.classList.add('active');
                    userDisplay.textContent = username;
                } else {
                    alert('Please log in first!');
                    window.location.hash = '#login';
                }
            } else {
                loginDiv.classList.add('active');
                dashboardDiv.classList.remove('active');
            }
        }

        // Login action
        document.getElementById('loginForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            sessionStorage.setItem('username', username);
            window.location.hash = '#dashboard';
        });

        // Logout action
        function logout() {
            sessionStorage.removeItem('username');
        }

        // Listen to hash changes
        window.addEventListener('hashchange', navigate);

        // Load correct page on initial load
        navigate();
    </script>
</body>
</html>
