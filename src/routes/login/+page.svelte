<script>
    import { goto } from '$app/navigation';
  
    let userId = '';
    let password = '';
    let error = '';

    let userValueMap = {
        "test": "테스트 지점",
        "oakberry1": "갤러리아백화점 광교점",
        "oakberry2": "갤러리아백화점 본점",
        "oakberry3": "더현대 대구점",
        "oakberry4": "더현대 서울",
        "oakberry5": "롯데백화점 명동본점",
        "oakberry6": "롯데백화점 부산본점",
        "oakberry7": "롯데백화점 인천점",
        "oakberry8": "신세계백화점 강남점",
        "oakberry9": "신세계백화점 대구점",
        "oakberry10": "신세계백화점 센텀시티점",
        "oakberry11": "타임스퀘어 영등포점",
        "oakberry12": "현대아울렛 송도점",
        "oakberry13": "현대백화점 목동점",
        "oakberry14": "현대백화점 무역점",
        "oakberry15": "현대백화점 부산본점",
        "oakberry16": "현대백화점 압구정본점",
        "oakberry17": "현대백화점 중동점",
        "oakberry18": "현대백화점 판교점",
        "oakberry19": "롯데프리미엄아울렛 기흥점",
        "oakberry20": "대전신세계 아트앤사이언스"
    }
  
    // Function to handle login
    async function handleLogin() {
      // Basic validation
      if (!userId || !password) {
        error = 'Please enter both userId and password';
        return;
      }

      if (userId == 'admin' && password == 'admin') {
        console.log('관리자 계정으로 로그인');
        goto('/admin');
        return;
      } else if (userId == 'test' && password == 'test') {
        console.log('테스트 계정으로 로그인');
        // encode user id and password into base64
        const token = btoa(JSON.stringify({ userId, password }));
        sessionStorage.setItem('accessToken', token);
        await goto('/');
        return;
      } else if (userId in userValueMap && password == 'oakberry') {
        console.log(`${userValueMap[userId]} 계정으로 로그인`);
        // encode user id and password into base64
        const token = btoa(JSON.stringify({ userId, password }));
        sessionStorage.setItem('accessToken', token);
        await goto('/');
        return;
      } else {
        error = '로그인 실패';
        return;
      }

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
  