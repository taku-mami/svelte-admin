<script>
    import { goto } from '$app/navigation';
  
    let userId = '';
    let password = '';
    let error = '';
  
    // Function to handle login
    async function handleLogin() {
      error = '';
  
      // Basic validation
      if (!userId || !password) {
        error = 'Please enter both userId and password';
        return;
      }
  
      // Simulate login request (replace this with your actual login logic)
      const response = await fakeLogin(userId, password);
  
      if (response.success) {
        if (response.name == '관리자 계정') {
          console.log('관리자 계정으로 로그인');
          goto('/admin');
        } else if (response.name == '테스트 계정') {
          console.log('테스트 계정으로 로그인');
          // encode user id and password into base64
          const token = btoa(JSON.stringify({ userId, password }));
          sessionStorage.setItem('accessToken', token);
          goto('/');
        } else {
          console.log('알 수 없는 계정으로 로그인');
          error = '알 수 없는 계정입니다.';
        }
      } else {
        error = '로그인 실패';
      }
    }
  
    // Example login simulation function
    async function fakeLogin(userId, password) {
      return new Promise((resolve) => {
        setTimeout(() => {
          if (userId === 'test' && password === 'test') {
            resolve({ success: true, name: '테스트 계정' });
          } else if (userId === 'admin' && password === 'admin') {
            resolve({ success: true, name: '관리자 계정' });
          } else {
            resolve({ success: false });
          }
        }, 1000);
      });
    }
  </script>
  
  <style>
    .login-container {
      max-width: 400px;
      margin: 50px auto;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      background-color: #f9f9f9;
    }

    h1 {
    text-align: center;
    margin-bottom: 1.5rem;
    color: #333;
    }

    .error {
    color: red;
    text-align: center;
    margin-bottom: 1rem;
    }

    form div {
    margin-bottom: 1rem;
    }

    label {
    display: block;
    margin-bottom: 0.5rem;
    color: #555;
    }

    input {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    }

    button {
    width: 100%;
    padding: 0.75rem;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    }

    button:hover {
    background-color: #0056b3;
    }
  </style>
  
  <div class="login-container">
    <h1>Login</h1>
  
    {#if error}
      <p class="error">{error}</p>
    {/if}
  
    <form on:submit|preventDefault={handleLogin}>
      <div>
        <label for="userId">Id</label>
        <input type="text" id="userId" bind:value={userId} required />
      </div>
      
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" bind:value={password} required />
      </div>
  
      <button type="submit">Login</button>
    </form>
  </div>
  