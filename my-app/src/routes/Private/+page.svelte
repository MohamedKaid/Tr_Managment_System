<script>
  let email = '';
  let password = '';
  let errorMessage = '';

  async function handleSubmit() {
    // In a real application, you would send this data to your backend
    console.log('Logging in with:', { email, password });

    // Simulate a login request (replace with your actual API call)
    try {
      const response = await fetch('/api/login', { // Replace '/api/login' with your actual endpoint
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ email, password }),
      });

      if (response.ok) {
        const data = await response.json();
        // Handle successful login (e.g., redirect, store token)
        console.log('Login successful:', data);
        errorMessage = ''; // Clear any previous error message
        // Example: window.location.href = '/dashboard';
      } else {
        const errorData = await response.json();
        errorMessage = errorData.message || 'Login failed. Please check your credentials.';
        console.error('Login failed:', errorData);
      }
    } catch (error) {
      errorMessage = 'An unexpected error occurred.';
      console.error('Login error:', error);
    }
  }
</script>

<main>
  <h1>Login</h1>

  {#if errorMessage}
    <p class="error">{errorMessage}</p>
  {/if}

  <form on:submit|preventDefault={handleSubmit}>
    <div class="form-group">
      <label for="email">Email:</label>
      <input type="email" id="email" bind:value={email} required>
    </div>

    <div class="form-group">
      <label for="password">Password:</label>
      <input type="password" id="password" bind:value={password} required>
    </div>

    <button type="submit">Log In</button>
  </form>

  <p class="signup-link">
    Don't have an account? <a href="/signup">Sign up</a>
  </p>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }

  h1 {
    margin-bottom: 20px;
  }

  .error {
    color: red;
    margin-bottom: 10px;
  }

  form {
    width: 300px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
  }

  .form-group {
    margin-bottom: 15px;
  }

  label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }

  input[type="email"],
  input[type="password"] {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 3px;
    box-sizing: border-box;
  }

  button[type="submit"] {
    background-color: #007bff;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 3px;
    cursor: pointer;
    font-size: 16px;
  }

  button[type="submit"]:hover {
    background-color: #0056b3;
  }

  .signup-link {
    margin-top: 15px;
    font-size: 0.9em;
  }

  .signup-link a {
    color: #007bff;
    text-decoration: none;
  }

  .signup-link a:hover {
    text-decoration: underline;
  }
</style>