<script>
  export let currentPage = "/"; // По умолчанию активна главная страница
</script>

<header class="navbar">
  <div class="nav-buttons">
    <button class="nav-button">
      Расписание <span class="icon"><img src="/top1.svg" alt="Расписание" /></span>
    </button>
    <a href="/forum" class="nav-link">
      <button class="nav-button {currentPage === '/forum' ? 'active' : ''}">
        Форум <span class="icon"><img src="/top2.svg" alt="Форум" /></span>
      </button>
    </a>
    <a href="/" class="nav-link">
      <button class="nav-button {currentPage === '/' ? 'active' : ''}">
        Сервисы <span class="icon"><img src="/top3.svg" alt="Сервисы" /></span>
      </button>
    </a>
  </div>
</header>

<style>
  /* Navbar */
  .navbar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 0;
  }

  .nav-buttons {
    display: flex;
    gap: 15px;
  }

  .nav-button {
    background-color: #f0f0f0;
    border: none;
    border-radius: 20px;
    padding: 8px 16px;
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 5px;
    cursor: pointer;
  }

  .icon {
    font-size: 18px;
    display: flex;
    align-items: center;
  }

  .icon img {
    width: 18px;
    height: 18px;
  }

  .nav-link {
    text-decoration: none;
  }

  .nav-button.active {
    background-color: #e0e0e0;
  }
</style> 