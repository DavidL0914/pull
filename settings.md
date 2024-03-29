<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Settings</title>
    <link rel="stylesheet" href="frontcasts-styling.scss">
</head>
<body>
    <div class="form-container">
        <h2>User Settings</h2>
        <form id="settings-form">
            <input type="text" id="uid" class="input" placeholder="User ID">
            <input type="text" id="username" class="input" placeholder="Username">
            <input type="password" id="password" class="input" placeholder="Password">
            <input type="text" id="theme" class="input" placeholder="Theme (light/dark)">
            <p id="error-message" style="display: none; color: red;"></p>
            <button type="button" onclick="saveSettings()">Save Changes</button>
        </form>
    </div>
    <script>
        // Function to save settings
        function saveSettings() {
            const username = document.getElementById("username").value;
            const password = document.getElementById("password").value;
            const theme = document.getElementById("theme").value;
            const uid = "root"; // Assign the correct uid value from the database
            const name = "Admin"; // Assign the correct name value from the database
            // Save theme setting to localStorage
            localStorage.setItem('theme', theme);
            const data = {
                uid: uid,
                name: name,
                password: password,
                theme: theme
            };
            fetch('http://127.0.0.1:8008/api/users/save_settings', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ settings: data })
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('User does not exist');
                }
                return response.json();
            })
            .then(data => {
                alert('Settings saved successfully');
                console.log(data);
                applyTheme(theme); // Apply theme immediately after saving
            })
            .catch(error => {
                document.getElementById("error-message").innerText = error.message;
                document.getElementById("error-message").style.display = "block";
                console.error('Error:', error);
            });
        }
        // Function to apply theme
        function applyTheme(theme) {
            if (theme === 'light') {
                document.documentElement.style.setProperty('--primary-color', '#fff');
                document.documentElement.style.setProperty('--secondary-color', '#333');
            } else if (theme === 'dark') {
                document.documentElement.style.setProperty('--primary-color', '#333');
                document.documentElement.style.setProperty('--secondary-color', '#fff');
            }
        }
        // Retrieve theme setting from localStorage and apply it
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            document.getElementById("theme").value = savedTheme;
            applyTheme(savedTheme);
        }
    </script>
</body>
</html>
