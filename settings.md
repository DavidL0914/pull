<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>User Settings</title>
</head>
<body>
  <div class="container">
    <h1>User Settings</h1>
    <div class="settings-form">
      <label for="username">Username:</label>
      <input type="text" id="username" name="username" disabled>
      <button id="edit-username">Edit</button>
      <br>
      <label for="password">New Password:</label>
      <input type="password" id="password" name="password">
      <br>
      <label for="theme">Theme:</label>
      <select id="theme" name="theme">
        <option value="light">Light</option>
        <option value="dark">Dark</option>
      </select>
      <br>
      <label for="font-size">Font Size:</label>
      <select id="font-size" name="font-size">
        <option value="small">Small</option>
        <option value="medium">Medium</option>
        <option value="large">Large</option>
      </select>
      <br>
      <button id="save-settings">Save Settings</button>
    </div>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', function() {
      // Fetch user's theme preference from the backend
      const userTheme = "light"; // Replace this with the actual value fetched from the backend

      // Apply theme class to the body
      document.body.classList.add(userTheme);

      // Edit username button functionality
      document.getElementById('edit-username').addEventListener('click', function() {
        const usernameInput = document.getElementById('username');
        usernameInput.disabled = !usernameInput.disabled;
      });

      // Save settings functionality
      document.getElementById('save-settings').addEventListener('click', function() {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;
        const theme = document.getElementById('theme').value;
        const fontSize = document.getElementById('font-size').value;

        // Save settings to local storage or send to backend
        // Here you can send the settings to the backend to update in the database
        // For demonstration purpose, we are not implementing backend interaction

        alert('Settings saved successfully!');
      });
    });
  </script>
</body>
</html>
