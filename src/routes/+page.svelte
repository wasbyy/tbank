<script lang="ts">
  import { onMount } from 'svelte';
  
  let avatar = '/account_photo.svg';
  let activeStory = 0;
  let showStory = false;
  
  function openStory(index: number) {
    activeStory = index;
    showStory = true;
  }
  
  function closeStory() {
    showStory = false;
  }
  
  function nextStory() {
    if (activeStory < stories.length - 1) {
      activeStory++;
    } else {
      activeStory = 0;
    }
  }
  
  function prevStory() {
    if (activeStory > 0) {
      activeStory--;
    } else {
      activeStory = stories.length - 1;
    }
  }
  
  let stories = [
    {
      id: 1,
      title: "Привет!",
      image: "/stories/story1.jpg",
      content: "Добро пожаловать в университет! Здесь ты найдешь множество возможностей для развития."
    },
    {
      id: 2,
      title: "Студенческая жизнь",
      image: "/stories/story2.jpg",
      content: "Участвуй в мероприятиях, находи друзей и развивайся вместе с нами!"
    },
    {
      id: 3,
      title: "Афиша",
      image: "/stories/story3.jpg",
      content: "Не пропусти интересные события в нашем университете!"
    }
  ];
  
  onMount(() => {
    // Initialization code if needed
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
    <a href="/account" class="profile-link">
      <div class="avatar">
        <img src={avatar} alt="Profile" />
      </div>
    </a>
  </div>

  <main>
    <h1 class="main-title">Твой ФФ - университет в одном клике.</h1>

    <!-- Main circular buttons -->
    <div class="circular-buttons">
      {#each stories as story, index}
        <div class="circular-button" on:click={() => openStory(index)}>
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
          <a href="/menu" class="card-link">
            <div class="service-icon">
              <img src="/main_page/cute shopping basket.svg" alt="Меню столовой" />
            </div>
            <h3>Меню столовой</h3>
          </a>
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
</div>

{#if showStory}
  <div class="stories-overlay">
    <div class="stories-slider">
      <div class="progress-bar">
        {#each stories as _, i}
          <div class="progress-segment {i === activeStory ? 'active' : i < activeStory ? 'completed' : ''}"></div>
        {/each}
      </div>
      
      <button class="close-stories" on:click={closeStory}>&times;</button>

      <div class="stories-carousel">
        {#if activeStory > 1}
          <div class="story-card far-prev-card" on:click={() => prevStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[activeStory - 2].title}</h2>
              <div class="story-image-container">
                <img src={stories[activeStory - 2].image} alt={stories[activeStory - 2].title} />
              </div>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}

        {#if activeStory > 0}
          <div class="story-card prev-card" on:click={() => prevStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[activeStory - 1].title}</h2>
              <div class="story-image-container">
                <img src={stories[activeStory - 1].image} alt={stories[activeStory - 1].title} />
              </div>
              <p class="story-description">{stories[activeStory - 1].content}</p>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}
        
        <div class="story-card current-card">
          <h2 class="story-title">{stories[activeStory].title}</h2>
          <div class="story-image-container">
            <img src={stories[activeStory].image} alt={stories[activeStory].title} />
          </div>
          <p class="story-description">{stories[activeStory].content}</p>
        </div>
        
        {#if activeStory < stories.length - 1}
          <div class="story-card next-card" on:click={() => nextStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[activeStory + 1].title}</h2>
              <div class="story-image-container">
                <img src={stories[activeStory + 1].image} alt={stories[activeStory + 1].title} />
              </div>
              <p class="story-description">{stories[activeStory + 1].content}</p>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}

        {#if activeStory < stories.length - 2}
          <div class="story-card far-next-card" on:click={() => nextStory()}>
            <div class="card-content">
              <h2 class="story-title">{stories[activeStory + 2].title}</h2>
              <div class="story-image-container">
                <img src={stories[activeStory + 2].image} alt={stories[activeStory + 2].title} />
              </div>
            </div>
            <div class="card-overlay"></div>
          </div>
        {/if}
      </div>
      
      <div class="story-navigation">
        <button class="story-nav-button prev" on:click={prevStory} disabled={activeStory === 0}>
          <span>❮</span>
        </button>
        <button class="story-nav-button next" on:click={nextStory} disabled={activeStory === stories.length - 1}>
          <span>❯</span>
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
    z-index: 100;
  }
  
  .profile-link {
    display: block;
    text-decoration: none;
  }
  
  .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
  
  .avatar img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    object-fit: cover;
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
