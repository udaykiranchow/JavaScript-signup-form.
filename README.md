<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Signup Form</title>
   <style>
       .valid {
           color: green;
       }
       .invalid {
           color: red;
       }
       button:disabled {
           opacity: 0.5;
           cursor: not-allowed;
       }
   </style>
</head>
<body>
   <h1>Signup Form</h1>
   <form id="signupForm">
       <label for="username">Username:</label>
       <input type="text" id="username" required>
       <span id="usernameMessage">Username must be alphanumeric and at least 6 characters long.</span>
       <br>

       <label for="email">Email:</label>
       <input type="email" id="email" required>
       <span id="emailMessage">Email address must be in a valid format.</span>
       <br>

       <label for="password">Password:</label>
       <input type="password" id="password" required>
       <span id="passwordMessage">Password must be at least 8 characters long.</span>
       <br>

       <button type="submit" id="submitBtn" disabled>Submit</button>
   </form>

   <script>
       // Get references to form elements
       const form = document.getElementById('signupForm');
       const username = document.getElementById('username');
       const email = document.getElementById('email');
       const password = document.getElementById('password');
       const submitBtn = document.getElementById('submitBtn');

       // Get references to validation message elements
       const usernameMessage = document.getElementById('usernameMessage');
       const emailMessage = document.getElementById('emailMessage');
       const passwordMessage = document.getElementById('passwordMessage');

       // Regular expressions for validation
       const usernameRegex = /^[a-zA-Z0-9]{6,}$/;
       const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

       // Function to validate username
       function validateUsername() {
           if (usernameRegex.test(username.value)) {
               usernameMessage.classList.remove('invalid');
               usernameMessage.classList.add('valid');
               usernameMessage.textContent = 'Valid username';
           } else {
               usernameMessage.classList.remove('valid');
               usernameMessage.classList.add('invalid');
               usernameMessage.textContent = 'Username must be alphanumeric and at least 6 characters long.';
           }
       }

       // Function to validate email
       function validateEmail() {
           if (emailRegex.test(email.value)) {
               emailMessage.classList.remove('invalid');
               emailMessage.classList.add('valid');
               emailMessage.textContent = 'Valid email address';
           } else {
               emailMessage.classList.remove('valid');
               emailMessage.classList.add('invalid');
               emailMessage.textContent = 'Email address must be in a valid format.';
           }
       }

       // Function to validate password
       function validatePassword() {
           if (password.value.length >= 8) {
               passwordMessage.classList.remove('invalid');
               passwordMessage.classList.add('valid');
               passwordMessage.textContent = 'Valid password';
           } else {
               passwordMessage.classList.remove('valid');
               passwordMessage.classList.add('invalid');
               passwordMessage.textContent = 'Password must be at least 8 characters long.';
           }
       }

       // Function to enable/disable submit button
       function toggleSubmitButton() {
           if (usernameRegex.test(username.value) && emailRegex.test(email.value) && password.value.length >= 8) {
               submitBtn.disabled = false;
           } else {
               submitBtn.disabled = true;
           }
       }

       // Add event listeners for input fields
       username.addEventListener('input', validateUsername);
       username.addEventListener('input', toggleSubmitButton);
       email.addEventListener('input', validateEmail);
       email.addEventListener('input', toggleSubmitButton);
       password.addEventListener('input', validatePassword);
       password.addEventListener('input', toggleSubmitButton);

       // Prevent form submission if any field is invalid
       form.addEventListener('submit', (event) => {
           if (!usernameRegex.test(username.value) || !emailRegex.test(email.value) || password.value.length < 8) {
               event.preventDefault();
           }
       });
   </script>
</body>
</html>
