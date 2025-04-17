<script>
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
    <div class="forum-header">
      <h1>Студенческий форум</h1>
      <p>5000 участников</p>
    </div>

    <div class="content">
      <div class="left-panel">
        <div class="section-header">
          <span class="section-icon">≡</span>
          <h2>Статьи</h2>
        </div>

        <div class="posts">
          <div class="post">
            <div class="user-avatar"></div>
            <div class="post-content">
              <div class="post-image-container">
                <div class="post-image-placeholder"></div>
              </div>
              <h3 class="post-title">Лежала на диване в Б корпусе, чья?</h3>
              <div class="post-meta">
                <span class="meta-item date">
                  <img src="/mdi_calendar.svg" alt="Дата" /> 20 мая
                </span>
                <span class="meta-item views">
                  <img src="/viev.svg" alt="Просмотры" /> 120
                </span>
                <span class="meta-item replies">
                  <img src="/otvet.svg" alt="Ответы" /> 2 ответа
                </span>
              </div>
              <button class="view-replies">Смотреть ответы</button>
            </div>
          </div>

          <div class="post">
            <div class="user-avatar"></div>
            <div class="post-content">
              <div class="post-image-container">
                <div class="post-image-placeholder"></div>
              </div>
              <h3 class="post-title">Чей кейс от наушников? Т корпус</h3>
              <div class="post-meta">
                <span class="meta-item date">
                  <img src="/mdi_calendar.svg" alt="Дата" />
                </span>
                <span class="meta-item views">
                  <img src="/viev.svg" alt="Просмотры" /> 20
                </span>
                <span class="meta-item replies">
                  <img src="/otvet.svg" alt="Ответы" /> 1 ответ
                </span>
              </div>
              <button class="view-replies">Смотреть ответы</button>
            </div>
          </div>
        </div>
      </div>

      <div class="right-panel">
        <div class="about-forum">
          <div class="section-header">
            <span class="section-icon">≡</span>
            <h2>О форуме</h2>
          </div>
          
          <div class="info-block">
            <span class="info-icon">
              <img src="/info.svg" alt="Информация" />
            </span>
            <p>Добро пожаловать на Студенческий Хаб — место, где встречаются знания, опыт и студенческая жизнь!</p>
          </div>
          
          <p class="about-text">
            Неважно, первокурсник ты или выпускник – здесь каждый найдёт что-то полезное (и забавное).
            Присоединяйся, задавай вопросы, делись опытом и делай студенческие годы ярче!
          </p>
        </div>

        <div class="topics">
          <div class="section-header">
            <span class="section-icon">≡</span>
            <h2>Темы</h2>
          </div>
          
          <div class="topic-icons">
            <div class="topic">
              <div class="topic-icon">
                <img src="/cute house.svg" alt="Флудилка" class="icon-house" />
              </div>
              <span>Флудилка</span>
            </div>
            <div class="topic">
              <div class="topic-icon">
                <img src="/search cute blue icon.svg" alt="Потеряшки" class="icon-search" />
              </div>
              <span>Потеряшки</span>
            </div>
            <div class="topic">
              <div class="topic-icon">
                <img src="/blue speech bubble.svg" alt="Подслушано" class="icon-speech" />
              </div>
              <span>Подслушано</span>
            </div>
            <div class="topic">
              <div class="topic-icon">
                <img src="/cute books.svg" alt="Конспекты" class="icon-books" />
              </div>
              <span>Конспекты</span>
            </div>
            <div class="topic">
              <div class="topic-icon">
                <img src="/thumbs up.svg" alt="Полезное" class="icon-thumbs" />
              </div>
              <span>Полезное</span>
            </div>
          </div>
        </div>
      </div>
    </div>
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

  .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #333;
  }

  .profile {
    position: fixed;
    top: 20px;
    right: 20px;
  }

  /* Forum Header */
  .forum-header {
    margin: 40px 0;
    text-align: center;
  }

  .forum-header h1 {
    font-size: 32px;
    margin-bottom: 10px;
  }

  .forum-header p {
    color: #666;
    margin: 0;
  }

  /* Content Layout */
  .content {
    display: flex;
    gap: 20px;
  }

  .left-panel {
    flex: 1.5;
    background-color: #e6e6e6;
    border-radius: 15px;
    padding: 20px;
  }

  .right-panel {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .about-forum, .topics {
    background-color: #e6e6e6;
    border-radius: 15px;
    padding: 20px;
  }

  /* Section Headers */
  .section-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 20px;
    background-color: #c0c0c0;
    padding: 8px 15px;
    border-radius: 12px;
    width: fit-content;
  }

  .section-icon {
    font-size: 22px;
  }

  .section-header h2 {
    font-size: 18px;
    margin: 0;
    font-weight: normal;
  }

  /* Posts */
  .posts {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .post {
    display: flex;
    gap: 8px;
  }

  .user-avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: #ffffff;
    flex-shrink: 0;
    margin-top: 5px;
  }

  .post-content {
    flex: 1;
    position: relative;
    padding-left: 5px;
  }

  .post-image-container {
    display: flex;
    justify-content: flex-start;
    width: 100%;
  }

  .post-image-placeholder {
    width: 70%;
    height: 150px;
    background-color: #ffffff;
    border-radius: 10px;
    margin-bottom: 15px;
  }

  .post-title {
    font-size: 18px;
    margin: 0 0 15px 0;
    font-weight: normal;
    text-align: left;
  }

  .post-meta {
    display: flex;
    gap: 15px;
    margin-bottom: 15px;
    color: #888;
    font-size: 14px;
    align-items: center;
  }
  
  .meta-item {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .meta-item img {
    width: 18px;
    height: 18px;
  }

  .view-replies {
    background-color: #cccccc;
    border: none;
    border-radius: 20px;
    padding: 8px 0;
    width: 45%;
    cursor: pointer;
    font-size: 14px;
    color: #333;
    text-align: center;
    margin-left: 10%;
  }

  /* About Forum */
  .info-block {
    display: flex;
    gap: 10px;
    margin-bottom: 10px;
  }

  .info-icon {
    font-size: 22px;
    display: flex;
    align-items: center;
  }

  .info-icon img {
    width: 20px;
    height: 20px;
  }

  .about-text {
    margin: 0;
    line-height: 1.5;
    color: #333;
  }

  /* Topics */
  .topics {
    padding: 25px;
  }

  .topic-icons {
    display: flex;
    justify-content: space-between;
    margin-top: 25px;
  }

  .topic {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    font-size: 14px;
  }

  .topic-icon {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #c0c0c0;
  }

  .topic-icon img {
    max-width: 100%;
    max-height: 100%;
  }

  /* Custom icon sizes with higher specificity */
  .topic-icon .icon-house {
    width: 48px !important;
    height: 38px !important;
  }

  .topic-icon .icon-search {
    width: 38px !important;
    height: 37px !important;
  }

  .topic-icon .icon-speech {
    width: 41px !important;
    height: 57px !important;
  }

  .topic-icon .icon-books {
    width: 40px !important;
    height: 40px !important;
  }

  .topic-icon .icon-thumbs {
    width: 35px !important;
    height: 40px !important;
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
