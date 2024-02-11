<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>User Settings</title>
  <!-- Include your SCSS styling file -->
  <link rel="stylesheet" href="frontcasts-styling.css">
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
      <span>Theme:</span>
      <button id="toggle-theme">Light</button>
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
      // Edit username button functionality
      document.getElementById('edit-username').addEventListener('click', function() {
        const usernameInput = document.getElementById('username');
        usernameInput.disabled = !usernameInput.disabled;
      });

      // Toggle theme functionality
      document.getElementById('toggle-theme').addEventListener('click', function() {
        const currentTheme = document.getElementById('toggle-theme').textContent;
        const newTheme = currentTheme === 'Light' ? 'Dark' : 'Light';
        document.getElementById('toggle-theme').textContent = newTheme;

        // Toggle dark-theme class on the body element
        document.body.classList.toggle('dark-theme');
      });

      // Save settings functionality
      document.getElementById('save-settings').addEventListener('click', function() {
        const username = document.getElementById('username').value;
        const password = document.getElementById('password').value;
        const theme = document.getElementById('toggle-theme').textContent; // Get the theme text directly from the button
        const fontSize = document.getElementById('font-size').value;

        // Send settings data to backend
        fetch('/save_settings', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            username: username,
            password: password,
            theme: theme,
            'font-size': fontSize
          })
        })
        .then(response => {
          if (response.ok) {
            alert('Settings saved successfully!');
          } else {
            alert('Failed to save settings.');
          }
        })
        .catch(error => {
          console.error('Error saving settings:', error);
          alert('Failed to save settings.');
        });
      });
    });
  </script>
</body>
</html>
