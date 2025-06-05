<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Clã SOUNDS - The Bridge</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #b30000;
    color: #fff;
    margin: 0;
    padding: 0;
  }
  header {
    background: #8c0000;
    padding: 10px 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  nav {
    display: flex;
    gap: 25px;
  }
  nav a {
    color: #f2c1c1;
    text-decoration: none;
    font-weight: bold;
    font-size: 1.1rem;
    padding: 6px 10px;
    border-radius: 8px;
  }
  nav a:hover, nav a.active {
    background: #ff4d4d;
    color: #fff;
  }
  #loginBtn {
    background: #ff4d4d;
    border: none;
    color: white;
    padding: 8px 16px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
    font-size: 0.9rem;
  }
  #loginBtn:hover {
    background: #ff1a1a;
  }
  #userInfo {
    color: #ffdede;
    font-weight: bold;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  #logoutBtn {
    background: transparent;
    border: 1.5px solid #ffdede;
    padding: 5px 10px;
    border-radius: 8px;
    color: #ffdede;
    cursor: pointer;
    font-size: 0.9rem;
  }
  #logoutBtn:hover {
    background: #ffdede;
    color: #8c0000;
  }
  #authPanel {
    position: fixed;
    top: 50px;
    left: 20px;
    background: rgba(0,0,0,0.9);
    padding: 20px;
    border-radius: 12px;
    width: 320px;
    display: none;
    z-index: 1001;
    color: white;
  }
  #authPanel h3 {
    margin-top: 0;
    text-align: center;
  }
  label {
    display: block;
    margin: 8px 0 4px;
  }
  input[type=text], input[type=email], input[type=password] {
    width: 100%;
    padding: 8px;
    border-radius: 6px;
    border: none;
    font-size: 16px;
  }
  button.authSubmit {
    margin-top: 15px;
    width: 100%;
    padding: 10px;
    background-color: #ff4d4d;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 18px;
    cursor: pointer;
  }
  button.authSubmit:hover {
    background-color: #ff1a1a;
  }
  .switchAuth {
    text-align: center;
    margin-top: 12px;
  }
  .switchAuth a {
    color: #ff9999;
    cursor: pointer;
    text-decoration: underline;
  }
  .error {
    color: #f55;
    margin-top: 5px;
  }
  .success {
    color: #8f8;
    margin-top: 5px;
  }
  main {
    max-width: 900px;
    margin: 40px auto 60px;
    background: rgba(0,0,0,0.3);
    padding: 20px 30px 40px;
    border-radius: 12px;
  }
  h1 {
    text-align: center;
    color: #ffdede;
    margin-bottom: 0;
    font-size: 3rem;
    user-select: none;
  }
  h2 {
    text-align: center;
    font-weight: normal;
    margin-top: 5px;
    font-size: 1.3rem;
  }
  #inicio, #sobre, #discordComentarios, #regras {
    user-select: none;
  }
  /* Lado a lado Discord + Comentários */
  #discordComentariosWrapper {
    display: flex;
    gap: 20px;
    margin-top: 35px;
  }
  section#discord, section#comentarios {
    flex: 1;
    background: #ff6666;
    border-radius: 10px;
    padding: 15px;
    font-size: 1.1rem;
  }
  section#comentarios {
    background: #ff4d4d;
    color: #fff;
  }
  section#comentarios h2 {
    text-align: center;
    margin-top: 0;
  }
  /* Comentários */
  #commentsList {
    margin-top: 20px;
    max-height: 350px;
    overflow-y: auto;
  }
  .comment {
    background: #ff1a1a;
    padding: 10px;
    margin-bottom: 15px;
    border-radius: 8px;
  }
  .comment-header {
    display: flex;
    align-items: center;
    margin-bottom: 8px;
  }
  .comment-username {
    font-weight: bold;
    font-size: 1.1rem;
    margin-left: 10px;
  }
  .comment-text {
    font-size: 1rem;
  }
  .comment-avatar {
    width: 40px;
    height: 55px;
    position: relative;
  }
  .head {
    width: 20px;
    height: 20px;
    background: white;
    border-radius: 50%;
    margin: 0 auto;
  }
  .body {
    width: 4px;
    height: 25px;
    background: white;
    margin: 2px auto 0 auto;
  }
  .arms {
    position: absolute;
    top: 20px;
    width: 30px;
    height: 4px;
    background: white;
    left: 5px;
  }
  .legs {
    position: absolute;
    top: 45px;
    width: 30px;
    height: 4px;
    background: white;
    left: 5px;
  }
  /* Formulário de comentário na seção Comentários */
  #commentInput {
    width: 100%;
    padding: 10px;
    border-radius: 8px;
    border: none;
    font-size: 16px;
    resize: vertical;
  }
  #sendCommentBtn {
    margin-top: 10px;
    padding: 10px;
    width: 100%;
    background: #ff4d4d;
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 18px;
    cursor: pointer;
  }
  #sendCommentBtn:hover {
    background: #ff1a1a;
  }
  #mustLoginMsg {
    text-align: center;
    font-style: italic;
    margin-top: 15px;
    color: #ffb3b3;
  }
  #loggedUserInfo {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 15px;
    font-weight: bold;
    color: #ffdede;
  }
  #loggedUserInfo .avatar {
    width: 40px;
    height: 55px;
    position: relative;
  }
  #loggedUserInfo .avatar > div {
    background: white;
    border-radius: 50%;
  }
  /* Regras */
  #regras ul {
    max-width: 600px;
    margin: 20px auto;
    padding-left: 20px;
    font-size: 1.15rem;
    line-height: 1.5;
  }
  #regras ul li {
    margin-bottom: 10px;
  }

  /* NOVO: Caixinha azul do Discord - estilo */
  .discord-box {
    background-color: #5865F2; /* azul Discord */
    border-radius: 12px;
    padding: 20px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 15px;
    transition: background-color 0.3s ease;
    user-select: none;
  }
  .discord-box:hover {
    background-color: #4752c4;
  }
  .discord-logo {
    width: 40px;
    height: 40px;
    fill: white;
  }
  .discord-text {
    color: white;
    font-weight: bold;
    font-size: 1.4rem;
    text-decoration: none;
  }
</style>
</head>
<body>

<header>
  <button id="loginBtn">Login / Cadastro</button>
  <nav>
    <a href="#" class="active" data-section="inicio">INÍCIO</a>
    <a href="#" data-section="sobre">SOBRE</a>
    <a href="#" data-section="discordComentarios">DISCORD</a>
    <a href="#" data-section="regras">REGRAS</a>
  </nav>
  <div id="userInfo" style="display:none;">
    <span id="userDisplayName"></span>
    <button id="logoutBtn">Sair</button>
  </div>
</header>

<!-- Painel de autenticação -->
<div id="authPanel">
  <h3 id="authTitle">Login</h3>
  <form id="authForm">
    <div id="nameField" style="display:none;">
      <label for="nameInput">Nome</label>
      <input type="text" id="nameInput" autocomplete="name" />
    </div>
    <label for="emailInput">Email</label>
    <input type="email" id="emailInput" autocomplete="email" required />
    <label for="passwordInput">Senha</label>
    <input type="password" id="passwordInput" autocomplete="current-password" required minlength="6" />
    <button type="submit" class="authSubmit">Entrar</button>
    <div class="switchAuth" id="switchAuthText">
      Ainda não tem conta? <a href="#" id="switchToRegister">Cadastre-se</a>
    </div>
    <div class="error" id="authError" style="display:none;"></div>
    <div class="success" id="authSuccess" style="display:none;"></div>
  </form>
</div>

<main>
  <section id="inicio" class="section active">
    <h1>CLÃ SOUNDS - THE BRIDGE</h1>
    <h2>Seja bem-vindo(a) ao nosso clã!</h2>
  </section>

  <section id="sobre" class="section" style="display:none;">
    <h2>Sobre o Clã SOUNDS - THE BRIDGE</h2>
    <p>Somos um clã dedicado a jogos de estratégia e ação, com foco em diversão, amizade e competição saudável. Aqui, você encontra um ambiente acolhedor para compartilhar táticas, treinar e participar de eventos exclusivos.</p>
  </section>

  <section id="discordComentarios" class="section" style="display:none;">
    <div id="discordComentariosWrapper">
      <section id="discord">
        <h2>Nosso Discord</h2>
        <!-- Caixinha azul Discord com logo e nome, clicável -->
        <div class="discord-box" onclick="window.open('https://discord.gg/NVjqJfhA', '_blank')"
          role="button" tabindex="0" aria-label="Abrir Discord do clã SOUNDS">
          <svg class="discord-logo" viewBox="0 0 245 240" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false">
            <path d="M104.4 114.5c-5.7 0-10.2 5-10.2 11.1 0 6.1 4.6 11.1 10.2 11.1 5.7 0 10.2-5 10.2-11.1 0-6.2-4.5-11.1-10.2-11.1zm36.2 0c-5.7 0-10.2 5-10.2 11.1 0 6.1 4.6 11.1 10.2 11.1 5.7 0 10.2-5 10.2-11.1 0-6.2-4.5-11.1-10.2-11.1z" />
            <path d="M189.5 20h-134C41 20 20 40.4 20 69.4v101.2c0 28.8 21 49.3 35.5 49.3h114.3l-5.3-18.2 12.8 11.9 12.1 11.1 21.5 18.2V69.3c0-29-21-49.3-46.4-49.3zM164 162.2s-5.2-6.1-9.5-11.4c19-5.4 26-17.3 26-17.3-6 4-11.7 6.8-16.8 8.7-7.3 3.1-14.4 5.2-21.5 6.3-14.1 2.8-26.9 1.3-37.8-0.9-8.3-1.7-15.4-4.1-21-6.3-2.3-1.1-4.8-2.3-7.3-4-0.3-0.2-0.6-0.3-0.9-0.5-0.2-0.1-0.3-0.2-0.4-0.3-0.1-0.1-0.2-0.2-0.3-0.3-2.5-1.6-3.9-2.5-3.9-2.5s6.5 11.3 23.4 16.9c-4.3 5.3-9.6 11.5-9.6 11.5-31.7-1-43.7-21.8-43.7-21.8 0-46.1 20.6-83.5 20.6-83.5 20.6-15.4 40.3-15 40.3-15l1.4 1.6c-25.9 7.4-37.8 18.5-37.8 18.5s3.1-1.7 8.4-4.1c15.3-6.9 27.4-8.7 32.4-9.2 0.8-0.1 1.5-0.2 2.3-0.2 8.1-1.1 17.3-1.4 27.1 0.4 12.4 2.4 25.7 7.7 39 18.5 0 0-11.5-11.2-35.3-18.6l1.9-2.2s19.5-0.5 40.3 15c0 0 20.6 37.4 20.6 83.5 0 0-12.1 20.8-43.9 21.8z" />
          </svg>
          <span class="discord-text">Discord do Clã SOUNDS</span>
        </div>
      </section>

      <section id="comentarios">
        <h2>Comentários</h2>
        <div id="loggedUserInfo" style="display:none;">
          <div class="avatar">
            <div class="head"></div>
            <div class="body"></div>
            <div class="arms"></div>
            <div class="legs"></div>
          </div>
          <span id="loggedUserName"></span>
        </div>
        <textarea id="commentInput" placeholder="Deixe seu comentário..." rows="3"></textarea>
        <button id="sendCommentBtn">Enviar</button>
        <p id="mustLoginMsg" style="display:none;">Você precisa estar logado para enviar comentários.</p>
        <div id="commentsList"></div>
      </section>
    </div>
  </section>

  <section id="regras" class="section" style="display:none;">
    <h2>Regras do Clã SOUNDS</h2>
    <ul>
      <li>Respeite todos os membros do clã.</li>
      <li>Não use linguagem ofensiva ou discriminatória.</li>
      <li>Evite discussões desnecessárias no chat.</li>
      <li>Colabore e participe das atividades do clã.</li>
      <li>Denuncie comportamentos inadequados aos administradores.</li>
    </ul>
  </section>
</main>

<script>
  // Navegação entre seções
  const navLinks = document.querySelectorAll('nav a');
  const sections = document.querySelectorAll('main .section');

  navLinks.forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault();
      const target = link.dataset.section;
      navLinks.forEach(l => l.classList.remove('active'));
      link.classList.add('active');
      sections.forEach(sec => {
        sec.style.display = (sec.id === target) ? 'block' : 'none';
      });
    });
  });

  // Controle painel login/cadastro
  const loginBtn = document.getElementById('loginBtn');
  const authPanel = document.getElementById('authPanel');
  const authTitle = document.getElementById('authTitle');
  const authForm = document.getElementById('authForm');
  const nameField = document.getElementById('nameField');
  const nameInput = document.getElementById('nameInput');
  const emailInput = document.getElementById('emailInput');
  const passwordInput = document.getElementById('passwordInput');
  const switchAuthText = document.getElementById('switchAuthText');
  const switchToRegister = document.getElementById('switchToRegister');
  const authError = document.getElementById('authError');
  const authSuccess = document.getElementById('authSuccess');
  const userInfo = document.getElementById('userInfo');
  const userDisplayName = document.getElementById('userDisplayName');
  const logoutBtn = document.getElementById('logoutBtn');

  let isLoginMode = true;

  loginBtn.addEventListener('click', () => {
    authPanel.style.display = 'block';
    resetAuthForm();
  });

  switchToRegister.addEventListener('click', (e) => {
    e.preventDefault();
    isLoginMode = !isLoginMode;
    updateAuthForm();
  });

  function updateAuthForm() {
    if (isLoginMode) {
      authTitle.textContent = 'Login';
      nameField.style.display = 'none';
      switchAuthText.innerHTML = 'Ainda não tem conta? <a href="#" id="switchToRegister">Cadastre-se</a>';
      authForm.querySelector('button').textContent = 'Entrar';
    } else {
      authTitle.textContent = 'Cadastro';
      nameField.style.display = 'block';
      switchAuthText.innerHTML = 'Já tem conta? <a href="#" id="switchToRegister">Login</a>';
      authForm.querySelector('button').textContent = 'Cadastrar';
    }
    authError.style.display = 'none';
    authSuccess.style.display = 'none';

    // Re-bind the new link
    document.getElementById('switchToRegister').addEventListener('click', (e) => {
      e.preventDefault();
      isLoginMode = !isLoginMode;
      updateAuthForm();
    });
  }

  function resetAuthForm() {
    authForm.reset();
    authError.style.display = 'none';
    authSuccess.style.display = 'none';
    isLoginMode = true;
    updateAuthForm();
  }

  // Simulando armazenamento de usuários local
  let users = JSON.parse(localStorage.getItem('users') || '{}');

  authForm.addEventListener('submit', (e) => {
    e.preventDefault();
    const email = emailInput.value.trim().toLowerCase();
    const password = passwordInput.value.trim();
    const name = nameInput.value.trim();

    if (isLoginMode) {
      // Login
      if (users[email] && users[email].password === password) {
        // Sucesso
        authSuccess.textContent = 'Login realizado com sucesso!';
        authSuccess.style.display = 'block';
        authError.style.display = 'none';
        setTimeout(() => {
          authPanel.style.display = 'none';
          setLoggedInUser({email, name: users[email].name});
          authForm.reset();
          authSuccess.style.display = 'none';
        }, 1200);
      } else {
        authError.textContent = 'Email ou senha incorretos.';
        authError.style.display = 'block';
        authSuccess.style.display = 'none';
      }
    } else {
      // Cadastro
      if (!name) {
        authError.textContent = 'Por favor, informe seu nome.';
        authError.style.display = 'block';
        authSuccess.style.display = 'none';
        return;
      }
      if (users[email]) {
        authError.textContent = 'Este email já está cadastrado.';
        authError.style.display = 'block';
        authSuccess.style.display = 'none';
        return;
      }
      // Criar novo usuário
      users[email] = {name, password};
      localStorage.setItem('users', JSON.stringify(users));
      authSuccess.textContent = 'Cadastro realizado com sucesso! Faça login.';
      authSuccess.style.display = 'block';
      authError.style.display = 'none';
      setTimeout(() => {
        isLoginMode = true;
        updateAuthForm();
        authForm.reset();
        authSuccess.style.display = 'none';
      }, 1500);
    }
  });

  // Sessão usuário logado
  function setLoggedInUser(user) {
    localStorage.setItem('loggedInUser', JSON.stringify(user));
    userDisplayName.textContent = user.name || user.email;
    userInfo.style.display = 'flex';
    loginBtn.style.display = 'none';
    updateCommentSectionForUser(user);
  }
  function logoutUser() {
    localStorage.removeItem('loggedInUser');
    userInfo.style.display = 'none';
    loginBtn.style.display = 'inline-block';
    updateCommentSectionForUser(null);
  }

  logoutBtn.addEventListener('click', () => {
    logoutUser();
  });

  // No carregamento, verificar se usuário está logado
  const savedUser = JSON.parse(localStorage.getItem('loggedInUser'));
  if (savedUser) {
    setLoggedInUser(savedUser);
  }

  // Comentários
  const commentInput = document.getElementById('commentInput');
  const sendCommentBtn = document.getElementById('sendCommentBtn');
  const commentsList = document.getElementById('commentsList');
  const mustLoginMsg = document.getElementById('mustLoginMsg');
  const loggedUserInfo = document.getElementById('loggedUserInfo');
  const loggedUserName = document.getElementById('loggedUserName');

  // Comentários armazenados localmente
  let comments = JSON.parse(localStorage.getItem('comments') || '[]');

  function renderComments() {
    commentsList.innerHTML = '';
    if (comments.length === 0) {
      commentsList.innerHTML = '<p style="text-align:center;">Nenhum comentário ainda. Seja o primeiro!</p>';
      return;
    }
    comments.forEach(c => {
      const div = document.createElement('div');
      div.className = 'comment';
      div.innerHTML = `
        <div class="comment-header">
          <div class="comment-avatar">
            <div class="head"></div>
            <div class="body"></div>
            <div class="arms"></div>
            <div class="legs"></div>
          </div>
          <div class="comment-username">${escapeHtml(c.name)}</div>
        </div>
        <div class="comment-text">${escapeHtml(c.text)}</div>
      `;
      commentsList.appendChild(div);
    });
  }
  renderComments();

  function escapeHtml(text) {
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
  }

  sendCommentBtn.addEventListener('click', () => {
    const loggedUser = JSON.parse(localStorage.getItem('loggedInUser'));
    if (!loggedUser) {
      mustLoginMsg.style.display = 'block';
      return;
    }
    mustLoginMsg.style.display = 'none';
    const text = commentInput.value.trim();
    if (text.length === 0) return;
    comments.push({name: loggedUser.name || loggedUser.email, text});
    localStorage.setItem('comments', JSON.stringify(comments));
    commentInput.value = '';
    renderComments();
  });

  function updateCommentSectionForUser(user) {
    if (user) {
      loggedUserInfo.style.display = 'flex';
      loggedUserName.textContent = user.name || user.email;
      mustLoginMsg.style.display = 'none';
      commentInput.disabled = false;
      sendCommentBtn.disabled = false;
    } else {
      loggedUserInfo.style.display = 'none';
      mustLoginMsg.style.display = 'block';
      commentInput.disabled = true;
      sendCommentBtn.disabled = true;
    }
  }

  // Inicialmente atualizar estado do formulário de comentários conforme login
  updateCommentSectionForUser(savedUser);

  // Fechar painel ao clicar fora
  window.addEventListener('click', (e) => {
    if (!authPanel.contains(e.target) && e.target !== loginBtn) {
      authPanel.style.display = 'none';
    }
  });

  // Accessibility: Allow keyboard "Enter" on discord-box
  document.querySelector('.discord-box').addEventListener('keypress', (e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      e.currentTarget.click();
    }
  });

</script>

</body>
</html>
