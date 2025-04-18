<script lang="ts">
  import { onMount } from 'svelte';
  
  let avatar = '/avatar.png';
  
  onMount(() => {
    // Any initialization code can go here
  });
</script>

<div class="container">
  <header class="navbar">
    <div class="nav-buttons">
      <button class="nav-button">
        Расписание <span class="icon"><img src="/top1.svg" alt="Расписание" /></span>
      </button>
      <button class="nav-button">
        Форум <span class="icon"><img src="/top2.svg" alt="Форум" /></span>
      </button>
      <button class="nav-button">
        Сервисы <span class="icon"><img src="/top3.svg" alt="Сервисы" /></span>
      </button>
    </div>
  </header>

  <div class="profile">
    <div class="avatar"></div>
  </div>

  <main>
    <h1 class="main-title">Твой ФФ - университет в одном клике.</h1>

    <!-- Main circular buttons -->
    <div class="circular-buttons">
      <div class="circular-button">
        <div class="circle blue">
          <div class="icon-placeholder"></div>
        </div>
        <span>Бесплатный курс "Вычматика" по математике</span>
      </div>
      <div class="circular-button">
        <div class="circle light-blue">
          <div class="icon-placeholder"></div>
        </div>
        <span>Изменения в расписании</span>
      </div>
      <div class="circular-button">
        <div class="circle pink">
          <div class="icon-placeholder"></div>
        </div>
        <span>Новинки недели в столовой</span>
      </div>
      <div class="circular-button">
        <div class="circle beige">
          <div class="icon-placeholder"></div>
        </div>
        <span>Открытие лаборатории в корпусе Б</span>
      </div>
      <div class="circular-button">
        <div class="circle green">
          <div class="icon-placeholder"></div>
        </div>
        <span>Студенты ФФ и кафедры</span>
      </div>
      <div class="circular-button">
        <div class="circle gray">
          <div class="icon-placeholder"></div>
        </div>
        <span>Для иностранных студентов</span>
      </div>
    </div>

    <!-- Services section -->
    <section class="services">
      <h2>Сервисы</h2>
      <div class="services-grid">
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/map and pencil.svg" alt="Карта корпусов" />
          </div>
          <h3>Карта корпусов</h3>
        </div>
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/cute calendar.svg" alt="Афиша мероприятий" />
          </div>
          <h3>Афиша мероприятий</h3>
        </div>
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/cute books.svg" alt="База знаний" />
          </div>
          <h3>База знаний</h3>
        </div>
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/search cute blue icon.svg" alt="Бюро находок" />
          </div>
          <h3>Бюро находок</h3>
        </div>
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/cute shopping basket.svg" alt="Меню столовой" />
          </div>
          <h3>Меню столовой</h3>
        </div>
        <div class="service-card">
          <div class="service-icon">
            <img src="/main_page/emoji with tongue.svg" alt="Мемы от студентов" />
          </div>
          <h3>Мемы от студентов</h3>
        </div>
      </div>
    </section>
  </main>

  <div class="chat-bot">
    <img src="/chatbot head.svg" alt="Чат-бот" />
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
    background-color: #ffffff;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
  }

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

  /* Profile */
  .profile {
    position: fixed;
    top: 20px;
    right: 20px;
  }

  .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #333;
  }

  /* Main content */
  .main-title {
    text-align: center;
    margin: 40px 0;
    font-size: 32px;
  }

  /* Circular buttons */
  .circular-buttons {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 15px;
    margin: 40px 0;
  }

  .circular-button {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 140px;
    text-align: center;
  }

  .circle {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .circle.blue { background-color: #7CD7F7; }
  .circle.light-blue { background-color: #B8E3F5; }
  .circle.pink { background-color: #FFD6CC; }
  .circle.beige { background-color: #E5D6CC; }
  .circle.green { background-color: #B8F5CC; }
  .circle.gray { background-color: #E6E6E6; }

  .icon-placeholder {
    width: 60px;
    height: 60px;
    background-color: rgba(255, 255, 255, 0.5);
  }

  .circular-button span {
    font-size: 14px;
    line-height: 1.3;
  }

  /* Services section */
  .services {
    margin: 60px 0;
    padding: 0 20px;
  }

  .services h2 {
    margin-bottom: 30px;
    font-size: 24px;
    padding-left: 20px;
  }

  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 25px;
  }

  .service-card {
    background-color: #E4E4E4;
    border-radius: 20px;
    padding: 30px;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 20px;
    min-height: 120px;
    transition: transform 0.2s ease;
    cursor: pointer;
    position: relative;
  }

  .service-card:hover {
    transform: translateY(-5px);
  }

  .service-card h3 {
    margin: 0;
    font-size: 24px;
    font-weight: 500;
    line-height: 1.2;
    order: 1;
  }

  .service-icon {
    width: 100px;
    height: 100px;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    order: 2;
  }

  .service-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  /* Chat Bot */
  .chat-bot {
    position: fixed;
    bottom: 30px;
    right: 30px;
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .chat-bot img {
    width: 65px;
    height: 65px;
  }
</style>
