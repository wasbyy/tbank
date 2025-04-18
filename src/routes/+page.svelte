<script lang="ts">
  import { onMount } from 'svelte';
  
  let avatar = '/avatar.png';
  let showChatBubble = true;
  let showStories = false;
  let currentStoryIndex = 0;
  let showChatDialog = false;
  let userMessage = '';
  
  interface Story {
    id: number;
    image: string;
    title: string;
    content: string;
  }
  
  let stories: Story[] = [
    {
      id: 1,
      image: '/main_page/stories1.svg',
      title: 'Новости факультета',
      content: 'Подробное содержание новостей факультета. Здесь будет отображаться полная информация о событии.'
    },
    {
      id: 2,
      image: '/main_page/stories2.svg',
      title: 'Студенческая жизнь',
      content: 'Подробное содержание о студенческой жизни. Здесь будет отображаться полная информация о событии.'
    },
    {
      id: 3,
      image: '/main_page/stories3.svg',
      title: 'Научные достижения',
      content: 'Подробное содержание о научных достижениях. Здесь будет отображаться полная информация о событии.'
    },
    {
      id: 4,
      image: '/main_page/stories4.svg',
      title: 'Конференции',
      content: 'Подробное содержание о конференциях. Здесь будет отображаться полная информация о событии.'
    },
    {
      id: 5,
      image: '/main_page/stories5.svg',
      title: 'Стажировки',
      content: 'Подробное содержание о стажировках. Здесь будет отображаться полная информация о событии.'
    },
    {
      id: 6,
      image: '/main_page/stories6.svg',
      title: 'Спортивные события',
      content: 'Подробное содержание о спортивных событиях. Здесь будет отображаться полная информация о событии.'
    }
  ];
  
  function closeChatBubble() {
    showChatBubble = false;
  }
  
  function toggleChatDialog() {
    showChatDialog = !showChatDialog;
    showChatBubble = false;
  }
  
  function closeChatDialog() {
    showChatDialog = false;
  }
  
  function sendMessage() {
    if (userMessage.trim() !== '') {
      // Here you would normally process the message and get a response
      userMessage = '';
    }
  }
  
  function openStories(index: number) {
    currentStoryIndex = index;
    showStories = true;
  }
  
  function closeStories() {
    showStories = false;
  }
  
  function nextStory() {
    if (currentStoryIndex < stories.length - 1) {
      currentStoryIndex++;
    } else {
      closeStories();
    }
  }
  
  function prevStory() {
    if (currentStoryIndex > 0) {
      currentStoryIndex--;
    }
  }
  
  function getCurrentDate() {
    const now = new Date();
    const months = [
      'января', 'февраля', 'марта', 'апреля', 'мая', 'июня', 
      'июля', 'августа', 'сентября', 'октября', 'ноября', 'декабря'
    ];
    return `${now.getDate()} ${months[now.getMonth()]}`;
  }
  
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
      <a href="/forum" class="nav-link">
        <button class="nav-button">
          Форум <span class="icon"><img src="/top2.svg" alt="Форум" /></span>
        </button>
      </a>
      <a href="/" class="nav-link">
        <button class="nav-button active">
          Сервисы <span class="icon"><img src="/top3.svg" alt="Сервисы" /></span>
        </button>
      </a>
    </div>
  </header>

  <div class="profile">
    <div class="avatar"></div>
  </div>

  <main>
    <h1 class="main-title">Твой ФФ - университет в одном клике.</h1>

    <!-- Main circular buttons -->
    <div class="circular-buttons">
      {#each stories as story, index}
        <div class="circular-button" on:click={() => openStories(index)}>
          <img src={story.image} alt={story.title} class="story-image">
        </div>
      {/each}
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
          <a href="/afisha" class="card-link">
            <div class="service-icon">
              <img src="/main_page/cute calendar.svg" alt="Афиша мероприятий" />
            </div>
            <h3>Афиша мероприятий</h3>
          </a>
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
    {#if showChatBubble}
      <div class="chat-bubble">
        <span class="close-bubble" on:click={closeChatBubble}>&times;</span>
        Привет! Я - физик,<br>твой виртуальный помощник
      </div>
    {/if}
    <img src="/chatbot head.svg" alt="Чат-бот" on:click={toggleChatDialog} />
  </div>
</div>

{#if showStories}
  <div class="stories-overlay">
    <div class="stories-slider">
      <div class="progress-bar">
        {#each stories as _, i}
          <div class="progress-segment {i === currentStoryIndex ? 'active' : i < currentStoryIndex ? 'completed' : ''}"></div>
        {/each}
      </div>
      
      <button class="close-stories" on:click={closeStories}>&times;</button>

      <div class="stories-carousel">
        {#if currentStoryIndex > 1}
          <div class="story-card far-prev-card" on:click={() => prevStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[currentStoryIndex - 2].title}</h2>
              <div class="story-image-container">
                <img src={stories[currentStoryIndex - 2].image} alt={stories[currentStoryIndex - 2].title} />
              </div>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}

        {#if currentStoryIndex > 0}
          <div class="story-card prev-card" on:click={() => prevStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[currentStoryIndex - 1].title}</h2>
              <div class="story-image-container">
                <img src={stories[currentStoryIndex - 1].image} alt={stories[currentStoryIndex - 1].title} />
              </div>
              <p class="story-description">{stories[currentStoryIndex - 1].content}</p>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}
        
        <div class="story-card current-card">
          <h2 class="story-title">{stories[currentStoryIndex].title}</h2>
          <div class="story-image-container">
            <img src={stories[currentStoryIndex].image} alt={stories[currentStoryIndex].title} />
          </div>
          <p class="story-description">{stories[currentStoryIndex].content}</p>
        </div>
        
        {#if currentStoryIndex < stories.length - 1}
          <div class="story-card next-card" on:click={() => nextStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[currentStoryIndex + 1].title}</h2>
              <div class="story-image-container">
                <img src={stories[currentStoryIndex + 1].image} alt={stories[currentStoryIndex + 1].title} />
              </div>
              <p class="story-description">{stories[currentStoryIndex + 1].content}</p>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}

        {#if currentStoryIndex < stories.length - 2}
          <div class="story-card far-next-card" on:click={() => nextStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[currentStoryIndex + 2].title}</h2>
              <div class="story-image-container">
                <img src={stories[currentStoryIndex + 2].image} alt={stories[currentStoryIndex + 2].title} />
              </div>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}
      </div>
      
      <div class="story-navigation">
        <button class="story-nav-button prev" on:click={prevStory} disabled={currentStoryIndex === 0}>
          <span>❮</span>
        </button>
        <button class="story-nav-button next" on:click={nextStory} disabled={currentStoryIndex === stories.length - 1}>
          <span>❯</span>
        </button>
      </div>
    </div>
  </div>
{/if}

{#if showChatDialog}
  <div class="chat-dialog-overlay">
    <div class="chat-dialog">
      <div class="chat-header">
        <div class="chat-header-left">
          <img src="/chatbot head.svg" alt="Физик" class="chat-avatar" />
          <h3>Физик чат-бот</h3>
        </div>
        <div class="chat-header-right">
          <button class="settings-button">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="3"></circle>
              <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path>
            </svg>
          </button>
          <button class="close-dialog" on:click={closeChatDialog}>&times;</button>
        </div>
      </div>
      
      <div class="chat-divider"></div>
      
      <div class="chat-date">
        {getCurrentDate()}
      </div>
      
      <div class="chat-messages">
        <div class="message bot">
          <div class="message-sender">Физик</div>
          <div class="message-content">
            Привет! Я - физик,<br>
            твой виртуальный помощник<br>
            С чем тебе помочь сегодня?<br>
            Навигация по сайту или<br>
            пересказ лекции?
          </div>
        </div>
        <!-- More messages would be added here -->
      </div>
      
      <div class="chat-input">
        <button class="voice-button">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"></path>
            <path d="M19 10v2a7 7 0 0 1-14 0v-2"></path>
            <line x1="12" y1="19" x2="12" y2="23"></line>
            <line x1="8" y1="23" x2="16" y2="23"></line>
          </svg>
        </button>
        <input 
          type="text" 
          placeholder="Ваше сообщение" 
          bind:value={userMessage}
          on:keydown={(e) => e.key === 'Enter' && sendMessage()}
        />
        <button class="send-button" on:click={sendMessage}>
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="22" y1="2" x2="11" y2="13"></line>
            <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
          </svg>
        </button>
      </div>
    </div>
  </div>
{/if}

<style>
  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Regular.otf') format('opentype');
    font-weight: 400;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Medium.otf') format('opentype');
    font-weight: 500;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Bold.otf') format('opentype');
    font-weight: 700;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Light.otf') format('opentype');
    font-weight: 300;
    font-style: normal;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'SF Pro Display', Arial, sans-serif;
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

  .nav-link {
    text-decoration: none;
  }

  .nav-button.active {
    background-color: #e0e0e0;
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
    margin: 20px 0;
    font-size: 28px;
  }

  /* Circular buttons */
  .circular-buttons {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 15px;
    margin: 20px 0;
  }

  .circular-button {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: auto;
    margin: 0 10px;
    cursor: pointer;
  }

  .story-image {
    width: 90px;
    height: 90px;
    border-radius: 50%;
    object-fit: cover;
  }

  /* Services section */
  .services {
    margin: 20px 0;
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

  .card-link {
    display: flex;
    width: 100%;
    height: 100%;
    text-decoration: none;
    color: inherit;
    justify-content: space-between;
    align-items: flex-start;
    gap: 20px;
  }

  /* Chat Bot */
  .chat-bot {
    position: fixed;
    bottom: 30px;
    right: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .chat-bot img {
    width: 65px;
    height: 65px;
    cursor: pointer;
  }

  .chat-bubble {
    position: absolute;
    bottom: 70px;
    right: 20px;
    background-color: #fff;
    padding: 10px 20px;
    border-radius: 18px;
    width: 320px;
    max-width: 90vw;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    font-size: 14px;
    line-height: 1.4;
    z-index: 10;
    border: 1px solid #e0e0e0;
    text-align: left;
  }

  .close-bubble {
    position: absolute;
    top: 5px;
    right: 12px;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
    color: #aaa;
    line-height: 1;
  }

  .close-bubble:hover {
    color: #555;
  }

  .chat-bubble:after {
    content: '';
    position: absolute;
    bottom: -10px;
    right: 20px;
    width: 0;
    height: 0;
    border-left: 10px solid transparent;
    border-right: 10px solid transparent;
    border-top: 10px solid #fff;
  }

  /* Stories Overlay */
  .stories-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
    z-index: 2000;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .stories-slider {
    position: relative;
    width: 100%;
    max-width: 1200px;
    height: 90vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 20px;
  }
  
  .progress-bar {
    display: flex;
    gap: 5px;
    width: 400px;
    margin-bottom: 15px;
    z-index: 10;
  }
  
  .progress-segment {
    height: 3px;
    flex: 1;
    background-color: rgba(255, 255, 255, 0.3);
    border-radius: 3px;
  }
  
  .progress-segment.active {
    background-color: #1A3882;
  }
  
  .progress-segment.completed {
    background-color: #1A3882;
  }
  
  .close-stories {
    position: absolute;
    top: 10px;
    right: 20px;
    background: none;
    border: none;
    font-size: 30px;
    color: white;
    cursor: pointer;
    z-index: 10;
  }
  
  .stories-carousel {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 80vh;
    position: relative;
    gap: 20px;
  }
  
  .story-card {
    position: relative;
    border-radius: 20px;
    overflow: hidden;
    transition: all 0.3s ease;
    background-color: #E4E4E4;
    flex-shrink: 0;
  }
  
  .current-card {
    width: 400px;
    height: 90%;
    z-index: 5;
    padding: 20px;
    display: flex;
    flex-direction: column;
  }
  
  .prev-card, .next-card {
    height: 70%;
    width: 250px;
    z-index: 3;
    cursor: pointer;
  }
  
  .far-prev-card, .far-next-card {
    height: 60%;
    width: 200px;
    z-index: 1;
    cursor: pointer;
  }
  
  .prev-card, .far-prev-card, .next-card, .far-next-card {
    display: flex;
    flex-direction: column;
  }
  
  .card-content {
    padding: 15px;
    display: flex;
    flex-direction: column;
    height: 100%;
    position: relative;
    z-index: 1;
  }
  
  .card-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 2;
  }
  
  .far-prev-card .card-overlay, 
  .far-next-card .card-overlay {
    background-color: rgba(0, 0, 0, 0.7);
  }
  
  .story-title {
    font-size: 24px;
    margin-bottom: 20px;
    color: #333;
  }
  
  .story-image-container {
    width: 100%;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
    overflow: hidden;
    border-radius: 15px;
  }
  
  .story-image-container img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  
  .story-description {
    font-size: 16px;
    line-height: 1.5;
    color: #333;
    flex-grow: 1;
    overflow-y: auto;
  }
  
  .prev-card .story-description, 
  .next-card .story-description {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
  }
  
  .story-navigation {
    position: fixed;
    top: 50%;
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 0;
    transform: translateY(-50%);
    pointer-events: none;
    z-index: 10;
    left: 0;
    right: 0;
  }
  
  .story-nav-button {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.2);
    border: none;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    color: white;
    cursor: pointer;
    pointer-events: auto;
    margin: 0 20px;
  }
  
  .story-nav-button.prev {
    margin-left: 30px;
  }
  
  .story-nav-button.next {
    margin-right: 30px;
  }
  
  .story-nav-button:disabled {
    opacity: 0.3;
    cursor: not-allowed;
  }
  
  /* Chat Dialog */
  .chat-dialog-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 3000;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }
  
  .chat-dialog {
    width: 90%;
    max-width: 450px;
    height: 80vh;
    background-color: #f5f5f5;
    border-radius: 20px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    margin-right: 30px;
  }
  
  .chat-header {
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #ffffff;
  }
  
  .chat-header-left {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .chat-header-left h3 {
    margin: 0;
    font-size: 18px;
    font-weight: 600;
  }
  
  .chat-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  
  .chat-header-right {
    display: flex;
    align-items: center;
    gap: 15px;
  }
  
  .settings-button, .close-dialog {
    background: none;
    border: none;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #555;
  }
  
  .close-dialog {
    font-size: 24px;
    font-weight: bold;
    color: #999;
  }
  
  .chat-divider {
    height: 1px;
    background-color: #e0e0e0;
    width: 100%;
  }
  
  .chat-date {
    text-align: center;
    padding: 15px 0;
    color: #999;
    font-size: 16px;
  }
  
  .chat-messages {
    flex: 1;
    padding: 0 20px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  
  .message {
    max-width: 70%;
    border-radius: 18px;
    padding: 12px 15px;
    position: relative;
  }
  
  .message.bot {
    align-self: flex-start;
    background-color: #fff;
    border-top-left-radius: 0;
  }
  
  .message.user {
    align-self: flex-end;
    background-color: #e3f2fd;
    border-top-right-radius: 0;
  }
  
  .message-sender {
    font-weight: 600;
    margin-bottom: 5px;
    font-size: 14px;
  }
  
  .message-content {
    line-height: 1.4;
  }
  
  .chat-input {
    padding: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
    background-color: #fff;
    border-top: 1px solid #e0e0e0;
  }
  
  .chat-input input {
    flex: 1;
    padding: 10px 15px;
    border: none;
    border-radius: 30px;
    background-color: #f0f0f0;
    font-size: 16px;
    outline: none;
  }
  
  .voice-button, .send-button {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background: none;
    color: #999;
  }
  
  .send-button {
    color: #666;
  }

  @media (max-width: 768px) {
    .services-grid {
      grid-template-columns: 1fr;
    }
    
    .circular-buttons {
      gap: 10px;
    }
    
    .circular-button {
      margin: 0 5px;
    }
    
    .story-image {
      width: 70px;
      height: 70px;
    }
  }
</style>
